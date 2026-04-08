---
layout: post
title: 'The Heart of the App: Growth Velocity and Sibling Rivalry'
date: 2026-04-06 09:00:00 +0000
categories: [data-science, visualization]
tags: [recharts, growth-charts, algorithms]
---

This is what I built the app for. In Build 00059, I finally implemented the "Advanced Growth Analysis" engine. 

### Growth Velocity
A single height measurement doesn't tell you much. The *rate* of growth is what matters. I wrote a utility to calculate "Growth Velocity" (cm/month). If your kid grows 1cm in two months, that’s 0.5cm/month. Seeing this trend over time helps identify growth spurts before they happen.

### Sibling Comparison (The "Catch-up" Logic)
As a parent of two, I’m always asked: "Was the older one this tall at this age?" 
Now I can answer it. I built a "Same Age" comparison feature that overlays the older sibling's growth curve onto the younger sibling's chart, adjusted so their birthdays align. 

I even added a "Catch-up" prediction. It calculates, based on current velocities, exactly when the younger sibling might reach the older sibling's *current* height. It’s a bit of fun math that adds personality to the app.

### Percentiles & Reference Charts
I integrated the UK NHS/WHO growth standards. Adding those 10th, 50th, and 90th percentile lines using `Recharts` was a challenge in data normalization, but the result is a professional-grade chart that looks just like what you’d see at the pediatrician’s office.

Everything was perfect. The UI was polished, the data was flowing, and then... I decided to do a "Phase 2" migration.

Hold onto your hats, because the next post is a horror story.
