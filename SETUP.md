# NoteSync — Setup Guide
*Snap a photo of your handwritten notes → structured Google Doc + Keep note, automatically.*

---

## What You'll Need
- A free GitHub account (for hosting)
- A Google AI Studio account (for Gemini — you already have this)
- Your existing Google account (for Docs/Drive/Keep)
- About 20–30 minutes for first-time setup

---

## Step 1: Create a GitHub Account

1. Go to **https://github.com** on your PC
2. Click **Sign up** — use your personal email
3. Choose the **Free** plan
4. Verify your email address

---

## Step 2: Upload the App to GitHub

1. On GitHub, click the **+** icon (top right) → **New repository**
2. Name it: `notesync` (all lowercase)
3. Set it to **Public**
4. Check **"Add a README file"**
5. Click **Create repository**

Now upload the files:
1. Click **Add file → Upload files**
2. Drag and drop all 4 files:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `SETUP.md` (this file)
3. Click **Commit changes**

---

## Step 3: Enable GitHub Pages (Free Hosting)

1. In your repository, click **Settings** (top tab)
2. Scroll down to **Pages** in the left sidebar
3. Under **Source**, select **Deploy from a branch**
4. Branch: **main** / Folder: **/ (root)**
5. Click **Save**
6. Wait 1–2 minutes, then your app URL will appear:
   `https://YOUR-USERNAME.github.io/notesync`

✅ Save that URL — that's your app address.

---

## Step 4: Get Your Gemini API Key

You already have a Google AI Pro plan, so this is quick:

1. Go to **https://aistudio.google.com/app/apikey**
2. Click **Create API key**
3. Select your existing Google project (or create a new one)
4. Copy the key — it starts with `AIza...`

Keep this key handy for the app settings.

---

## Step 5: Set Up Google OAuth (Docs + Drive + Keep Access)

This lets the app create Docs and send to Keep in your Google account.

### 5a. Create a Google Cloud Project
1. Go to **https://console.cloud.google.com/**
2. Click the project dropdown (top left) → **New Project**
3. Name it `NoteSync` → **Create**

### 5b. Enable Required APIs
1. In the left menu → **APIs & Services → Library**
2. Search and enable each of these:
   - **Google Docs API** → Enable
   - **Google Drive API** → Enable
   - **Gmail API** → Enable (used for Keep notes)

### 5c. Configure OAuth Consent Screen
1. Left menu → **APIs & Services → OAuth consent screen**
2. Choose **External** → **Create**
3. Fill in:
   - App name: `NoteSync`
   - User support email: your Gmail
   - Developer contact email: your Gmail
4. Click **Save and Continue** through all steps
5. On the **Test users** screen, click **Add Users** → add your own Gmail address
6. Click **Save and Continue** → **Back to Dashboard**

### 5d. Create OAuth Credentials
1. Left menu → **APIs & Services → Credentials**
2. Click **+ Create Credentials → OAuth client ID**
3. Application type: **Web application**
4. Name: `NoteSync PWA`
5. Under **Authorized JavaScript origins**, click **Add URI**:
   - `https://YOUR-USERNAME.github.io`
6. Under **Authorized redirect URIs**, click **Add URI**:
   - `https://YOUR-USERNAME.github.io/notesync/index.html`
7. Click **Create**
8. Copy the **Client ID** — it ends with `.apps.googleusercontent.com`

---

## Step 6: Configure the App

1. Open your app: `https://YOUR-USERNAME.github.io/notesync`
2. Tap the **⚙️ Settings** button (top right)
3. Enter:
   - **Gemini API Key**: paste from Step 4
   - **Google Client ID**: paste from Step 5d
   - **Drive Folder Name**: `Daily Notes` (or whatever you prefer)
4. Tap **Save Settings**
5. Tap **Connect Google Account** → sign in with your Google account → Allow
6. You'll be redirected back to the app with a ✓ confirmation

---

## Step 7: Install on Your S24 Ultra Home Screen

1. Open Chrome on your S24 Ultra
2. Navigate to `https://YOUR-USERNAME.github.io/notesync`
3. Tap the **⋮ menu** (three dots, top right)
4. Tap **Add to Home screen**
5. Name it `NoteSync` → **Add**

The app icon now lives on your home screen like any other app. Tap it and it opens full screen with no browser chrome.

---

## Daily Usage

1. **Tap the NoteSync icon** on your home screen
2. Tap **📸 Camera** to snap your notes, or **🖼️ Gallery** to pick an existing photo
3. Choose your output:
   - **📄 Docs Only** — full structured Google Doc
   - **📌 Keep Only** — action items summary card in Keep
   - **📄📌 Both** — Doc + Keep card
4. Tap **✨ Digitize Notes**
5. In ~10–15 seconds, tap the link to open your Doc or go to Keep

Your Docs are organized automatically in Google Drive:
```
Daily Notes/
  2026/
    March/
      📓 Daily Notes — Tuesday, March 24, 2026
    April/
      ...
```

---

## Troubleshooting

| Problem | Fix |
|---|---|
| "Add your Gemini API key" toast | Open Settings ⚙️, paste your Gemini key, Save |
| "Connect your Google account" toast | Open Settings ⚙️, tap Connect Google Account |
| Blank page on open | Wait 1–2 min after GitHub Pages deploy, hard refresh |
| OAuth error "redirect_uri_mismatch" | Double-check the redirect URI in Google Cloud Console matches your GitHub Pages URL exactly |
| Doc created but empty | Gemini couldn't read the image — try better lighting or a higher contrast photo |
| Keep note not appearing | Gmail → Keep delivery can take up to 2 minutes |

---

## Notes on Security

- Your Gemini API key and Google token are stored in your phone's local browser storage — they never leave your device or touch any third-party server
- The only external calls are directly to Google's APIs (Gemini, Docs, Drive, Gmail)
- This app is for personal use only — do not share your GitHub Pages URL publicly if you store your API key in the app

---

*Built with Gemini Vision + Google Docs API + Gmail API*
