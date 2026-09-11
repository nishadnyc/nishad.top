---
layout: post
title: "server-manager-discord-bot"
date: 2026-03-28 09:27:52 +0000
categories: projects
excerpt: "<div align='center'> <img src='LOGO.svg' alt='ServerManager Logo'> <h1>ServerManager 🎯</h1> </div>..."
---

<div align="center">
  <img src="LOGO.svg" alt="ServerManager Logo">
  <h1>ServerManager 🎯</h1>
</div>

Managing a Discord server can be a tedious process, especially when you are starting from scratch. Between creating dozens of channels, organizing them into categories, setting up permission-based roles, and crafting welcome messages, the initial setup often takes hours of manual work. 

I created **ServerManager**, a Discord bot designed to handle the heavy lifting for you. Whether you are launching a gaming community, a professional workspace, or a hobbyist group, ServerManager allows you to deploy a fully organized server structure in seconds.

## What is ServerManager?

ServerManager is an automated administration tool that transforms the way Discord servers are built. Instead of manually creating every element of your community, I have implemented a template-based system. By using a single command, the bot can generate an entire server ecosystem—including categories, text and voice channels, and roles—based on predefined JSON configurations.

## Key Features

### 🚀 Instant Server Architecture
The core of the project is the `!setup` command. I designed this to allow users to apply templates instantly. You can even customize the server name on the fly using the `--name` flag. 

### 🛠️ Custom Templating System
I wanted the bot to be flexible, so I built a custom template engine. You can create your own `.json` files in the `templates/` folder to define:
*   **Categories:** Grouped sections with emoji support for better visual organization.
*   **Text Channels:** Complete with custom topics and initial "welcome" messages that post automatically upon creation.
*   **Voice Channels:** Quick deployment of audio hubs.
*   **Roles:** Defined roles with specific hex colors and permissions (e.g., Administrator, Moderate Members).

### 🛡️ Integrated Moderation
Beyond setup, I've included a robust suite of moderation tools to keep your community safe:
*   **Member Management:** Standard `!kick`, `!ban`, and `!unban` functionality.
*   **Mute System:** Temporary mutes with flexible durations (e.g., 1m, 1h, 1d).
*   **Automated Warning System:** To reduce manual oversight, I implemented a warning tracker. If a user reaches 3 warnings via the `!warn` command, the bot automatically kicks them from the server.

### 💬 Community Engagement Tools
To help admins communicate more effectively, I added:
*   **Anonymous Messaging:** Using the `.say` command, admins can send messages that appear to come from the bot, keeping the admin's personal account private.
*   **Dynamic Welcome Messages:** The `!welcomechannel` command allows me to toggle a welcome system that greets new members with an embed in a specific channel.

## Potential Use Cases

Because of the template system, ServerManager is highly versatile:

*   **Gaming Communities:** Quickly deploy a structure with specific channels for different games (e.g., Valorant, Minecraft) and roles for "Streamers" or "Competitive Players."
*   **Project Management:** Set up a professional environment with categories for "Development," "Design," and "Feedback," with roles assigned to different team leads.
*   **Template Distribution:** Developers can create and share `.json` templates, allowing others to clone proven community structures effortlessly.
*   **Rapid Prototyping:** If you are testing different community layouts, you can wipe and rebuild your server structure in seconds to see what works best.

## Getting Started

If you want to run ServerManager yourself, the process is straightforward. I've built it using **Node.js (v16+)**.

1.  **Clone and Install:** Clone the repository and run `npm install`.
2.  **Configure:** Add your `DISCORD_TOKEN` to a `.env` file.
3.  **Intents:** In the Discord Developer Portal, ensure you enable **Message Content Intent** and **Server Members Intent** so the bot can read commands and detect new members.
4.  **Launch:** Run `npm start` and invite the bot to your server using the invite link.

By automating the mundane aspects of server creation and providing a reliable moderation toolkit, I hope ServerManager allows community leaders to spend less time on configuration and more time engaging with their members.