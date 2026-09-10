---
layout: post
title: "Github-Stats-Card"
date: 2026-09-09 18:32:58 +0000
categories: projects
excerpt: "GitHub Stats Card Generator – Turn Your Profile into a Visual Showcase Overview The GitHub Stats Ca..."
---

# GitHub Stats Card Generator – Turn Your Profile into a Visual Showcase

## Overview  

The GitHub Stats Card Generator is a web‑based tool that creates animated, customizable stats cards for any GitHub user. By combining real‑time data from the GitHub REST API with eye‑catching water‑ripple effects, circular avatars, and theme‑driven color palettes, the generator produces ready‑to‑embed markdown snippets that instantly enrich a profile README.

> **Live Demo:** <https://github-stats.nishad.top>  

![GitHub Stats Card Example](https://github-stats.nishad.top/api/card-with-avatar?username=nishadnyc&theme=%7B%22backgroundColor%22%3A%22%231a1b27%22%2C%22textColor%22%3A%22%23ffffff%22%2C%22accentColor%22%3A%22%2300d4aa%22%2C%22borderColor%22%3A%22%2330363d%22%2C%22waterColor%22%3A%22%2300d4aa%22%2C%22streakColor%22%3A%22%23ff6b6b%22%7D)

---

## Why a Visual Stats Card?

- **Instant Impact:** A colorful card draws a reader’s eye far more effectively than raw numbers.
- **Live Updates:** The card fetches current statistics each time it loads, ensuring the displayed data never becomes stale.
- **One‑Click Embedding:** The generated markdown snippet works out‑of‑the‑box with any GitHub README or documentation file.
- **Brand Consistency:** Customizable themes let developers align the card with personal branding or project colors.

---

## Core Features

| Feature | Description |
|---------|-------------|
| **Live Current Stats** | Shows total stars, public repos, followers, and the newest contributions. |
| **Longest Streak Tracker** | Displays the longest consecutive‑day contribution streak with a pulsating water animation. |
| **Yearly & Total Contributions** | Visualizes contribution counts for the current year and overall. |
| **Circular Avatar Integration** | Renders the user’s avatar inside a neat circle, automatically fetched from GitHub. |
| **Water Ripple Animation** | Dynamic water effect runs around the streak circle, adding motion to a static README. |
| **5+ Pre‑Built Themes** | Dark, Ocean (default), Sunset, Forest, Purple – each with carefully tuned palettes. |
| **Full Color Customization** | Override background, text, accent, border, water, and streak colors via JSON theme objects. |
| **Responsive Layout** | Card adapts to GitHub’s markdown rendering constraints while preserving visual hierarchy. |
| **README Code Generator** | One‑click copy button produces the exact markdown needed for embedding. |
| **PNG Export** | Download a static PNG version for use outside of GitHub (e.g., personal websites, presentations). |

---

## Theme Gallery  

| Theme | Preview |
|-------|---------|
| **Ocean** (default) | <div align="center"><img src="https://github-stats.nishad.top/api/card-with-avatar?username=henry-jackson&theme=%7B%22backgroundColor%22%3A%22%230f172a%22%2C%22textColor%22%3A%22%23e2e8f0%22%2C%22accentColor%22%3A%22%230ea5e9%22%2C%22borderColor%22%3A%22%231e293b%22%2C%22waterColor%22%3A%22%230ea5e9%22%2C%22streakColor%22%3A%22%2306b6d4%22%7D" alt="Ocean Theme"></div> |
| **Purple** | <div align="center"><img src="https://github-stats.nishad.top/api/card-with-avatar?username=gijzelaerr&theme=%7B%22backgroundColor%22%3A%22%23581c87%22%2C%22textColor%22%3A%22%23f3e8ff%22%2C%22accentColor%22%3A%22%23a855f7%22%2C%22borderColor%22%3A%22%237c3aed%22%2C%22waterColor%22%3A%22%23a855f7%22%2C%22streakColor%22%3A%22%23c084fc%22%7D" alt="Purple Theme"></div> |
| **Sunset** | <div align="center"><img src="https://github-stats.nishad.top/api/card-with-avatar?username=viktorgardart&theme=%7B%22backgroundColor%22%3A%22%23451a03%22%2C%22textColor%22%3A%22%23fef3c7%22%2C%22accentColor%22%3A%22%23f59e0b%22%2C%22borderColor%22%3A%22%2392400e%22%2C%22waterColor%22%3A%22%23f59e0b%22%2C%22streakColor%22%3A%22%23dc2626%22%7D" alt="Sunset Theme"></div> |
| **Dark** | <div align="center"><img src="https://github-stats.nishad.top/api/card-with-avatar?username=fedetrim&theme=%7B%22backgroundColor%22%3A%22%231a1b27%22%2C%22textColor%22%3A%22%23ffffff%22%2C%22accentColor%22%3A%22%2300d4aa%22%2C%22borderColor%22%3A%22%2330363d%22%2C%22waterColor%22%3A%22%2300d4aa%22%2C%22streakColor%22%3A%22%23ff6b6b%22%7D" alt="Dark Theme"></div> |
| **Forest** | (Custom colors via JSON – see “Full Customization” table below) |

---

## Layout Anatomy  

```
[ Circular Avatar ] | [ Animated Streak Circle ] | [ Stats & Languages ]
```

- **Profile Block:** Avatar, username, and account creation date.
- **Streak Counter:** Animated circle with water ripple and numeric streak value.
- **Stat Panels:** Contributions bar, repository count, star total, follower count, and a ranked language bar.

The layout is deliberately compact to fit within GitHub’s markdown width while remaining legible on mobile and desktop.

---

## Full Customization  

| Option | Effect |
|--------|--------|
| **Background** | Overall card background color. |
| **Text** | Color used for usernames, numbers, and labels. |
| **Accent** | Highlights for icons, borders, and interactive elements. |
| **Border** | Card outline and separators between sections. |
| **Water** | Tint of the animated water ripple around the streak circle. |
| **Streak Counter** | Color of the streak number and its pulse animation. |

Customization is supplied as a JSON object appended to the API URL (`theme=` query parameter). Example:

```json
{
  "backgroundColor": "#0f172a",
  "textColor": "#e2e8f0",
  "accentColor": "#0ea5e9",
  "borderColor": "#1e293b",
  "waterColor": "#0ea5e9",
  "streakColor": "#06b6d4"
}
```

---

## Getting Started in 5 Minutes  

1. **Visit the generator** – <https://github-stats.nishad.top>.
2. **Enter your GitHub username** in the input field.
3. **Select a theme** or paste a custom JSON theme.
4. **Preview** updates instantly as you tweak colors.
5. Click **“Copy README code”** – the clipboard now holds a markdown snippet such as:

   ```markdown
   ![My GitHub Stats](https://github-stats.nishad.top/api/card-with-avatar?username=your-username&theme=...)
   ```

6. Paste the snippet into any `README.md` or documentation file, commit, and push.

*Optional:* Click **“Export PNG”** to download a static image for use outside of GitHub.

---

## Real‑World Use Cases  

- **Personal Profiles:** Showcase contribution streaks, language expertise, and repo activity at a glance.
- **Open‑Source Project READMEs:** Highlight core maintainers’ stats or project contribution health.
- **Developer Portfolios:** Embed a live stats card on a personal website to demonstrate ongoing activity.
- **Team Dashboards:** Generate cards for each team member to visualize collective contribution levels.
- **Education & Hackathons:** Provide participants with a quick visual summary of their GitHub activity.

---

## Under the Hood  

- **Data Source:** GitHub REST API provides real‑time user statistics, contribution graphs, and repository metadata.
- **Hosting:** Deployed on Vercel, offering low‑latency edge functions for rapid image generation.
- **Image Generation:** Server‑side rendering creates an SVG/PNG blend with animated CSS for the water effect, then serves it as a single image URL.
- **Stateless Architecture:** Each request is independent; no database storage is required, guaranteeing privacy and minimal maintenance.

---

## Benefits Over Traditional Badges  

| Traditional Badge | GitHub Stats Card |
|-------------------|-------------------|
| Static text & numbers | Animated water ripple adds motion |
| Fixed color schemes | Full theme customization via JSON |
| Limited data (stars, forks) | Includes streak, contributions, language bar |
| No avatar support | Circular avatar integrated |
| No live refresh | Image URL always reflects current GitHub data |

---

## Future Directions  

- **Multi‑User Collage:** Combine several users into a single card for team showcases.
- **Dark/Light Auto‑Detect:** Dynamically switch themes based on GitHub’s UI mode.
- **Additional Animations:** Expand water effect to include snowfall, fire, or particle systems.
- **API Rate‑Limit Handling:** Implement caching layers to stay within GitHub’s API limits while preserving live data freshness.

---

## Quick Reference Cheat Sheet  

```markdown
# Example Markdown to embed a card
![My Stats](https://github-stats.nishad.top/api/card-with-avatar?username=YOUR_USERNAME&theme=%7B%22backgroundColor%22%3A%22%231a1b27%22%2C%22textColor%22%3A%22%23ffffff%22%2C%22accentColor%22%3A%22%2300d4aa%22%2C%22borderColor%22%3A%22%2330363d%22%2C%22waterColor%22%3A%22%2300d4aa%22%2C%22streakColor%22%3A%22%23ff6b6b%22%7D)
```

Replace `YOUR_USERNAME` with any GitHub handle and adjust the `theme` JSON string to match your desired color palette.

---

## Connect & Contribute  

- **API & Front‑end:** Open‑source contributions are welcome to extend themes, add new animations, or improve performance.
- **Support:** Issues and feature requests can be filed on the project’s GitHub repository.
- **Portfolio:** Learn more about the creator at <https://nishad.top>.

---

**Elevate your GitHub presence today—turn raw contribution numbers into a captivating visual story.**