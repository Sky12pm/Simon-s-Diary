# Simon Riley — Interactive Artifacts

> *"If this letter ever reaches you... Pretend it didn't."*
> — Simon Riley

---

## What is this?

This repository holds two interactive, single-file experiences built around the same character: **Simon Riley** — a fictional Formula 1 version of Ghost (Call of Duty), racing for Red Bull Racing.

Neither of these is "just a webpage." Both are hand-crafted, immersive artifacts designed to feel like real objects you've stumbled onto — a notebook he never meant for anyone to read, and a phone he left unlocked by accident. No frameworks, no build steps, no unnecessary dependencies. Open the file, and it works.

- 📓 **[Diary](#-diary)** — a leather-bound notebook full of things he never said out loud
- 📱 **[iPhone Simulation](#-iphone-simulation)** — a fully functional phone simulation, app by app

---

## 📓 Diary

### The concept

Simon Riley doesn't talk about his feelings. He races. He wins. He disappears before the ceremony ends.

But somewhere between the pit lane and the podium, between telemetry sheets and pre-race briefings, he wrote things down. Small things. Big things. Things he crossed out and rewrote and crossed out again.

This diary is what he left behind — or what he forgot to burn.

### What's inside

The diary opens with a **leather-bound cover** sitting on a dark wooden desk, worn at the corners, with stickers collected over the years — a Ghost skull sticker, a mugshot badge, a license plate that reads *MEMORIES*. A leather cord holds it shut. It looks like it has a story. It does.

Inside, spread across **7 double-page spreads**, you'll find:

- **A love letter** — two full pages, handwritten style, never meant to be sent
- **Post-it notes** stuck to pages — thoughts too short for a full entry, too loud to ignore
- **A lost to-do list** — *"Buy coffee. Review telemetry. Ignore {{user}}."* (he failed the last one)
- **A strategy note from the Spanish GP** — with checkboxes. Two are ticked. One isn't.
- **A torn page** — something was ripped out. What's left is enough.
- **Diary entries, scattered thoughts, handwritten notes** — the kind of writing that only happens at 2am
- **A telemetry sheet with a name scribbled on it** — crossed out. Three times. Still visible.

### Design & details

Every element was built with intention.

**The cover** feels like a real object — the leather texture, the aged corners, the cord wrapped around it are all CSS, no images. The stickers were chosen deliberately: they say something about who this person is without him ever having to say it out loud.

**The pages** use a handwriting font that makes every word feel personal. The paper is aged, ruled with faint lines, with a red margin line on the left — like a real notebook pulled off a shelf.

**The spread layout** shows two pages at a time, exactly like opening a physical book. On mobile, you swipe left and right to turn pages. On desktop, you use the arrows on either side.

**Mixed media throughout** — not every page looks the same. Some have post-its, some have documents, some have objects from the paddock. The variety makes it feel like a real diary that accumulated things over time, not a designed template.

**The zoom** — on the cover, you can scroll (or pinch on mobile) to zoom into the stickers and texture details before opening the diary. It rewards curiosity.

### Technical details

Built entirely in **vanilla HTML + CSS + JavaScript** — no frameworks, no dependencies, nothing external beyond Google Fonts.

- ✓ Single `.html` file — open it anywhere, share it as one file
- ✓ Mobile-first — designed to feel natural on phone screens
- ✓ Swipe to turn pages on touch devices
- ✓ Scroll/pinch to zoom on the cover
- ✓ All images embedded as base64 — nothing breaks no matter where it's hosted
- ✓ Google Fonts loaded for the handwriting and display typefaces

**Fonts used:** Cinzel · Teko · Caveat · JetBrains Mono
**Core techniques:** CSS 3D transforms · clip-path · SVG inline · base64 image embedding · touch event handling

### Context

The love letter inside was written for a rivals-to-lovers scenario set during the Monaco Grand Prix qualifying session. The other entries fill in the gaps between races — the silence he keeps in interviews, the thoughts he doesn't say out loud, the name he keeps writing down and crossing out.

---

## 📱 iPhone Simulation

### The concept

Imagine borrowing this character's phone for a day. Not a gallery of pretty screens pretending to be an app — an iPhone that actually *works*, where every app reveals a piece of who this person is, without a single line of dialogue explaining it.

That's what this project set out to build: a complete iPhone simulation, entirely in one HTML file. No frameworks, no build step, no external dependencies beyond a single call to the SoundCloud player. Open it in a browser, and it just works — tap, type, play, navigate.

### What's inside

- **Lock Screen & Home Screen** — wallpaper, unlock animation, and a navigable app grid, styled like real iOS.
- **Phone** — contacts, favorites, call history, and a voicemail inbox, each contact with its own photo and context.
- **Messages** — real conversations with multiple contacts, timestamps, read receipts, and even a scripted "typing..." moment mid-conversation — small details that make the interface feel lived-in, not static.
- **Gramly** — a fictional social network with a profile, posts, and the character's visual aesthetic.
- **Playback** — a functional music player, streaming a real playlist via SoundCloud, with the actual player hidden and only custom controls visible — it feels native.
- **Calendar** — a full race-weekend schedule, with attachments that open like real documents (including a heart-rate report with a chart) and voice notes with text highlighting synced to the "speech."
- **Sudoku** — the technical detail I'm proudest of: **it's not a randomly generated Sudoku**. It's a fixed board with a single verified solution, validated by a backtracking algorithm — every row, column, and 3×3 block is mathematically guaranteed correct. The player literally picks up exactly where the character left off.

### How it was built

Everything runs on **plain HTML + CSS + JavaScript** — no React, no UI libraries. The architecture is based on a "screens" system (each app is a `<div class="screen">` that appears/disappears with transitions), simple JavaScript-based navigation, and data centralized in JS objects (contact lists, message threads, calendar events) that feed rendering functions — so adding a new message or event just means editing an object, not rebuilding HTML by hand.

The visuals follow a consistent design system: a dark palette (black, graphite, gold, blood red), Bebas Neue + Space Mono typography, and shared components reused across every screen (top bar, back button, message bubbles) — the kind of visual discipline that makes a project feel professional instead of a patchwork of screens.

---

## How to use

**Option 1 — Direct:**
Download the `.html` file and open it in any browser. That's it.

**Option 2 — Hosted:**
The live version is available at:
👉 `[your GitHub Pages link here]`

---

## Credits & notes

- Concept, writing, and design direction by **Sky12pm**
- Built with [Claude](https://claude.ai) (Anthropic)
- All written content is original fiction
- Character Simon Riley / Ghost belongs to Activision · Call of Duty franchise

---

## Using this project

Feel free to use this code as a base or inspiration for your own interactive diary, character artifact, or creative project — just make sure to give proper credit.

If you use, adapt, or build upon this project, please include a visible credit somewhere in your work:

```
Original project: Diary & iPhone Simulation — Simon Riley
Created by: Sky12pm
Built with: Claude (Anthropic)
Source: github.com/Sky12pm/Diary-Simon-Riley
```

You're free to:
- ✓ Use the code as a learning reference
- ✓ Adapt the layout and structure for your own character/project
- ✓ Share it, as long as you link back to this repository

Please don't:
- ✖️ Republish it as entirely your own work without credit
- ✖️ Use the original written content (letters, diary entries, character notes) without permission — those are original fiction and belong to their creator
- ✖️ Remove the credit section from the code itself

> *This project was made with a lot of care and detail. If it inspired something in you, that's exactly what it was meant to do — just carry the name forward.*

---

*He said to burn it.*
*You didn't.*
*Good.*
