# 🧹 bersihkan

Hapus `node_modules`, `.next`, `dist`, `build`, cache Laravel, dan artefak framework lainnya secara **rekursif** — bisa dipanggil dari mana pun.

> Support: **Next.js / React / Nuxt / Vite / Astro / Laravel / Go / Rust / Java / Flutter / Terraform / Python** dan umum. Aman, ada `--dry-run` + live spinner.

![disk full](disk-full.png)

## ✨ Fitur

- 🔁 **Rekursif** — scan semua subfolder dari posisi kamu berdiri
- 👀 **Aman** — konfirmasi sebelum hapus + mode `--dry-run`
- 🔍 **Live spinner** — tampil folder yang sedang di-scan + jumlah found (tidak kelihatan hang)
- 📊 **Hitung ukuran** — tampil total yang dibebaskan
- 📂 **Sort** — `name` (A-Z, cepat) atau `size` (terbesar dulu)
- 🚫 **Exclude** — `-e` / `--exclude` untuk kecualikan folder/file/ekstensi
- 🌍 **Global command** — install sekali, pakai di mana pun
- ⚡ **Cepat** — `find` single-pass + `-prune` `.git`, compatible `bash 3.2` (macOS)

## 📦 Yang Dibersihkan

| Kategori | Target |
|----------|--------|
| **JS/Node/React/Next/Nuxt/Vite/Astro** | `node_modules`, `.next`, `.nuxt`, `.output`, `.vercel`, `.turbo`, `out`, `dist`, `build`, `.parcel-cache`, `.vite`, `coverage`, `.nyc_output`, `.cache` |
| **Laravel/PHP** | `bootstrap/cache/*.php`, `storage/framework/views/*`, `storage/framework/cache/data/*`, `storage/framework/sessions/*`, `storage/logs/*.log` (+ `vendor/` jika `--vendor`) |
| **Go** | `bin/` (jika ada `go.mod`), `vendor/` (jika `--vendor`), `*.out`, `*.test` |
| **Rust** | `target/` |
| **Java/Kotlin** | `target/`, `build/`, `.gradle/`, `out/` |
| **Flutter/Dart** | `.dart_tool/`, `build/` |
| **Terraform** | `.terraform/` |
| **Python** | `__pycache__`, `.pytest_cache`, `.mypy_cache`, `.ruff_cache`, `.tox` |
| **Umum** | `.DS_Store`, `Pods/`, `_build/` |

## 🚀 Instalasi

### Homebrew (macOS / Linux) — Recommended

```bash
brew tap dankerizer/bersihkan
brew install bersihkan
```

Atau one-liner:

```bash
brew install dankerizer/bersihkan/bersihkan
```

> Setelah di-approve di [homebrew-core](https://github.com/Homebrew/homebrew-core/pull/300131), cukup:
> ```bash
> brew install bersihkan
> ```

Verifikasi:

```bash
bersihkan --help
```

### One-liner (tanpa Homebrew)

```bash
curl -fsSL https://raw.githubusercontent.com/dankerizer/bersihkan/master/bersihkan -o ~/.local/bin/bersihkan && chmod +x ~/.local/bin/bersihkan
```

Jika `command not found`, tambahkan ke PATH:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
# atau bash:
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

### Manual

```bash
git clone https://github.com/dankerizer/bersihkan.git
cd bersihkan
chmod +x bersihkan
mkdir -p ~/.local/bin && cp bersihkan ~/.local/bin/bersihkan
```

### System-wide (butuh sudo)

```bash
sudo curl -fsSL https://raw.githubusercontent.com/dankerizer/bersihkan/master/bersihkan -o /usr/local/bin/bersihkan
sudo chmod +x /usr/local/bin/bersihkan
```

## 💻 Cara Pakai

```bash
bersihkan                                  # urut nama A-Z (default)
bersihkan --sort=size                      # urut ukuran terbesar dulu
bersihkan -e vendor -e bin                 # jangan hapus vendor & bin
bersihkan --exclude="*.log" --dry-run      # jangan hapus *.log
bersihkan -e ".next" -e "dist" -y          # kecualikan .next & dist
bersihkan -e "target" --sort=size -v       # kecualikan Rust target, urut size
bersihkan ~/Projects --sort=name           # urut folder A-Z
bersihkan . --dry-run                      # cek dulu (tanpa hapus)
bersihkan . --vendor -y                    # hapus termasuk vendor/
bersihkan --help                           # bantuan lengkap
```

### Contoh Output

#### Sort by name (default)
```
🧹 bersihkan → /Users/hadie/Projects
Ditemukan 3 item (urut: nama A-Z):

  • my-app/.next
  • my-app/node_modules
  • api/dist

  Total: 365M (3 item)
```

#### Sort by size + exclude
```
🧹 bersihkan → /Users/hadie/Projects
  Exclude: vendor *.log
  → 2 item di-exclude (vendor *.log)
Ditemukan 3 item (urut: terbesar dulu):

  320M     my-app/node_modules
   45M     api/dist
  120K     my-app/.next

  Total: 365M (3 item)

✨ Selesai! 3 item dibersihkan (365M dibebaskan)
```

#### Live scanning (saat scan folder besar)
```
⠹ Mencari... 12 found → my-app/.next
```

## ⚙️ Opsi

```
PATH              Folder target (default: ".")
-n, --dry-run     Hanya tampilkan apa yang akan dihapus
-v, --verbose     Tampilkan detail + ukuran (lebih lambat)
    --vendor      Juga hapus vendor/ (PHP/Laravel/Go)
    --sort <mode> Urutan: name (default, A-Z) | size (terbesar dulu)
-e, --exclude <pat> Kecualikan folder/file/ekstensi (bisa berulang)
                  Contoh: -e vendor -e "*.log" -e "bin" -e ".next"
-y, --yes         Langsung hapus tanpa konfirmasi
-h, --help        Bantuan
```

## 🧠 SKILL.md (untuk AI Agent)

Repo ini menyertakan `SKILL.md` agar AI agent (OpenCode, Claude Code, dll) bisa auto-detect skill `bersihkan`.

```bash
# Install skill untuk agent
mkdir -p ~/.config/opencode/skills/bersihkan
curl -fsSL https://raw.githubusercontent.com/dankerizer/bersihkan/master/SKILL.md -o ~/.config/opencode/skills/bersihkan/SKILL.md
```

Lihat [`SKILL.md`](./SKILL.md) untuk detail trigger & workflow agent.

## 🔧 Uninstall

```bash
# Homebrew
brew uninstall bersihkan
brew untap dankerizer/bersihkan  # jika pakai tap

# Manual
rm ~/.local/bin/bersihkan
# atau system-wide:
sudo rm /usr/local/bin/bersihkan
```

## ⚠️ Disclaimer

> **Harap pastikan dan/atau push ke git terlebih dahulu sebelum mengkonfirmasi penghapusan.**
> Segala risiko kehilangan data bukan menjadi tanggung jawab kami. Gunakan `--dry-run` untuk memeriksa terlebih dahulu. Tindakan `bersihkan` bersifat permanen (`rm -rf`).

## 📝 Lisensi

Apache-2.0 — lihat [LICENSE](./LICENSE)

## 📜 Changelog

- **v2.5** — `--exclude` + Rust/Java/Flutter/Terraform support
- **v2.4** — support Go (`bin/`, `vendor/`, `*.out`, `*.test`)
- **v2.3** — `--sort=name|size` + live spinner, single-pass find + prune
- **v2.2** — live spinner (tampil folder sedang di-scan)
- **v2.1** — single find + prune `.git`, skip `du` kecuali `--verbose`
- **v2.0** — support Next.js, Laravel, Python, global command + SKILL.md

---
[dankedev.com](https://dankedev.com)
