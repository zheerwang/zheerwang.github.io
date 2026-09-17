---
layout: zw-research-project
title: "Era-Adjusted Baseball Analytics"
description: "Full House Modeling \u00b7 Public-Facing Data Tools"
permalink: /project/baseball-analytics/
nav: false
technologies: ["Python", "R", "React", "Firebase", "Docker", "GitHub Actions"]
project_image: /assets/img/research/baseball-analytics.svg
image_caption: "An automated data pipeline connects baseball statistics, statistical models, and an interactive application."
resources: [{"label": "Project website", "url": "https://eckeraadjustment.web.illinois.edu/"}, {"label": "Eck Sports Lab", "url": "https://ecklab.github.io/"}]
# Optional: add github_url or demo_url when you have the real URLs.
---

## Overview

How can we compare baseball players who competed in different eras? The **Full House Modeling** project at **Eck Sports Lab**, led by Professor **Daniel J. Eck** at the University of Illinois Urbana-Champaign, develops statistical tools for this question.

The lab's approach considers both performance relative to contemporaries and the quality of the available talent pool. Its era-adjusted measures include **ebWAR** (era-adjusted Baseball-Reference wins above replacement) and **efWAR** (era-adjusted FanGraphs wins above replacement). [Explore the lab's research](https://ecklab.github.io/).

As a **Software Engineering Research Assistant (August 2024–May 2025)**, I contributed public-facing software and data tools that help users explore these statistics. My work connected the lab's statistical methods with data ingestion, backend services, and an interactive application.

## My engineering contributions

**Automated ingestion.** Built a Python pipeline using Selenium and BeautifulSoup to scrape and process baseball statistics, with GitHub Actions scheduling daily updates.

**Statistical data services.** Developed Python backend services integrating R modules for statistical transformations. Deployed Docker containers backed by Firebase Realtime Database and improved database schema and indexing.

**Interactive web application.** Built and deployed a responsive React application with Material UI, desktop and mobile layouts, 250 ms-debounced search, and interactive statistical filters.

**Research communication.** Helped make era-adjusted player statistics accessible through public-facing tools and content for the Full House Modeling project. The underlying methodology and era-adjusted metrics are part of the lab's collaborative research.

## Engineering outcomes

| Measure | Result from my research-assistant work |
| :--- | :--- |
| Baseball statistics processed | **Over 2 TB** |
| Query latency | **45% reduction** |
| Initial application load time | **40% reduction** |
| Application audience | **1,000+ active users** |
| Data refresh | **Scheduled daily updates** |

These engineering results describe my contributions during the research-assistant period. The linked research application continues to evolve as part of the lab's ongoing work.

## Explore the project

The project website provides access to era-adjusted baseball statistics. The Eck Sports Lab website explains the research, related publications, and the people behind it.
