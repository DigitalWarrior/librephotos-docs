---
title: "🐋 Docker"
excerpt: "How to install Libre Photos using Docker and Docker Compose."
last_modified_at: 2022-05-07
category: 1
---

## Docker Compose

We recommend you use docker compose as this matches the demo and development environment the most.

### Compatibility

You need a x86 or a ARM64 processor, and it is recommended to have 4GBs of RAM. Due to limited ram & processing power ARM64 will not be as fast.

### Size

You will need at least 10 GB of HDD Space for the docker images. It needs that space because of the machine learning
models. Librephotos will also create a database and thumbnails which will need additional space.

### 🚀 Installation

Clone the repo: `git clone https://github.com/LibrePhotos/librephotos-docker.git`

Navigate to the librephotos-docker folder: `cd librephotos-docker`

Copy the template variable file (containing options such as the location of your photos): `cp librephotos.env .env`

Open `.env` in your favorite text editor and make the required changes. E.g., using nano: `nano .env`

Do not forget to create the directories you specified in the `.env` file if they do not exist.

Start LibrePhotos with `docker-compose up -d`

You should have LibrePhotos accessible after a few minutes of boot-up on [localhost:3000](http://localhost:3000)
unless you changed this in the `.env` file. The username is `admin` & the password is `admin` unless you changed them in the `.env` file.
It is recommended you change the admin username and password if LibrePhotos is going to be publicly accessible. This is done via the `.env` file.

### Updating

To update LibrePhotos when using Docker Compose, navigate to the librephotos-docker folder that was created when you installed LibrePhotos.

Then run:

```sh
docker-compose down
docker-compose pull
docker-compose up -d
```

## Docker

Overview of the folders that can be mounted as volumes:

- `/var/lib/librephotos/photos/` your actual photos
- `/var/lib/librephotos/data/protected_media/` thumbnails
- `/var/log/librephotos/` logs
- `/var/lib/postgresql/data/` database

Replace the first part that is in brackets with the actual location of the folder:

```sh
sudo docker run -v <photos>:/var/lib/librephotos/photos/ -v <thumbnails>:/var/lib/librephotos/data/protected_media -v <logs>:/var/log/librephotos/ -v <db>:/var/lib/postgresql/data -p 3000:80 -d reallibrephotos/singleton
```

If you run into any permission issue add `-e FIXPERMISSIONS=true` or change the permission to allow read/write/exectute for others of your photos folder.
