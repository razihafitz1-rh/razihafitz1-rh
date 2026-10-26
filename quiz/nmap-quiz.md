# 🧪 NMAP QUIZ — Bank Soal, Kunci Jawaban & Pembahasan

> Kuis pemahaman **Nmap (Network Mapper)** untuk latihan Home Lab.
> Referensi utama: dokumentasi resmi [nmap.org/book](https://nmap.org/book/).

| Info | Detail |
|---|---|
| Jumlah soal | **25** (20 pilihan ganda + 5 benar/salah) |
| Skor maksimal | **100** (4 poin per jawaban benar) |
| Versi interaktif | [`nmap-quiz.html`](./nmap-quiz.html) — buka langsung di browser |
| Tingkat | Pemula → menengah (flag, port state, NSE, etika) |

**Cara pakai**

- Versi interaktif: buka `nmap-quiz.html`, soal & opsi otomatis diacak, pembahasan muncul setelah menjawab.
- Versi markdown: kerjakan dulu tanpa melihat **Bagian C**, baru cocokkan dengan kunci.
- Target lulus: **≥ 80 poin**. Di bawah 60 → ulangi materi port scanning & port state.

---

## Bagian A — Pilihan Ganda (20 soal, 4 poin each)

**1.** Nmap adalah singkatan dari ...

- A. Network Management Application Protocol
- B. Network Mapper
- C. Node Mapping
- D. Nmap Network Analyzer

**2.** Opsi yang **hanya** melakukan host discovery tanpa scan port adalah ...

- A. `-Pn`
- B. `-sV`
- C. `-sn`
- D. `-p-`

**3.** Apa arti opsi `-sS` pada Nmap?

- A. TCP SYN scan (half-open scan)
- B. TCP connect scan
- C. UDP scan
- D. ACK scan untuk memetakan firewall

**4.** Apa perbedaan utama `-sT` dibanding `-sS`?

- A. `-sT` mengirim paket UDP, sedangkan `-sS` mengirim TCP
- B. `-sT` menyelesaikan TCP handshake penuh lewat `connect()` sistem operasi, jadi lebih mudah tercatat di log aplikasi
- C. `-sT` hanya bisa dipakai pada alamat IPv6
- D. `-sT` tidak bisa mendeteksi port tertutup

**5.** Opsi `-sV` digunakan untuk ...

- A. Menampilkan versi Nmap yang terpasang
- B. Memindai versi kernel target
- C. Mengaktifkan mode verbose
- D. Mendeteksi versi layanan yang berjalan di port terbuka

**6.** Opsi `-O` pada Nmap berfungsi untuk ...

- A. Membuka port secara paksa
- B. Mendeteksi sistem operasi target lewat analisis fingerprint TCP/IP
- C. Menampilkan output dalam format XML
- D. Mempercepat scan dengan banyak thread

**7.** Perintah `nmap -p- 192.168.1.10` akan memindai ...

- A. Seluruh 65535 port TCP
- B. Hanya 1000 port terpopuler
- C. Hanya port 1 sampai 100
- D. Port UDP saja

**8.** Perintah `nmap -p 22,80,443,8000-8100 target` berarti ...

- A. Memindai port 22 sampai 8100 secara berurutan
- B. Memindai 4 port saja yaitu 22, 80, 443, dan 8000
- C. Memindai port 22, 80, 443, dan seluruh port 8000 sampai 8100
- D. Memindai port 8000–8100 dengan 4 percobaan

**9.** Jika hanya menjalankan `nmap target` tanpa opsi port, Nmap memindai ...

- A. Seluruh 65535 port
- B. 1000 port TCP yang paling umum digunakan
- C. Hanya port 80 dan 443
- D. Port yang tertulis di `/etc/services` saja

**10.** State `filtered` pada hasil scan berarti ...

- A. Port terbuka dan menerima koneksi
- B. Port tertutup tetapi host aktif
- C. Host tujuan tidak pernah merespons sama sekali
- D. Nmap tidak bisa memastikan port terbuka atau tertutup karena paket diblokir/difilter (mis. firewall)

**11.** Pada TCP scan, state `closed` menunjukkan bahwa ...

- A. Host aktif dan mengirim balasan RST, tetapi tidak ada layanan yang mendengarkan di port itu
- B. Port terbuka dan siap menerima koneksi
- C. Firewall membuang paket tanpa balasan
- D. Host tujuan mati total

**12.** NSE adalah singkatan dari ...

- A. Network Security Enumeration
- B. Nmap Service Extension
- C. Nmap Scripting Engine
- D. Node Scanning Engine

**13.** Perintah `nmap --script vuln target` akan ...

- A. Mengunci target agar tidak bisa diakses
- B. Menjalankan semua script NSE kategori `vuln` untuk mencari kerentanan umum
- C. Memindai seluruh 65535 port terlebih dahulu
- D. Mengaktifkan mode verbose pada Nmap

**14.** Opsi `-T4` pada Nmap berarti ...

- A. Melakukan 4 kali percobaan ulang setiap port
- B. Memindai 4 port sekaligus
- C. Menunggu 4 detik di antara paket
- D. Menggunakan timing template *aggressive* yang lebih cepat, cocok untuk jaringan lokal yang stabil

**15.** Opsi `-Pn` berguna ketika ...

- A. Host target memblokir ping, sehingga Nmap melewati host discovery dan menganggap semua target hidup
- B. Kita ingin memindai port UDP saja
- C. Kita ingin menyembunyikan alamat IP sumber
- D. Kita ingin menampilkan alasan state port

**16.** Opsi untuk menyimpan hasil scan dalam format XML adalah ...

- A. `-oN`
- B. `-oG`
- C. `-oX`
- D. `-oS`

**17.** Opsi `-oA hasil_scan` akan menghasilkan ...

- A. Satu file HTML berisi laporan lengkap
- B. Tiga file sekaligus: `.nmap` (normal), `.xml`, dan `.gnmap` (grepable)
- C. File konfigurasi Nmap yang bisa dipakai ulang
- D. Arsip ZIP berisi seluruh screenshot scan

**18.** Apa fungsi ACK scan (`-sA`)?

- A. Menemukan port terbuka lebih cepat daripada SYN scan
- B. Mendeteksi versi layanan secara akurat
- C. Melakukan scan pada protokol selain TCP dan UDP
- D. Memetakan aturan firewall (mana port yang difilter), bukan menentukan port terbuka

**19.** Opsi `-D RND:5` pada Nmap digunakan untuk ...

- A. Menggunakan 5 alamat IP decoy agar scan tampak berasal dari banyak sumber
- B. Membatasi scan hanya 5 host
- C. Mengulang scan maksimal 5 kali
- D. Mengenkripsi paket scan

**20.** Opsi `-A` (*aggressive scan*) setara dengan menggabungkan ...

- A. Hanya `-p-` dan `-T5`
- B. Hanya UDP scan dan ACK scan
- C. OS detection, version detection, script default, dan traceroute
- D. Hanya host discovery dan output XML

---

## Bagian B — Benar / Salah (5 soal, 4 poin each)

**B1.** Nmap boleh digunakan untuk memindai jaringan publik mana pun tanpa izin, karena hanya membaca informasi.
→ **Benar / Salah**

**B2.** SYN scan tidak menyelesaikan TCP handshake sehingga lebih jarang tercatat di log aplikasi — tetapi tetap dapat terlihat oleh firewall atau IDS.
→ **Benar / Salah**

**B3.** Scan UDP umumnya lebih lambat dan hasilnya kurang pasti dibandingkan scan TCP.
→ **Benar / Salah**

**B4.** Opsi `-sT` selalu membutuhkan hak akses root.
→ **Benar / Salah**

**B5.** Hasil OS detection Nmap selalu 100% akurat dan tidak pernah salah.
→ **Benar / Salah**

---

## Bagian C — Kunci Jawaban Cepat

> ⚠️ Jangan buka bagian ini sebelum mengerjakan.

| No | Kunci | No | Kunci | No | Kunci |
|:--:|:--:|:--:|:--:|:--:|:--:|
| 1 | B | 8 | C | 15 | A |
| 2 | C | 9 | B | 16 | C |
| 3 | A | 10 | D | 17 | B |
| 4 | B | 11 | A | 18 | D |
| 5 | D | 12 | C | 19 | A |
| 6 | B | 13 | B | 20 | C |
| 7 | A | 14 | D | | |

| No | Kunci |
|:--:|:--:|
| B1 | Salah |
| B2 | Benar |
| B3 | Benar |
| B4 | Salah |
| B5 | Salah |

---

## Bagian D — Pembahasan Lengkap

### Pilihan Ganda

**1. B — Network Mapper.**
Nmap adalah tool open-source untuk pemetaan jaringan: host discovery, port scanning, deteksi service/OS, dan otomasi lewat NSE. Bukan protokol atau aplikasi manajemen.

**2. C — `-sn`.**
`-sn` (dahulu `-sP`) hanya memeriksa host hidup tanpa scan port. Ingat: `-Pn` justru **mematikan** host discovery, `-sV` deteksi versi, `-p-` scan semua port.

**3. A — TCP SYN scan.**
Nmap mengirim SYN; bila dibalas SYN/ACK berarti port terbuka, lalu Nmap mengirim RST sehingga handshake tidak pernah selesai. Cepat dan relatif tidak mencolok, tetapi butuh root/raw socket.

**4. B — `-sT` memakai `connect()` OS.**
Karena handshake TCP diselesaikan penuh, koneksi tercatat di log aplikasi. Kelebihannya: bisa dijalankan user biasa. `-sS` lebih senyap tetapi butuh privilege.

**5. D — versi layanan.**
`-sV` mengirim probe ke port terbuka dan mencocokkan respons dengan database `nmap-service-probes`, menampilkan produk + versi (mis. `nginx 1.18.0`).

**6. B — OS fingerprinting.**
`-O` menganalisis karakteristik stack TCP/IP (TTL, window size, opsi TCP, perilaku ICMP). Hasilnya bisa beberapa kandidat dan bisa keliru bila ada firewall/NAT.

**7. A — seluruh 65535 port.**
`-p-` = `-p 1-65535`. Scan ini jauh lebih lama; gunakan `--min-rate` atau `-T4` bila perlu, dan pastikan punya izin.

**8. C — daftar + rentang.**
Nmap menerima campuran port tunggal dan rentang dipisah koma. `8000-8100` berarti 101 port (bukan 4).

**9. B — 1000 port teratas.**
Default sama dengan `--top-ports 1000` berdasarkan `nmap-services`. Untuk semua port gunakan `-p-` atau `-p 0-65535`.

**10. D — tidak bisa dipastikan.**
`filtered` muncul saat paket dibuang firewall, diblokir, atau dibalas ICMP error. Beda dengan `closed` (dibalas RST) dan `open` (ada layanan).

**11. A — host aktif, port tanpa listener.**
Balasan RST menandakan port tertutup tetapi host hidup. Kalau host mati atau paket dibuang, hasilnya biasanya `filtered` atau host tidak muncul.

**12. C — Nmap Scripting Engine.**
NSE menjalankan script Lua dari `/usr/share/nmap/scripts` (Linux) untuk enumerasi, deteksi kerentanan, brute force, dan audit konfigurasi.

**13. B — kategori `vuln`.**
`--script vuln` menjalankan semua script berkategori `vuln`. Untuk script spesifik: `--script http-shellshock`. Script default: `-sC` atau `--script default`.

**14. D — timing template aggressive.**
Template: `-T0` paranoid, `-T1` sneaky, `-T2` polite, `-T3` normal (default), `-T4` aggressive, `-T5` insane. `-T4` umum di LAN stabil.

**15. A — melewati host discovery.**
`-Pn` (no ping) menganggap semua target hidup. Dipakai saat target memblokir ICMP; konsekuensinya scan lebih lama karena tidak ada host yang dilewati.

**16. C — `-oX`.**
`-oX file.xml` untuk XML (mudah di-parse), `-oN` normal, `-oG` grepable, `-oS` "script kiddie" (format iseng).

**17. B — tiga format sekaligus.**
`-oA nama` menghasilkan `nama.nmap`, `nama.xml`, dan `nama.gnmap`. Praktis untuk dokumentasi lab atau diolah tool lain (mis. Nmap XML → laporan).

**18. D — memetakan firewall.**
ACK scan mengirim paket ACK: balasan RST = `unfiltered`, tanpa balasan = `filtered`. Hasilnya **tidak** menunjukkan open/closed, hanya aturan filtering.

**19. A — decoy.**
`-D RND:5` menambahkan 5 IP acak sebagai pengirim palsu. Ini teknik evasion untuk pengujian sah, bukan jaminan anonimitas, dan bisa mengganggu host lain.

**20. C — gabungan fitur.**
`-A` = `-O -sV -sC --traceroute`. Sangat informatif tetapi lebih lambat dan lebih "berisik", jadi jangan dipakai sembarangan.

### Benar / Salah

**B1. Salah.**
Memindai jaringan tanpa izin dapat melanggar hukum (mis. UU ITE di Indonesia) dan ToS penyedia jaringan. Batasi ke lab sendiri, `scanme.nmap.org`, atau target dengan izin tertulis.

**B2. Benar.**
Karena sesi tidak pernah penuh, aplikasi biasanya tidak mencatat login/koneksi; namun paket SYN tetap terekam oleh firewall, IDS/IPS, atau NetFlow.

**B3. Benar.**
UDP tidak punya handshake. Nmap harus menunggu timeout dan menyimpulkan dari ICMP port unreachable, sehingga lebih lambat dan lebih ambigu (sering muncul `open|filtered`).

**B4. Salah.**
`-sT` memakai `connect()` milik OS sehingga bisa dijalankan user biasa. Yang butuh root: `-sS`, `-sU`, `-sA`, `-O`, dan opsi raw packet lain.

**B5. Salah.**
OS detection adalah estimasi berbasis fingerprint. Firewall, NAT, virtualisasi, dan service yang meniru stack lain dapat membuat hasil meleset.

---

## Bagian E — Soal Esai (untuk latihan mandiri)

**E1.** Jelaskan perbedaan lima kemampuan inti Nmap: host discovery, port scanning, service/version detection, OS detection, dan NSE.

<details><summary>Lihat jawaban model</summary>

1. **Host discovery** — menentukan host mana yang hidup (`-sn`, ARP/ICMP/TCP ping).
2. **Port scanning** — menentukan status port pada host hidup (`-sS`, `-sT`, `-sU`).
3. **Service/version detection** — menebak aplikasi & versi di port terbuka (`-sV`).
4. **OS detection** — menebak sistem operasi via fingerprint stack TCP/IP (`-O`).
5. **NSE** — menjalankan script Lua untuk enumerasi, deteksi kerentanan, brute force, dan audit (`-sC`, `--script`).

Alur logisnya: temukan host → temukan port → kenali layanan → kenali OS → jalankan script yang relevan.

</details>

**E2.** Kapan sebaiknya memakai `-sS` dan kapan `-sT`? Kaitkan dengan hak akses dan tingkat "kebisingan".

<details><summary>Lihat jawaban model</summary>

- `-sS` (SYN/half-open): butuh root/raw socket, lebih cepat, tidak menyelesaikan handshake sehingga jarang tercatat di log aplikasi. Default Nmap bila dijalankan sebagai root.
- `-sT` (connect): tidak butuh root, memakai `connect()` OS, menyelesaikan handshake penuh sehingga mudah terlihat di log aplikasi dan firewall.
- Pilih `-sT` bila tidak punya privilege atau butuh kompatibilitas; pilih `-sS` bila butuh kecepatan pada pengujian yang sah. Keduanya **tetap terdeteksi** IDS.

</details>

**E3.** Jelaskan arti state `open`, `closed`, `filtered`, dan `open|filtered`, serta penyebab utamanya.

<details><summary>Lihat jawaban model</summary>

- `open` — ada aplikasi yang listen; Nmap menerima SYN/ACK (TCP) atau respons aplikasi (UDP).
- `closed` — host hidup tetapi tidak ada listener; dibalas RST (TCP) atau ICMP port unreachable (UDP).
- `filtered` — paket dibuang/diblokir firewall, atau dibalas ICMP admin-prohibited; status tidak dapat dipastikan.
- `open|filtered` — Nmap tidak menerima balasan apa pun (umum pada UDP), sehingga tidak bisa membedakan terbuka atau tersaring.

</details>

**E4.** Tuliskan rangkaian perintah untuk mengaudit satu host di lab: temukan host, cari port terbuka, deteksi versi, cek kerentanan, lalu simpan hasil ke tiga format.

<details><summary>Lihat jawaban model</summary>

```bash
# 1) pastikan host hidup
nmap -sn 192.168.56.10

# 2) port terbuka + versi layanan (cepat)
sudo nmap -sS -sV --open -T4 192.168.56.10

# 3) semua port jika perlu
sudo nmap -sS -p- --min-rate 1000 192.168.56.10

# 4) pemeriksaan kerentanan (hati-hati, hanya di lab)
sudo nmap -sV --script vuln 192.168.56.10

# 5) simpan ketiga format output
sudo nmap -A -oA hasil_audit 192.168.56.10
```

</details>

**E5.** Mengapa izin tertulis penting sebelum scanning, dan apa risikonya memakai `-T5`, `--script vuln`, atau `-D` di jaringan produksi?

<details><summary>Lihat jawaban model</summary>

- Scanning tanpa izin dapat melanggar hukum (mis. UU ITE) dan kebijakan penyedia layanan, meski hanya "membaca".
- `-T5`/`--min-rate` tinggi dapat membanjiri perangkat lemah (switch, printer, IoT) hingga down.
- `--script vuln` dapat memicu crash pada layanan rentan atau memicu alarm IDS/IPS.
- `-D` (decoy) mengirim trafik dari IP palsu sehingga bisa menyeret pihak lain dalam log dan menyulitkan investigasi.
- Praktik aman: izin tertulis, jadwal maintenance, timing konservatif (`-T2`/`-T3`), dan dokumentasi target.

</details>

---

## Bagian F — Cheat Sheet Flag Nmap

| Flag | Fungsi | Contoh |
|---|---|---|
| `-sn` | Host discovery saja | `nmap -sn 192.168.1.0/24` |
| `-Pn` | Anggap semua host hidup (skip ping) | `nmap -Pn 10.0.0.5` |
| `-sS` | TCP SYN (half-open) scan | `sudo nmap -sS 10.0.0.5` |
| `-sT` | TCP connect scan | `nmap -sT 10.0.0.5` |
| `-sU` | UDP scan | `sudo nmap -sU -p 53,123 10.0.0.5` |
| `-sA` | ACK scan (petakan firewall) | `sudo nmap -sA 10.0.0.5` |
| `-sV` | Deteksi versi layanan | `nmap -sV 10.0.0.5` |
| `-O` | Deteksi OS | `sudo nmap -O 10.0.0.5` |
| `-A` | Aggressive (`-O -sV -sC --traceroute`) | `sudo nmap -A 10.0.0.5` |
| `-p-` | Semua 65535 port | `nmap -p- 10.0.0.5` |
| `-p 22,80,443,8000-8100` | Port tertentu + rentang | `nmap -p 22,80,443,8000-8100 10.0.0.5` |
| `--top-ports 100` | N port terpopuler | `nmap --top-ports 100 10.0.0.5` |
| `--open` | Tampilkan hanya port terbuka | `nmap --open 10.0.0.5` |
| `-sC` | Script default NSE | `nmap -sC -sV 10.0.0.5` |
| `--script vuln` | Script kategori kerentanan | `nmap --script vuln 10.0.0.5` |
| `--script-help` | Bantuan script | `nmap --script-help "http-*"` |
| `-T0` … `-T5` | Timing template | `nmap -T4 10.0.0.5` |
| `--min-rate 500` | Minimal 500 paket/detik | `nmap --min-rate 500 -p- 10.0.0.5` |
| `-f` | Fragmentasi paket | `sudo nmap -f 10.0.0.5` |
| `-D RND:5` | Decoy IP acak | `sudo nmap -D RND:5 10.0.0.5` |
| `-6` | Scan target IPv6 | `nmap -6 fe80::1` |
| `-oN` / `-oX` / `-oG` / `-oA` | Format output | `nmap -oA hasil 10.0.0.5` |
| `-v` / `-vv` | Verbose | `nmap -vv 10.0.0.5` |
| `--reason` | Alasan state port | `nmap --reason 10.0.0.5` |

### Port state yang perlu dihafal

| State | Arti |
|---|---|
| `open` | Ada layanan yang menerima koneksi |
| `closed` | Host hidup, tidak ada listener (dibalas RST) |
| `filtered` | Diblokir firewall/IDS, status tak pasti |
| `unfiltered` | Bisa dijangkau, status open/closed belum diketahui (khas ACK scan) |
| `open\|filtered` | Tidak ada balasan — umum pada UDP |
| `closed\|filtered` | Tidak ada balasan, biasanya pada IP ID scan |

---

## Etika & Referensi

> ⚠️ **Gunakan Nmap hanya pada perangkat dan jaringan yang kamu miliki atau punya izin tertulis.** Untuk latihan legal gunakan lab pribadi (VM/VLAN terisolasi) atau target resmi seperti `scanme.nmap.org`.

- Buku resmi: <https://nmap.org/book/>
- Referensi opsi: <https://nmap.org/book/man.html>
- Portal NSE: <https://nmap.org/nsedoc/>
- Target latihan resmi: <https://scanme.nmap.org/>

---

<div align="center">

**Keep tinkering · stay curious** ⚡ `razihafitz1-rh`

</div>
