---
layout: post
title: "Github-Stats-Card"
date: 2026-09-10 08:50:48 +0000
categories: projects
excerpt: "GitHub Stats Card Generator – Bringing Your Contributions to Life I’m thrilled to share the GitHub..."
---

# GitHub Stats Card Generator – Bringing Your Contributions to Life  

I’m thrilled to share the **GitHub Stats Card Generator** I built, a lightweight web app that turns raw GitHub statistics into animated, eye‑catching cards. Whether you want to spice up your profile README, showcase your coding streak, or simply enjoy a splash of animated water, this tool delivers a fully customizable, real‑time visual of your open‑source activity.

![My GitHub Card](https://github-stats.nishad.top/api/card-with-avatar?username=nishadnyc&theme=%7B%22backgroundColor%22%3A%22%231a1b27%22%2C%22textColor%22%3A%22%23ffffff%22%2C%22accentColor%22%3A%22%2300d4aa%22%2C%22borderColor%22%3A%22%2330363d%22%2C%22waterColor%22%3A%22%2300d4aa%22%2C%22streakColor%22%3A%22%23ff6b6b%22%7D)

---

## Why I Created This Tool  

GitHub profiles are often a wall of numbers—repositories, stars, followers—presented in plain text. I wanted a way to **visualize** those metrics with flair, allowing developers to instantly convey their activity, passion, and consistency. The result is an animated stats card that feels like a badge of honor, complete with a circulating avatar, a water‑ripple streak indicator, and a sleek language breakdown.

---

## Core Features  

- **Live Current Stats** – Pulls the latest data directly from the GitHub REST API.  
- **Longest Streak Tracker** – Shows your current contribution streak with a pulsating water animation.  
- **Yearly & Total Contributions** – Displays both the current year’s contribution graph and the overall count.  
- **Public Repos, Stars, Followers** – Summarizes the most sought‑after GitHub metrics at a glance.  
- **Circular Avatar Integration** – Embeds your profile picture inside a clean, rounded frame.  
- **Water Ripple Animation** – Adds a subtle yet dynamic wave effect around the streak counter.  
- **5+ Beautiful Themes** – Dark, Ocean, Sunset, Forest, Purple — each with distinct color palettes.  
- **Full Color & Layout Customization** – Tweak background, text, accent, border, water, and streak colors to match any personal brand.  
- **README Code Generator** – One‑click copy of the markdown snippet ready for your profile.  
- **Export as PNG** – Capture a static image for use outside GitHub, such as blogs or portfolios.  

---

## Theme Gallery  

| Theme | Preview |
|-------|---------|
| **Ocean** (default) | ![Ocean Theme](https://github-stats.nishad.top/api/card-with-avatar?username=henry-jackson&theme=%7B%22backgroundColor%22%3A%22%230f172a%22%2C%22textColor%22%3A%22%23e2e8f0%22%2C%22accentColor%22%3A%22%230ea5e9%22%2C%22borderColor%22%3A%22%231e293b%22%2C%22waterColor%22%3A%22%230ea5e9%22%2C%22streakColor%22%3A%22%2306b6d4%22%7D) |
| **Purple** | ![Purple Theme](https://github-stats.nishad.top/api/card-with-avatar?username=gijzelaerr&theme=%7B%22backgroundColor%22%3A%22%23581c87%22%2C%22textColor%22%3A%22%23f3e8ff%22%2C%22accentColor%22%3A%22%23a855f7%22%2C%22borderColor%22%3A%22%237c3aed%22%2C%22waterColor%22%3A%22%23a855f7%22%2C%22streakColor%22%3A%22%23c084fc%22%7D) |
| **Sunset** | ![Sunset Theme](https://github-stats.nishad.top/api/card-with-avatar?username=viktorgardart&theme=%7B%22backgroundColor%22%3A%22%23451a03%22%2C%22textColor%22%3A%22%23fef3c7%22%2C%22accentColor%22%3A%22%23f59e0b%22%2C%22borderColor%22%3A%22%2392400e%22%2C%22waterColor%22%3A%22%23f59e0b%22%2C%22streakColor%22%3A%22%23dc2626%22%7D) |
| **Dark** | ![Dark Theme](https://github-stats.nishad.top/api/card-with-avatar?username=fedetrim&theme=%7B%22backgroundColor%22%3A%22%231a1b27%22%2C%22textColor%22%3A%22%23ffffff%22%2C%22accentColor%22%3A%22%2300d4aa%22%2C%22borderColor%22%3A%22%2330363d%22%2C%22waterColor%22%3A%22%2300d4aa%22%2C%22streakColor%22%3A%22%23ff6b6b%22%7D) |
| **Forest** | *(preview available in the live app)* |

---

## Layout Overview  

```
[ Circular Avatar ] | [ Animated Streak Circle ] | [ Stats & Languages ]
```

- **Profile block** – Avatar, username, and join date.  
- **Streak counter** – Animated water‑filled circle that pulses with each day of continuous contribution.  
- **Stats panel** – Contributions, repo count, stars, followers, plus a ranked language bar.  

The layout balances visual appeal with information density, making the card suitable for both wide and narrow contexts.

---

## Getting Started – One‑Minute Setup  

1. **Visit the generator** – Open https://github-stats.nishad.top.  
2. **Enter your GitHub username** – The app instantly fetches your data.  
3. **Choose a theme** – Pick from the preset collection or dive into the custom color picker.  
4. **Preview in real���time** – Watch the water ripple react as you adjust settings.  
5. **Copy the markdown** – Click “Copy README code” and paste the snippet into any markdown file (e.g., your GitHub profile README).  
6. **Optional: Export PNG** – Save a static image for blogs, slide decks, or personal sites.  

And that’s it—your profile now sports an animated, data‑rich badge that updates automatically.

---

## Real‑World Use Cases  

- **Developer portfolios** – Add a dynamic stats card to showcase recent activity without clutter.  
- **Open‑source project READMEs** – Highlight contributors’ streaks and language expertise.  
- **Team dashboards** – Generate cards for each member to visualize collective contributions.  
- **Technical blogs & newsletters** – Embed a PNG export to illustrate personal coding journeys.  
- **Hackathon submissions** – Use the card as a visual “scoreboard” for individual or team contributions.  

Because the card is generated on the fly via the GitHub API, it stays current without any manual updates.

---

## Deep Customization  

| Option | What It Controls |
|--------|------------------|
| **Background** | Overall card color. |
| **Text** | Color of usernames, numbers, and labels. |
| **Accent** | Highlights for icons, streak outline, and small UI elements. |
| **Border** | Edge color and separation lines between sections. |
| **Water** | Hue of the animated ripple surrounding the streak. |
| **Streak Counter** | Color and pulse intensity of the current streak display. |

The UI exposes a JSON editor for those who prefer to paste a full theme object, granting limitless design possibilities.

---

## Under the Hood  

- **Data source** – GitHub REST API (public endpoints, no auth required for public data).  
- **Hosting** – Deployed on Vercel for instant global CDN delivery and zero‑maintenance scaling.  
- **Frontend** – Built with modern JavaScript, leveraging SVG and Canvas for smooth animations.  

I chose this stack for its speed, reliability, and low cost, ensuring the generator stays fast even under heavy traffic.

---

## Final Thoughts  

If you’re looking to give your GitHub presence a visual upgrade, the **GitHub Stats Card Generator** is ready out of the box. It blends accurate statistics with playful animation, and the high degree of customization means you can align it perfectly with any personal brand or project aesthetic.

Ready to try it? Head over to **[Generate Your Card Now](https://github-stats.nishad.top)**, craft a design you love, and watch the numbers come alive on your profile.  

Happy coding, and may your streaks be ever‑lasting!  

---  

🌟 **[My Portfolio](https://nishad.top)** 🌟   🔗 **Generate Your Card Now**: https://github-stats.nishad.top   🎨 **Elevate your GitHub presence today!**  