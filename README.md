# Catatan Git dan GitHub

## 1. Git dan GitHub

**Git** adalah sistem kontrol versi terdistribusi yang mencatat perubahan berkas dari waktu ke waktu. Git membantu kita membandingkan atau memulihkan versi, serta bekerja sama melalui branch.

**GitHub** adalah platform untuk menyimpan repositori Git dan berkolaborasi dalam proyek. GitHub menyediakan fitur seperti pull request, issue, code review, project board, dan GitHub Actions.

Git dan GitHub saling berkaitan, tetapi bukan hal yang sama. Git dapat digunakan tanpa GitHub, sedangkan repositori GitHub menggunakan Git untuk mengelola versi.

## 2. Repositori

**Repositori** (repo) adalah folder proyek yang dilacak oleh Git. Isinya mencakup berkas proyek dan riwayat perubahannya.

- **Repositori lokal** adalah salinan proyek di komputer.
- **Repositori remote** adalah salinan yang dihosting di server, misalnya GitHub.
- `origin` adalah nama standar untuk remote yang dibuat saat melakukan clone.
- `main` adalah nama branch utama yang umum digunakan. Sebagian repositori mungkin memakai nama branch utama yang berbeda.

Membuat atau menyalin repositori:

```bash
# Mulai melacak folder saat ini dengan Git
git init

# Salin repositori GitHub ke komputer
git clone https://github.com/OWNER/REPOSITORY.git

# Lihat URL remote yang sudah dikonfigurasi
git remote -v
```

## 3. Alur kerja Git

Perubahan di Git melewati tiga area utama:

1. **Working tree** — berkas yang sedang diedit.
2. **Staging area (index)** — perubahan yang dipilih untuk dimasukkan ke commit berikutnya.
3. **Riwayat repositori** — kumpulan commit yang sudah disimpan.

Alur kerja umum:

```bash
git status
git add README.md
git diff --staged
git commit -m "docs: add project overview"
git push origin main
```

- `git status` menampilkan perubahan, berkas yang sudah di-stage, berkas baru, dan branch aktif.
- `git add` memasukkan perubahan ke staging area. Perintah `git add .` memasukkan semua perubahan di folder saat ini, jadi periksa dahulu berkas yang akan disertakan.
- `git diff` menampilkan perubahan yang belum di-stage; `git diff --staged` menampilkan perubahan yang sudah di-stage.
- `git commit` menyimpan snapshot dari perubahan yang sudah di-stage ke riwayat lokal.
- `git push` mengirim commit lokal ke repositori remote.

Commit tetap tersimpan secara lokal sampai di-push. Commit yang baik berfokus pada satu perubahan logis dan memiliki pesan yang jelas.

## 4. Branch

**Branch** adalah penunjuk ke jalur pengembangan. Branch memungkinkan seseorang mengerjakan fitur atau perbaikan tanpa langsung mengubah jalur utama proyek.

```bash
# Tampilkan daftar branch; tanda bintang menunjukkan branch aktif
git branch

# Buat branch baru sekaligus berpindah ke branch tersebut
git switch -c feat/profile-readme

# Berpindah ke branch yang sudah ada
git switch main

# Publikasikan branch dan tetapkan upstream remote
git push -u origin feat/profile-readme
```

Gunakan nama branch yang singkat dan deskriptif, seperti `feat/login-page`, `fix/map-rendering`, atau `docs/github-notes`.

## 5. Pull, fetch, dan sinkronisasi

- `git fetch` mengunduh commit dan informasi branch dari remote, tetapi tidak menggabungkannya ke branch aktif.
- `git pull` mengambil lalu mengintegrasikan perubahan dari branch upstream ke branch aktif. Umumnya Git menggunakan merge, tetapi pengaturan Git dapat mengubah cara integrasinya.
- `git push` mengirim commit lokal ke repositori remote.

```bash
git fetch origin
git pull origin main
git push origin main
```

Sebelum mulai bekerja, periksa branch dan working tree dengan `git status`, lalu ambil pembaruan dari branch upstream yang sesuai.

## 6. Merge dan pull request

**Merge** mengintegrasikan commit dari satu branch ke branch lain. **Pull request (PR)** adalah usulan di GitHub untuk menggabungkan branch ke branch tujuan. PR menyediakan tempat untuk meninjau perubahan, berdiskusi, menjalankan pemeriksaan, dan meminta revisi sebelum merge.

Alur kolaborasi yang umum:

1. Buat branch.
2. Buat perubahan dan commit secara terfokus.
3. Push branch ke GitHub.
4. Buka PR dengan branch tujuan yang sesuai, biasanya `main`.
5. Tinjau perubahan dan tanggapi masukan.
6. Pastikan pemeriksaan yang diwajibkan berhasil, lalu merge PR.
7. Hapus branch fitur jika sudah tidak diperlukan.

**Fork** adalah salinan repositori pengguna lain yang dibuat di akun GitHub Anda. Fork biasanya digunakan jika Anda tidak memiliki izin untuk melakukan push langsung ke repositori asli. Anda dapat melakukan clone pada fork, membuat branch, mengirim perubahan, lalu membuka PR ke repositori asli.

**Clone** adalah salinan repositori remote ke komputer. Fork dilakukan di GitHub, sedangkan clone dilakukan di komputer. Keduanya sering digunakan bersama saat berkontribusi ke proyek milik orang lain.

## 7. Issue dan fitur kolaborasi

**Issue** GitHub digunakan untuk melacak bug, tugas, pertanyaan, atau ide. Issue dapat memiliki deskripsi, label, assignee, dan milestone. PR dapat merujuk ke issue, misalnya menggunakan `Closes #12`, agar GitHub menutup issue tersebut setelah PR di-merge ke branch default.

Fitur kolaborasi GitHub lainnya:

- **Code review:** komentar dan permintaan perubahan pada diff PR.
- **Label dan milestone:** membantu mengelompokkan issue dan PR.
- **Projects:** melacak pekerjaan dalam bentuk tabel atau papan.
- **GitHub Actions:** mengotomatiskan alur kerja seperti pengujian, build, dan deployment.
- **README:** memperkenalkan repositori dan menjelaskan cara menggunakannya.
- **`.gitignore`:** mencantumkan berkas yang tidak perlu dilacak Git, seperti berkas hasil generate atau rahasia lokal.

Jangan pernah memasukkan kata sandi, access token, private key, atau kredensial lain ke dalam commit. Menghapus rahasia pada commit berikutnya tidak menghapusnya dari riwayat. Jika rahasia terekspos, segera cabut atau ganti rahasia tersebut.

## 8. Merge conflict

**Merge conflict** terjadi ketika Git tidak dapat menggabungkan perubahan secara otomatis, biasanya karena dua branch mengubah baris yang sama. Git menandai bagian yang konflik di berkas terkait.

Langkah aman untuk menyelesaikannya:

1. Jalankan `git status` untuk mengetahui berkas yang konflik.
2. Buka setiap berkas dan periksa penanda konflik: `<<<<<<<`, `=======`, dan `>>>>>>>`.
3. Pilih atau gabungkan konten yang benar, lalu hapus penanda konflik.
4. Periksa berkas yang sudah diperbaiki dan stage dengan `git add <file>`.
5. Selesaikan merge dengan `git commit` jika Git belum melakukannya.

Jangan langsung memilih perubahan dari satu sisi tanpa memahami perubahan dari sisi lainnya.

## 9. Perintah untuk memeriksa dan memulihkan perubahan

```bash
# Tampilkan status working tree dan branch aktif
git status

# Tampilkan beberapa commit terakhir
git log --oneline --graph --decorate -10

# Tampilkan perubahan yang belum di-stage
git diff

# Keluarkan berkas dari staging area tanpa menghapus editannya
git restore --staged README.md

# Buang edit yang belum di-stage pada berkas (destruktif; gunakan dengan hati-hati)
git restore README.md

# Buat commit baru untuk membatalkan commit sebelumnya dengan aman
git revert COMMIT_HASH
```

Periksa dampak perintah sebelum menggunakan operasi destruktif. `git reset --hard` dan `git clean -fd` dapat menghapus pekerjaan lokal secara permanen.

## 10. Conventional Commits

**Conventional Commits** adalah konvensi untuk menulis pesan commit dengan format terstruktur. Format umumnya:

```text
<type>[scope opsional][!]: <deskripsi singkat>

[isi opsional]

[footer opsional]
```

Contoh:

```bash
git commit -m "docs: add GitHub notes"
git commit -m "feat(auth): add login page"
git commit -m "fix(readme): correct broken image path"
```

Gunakan deskripsi yang singkat dan jelas. Sebisa mungkin tulis dalam bentuk perintah, seperti `add`, `fix`, atau `update`. Jangan akhiri subjek dengan titik. Scope bersifat opsional dan menunjukkan bagian proyek yang terdampak.

### Jenis commit yang umum

| Jenis | Digunakan untuk | Contoh |
|---|---|---|
| `feat` | Menambahkan fitur atau kemampuan yang terlihat oleh pengguna. | `feat(profile): add contact links` |
| `fix` | Memperbaiki bug. | `fix(map): handle empty coordinates` |
| `docs` | Perubahan dokumentasi saja. | `docs: add GitHub notes` |
| `style` | Perubahan format atau gaya yang tidak mengubah perilaku, seperti spasi atau pemformatan lint. | `style: format Python files` |
| `refactor` | Menata ulang kode tanpa mengubah perilaku yang terlihat dari luar. | `refactor(api): extract request helper` |
| `test` | Menambahkan, memperbarui, atau memperbaiki pengujian. | `test(map): cover missing geometry` |
| `chore` | Tugas pemeliharaan yang bukan fitur baru atau perbaikan bug untuk pengguna. | `chore: update editor settings` |
| `build` | Perubahan sistem build atau dependensi. | `build: add Vite configuration` |
| `ci` | Perubahan konfigurasi integrasi atau pengiriman berkelanjutan. | `ci: run tests on pull requests` |
| `perf` | Perubahan yang tujuan utamanya meningkatkan performa. | `perf(map): cache tile lookups` |
| `revert` | Membatalkan commit sebelumnya. | `revert: revert \"feat: add login page\"` |
| `core` | Gunakan hanya jika proyek mendefinisikannya untuk perubahan inti/internal; `core` bukan jenis standar dalam spesifikasi Conventional Commits. | `core: update PID controller` |

Jenis standar `feat` dan `fix` memiliki arti khusus dalam spesifikasi. Jenis lain dapat digunakan sesuai konvensi proyek. Gunakan arti yang konsisten di seluruh proyek.

### Breaking change

Tambahkan `!` setelah jenis atau scope untuk menandai perubahan yang tidak kompatibel (breaking change), atau jelaskan melalui footer yang diawali `BREAKING CHANGE:`. Breaking change mengubah perilaku sehingga pengguna atau kode yang bergantung padanya perlu melakukan penyesuaian.

```text
feat(api)!: remove the v1 endpoint

BREAKING CHANGE: Clients must use the v2 endpoint.
```

Breaking change juga dapat dicatat melalui footer tanpa `!`, jika itu konvensi yang dipilih proyek.

### Contoh pesan commit untuk berbagai jenis perubahan

```bash
git commit -m "feat: add login page"
git commit -m "fix: correct typo in README"
git commit -m "docs: add GitHub notes"
git commit -m "style: format Python files"
git commit -m "refactor: simplify map rendering"
git commit -m "test: add coordinate parser tests"
git commit -m "chore: update editor settings"
git commit -m "build: add Vite configuration"
git commit -m "ci: run tests on pull requests"
git commit -m "perf: cache map tile lookups"
git commit -m "core: update PID controller"
```

`core` hanya digunakan jika tim atau proyek memang menetapkan jenis tersebut. Jika belum ada aturan seperti itu, gunakan jenis yang paling sesuai, misalnya `feat`, `fix`, atau `refactor`.

## 11. Contoh kontribusi dari awal hingga akhir

```bash
# Mulai dari branch main terbaru
git switch main
git pull origin main

# Buat branch khusus untuk perubahan ini
git switch -c docs/github-notes

# Stage dan periksa perubahan yang akan dimasukkan
git add 02-intro-to-github/notes/github-notes.md
git diff --staged

# Buat commit dengan Conventional Commits
git commit -m "docs: add GitHub notes"

# Publikasikan branch
git push -u origin docs/github-notes
```

Setelah itu, buka pull request di GitHub. Jika tugas secara khusus meminta perubahan langsung di `main`, ikuti alur kerja dan izin yang ditetapkan pemilik repositori. Banyak tim mewajibkan PR dan tidak mengizinkan push langsung ke `main`.
