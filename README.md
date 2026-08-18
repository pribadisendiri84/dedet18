# Dedet 18

Landing page rumah Scandinavian di Jl. Dedet No.18, Beji Timur, Depok.

Repo GitHub: https://github.com/pribadisendiri84/dedet18

---

## Push ke GitHub (Manual)

Repo ini memakai **SSH key terpisah** dari akun Git Bukalapak di laptop.

### 1. Masuk ke folder project

```bash
cd ~/bukalapak/Noted/dedet18
```

### 2. Pastikan identitas Git untuk repo ini (lokal)

Jangan pakai `--global`, supaya tidak mengubah repo kerja.

```bash
git config user.name "pribadisendiri84"
git config user.email "pribadisendiri@gmail.com"
```

Cek:

```bash
git config user.email
git config --global user.email
```

- Lokal → email personal
- Global → boleh tetap email Bukalapak

### 3. Pastikan SSH key personal sudah ada

Key khusus repo ini:

```bash
ls ~/.ssh/id_ed25519_dedet18 ~/.ssh/id_ed25519_dedet18.pub
```

Kalau belum ada, buat:

```bash
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_dedet18 -C "pribadisendiri84-dedet18"
```

Copy public key:

```bash
cat ~/.ssh/id_ed25519_dedet18.pub
```

Tambahkan ke GitHub → **Settings → SSH and GPG keys → New SSH key**  
https://github.com/settings/keys

### 4. Tes koneksi SSH (pakai key personal)

```bash
ssh -i ~/.ssh/id_ed25519_dedet18 -o IdentitiesOnly=yes -T git@github.com
```

Kalau berhasil, muncul:

```text
Hi pribadisendiri84! You've successfully authenticated...
```

> `ssh -T git@github.com` tanpa `-i` bisa gagal jika default laptop belum terdaftar di GitHub. Itu normal.

### 5. Pastikan remote repo benar

```bash
git remote -v
```

Harus menunjuk ke:

```text
git@github.com:pribadisendiri84/dedet18.git
```

Repo ini sudah diset pakai SSH key khusus lewat:

```bash
git config core.sshcommand
```

### 6. Commit & push

```bash
git add .
git status
git commit -m "Update landing page Dedet 18"
git push origin main
```

Push pertama kali (kalau branch belum pernah di-push):

```bash
git push -u origin main
```

---

## Cek sedang pakai Git yang mana

Jalankan di folder `dedet18`:

```bash
echo "Name: $(git config user.name)"
echo "Email: $(git config user.email)"
echo "Remote: $(git remote get-url origin)"
echo "SSH: $(git config core.sshcommand)"
```

---

## Struktur file

```text
dedet18/
├── index.html      # Landing page
├── images/         # Foto unit & denah
├── README.md       # Panduan ini
└── .gitignore
```

---

## Deploy (GitHub Pages)

1. Buka repo → **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** / folder **/ (root)**
4. Save

Website akan tersedia di:

```text
https://pribadisendiri84.github.io/dedet18/
```
