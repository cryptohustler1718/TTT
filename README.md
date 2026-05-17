# Ten Thousand Tokens — Protocol Calculator

A production-ready, fully static interactive calculator and protocol analysis tool for the [Ten Thousand Tokens](https://www.tenthousandtokens.net) NFT collection.

## ⚡ Before you deploy

**Step 1 — Set your ETH tip address**

Open `index.html` and find this line (around line 160):

```html
<div class="eth-addr" id="ethAddr">0xYOUR_ETH_ADDRESS_HERE</div>
```

Replace `0xYOUR_ETH_ADDRESS_HERE` with your actual Ethereum wallet address. This is what gets copied when visitors click "Send a tip."

---

## 🚀 Deploy: GitHub → Vercel

### 1. Create a GitHub repository

Go to [github.com/new](https://github.com/new):
- **Repository name:** `ttt-calculator` (or anything you like)
- **Visibility:** Public
- Click **Create repository**

### 2. Push your files

```bash
# In this project folder:
git init
git add .
git commit -m "feat: TTT protocol calculator"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/ttt-calculator.git
git push -u origin main
```

### 3. Deploy on Vercel

1. Go to [vercel.com](https://vercel.com) — sign in with GitHub
2. Click **Add New… → Project**
3. Click **Import** next to `ttt-calculator`
4. Settings:
   - **Framework Preset:** Other
   - **Root Directory:** `./`
   - **Build Command:** *(leave empty)*
   - **Output Directory:** `./`
5. Click **Deploy**

Vercel detects static HTML automatically. Your site will be live at `https://ttt-calculator.vercel.app` within ~30 seconds.

### 4. Custom domain (optional)

In Vercel → Project → **Settings → Domains → Add**:
- Enter your domain (e.g. `tttcalculator.xyz`)
- Add a `CNAME` record in your DNS pointing to `cname.vercel-dns.com`
- Vercel provisions HTTPS automatically via Let's Encrypt

### 5. Future updates

Any `git push` to `main` auto-deploys. Zero downtime. Preview URLs are generated for every branch.

```bash
# Make a change, then:
git add .
git commit -m "update: improved chart labels"
git push
# → auto-deploys in ~20 seconds
```

---

## 🏗️ Why this scales infinitely

| Property | Detail |
|---|---|
| **Architecture** | 100% static — HTML + CSS + JS, no server |
| **CDN** | Vercel edge network, 100+ global PoPs |
| **Chart.js** | Loaded from Cloudflare's cdnjs (not your domain) |
| **Fonts** | Loaded from Google Fonts CDN |
| **Concurrency** | Unlimited — static files served from cache |
| **Vercel free tier** | 100 GB/month bandwidth, handles millions of visits |
| **No database** | All calculations run client-side in browser |

---

## 🧮 Verified fee math

Per the Ten Thousand Tokens whitepaper (§8–9):

- **1% of every swap amount** → FeeSplitter (both buys at resting rate and sells)
- **Decay surplus** (99% → 1% over 98 blocks on buys) → buyback reservoir (separate, not FeeSplitter)
- **FeeSplitter split:** 50% launcher · 30% holders · 10% TokenWorks · 10% PNKSTR
- **Holder pool** is shared pro-rata across all unburned NFTs from ALL launched tokens

### Example — 100 tokens, $1M avg volume each:
```
Total volume:     100 × $1,000,000 = $100,000,000
Total fees (1%):  $1,000,000
Holder pool (30%): $300,000
Remaining holders: 9,900
Per holder:        $300,000 / 9,900 ≈ $30.30
Launcher (avg):    $1,000,000 × 50% / 100 = $5,000 per launcher
```

---

## 📁 File structure

```
ttt-calculator/
├── index.html      ← entire app (self-contained)
├── vercel.json     ← security headers + cache config
└── README.md       ← this file
```

---

## ⚠️ Disclaimer

This is an independent analytical tool. Not financial advice. Protocol mechanics sourced from the publicly available TTT whitepaper. All on-chain interactions are irreversible — always verify independently.
