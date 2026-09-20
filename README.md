# Kifayati (किफ़ायती) 🏷️
### Real-Time Multi-Store Price Surfing & Comparison Engine

**Kifayati** is an automated, real-time price comparison engine tailored for top Indian e-commerce platforms. Simply paste any product URL or search query, and Kifayati concurrently surfs live storefronts to identify the best price, verify availability, and link you directly to the lowest seller.

---

## ✨ Key Features

- **⚡ Real-Time Live Surfing**: Fetches live HTML and public storefront APIs directly—no stale static databases or synthetic mock data.
- **🛡️ Live Verification Badges**: Every deal displays a verification badge, timestamp, and direct outbound link to purchase at the verified price.
- **🚀 Zero Dependencies**: Built completely using Python's standard library (`http.server`, `urllib`, `sqlite3`, `concurrent.futures`). No `pip install` required!
- **🌐 Wide Storefront Coverage**:
  - **E-Commerce & Electronics**: Amazon India, Flipkart, JioMart, Croma, Reliance Digital
  - **Fashion & Lifestyle**: Myntra, Ajio
  - **Quick Commerce & Grocery**: Blinkit, Zepto, BigBasket
- **🧠 Exact Model & ASIN Extraction**: Parses product codes, color variants, storage configurations, and title tokens to prevent mismatched comparisons.
- **💾 Smart Local Caching**: SQLite database with configurable 15-minute TTL to ensure fast lookups without overloading storefront servers.
- **🎨 Modern Glassmorphism UI**: High-contrast, responsive interface with instant search suggestions, price history, and direct store redirection.

---

## 📸 How It Works

```
                          ┌───────────────────────────┐
                          │   User Query / Item URL   │
                          └─────────────┬─────────────┘
                                        │
                                        ▼
                          ┌───────────────────────────┐
                          │  URL & Title Parser       │
                          │  (ASIN, Clean Brand/Model)│
                          └─────────────┬─────────────┘
                                        │
                 ┌──────────────────────┼──────────────────────┐
                 ▼                      ▼                      ▼
        ┌────────────────┐     ┌────────────────┐     ┌────────────────┐
        │ Amazon Surfer  │     │ Flipkart Surfer│     │  Croma Surfer  │ ...
        └────────┬───────┘     └────────┬───────┘     └────────┬───────┘
                 │                      │                      │
                 └──────────────────────┼──────────────────────┘
                                        │
                                        ▼
                          ┌───────────────────────────┐
                          │  Price Normalizer & Ranker│
                          │  (Identifies Lowest Deal) │
                          └─────────────┬─────────────┘
                                        │
                                        ▼
                          ┌───────────────────────────┐
                          │ Live Verified Deal Matrix │
                          └───────────────────────────┘
```

---

## 🚀 Quickstart

### Prerequisites
- Node.js 20 or higher installed.

### Standard Command Line
```bash
npm install
npm run dev
```

Then navigate to:
```
http://localhost:3000
```

---

## 🔌 API Endpoints

### 1. Compare Prices
`GET /api/compare?url=<product_url_or_query>`

**Response Format:**
```json
{
  "query": "Safari Laptop Backpack",
  "product": {
    "title": "Safari Laptop Backpack with Raincover",
    "brand": "Safari",
    "category": "luggage"
  },
  "best_deal": {
    "retailer": "Amazon",
    "price": 709,
    "currency": "INR",
    "url": "https://www.amazon.in/dp/B097JJ2CK6",
    "verified_at": "2026-09-19T14:50:00Z"
  },
  "stores": [
    {
      "retailer": "Amazon",
      "price": 709,
      "original_price": 2899,
      "discount_percent": 75,
      "in_stock": true,
      "verified": true,
      "url": "https://www.amazon.in/dp/B097JJ2CK6"
    },
    {
      "retailer": "Flipkart",
      "price": 749,
      "original_price": 2899,
      "discount_percent": 74,
      "in_stock": true,
      "verified": true,
      "url": "https://www.flipkart.com/..."
    }
  ]
}
```

### 2. Supported Retailers
`GET /api/stores`

### 3. Server Health
`GET /api/health`

---

## 📁 Project Structure

```
Kifayati/
├── index.html           # Single-page modern glassmorphism frontend
├── server.py            # Real-time multi-store scraping & comparison server
├── start-kifayati.ps1   # PowerShell automated runner & port binder
├── .gitignore           # Ignores database, pycache, and logs
└── README.md            # Documentation & setup guide
```

---

## ⚖️ Disclaimer

Kifayati is designed for personal shopping assistance and educational purposes. Prices, stock status, and deal terms are subject to change by respective e-commerce retailers. Always review product specifications and final prices on the seller's storefront prior to making any purchase.
