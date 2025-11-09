# EasySail
Use **Laravel Sail** without any <ins>builds or additional installations</ins> on your **host system**. [Latest Release](https://github.com/karbordia/easysail/releases/latest)

## 📚 Table of Contents
- [📝 Notes](#-notes)
- [🎯 Why This Repository Exists](#-why-this-repository-exists)
  - [1️⃣ Stop Rebuilding Sail](#1️⃣-stop-rebuilding-sail)
  - [2️⃣ Remove Unnecessary Steps](#2️⃣-remove-unnecessary-steps)
- [⚙️ Usage](#%EF%B8%8F-usage)
    - [🛠️ EasySail Tool - (As Soon)](##%EF%B8%8F-easysail-tool---as-soon)
    - [⚡ Manual](#-manual)
        - [🖼️ Load Image](#%EF%B8%8F-load-image)
        - [💻 Using Command Prompt](#-using-command-prompt)
        - [🚀 Existing Laravel Project Serving](#-existing-laravel-project-serving)

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

### ⚙️ EasySail Tool - (As Soon)
> We will soon introduce a gui|cli tool to make using Laravel Sail easier.
### ⚡ Manual
#### 🖼️ Load Image
Completely easy and hassle-free — no builds required!

First, download the Laravel Sail version you need.

```bash
wget -P ~/Downloads https://github.com/karbordia/easysail/releases/latest/download/laravel-sail-php8.x.zip
```
Or, if you want to use the mini version:
```bash
wget -P ~/Downloads https://github.com/karbordia/easysail/releases/latest/download/laravel-sail-php8.x-mini.zip
```

💡 In this example, we’re using **laravel-sail-php8.4-mini**.

The extracted `.tar` file is the prebuilt Docker image, which you can import into your local Docker images using:

```bash
unzip ~/Downloads/laravel-sail-php8.4-mini.zip -d ~/Downloads
docker load -i ~/Downloads/sail-php8.4-mini/laravel-sail-php8.4-mini.tar
```

🔽 The output should look like this:

```bash
$ docker load -i ~/Downloads/sail-php8.4-mini/laravel-sail-php8.4-mini.tar
d05aa0ce0c21: Loading layer   2.56kB/2.56kB
9e89562f7150: Loading layer  3.072kB/3.072kB
............................................
53eb959af5ca: Loading layer  4.608kB/4.608kB
1e1ed732bab1: Loading layer  4.096kB/4.096kB
Loaded image: laravel-sail-php8.4-mini:latest
$
```

#### 💻 Using Command Prompt

You can use the container’s command prompt to create your Laravel project.

```bash
## Host Prompt
$ mkdir -p ~/Documents/laravel_sail
$ cd ~/Documents/laravel_sail
$ docker run --rm -it --entrypoint "/bin/bash" -v "$PWD:/laravel_sail" laravel-sail-php8.4-mini:latest
```
Then:
```bash
## Container Prompt
root@80fd8c255a07:/var/www/html# cd /laravel_sail
root@80fd8c255a07:/laravel_sail# composer create-project laravel/laravel example-app
root@80fd8c255a07:/laravel_sail# cd example-app
root@80fd8c255a07:/laravel_sail# composer require laravel/sail --dev
root@80fd8c255a07:/laravel_sail# php artisan sail:install
root@80fd8c255a07:/laravel_sail# sed -i "s|['\"]\?sail-[0-9.]\+/app['\"]\?|laravel-sail-php8.4-mini|g" compose.yaml
root@80fd8c255a07:/laravel_sail# exit
```

finally:

```bash
## Host Prompt
$ cd example-app
& sudo chmod -R 777 .
$ vendor/bin/sail up -d
$ vendor/bin/sail artisan migrate
```

Open **127.0.0.1:80** in your browser and enjoy Laravel.

#### 🚀 Existing Laravel Project Serving

If you want to run an existing Laravel project using Sail, follow these steps:

```bash
$  example-app ls
app      bootstrap      composer.lock  database      phpunit.xml  README.md  routes   tests   vite.config.js
artisan  composer.json  config         package.json  public       resources  storage  vendor
```

This is an existing Laravel project that was running without Sail.
We want to run it using Sail.

First, check the PHP version of the project.

```bash
$  example-app cat composer.json | grep "\"php\":"
        "php": "^8.2",
```

So we can use PHP 8.2 or higher.
Let's go ahead and use 8.4.

```bash
##Host Prompt
$ docker run --rm -it --entrypoint "/bin/bash" -v "$PWD:/existed_laravel" laravel-sail-php8.4-mini:latest
```
then (existing project):
```bash
## Container Prompt
root@80fd8c255a07:/var/www/html# cd /existed_laravel
root@80fd8c255a07:/laravel_sail# composer require laravel/sail --dev
root@80fd8c255a07:/laravel_sail# php artisan sail:install
root@80fd8c255a07:/laravel_sail# sed -i "s|['\"]\?sail-[0-9.]\+/app['\"]\?|laravel-sail-php8.4-mini|g" compose.yaml
root@80fd8c255a07:/laravel_sail# exit
```
finally (existing project):
```bash
## Host Prompt
$ sudo chmod -R 777 .
$ vendor/bin/sail up -d
$ vendor/bin/sail artisan migrate
```