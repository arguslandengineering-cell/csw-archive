# ArgusLand CSW System

**Completed Staff Work Management PWA**  
Planning & Engineering Department — ArgusLand, Inc.  
Damilag, Manolo Fortich, Bukidnon, Philippines

---

## What This System Does

| Feature | Description |
|---|---|
| **Prompt Generator** | Staff fills a structured form → app builds a ready AI prompt → copy-paste into Claude or any AI to get a full formal CSW draft |
| **CSW Directory** | All approved CSWs stored on GitHub, searchable by keyword, type, site, department |
| **Duplicate Check** | Warns if a similar CSW already exists before staff creates a new one |
| **Upload Archive** | Upload signed PDF or JPEG of approved CSW directly from phone to GitHub |
| **Dashboard** | Tracks approval rate, average duration, stale items, breakdown by type and site |
| **Email Alerts** | You receive an email every time a new CSW is uploaded to the archive |
| **Offline Support** | App works without internet — drafts and searches cached data locally |
| **Installable APK** | Can be installed on any Android phone, no Play Store needed |

---

## File Structure

```
csw-archive/              ← your GitHub repository
├── index.html            ← main PWA app
├── manifest.json         ← PWA install config
├── sw.js                 ← offline service worker
├── csw-index.json        ← auto-generated directory index (do not edit manually)
├── icons/
│   ├── icon-192.png
│   └── icon-512.png
├── csw-files/            ← all uploaded PDF/JPEG files go here (auto-created)
│   ├── CSW-2026-001_....pdf
│   └── CSW-2026-002_....jpg
└── .github/
    └── workflows/
        └── notify.yml    ← email notification automation
```

---

## SETUP GUIDE (Do This Once)

### Step 1 — Create GitHub Repository

1. Go to **github.com** → sign in
2. Click **+** → **New repository**
3. Name it: `csw-archive`
4. Set to **Public**
5. Check **"Add a README file"**
6. Click **Create repository**

### Step 2 — Enable GitHub Pages

1. In your repo → **Settings** → **Pages**
2. Branch: **main** → folder: **/ (root)**
3. Click **Save**
4. Wait 2 minutes
5. Your app URL will be: `https://YOUR-USERNAME.github.io/csw-archive`

### Step 3 — Upload All Files

Upload these files to your repo root via **"Add file → Upload files"**:

```
index.html
manifest.json
sw.js
```

For icons, create the folder first:
1. **"Add file → Create new file"** → name it `icons/placeholder.txt` → commit
2. Then **"Add file → Upload files"** → upload both PNG files into the `icons/` folder

### Step 4 — Create GitHub Personal Access Token

This allows the app to upload files directly from your phone to GitHub.

1. GitHub → top-right avatar → **Settings**
2. Left sidebar → **Developer settings**
3. **Personal access tokens → Tokens (classic)**
4. Click **Generate new token (classic)**
5. Note: `ArgusLand CSW Upload`
6. Expiration: **No expiration** (or 1 year)
7. Check scope: ✅ **repo** (full repo access)
8. Click **Generate token**
9. **Copy the token immediately** — you cannot see it again
10. It looks like: `ghp_xxxxxxxxxxxxxxxxxxxx`

### Step 5 — Set Up Email Notifications (GitHub Actions)

1. Go to your repo → **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Add these two secrets:

| Secret Name | Value |
|---|---|
| `MAIL_USERNAME` | `arguslandengineering@gmail.com` |
| `MAIL_PASSWORD` | Gmail App Password (see below) |

**Getting Gmail App Password:**
1. Go to **myaccount.google.com**
2. Security → **2-Step Verification** (enable if not yet)
3. Security → **App passwords**
4. Select app: **Mail** → Select device: **Other** → type `GitHub CSW`
5. Copy the 16-character password
6. Use this as `MAIL_PASSWORD` secret

### Step 6 — Configure the App

1. Open your app URL in Chrome on your phone
2. Go to **⚙️ Config tab**
3. Fill in:
   - **GitHub Username**: your GitHub username
   - **Repository Name**: `csw-archive`
   - **Personal Access Token**: paste the token from Step 4
   - **Notification Email**: `arguslandengineering@gmail.com`
4. Click **Save Configuration**
5. Fill in your name under **My Profile**
6. Fill in **Signatories** (reviewed by, noted by, approved by)
7. Click **Save** on each section

### Step 7 — Install on Phone (PWA)

**Android Chrome:**
1. Open the app URL
2. Tap **⋮ menu** (3 dots top right)
3. Tap **"Add to Home screen"**
4. App installs with CSW icon — no Play Store needed

**iPhone Safari:**
1. Open the app URL
2. Tap **Share button** (box with arrow)
3. Tap **"Add to Home Screen"**

### Step 8 — Convert to APK (Optional, for sharing)

1. Go to **pwabuilder.com**
2. Paste your GitHub Pages URL
3. Click **Package for stores → Android**
4. Download the `.apk` file
5. Send via WhatsApp or Telegram to any team member
6. On their phone: Settings → **Install unknown apps** → Allow → Install

---

## HOW TO USE — Daily Operations

### Creating a New CSW

1. Open app → **✏️ New CSW tab**
2. Select **CSW Type** (Field Issue / Policy-System / Inter-Department)
3. Fill in Title — app automatically checks for duplicates
4. Fill in Site, Department, Situation, Impact, Recommendation
5. Tap **✨ Generate AI Prompt**
6. Tap **📋 Copy Prompt**
7. Open Claude.ai or any AI → paste → get your CSW draft
8. **Review the draft** — correct any errors
9. Print and route for signatures
10. Tap **💾 Save Draft** to log it in the directory while pending approval

### Uploading an Approved CSW

1. Get the physical signed CSW scanned as **PDF or JPEG**
2. Open app → **📤 Upload tab**
3. Fill: CSW Number, Title, Type, Site, Date Approved, Status
4. Tap **📄 Tap to select PDF or JPEG** → choose your file
5. Tap **📤 Upload to ArgusLand Archive**
6. Done — file is permanently stored in GitHub
7. You will receive an email notification automatically

### Searching the Directory

1. Open app → **🔍 Search tab**
2. Type any keyword — title, site, department, CSW number
3. Filter by Status or Type
4. Tap any result to view full details
5. Tap **📄 Open / Reprint Signed CSW** to open the original file

### Checking the Dashboard

1. Open app → **📊 Dashboard tab**
2. See: total CSWs, pending count, approval rate, average approval duration
3. Check **⚠️ Stale** section — any CSW with no update for 7+ days is flagged
4. Check **By Type** and **By Site** bar charts for pattern analysis

### Syncing on a New Phone

1. Install the app
2. Go to **⚙️ Config tab**
3. Enter GitHub username, repo name, token
4. Tap **🔄 Sync from GitHub**
5. Full directory loads instantly

---

## CSW TYPES — When to Use What

| Type | Use When |
|---|---|
| **Field Issue** | One-time problem at a site — encroachment, discrepancy, wrong orientation, damage, safety concern |
| **Policy/System** | Proposing a new standing rule — once approved, cite this CSW number for all future recurrences instead of making a new one |
| **Inter-Department** | One department needs specific action from another — Finance to release funds, Admin to issue memo, Sales to stop a practice |

**Key Rule:** A Policy/System CSW, once approved by the President, becomes a **perpetual ruling**. Staff apply it by citing the CSW number — no need to write a new one for the same situation.

---

## SIGNATORY CHAIN

| Role | Position | Action |
|---|---|---|
| Prepared By | Any staff | Fills form, generates prompt, produces draft |
| Reviewed By | Engineers | Checks technical accuracy |
| Noted By | Technical Head (Charles) | Validates completeness and recommendation |
| Approved By | President | Final authority — signature makes it official |

---

## EMAIL NOTIFICATION TRIGGERS

| Event | Email Sent |
|---|---|
| New PDF/JPEG uploaded to archive | ✅ Yes — automatic via GitHub Actions |
| New draft saved (prompt generated) | ❌ No — drafts are local only until uploaded |
| Status changed to Approved | ✅ Yes — triggers on file commit |

---

## TROUBLESHOOTING

| Problem | Fix |
|---|---|
| Upload fails | Check Config tab — token, username, repo name must be exact |
| Token expired | Generate new token in GitHub → update Config tab |
| No email received | Check GitHub Actions tab in repo for errors, verify MAIL_PASSWORD secret |
| App not loading offline | Open once on WiFi first to cache assets, then works offline |
| Sync fails | Check internet connection, verify repo is public |
| Duplicate warning on every entry | Expected behavior — just verify it's truly new before proceeding |

---

## SUSTAINABILITY NOTES

- **No subscriptions, no billing** — GitHub Free tier, no APIs that charge per call
- **No backend server** — app runs entirely on the phone + GitHub storage
- **No login fatigue** — token is stored once, no repeated sign-ins
- **Offline-first** — field staff can draft prompts in dead zones, upload when back on signal
- **Token rotation** — recommended every 12 months for security, takes 5 minutes

---

*ArgusLand Planning & Engineering Department*  
*CSW System v1.0*
