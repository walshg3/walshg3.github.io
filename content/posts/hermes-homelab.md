---
title: "Using Hermes Agent to administer and automate my homelab"
author: ["Greg Walsh"]
date: "2026-09-30"
lastmod: "2026-10-30"
draft: false
description: "How I use Hermes for troubleshooting, maintenance, and scheduled automation, and where I still require human decisions."
tags: ["homelab", "automation", "Hermes Agent", "AI", "Docker"]
ShowToc: true
images: ["/web-app-manifest-512x512.png"]
editPost:
  URL: "https://github.com/walshg3/walshg3.github.io/edit/master/content"
  Text: "Suggest changes"
  appendFilePath: true
---

One evening, my notification setup produced 75 failure alerts for a season of the TV show *Suits*. Sonarr kept retrying failed download candidates, and SABnzbd sent a notification for each failed attempt. Normally, this would mean I'd have to stop what I was doing, open my laptop, and begin the daunting task of figuring out where in my homelab stack the issue occurred.

This time, I remembered I had installed [Hermes Agent](https://hermes-agent.nousresearch.com/docs/) and thought maybe Hermes could help trace the error. I kicked off a task in my default profile, and after a few permission approvals, Hermes came back with a diagnosis of the problem. Hermes had discovered a misconfiguration in my SABnzbd storage settings and offered a solution that would fix the issue. It was such a niche setting that it would probably have taken me close to an hour to figure out.

I let Hermes change the config and test its changes, and sure enough, the notifications disappeared and my homelab was healthy again. This was my coming-of-age moment with Hermes Agent, and it's been an addiction ever since.

This post is my journey with Hermes Agent and how it has evolved since its conception in February.

## Background setup

My lab includes Proxmox on multiple nodes in a cluster, TrueNAS, Docker applications, UniFi networking, and a Prometheus and Grafana monitoring stack. A problem that first appears in one application can involve several of those systems before I find the cause. You can find more about it in my [GitHub homelab repository](https://github.com/walshg3/Homelab).

I use Hermes through the Hermes desktop app, the Conduit iOS app (official Hermes Agent iOS app when?), iMessage through Proton, and a private Discord bot. It can run commands, query APIs, and read the documentation while it investigates. If I ask it to compare an application's configuration with the running service, it can retrieve both without me copying each command and result between a chatbot and a terminal. It can also load the procedures I've saved and look up what happened in an earlier maintenance session.

I use a combination of models and have jumped between many over the past year. Currently, I'm defaulting to OpenAI's GPT-6.1 Sol and using Herdr to run Anthropic's Claude Opus 5.5 or Fable subagents where needed.

## Hermes in my homelab

Over time, as models got better, I slowly started to trust Hermes in my homelab more. Here are a few examples of troubleshooting and project work I've had Hermes do:

- One early repair involved a container marked unhealthy even though the application worked. Hermes found that the health check probed the wrong port. We corrected the check and recreated only that service, then verified the application and its dependencies.
- For a database-backed application upgrade, Hermes helped restore a backup into a separate database and rehearse the migration before the production cutover. Afterward, we checked existing record IDs, integrations, and previously imported content.
- We built a watchdog for the notification service itself. A script checks it every five minutes, reports an outage through a separate Discord path after repeated failures, and sends a recovery message once the checks succeed again. The recurring checks run without calling a model.

## Giving Hermes access

Over time, I noticed my default profile was starting to get confused with some homelab tasks. After some research, I learned about profiles and how they could help with this use case. I created a dedicated `homelab` profile instead of continuing to add infrastructure access to my general assistant. [Profiles](https://hermes-agent.nousresearch.com/docs/user-guide/profiles) keep configuration, sessions, memory, skills, and scheduled jobs separate. They organize the work, but they aren't an operating-system sandbox.

I started with an authenticated, read-only inventory of the lab. Before asking Hermes to maintain anything, I wanted it to establish what existed and which systems depended on each other.

My policy now lets Hermes carry out maintenance I've asked for once its pre-checks pass, as long as the work doesn't remove anything or risk irreversible data loss. I don't have to give a new instruction for every restart or configuration change along the way. If an action would remove something or could cause that kind of loss, Hermes needs my approval for the exact target and an explanation of what can be recovered. That includes upgrades that discard database fields and restores that overwrite newer data.

Lately, I'm finding that Hermes and the newer models are getting better at distinguishing high-impact maintenance from routine work. Cleanup still needs approval when it removes data or resources.

I have also started separating read-only API work from maintenance that needs write access across services such as Cloudflare, Proxmox, TrueNAS, and UniFi. Where possible, I use read-only credentials for discovery and restrict write access to specific maintenance tasks. Written rules don't reduce a credential's actual permissions.

## Custom Hermes skills

Hermes [skills](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills) are readable instructions it can load for a task. I use many of the built-in ones, but I've also created a few noteworthy custom skills.

### Homelab operations

This skill records the operating rules for the lab, including read-only discovery, checks before a change, and verification afterward. It also defines which maintenance Hermes can carry out and when it needs my approval for removal or irreversible data loss. That gives a new session a procedure to follow instead of making me explain the same boundaries again.

### Container updates

My container-update skill compares deployed images with available releases and reviews breaking changes, migrations, and active work before an update. It applies only the selected service update and then checks the application and its integrations. Database migrations get more preparation than routine updates, and an update request doesn't include permission to prune old containers, images, or volumes.

### Media automation

My media-automation skills trace problems through Sonarr or Radarr, the actual download client, and the files on disk. They check identity and import requirements before proposing a repair, rather than assuming that a completed download is ready to import. Queue or download-folder removal remains a separate approval step.

## Installing Proxmox through a GL.iNet KVM

As mentioned before, I have a clustered Proxmox setup with three HP EliteDesk G6 machines. I created the first node manually, but for the second and third, I used GPT-6.1 Sol's computer use to navigate the GL.iNet KVM interface, install Proxmox, and adopt each node into the cluster.

This was a mind-blowing experience to witness, and I highly recommend a KVM with a web GUI if you're setting up a homelab. Computer use is becoming so good at daunting tasks.

## Media troubleshooting

A primary use case for Hermes has been media troubleshooting. When a user was having difficulty with a movie or TV show they were trying to watch, I used to spend time debugging their setup or checking whether there was an issue with the media format I had.

Now, when a user submits an issue, Hermes automatically starts triaging and debugging it and, most of the time, fixes it without intervention. This has saved me countless hours.

## A spooky birthday celebration

My 30th birthday is coming up, and I came up with the idea of hosting a website for RSVPs. After a few prompts, I was able to get Hermes to make a Docker container and Cloudflare DNS entries to host the website. People used the site to RSVP, and I even created an interactive quiz about me that people could fill out.

The best part about having an always-on agent is that any idea that pops into my head can become a message to Hermes. Usually, within two or three rounds of back-and-forth, it can turn the idea into something real. It's truly amazing what I'm able to accomplish with my homelab right now.

## Building a Homarr dashboard

I was always jealous of people who made cool-looking homelab dashboards. I never had the time to set up and integrate my own. One night, I asked Hermes to do some research online about [Homarr](https://homarr.dev/) and build out a custom dashboard.

The next morning, I woke up with a Homarr subdomain and a beautiful dashboard. I was amazed. The only thing I had to do was ask it to change the theme colors.

## The walshit.com homepage

One of the first tasks I had my `coder` Hermes profile work on was a new page for [walshit.com](https://walshit.com/). I needed a way to give people a brief overview of what my homelab media server was about and a home for my other subdomains. Hermes was able to build a unique-looking site, set up the hosting, and secure it using Cloudflare. After a few changes to the look and feel, I now have a great landing page.

I'm probably missing a bunch of other use cases, and I'll continue to write about all the awesome ways I'm using Hermes. For now, I hope this inspires you to set up Hermes yourself or give one of these ideas a go.
