# Jeopardy! Classroom Edition — Setup Guide

## File Structure

```
your-website/
├── jeopardy.html          ← The game (single file)
├── daily/
│   ├── TEMPLATE.csv       ← Copy this to make new games
│   ├── 2026-04-14.csv     ← Example daily game
│   ├── 2026-04-15.csv     ← Example daily game
│   ├── 2026-09-05.csv     ← Add as many as you want
│   └── ...
```

---

## How to Host

Upload the entire folder to any web host — the game just needs to be served over HTTP/HTTPS. 
It will **not** work as a local file (file://) for the Daily Game feature because browsers 
block local file fetching. The Custom Game mode works fine locally.

**Recommended free/cheap hosts:**
- **Netlify** (free) — drag and drop the folder at netlify.com
- **GitHub Pages** (free) — push to a repo, enable Pages in settings
- **Vercel** (free) — similar to Netlify
- Any shared hosting (GoDaddy, Bluehost, etc.) via FTP

---

## Daily Game System

### How it works
When a teacher selects "Daily Game" on the menu, the game fetches:
```
daily/YYYY-MM-DD.csv
```
where YYYY-MM-DD is today's date in their local timezone. If the file exists, 
it loads automatically. If not, it shows a friendly message saying which file to upload.

### Creating Daily Games (Bulk Method — Recommended)

1. Open **TEMPLATE.csv** in Excel
2. Fill in all your questions for one day
3. Go to File → Save As → choose **CSV (Comma delimited)**
4. Name the file with the date: `2026-09-05.csv`
5. Repeat for each day you want to pre-load
6. Upload all CSVs to the `/daily/` folder on your server

**Pro tip:** Open TEMPLATE.csv in Excel, fill it in for Monday, 
save as the Monday date, then fill in Tuesday's questions on top of Monday's, 
save as Tuesday's date, and so on. Fast batch creation.

### CSV Format Rules

```
--- ROUND 1 ---
,CAT1,CAT2,CAT3,CAT4,CAT5,CAT6
CATEGORY,Science,History,Math,Literature,Capitals,Pop Culture
$200 CLUE,clue1,clue2,clue3,clue4,clue5,clue6
$200 ANSWER,ans1,ans2,ans3,ans4,ans5,ans6
$400 CLUE,...
$400 ANSWER,...
$600 CLUE,...
$600 ANSWER,...
$800 CLUE,...
$800 ANSWER,...
$1000 CLUE,...
$1000 ANSWER,...

--- ROUND 2 ---
,CAT1,CAT2,CAT3,CAT4,CAT5,CAT6
CATEGORY,Geography,Chemistry,...
$400 CLUE,...
... (same pattern, values: 400/800/1200/1600/2000)

--- FINAL JEOPARDY ---
FINAL CATEGORY,Category Name Here
FINAL CLUE,The clue text goes here
FINAL ANSWER,What is the answer?
```

**Key rules:**
- Commas inside a clue are fine — Excel wraps them in quotes automatically
- Keep the section headers exactly as shown: `--- ROUND 1 ---`, `--- ROUND 2 ---`, `--- FINAL JEOPARDY ---`
- The CATEGORY row must come before the clue rows
- You can have 3–8 categories (default is 6)
- Values are fixed: Round 1 = 200/400/600/800/1000, Round 2 = 400/800/1200/1600/2000

---

## Ad Setup

Replace the placeholder `<!-- REPLACE -->` comments in jeopardy.html 
with your actual ad network embed codes.

| Slot | Location | Size | Notes |
|------|----------|------|-------|
| 1 | Setup screen top | 728×90 | Seen every session |
| 2 | Setup screen left rail | 160×600 | High CPM skyscraper |
| 3 | Setup screen right rail | 160×600 | High CPM skyscraper |
| 4 | Game screen bottom | 728×60 | **Best earner** — persistent all class |
| 5 | Winner screen | 728×90 | Captive end-of-game audience |
| 6 | Between-rounds interstitial | 480×260 | Full attention for 6 seconds |

**Recommended networks for teacher/education audiences:**
- Google AdSense (most common, easiest setup)
- Media.net (good for education content)
- Ezoic (higher RPM but requires approval)

---

## Custom Game Mode

Teachers can edit all questions directly in the browser via the 
**✏ Edit Questions** button. All changes save automatically to the 
browser's localStorage and persist across sessions.

To reset to the built-in default questions, click **↺ Reset** on the menu.

---

## Troubleshooting

**Daily Game says "Cannot load" when running locally:**
This is expected. Browsers block local file fetching. 
Host on any web server and it works immediately.

**Daily Game says file not found:**
Check that the filename exactly matches today's date in YYYY-MM-DD format 
and is in the `/daily/` folder. Example: `daily/2026-09-05.csv`

**CSV loads but shows wrong questions:**
Make sure you saved as CSV (not .xlsx) and that the section headers 
`--- ROUND 1 ---` etc. are on their own rows with no leading spaces.
