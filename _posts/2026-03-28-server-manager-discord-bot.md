---
layout: post
title: "server-manager-discord-bot"
date: 2026-03-28 09:27:52 +0000
categories: projects
excerpt: "ServerManager 🎯 – Your All‑In‑One Discord Server Automation Bot ! ServerManager Logo (LOGO.svg) I..."
---

# ServerManager 🎯 – Your All‑In‑One Discord Server Automation Bot  

![ServerManager Logo](LOGO.svg)

I built **ServerManager** to take the grunt work out of Discord server setup and moderation. Whether you’re launching a brand‑new community, revamping an old server, or just need reliable moderation tools, this bot gives you a single command to create a polished structure, manage members, and keep the vibe friendly.

---

## Why I Created ServerManager  

Running a growing Discord community means constantly juggling channels, roles, and welcome messages.  
I wanted a solution that:

* **Creates a full server layout with one command** – no manual channel creation.  
* **Handles routine moderation** (kick, ban, mute, warn) without third‑party bots.  
* **Lets admins broadcast anonymous messages** for announcements or tests.  
* **Is fully customizable** through JSON templates so each community can have its own look and feel.

---

## Core Features at a Glance  

| 🎯 Feature | What It Does |
|-----------|--------------|
| `!setup` | Builds an entire server from a JSON template (optional `--name` flag to rename the guild). |
| `.say` | Sends an anonymous message and instantly deletes the command (admin‑only). |
| `!welcomechannel` | Toggles a friendly embed welcome for new members in the current channel. |
| `!invite` | Returns the bot’s invite link in an instant. |
| `!help` | Lists every available command with usage examples. |
| **Dynamic Server Names** | Customize the server name on the fly with `--name`. |
| **Custom Templates** | Drop your own JSON files into `templates/` and let the bot spin them up. |
| **Moderation Suite** | Kick, ban, mute, warn, unmute, unban – all with one‑line commands. |
| **Warning System** | Automatic auto‑kick after three warnings. |
| **Full‑Permission Mode** | Runs with Administrator rights for seamless channel/role management, or with fine‑grained permissions if you prefer. |

---

## Getting Started – From Zero to Bot in Minutes  

1. **Add ServerManager to Your Server**  
   Click the badge below, grant Administrator access, and the bot will appear in your member list.  

   [![Discord Invite](https://img.shields.io/badge/Discord-Invite_ServerManager-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/api/oauth2/authorize?client_id=1486709634982088744&permissions=8&scope=bot)

2. **Clone & Install (if you want to host it yourself)**  

   ```bash
   git clone https://github.com/Evilman34/template-bot.git
   cd template-bot
   npm install
   ```

3. **Create a `.env` file** with your bot token  

   ```
   DISCORD_TOKEN=YOUR_BOT_TOKEN_HERE
   ```

4. **Enable Privileged Intents** in the Discord Developer Portal  
   *Message Content Intent* and *Server Members Intent* are required for welcome messages and moderation.

5. **Launch the bot**  

   ```bash
   npm start
   ```

6. **Test it out**  

   ```text
   !ping
   !help
   ```

   If the bot replies, you’re ready to automate!

---

## Command Cheat Sheet  

### Public Commands  

| Command | Description | Example |
|---------|-------------|---------|
| `!ping` | Verify the bot is online | `!ping` |
| `!help` | Show every command with usage | `!help` |
| `!invite` | Get the invite URL | `!invite` |

### Admin‑Only Commands  

| Command | Description | Example |
|---------|-------------|---------|
| `!setup [template] [--name "Name"]` | Build server from a template (default if omitted) | `!setup rimel.json --name "My Server"` |
| `.say <message>` | Post an anonymous message (command deleted) | `.say Welcome to the server!` |
| `!welcomechannel` | Turn welcome embeds on/off in the current channel | `!welcomechannel` |

### Moderation Commands (Admin Only)  

| Command | Description | Example |
|---------|-------------|---------|
| `!kick <@user> [reason]` | Kick a member | `!kick @spamuser Spamming` |
| `!ban <@user> [reason]` | Ban a member | `!ban @troll Harassment` |
| `!unban <user-id>` | Re‑invite a banned user by ID | `!unban 123456789012345678` |
| `!warn <@user> [reason]` | Issue a warning (3 → auto‑kick) | `!warn @noisy Noise` |
| `!warns <@user>` | View a user’s warning count | `!warns @noisy` |
| `!mute <@user> [duration]` | Mute for 1m/1h/1d (default 10m) | `!mute @chatty 1h` |
| `!unmute <@user>` | Remove mute | `!unmute @chatty` |

---

## Templates – The Heart of ServerManager  

A template is a simple JSON file that describes **categories**, **channels**, and **roles**. Drop any number of template files into the `templates/` folder and use them with `!setup`.

### Built‑In Templates  

| Template | Ideal For |
|----------|-----------|
| `default.json` | A basic community with General, Support, and Voice sections. |
| `template.json` | A showcase‑heavy server for Template Bot users, with dedicated showcase and support channels. |

### Creating Your Own Template  

Here’s the skeleton you need to follow (saved as `templates/my-template.json`):

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
          "topic": "Welcome to our community",
          "initialMessage": "🎉 **Welcome!** Introduce yourself below."
        },
        {
          "name": "voice-chat",
          "type": "voice"
        }
      ]
    }
  ],
  "roles": [
    {
      "name": "Admin",
      "color": "#FF0000",
      "permissions": ["administrator"]
    },
    {
      "name": "Member",
      "color": "#808080",
      "permissions": []
    }
  ]
}
```

> **Pro tip:**  
> * Prefix categories with emojis for instant visual cues.  
> * Keep channel names lowercase and hyphen‑separated (`general-chat`).  
> * Add an `initialMessage` to each text channel to explain its purpose right away.

### Full‑Featured Gaming Template Example  

```json
{
  "categories": [
    {
      "id": "general",
      "name": "💬 General",
      "channels": [
        {"name": "welcome", "type": "text", "topic": "Intro & rules", "initialMessage": "👋 **Welcome!** Read the rules and say hi!"},
        {"name": "announcements", "type": "text", "topic": "Server news", "initialMessage": "📢 **Announcements**"},
        {"name": "general-chat", "type": "text", "topic": "Casual chat", "initialMessage": "💬 **General Chat**"}
      ]
    },
    {
      "id": "games",
      "name": "🎮 Games",
      "channels": [
        {"name": "valorant", "type": "text", "topic": "Valorant LFG", "initialMessage": "🎯 **Valorant**"},
        {"name": "valorant-voice", "type": "voice"},
        {"name": "minecraft", "type": "text", "topic": "Minecraft talk", "initialMessage": "⛏️ **Minecraft**"}
      ]
    },
    {
      "id": "voice",
      "name": "🎙️ Voice",
      "channels": [
        {"name": "hangout", "type": "voice"},
        {"name": "gaming", "type": "voice"}
      ]
    }
  ],
  "roles": [
    {"name": "Owner", "color": "#FF0000", "permissions": ["administrator"]},
    {"name": "Moderator", "color": "#0099FF", "permissions": ["moderateMembers","manageMessages"]},
    {"name": "Streamer", "color": "#FF00FF", "permissions": []},
    {"name": "Member", "color": "#808080", "permissions": []}
  ]
}
```

Deploy it with:

```text
!setup my-template.json --name "Epic Gaming Hub"
```

---

## Real‑World Use Cases  

- **Community Launches** – Instantly provision a clean hierarchy (rules, announcements, voice rooms) for a brand‑new Discord.  
- **Gaming Guilds** – Pre‑built game‑specific categories, LFG channels, and role tiers for clan hierarchy.  
- **Support & Help Desks** – Template with ticket channels, FAQ sections, and a moderator role for quick response.  
- **Streamer Hubs** – Auto‑create “Live” voice rooms, subscriber roles, and promotion channels.  
- **Education Groups** – Separate categories for lectures, labs, and study groups, each with its own voice channel.  

Because templates are just JSON files, any niche can be served with a few lines of configuration.

---

## Permissions & Security  

ServerManager prefers the **Administrator** permission for a frictionless experience, but you can also grant the minimal set:

- Manage Channels
- Manage Roles
- Send Messages / Read Message History
- Manage Guild (for server name changes)

Make sure the **Message Content** and **Server Members** intents are enabled; otherwise welcome messages and moderation commands will silently fail.

---

## Contributing & Extending  

I welcome community contributions! If you have a fresh template idea, a bug fix, or a new feature:

1. Fork the repository.  
2. Add your template under `templates/` or open a PR for code changes.  
3. Submit an issue if you discover a problem or have a feature request.

The project is MIT‑licensed, so feel free to remix, share, or embed ServerManager into larger bot ecosystems.

---

## Where to Find ServerManager  

I’ve listed the bot on the major Discord bot directories to make discovery easy:

- **[top.gg](https://top.gg/)**  
- **[discord.bots.gg](https://discord.bots.gg/)**  
- **[discordbotlist.com](https://discordbotlist.com/)**  

These pages include ratings, usage statistics, and a quick “Add to Server” button.

---

## Final Thoughts  

ServerManager turned my chaotic server‑setup process into a single command line. If you’re tired of manually creating categories, assigning permissions, and writing welcome messages, give this bot a spin. With a handful of templates and a few admin commands, your Discord can go from empty shell to fully‑featured community in seconds.

*Made with ❤️ by Evilman34*  

[![GitHub](https://img.shields.io/badge/GitHub-View_Repository-181717?style=flat-square&logo=github)](https://github.com/Evilman34/template-bot)  
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)  