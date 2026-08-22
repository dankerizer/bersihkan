# 🧹 bersihkan

Hapus `node_modules`, `.next`, `dist`, `build`, cache Laravel, dan artefak framework lainnya secara **rekursif** — bisa dipanggil dari mana pun.

> Support: **Next.js / React / Nuxt / Vite / Astro / Laravel / Python** dan umum. Aman, ada `--dry-run` + live spinner.

![disk full](disk-full.png)

## ✨ Fitur

- 🔁 **Rekursif** — scan semua subfolder dari posisi kamu berdiri
- 👀 **Aman** — konfirmasi sebelum hapus + mode `--dry-run`
- 🔍 **Live spinner** — tampil folder yang sedang di-scan + jumlah found (tidak kelihatan hang)
- 📊 **Hitung ukuran** — tampil total yang dibebaskan (hanya jika `--verbose`/`--sort=size`)
- 📂 **Sort** — `name` (A-Z, cepat) atau `size` (terbesar dulu)
- 🌍 **Global command** — install sekali, pakai di mana pun
- ⚡ **Cepat** — `find` single-pass + `-prune` `.git` & `node_modules`, compatible `bash 3.2` (macOS)

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
bersihkan                          # urut nama A-Z (default)
bersihkan --sort=size              # urut ukuran terbesar dulu
bersihkan --sort=size --dry-run    # preview urut size
bersihkan ~/Projects --sort=name   # urut folder A-Z
bersihkan . --dry-run              # cek dulu (tanpa hapus)
bersihkan . --dry-run -v           # cek + ukuran tiap item
bersihkan -y                       # langsung hapus tanpa konfirmasi
bersihkan --vendor -y              # hapus juga vendor/ (Laravel)
bersihkan --help                   # bantuan lengkap
```

### Contoh Output

#### Sort by name (default)
```
🧹 bersihkan → /Users/hadie/Projects
Ditemukan 3 item (urut: nama A-Z):

  • my-app/.next
  • my-app/node_modules
  • api/dist

  (3 item)
```

#### Sort by size (terbesar dulu)
```
🧹 bersihkan → /Users/hadie/Projects
Mengurutkan berdasarkan ukuran (menghitung size, bisa agak lambat)...
Ditemukan 3 item (urut: terbesar dulu):

  320M     my-app/node_modules
   45M     api/dist
  120K     my-app/.next

  Total: 365M (3 item)
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
    --vendor      Juga hapus vendor/ (PHP/Laravel)
    --sort <mode> Urutan: name (default, A-Z) | size (terbesar dulu)
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
rm ~/.local/bin/bersihkan
# atau system-wide:
sudo rm /usr/local/bin/bersihkan
```

## 📝 Lisensi

Apache-2.0 — lihat [LICENSE](./LICENSE)

## 📜 Changelog

- **v2.3** — `--sort=name|size` + live spinner, single-pass find + prune
- **v2.2** — live spinner (tampil folder sedang di-scan)
- **v2.1** — single find + prune `.git`, skip `du` kecuali `--verbose`
- **v2.0** — support Next.js, Laravel, Python, global command + SKILL.md

---
dankedev.com
