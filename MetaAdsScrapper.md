# Meta Ads Scraper — Chrome Extension Module
**Purpose:** Core logic for scraping, storing, and displaying ads from the **Facebook Ads Library** within the Chrome extension.

---

## ✨ Core Features

- **Store-Specific Scraping**
  - Select a store from dropdown and fetch all ads tied to its domain.
  - Normalizes store URLs and manages previously scraped data.

- **IndexedDB Integration**
  - Stores ads persistently in `metaAdsDB` → `metaAdsStore`.
  - Supports insert, retrieval, and deletion of ads per store.
  - Debug function for reviewing all stored data.

- **Smart Scraping Workflow**
  - Opens a dedicated Chrome popup window and loads the **Facebook Ads Library**.
  - Auto-scrolls page with stop detection and “See more” button handling.
  - Extracts ads with rich details (status, libraryId, date ranges, platforms, advertiser info, text, hashtags, media).

- **Graceful Stop & Save**
  - On clicking **Stop**, halts scrolling, extracts visible ads, saves partial results, and closes scraping window.

- **UI Rendering**
  - Renders results into ad cards with:
    - Media (images/videos)
    - Advertiser info & profile image
    - Status (Active/Inactive)
    - Dates, platforms, hashtags, buttons
    - Link to the original Ad Library entry
  - Pagination with adjustable rows per page.
  - Notices for previously scraped or empty results.

---

## 🛠️ Data Model

Each ad object stored includes:

- `libraryId` — Unique ad ID (used as primary key in DB).
- `advertiserName` / `advertiserUrl` — Brand/page running the ad.
- `profileImgSrc` — Advertiser profile image.
- `status` — Active / Inactive.
- `startDate`, `endDate`, `activeTime` — Duration metadata.
- `platforms`, `platformCount` — Platforms where ad ran.
- `adText` — Extracted textual content.
- `mediaType`, `mediaSrc`, `isVideo` — Creative details.
- `buttons` — CTA buttons found.
- `hashtags` — Hashtags in content.
- `adLink` — Direct link to Ad Library entry.
- `store`, `storeUrl` — Store context.
- `country` — Currently set to `ALL`.
- `timestamp` — Time of scrape.

---

## 🚀 Workflow

1. **Select Store**  
   Dropdown triggers store name & URL normalization.  
   Loads previously stored ads if available.

2. **Start Scraping**  
   - Opens popup window.  
   - Navigates to Ads Library.  
   - Auto-scrolls to load ads.  
   - Extracts structured ad data.

3. **Stop Scraping**  
   - Saves current visible ads.  
   - Updates IndexedDB and UI.  
   - Closes popup gracefully.

4. **Results Display**  
   - Cards shown in grid with pagination.  
   - Rich metadata and quick link to original Ad.  
   - Expanded view (commented code ready for future).

---

## 🧭 Key Functions

- `initDB()` — Initialize IndexedDB.  
- `storeAdsData(adsData)` — Save ads to DB.  
- `getAdsByStore(storeUrl)` — Retrieve ads by store.  
- `deleteAdsByStore(storeUrl)` — Delete all ads of a store.  
- `debugAllStoredData()` — Debug stored ads grouped by store.  
- `openScrapingWindow()` — Opens Chrome popup and starts scraping.  
- `stopScraping()` — Gracefully stops scraping, saves data.  
- `scrapeStoreAds(tabId)` — Core scraper injecting DOM logic.  
- `autoScroll(tabId)` — Controlled infinite scroll with stop flag.  
- `updateResults()` — Paginate and render ad cards.  
- `createAdCard(ad)` — UI builder for ad card.

---

## 📌 Notes & Improvements

- Current version uses **Facebook Ads Library** DOM classes — these may change, requiring updates.  
- Expanded card UI is scaffolded but commented out.  
- Supports only **keyword + store** scraping for now — extendable to more filters.  
- `getLast3MonthsRange()` ensures scraping window is limited to recent 3 months.

---

## 📜 Copyright

© 2024 **Meta Ads Scraper** (part of Mergeline Business Analyzer).  
For research, analytics, and professional lead-generation use only.  
