# 🏸 Unplugged Badminton

A session sign-up app for **Unplugged - Badminton**, a community under [IPA
Singapore](https://ipasg.com) (Indonesian Professionals Association). It
replaces manual headcounts in the group chat with a real first-come,
first-served sign-up flow, an automatic waitlist, and email notifications —
available both as a normal web page and as a Telegram Mini App.

**Live app:** https://gjsjessy.github.io/unplugged-badminton/
*(also opens directly inside Telegram as a Mini App)*

---

## What it does

- **Post a session** — date, time, location, court, organiser, price per
  player, number of spots, and skill level (Open to all / Beginner /
  Intermediate / Advanced / Intermediate & Advanced).
- **Join a session** — with name, email, optional phone, and your own level.
  Bring guests along in the same sign-up.
- **Automatic waitlist** — once a session fills up, new sign-ups land on a
  waitlist and are promoted in order the moment a spot opens, with an email
  to match.
- **Self-service cancel** — drop your own spot, or an organiser can cancel or
  reactivate an entire session (with a reason, and an email to everyone
  affected).
- **One live roster per session** — confirmed players and waitlist, organiser,
  price, and level all visible on a single board, plus an "Add to Google
  Calendar" link once you're in.
- **Accounts, not just a name in a box** — sign in with email + password, or
  (once the group has fully moved over) with Telegram. Signing in with
  Telegram links straight to an existing email account so nobody's history
  gets split across two identities.

## Why it exists

Sessions used to be organised as numbered lists typed into the WhatsApp group
— no real waitlist, no notifications, cancellations easy to lose in the
scroll. This app keeps the same first-come-first-served spirit the group
already used, but makes the bookkeeping automatic.

## How it's built

Two files, two places to deploy, one Google Sheet as the database:

| Piece | What it is | Where it lives |
|---|---|---|
| `index.html` | The entire front end (HTML/CSS/vanilla JS) | This repo, served by GitHub Pages |
| `Code.gs` | The entire backend | A Google Apps Script project (not in this repo) |
| The data | `Users`, `Sessions`, `Registrations`, `Tokens`, `PasswordResets` tabs | A Google Sheet bound to the Apps Script project |

`index.html` is deliberately a single file shared by both deployments. It
detects at runtime whether it's being served by Apps Script
(`google.script.run` exists) or statically by GitHub Pages (it doesn't) and
talks to the backend either way — so there's one source of truth for the UI
instead of two copies that can drift apart.

Telegram opens the GitHub Pages URL as a Mini App, using Telegram's own
sign-in flow (`initData`, verified against the bot token) to recognise
returning players.

**Stack:** vanilla HTML/CSS/JS front end · Google Apps Script backend ·
Google Sheets as the database · Telegram Bot API for the Mini App · GitHub
Pages for static hosting.

## Status

Live and in active use by the group. Currently gathering real usability
feedback from players (registering, cancelling, getting promoted off the
waitlist) before the next round of polish.

**On the radar:**
- Registering more than one person at once for a partner or friend in a
  single tap ("+1").
- Remembering returning players so they don't have to re-enter their details
  every session.
- A better bridge back to WhatsApp, since the app can't push notifications
  there directly (e.g. a share / deep-link button).

## Design

Designed and built by [Jessica](https://github.com/gjsjessy), a UX/product
designer, for the IPA Singapore badminton community. Visual identity is
carried over from [ipasg.com](https://ipasg.com) — red for calls to action,
grey/black neutrals, Poppins for type.
