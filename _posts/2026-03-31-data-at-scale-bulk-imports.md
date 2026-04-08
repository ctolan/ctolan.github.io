---
layout: post
title: 'Data at Scale: Bulk Imports and the Admin View'
date: 2026-03-31 18:00:00 +0000
categories: [features, productivity]
tags: [csv-import, admin-dashboard, next-auth]
---

Once the app was live, I had a problem: I had five years of height data for my oldest child sitting in a Notes app. Typing those in one-by-one was a non-starter. 

### The "Bulk Import" Solution
I built a `BulkImportDialog` that allows for "Paste-and-Go" functionality. You can copy a table from a spreadsheet or a text file, paste it into a textarea, and the app parses it into measurement records.

The technical challenge here was mapping the imported rows to the correct child profile. I built a mapping interface where you can explicitly select which child each row belongs to. It supports multiple date formats (ISO, US, etc.) because, let’s face it, date parsing is the bane of our existence.

### The Admin Dashboard: Peeking Under the Hood
As the database grew, I needed a way to monitor the system. I added an `/admin` route (Build 00057) that gives me a high-level view of:
*   Total users and children.
*   Recent height measurements.
*   System health stats.

I secured it with a simple email whitelist in the `admin-check.ts` utility. It’s not complex, but it makes the app feel like a managed service rather than just a hobby project.

### Security First
With a public-facing app involving children's data, security isn't optional. I spent a good chunk of time hardening the API endpoints using `api-security.ts`, ensuring that you can only see or edit data for children you actually own. 

But enough about the "plumbing." Let's talk about the cool stuff: The data analysis.
