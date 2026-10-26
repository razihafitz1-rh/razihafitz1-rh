# 🧪 Rangkuman Nmap (Network Mapper)

> Catatan ringkas untuk latihan Home Lab — konsep inti, flag penting, port state, NSE, dan contoh perintah.
> Referensi resmi: [nmap.org/book](https://nmap.org/book/) · Daftar opsi: [nmap.org/book/man.html](https://nmap.org/book/man.html)

---

## 1. Apa itu Nmap

**Nmap = Network Mapper**, tool open-source (lisensi NPSL/GPL) untuk memetakan jaringan. Fungsi utamanya:

| Kemampuan | Arti singkat | Opsi khas |
|---|---|---|
| Host discovery | Cari host yang hidup | `-sn`, `-Pn` |
| Port scanning | Cek port terbuka/tertutup | `-sS`, `-sT`, `-sU` |
| Service/version detection | Tebak aplikasi + versi | `-sV` |
| OS detection | Tebak sistem operasi | `-O` |
| Scripting (NSE) | Otomasi cek lanjutan | `-sC`, `--script` |
| Traceroute | Peta jalur ke target | `--traceroute` |

Nmap mengirim paket khusus lalu membaca balasan (SYN/ACK, RST, ICMP error) untuk menyimpulkan status target. **Bukan** alat eksploitasi — Nmap memetakan, script NSE hanya membantu *mendeteksi* kerentanan.

---

## 2. Instalasi

```bash
# Debian / Ubuntu / Kali
sudo apt update && sudo apt install nmap

# Fedora / RHEL
sudo dnf install nmap

# macOS
brew install nmap

# Windows: installer dari nmap.org/download (sertakan Npcap)
```

Cek versi: `nmap --version` · Bantuan: `nmap -h` atau `man nmap`

---

## 3. Alur kerja standar

```
1. Tentukan target & pastikan IZIN
2. Host discovery        → nmap -sn 192.168.56.0/24
3. Port scan             → nmap -sS --open -T4 192.168.56.10
4. Service detection     → nmap -sV -p 22,80,443 192.168.56.10
5. OS detection (opsional) → sudo nmap -O 192.168.56.10
6. Script relevan        → nmap --script "http-*" -p 80 192.168.56.10
7. Simpan hasil          → nmap -oA hasil_scan <target>
```

Semakin banyak tahap diaktifkan, semakin **lambat** dan semakin **"berisik"** di log/IDS.

---

## 4. Flag penting

### Pemilihan target & host discovery

| Flag | Fungsi |
|---|---|
| `192.168.1.0/24` | Satu subnet (CIDR) |
| `192.168.1.1-20` | Rentang IP |
| `-iL targets.txt` | Daftar target dari file |
| `--exclude 192.168.1.1` | Kecualikan host |
| `-sn` | Host discovery saja, tanpa scan port |
| `-Pn` | Anggap semua target hidup (lewati ping) |
| `-n` / `-R` | Tanpa DNS resolve / paksa resolve |

### Tipe scan port

| Flag | Fungsi | Butuh root? |
|---|---|---|
| `-sS` | TCP SYN / half-open (default bila root) | Ya |
| `-sT` | TCP connect (pakai `connect()` OS) | Tidak |
| `-sU` | UDP scan (lambat, sering `open\|filtered`) | Ya |
| `-sA` | ACK scan — memetakan aturan firewall | Ya |
| `-sN` / `-sF` / `-sX` | Null / FIN / Xmas scan | Ya |
| `-sI` | Idle (zombie) scan | Ya |
| `-sL` | List scan — hanya daftar target, tak kirim paket | Tidak |

### Pemilihan port

| Flag | Arti |
|---|---|
| *(tanpa flag)* | 1000 port TCP terpopuler (`--top-ports 1000`) |
| `-p-` | Semua 65535 port |
| `-p 22,80,443` | Port tertentu |
| `-p 8000-8100` | Rentang port |
| `-p T:80,U:53` | Bedakan TCP/UDP |
| `--top-ports 100` | N port terpopuler |
| `-F` | Fast scan (100 port) |
| `--open` | Tampilkan hanya port terbuka |
| `--reason` | Tampilkan alasan state port |

### Deteksi & timing

| Flag | Fungsi |
|---|---|
| `-sV` | Deteksi versi layanan (`--version-intensity 0-9`) |
| `-O` | Deteksi OS (`--osscan-guess` untuk tebakan agresif) |
| `-A` | Gabungan: `-O -sV -sC --traceroute` |
| `-T0`…`-T5` | Timing template: paranoid → insane |
| `--min-rate 500` | Minimal 500 paket/detik |
| `--max-retries 1` | Kurangi retry agar lebih cepat |
| `--host-timeout 30s` | Batas waktu per host |
| `-f` | Fragmentasi paket (evasion) |
| `-D RND:5` | Decoy 5 IP acak (evasion) |

---

## 5. Port state — wajib hafal

| State | Arti | Penyebab umum |
|---|---|---|
| `open` | Ada layanan menerima koneksi | Balasan SYN/ACK (TCP) / respons app (UDP) |
| `closed` | Host hidup, tak ada listener | Balasan RST (TCP) / ICMP port unreachable (UDP) |
| `filtered` | Tidak bisa dipastikan | Paket dibuang firewall / ICMP admin-prohibited |
| `unfiltered` | Bisa dijangkau, status belum tahu | Khas ACK scan (balasan RST) |
| `open\|filtered` | Tak ada balasan sama sekali | Umum pada UDP |
| `closed\|filtered` | Tak ada balasan | Biasanya pada IP ID scan |

Contoh output:

```
PORT     STATE    SERVICE   VERSION
22/tcp   open     ssh       OpenSSH 8.9p1 Ubuntu 3ubuntu0.4
80/tcp   open     http      nginx 1.18.0 (Ubuntu)
3306/tcp filtered mysql
```

Baca cepat: **open** = bisa diakses · **closed** = host hidup tanpa layanan · **filtered** = ada penghalang.

---

## 6. Timing template

| Template | Karakter | Cocok untuk |
|---|---|---|
| `-T0` paranoid | Sangat lambat, 1 port per 5 menit | Menghindari IDS (uji sangat hati-hati) |
| `-T1` sneaky | Lambat | Link rapuh |
| `-T2` polite | Lebih lambat dari normal | Jaringan produksi |
| `-T3` normal | Default | Umum |
| `-T4` aggressive | Cepat | LAN stabil / lab |
| `-T5` insane | Sangat agresif | Hanya lab terisolasi (bisa bikin device down) |

---

## 7. Format output

| Flag | Hasil |
|---|---|
| `-oN file.txt` | Teks normal (seperti tampilan terminal) |
| `-oX file.xml` | XML — mudah di-parse tool lain |
| `-oG file.gnmap` | Grepable (warisan, masih dipakai untuk `grep`) |
| `-oS file.txt` | "Script kiddie" (iseng) |
| `-oA nama` | Ketiganya sekaligus: `.nmap`, `.xml`, `.gnmap` |
| `-v` / `-vv` | Verbose / lebih verbose |
| `--stats-every 10s` | Progress berkala |

---

## 8. NSE (Nmap Scripting Engine)

- Ditulis dengan **Lua**, tersimpan di `/usr/share/nmap/scripts` (Linux) atau `C:\Program Files (x86)\Nmap\scripts` (Windows).
- Update database: `sudo nmap --script-updatedb`
- Lihat script: `ls /usr/share/nmap/scripts | grep http`

```bash
nmap -sC -sV target                       # script default (aman, informatif)
nmap --script vuln target                 # kategori deteksi kerentanan
nmap --script "http-*" -p 80 target       # wildcard kategori/nama
nmap --script http-headers,http-title -p 80 target
nmap --script-help "smb-*"                # bantuan script
nmap --script brute --script-args user=admin,pass=123456 target
```

Kategori umum: `default`, `safe`, `discovery`, `version`, `auth`, `vuln`, `brute`, `exploit`, `malware`, `intrusive`.
Ingat: `vuln`, `brute`, dan `intrusive` bisa memicu crash atau alarm — hanya untuk lab.

---

## 9. Contoh perintah siap pakai (lab)

```bash
# 1) Inventaris host di subnet
nmap -sn 192.168.56.0/24

# 2) Port terbuka + versi layanan, cepat
sudo nmap -sS -sV --open -T4 192.168.56.10

# 3) Semua port (65535) dengan rate terkendali
sudo nmap -sS -p- --min-rate 1000 192.168.56.10

# 4) Profil lengkap satu host
sudo nmap -A -p- -oA hasil_lengkap 192.168.56.10

# 5) Cek service web + header + metode HTTP
nmap -sV -p 80,443 --script "http-headers,http-methods,http-title" 192.168.56.10

# 6) UDP umum (DNS, NTP, SNMP)
sudo nmap -sU -p 53,123,161 192.168.56.10

# 7) Scan via IPv6
nmap -6 fe80::20c:29ff:fe1a:2b3c

# 8) Target dari file + simpan 3 format
nmap -iL targets.txt -sV -oA audit_jaringan
```

---

## 10. Tips & kesalahan umum

- **Tidak butuh root** untuk `-sT`, `-sn`, `-sL`; scan raw packet (`-sS`, `-sU`, `-O`, `-sA`) butuh privilege.
- `-Pn` dipakai kalau target **memblokir ping** — tapi scan jadi lebih lama.
- Hasil `filtered` bukan berarti port tertutup; bisa jadi firewall membuang paket.
- `-O` sering memberi beberapa kandidat OS — anggap **estimasi**, bukan kepastian.
- `-p-` tanpa `--min-rate`/`-T4` bisa sangat lama; kombinasikan dengan bijak.
- Simpan hasil dengan `-oA` supaya bisa dibandingkan antar waktu.
- Untuk scan berulang, simpan target di file (`-iL`) agar rapi.
- Bandingkan baseline: scan rutin → temukan port baru tak terduga → indikasi perubahan konfigurasi/malware.

---

## 11. Etika & legalitas

> ⚠️ **Scan hanya perangkat/jaringan milik sendiri atau yang punya izin tertulis.**
> Scanning tanpa izin dapat melanggar hukum (mis. UU ITE) dan ToS penyedia layanan, walaupun hanya "membaca".

- Latihan legal: VM di host-only/VLAN terisolasi, atau target resmi `scanme.nmap.org`.
- Di jaringan produksi: pakai `-T2`/`-T3`, hindari `--script vuln`/`brute`, jadwalkan di luar jam sibuk.
- Dokumentasikan target, waktu, dan opsi yang dipakai.

---

## 12. Referensi

- Buku resmi: <https://nmap.org/book/>
- Manual lengkap: <https://nmap.org/book/man.html>
- Portal NSE: <https://nmap.org/nsedoc/>
- Target latihan: <https://scanme.nmap.org/>
- Cheat sheet komunitas: <https://nmap.org/book/man-briefoptions.html>

---

<div align="center">

**Keep tinkering · stay curious** ⚡ `razihafitz1-rh`

</div>
