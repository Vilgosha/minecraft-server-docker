# 🎮 Minecraft Server

A Dockerized Minecraft Java Edition server (v1.20.4) using [`itzg/minecraft-server`](https://github.com/itzg/docker-minecraft-server).

---

## 📁 Repository Structure

```
.
├── docker-compose.yaml           # Container definition
├── server.properties             # Minecraft server configuration
└── server-properties-reference.md  # Description of every server.properties parameter
```

---

## 🚀 Getting Started

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd <repo-folder>
```

### 2. Place server data

The server data directory is mounted from `/home/minecraft` on the host. Make sure it exists:

```bash
sudo mkdir -p /home/minecraft
```

If you have an existing world or `server.properties`, copy them there:

```bash
sudo cp server.properties /home/minecraft/server.properties
```

### 3. Start the server

```bash
docker compose up -d
```

The server will automatically download Minecraft 1.20.4 on first run. Wait for it to become healthy before connecting.

### 4. Check server status

```bash
docker compose ps
docker compose logs -f
```

---

## ⚙️ Configuration

Server settings are managed via `/home/minecraft/server.properties` on the host (mapped to `/data/server.properties` inside the container).

To apply changes, edit the file and restart the container:

```bash
docker compose restart
```

See [`server-properties-reference.md`](./server-properties-reference.md) for a full description of every available parameter.

### Key settings at a glance

| Parameter | Value | Notes |
|-----------|-------|-------|
| Version | `1.20.4` | Vanilla Java Edition |
| Port | `25565` | Default Minecraft port |
| Max players | `8` | Edit in `server.properties` |
| Game mode | `survival` | |
| Difficulty | `normal` | |
| Online mode | `false` | Allows offline/cracked clients |
| RCON | enabled | Port `25575` |
| Memory | `4G` | Set in `docker-compose.yaml` |

---

## 🖥️ RCON (Remote Console)

RCON allows you to run server commands remotely without attaching to the container.

```bash
# Using docker exec
docker exec -i mc rcon-cli <command>

# Example: list online players
docker exec -i mc rcon-cli list
```

Or connect with any RCON client to `<server-ip>:25575` using the password from `server.properties`.

> ⚠️ **Security:** Keep your `rcon.password` out of public repositories. Consider using a `.env` file and adding `server.properties` to `.gitignore` if this repo is public.

---

## 🔧 Common Operations

### Stop the server
```bash
docker compose down
```

### Restart the server
```bash
docker compose restart
```

### View live logs
```bash
docker compose logs -f
```

### Run a server command
```bash
docker exec -i mc rcon-cli say Hello everyone!
docker exec -i mc rcon-cli op <username>
```

### Backup the world
```bash
tar -czf backup-$(date +%Y%m%d).tar.gz /home/minecraft
```

---

## 🩺 Health Check

The container includes a built-in health check using `mc-health`. It pings the server every 30 seconds with a 120-second grace period on startup. You can check the status with:

```bash
docker inspect --format='{{.State.Health.Status}}' mc
```

---

## 📜 License

This repository contains server configuration only. Minecraft itself is property of [Mojang Studios / Microsoft](https://www.minecraft.net).
