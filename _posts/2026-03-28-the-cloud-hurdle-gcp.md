---
layout: post
title: 'The Cloud Hurdle: GCP and the Quest for a Custom Domain'
date: 2026-03-28 15:00:00 +0000
categories: [devops, gcp]
tags: [cloud-run, docker, gcp, deployment]
---

"It works on my machine" is a phrase that should haunt every developer. The real test of a project is when it lives on the public internet. For **Growing-Together**, I decided to go "all-in" on Google Cloud Platform (GCP).

### Why GCP?
I wanted to learn the Cloud Run workflow. Containerize the app, push it, and let Google handle the scaling. Plus, I wanted a custom domain (`growingtogether.ie`) to make it feel like a real product.

### The Containerization Dance
Step one was the `Dockerfile`. Next.js in a container is standard, but you have to be careful with environment variables. I learned the hard way that Prisma needs to know the database URL during the build if you're not careful, but I wanted to inject it at runtime using GCP Secret Manager.

### The "Cloud Build" Nightmare
Automating the deployment with `cloudbuild.yaml` was where the real "fun" began. Managing permissions between Cloud Build, Cloud Run, and Cloud SQL is a delicate dance of IAM roles. 

I wrote a PowerShell script (`deploy-gcp.ps1`) to wrap the complexity. It handles:
1. Building the Docker image.
2. Pushing to Artifact Registry.
3. Deploying to Cloud Run with the correct secrets and SQL connections.

### Custom Domains & SSL
There's something incredibly satisfying about seeing your side project behind an `https://` lock on a custom domain. It took a few hours for the DNS to propagate, but once it did, **Growing-Together** was officially "live."

Of course, once people can actually *use* the app, you realize you need a better way to get data in than one-by-one forms.

Next post: Handling the data deluge with Bulk Imports.
