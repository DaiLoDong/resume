---
title: Self-hosted Web Apps and Custom Domain
date: 2019-09-16
links:
  - type: site
    url: https://donger.ca
tags:
  - Docker
  - Linux
  - Networking
  - Cloudflare
---

What started as a way to play games with friends during COVID has grown into a personal infrastructure platform serving **30+ web apps** to friends and family, with monitoring, alerting, and security that mirrors what I work on professionally.
<!--more-->

## How it started

I've always had an itch to tinker, and COVID gave me the time to scratch it. The first version of this project was a handful of self-hosted game servers. Just somewhere free and on all the time so my friends and I could play whenever we wanted, without depending on whoever happened to be hosting that night.

That shortly became a Windows Server running under my desk, built from spare parts out of an old PC. It hosted a private TeamSpeak 3 server, various game servers using headless Steam, and some small-scale file sharing.

Looking back, that scrappy first setup is where I learned the fundamentals: port forwarding, DNS, the difference between a local and a public IP, why "it works on my LAN" doesn't mean it works on the internet, and all the frustrating ways networking breaks.

## Moving in and going Linux

Buying my first home meant more space and more opportunity to take the project seriously. It also felt like the right moment to stop hiding behind a familiar OS, so I committed to learning Linux properly. I picked Debian on the recommendation of a friend that works as a computer repair technician. He assured me Debian was beginner-friendly and well documented, and it's been the foundation of my infrastructure since I took his word for it.

## Where it is today

The current platform runs **30+ containerized web apps** across three machines, all orchestrated with Docker and managed centrally through Komodo. The mix has grown well beyond game servers. There's a private media server, photo backup, document tools, PDF utilities, collaborative whiteboards, and a self-hosted Google Suite replacement, among others. A handful of them are now part of my and my family's daily routines.

### Reliability

Running apps is the easy part. Keeping them up is where it builds user's trust.

I use **Beszel** for system-level metrics and **Uptime Kuma** for service-level checks, with **Apprise** and Discord webhooks so alerts land in my inbox over SMTP and on Discord. The setup has held a **rolling 12-month uptime above 99.90%** which is a number I'm proud of mainly because it forced me to think about *how/why* things fail and strategies to prevent these failures. Recursively, this has improved significantly with each successive failure.

### Security

The other half of the problem is keeping the wrong people out. Anything that needs to be reachable from the internet sits behind **Cloudflare Tunnels** acting as a reverse proxy, so my home network is never exposed directly. Most public-facing apps are gated by **Cloudflare Access** policies with **GitHub OAuth** as the identity provider, which gives me real authentication on apps that were never designed to have it.

## Why I keep doing it

First and foremost, I do it for myself. I use these apps multiple times a day and they genuinely make my life easier. But the more interesting answer is that this hobby has been one of the most useful learning environments I've had. A lot of what I run into here (orchestration, monitoring, identity, secure exposure, debugging weird failure modes at 11 pm) shows up in some form in my professional work as a data engineer. Getting reps on it at home has made me noticeably better at it during the day. You also develop an eye for failure. This helps develop a taste for something off or odd and helps me catch things before they go awry in production.