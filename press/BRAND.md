# Anonicall Brand Guidelines

## About Anonicall

Anonicall is a privacy-first communication platform powered by blockchain authentication. Users connect with their BSC wallet — no email, no phone number, no personal data. All messages are end-to-end encrypted. The aesthetic is cyberpunk / hacker terminal: dark, neon-lit, and unapologetically bold.

---

## Logo

### Files Provided

| File | Format | Use Case |
|------|--------|----------|
| `logos/anonicall-logo.svg` | SVG (dark bg) | Primary logo — websites, presentations, dark backgrounds |
| `logos/anonicall-logo-wordmark-light.svg` | SVG (transparent, dark text) | Light backgrounds, print |
| `logos/anonicall-logo.png` | PNG | General digital use |
| `logos/anonicall-logo-dark.png` | PNG | Dark background contexts |
| `logos/anonicall-logo-light.png` | PNG | Light background contexts |

### Logo Usage Rules

- **Do** use the provided logo files without modification.
- **Do** maintain clear space around the logo equal to the height of the "A" lettermark on all sides.
- **Do not** change the logo colors.
- **Do not** stretch, skew, rotate, or distort the logo.
- **Do not** place the logo on backgrounds that reduce legibility (e.g., busy photographs without contrast).
- **Do not** recreate the logo in other typefaces.

---

## Brand Colors

### Primary Palette

| Name | Hex | HSL | Usage |
|------|-----|-----|-------|
| **Neon Pink** | `#E82E8A` | `hsl(326, 81%, 54%)` | Primary brand color — CTAs, highlights, logo |
| **Dark Navy** | `#07091A` | `hsl(222, 65%, 7%)` | Main background |
| **Light Text** | `#EDEEF2` | `hsl(220, 10%, 94%)` | Primary text on dark backgrounds |

### Accent Palette

| Name | Hex | HSL | Usage |
|------|-----|-----|-------|
| **Neon Cyan** | `#08E8EB` | `hsl(185, 100%, 52%)` | Secondary highlights, links, taglines |
| **Neon Green** | `#22C55E` | `hsl(142, 71%, 48%)` | Success states, confirmations, wallet activity |
| **Neon Gold** | `#F9C21E` | `hsl(45, 96%, 53%)` | Warnings, premium tier indicators |
| **Neon Purple** | `#9D4EDD` | `hsl(269, 75%, 60%)` | AI assistant, secondary accent |
| **Deep Purple** | `#4C2A7A` | `hsl(269, 31%, 36%)` | Secondary elements |

### Color Usage Notes

- Dark Navy (`#07091A`) is the canonical background. Always pair with Neon Pink or Neon Cyan text accents for the authentic Anonicall look.
- Neon Pink is the signature color — use it for primary actions and critical brand moments.
- Neon Cyan is used for data, links, and secondary emphasis.
- Avoid using more than two neon colors simultaneously to prevent visual noise.

---

## Typography

### Wordmark Font
**Share Tech Mono** — Used exclusively for the "ANONICALL" wordmark and any UI display of the product name. This is a DIN1451-style monospace typeface that reinforces the hacker/terminal identity.

- Google Fonts: [Share Tech Mono](https://fonts.google.com/specimen/Share+Tech+Mono)
- Weight: Regular (400) / Bold simulated via letter-spacing

### UI Body Font
**Inter** — Used for all body copy, descriptions, and general UI text.

### Terminal / Matrix Aesthetic Font
**VT323** — Used for boot screens and stylized terminal paragraphs.

---

## Voice & Tone

- **Private**: Never reference personal data. The product never knows who you are.
- **Precise**: Technical and direct. No fluff.
- **Bold**: Cyberpunk confidence. Speak in declaratives.
- **Empowering**: The user is in control — not a platform, not an algorithm.

### Example Copy
- ✅ "No email. No phone. Just your wallet."
- ✅ "Encrypted. Anonymous. Yours."
- ✅ "Private communication, powered by blockchain."
- ❌ "We respect your privacy." (passive — implies we could choose not to)
- ❌ "Join our community!" (too warm / social-media-adjacent)

---

## Screenshots

App screenshots are provided in the `screenshots/` folder:

| File | Description |
|------|-------------|
| `screenshots/01-chat.jpg` | Private 1-on-1 encrypted chat with Circuit tabs and burn-after-read |
| `screenshots/02-wallet.jpg` | Portfolio dashboard, token list, and real-time BSC activity |
| `screenshots/03-ai-assistant.jpg` | Anonicall AI (JARVIS) — GPT-4o voice/text assistant |
| `screenshots/04-marketplace.jpg` | Marketplace shop dashboard — stats, product list, orders |
| `screenshots/05-hey-money.jpg` | Hey Money — crypto payment request across multiple chains |
| `screenshots/06-phantom-chat.jpg` | Phantom Chat — ephemeral anonymous encounter with reveal system |

All screenshots are **2560×1600 px** (1280×800 rendered at 2× pixel density), JPEG quality 92.

Screenshots may be used in editorial contexts (articles, reviews, app directory listings) without prior written permission, provided Anonicall is credited.

### Regenerating screenshots

Screenshots are rendered from design mockup components and captured with Puppeteer:

```bash
# 1. Start the mockup sandbox (runs on port 23636)
npm run dev   # or restart the "Component Preview Server" workflow

# 2. Run the capture script
node scripts/take-press-screenshots.mjs
```

To use a custom Chromium binary, set `CHROMIUM_PATH` before running:

```bash
CHROMIUM_PATH=/path/to/chromium node scripts/take-press-screenshots.mjs
```

Mockup source components: `artifacts/mockup-sandbox/src/components/mockups/press/`

---

## Media Inquiries

For press, partnership, and licensing inquiries, contact us directly via the app at **[anonicall.app](https://anonicall.app)** or reach the security team at **security@anonicall.app** for responsible disclosure.

---

*© Anonicall. All rights reserved. The Anonicall name, logo, and brand assets are proprietary. Unauthorized commercial use is prohibited.*
