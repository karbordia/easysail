# EasySail
Use **Laravel Sail** without any <ins>builds or additional installations</ins> on your **host system**. [Latest Release](https://github.com/karbordia/easysail/releases/latest)

## 📚 Table of Contents
- [📝 Notes](#-notes)
- [🎯 Why This Repository Exists](#-why-this-repository-exists)
- [⚙️ Usage](#%EF%B8%8F-usage)
	- [🖼️ Load Image](#%EF%B8%8F-load-image)
    - [💻 Using Command Prompt](#-using-command-prompt)
    - [🚀 Existing Laravel Project Serving](#-existing-laravel-project-serving)

## 📝 Notes

- The **full versions** are built **directly from [laravel/sail](https://github.com/laravel/sail/tree/1.x/runtimes)** without any modifications.
- The **mini versions** are identical to the full ones, **except** they do **not include**: [see](https://github.com/karbordia/easysail/blob/main/.github/workflows/build-sail-images.yml#L47#L58)

  - node.js
  - npm
  - pnpm
  - bun

## 🎯 Why This Repository Exists

Let’s be honest — some people might not see this as a big deal,
but here in **Iran** (and maybe in some other countries too),
many Laravel developers spend **an entire day or more** just trying to **build Laravel Sail**.

Because of **sanctions** and **slow internet**, some developers even try to modify the **Dockerfile** to make it work which often leads to more errors and broken builds.  
The whole process can be painful and time-consuming.

This repository solves that problem.
All you need is a **simple download from the [Latest Release](https://github.com/karbordia/easysail/releases/latest)**, and you’re done — **no more builds**.

---

> “Run Laravel Sail **easily** — no builds, no setup, no mess.”

## ⚙️ Usage
#### 🖼️ Load Image
Completely easy and hassle-free — no builds required!

First, download the Laravel Sail version you need.

```bash
wget -P ~/Downloads https://github.com/karbordia/easysail/releases/latest/download/sail-8.x.zip
```
Or, if you want to use the mini version:
```bash
wget -P ~/Downloads https://github.com/karbordia/easysail/releases/latest/download/sail-8.x-mini.zip
```

> 💡 In this example, we’re using **sail-8.4**.

The extracted `.tar` file is the prebuilt Docker image, which you can import into your local Docker images using:

```bash
unzip ~/Downloads/sail-8.4.zip -d ~/Downloads
docker load -i ~/Downloads/sail-8.4/sail-8.4.tar
```

🔽 The output should look like this:

```bash
$ docker load -i ~/Downloads/sail-8.4/sail-8.4.tar
d05aa0ce0c21: Loading layer   2.56kB/2.56kB
9e89562f7150: Loading layer  3.072kB/3.072kB
............................................
53eb959af5ca: Loading layer  4.608kB/4.608kB
1e1ed732bab1: Loading layer  4.096kB/4.096kB
Loaded image: sail-8.4:latest
$
```

#### 💻 Using Command Prompt

You can use the container’s command prompt to create your Laravel project.

> 💡 **Tip:**
> If you're using the **mini** version, use `sail-8.4/app-mini:latest` instead of `sail-8.4/app:latest` for your Docker command.

```bash
$ mkdir -p ~/Documents/laravel_sail
$ cd ~/Documents/laravel_sail
$ PROJECT_NAME=example-app
$ docker run -u "$(id -u):$(id -g)" \
--rm -it --entrypoint "/bin/bash" \
-v "$PWD:/var/www/html" sail-8.4/app:latest \
-c "composer create-project laravel/laravel $PROJECT_NAME && cd $PROJECT_NAME && composer require laravel/sail --dev && php artisan sail:install"
```

> 💡 **Tip:**
> If you're using the **mini** version, open your `compose.yml` file and change the image name from `sail-8.x/app` to `sail-8.x/app-mini`.

```bash
$ cd $PROJECT_NAME
$ vendor/bin/sail up -d
$ vendor/bin/sail artisan migrate
```

Open **127.0.0.1:80** in your browser and enjoy Laravel.

#### 🚀 Existing Laravel Project Serving

If you want to run an existing Laravel project using Sail, follow these steps:

```bash
$ ls
app      bootstrap      composer.lock  database      phpunit.xml  README.md  routes   tests   vite.config.js
artisan  composer.json  config         package.json  public       resources  storage  vendor
```

This is an existing Laravel project that was running without Sail.
We want to run it using Sail.

First, check the PHP version of the project.

```bash
$ cat composer.json | grep "\"php\":"
        "php": "^8.2",
```

So we can use PHP 8.2 or higher.
Let's go ahead and use 8.4.
Run the following command in the root of your Laravel project.

> 💡 **Tip:**
> If you're using the **mini** version, use `sail-8.4/app-mini:latest` instead of `sail-8.4/app:latest` for your Docker command.

```bash
$ docker run -u "$(id -u):$(id -g)" \
--rm -it --entrypoint "/bin/bash" \
-v "$PWD:/var/www/html" sail-8.4/app:latest \
-c "composer require laravel/sail --dev && php artisan sail:install"
```

> 💡 **Tip:**
> If you're using the **mini** version, open your `compose.yml` file and change the image name from `sail-8.4/app` to `sail-8.4/app-mini`.

```bash
$ vendor/bin/sail up -d
$ vendor/bin/sail artisan migrate
```