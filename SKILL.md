---
name: bersihkan
description: "Hapus node_modules, .next, dist, build, dan cache framework (Next.js, React, Vite, Nuxt, Laravel, Go, Rust, Java, Flutter, Python) secara rekursif. Gunakan saat user ingin membersihkan project, menghemat disk, atau sebelum reinstall dependencies."
---

# bersihkan 🧹

Command global untuk membersihkan artefak build dan cache framework secara **rekursif** dari folder mana pun.

## Kapan Gunakan Skill Ini

Aktifkan skill ini ketika user:
- Meminta membersihkan `node_modules`, `.next`, `dist`, `build`, atau cache project
- Mengeluh disk penuh karena project JS/PHP/Go/Rust/Python
- Ingin install ulang dependencies (`npm install`, `composer install`, `cargo build`) dari kondisi bersih
- Menyebut kata kunci: `bersihkan`, `clean`, `hapus node_modules`, `bersihkan cache`, `clean project`

## Instalasi

### One-liner (Recommended)

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
# atau untuk bash:
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

### System-wide

```bash
sudo curl -fsSL https://raw.githubusercontent.com/dankerizer/bersihkan/master/bersihkan -o /usr/local/bin/bersihkan && sudo chmod +x /usr/local/bin/bersihkan
```

## Yang Dibersihkan (Rekursif)

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

## Cara Pakai

```bash
bersihkan                                  # urut nama A-Z (default)
bersihkan --sort=size                      # urut ukuran terbesar dulu
bersihkan -e vendor -e bin                 # jangan hapus vendor & bin
bersihkan --exclude="*.log" --dry-run      # jangan hapus *.log
bersihkan -e ".next" -e "dist" -y          # kecualikan .next & dist
bersihkan --vendor -y                      # termasuk hapus vendor/
bersihkan --help                           # bantuan lengkap
```

## Opsi

```
PATH              Folder target (default: ".")
-n, --dry-run     Preview saja
-v, --verbose     Tampilkan ukuran tiap item (lebih lambat)
    --vendor      Juga hapus vendor/
    --sort <mode> Urutan: name (default, A-Z) | size (terbesar dulu)
-e, --exclude <pat> Kecualikan folder/file/ekstensi (bisa berulang)
                  Contoh: -e vendor -e "*.log" -e "bin"
-y, --yes         Skip konfirmasi
-h, --help        Bantuan
```

## Contoh Workflow Agent

Ketika user minta bersihkan project, agent harus:

1. **Cek dulu** dengan dry-run:
   ```bash
   bersihkan . --dry-run -v
   # atau exclude yang tidak mau dihapus:
   bersihkan . --dry-run -e vendor
   ```

2. **Konfirmasi** ke user total ukuran & jumlah item yang akan dihapus

3. **Eksekusi** jika user setuju:
   ```bash
   bersihkan -y
   # atau dengan vendor jika Laravel/Go:
   bersihkan --vendor -y
   # atau exclude:
   bersihkan -e ".next" -y
   ```

4. **Laporkan** hasil (berapa item & ukuran dibebaskan)

## Contoh Output

```
🧹 bersihkan → /Users/hadie/Projects
  Exclude: vendor
  → 1 item di-exclude (vendor)
Ditemukan 7 item (urut: nama A-Z):

  • my-app/node_modules
  • my-app/.next
  • api/dist

  Total: 1.2G (7 item)

Hapus semua di atas? [y/N] y

  ✓ my-app/node_modules
  ✓ my-app/.next
✨ Selesai! 7 item dibersihkan (1.2G dibebaskan)
```

## Uninstall

```bash
rm ~/.local/bin/bersihkan
# atau system-wide:
sudo rm /usr/local/bin/bersihkan
```

## Catatan

- Script compatible dengan `bash 3.2` (macOS default) dan `zsh`
- Cari secara rekursif dengan `find` + `-prune` (skip `.git` & tidak masuk ke `node_modules`) - aman untuk monorepo
- Live spinner selama scan + `--exclude` untuk fleksibilitas
- `--sort=size` otomatis aktifkan verbose & hitung size (lebih lambat tapi urut akurat)
- Selalu gunakan `--dry-run` dulu sebelum hapus di project penting
