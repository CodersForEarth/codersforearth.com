---

<p align="center">
  <a href="https://nsustain.com">
    <img alt="logo" src="https://raw.githubusercontent.com/Nsustain/.github/main/logo/logo-github.png" width="350">
  </a>
</p>


---

<p align="center">
  <a href="https://github.com/Nsustain/nsustain.com/graphs/contributors">
    <img alt="List of contributors page" src="https://img.shields.io/github/contributors/Nsustain/nsustain.com">
  </a>
  <a href="https://github.com/Nsustain/nsustain.com/blob/main/LICENSE">
    <img alt="Apache License 2.0" src="https://user-images.githubusercontent.com/19341857/184765929-fec61d10-d714-488e-94c7-153e00070a2d.svg">
  </a>
</p>

---

<br>
<br>
<br>

<p align="center">
  <b>
    Source code for
    <a href="https://nsustain.com">Nsustain.com</a>
  </b>
</p>

This repository shows you how to run it and
how it works. Read the whole documetation
if you'd like to get an overall understanding of
how Nsustain works. If, however, you're just trying
to spin up a development server as easily as possible,
just read the first section.

<br>
<br>

## Getting Started
[1.](#1-how-to-spin-up-a-developmental-server) How to spin up a development server<br>
[2.](#2-how-to-set-up-a-production-server) How to set up a production server<br>
&#160;&#160;&#160;&#160;[A.](#docker-compose-way) Docker Compose way<br>
&#160;&#160;&#160;&#160;[B.](#kubernetes-way) Kubernetes way<br>
[3.](#3-how-we-deploy-nsustaincom) How we deploy Nsustain.com

<br>
<br>

## 1. How to spin up a developmental server

Assuming you're a developer trying to test out
Nsustain's source code, we're going to
show you how to run a development server
in the fastest way possible so that you
can tinker it with as soon as possible ⚡

<br>

***Install***<br>
```bash
sudo dnf install -y git
git clone https://github.com/Nsustain/nsustain.com.git
# Install Docker Engine and Docker Compose
# Remove the comments, unless absolutely necessary
```

<br>

***Build and run***<br>
```bash
cd nsustain.com/src/docker
docker compose up
```

Usually, it takes our eight-years-old laptop
around 80 seconds to complete this process.
We know that the build process is complete
when it prints out "[INFO] Starting nginx"

Open your web browser and then type in
`https://127.0.0.1`. That's it!

[Insert screenshot]

<br>

***Default admin ID and password***<br>
The default admin ID is `nim3594` and
the password `369FQUv4eS`.

The default admin ID and the password
are baked inside our docker image.
On one hand, this is good because
we can spin up a development server fast 
this way, without having to
go through the process of
setting up every configuration.

On the other hand, this is a security hazard.
Never use this in your production server,
since the admin ID and password are
publically available right here.

<br>

***How to stop***<br>
```bash
# Press <Ctrl + c> on your keyboard

# Use docker compose to stop
docker compose down
```

<br>

***How to restart***<br>
```bash
cd nsustain.com/src/docker
docker compose up -d
```

<br>
<br>

## 2. How to set up a production server

***Difference between the development server and [Nsustain.com](https://nsustain.com)***<br>
Default env variables...

### Docker Compose way

### Kubernetes way

### [come up with a new name]

***How to debug***<br>
```bash

```

***How to install an extension***<br>
Flarum extensions are available at
https://extiverse.com/ which is created by
one of Flarum core developers.
You can install them with
```bash

```

<br>
<br>

## 3. How Nsustain.com was made

Read this section if you'd like to get a
general big picture of how Nsustain works.

Flarum, php, Mithrill.js,
MariaDB, PHP-FPM, Nginx, and
Flarum extensions

How we started from DigitalOcean
Droplet with Docker Compose, but then
decided to migrate to IBM Cloud
Kubernetes. How we used Kompose to
convert our 
`nsustain.com/src/docker/compose.yaml`
into Kubernetes objects.

How we used IBM Cloud load balancer and
Cloudflare tunnels to connect our Kubernetes
load balancer to our domain name Nsustain.com

<br>
<br>

<!--

We run Nsustain on Kubernetes, but
you can slow run Nsustain on
Docker Compose. If your host is
a single computer, then
Docker Compose is better suited.
If you want to use two or more
hosts, then run on Kubernetes.

# ----------------
# October 24, 2022
1. How to spin up a development server
2. How to host your production server

2.1 if you're using only one server host:
Docker Compose Method
General description of this method

2.2 if you're using two or more servet hosts:
Kubernetes Method
Describe what this method looks like and
my personal explanation of this method

3. How we deploy [Nsustain.com](https://Nsustain.com)
We got the domain name nsustain.com from Google Domains.
When we first started, we hosted on a DigitalOcean droplet:
 - Ubuntu 22.04 (LTS) x64, 1 vCPU, 1GB RAM, 10GB SSD ($6 per month)
 - Backups service on ($1.2 per month)

Since ... We then migrated to IBM Cloud Kubernetes because ...
 - Two worker nodes, each containing 2 vCPU, 4GB RAM, and 125GB SSD ($166 per month but first for the first month because of the $200 sign-ups credit)

*. Explanation on how it works
 - where does it begin and where does it end
 - folder structure and how everything works with each other
# ----------------

1.1 ...
### Install Docker
Source: https://docs.docker.com/compose/install/linux/#install-using-the-repository

We use Fedora Linux. If you're using any other opearting system,
Docker installation guide for outher operating systems is at
https://docs.docker.com/compose/install/linux/#install-using-the-repository
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager \
         --add-repo \
         https://download.docker.com/linux/fedora/docker-ce.repo

1. 2 if you're setting up SSL:


# Run a shell inside the docker container
docker compose exec -it flarum sh

# Run certbot. It automatically generates a certificate for you
certbot

# Change flarum setting
cd /var/www/html/flarum
vim config.php
<Change 'uri' => 'http://nsustain.com' to 'uri' => 'https://nsustain.com'>
<Ctrl + d in order to log out of the docker exec session>
cd /nsustain.com/src/docker
vim .envflarum
<Change FORUM_URL="http://nsustain.com" => FORUM_URL="https://nsustain.com">

# Reset flarum
php flarum cache:clear
php flarum assets:publish

How to renew the certificate:
https://eff-certbot.readthedocs.io/en/stable/using.html#renewing-certificates


1.1.2 How to add Flarum extension
cd nsustain.com/src/docker
docker compose exec -it flarum sh
composer require fof/sitemap
-->




**Getting a domain from a domain registrar**<br>

Our domain name
**[[Nsustain.com](nsustain.com)]**
costs $12 per year.

**(Optional) Setting up a custom-domain email forwarding service
[[Source](https://forwardemail.net/en/faq#how-do-i-get-started-and-set-up-email-forwarding)]**<br>

One way of doing this would be setting up an
email server on the VPS we just got, but
we didn't need such complexity. We didn't
need to have multiple email accounts.
We could just use one email account.
All our email needs were such that just using an email
forwarding service would solve all of them.

**Setting up remote caching and DDoS protection
[[Source](https://blog.prutser.net/2021/01/20/how-to-securely-self-host-a-website-or-web-app/)]**

It also takes care of issuing SSL certificates.

The traffic between the user and Cloudflare
is automatically SSL encrypted, but the traffic
between Cloudflare and our server needs one
extra step to be SSL encrypted -- i.e.
download the "Cloudflare-issued SSL certificate"
on their settings and install it in our server.

<br>
<br>

<p align="center">
  <b>Repository Folder Structure</b>
</p>

```bash
# This output, by the way, can be obtained
# with the `tree` command
├──                       #
├──                       #
├──                       #
├──                       #
├── LICENSE               # details on our Apache License
├── NOTICE.md             # `...`'s MIT License
└── README.md             # file you're reading now. Documentation goes here
```

Explanation of every folder

<br>
<br>
<br>

<p align="center">
  <b>What next?</b>
</p>

If you have a question, please reach out
to Soobin Rho &lt;soobinrho@nsustain.com&gt;.
If you'd like to contribute,
[Contribution Guidelines](https://github.com/Nsustain/nsustain.com/blob/main/.github/CONTRIBUTING.md)
would be a good starting point.

[Security Hall of Frame](./HALL-OF-FRAME.md)
is dedicated for those who helped us
make Naustain a better, safer place.
If you found a vulnerability,
please email security@nsustain.com

<br>
<br>
<br>

<!-- Summary example
<details>
<summary>lsp finder</summary>

<div align='center'>
<img
src="https://user-images.githubusercontent.com/41671631/181253960-cef49f9d-db8b-4b04-92d8-cb6322749414.png" />
</div>
</details>
-->
