---
title: Personal Wedding Website
date: 2025-11-12
links:
  - type: site
    url: https://github.com/DaiLoDong/wedding
tags:
  - wedding
  - custom-website
  - front-end
  - back-end
---

When my wife and I started planning our wedding, the standard canned "custom" website templates didn't sit right with me. Paper invites get misplaced, physical RSVP cards can take weeks to arrive (if we are lucky and Canada Post isn't on strike), and an evergrowing FAQ isn't a sustainable solution. 

I wanted something better. I could build something better.
<!--more-->

## Why a custom site

Why buy an off the shelf suit, when you can get one tailored for you.

I could have used one of the off-the-shelf wedding website builders. They're ok. But "ok" wasn't really good enough for a wedding, much less my own wedding. I wanted a single link that guests could open on any device, find everything they needed in a handful of seconds and act on without friction. I honestly just did not want emails with questions.

I am very particular about the user experience. I am one of those users who has a custom config for everything I use. Every feature on the site started as a real question a guest asked us (before the site was even live!), or a real moment of friction I had experienced at another wedding. If it took more than 15 seconds to answer, I considered that too cumbersome.


## What the site does

The site became the central landing page for everything wedding related. Some highlights:

### Guest experience

- **Fully responsive design** that works on every device, screen size, and aspect ratio.
- **One-tap RSVP** that writes directly to a Google Sheet via a Google Apps Script REST endpoint. No third party form service, no signup required.
- **Digital seating chart** searchable by either guest name or table number using a lightweight JS string search.
- **Add to Calendar** with support for Google, iCal, Outlook, and Yahoo. Whichever ecosystem the guest prefers.
- **Countdown timer** showing time remaining until the ceremony.
- **Embedded venue video** with a fallback image on mobile to keep things fast.

### Travel and logistics

- **Interactive Google Maps** powered by the Google Maps Platform API, showing both the ceremony and reception locations with directions.
- **Flight booking shortcut** that auto-detects the visitor's location and pre-fills the origin city and event date.
- **Weather forecast** for the wedding date via a third-party API. Important because the ceremony was outdoors and rain is always a probability in Victoria.

### Event gallery (the crowd favourite)

This one was the most fun to build. Guests could upload their event photos directly through the site and watch the gallery update live for everyone else viewing it.

- A **Cloudflare Worker** handles uploads, retrievals, and CORS headers.
- Image data is stored on a private image host.
- **Cloudflare KV** acts as a lightweight database for metadata.

The result was a shared, real-time photo wall that captured candid moments from dozens of angles I would have never gotten from a single photographer.

### Behind the scenes

- **Automated email alerts** to my inbox the moment anyone RSVPs, handled by Google Apps Script triggering Gmail sends so I always know the expected head count.
- **Custom domain** hosted on GitHub Pages and routed through my own Cloudflare domain, with full DNS control and analytics.

## Retrospective

Building this taught me more about shipping product than most professional projects I've worked on. I was the developer, the designer, the QA, and a user. It's not often you sit on every side of a project at once, and it makes you a lot more aware of tradeoffs. The right technical decision and the right design decision aren't always the same one. 

The reward was watching it actually work on the days leading up to the wedding and of course on the day itself. Having guests RSVP within hours of the site going live and using the gallery in real time during the reception brought a great feeling of accomplishment. A few guests told us, unprompted, that it was the smoothest wedding logistics they'd ever experienced.

With how much weddings cost, the cherry on top was it's all free.


## Stack

**Frontend:** HTML, CSS, JavaScript
**Hosting:** GitHub Pages with a custom Cloudflare-routed domain
**APIs & Integrations:** Google Maps Platform, Google Apps Script (RSVP + Gmail automation), Cloudflare Workers, Cloudflare KV, third-party weather API
**Other:** Embedded YouTube with mobile fallback, multi-calendar export