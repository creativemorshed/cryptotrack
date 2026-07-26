# 📊 CryptoTrack v4.3

> একটি personal crypto portfolio tracker — Progressive Web App (PWA)

**Live:** `https://morshed.github.io` | **Stack:** Vanilla HTML/CSS/JS + Firebase + CoinGecko API

---

## 🚀 Features

### 🔐 Authentication
- Google Sign-In via Firebase Auth
- সব device-এ real-time cloud sync (Firestore)
- User avatar-এ gradient ring সহ header-এ

---

### 💰 Portfolio Overview

#### Current Portfolio Balance Card
- **Capital** — manually set করা main investment
- **P&L $** — সব coin-এর মোট লাভ/লস
- **P&L %** — Capital-এর বিপরীতে percentage

#### Spot Balance & Future Balance Cards
- দুটো আলাদা balance card পাশাপাশি
- **Spot Balance** = Spot Capital + Spot coin P&L
- **Future Balance** = Future Capital + Long/Short coin P&L
- Profile থেকে আলাদাভাবে SET করা যায়

---

### 🪙 Position Types

| Type | Description |
|------|-------------|
| 🪙 **Spot** | Leverage নেই, Capital limit আছে |
| 📈 **Long** | Leverage সহ, price বাড়লে লাভ |
| 📉 **Short** | Leverage সহ, price কমলে লাভ |

---

### ➕ Buy Management

#### Add Buy
- Coin search (CoinGecko API)
- Quantity, Buy Price, Date, Note
- Long/Short-এ **Leverage** field (P&L% calculation-এ ব্যবহৃত)
- **Real-time preview** — Qty দিলেই Average Price দেখায় (buy price না দিলে current price দিয়ে estimate)
- DCA preview: avg buy price, new qty, P&L%

#### Edit Buy ✎
- প্রতিটা buy entry-তে ✎ বাটন
- Quantity, Price, Leverage, Date, Note সব update করা যায়
- Firestore-এ instant save

#### Delete Buy ✕
- Individual buy entry delete
- পুরো coin remove করা যায়

---

### 📐 Leverage System
- **Spot** — Leverage নেই (1×)
- **Long/Short** — Add/Edit Buy-এ leverage set করা যায়
- Balance সব জায়গায় **margin (invested)** দেখায়
- **P&L%** = actual price move × leverage
- Coin card-এ leverage badge দেখায় (যেমন `20×`)

---

### 💵 Capital Management

Profile icon → **Spot Capital SET** বা **Future Capital SET**

```
Current Portfolio Balance = (Spot Capital + Spot P&L) + (Future Capital + Future P&L)
```

#### Spot Capital Limit
- Spot-এ buy করার সময় Capital-এর বেশি invest করা যাবে না
- Available balance real-time দেখায়
- Exceeded হলে error toast দেখায়

---

### 📈 Coin Cards
- Live price (CoinGecko, 2 min auto-refresh)
- 24h price change %
- DCA stats: Avg Buy, Margin, P&L
- Buy history সব entry দেখায়
- **Coin icon** — চারপাশে accent color border ring
- **Dropdown arrow** — coin icon-এর নিচে
- Long name truncate হয় (`Venice To...`), card expand করলে full name দেখায়
- সব price ও quantity **2 decimal** format-এ

---

### 📊 Allocation Section
- `▶ ALLOCATION` pill button — click করলে toggle
- Gradient background সহ distinct card design
- Thicker bar, accent color label
- Percentage breakdown সব coin-এর

---

### 📊 Sections
- **SPOT** — Spot holdings
- **LONG** — Long positions
- **SHORT** — Short positions
- 0 holdings হলে section hide হয়
- Click করলে toggle (expand/collapse)

---

### 🔒 Privacy Mode
- Header-এ 👁 বাটন — সব balance blur হয়ে যায়

---

### 🔄 Sync & Refresh
- Header-এ circular arrow — manual price refresh
- প্রতি ২ মিনিটে auto-refresh
- Sync dot: 🟢 Synced / 🟡 Syncing / 🔴 Error
- Price fetch fail হলে Retry banner

---

### 🎨 UI/UX
- Glassmorphism design — light blue gradient background
- Semi-round icon buttons (👁 Hide, 🔄 Refresh, Avatar)
- Profile avatar-এ gradient ring
- Coin name truncate with `...`
- সব card value 2 decimal format

---

### 📱 PWA Features
- Home screen-এ install করা যায় (Android/iOS)
- Offline support (Service Worker)
- Mobile-optimized UI

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML5 + CSS3 + ES6 JS |
| Auth | Firebase Authentication (Google) |
| Database | Cloud Firestore (real-time) |
| Price API | CoinGecko Demo API |
| Offline | Service Worker (PWA) |
| Hosting | GitHub Pages |
| Fonts | Inter + DM Mono (Google Fonts) |

---

## 📁 File Structure

```
CryptoTrack/
├── index.html      ← পুরো অ্যাপ (HTML + CSS + JS)
├── manifest.json   ← PWA config
├── sw.js           ← Service Worker (offline)
└── icons/
    ├── icon-192.png
    └── icon-512.png
```

---

## ⚙️ Firebase Setup

**Firestore Rules:**
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /portfolios/{userId} {
      allow read, write: if request.auth != null
                         && request.auth.uid == userId;
    }
  }
}
```

---

## 📦 Version History

| Version | Changes |
|---------|---------|
| v4.0 | Glassmorphism UI redesign |
| v4.1 | Spot/Long/Short sections, Allocation toggle, 0-holdings hide |
| v4.2 | Leverage system, Edit Buy, Spot capital limit |
| v4.3 | Spot+Future Balance cards, Capital management, Edit Buy, Coin name truncate, 2 decimal format, Gradient avatar ring, Semi-round buttons, Allocation redesign, Real-time avg preview |

---

## 👤 Developer

**Morshedul Islam** — [morshed.github.io](https://morshed.github.io)
