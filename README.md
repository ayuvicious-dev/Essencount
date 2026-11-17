# Essencount

Aplikasi pembukuan (accounting) berbasis PWA. Login dan penyimpanan data memakai Firebase (Authentication + Firestore). Tidak ada fitur daftar: akun dibuat manual di Firebase Console.

## Isi folder

| File | Fungsi |
|---|---|
| `index.html` | Seluruh aplikasi (HTML, CSS, JS, logo tertanam) |
| `manifest.json` | Pengaturan PWA (nama, warna, ikon) |
| `service-worker.js` | Cache offline |
| `icons/` | Ikon aplikasi |
| `.nojekyll` | Agar GitHub Pages menyajikan file apa adanya |

## Pasang di Firebase

1. **Authentication > Sign-in method**: aktifkan **Email/Password**.
2. **Authentication > Users > Add user**: buat email dan kata sandi untuk setiap pengguna.
3. **Firestore Database > Rules**: ganti seluruh isi dengan aturan berikut, lalu klik **Publish**.

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

Setiap pengguna hanya bisa membaca dan menulis data miliknya sendiri.

## Pasang di GitHub Pages

1. Unggah semua file dan folder `icons` ke repository.
2. **Settings > Pages**: pilih branch `main`, folder `/ (root)`.
3. Buka `https://USERNAME.github.io/NAMA-REPO/`.

## Update berikutnya

Cukup ganti `index.html` di GitHub. Service worker mengambil `index.html` terbaru lebih dulu, jadi pembaruan muncul saat aplikasi dibuka kembali.

## Mode demo

Buka alamat aplikasi dengan tambahan `?demo=1`, atau tekan **Coba akun demo** di halaman login. Data demo berupa contoh dan tidak disimpan.
