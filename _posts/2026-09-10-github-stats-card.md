---
layout: post
title: "Github-Stats-Card"
date: 2026-09-10 08:50:48 +0000
categories: projects
excerpt: "Elevate Your GitHub Profile with the GitHub Stats Card Generator Your GitHub profile is more than j..."
---

# Elevate Your GitHub Profile with the GitHub Stats Card Generator

Your GitHub profile is more than just a list of repositories; it is your digital resume and a testament to your journey as a developer. While the standard contribution graph is great, I wanted to create something more visually striking—a way to showcase achievements, streaks, and language proficiency in a single, elegant card.

That is why I built the **GitHub Stats Card Generator**.

## What is the GitHub Stats Card Generator?

The GitHub Stats Card Generator is a tool designed to transform raw GitHub data into stunning, animated visual cards. Instead of relying on plain text or basic tables, I’ve created a system that generates dynamic images featuring water effects and professional layouts that you can embed directly into your profile README.

You can try it live here: [https://github-stats.nishad.top](https://github-stats.nishad.top)

## Key Features

I focused on combining data accuracy with high-end aesthetics. Here are the primary features I've integrated into the tool:

### 📊 Comprehensive Data Tracking
The cards don't just look good; they provide real-time insights into your activity:
*   **Live Current Stats:** Immediate visibility into your profile metrics.
*   **Streak Tracker:** A dedicated highlight for your longest contribution streak.
*   **Contribution Totals:** A breakdown of yearly and total contributions.
*   **Profile Metrics:** Quick view of public repositories, stars, and followers.

### 🎨 Visual Sophistication
To make the cards stand out, I implemented several design-centric features:
*   **Water Ripple Animation:** A unique, fluid animation within the streak circle to add life to your profile.
*   **Circular Avatar Integration:** Your profile picture is seamlessly integrated into the card layout.
*   **Language Ranking:** A visual bar that ranks your top languages based on usage.
*   **Export Options:** While the primary use is embedding via code, you can also export your card as a PNG.

### 🛠️ Deep Customization
I believe every developer has their own aesthetic. That's why I included a full suite of customization options:
*   **Pre-set Themes:** I've designed five beautiful themes: **Dark** (rich contrast), **Ocean** (cool blues), **Sunset** (bold reds/oranges), **Forest** (earthy greens), and **Purple** (royal hues).
*   **Granular Control:** You can manually adjust the background color, text color, accent highlights, border colors, and the specific colors for the water and streak animations.

## The Layout Overview

I designed the card to be read from left to right, ensuring a logical flow of information:
`[ Circular Avatar ]` $\rightarrow$ `[ Animated Streak Circle ]` $\rightarrow$ `[ Stats & Languages ]`

This layout ensures that your identity, your consistency (streak), and your technical skill set (languages/stats) are all visible at a single glance.

## Potential Use Cases

While the most obvious use case is the **GitHub Profile README**, there are several other ways I envision people using these cards:

*   **Portfolio Websites:** Embed your live GitHub stats on your personal portfolio to provide real-time proof of your activity.
*   **Technical Blogs:** Use the cards in "About Me" sections of your blog to showcase your growth as a coder.
*   **Social Media:** Export the cards as PNGs to share your milestones or "end-of-year" stats on Twitter or LinkedIn.

## Getting Started

I made the process as simple as possible so you can spend less time configuring and more time coding:

1.  Visit the [Stats Card Generator](https://github-stats.nishad.top).
2.  Enter your GitHub username.
3.  Select a theme or customize your colors.
4.  Preview the card in real-time.
5.  Copy the generated README code and paste it into your profile.

By leveraging the GitHub REST API and deploying via Vercel, I've ensured that the generation process is fast, smooth, and always up to date.