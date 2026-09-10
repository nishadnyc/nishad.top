---
layout: post
title: "server-manager-discord-bot"
date: 2026-03-28 09:27:52 +0000
categories: projects
excerpt: "ServerManager – The All‑in‑One Discord Server Automation Bot ! ServerManager Logo (https://raw.gith..."
---

# ServerManager – The All‑in‑One Discord Server Automation Bot  

![ServerManager Logo](https://raw.githubusercontent.com/Evilman34/template-bot/main/LOGO.svg)

## What Is ServerManager?

ServerManager is a lightweight Discord bot designed to automate the creation and moderation of Discord servers. With a single command, it can spin up a fully‑structured community—complete with categories, channels, roles, and welcome messages—based on reusable JSON templates. It also provides a suite of moderation tools, anonymous announcements, and dynamic server‑name handling, making it ideal for anyone who wants a clean, organized Discord community without manual setup.

## Why Use ServerManager?

- **Speed:** Deploy an entire server layout in seconds instead of minutes of manual channel/role creation.  
- **Consistency:** Templates guarantee the same structure across multiple servers, preserving branding and organization.  
- **Moderation:** Integrated kick/ban/mute/ warning system reduces the workload on human moderators.  
- **Flexibility:** Create custom templates to fit niches ranging from gaming clans to professional workspaces.  

## Core Features  

| Feature | Description | Example |
|---|---|---|
| **`!setup`** | Generates a complete server layout from a JSON template. Supports a `--name` flag to rename the server on‑the‑fly. | `!setup gaming.json --name "Pixel PvP"` |
| **`.say`** | Sends an anonymous message on behalf of an admin, then deletes the command for privacy. | `.say Welcome to the tournament!` |
| **`!welcomechannel`** | Toggles welcome embeds in the current channel, greeting new members automatically. | `!welcomechannel` |
| **`!invite`** | Returns the bot’s OAuth2 invite link (full permissions). | `!invite` |
| **`!help`** | Lists every public and admin command with short descriptions. | `!help` |
| **Dynamic Server Names** | Rename the guild instantly using the `--name` flag with `!setup`. | `!setup default.json --name "Study Hub"` |
| **Custom Templates** | Add your own JSON files to the `templates/` folder to define categories, channels, and roles. | `!setup my‑template.json` |
| **Moderation Toolkit** | Kick, ban, mute, and warn members; auto‑kick after three warnings. | `!warn @user spamming` |
| **Warning System** | Tracks warnings per user; after three infractions, the bot automatically kicks the offender. | `!warns @user` |

### Additional Public Commands  

- `!ping` – Checks bot latency.  
- `!help` – Shows an overview of all commands.  

### Admin‑Only Moderation Commands  

- `!kick <@user> [reason]`  
- `!ban <@user> [reason]`  
- `!unban <user‑id>`  
- `!warn <@user> [reason]`  
- `!warns <@user>`  
- `!mute <@user> [duration]` (default 10 min)  
- `!unmute <@user>`  

## How It Works  

### 1. Add the Bot to Your Server  

Click the **Discord Invite** badge at the top of this article (or use the link below) and authorize ServerManager with Administrator permissions.  

[Invite ServerManager](https://discord.com/api/oauth2/authorize?client_id=1486709634982088744&permissions=8&scope=bot)

### 2. Enable Required Gateway Intents  

In the Discord Developer Portal, enable **Message Content Intent** and **Server Members Intent** for the bot to read messages and welcome new members.

### 3. Set Up Locally (Optional)  

If you want to host your own instance:

```bash
git clone https://github.com/Evilman34/template-bot.git
cd template-bot
npm install
# Create a .env file with your bot token
echo "DISCORD_TOKEN=YOUR_TOKEN_HERE" > .env
npm start
```

Node.js v16+ and npm (or yarn) are required.

### 4. Run the Setup Command  

```text
!setup <template-file> [--name "New Server Name"]
```

- **Default template:** `!setup` (creates a minimal community).  
- **Custom template:** `!setup my-template.json --name "My Community"`  

The bot reads the JSON template, creates categories, channels, assigns roles, and posts any *initialMessage* fields.

### 5. Manage the Server  

- Use `.say` for anonymous announcements.  
- Toggle welcome embeds with `!welcomechannel`.  
- Moderate with the kick/ban/mute commands.  

## Creating & Using Custom Templates  

Templates live in `templates/` and follow a simple JSON schema:

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
          "topic": "Introduce yourself",
          "initialMessage": "👋 Welcome to the server!"
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
      "name": "Moderator",
      "color": "#0099FF",
      "permissions": ["moderateMembers", "manageMessages"]
    }
  ]
}
```

**Tips for effective templates**

- Prefix category names with emojis for instant visual cues.  
- Keep channel names lowercase, hyphen‑separated (`general-chat`).  
- Add a helpful *initialMessage* to orient newcomers.  
- Use distinct hex colors for role differentiation.  
- Test locally with `!setup your-template.json --name "Test Server"` before publishing.

## Real‑World Use Cases  

| Scenario | How ServerManager Helps |
|---|---|
| **Gaming Clan** | Deploy a "Games" category with game‑specific text/voice channels, assign roles like *Owner* and *Streamer*, and auto‑welcome new recruits. |
| **Study Group / Academic Server** | Create a "Resources" category with channels for notes, assignments, and voice rooms for study sessions; use the warning system to keep discussions on‑topic. |
| **Corporate Community** | Generate a professional layout with *Announcements*, *HR*, *Project‑X* channels, and role‑based permissions for managers vs. staff. |
| **Event / Tournament Hub** | Spin up a temporary server with *Sign‑up*, *Bracket*, and *Live‑Chat* channels, then tear it down after the event by simply deleting the server. |
| **Open‑Source Project** | Provide a ready‑made environment for contributors: *Code‑Help*, *Bug‑Reports*, *Voice‑Dev* channels, plus a *Contributor* role that can be granted automatically. |

## Permissions Required  

- **Administrator** (simplest) – grants full control.  
- Or granular: `Manage Channels`, `Manage Roles`, `Send Messages`, `Read Message History`, `Manage Guild`.

## Troubleshooting at a Glance  

- **Bot silent?** Verify Administrator permission and that gateway intents are enabled.  
- **`!setup` fails** – Ensure the template file exists, JSON syntax is correct, and the bot can create/delete channels/roles.  
- **Welcome embeds missing** – Confirm the Server Members intent is active and that `!welcomechannel` was run in the target channel.  
- **Roles not appearing** – Check for name collisions and that the bot has the `Manage Roles` permission.  

## Getting the Bot Listed  

ServerManager is already listed on major Discord bot directories:

- **[top.gg](https://top.gg/)**  
- **[discord.bots.gg](https://discord.bots.gg/)**  
- **[discordbotlist.com](https://discordbotlist.com/)**  

Listing boosts discoverability and encourages community contributions.

## Contributing & License  

ServerManager is released under the **MIT License**—free to use, modify, and distribute. Contributions are welcome:

1. Fork the repository.  
2. Add or improve a template in the `templates/` folder.  
3. Submit a pull request or open an issue for discussion.  

## TL;DR  

- **Add:** Invite the bot with full permissions.  
- **Setup:** Run `!setup` (or a custom template) to instantly generate a polished server.  
- **Manage:** Use admin and moderation commands to keep the community safe and organized.  
- **Customize:** Build reusable JSON templates for any niche.  

ServerManager turns a blank Discord server into a thriving, well‑structured community in seconds—saving you time, reducing errors, and letting you focus on what truly matters: the people behind the chats.  

*Made with ❤️ by Evilman34*  