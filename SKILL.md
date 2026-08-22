---
name: bersihkan
description: "Hapus node_modules, .next, dist, build, dan cache framework (Next.js, React, Vite, Nuxt, Laravel, Python) secara rekursif. Gunakan saat user ingin membersihkan project, menghemat disk, atau sebelum reinstall dependencies."
---

# bersihkan 🧹

Command global untuk membersihkan artefak build dan cache framework secara **rekursif** dari folder mana pun.

## Kapan Gunakan Skill Ini

Aktifkan skill ini ketika user:
- Meminta membersihkan `node_modules`, `.next`, `dist`, `build`, atau cache project
- Mengeluh disk penuh karena project JS/PHP/Python
- Ingin install ulang dependencies (`npm install`, `composer install`) dari kondisi bersih
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
| **Python** | `__pycache__`, `.pytest_cache`, `.mypy_cache`, `.ruff_cache` |
| **Umum** | `.DS_Store` |

## Cara Pakai

```bash
bersihkan                          # urut nama A-Z (default)
bersihkan --sort=size              # urut ukuran terbesar dulu
bersihkan --sort=size --dry-run    # preview urut size
bersihkan ~/Projects --sort=name   # urut folder A-Z
bersihkan . --dry-run              # preview - hanya tampilkan, tidak menghapus
bersihkan . --dry-run -v           # preview + ukuran tiap item
bersihkan -y                       # langsung hapus tanpa konfirmasi
bersihkan --vendor -y              # termasuk hapus vendor/ (Laravel)
bersihkan --help                   # bantuan lengkap
```

## Opsi

```
PATH              Folder target (default: ".")
-n, --dry-run     Preview saja
-v, --verbose     Tampilkan ukuran tiap item (lebih lambat)
    --vendor      Juga hapus vendor/
    --sort <mode> Urutan: name (default, A-Z) | size (terbesar dulu)
-y, --yes         Skip konfirmasi
-h, --help        Bantuan
```

## Contoh Workflow Agent

Ketika user minta bersihkan project, agent harus:

1. **Cek dulu** dengan dry-run:
   ```bash
   bersihkan . --dry-run -v
   ```

2. **Konfirmasi** ke user total ukuran & jumlah item yang akan dihapus

3. **Eksekusi** jika user setuju:
   ```bash
   bersihkan -y
   # atau dengan vendor jika Laravel:
   bersihkan --vendor -y
   ```

4. **Laporkan** hasil (berapa item & ukuran dibebaskan)

## Contoh Output

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

## Uninstall

```bash
rm ~/.local/bin/bersihkan
# atau system-wide:
sudo rm /usr/local/bin/bersihkan
```

## Catatan

- Script compatible dengan `bash 3.2` (macOS default) dan `zsh`
- Cari secara rekursif dengan `find` + `-prune` (skip `.git` & tidak masuk ke `node_modules`) - aman untuk monorepo
- Live spinner selama scan + hitung ukuran hanya jika `--verbose`/`--sort=size`
- `--sort=size` otomatis aktifkan verbose & hitung size (lebih lambat tapi urut akurat)
- Selalu gunakan `--dry-run` dulu sebelum hapus di project penting

---
Gist: https://gist.github.com/dankerizer/372c92d3a64586a35dc1d23db5e0188e
Raw: https://raw.githubusercontent.com/dankerizer/bersihkan/master/bersihkan
