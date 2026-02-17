# 🎊 Jet & Jev Wedding Site — Deployment Guide

## Folder Structure
Upload ALL of these to your GitHub repo:

```
your-repo/
├── index.html
├── netlify.toml
├── package.json
├── data/
│   └── guests.json
├── css/
│   └── styles.css
├── js/
│   └── script.js
├── netlify/
│   └── functions/
│       └── rsvp.js
├── images/          ← copy from your original folder
│   ├── BGG.jpeg
│   ├── bg.jpg
│   ├── cam.png
│   ├── celeb.png
│   ├── hearts.png
│   ├── program.png
│   ├── rings.png
│   └── spag.png
└── song/            ← copy from your original folder
    └── blue (instrumental).mp3
```

---

## Step 1 — Enable Gmail App Password

> You MUST do this — Gmail blocks direct password use for apps.

1. Go to your Google Account → **Security**
2. Make sure **2-Step Verification** is ON
3. Search for **"App passwords"** → select it
4. Click **Generate** → choose "Mail" + "Other (custom name)" → type "Wedding RSVP"
5. **Copy the 16-character password** (e.g. `abcd efgh ijkl mnop`)
6. Keep it — you'll need it in Step 3

---

## Step 2 — Push to GitHub

1. Go to [github.com](https://github.com) → **New repository**
2. Name it `jet-and-jev-wedding` (or anything you like)
3. Upload all the files above (drag & drop or use Git)

---

## Step 3 — Deploy on Netlify + Set Environment Variables

1. Go to [netlify.com](https://netlify.com) → **Add new site** → **Import from Git**
2. Choose your GitHub repo → click **Deploy**
3. After deploy, go to: **Site settings → Environment variables → Add variable**

   Add these TWO variables:

   | Key | Value |
   |-----|-------|
   | `GMAIL_USER` | `mallows3124@gmail.com` |
   | `GMAIL_PASS` | *(the 16-char App Password from Step 1)* |

4. Go to **Deploys → Trigger deploy → Deploy site** to apply the variables

---

## Step 4 — Test It

1. Open your Netlify URL (e.g. `https://jet-and-jev.netlify.app`)
2. Click **RSVP Now** → it should scroll down
3. Click **Yes** → choose attendance → enter a name from the guest list + your email
4. Submit → you should receive:
   - ✅ An email at `mallows3124@gmail.com` with the RSVP details
   - ✅ A confirmation email to the guest with their table number
5. Try a name NOT on the list → they should get the polite capacity message

---

## How the Guest Name Matching Works

The system does a **loose match** — it doesn't need to be perfectly spelled:
- `"Jessa B"` will still match `"Jessa Bacani"`
- `"JOEY DEL ROSARIO"` will match `"Joey Del Rosario"` (case-insensitive)

---

## Later: Replace the Seating Chart Image

In `netlify/functions/rsvp.js`, find the line:
```
src="https://placehold.co/480x280/..."
```
Replace the URL with your actual seating chart image URL (upload it to your GitHub repo or any image host).

---

## Summary of Email Flows

| Scenario | Host Email | Guest Email |
|----------|-----------|-------------|
| Name on list, submits RSVP | ✅ Gets name, email, attendance type | ✅ Gets table number + event details |
| Name NOT on list | ⚠️ Gets name + "not on list" flag | 💙 Gets polite capacity message |
