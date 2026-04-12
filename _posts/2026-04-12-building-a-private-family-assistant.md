---
layout: post
title: "Building a Private Family Assistant: From Monorepo to Cloud Run"
date: 2026-04-12 15:00:00 +0000
categories: [ai, engineering, gcp]
tags: [pydanticai, langgraph, nextjs, cloud-run, monorepo]
---

Today was a high-velocity day for the **Tolan Agents** ecosystem. We've officially moved from a single-repo prototype to a robust, scalable, and secure polyglot monorepo architecture.

### The Vision
The goal is simple but ambitious: build a **private family AI assistant** that helps manage the household (shopping lists, reminders, knowledge) while maintaining absolute privacy and security.

### 1. The Polyglot Monorepo
We restructured the codebase into a monorepo to separate concerns:
- **`apps/api` (Python)**: The "Agent Brain." Powered by **PydanticAI** and **LangGraph**, it handles the heavy lifting of reasoning, tool calling, and persistent memory.
- **`apps/web` (Next.js)**: The "Command Center." A high-fidelity dashboard for the family to interact with the ecosystem.

### 2. Engineering the Brain
We chose **Python** for the backend to leverage the mature AI ecosystem.
- **PydanticAI**: Ensures all tool calls (like adding to a shopping list) are rigorously validated.
- **LangGraph**: Manages complex, multi-turn conversations with **Persistent Memory** stored in Postgres.
- **Human-in-the-Loop**: A critical security feature. The agent *must* request explicit confirmation before modifying any family data.

### 3. The "Family Pulse" Dashboard
We didn't just build an API; we built an experience. The new dashboard features:
- **Emerald/Forest Green Theme**: A premium, natural aesthetic that moves away from the standard AI purple/blue hues.
- **Bento Grid Layout**: High-density cards showing the live Audit Trail, Shopping List counts, and Private Tasks.
- **Glassmorphism**: Modern, translucent UI elements with animated mesh backgrounds.

### 4. Automated GCP Deployment
Infrastructure is managed entirely through a custom PowerShell deployment pipeline. One command (`.\deploy-gcp.ps1`) now handles:
- Provisioning **Cloud Run** services for both API and Web.
- Setting up **Cloud SQL (Postgres 14)** for persistent memory.
- Managing secrets securely via **GCP Secret Manager**.
- Hardening authentication with **NextAuth** and Google OAuth.

### What's Next?
The foundation is solid. Next up is **Phase 2: WhatsApp Integration**, followed by **Google Calendar** syncing.

Stay tuned as we continue to evolve this private AI ecosystem!
