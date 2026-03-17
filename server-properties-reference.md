# Minecraft `server.properties` — Parameter Reference

All parameters listed alphabetically by section. Values shown are from your current config.

---

## 🔌 Connection & Network

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `server-ip` | *(empty)* | IP address the server binds to. Leave empty to bind to all interfaces (0.0.0.0). |
| `server-port` | `25565` | TCP port the server listens on for player connections. Default is `25565`. |
| `network-compression-threshold` | `256` | Minimum packet size (bytes) before compression is applied. `-1` disables compression, `0` compresses everything. Lower values save bandwidth at CPU cost. |
| `use-native-transport` | `true` | Enables Netty's native transport (epoll on Linux) for better network performance. |
| `prevent-proxy-connections` | `false` | If `true`, the server rejects connections via proxies/VPNs by verifying player IPs with Mojang. |
| `rate-limit` | `0` | Max packets per second from a single connection before the player is kicked. `0` = disabled. |
| `accepts-transfers` | `false` | Allows players to be transferred from another server using the Transfer packet (1.20.5+ feature). |

---

## 👤 Player & Authentication

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `online-mode` | `false` | If `true`, authenticates players with Mojang's servers (requires valid accounts). `false` allows cracked/offline clients. |
| `enforce-secure-profile` | `true` | Requires players to have a Mojang-signed public key. Prevents joining without a verified cryptographic profile. |
| `max-players` | `8` | Maximum number of players allowed online simultaneously. |
| `player-idle-timeout` | `0` | Minutes of inactivity before a player is kicked. `0` = never kick idle players. |
| `pause-when-empty-seconds` | `600` | Seconds to wait before pausing the server tick loop when no players are online. `0` = never pause. |
| `hide-online-players` | `false` | If `true`, the player list in the server status ping is hidden. |
| `log-ips` | `true` | Whether player IP addresses are written to the server log on connection. |
| `bug-report-link` | *(empty)* | URL shown to players when they report bugs via the in-game menu. Leave empty to hide the button. |

---

## 🌍 World Generation

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `level-name` | `world` | Name of the world folder. This is the directory inside `/data` where world files are saved. |
| `level-seed` | *(empty)* | Seed for world generation. Leave empty for a random seed. |
| `level-type` | `minecraft:normal` | World generator type. Options: `minecraft:normal`, `minecraft:flat`, `minecraft:large_biomes`, `minecraft:amplified`, `minecraft:single_biome_surface`. |
| `generator-settings` | `{}` | JSON settings passed to the world generator (mainly used with `minecraft:flat` or custom generators). |
| `generate-structures` | `true` | Whether villages, dungeons, temples, strongholds, etc. generate in the world. |
| `max-world-size` | `29999984` | Maximum radius (blocks) of the world border from center. Capped at `29999984` (the Minecraft hard limit). |

---

## ⚔️ Gameplay

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `gamemode` | `survival` | Default game mode for new players. Options: `survival`, `creative`, `adventure`, `spectator`. |
| `force-gamemode` | `false` | If `true`, players are switched to the default `gamemode` every time they join, overriding their saved game mode. |
| `difficulty` | `normal` | World difficulty. Options: `peaceful`, `easy`, `normal`, `hard`. |
| `hardcore` | `false` | Enables hardcore mode — players are permanently banned (spectator mode) on death. Forces `difficulty=hard`. |
| `pvp` | `true` | Allows players to damage each other. |
| `allow-flight` | `false` | If `false`, players using unapproved flight (hacked clients) are kicked. Set `true` if using flight-enabling mods/plugins. |
| `allow-nether` | `true` | Allows players to travel to the Nether dimension. |
| `spawn-animals` | `true` | Whether passive animals (cows, pigs, sheep, etc.) spawn in the world. |
| `spawn-monsters` | `true` | Whether hostile mobs (zombies, creepers, etc.) spawn in the world. |
| `spawn-npcs` | `true` | Whether villagers spawn in villages and interact with players. |
| `spawn-protection` | `16` | Radius (blocks) around the world spawn point where only ops can build/destroy. `0` = disabled. |

---

## 🏗️ Data Packs

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `initial-enabled-packs` | `vanilla` | Comma-separated list of data packs enabled when a new world is created. |
| `initial-disabled-packs` | *(empty)* | Comma-separated list of data packs disabled by default on new world creation. |

---

## ⚡ Performance & Simulation

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `view-distance` | `16` | Number of chunks sent to each player in each direction (server-side render distance). Higher values increase server load. |
| `simulation-distance` | `10` | Radius (chunks) in which mobs, redstone, and other game mechanics are actively simulated. |
| `max-tick-time` | `60000` | Maximum milliseconds a single server tick can take before the watchdog crashes the server. `-1` = disabled. |
| `max-chained-neighbor-updates` | `1000000` | Limits cascading block update chains (prevents lag from update loops). Raises a log warning if exceeded. |
| `entity-broadcast-range-percentage` | `100` | Percentage of view distance at which entities are sent to clients. Lower values reduce client load. `10`–`100`. |
| `sync-chunk-writes` | `true` | Forces synchronous chunk save operations. Safer but slower; set `false` for better I/O performance on trusted hardware. |
| `region-file-compression` | `deflate` | Compression algorithm for region files. Options: `deflate` (default), `lz4` (faster, larger), `none`. |

---

## 🔐 Permissions & Ops

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `op-permission-level` | `4` | Default permission level granted to ops. `1`=bypass spawn protection, `2`=use commands/command blocks, `3`=manage players, `4`=full server control. |
| `function-permission-level` | `2` | Permission level required to run functions (`.mcfunction` files) from data packs. |
| `enable-command-block` | `false` | Enables in-game command blocks. Disable on public servers to prevent misuse. |
| `broadcast-console-to-ops` | `true` | Sends server console output to all online operators as chat messages. |
| `broadcast-rcon-to-ops` | `true` | Broadcasts RCON command output to all online operators. |

---

## 📋 Whitelist

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `white-list` | `false` | Enables the server whitelist. Only players on the whitelist can join when `true`. |
| `enforce-whitelist` | `false` | If `true`, players not on the whitelist are kicked immediately when the whitelist is reloaded (even if already online). |

---

## 📡 Query (GameSpy4)

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `enable-query` | `false` | Enables the GameSpy4 query protocol, allowing external tools to query server status. |
| `query.port` | `25565` | UDP port for the query protocol (only used when `enable-query=true`). |

---

## 🖥️ RCON (Remote Console)

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `enable-rcon` | `true` | Enables the RCON protocol, allowing remote command execution over TCP. |
| `rcon.port` | `25575` | TCP port for RCON connections. |
| `rcon.password` | `81a4a5f6f4629889468f26ec` | Password required to authenticate RCON connections. **Keep this secret!** |

---

## 📊 Status & Monitoring

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `enable-status` | `true` | Enables the server list ping response (shows player count, MOTD, version in the multiplayer list). |
| `enable-jmx-monitoring` | `false` | Exposes server metrics via JMX (Java Management Extensions) for monitoring tools like JConsole or Prometheus JMX exporter. |
| `motd` | `₍ ˶ᵔ ᵕ ᵔ˶ ₎ ▀▄▀▄▀▄ Welcome ▀▄▀▄▀▄ ₍ ˶ᵔ ᵕ ᵔ˶ ₎` | Message of the Day shown in the multiplayer server list. Supports color codes (`§`) and Unicode. Max ~59 chars visible. |

---

## 🎨 Resource Pack

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `resource-pack` | *(empty)* | Direct URL to a `.zip` resource pack file hosted online. Players are prompted to download it. |
| `resource-pack-sha1` | *(empty)* | SHA-1 hash of the resource pack for integrity verification. Leave empty if not using a pack. |
| `resource-pack-id` | *(empty)* | UUID identifier for the resource pack (used by the client to cache it). |
| `resource-pack-prompt` | *(empty)* | Custom message shown to players when prompted to download the resource pack. Supports JSON text. |
| `require-resource-pack` | `false` | If `true`, players who decline the resource pack are kicked from the server. |

---

## 🔍 Text Filtering

| Parameter | Your Value | Description |
|-----------|------------|-------------|
| `text-filtering-config` | *(empty)* | Path to a config file for server-side text filtering (chat moderation). Primarily used with Minecraft Realms. |
| `text-filtering-version` | `0` | Internal version identifier for the text filtering system. |

---

> **Tip:** All of these can be set as environment variables in the `docker-compose.yaml` for the `itzg/minecraft-server` image — no need to manually edit `server.properties`.
