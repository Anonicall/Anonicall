# Anonicall Press Kit

## Screenshots

### Desktop (1280×800 @ 2x)

Located in `press/screenshots/`:

| File | Feature |
|------|---------|
| `01-chat.jpg` | Encrypted chat with E2E messaging, circuit tabs, and burn messages |
| `02-wallet.jpg` | Multi-chain wallet with portfolio, assets, and BSC activity feed |
| `03-ai-assistant.jpg` | JARVIS AI assistant powered by GPT-4o |
| `04-marketplace.jpg` | Shop dashboard with listings, orders, and revenue stats |
| `05-hey-money.jpg` | Hey Money crypto payment requests across chains |
| `06-phantom-chat.jpg` | Phantom Chat — ephemeral anonymous encounters with Reveal system |

### Mobile Portrait (390×844 @ 2x = 780×1688px)

Located in `press/screenshots/mobile/`:

| File | Feature |
|------|---------|
| `01-chat.jpg` | Chat list with circuit filters, online presence, and unread badges |
| `02-wallet.jpg` | Mobile wallet with portfolio hero card and token list |
| `03-ai-assistant.jpg` | JARVIS AI mobile interface with streaming response |
| `04-marketplace.jpg` | Shop dashboard with cover, stats, and product list |
| `05-hey-money.jpg` | Hey Money payment requests with pay-now action |
| `06-phantom-chat.jpg` | Phantom Chat with reveal request and ephemeral notice |

Mobile screenshots are suitable for App Store previews, social media stories, and portrait-format press placements.

### Mobile Portrait — Phone Framed (1290×2796px, App Store ready)

Located in `press/screenshots/mobile/framed/`:

| File | Feature |
|------|---------|
| `01-chat.png` | Chat list — in phone frame |
| `02-wallet.png` | Wallet — in phone frame |
| `03-ai-assistant.png` | JARVIS AI — in phone frame |
| `04-marketplace.png` | Marketplace — in phone frame |
| `05-hey-money.png` | Hey Money — in phone frame |
| `06-phantom-chat.png` | Phantom Chat — in phone frame |

Framed screenshots are production-ready for App Store listings, press releases, and social media. The phone frame uses the Anonicall cyberpunk aesthetic (dark bezel, pink/purple glow background, pill notch).

Served at: `/press/screenshots/mobile/framed/<filename>`

## Regenerating Screenshots

**Desktop:**
```bash
node scripts/take-press-screenshots.mjs
```

**Mobile (bare):**
```bash
node scripts/take-press-screenshots-mobile.mjs
```

**Mobile (phone framed):**
```bash
node scripts/frame-press-screenshots-mobile.mjs
```

The frame script reads from `press/screenshots/mobile/` and writes to `press/screenshots/mobile/framed/`. Run the mobile capture script first if source screenshots are missing.

Both capture scripts require the mockup sandbox to be running on port 23636.

## Branding

See `press/BRAND.md` for color palette, typography, and logo usage guidelines.

Logos are available in `press/logos/`.
