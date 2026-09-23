# Inception

A Docker infrastructure project developed as part of the 42 curriculum.

The goal is to build a small multi-container web stack from individual Dockerfiles instead of relying on pre-built application images.

## Architecture

```text
                    HTTPS :443
                        │
                     Nginx
                        │
                    WordPress
                        │
                     MariaDB
```

The three services communicate through a dedicated Docker network.

Persistent data is stored on the host through bind-mounted Docker volumes:

```text
~/data/
├── mariadb/
└── wordpress/
```

## Services

| Service | Role |
| --- | --- |
| **Nginx** | HTTPS entry point and web server |
| **WordPress** | PHP-FPM application |
| **MariaDB** | Persistent database |

## Configuration

Copy the example environment file:

```bash
cp srcs/.env.example srcs/.env
```

Then replace every placeholder value before starting the stack.

Private environment files are intentionally excluded from version control.

## Usage

Build and start everything:

```bash
make
```

Useful commands:

```bash
make build
make up
make down
make status
make check
make clean
make fclean
make re
```

The Docker Compose configuration creates the required local data directories and starts the services on the `inception_network` bridge network.

## What this project demonstrates

Inception is less about WordPress itself than about infrastructure boundaries: image construction, container lifecycle, networking, persistent data, environment configuration and service dependencies.

It also reinforces an important distinction between containers and virtual machines: containers isolate processes while sharing the host kernel, making them much lighter than running a full operating system for every service.

## Security note

Secrets and passwords must stay outside the repository. The tracked `.env.example` contains placeholders only and is intended as a template.

---

Part of my developer portfolio: **[github.com/Overflow-ADW](https://github.com/Overflow-ADW)**  
Professional work: **[Avenue du Web](https://avenueduweb.be)**
