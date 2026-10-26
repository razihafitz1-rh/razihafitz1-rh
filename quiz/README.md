# 🧪 Nmap Quiz — Home Lab Nexus

Paket latihan **Nmap (Network Mapper)** berbahasa Indonesia, dibuat untuk latihan mandiri di Home Lab.

| File | Isi | Cara pakai |
|---|---|---|
| [`nmap-quiz.html`](./nmap-quiz.html) | Quiz interaktif 25 soal (single-file, tanpa dependency) | Buka langsung di browser — double-click, atau `xdg-open nmap-quiz.html` |
| [`nmap-quiz.md`](./nmap-quiz.md) | Bank soal + kunci + pembahasan + 5 esai + cheat sheet | Baca di GitHub / editor markdown mana pun |

## Fitur quiz interaktif

- 25 soal: **20 pilihan ganda + 5 benar/salah**, diacak setiap sesi.
- Opsi jawaban ikut diacak (kunci tidak selalu di posisi A).
- Pembahasan langsung muncul setelah menjawab.
- Skor otomatis `+4` per jawaban benar (maks. **100**) + grade akhir.
- Halaman review berisi jawabanmu vs kunci dan alasannya.
- Keyboard: `Enter` untuk lanjut ke soal berikutnya.

## Cakupan materi

Host discovery · port scanning (`-sS`, `-sT`, `-sU`, `-sA`) · service/version detection · OS detection · port state (`open`, `closed`, `filtered`, `open|filtered`) · NSE · timing template · output format · evasion dasar · etika & legalitas.

## Target penilaian

| Skor | Grade |
|---|---|
| ≥ 92 | 🏆 Nmap Master |
| 80–91 | 🛡️ Solid — siap lanjut NSE |
| 60–79 | 📚 Cukup — ulangi port & state |
| < 60 | 🔁 Perlu ulang — baca nmap.org/book |

## Etika

> Gunakan Nmap hanya pada perangkat/jaringan milik sendiri atau yang memiliki izin tertulis.
> Untuk latihan legal, gunakan lab terisolasi (VM/VLAN) atau target resmi `scanme.nmap.org`.

Referensi: <https://nmap.org/book/> · <https://nmap.org/nsedoc/>

---

Keep tinkering · stay curious ⚡ `razihafitz1-rh`
