---
layout: post
title: '"Growing Together": The Spark and the Stack'
date: 2026-03-21 12:00:00 +0000
categories: [side-project, nextjs]
tags: [nextjs, prisma, fatherhood, tech-stack]
---

Every developer has that one "itch" they need to scratch. For me, it was tracking my kids' height. Sure, there are apps for that, but none of them felt *right*. They were either cluttered with ads or lacked the specific "sibling comparison" logic I wanted. 

So, I did what any self-respecting IT professional does: I spent three weeks building a custom web app instead of just using a spreadsheet.

### The Vision
The goal for **Growing-Together** was simple: A clean, emerald-themed dashboard where I can log height measurements and see exactly how my kids are tracking against WHO growth charts. 

### The Stack: Choosing "The New Shiny"
I decided to go with a modern, production-grade stack to keep my skills sharp:

*   **Next.js 16 (App Router):** Because if you're not using the latest React features, are you even developing?
*   **TypeScript:** Because I value my sanity and don't like `undefined is not a function` at 2 AM.
*   **Prisma + PostgreSQL:** The ultimate developer experience for database management.
*   **NextAuth.js:** Handling auth so I don't have to (more on that later).
*   **Tailwind CSS:** For that crisp, responsive UI that looks good on my phone while I'm actually at the measuring tape.

### The First Commit
Day one was all about the "Initial Project Structure." I wanted a clean foundation. I set up the `Child` and `Height` models in Prisma, wired up the basic CRUD operations, and got the first measurement saved to a local DB.

It’s just a "Hello World" with a database, but seeing that first data point pop up on a chart? That’s the spark that keeps a side project alive.

Next up: Moving this thing off my local machine and into the cloud. (Spoiler: It involves a lot of YAML).

Stay tuned!
