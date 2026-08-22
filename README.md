# 🧹 bersihkan

Hapus `node_modules`, `.next`, `dist`, `build`, cache Laravel, dan artefak framework lainnya secara **rekursif** — bisa dipanggil dari mana pun.

> Support: **Next.js / React / Nuxt / Vite / Astro / Laravel / Python** dan umum. Aman, ada `--dry-run` + hitung ukuran.

![disk full](disk-full.png)

## ✨ Fitur

- 🔁 **Rekursif** — scan semua subfolder dari posisi kamu berdiri
- 👀 **Aman** — konfirmasi sebelum hapus + mode `--dry-run`
- 📊 **Hitung ukuran** — tampil total yang dibebaskan
- 🌍 **Global command** — install sekali, pakai di mana pun
- ⚡ **Cepat** — pakai `find` native, compatible `bash 3.2` (macOS)

## 📦 Yang Dibersihkan

| Kategori | Target |
|----------|--------|
| **JS/Node/React/Next/Nuxt/Vite/Astro** | `node_modules`, `.next`, `.nuxt`, `.output`, `.vercel`, `.turbo`, `out`, `dist`, `build`, `.parcel-cache`, `.vite`, `coverage`, `.nyc_output`, `.cache` |
| **Laravel/PHP** | `bootstrap/cache/*.php`, `storage/framework/views/*`, `storage/framework/cache/data/*`, `storage/framework/sessions/*`, `storage/logs/*.log` (+ `vendor/` jika `--vendor`) |
| **Python** | `__pycache__`, `.pytest_cache`, `.mypy_cache`, `.ruff_cache` |
| **Umum** | `.DS_Store` |

## 🚀 Instalasi

### Opsi 1: One-liner (Recommended)

```bash
curl -fsSL https://raw.githubusercontent.com/dankerizer/bersihkan/master/bersihkan -o ~/.local/bin/bersihkan && chmod +x ~/.local/bin/bersihkan
```

Verifikasi:

```bash
bersihkan --help
```

Jika `command not found`, tambahkan ke PATH:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
# atau bash:
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

### Opsi 2: Manual

```bash
git clone https://github.com/dankerizer/bersihkan.git
cd bersihkan
chmod +x bersihkan
mkdir -p ~/.local/bin && cp bersihkan ~/.local/bin/bersihkan
```

### Opsi 3: System-wide (butuh sudo)

```bash
sudo curl -fsSL https://raw.githubusercontent.com/dankerizer/bersihkan/master/bersihkan -o /usr/local/bin/bersihkan
sudo chmod +x /usr/local/bin/bersihkan
```

## 💻 Cara Pakai

```bash
bersihkan                  # bersihkan folder saat ini (rekursif)
bersihkan ~/Projects       # bersihkan semua project di folder itu
bersihkan . --dry-run      # cek dulu apa yang akan dihapus (tidak menghapus)
bersihkan . --dry-run -v   # cek + lihat ukuran tiap item
bersihkan -y               # langsung hapus tanpa konfirmasi
bersihkan --vendor -y      # hapus juga vendor/ (Laravel)
bersihkan --help           # bantuan lengkap
```

### Contoh Output

```
🧹 bersihkan → /Users/hadie/Projects
Ditemukan 7 item:

  • my-app/node_modules
  • my-app/.next
  • api/dist
  • laravel-app/storage/framework/views/cache.php

  Total: 1.2G (7 item)

Hapus semua di atas? [y/N] y

  ✓ my-app/node_modules
  ✓ my-app/.next
✨ Selesai! 7 item dibersihkan (1.2G dibebaskan)
```

## ⚙️ Opsi

```
PATH         Folder target (default: ".")
-n, --dry-run    Hanya tampilkan apa yang akan dihapus
-v, --verbose    Tampilkan detail + ukuran
    --vendor     Juga hapus vendor/ (PHP/Laravel)
-y, --yes        Langsung hapus tanpa konfirmasi
-h, --help       Bantuan
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
rm ~/.local/bin/bersihkan
# atau system-wide:
sudo rm /usr/local/bin/bersihkan
```

## 📝 Lisensi

Apache-2.0 — lihat [LICENSE](./LICENSE)

---
Made with ❤️ — https://github.com/dankerizer/bersihkan
Gist mirror: https://gist.github.com/dankerizer/372c92d3a64586a35dc1d23db5e0188e
