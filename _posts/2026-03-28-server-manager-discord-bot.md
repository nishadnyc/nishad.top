---
layout: post
title: "server-manager-discord-bot"
date: 2026-03-28 09:27:52 +0000
categories: projects
excerpt: "ServerManager 🎯 – Automate Your Discord Server in Seconds ! ServerManager Logo (LOGO.svg) ! Discor..."
---

# ServerManager 🎯 – Automate Your Discord Server in Seconds  

![ServerManager Logo](LOGO.svg)  
[![Discord Invite](https://img.shields.io/badge/Discord-Invite_ServerManager-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/api/oauth2/authorize?client_id=1486709634982088744&permissions=8&scope=bot)  
[![GitHub](https://img.shields.io/badge/GitHub-View_Repository-181717?style=flat-square&logo=github)](https://github.com/Evilman34/template-bot)  
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## Why ServerManager?  

Managing a Discord community can be a full‑time job: you have to create categories, channels, roles, set permissions, and keep newcomers welcomed. ServerManager removes the manual grind by turning a **single command** into a fully‑fledged server structure—complete with welcome messages, moderation tools, and custom templates. The bot is ideal for:

- **New communities** that need a clean, organized start.  
- **Gaming clans, study groups, hobby clubs** that want pre‑built channel layouts.  
- **Server admins** looking for a quick way to apply consistent role permissions.  
- **Developers** who want to share their own server blueprints as JSON templates.

---

## Core Features at a Glance  

| Feature | Description |
|--------|-------------|
| `!setup` | Build an entire server from a JSON template (default, custom, or community‑provided). |
| `.say` | Send an anonymous message—perfect for announcements without revealing the author. |
| `!welcomechannel` | Turn the current text channel into a welcome hub that greets new members with a rich embed. |
| `!invite` | Instantly retrieve the bot’s invite link (full permissions). |
| `!help` | Show a tidy list of every available command. |
| Dynamic Server Names | Use the `--name` flag with `!setup` to rename the server on the fly. |
| Custom Templates | Drop a JSON file into `templates/` and let anyone spin up that exact layout. |
| Moderation Suite | Kick, ban, mute, warn, and automatically kick after three warnings. |
| Warning System | Persisted warnings that trigger auto‑kick, helping keep the community safe. |

---

## Getting Started  

### Prerequisites  

- **Node.js** v16 +  
- **npm** or **yarn**  
- A Discord Bot Token (create one in the [Discord Developer Portal](https://discord.com/developers/applications))

### Installation Steps  

```bash
# 1️⃣ Clone the repository
git clone https://github.com/Evilman34/template-bot.git
cd template-bot

# 2️⃣ Install dependencies
npm install      # or `yarn`

# 3️⃣ Configure environment variables
echo "DISCORD_TOKEN=your_bot_token_here" > .env

# 4️⃣ Enable privileged intents
#    – Message Content Intent
#    – Server Members Intent
#    (set them on the Bot page of the Developer Portal)

# 5️⃣ Launch the bot
npm start
```

Once the bot is online, use the **Discord Invite** button above to add it to your server. The bot will request **Administrator** permission, which guarantees it can create channels, roles, and manage members without additional tweaks.

---

## Command Reference  

### Public Commands  

| Command | What It Does | Example |
|---------|--------------|---------|
| `!ping` | Checks that the bot is responsive. | `!ping` |
| `!help` | Lists every command with a short description. | `!help` |
| `!invite` | Returns the bot’s OAuth2 invite link. | `!invite` |

### Admin‑Only Commands  

| Command | Description | Example |
|---------|-------------|---------|
| `!setup [template] [--name "Name"]` | Generates the full server layout from a template. | `!setup rimel.json --name "My Server"` |
| `.say <message>` | Sends an anonymous message and deletes the command message. | `.say Welcome to the community!` |
| `!welcomechannel` | Toggles welcome embeds for the current channel. | `!welcomechannel` |

### Moderation Commands (Admin Only)  

| Command | Action | Example |
|---------|--------|---------|
| `!kick <@user> [reason]` | Removes a user from the server. | `!kick @troublemaker spamming` |
| `!ban <@user> [reason]` | Bans a user permanently. | `!ban @troll harassment` |
| `!unban <user-id>` | Lifts a ban using the user’s ID. | `!unban 123456789012345678` |
| `!warn <@user> [reason]` | Issues a warning (3 warnings = auto‑kick). | `!warn @noob spam` |
| `!warns <@user>` | Shows how many warnings a user has. | `!warns @noob` |
| `!mute <@user> [duration]` | Mutes a user (default 10 min). | `!mute @noob 1h` |
| `!unmute <@user>` | Restores a muted user’s speaking rights. | `!unmute @noob` |

---

## Templates: From Built‑In to Fully Custom  

### Built‑In Templates  

| Template | Use‑Case | Command |
|----------|----------|--------|
| `default.json` | Simple community with General, Support, and Voice channels. | `!setup default.json --name "My Community"` |
| `template.json` | Dedicated space for users of the original Template Bot. | `!setup template.json --name "Template Bot Community"` |

### Crafting Your Own Template  

1. **Create a JSON file** inside the `templates/` folder (e.g., `my-gaming.json`).  
2. **Define categories**, each with an `id`, a display `name` (emoji‑prefixed recommended), and an array of `channels`.  
3. **Add channels**:  
   - **Text channels** need `name`, `type: "text"`, optional `topic`, and optional `initialMessage`.  
   - **Voice channels** need `name` and `type: "voice"`.  
4. **Specify roles** with `name`, hex `color`, and a list of permission strings (e.g., `"administrator"`).

#### Minimal Example  

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
          "topic": "Introductions and rules",
          "initialMessage": "👋 Welcome! Please read the rules and introduce yourself."
        }
      ]
    }
  ],
  "roles": [
    {
      "name": "Admin",
      "color": "#FF0000",
      "permissions": ["administrator"]
    }
  ]
}
```

#### Full‑Featured Gaming Template (excerpt)  

```json
{
  "categories": [
    {
      "id": "games",
      "name": "🎮 Games",
      "channels": [
        {
          "name": "valorant",
          "type": "text",
          "topic": "Valorant discussion and LFG",
          "initialMessage": "🎯 Find teammates and share strategies here!"
        },
        {
          "name": "valorant-voice",
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

### Best Practices  

- **Descriptive, lower‑case channel names** (use hyphens for spaces).  
- **Emojis in category names** for instant visual identification.  
- **Initial messages** that explain a channel’s purpose.  
- **Logical grouping**—keep related channels together.  
- **Consistent role colors** to differentiate ranks.  
- **Validate JSON** before deployment (`jsonlint` or VS Code’s built‑in linter).  

---

## Real‑World Use Cases  

| Scenario | How ServerManager Helps |
|----------|------------------------|
| **Gaming Clan** | Deploy a *games* category with separate voice/text rooms for each title, plus role hierarchy (Owner, Moderator, Member). |
| **Study Group** | Create a *resources* category with channels for notes, assignments, and voice study rooms. |
| **Open‑Source Project** | Spin up a *documentation* and *support* section, assign *Maintainer* and *Contributor* roles, and enable welcome embeds for new contributors. |
| **Event Organizers** | Quickly launch an *event* server with announcement, registration, and live‑chat channels; enable temporary mute/kick for disruptive participants. |
| **Community Templates Marketplace** | Publish your JSON blueprint, let other server owners import it with `!setup my‑template.json`. |

---

## Permissions & Security  

The bot functions best with **Administrator** permission, eliminating the need to manually grant each individual permission. If you prefer a principle‑of‑least‑privilege approach, ensure the bot has at least:

- **Manage Channels**  
- **Manage Roles**  
- **Send Messages** & **Read Message History**  
- **Manage Guild** (for server name changes)  

**Privileged Gateway Intents** must be enabled in the Discord Developer Portal:

- **Message Content Intent** – required for `.say` and command parsing.  
- **Server Members Intent** – required for welcome messages and member‑based moderation.

---

## Troubleshooting Quick Guide  

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Bot ignores commands | Missing intents or insufficient permissions | Verify intents are enabled and the bot has Administrator or required individual permissions. |
| `!setup` fails | Template file missing or malformed JSON | Check that the file exists in `templates/` and run it through a JSON validator. |
| Welcome embed never appears | Server Members intent disabled or `!welcomechannel` not run in the target channel | Enable the intent, then re‑run `!welcomechannel` in the desired text channel. |
| Roles not created | Bot lacks Manage Roles or the role name already exists | Grant Manage Roles permission or rename the conflicting role. |
| Bot crashes on start | Node version too low or missing `.env` variable | Upgrade to Node ≥ 16 and ensure `DISCORD_TOKEN` is set correctly. |

---

## Contributing & Extending  

1. **Fork the repo** and create a new branch for your changes.  
2. **Add or improve templates** in the `templates/` folder.  
3. **Submit a Pull Request** – include a short description and any relevant screenshots.  
4. **Report bugs** via the **Issues** tab on GitHub.  

All contributions are covered under the **MIT License**, meaning you’re free to use, modify, and redistribute the code as long as the original license notice is retained.

---

## Where to Find ServerManager  

- **Top.gg** – the largest Discord bot listing.  
- **discord.bots.gg** – community‑driven directory.  
- **discordbotlist.com** – another popular marketplace.  

Listing the bot on these platforms helps people discover ServerManager and grow the community around it.

---

## Final Thoughts  

ServerManager turns the often‑tedious process of server setup into a **single line of text**. Whether you’re launching a brand‑new gaming clan, a professional study hub, or a public community, the combination of **template‑driven architecture**, **built‑in moderation**, and **welcome automation** gives you a polished Discord experience in minutes.  

Give it a spin, create your own templates, and let the bot do the heavy lifting—so you can focus on what really matters: building a thriving community.  

*Made with ❤️ by Evilman34*