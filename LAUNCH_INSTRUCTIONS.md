# Holy Virgin Protection Church — Website Launch Instructions
## Rebuilt April 2026 | 16 Pages | Static HTML

---

## WHAT'S IN THIS FOLDER

All 16 pages of the new site plus supporting assets. Every file that needs
to be in the same folder on the web server is included here.

### HTML Pages (16)
| File | Page |
|------|------|
| index.html | Homepage |
| schedule.html | Service Schedule |
| directions.html | Driving Directions |
| bookstore1.html | Book & Gift Store |
| feast_day1.html | Church Feast Day |
| parishhistory.html | Parish History |
| photos.html | Photo Gallery |
| churchinterioandgrounds.html | Church Interior & Grounds (22 saints) |
| obituaries.html | Parishioner Obituaries |
| about_orthodoxy.html | About Orthodoxy (resource hub) |
| bylaws.html | ROCOR By-Laws / Ustav (bilingual) |
| application.html | Membership Application |
| administration.html | Administration / Staff |
| contact2.html | Contact Us |
| mailing1.html | Join Our Mailing List |
| donate.html | Donate |

### Asset Files (7)
| File | Used In |
|------|---------|
| icon.png | Nav logo on all pages |
| kursk-root-icon.jpg | administration.html |
| saint-dimitri-rostov.png | churchinterioandgrounds.html |
| saint-germogen.png | churchinterioandgrounds.html |
| saint-john-tobolsk.png | churchinterioandgrounds.html |
| saint-mitrofan-voronezh.png | churchinterioandgrounds.html |
| HVPC_Membership_Application.pdf | application.html |

---

## HOW TO GO LIVE

### Option A — Upload directly to your web server (recommended)
1. Log in to your hosting control panel (cPanel, Plesk, etc.)
2. Open the File Manager and navigate to your `public_html` folder
   (or whatever root folder your domain points to)
3. Upload ALL files in this folder — HTML pages AND all asset files —
   into the same directory. Do not put them in subfolders.
4. Make sure your old site's `index.html` (or `index.php`) is deleted or
   renamed first, so the new `index.html` takes over.
5. Visit your domain in a browser to confirm it's live.

### Option B — FTP
Use FileZilla or any FTP client. Upload all files to `public_html/` in one batch.

### Option C — WordPress host (All-in-One WP Migration)
If the current host runs WordPress, the cleanest move is to:
1. Point the domain to a new host (Bluehost, SiteGround, etc.)
2. Upload files there directly — no WordPress needed, this is pure static HTML.

---

## PUNCHLIST — FINISH BEFORE LAUNCH

Complete these tasks in order. Everything else is done.

---

### 1. SANITY CMS (Announcements on Homepage)
The homepage pulls live announcements from Sanity.io.

**Sanity project details:**
- Project ID: `rjehmfla`
- Dataset: `production`
- Studio URL: https://rjehmfla.sanity.studio

**Steps:**
1. Go to https://rjehmfla.sanity.studio
2. Create a new document type called `announcement` with these fields:
   - `title` (string)
   - `date` (date)
   - `body` (text)
   - `link` (url, optional)
   - `type` (string: "news" | "event" | "urgent")
   - `order` (number)
   - `active` (boolean)
3. Add a few announcements and mark `active: true`
4. Once the site is on the real domain, go to Sanity → Settings → API → CORS Origins
   and replace the current `*` wildcard with your actual domain (e.g. `https://www.holyvirginprotectionchurch.org`)

If Sanity is unreachable, the homepage falls back gracefully to hardcoded news items.

---

### 2. DONATE PAGE — Add Payment Links
File: `donate.html`

Search for these two comments in the file:
```
PUNCHLIST: Replace # below with the parish PayPal donation link
PUNCHLIST: Replace # below with the parish Cornerstone donation link
```

Replace both `href="#"` values with the actual donation URLs.

---

### 3. MEMBERSHIP APPLICATION PDF — Host on Server
File: `application.html`

Once the PDF is uploaded to the web server, update the download link.

Find this line in `application.html`:
```html
<a class="btn-download" href="HVPC_Membership_Application.pdf" ...>
```

If the PDF lives in the same folder as the HTML files, no change is needed.
If you host it elsewhere (e.g. Google Drive), replace with the full URL:
```html
href="https://www.holyvirginprotectionchurch.org/files/HVPC_Membership_Application.pdf"
```

---

### 4. GOOGLE CALENDAR (Events on Homepage)
The homepage has a placeholder section for the parish Google Calendar.

**Steps:**
1. Create a Google Calendar for the parish (or use an existing one)
2. In Google Calendar settings, make the calendar public
3. Go to Settings → Integrate Calendar → copy the "Embed code"
4. In `index.html`, find the comment:
   ```
   <!-- PUNCHLIST: Paste Google Calendar embed URL here -->
   ```
5. Replace the placeholder iframe src with your calendar's embed URL

---

### 5. CONSTANT CONTACT (Mailing List)
File: `mailing1.html`

**Steps:**
1. Log in to Constant Contact and get your signup form embed code
2. In `mailing1.html`, find the placeholder div:
   ```html
   <!-- PUNCHLIST: Paste Constant Contact embed code here -->
   ```
3. Replace it with the embed code from Constant Contact

---

### 6. GOOGLE PHOTOS (Photo Gallery)
File: `photos.html`

The gallery has 4 album tabs with placeholder embed areas:
- Church & Grounds
- Feast Days
- Parish Life
- Historical

**Steps:**
1. Create a Google Photos account for the parish
2. Create one shared album per tab
3. For each album: open it → Share → Create link → copy the share URL
4. In `photos.html`, find the 4 placeholder comments and paste each album URL

---

### 7. ST. ALEXIS & ST. TIKHON ICONS
File: `churchinterioandgrounds.html`

Two of the six Russian Clerical Saints (Alexis of Moscow and Tikhon of Zadonsk)
use image URLs from the existing server's `/images/iconfrescoes/` directory.
These should load automatically once the existing content is preserved.

If they appear broken after launch, right-click the images on the OLD site
at `holyvirginprotectionchurch.org/churchinterioandgrounds.html`, copy their
image addresses, and paste those URLs into the two `src=""` attributes in the file.
Search for `alexismetofmoscow` and `tikhonzadonsk` to find them.

---

### 8. EMBED ICON.PNG AS BASE64 (Optional but recommended)
Currently all pages reference `icon.png` as an external file.
If you want the nav logo to work even if the asset file gets separated,
you can embed it as a base64 data URI.

Run this Python snippet on your computer (requires Python 3):
```python
import base64
with open('icon.png', 'rb') as f:
    data = base64.b64encode(f.read()).decode()
print(f"data:image/png;base64,{data}")
```

Then find-and-replace `src="icon.png"` with `src="data:image/png;base64,[output]"`
across all 16 HTML files. A code editor like VS Code can do this in one step
with Find in Files (Ctrl+Shift+H).

---

### 9. HISTORICAL PHOTOS (Parish History page)
File: `parishhistory.html`

There are 2 placeholder slots in the photo strip at the top of the page.
Source pre-1980 photos of the parish and upload them to the server,
then update the `src` attributes in the photo strip section.

---

## CONTACT INFORMATION REFERENCE
*(already built into all pages — for your records)*

| | |
|---|---|
| Church Address | 38 South Mill Street, Nyack, NY 10960 |
| Church Phone | 845-353-1155 |
| Rector Office | 845-618-5308 |
| Fax | 845-497-7963 |
| Rector | V. Rev. Elias Gorsky — frilya@egcon.com |
| Bookstore | Irina Gorsky — 914-414-0052 / mairag050@gmail.com |
| Hall Rental | Maxime Kudinoff — 845-358-0190 / ksunusha@aol.com |
| Hall Address | 51 Prospect Street, Nyack, NY 10960 |
| YouTube | youtube.com/channel/UCAd-5xu1S1rHwHoadO2LSAQ |
| Candle Orders | form.jotform.com/202454512119144 |

---

## TECH NOTES FOR DEVELOPERS

- **Zero dependencies.** Pure HTML/CSS/JS. No build step, no npm, no framework.
- **Google Fonts** are loaded via CDN (IM Fell English + Lato). Requires internet.
- **Sanity CMS** is wired into the homepage announcements section via their CDN API.
  Token is embedded in index.html — rotate it if the site is ever compromised.
- **All product/saint images** in bookstore1.html and churchinterioandgrounds.html
  are embedded as base64 data URIs — those images have zero external dependencies.
- **Other images** (clergy photos, church exterior, icon frescoes) are hotlinked
  from the existing holyvirginprotectionchurch.org server. After domain cutover,
  these will need to be downloaded and re-hosted, or the URLs updated.
- **No cookies, no tracking, no analytics** are currently included.
  Add Google Analytics by pasting the GA4 tag into the `<head>` of index.html
  and propagating to the other pages.

---

*Built with Claude — April 2026*
*Holy Virgin Protection Russian Orthodox Church, Nyack, NY*
