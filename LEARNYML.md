# Belajar YML (YAML) - GitHub Actions Deploy Workflow

## Apa itu YAML?

YAML = "YAML Ain't Markup Language"
Basically cuma file konfigurasi yang pakai **indentasi** (spasi) buat nunjukin struktur.
Mirip JSON tapi lebih gampang dibaca manusia.

Aturan dasar:
- Pakai **spasi** (BUKAN tab) buat indentasi
- `key: value` = pasangan data (kayak object di JS)
- `- item` = list/array
- Indentasi nunjukin parent-child relationship

---

## Bedah File `deploy.yml` Baris per Baris

```yaml
name: Deploy to GitHub Pages
```
Nama workflow-nya. Ini yang muncul di tab "Actions" di GitHub.

---

```yaml
on:
  push:
    branches: ['master']
  workflow_dispatch:
```

**`on`** = Kapan workflow ini jalan? (trigger/pemicu)

- `push: branches: ['master']` = Jalan otomatis setiap kali kamu push ke branch `master`
- `workflow_dispatch` = Bisa juga di-trigger manual dari tab Actions di GitHub (ada tombol "Run workflow")

---

```yaml
permissions:
  contents: read
  pages: write
  id-token: write
```

**`permissions`** = Izin yang dikasih ke workflow ini

- `contents: read` = Boleh baca isi repo kamu
- `pages: write` = Boleh nulis/deploy ke GitHub Pages
- `id-token: write` = Buat autentikasi deployment

Anggap ini kayak ngasih kunci rumah ke tukang - cuma dikasih akses yang dia butuhkan.

---

```yaml
concurrency:
  group: 'pages'
  cancel-in-progress: true
```

**`concurrency`** = Biar gak bentrok kalau ada 2 deploy barengan

Misalnya kamu push 2x cepet-cepet, yang pertama langsung di-cancel, yang kedua yang jalan.

---

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
```

**`jobs`** = Kerjaan yang harus dilakukan. Di sini ada 2 job: `build` dan `deploy`.

- `build` = nama job pertama
- `runs-on: ubuntu-latest` = Jalanin di komputer virtual Linux (server GitHub gratis)

---

```yaml
    steps:
      - uses: actions/checkout@v4
```

**`steps`** = Langkah-langkah dalam job `build`

- `uses: actions/checkout@v4` = Download/clone kode repo kamu ke server.
  Tanpa ini, server-nya kosong, gak punya kode kamu.

---

```yaml
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'
```

Install Node.js versi 20 di server.
`cache: 'npm'` = cache node_modules biar next build lebih cepet.

---

```yaml
      - run: npm ci
      - run: npm run build
```

**`run`** = Jalanin command di terminal (sama kayak kamu ketik di cmd/terminal)

- `npm ci` = Install semua dependencies dari package-lock.json (kayak `npm install` tapi lebih strict & cepet)
- `npm run build` = Build project Svelte kamu jadi file static (HTML/CSS/JS) ke folder `dist/`

---

```yaml
      - uses: actions/upload-pages-artifact@v3
        with:
          path: './dist'
```

Upload folder `dist/` (hasil build) sebagai "artifact" biar bisa di-deploy di job berikutnya.

---

```yaml
  deploy:
    needs: build
    runs-on: ubuntu-latest
```

Job kedua: `deploy`

- `needs: build` = Job ini TUNGGU job `build` selesai dulu baru jalan.

---

```yaml
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
```

- `environment: github-pages` = Nandain ini deploy ke environment GitHub Pages
- `url: ${{ ... }}` = Ambil URL hasil deploy (kayak variable/template)

`${{ }}` = Syntax buat akses variable di GitHub Actions (mirip `${}` di JavaScript template literal)

---

```yaml
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```

Deploy artifact (folder `dist/` yang tadi di-upload) ke GitHub Pages. Done!

---

## Alur Lengkapnya (TL;DR)

```
Kamu push ke master
       |
       v
GitHub Actions triggered
       |
       v
[JOB: build]
  1. Clone repo kamu
  2. Install Node.js
  3. npm ci (install dependencies)
  4. npm run build (bikin folder dist/)
  5. Upload dist/ sebagai artifact
       |
       v
[JOB: deploy]
  1. Tunggu build selesai
  2. Ambil artifact (dist/)
  3. Deploy ke GitHub Pages
       |
       v
Website live di https://syauqi357.github.io/PLATFORM-AKADEMIK/
```

## Cheatsheet YAML Syntax

```yaml
# Ini komentar

# Key-value (object)
name: Deploy
version: 1

# Nested object (pakai indentasi 2 spasi)
person:
  name: Syauqi
  age: 21

# Array/list
fruits:
  - apple
  - banana
  - mango

# Inline array
branches: ['master', 'main']

# Boolean
enabled: true
debug: false

# Multi-line string
description: |
  Ini baris pertama
  Ini baris kedua
```
