---
title: Personal Wedding Website
date: 2025-11-12
links:
  - type: site
    url: https://github.com/DaiLoDong/wedding
tags:
  - wedding
  - custom-website
---

When the love of my life and I started planning our wedding, the standard playbook didn't sit right with me. Paper invites get buried in drawers, RSVP cards take weeks to arrive (if we are lucky and Canada Post isn't on a strike), and the moment a guest has a question: *what time does it start? Where do I park? Can I bring a plus-one?* they're stuck digging through old emails or texting one of us sent at midnight. I wanted something better. So I built it.
<!--more-->

## Why a custom site

I could have used one of the off-the-shelf wedding website builders. They're fine. But "fine" wasn't what I wanted for one of the most important days of our lives, and I knew exactly the experience I was chasing: **one link that guests could open on any device, find everything they needed in seconds, and act on without friction.** RSVP in one tap. Get directions in one tap. Add the event to their calendar. Check the weather, book a flight, find their seat. All without leaving the page or emailing me.

I'll admit I got obsessive about the user experience. Every feature on the site started as a real question a guest asked us, or a real moment of friction I noticed someone else hit at a wedding I'd been to. If it took more than two taps to answer, I considered that unacceptable.

## What the site does

The site became the single landing page for everything wedding related. Some highlights:

### Guest experience

- **Fully responsive design** that works on every device, because the majority of guests opened it on their phones
- **One-tap RSVP** that writes directly to a Google Sheet via a Google Apps Script REST endpoint. No third party form service, no signup required
- **Digital seating chart** searchable by either guest name or table number using a lightweight JS string search
- **Add to Calendar** with support for Google, iCal, Outlook, and Yahoo. Whichever ecosystem the guest prefers
- **Countdown timer** showing time remaining until the ceremony
- **Embedded venue video** with a fallback image on mobile to keep things fast

### Travel and logistics

- **Interactive Google Maps** powered by the Google Maps Platform API, showing both the ceremony and reception locations with directions
- **Flight booking shortcut** that auto-detects the visitor's location and pre-fills the origin city
- **Weather forecast** for the wedding date via a third-party API. Important because the ceremony was outdoors and I didn't want anyone showing up in the wrong shoes

### Event gallery (the favourite feature)

This one was the most fun to build. Guests could upload their event photos directly through the site and watch the gallery update **live** for everyone else viewing it.

- A **Cloudflare Worker** handles uploads, retrievals, and CORS headers
- Image data is stored on a private image host
- **Cloudflare KV** acts as a lightweight database for metadata

The result was a shared, real-time photo wall that captured candid moments from dozens of angles I'd never have gotten from a single photographer.

### Behind the scenes

- **Automated email alerts** to my inbox the moment anyone RSVP'd, handled by Google Apps Script triggering Gmail sends — so I always knew the count was current without having to refresh the sheet
- **Custom domain** hosted on GitHub Pages and routed through my own Cloudflare domain, with full DNS control

## What I learned

Building this taught me more about **end-to-end product thinking** than most professional projects I've worked on. When you're the developer, the designer, the QA, *and* one of the users, every shortcut you take comes back to bite you within a week. I rewrote the RSVP flow three times before I was happy with it. I obsessed over how the seating-chart search behaved when guests typed half a name. I tested the calendar feature on borrowed phones to make sure it worked on operating systems I'd never used.

The reward was watching it actually get used the way I'd hoped. Guests RSVP'd within hours of the site going live. People used the gallery in real time during the reception. A few guests told us, unprompted, that it was the smoothest wedding logistics they'd ever experienced — which was exactly the bar I'd set.

It also turned into one of my favourite technical projects because of how much of the stack I touched: frontend, responsive design, serverless functions, multiple third-party APIs, a custom domain pipeline, and a lightweight backend held together by Cloudflare Workers and Google Apps Script. All for free, all under my own infrastructure.

## Stack

**Frontend:** HTML, CSS, JavaScript
**Hosting:** GitHub Pages with a custom Cloudflare-routed domain
**APIs & Integrations:** Google Maps Platform, Google Apps Script (RSVP + Gmail automation), Cloudflare Workers, Cloudflare KV, third-party weather API
**Other:** Embedded YouTube with mobile fallback, multi-calendar export
