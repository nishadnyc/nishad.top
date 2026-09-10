---
layout: post
title: "Github-Stats-Card"
date: 2026-09-10 08:50:48 +0000
categories: projects
excerpt: "Elevate Your Profile with the GitHub Stats Card Generator Your GitHub profile is often the first pl..."
---

# Elevate Your Profile with the GitHub Stats Card Generator

Your GitHub profile is often the first place potential employers, collaborators, and fellow developers look to understand your coding habits and expertise. While the standard contribution graph is great, I wanted to create something more visually striking and dynamic. That is why I built the **GitHub Stats Card Generator**.

My goal was to create a tool that allows anyone to transform their raw GitHub data into a stunning, animated visual card that can be embedded directly into a profile README.

## What is the GitHub Stats Card Generator?

The GitHub Stats Card Generator is a web-based tool that pulls real-time data from the GitHub REST API to create a personalized statistics card. Unlike static images, these cards feature fluid animations—specifically a water ripple effect—and a highly customizable design system to match any personal brand or aesthetic.

You can try it out live here: [https://github-stats.nishad.top](https://github-stats.nishad.top)

## Key Features

I have packed the generator with features that go beyond simple numbers, focusing on both data and design:

### 📊 Comprehensive Data Tracking
The cards provide a snapshot of your activity, including:
* **Live Current Stats:** Up-to-the-minute data on your activity.
* **Streak Tracker:** Highlights your longest contribution streak to showcase consistency.
* **Contribution Metrics:** Total and yearly contribution counts.
* **Social Proof:** Displays your total public repositories, stars received, and followers.
* **Language Analysis:** A visually ranked language bar showing the technologies you use most.

### 🎨 Advanced Visual Customization
I believe aesthetics matter, so I included a deep level of customization:
* **Animated Effects:** A unique water ripple animation within the streak circle.
* **Themed Presets:** I've curated five beautiful themes:
    * **Ocean:** Cool blues and fluid design (the default).
    * **Dark:** Elegant high contrast for a professional look.
    * **Sunset:** Bold reds and oranges for a high-energy vibe.
    * **Forest:** Earthy greens and calm visuals.
    * **Purple:** A royal look with soft, sophisticated hues.
* **Full Granular Control:** You can manually adjust the background, text, accent, border, water, and streak counter colors.

### 🛠️ Seamless Integration
To make the tool accessible, I implemented a **README Code Generator**. Once you are happy with your preview, you can simply copy the generated markdown code and paste it into your GitHub profile. I also included an option to export your card as a PNG for use in portfolios or social media.

## Layout Overview

The card is structured to be readable yet information-dense, following this general flow:
`[ Circular Avatar ] | [ Animated Streak Circle ] | [ Stats & Languages ]`

This includes a dedicated profile block with your avatar and join date, a pulsing streak counter, and a detailed breakdown of your repository and language stats.

## Potential Use Cases

* **Personal Branding:** Make your GitHub profile stand out from the crowd to attract recruiters.
* **Portfolio Enhancement:** Embed your live stats in a personal portfolio website to prove your active development status.
* **Gamification:** Use the streak tracker to motivate yourself and others to commit code daily.
* **Community Sharing:** Share your PNG export on Twitter or LinkedIn to celebrate a milestone (like a 100-day streak).

## Examples in Action

Depending on the theme you choose, the vibe of your profile changes instantly. Here are a few examples of what the generator can produce:

**Ocean Theme**
![henry-jackson](https://github-stats.nishad.top/api/card-with-avatar?username=henry-jackson&theme=%7B%22backgroundColor%22%3A%22%230f172a%22%2C%22textColor%22%3A%22%23e2e8f0%22%2C%22accentColor%22%3A%22%230ea5e9%22%2C%22borderColor%22%3A%22%231e293b%22%2C%22waterColor%22%3A%22%230ea5e9%22%2C%22streakColor%22%3A%22%2306b6d4%22%7D)

**Purple Theme**
![gijzelaerr](https://github-stats.nishad.top/api/card-with-avatar?username=gijzelaerr&theme=%7B%22backgroundColor%22%3A%22%23581c87%22%2C%22textColor%22%3A%22%23f3e8ff%22%2C%22accentColor%22%3A%22%23a855f7%22%2C%22borderColor%22%3A%22%237c3aed%22%2C%22waterColor%22%3A%22%23a855f7%22%2C%22streakColor%22%3A%22%23c084fc%22%7D)

**Sunset Theme**
![viktorgardart](https://github-stats.nishad.top/api/card-with-avatar?username=viktorgardart&theme=%7B%22backgroundColor%22%3A%22%23451a03%22%2C%22textColor%22%3A%22%23fef3c7%22%2C%22accentColor%22%3A%22%23f59e0b%22%2C%22borderColor%22%3A%22%2392400e%22%2C%22waterColor%22%3A%22%23f59e0b%22%2C%22streakColor%22%3A%22%23dc2626%22%7D)