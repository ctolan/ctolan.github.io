---
layout: post
title: 'Letting My Son Add His Own Artwork (With a Parent in the Loop)'
date: 2026-10-02 06:00:00 +0000
categories: [ai, engineering, gcp]
tags: [ai, cloud-run, gcp, fatherhood]
ai_generated: true
---

Like the last post, this one was written by an AI agent, so it carries the badge. The feature it describes was built the same way, under my direction.

I run a small family art gallery site for my kids at patrick.tolan.ie. Until now, if Patrick drew something, I had to photograph it and add it myself. I wanted him to be able to add his own artwork from his phone, without handing a child publishing rights to a public website. Parents stay in control, and he gets to be the one who adds his work.

## What it does now

Patrick signs in with Google, takes or picks a photo on his phone, and gives it a title and an optional note. The photo is resized and re-encoded on the device, which also strips location metadata, and the original is discarded. It then goes to a private pending area. A parent opens a `/review` page and approves or rejects it. Only approved photos show up on the public gallery.

## The design choices

- **Google sign-in via Firebase Auth.** I didn't want to build a login system for a family gallery.
- **A small Cloud Run API that scales to zero.** When nobody is uploading, nothing runs and nothing bills.
- **Private storage buckets and a Firestore database.** Nothing is public by default.
- **Approved images are served through the API.** The API checks approval status first. I never made a bucket public.
- **Pending and rejected photos auto-delete after 14 days.** The queue can't turn into a pile of forgotten uploads.
- **The server doesn't trust the browser.** It re-validates and re-encodes every image itself, whatever the client claims to have done.

## How it was built

The agents did the building and the cloud setup. My job was deciding the requirements, approving each risky step, and testing on my phone. Cloud provisioning needed my go-ahead, and so did anything that could make something public. I would rather be asked one question too many than find out later that a bucket was open.

I also ran two independent AI security reviews. The first found nothing. The second found two medium issues in the auth proxy configuration: missing no-store caching on the auth paths, and upstream TLS verification not being enabled. Both are fixed. I'm glad I ran a second review rather than stopping at the clean first one.

## The hiccups

It didn't go smoothly, which is why I'm listing these.

1. **The site looked unchanged after deploying.** The frontend simply hadn't been redeployed. The backend was fine and the page still looked old.
2. **Google sign-in looped on my phone.** The fix was setting the Firebase auth domain to the custom domain, using a same-origin proxy, and adding the OAuth redirect URIs. That is fiddly, and I wouldn't have found it quickly alone.
3. **The review page then failed.** Firestore timestamps weren't being serialised correctly. That got fixed and is now covered by a regression test.
4. **I missed the submit button.** It sat at the bottom of a long mobile page and I didn't notice it at first. If I missed it, Patrick will too, so that is a usability problem worth fixing.

Testing on a real phone found most of these. None of them showed up from reading code.

## An honest caveat

For now my own Google account is temporarily both the submitter and the reviewer. That means self-approval is possible, so the "parent reviews it" control is only partly real until I set up separate accounts for Patrick and a parent. I'm saying so plainly because a safeguard that can approve itself isn't one yet.

## Why I'm writing it up

This is a good example of what I meant last time about AI-assisted work being worth labelling. The agents wrote a lot of code and ran a lot of cloud setup, and I still had to make the judgement calls about who can publish, what stays private, and when to say no. The tools are fast. Deciding what is safe to ship is still my job.

Next up is giving Patrick and a parent their own accounts, so the review step means something.
