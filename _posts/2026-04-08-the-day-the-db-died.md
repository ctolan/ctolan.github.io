---
layout: post
title: 'The Day the DB Died (And How I Brought it Back)'
date: 2026-04-08 10:00:00 +0000
categories: [disaster-recovery, database]
tags: [prisma, postgresql, incident-report, lessons-learned]
---

Every developer has a "Day the Music Died." Mine was April 6, 2026.

### The Incident
I was moving into "Phase 2" of development—adding weight tracking and family sharing. I needed to reorganize the database schema to better support NextAuth. I wrote a migration script that I *thought* was safe. 

It wasn't.

In my haste to align the schema, a destructive SQL script was executed. It dropped the original `Child` and `Height` tables before the data migration was verified. 

**Result:** Total data loss. Zero records. Five years of height data... gone.

### The Panic and the Pivot
After the initial five minutes of staring blankly at an empty dashboard, I went into recovery mode. 

1.  **Stop the Bleeding:** I locked down the database and restricted all access.
2.  **The Forensic Pull:** I used `prisma db pull` to see what the state of the database actually was.
3.  **The Auth Fix:** The migration had broken NextAuth because of a field name mismatch (`expiresAt` vs `expires_at`). I manually realigned the `schema.prisma` to match the production DB state.

### The Recovery (A Silver Lining)
Luckily, because of the "Bulk Import" feature I’d built the week before, I still had the original raw data files on my local machine. I was able to re-import the data and get the system back to 100% integrity.

### Lessons Learned
I’ve now added a **CRITICAL PREVENTION PROTOCOL** to my `PROJECT_PLAN.md`:
1. **No Destructive Migrations:** Never drop a table without a verified external SQL dump.
2. **Verification First:** Data migration must be verified with row counts before the old tables are touched.
3. **Rollback Plans:** Every schema change must have a tested reversal script.

It was a painful lesson, but it made the app (and my deployment process) significantly more robust. 

**Growing-Together** is now back online, more secure, and ready for whatever Phase 2 throws at it. 

Onward!
