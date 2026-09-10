---
layout: post
title: "server-manager-discord-bot"
date: 2026-03-28 09:27:52 +0000
categories: projects
excerpt: "<div align='center'> ! ServerManager Logo (LOGO.svg) ServerManager 🎯 A Discord bot that handles you..."
---

<div align="center">
  
  ![ServerManager Logo](LOGO.svg)
  
  # ServerManager 🎯
  
  **A Discord bot that handles your server for you.**  
  
  <a href="https://discord.com/api/oauth2/authorize?client_id=1486709634982088744&permissions=8&scope=bot">
    <img src="https://img.shields.io/badge/Discord-Invite_ServerManager-7289DA?style=for-the-badge&logo=discord&logoColor=white" alt="Discord Invite">
  </a>
  <a href="https://github.com/Evilman34/template-bot">
    <img src="https://img.shields.io/badge/GitHub-View_Repository-181717?style=flat-square&logo=github" alt="GitHub Repository">
  </a>
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="MIT License">
  </a>
</div>

---

## What Is ServerManager?

ServerManager is a feature‑rich Discord bot that automates the creation and maintenance of community servers. By supplying a JSON template, the bot can spin up a complete server structure—including categories, channels, and roles—within seconds. It also bundles moderation tools, welcome messages, and an anonymous broadcast command, making it ideal for fast‑track community deployment.

---

## Core Benefits

| Benefit | How ServerManager Delivers It |
|---------|------------------------------|
| **One‑click setup** | `!setup` reads a JSON template and builds the entire server hierarchy automatically. |
| **Consistent branding** | Dynamic server‑name flag (`--name`) lets you rename the server while preserving the template layout. |
| **Built‑in moderation** | Kick, ban, mute, and warn commands with an auto‑kick after three warnings. |
| **Customizable welcome** | `!welcomechannel` toggles a rich embed welcome message in any text channel. |
| **Anonymous announcements** | `.say` lets admins broadcast messages without revealing the sender. |
| **Extensible templates** | Create, share, and version‑control your own community blueprints in the `templates/` folder. |

---

## Quick Installation Guide

### Prerequisites
- Node.js **v16+**
- npm **or** Yarn
- Discord bot token (create one in the [Discord Developer Portal](https://discord.com/developers/applications))

### Setup Steps
```bash
# 1️⃣ Clone the repo
git clone https://github.com/Evilman34/template-bot.git
cd template-bot

# 2️⃣ Install dependencies
npm install   # or: yarn install

# 3️⃣ Add your token
#    Create a .env file in the project root:
#    DISCORD_TOKEN=your_bot_token_here
echo "DISCORD_TOKEN=your_bot_token_here" > .env

# 4️⃣ Enable privileged intents
#    - Message Content Intent
#    - Server Members Intent
#    (do this in the Bot section of the Developer Portal)

# 5️⃣ Launch the bot
npm start
```

Once the bot is running, invite it to a server using the **Discord Invite** button above. The bot will request *Administrator* access to manage channels, roles, and messages.

---

## Command Overview

### Public Commands
| Command | Description | Example |
|--------|-------------|---------|
| `!ping` | Verify the bot is online | `!ping` |
| `!help` | List every available command | `!help` |
| `!invite` | Get the bot’s invite link | `!invite` |

### Admin & Management Commands
| Command | Description | Example |
|--------|-------------|---------|
| `!setup [template] [--name "Server Name"]` | Build a server from a JSON template | `!setup default.json --name "My Community"` |
| `.say <message>` | Send an anonymous message and delete the trigger | `.say Welcome to the server!` |
| `!welcomechannel` | Enable/disable welcome embeds in the current channel | `!welcomechannel` |

### Moderation Suite (Admin Only)
| Command | Action | Example |
|--------|--------|---------|
| `!kick <@user> [reason]` | Remove a member | `!kick @Troublemaker Spamming` |
| `!ban <@user> [reason]` | Ban a member | `!ban @Hacker Harassment` |
| `!unban <user-id>` | Re‑allow a previously banned user | `!unban 123456789012345678` |
| `!mute <@user> [duration]` | Mute a member (default 10 min) | `!mute @Noisy 1h` |
| `!unmute <@user>` | Remove mute | `!unmute @Noisy` |
| `!warn <@user> [reason]` | Issue a warning (3 warnings → auto‑kick) | `!warn @Spammer Repeated spam` |
| `!warns <@user>` | Display a user’s warning count | `!warns @Spammer` |
| `!ban <@user> [reason]` | Permanently ban a user | `!ban @Evil` |

---

## Template System – The Heart of ServerManager

### How Templates Work
A template is a JSON file placed inside `templates/`. It defines:

- **Categories** – Groupings for channels, each with an optional emoji.
- **Channels** – Text or voice channels, optional topics, and an initial welcome message.
- **Roles** – Names, hex colors, and a list of Discord permissions.

#### Minimal Template Example
```json
{
  "categories": [
    {
      "id": "general",
      "name": "💬 General",
      "channels": [
        {
          "name": "welcome",
          "type": "text",
          "topic": "Introduce yourself!",
          "initialMessage": "👋 Welcome to our community!"
        }
      ]
    }
  ],
  "roles": [
    {
      "name": "Member",
      "color": "#808080",
      "permissions": []
    }
  ]
}
```

### Built‑In Templates
| Template | Intended Community | Command |
|----------|-------------------|---------|
| `default.json` | Basic text/voice community | `!setup default.json --name "My Community"` |
| `template.json` | Template‑Bot user hub | `!setup template.json --name "Template Bot Community"` |

### Creating Your Own Blueprint
1. **Add a new JSON file** in `templates/` (e.g., `my-gaming.json`).
2. Follow the schema shown above—categories → channels → roles.
3. Test locally:

```bash
!setup my-gaming.json --name "Gaming Hub"
```

4. Commit and push to share with the world.

#### Tips for Clean Templates
- Use **lowercase, hyphenated** channel names (`general-chat`).
- Prefix categories with **emojis** for instant visual sorting.
- Keep **initial messages** short, welcoming, and context‑rich.
- Assign **distinct hex colors** to each role for quick visual cues.
- Limit the number of channels to avoid clutter; group related topics in the same category.

---

## Real‑World Use Cases

| Scenario | How ServerManager Solves It |
|----------|----------------------------|
| **Launching a new gaming clan** | Deploy a ready‑made gaming template (`!setup gaming.json`) that includes LFG channels, voice rooms, and role hierarchies. |
| **Setting up a support hub for a product** | Create a `support.json` template with ticket, FAQ, and announcements channels; enable welcome messages to guide newcomers. |
| **Running a frequent event series** | Use `.say` to broadcast event details anonymously, then mute or unmute participants as needed with the moderation commands. |
| **On‑boarding new Discord servers for a brand** | Store brand‑specific templates (logo, colors, channel naming conventions) and spin them up instantly for each new client. |
| **Community moderation with minimal staff** | Leverage the warning system—after three warnings a user is automatically kicked, reducing manual oversight. |

---

## Deploying & Sharing Templates

```bash
# After creating templates/my-template.json
git add templates/my-template.json
git commit -m "Add custom community template"
git push origin main
```

Once pushed, other server owners can run:

```bash
!setup my-template.json --name "Awesome Community"
```

You can also list your bot on popular directories to increase visibility:

- **[top.gg](https://top.gg/)**
- **[discord.bots.gg](https://discord.bots.gg/)**
- **[discordbotlist.com](https://discordbotlist.com/)**

These platforms let users discover ServerManager and instantly add it to their servers.

---

## Troubleshooting Quick Reference

| Problem | Checklist |
|----------|-----------|
| Bot doesn’t respond | • Bot has **Administrator** or required permissions.<br>• **Message Content** and **Server Members** intents enabled.<br>• Bot is online (`!ping`). |
| `!setup` fails | • Template file exists in `templates/`.<br>• JSON is valid (no trailing commas).<br>• Bot can **Manage Channels** and **Manage Roles**. |
| Welcome messages silent | • `!welcomechannel` executed in desired channel.<br>• Bot has **Send Messages** permission.<br>• **Server Members** intent is active. |
| Roles not created | • Role name isn’t already taken.<br>• Bot has **Manage Roles** permission.<br>• Role name ≤ 100 characters and color is a valid hex code. |

---

## Contributing & Community

- **Feature ideas** → Open an issue on GitHub.  
- **New templates** → Fork the repo, add your JSON file to `templates/`, and submit a pull request.  
- **Bug reports** → Include the command you ran and any error messages.

All contributions are welcomed under the **MIT License**—feel free to remix, extend, or integrate ServerManager into your own projects.

---

## License

This project is licensed under the **MIT License**. See the `LICENSE` file for full terms.

--- 

**ServerManager – Handle Your Server Automatically**  
Made with ❤️ by **Evilman34**.