# EasySail
Use **Laravel Sail** without any <ins>builds or additional installations</ins> on your **host system**. [Latest Release](https://github.com/karbordia/easysail/releases/latest)

## 📚 Table of Contents
- [📝 Notes](#-notes)
- [🎯 Why This Repository Exists](#-why-this-repository-exists)
  - [1️⃣ Stop Rebuilding Sail](#1️⃣-stop-rebuilding-sail)
  - [2️⃣ Remove Unnecessary Steps](#2️⃣-remove-unnecessary-steps)
- [⚙️ Usage](#%EF%B8%8F-usage)


## 📝 Notes

- The **full versions** are built **directly from [laravel/sail](https://github.com/laravel/sail/tree/1.x/runtimes)** without any modifications.
- The **mini versions** are identical to the full ones, **except** they do **not include**: [see](https://github.com/karbordia/easysail/blob/main/.github/workflows/build-sail-images.yml#L47#L58)

  - Node.js
  - npm
  - pnpm
  - bun

## 🎯 Why This Repository Exists

This repository was created for **two main reasons**:

---

### 1️⃣ Stop Rebuilding Sail

Let’s be honest — some people might not see this as a big deal,
but here in **Iran** (and maybe in some other countries too),
many Laravel developers spend **an entire day or more** just trying to **build Laravel Sail**.

Because of **sanctions** and **slow internet**, some developers even try to modify the **Dockerfile** to make it work which often leads to more errors and broken builds.  
The whole process can be painful and time-consuming.

This repository solves that problem.
All you need is a **simple download from the [Latest Release](https://github.com/karbordia/easysail/releases/latest)**, and you’re done — **no more builds**.

---

### 2️⃣ Remove Unnecessary Steps

🚧 In Development

Think about it — if we’re using **Laravel Sail** to run our Laravel project inside Docker,
why should we have to install **PHP** and **Composer** on our host machine? It just doesn’t make sense.

I prefer to keep my system clean and lightweight.
With **EasySail**, you can deploy your Laravel project using **only Docker** —
no extra installations, no clutter, just pure simplicity and enjoyment.

---

> “Run Laravel Sail **easily** — no builds, no setup, no mess.”

## ⚙️ Usage

Completely easy and hassle-free — no builds required!  
Just download the PHP version you need from the [Latest Release](https://github.com/karbordia/easysail/releases/latest).  

For example:  
`laravel-sail-php8.4-mini.zip`

After downloading, extract the `.tar` file from the ZIP archive.  
The extracted `.tar` file is the prebuilt Docker image, which you can import into your local Docker images using:

```bash
unzip ~/Downloads/laravel-sail-php8.4-mini.zip -d ~/Downloads
docker load -i ~/Downloads/laravel-sail-php8.4-mini.tar
```