---
layout: post
title: "nishadnyc.github.io"
date: 2026-09-10 22:47:23 +0000
categories: projects
excerpt: "Automating My Technical Narrative: An AI-Driven Portfolio Maintaining a personal blog and portfolio..."
---

# Automating My Technical Narrative: An AI-Driven Portfolio

Maintaining a personal blog and portfolio is often a struggle for developers. The friction between writing code and documenting that code in an engaging way usually leads to a "ghost town" blog where the last post was from two years ago. To solve this, I built a system that bridges the gap between my active development on GitHub and my public-facing portfolio.

## What is this project?

I have developed an automated pipeline that transforms my GitHub activity into a living blog. Instead of manually drafting posts for every tool or library I create, this system leverages AI to analyze my repositories and auto-generate comprehensive blog articles.

The entire process is hands-off, powered by GitHub Actions and a scheduled cron job that triggers once every day to ensure my portfolio stays current with my latest commits and projects.

## Purpose and Motivation

The primary goal of this project is to eliminate the "documentation tax." As a developer, my primary focus is building software, but visibility is key for professional growth. I wanted a way to:
* **Maintain Consistency:** Ensure my blog is updated daily without requiring manual intervention.
* **Showcase Work in Real-Time:** Translate raw code and commit history into human-readable narratives.
* **Leverage Generative AI:** Use LLMs to synthesize technical specifications into engaging articles.

## Key Features

* **AI-Powered Content Generation:** The system uses an AI model to interpret the context, purpose, and functionality of my GitHub repositories, turning technical files into structured blog posts.
* **Automated Workflows:** Integration with GitHub Actions allows the system to run autonomously.
* **Daily Synchronization:** A built-in cron job ensures that the AI scans for updates every 24 hours, keeping the content fresh.
* **Seamless Portfolio Integration:** The generated articles are automatically fed into my portfolio website, creating a continuous stream of technical content.

## Potential Use Cases

While I designed this for my personal portfolio, this architecture has several broader applications:

* **Automatic Project Changelogs:** Transforming commit messages and PRs into user-friendly "What's New" posts for end-users.
* **Developer Portfolios:** Helping other engineers maintain a presence online by automatically highlighting their open-source contributions.
* **Technical Documentation:** Creating high-level introductory guides for complex repositories based on the codebase itself.