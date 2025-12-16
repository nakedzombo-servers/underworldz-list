# Underworldz ARK Survival Ascended Server Configuration

**Website:** [https://underworldz.net/](https://underworldz.net/)

This repository contains centralized player management configuration files for the **Underworldz ARK Survival Ascended (ASA)** dedicated gaming servers. These text files store EOS (Epic Online Services) IDs and are dynamically loaded by the game servers via URL, enabling real-time updates across all server instances without requiring restarts.

---

## Table of Contents

- [Overview](#overview)
- [How It Works](#how-it-works)
- [Directory Structure](#directory-structure)
- [File Descriptions](#file-descriptions)
  - [Access Control](#access-control)
  - [Roles](#roles)
  - [Moderation](#moderation)
  - [Messages](#messages)
  - [Discord Integration](#discord-integration)
- [EOS ID Format](#eos-id-format)
- [Usage](#usage)
- [Contributing](#contributing)

---

## Overview

ARK Survival Ascended servers can load player lists from remote URLs, allowing server administrators to manage player access, permissions, and bans from a single centralized location. When a player joins or an action is taken, the server fetches the latest version of these files, ensuring all changes take effect immediately across the entire server cluster.

This system is used by Underworldz to:
- Manage banned players across all servers simultaneously
- Grant admin and moderator privileges
- Control whitelist and exclusive access
- Handle VIP and donator perks
- Integrate with Discord for role-based access

---

## How It Works

1. **Centralized Management**: All configuration files are stored in this repository and hosted via a publicly accessible URL
2. **Dynamic Loading**: ARK servers are configured to fetch these files from the raw GitHub URL (or a custom CDN)
3. **Real-Time Updates**: When files are updated and pushed to the repository, all servers will pull the latest version on their next check
4. **No Restart Required**: Changes to player lists take effect without needing to restart the game servers

### Server Configuration Example

In your server's `GameUserSettings.ini` or command line, you can point to these files:

```ini
BanListURL=https://raw.githubusercontent.com/[username]/underworldz-txt-files/main/asa-config/moderation/BannedPlayers.txt
```

---

## Directory Structure

```
asa-config/
├── access/                    # Player access control lists
│   ├── AllowedPlayerIDs.txt   # Players explicitly allowed to join
│   ├── ExclusiveJoin.txt      # Exclusive access list (when server is in exclusive mode)
│   ├── ReservedSlots.txt      # Players with reserved server slots
│   └── Whitelist.txt          # Whitelisted players
│
├── discord/                   # Discord integration files
│   ├── DiscordWhitelist.txt   # Discord-linked whitelist
│   └── RoleAccess.txt         # Discord role to server access mapping
│
├── messages/                  # Server message configurations
│   ├── ExclusiveJoinMessage.txt  # Message shown when server is exclusive
│   └── JoinMessages.txt       # Custom join messages
│
├── moderation/                # Ban and moderation lists
│   ├── BannedPlayers.txt      # Permanently banned players
│   └── TempBans.txt           # Temporarily banned players
│
└── roles/                     # Player role assignments
    ├── Admins.txt             # Server administrators (full access)
    ├── Donators.txt           # Players who have donated
    ├── Moderators.txt         # Server moderators
    ├── Staff.txt              # General staff members
    └── VIP.txt                # VIP players
```

---

## File Descriptions

### Access Control

| File | Purpose |
|------|---------|
| `AllowedPlayerIDs.txt` | Master list of EOS IDs for players explicitly allowed to join the servers |
| `Whitelist.txt` | Standard whitelist - only players in this list can join when whitelist mode is enabled |
| `ExclusiveJoin.txt` | Used when the server is in exclusive mode (e.g., during events or maintenance) |
| `ReservedSlots.txt` | Players who have guaranteed slots even when the server is full |

### Roles

| File | Purpose |
|------|---------|
| `Admins.txt` | Full server administrators with complete access to all commands |
| `Moderators.txt` | Moderators who can kick, ban, and manage players |
| `Staff.txt` | General staff members with limited administrative capabilities |
| `VIP.txt` | VIP players with special perks (queue priority, cosmetics, etc.) |
| `Donators.txt` | Players who have financially supported the server |

### Moderation

| File | Purpose |
|------|---------|
| `BannedPlayers.txt` | Permanently banned players - cannot join any Underworldz server |
| `TempBans.txt` | Temporarily banned players with expiration dates |

### Messages

| File | Purpose |
|------|---------|
| `JoinMessages.txt` | Custom messages displayed to players when they join |
| `ExclusiveJoinMessage.txt` | Message shown to players when they cannot join due to exclusive mode |

### Discord Integration

| File | Purpose |
|------|---------|
| `DiscordWhitelist.txt` | Players who have linked their Discord and are whitelisted |
| `RoleAccess.txt` | Mapping between Discord roles and server access levels |

---

## EOS ID Format

All player identifiers use the **Epic Online Services (EOS) ID** format. EOS IDs are 32-character hexadecimal strings that uniquely identify each player.

### Format Example
```
0002a10186d9414496bf20d22d3860ba
```

### File Format
Each file contains one EOS ID per line:
```
0002a10186d9414496bf20d22d3860ba
0002b20297e0525507cg31e33e4971cb
0002c30308f1636618dh42f44f5082dc
```

**Notes:**
- Lines starting with `#` are treated as comments
- Empty lines are ignored
- EOS IDs are case-insensitive

---

## Usage

### Adding a Player to a List

1. Obtain the player's EOS ID from the server logs or admin panel
2. Open the appropriate `.txt` file
3. Add the EOS ID on a new line
4. Commit and push the changes
5. The server will automatically pick up the changes

### Banning a Player

1. Add the player's EOS ID to `asa-config/moderation/BannedPlayers.txt`
2. Optionally add a comment with the reason:
   ```
   # Banned for cheating - 2024-01-15
   0002a10186d9414496bf20d22d3860ba
   ```
3. Commit and push - the ban takes effect immediately

### Granting Admin Access

1. Add the player's EOS ID to `asa-config/roles/Admins.txt`
2. Commit and push
3. The player will have admin access on their next login

---

## Contributing

This repository is maintained by the Underworldz server administration team. If you need to request changes:

1. Contact a server administrator via Discord
2. Provide your EOS ID and the nature of your request
3. An admin will review and make the appropriate changes

**For Server Admins:**
- Always double-check EOS IDs before adding them to any list
- Use comments to document the reason for bans
- Test changes on a single server before deploying cluster-wide if possible

---

## Links

- **Website:** [https://underworldz.net/](https://underworldz.net/)
- **Discord:** Join our community for support and updates

---

*This repository is part of the Underworldz ARK Survival Ascended server infrastructure.*
