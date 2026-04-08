# 🎂 Birthday Surprise Page

A fully interactive, customizable birthday surprise page with a disguised clicker game that reveals the birthday message only after the recipient earns it.

**Live demo:** [chrissy.mivator.com](https://chrissy.mivator.com)

---

## How it works

1. The recipient opens the link and sees only a mystery game — **no birthday hints**.
2. They click a button **N times** (default: 30) to unlock the surprise.
3. The game overlay fades away, revealing the birthday page with confetti, balloons, and a full celebration.

---

## Customization

Everything is driven by `config.json`. Edit it to make the page your own:

```json
{
  "name": "Chrissy",
  "avatar_url": "https://avatars.githubusercontent.com/u/68145571?v=4",
  "badge": "🎉 B-Day Boss!",
  "subtitle": "Your personalized birthday message here.",
  "interests": [
    { "icon": "terminal",       "label": "OSS Developer"   },
    { "icon": "sports_esports", "label": "Anno & Fortnite" },
    { "icon": "location_on",    "label": "Austria 🇦🇹"     }
  ],
  "stats": [
    { "value": "∞",  "label": "Lines of Code", "color": "primary"   },
    { "value": "1",  "label": "Their Name",     "color": "secondary" },
    { "value": "🏆", "label": "Legend Status",  "color": "tertiary"  }
  ],
  "footer": "Built with love for Someone",
  "game": {
    "clicks_needed": 30,
    "title": "Psst.\nFriend. 👀",
    "subtitle": "Someone left something for you.\nBut you gotta earn it first. 😈"
  }
}
```

| Field | Description |
|---|---|
| `name` | Recipient's name — used throughout the page and messages |
| `avatar_url` | Profile picture URL (GitHub avatar, direct image link, etc.) |
| `badge` | Text on the small badge below the profile photo |
| `subtitle` | The paragraph shown after the big heading |
| `interests` | Array of `{ icon, label }` — `icon` is any [Material Symbol](https://fonts.google.com/icons) name |
| `stats` | Array of `{ value, label, color }` — `color` is `primary`, `secondary`, or `tertiary` |
| `secret_message` | Message revealed after 8 "Cheers" button clicks on the birthday page |
| `footer` | Footer line at the bottom |
| `toast_messages` | Array of strings shown when clicking "Cheers to you!" — use `{name}` as a placeholder |
| `chaos_labels` | Array of button labels that cycle when clicking 12+ times |
| `profile_messages` | Array of messages shown when clicking the profile photo — use `{name}` |
| `game.clicks_needed` | How many clicks to beat the game (default: 30) |
| `game.title` | Title shown on the game overlay (`\n` for line breaks, `{name}` supported) |
| `game.subtitle` | Subtitle on the game overlay |
| `game.win_title` | Heading shown on the win screen |
| `game.win_subtitle` | Subtext shown on the win screen |
| `game.milestones` | Object mapping click number → message shown during the game |
| `game.button_labels` | Object mapping click threshold → game button label |

---

## Features

- **Mystery clicker game** — recipient has no idea it's a birthday page until they win
- **Canvas confetti** — themed to purple/pink/cyan palette, fires on every interaction
- **Floating balloons** — emoji balloons drift up from the bottom
- **Escalating button chaos** — "Cheers to you!" button gets progressively unhinged after each click
- **Clickable profile photo** — wiggles and shows fun messages
- **Cursor sparkle mode** — unlocks after 5 cheers clicks
- **Rainbow title** — the name animates into rainbow after 3 clicks
- **Secret message** — hidden card that appears at click 8
- **Nav icon interactions** — celebration and cake icons trigger their own effects
- **40+ toast messages** — cycling through developer humour, game references, and birthday wishes

---

## Deployment

It's a single static HTML file — no build step, no dependencies except CDN-loaded Tailwind CSS and Google Fonts.

**Nginx example:**

```nginx
server {
    server_name yourdomain.com;
    root /var/www/your-bday-page;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Then get a free SSL cert:

```bash
certbot --nginx -d yourdomain.com --non-interactive --agree-tos --redirect
```

**Or serve locally:**

```bash
npx serve .
# open http://localhost:3000
```

> `config.json` is fetched at runtime via `fetch('./config.json')`. If you open `index.html` directly as a `file://` URL, the config fetch will fail silently and the page will use its built-in defaults — which is fine for testing.

---

## Tech stack

- Plain HTML + CSS + vanilla JS (zero build tooling)
- [Tailwind CSS](https://tailwindcss.com) via CDN
- [Material Symbols](https://fonts.google.com/icons) via Google Fonts
- [Let's Encrypt](https://letsencrypt.org) / Certbot for HTTPS
