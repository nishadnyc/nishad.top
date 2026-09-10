---
layout: post
title: "Github-Stats-Card"
date: 2026-09-10 08:50:48 +0000
categories: projects
excerpt: "Elevate Your GitHub Profile with the GitHub Stats Card Generator Your GitHub profile is more than j..."
---

# Elevate Your GitHub Profile with the GitHub Stats Card Generator

Your GitHub profile is more than just a list of repositories; it is your professional portfolio in the developer world. While the default contribution graph is great, I wanted to create a way to showcase my achievements with more flair and visual impact. That is why I built the **GitHub Stats Card Generator**.

The GitHub Stats Card Generator allows developers to create stunning, animated stats cards that bring live data to their profile READMEs. By combining real-time GitHub API data with a polished visual interface, I've made it possible to turn dry statistics into a dynamic visual highlight.

## What is the GitHub Stats Card Generator?

At its core, this project is a tool that generates a custom image (via an API) that displays a user's GitHub activity. Instead of a static text list, you get a high-quality card featuring water-ripple animations and a modern layout that automatically updates as you commit code.

You can try it out live here: [https://github-stats.nishad.top](https://github-stats.nishad.top)

## Key Features

I designed this tool to be both powerful and user-friendly, ensuring that anyone can customize their card without needing to write complex CSS or SVG code.

### 📊 Real-Time Data Tracking
The cards pull live data directly from the GitHub REST API to showcase:
* **Contribution Metrics:** Total and yearly contributions.
* **Engagement:** Number of public repositories, stars, and followers.
* **Consistency:** A dedicated longest streak tracker to highlight your dedication.
* **Skillset:** A visually ranked language bar showing your top programming languages.

### 🎨 Advanced Visual Customization
I believe aesthetics matter. The generator includes several built-in themes and deep customization options:
* **Preset Themes:** Choose from **Ocean** (Cool blues), **Dark** (Elegant contrast), **Sunset** (Bold reds/oranges), **Forest** (Earthy greens), or **Purple** (Royal hues).
* **Custom Color Control:** You can manually adjust the background, text, accent, border, and streak colors.
* **Dynamic Animations:** The "Water Ripple" effect adds a fluid, living element to the streak counter, making the card feel interactive.
* **Circular Avatar Integration:** Your profile picture is seamlessly integrated into the layout for a personalized touch.

### 🛠️ Seamless Integration
I wanted the transition from "generating" to "displaying" to be instant. The tool includes a **README Code Generator**, meaning you can simply copy a snippet of markdown and paste it directly into your profile. I also included an **Export as PNG** option for those who want to use their stats in other presentations or portfolios.

## Layout Overview

The cards are structured to provide maximum information at a glance:
`[ Circular Avatar ] | [ Animated Streak Circle ] | [ Stats & Languages ]`

This layout ensures that your identity, your current momentum (the streak), and your overall technical reach (stats/languages) are all balanced within a single visual asset.

## Use Cases

Who is this for? I built this for any developer looking to stand out:

* **Job Seekers:** Impress recruiters by showcasing your most-used languages and contribution streaks visually.
* **Open Source Contributors:** Highlight your impact on the community through star and follower counts.
* **Personal Branding:** Maintain a cohesive aesthetic across your GitHub profile that matches your personal brand colors.

## Getting Started

If you want to enhance your profile, the process is simple:
1. Visit the [Stats Card Generator](https://github-stats.nishad.top).
2. Enter your GitHub username.
3. Select a theme or customize your own colors.
4. Copy the generated README code and paste it into your GitHub profile.

By leveraging the GitHub REST API and Vercel for deployment, I've ensured that these cards are fast, responsive, and always up-to-date.