# ROBOCHIPX 2026

A premium 24-hour intercollege Robotics and VLSI Innovation Challenge hosted at Rajalakshmi Institute of Technology, Chennai. Vanilla HTML, CSS, and JavaScript — no frameworks, no build tools.

---

## Folder Structure

```
project-root/
├── public/
│   ├── index.html          # Main landing page
│   ├── registration.html   # Team registration form
│   ├── payment.html        # Payment instructions page
│   └── assets/             # Static assets (images, icons, etc.)
│
├── src/
│   ├── js/
│   │   ├── app.js              # All client-side logic (starfield, countdown, registration)
│   │   ├── firebase-config.js  # Firebase app initialisation & Firestore export
│   │   └── mailer.js           # Reference stub (email handled server-side)
│   │
│   ├── css/
│   │   └── styles.css          # Full stylesheet
│   │
│   └── config/                 # Reserved for future config files
│
├── firebase/
│   ├── firestore.rules         # Firestore security rules
│   └── firestore.indexes.json  # Firestore field-level indexes
│
├── scripts/
│   └── google-apps-script.gs  # Google Apps Script (Sheets + confirmation email)
│
├── .gitignore
├── README.md
├── LICENSE
└── vercel.json                 # Vercel routing + JS Content-Type headers
```

---

## Deployment to Vercel

1. Push this repository to GitHub (or GitLab / Bitbucket).
2. Go to [vercel.com](https://vercel.com) → **Add New Project** → import your repo.
3. Leave **Framework Preset** as **Other** (no build step required).
4. Leave **Build Command** and **Output Directory** blank.
5. Click **Deploy**.

Vercel uses `vercel.json` to route `/` → `public/index.html`, `/registration` → `public/registration.html`, and `/payment` → `public/payment.html`.

---

## Firebase Setup

1. Create a project at [console.firebase.google.com](https://console.firebase.google.com).
2. Enable **Firestore Database** in production mode.
3. Replace the config values in `src/js/firebase-config.js` with your project's credentials.
4. Deploy Firestore rules:
   ```
   firebase deploy --only firestore:rules,firestore:indexes
   ```
   Or paste the contents of `firebase/firestore.rules` directly in the Firebase console under **Firestore → Rules**.

---

## Google Apps Script Setup

1. Open your Google Sheet (create one if needed, name the tab **Registrations**).
2. Go to **Extensions → Apps Script**.
3. Paste the contents of `scripts/google-apps-script.gs`.
4. Update `PAYMENT_URL` at the top to your Vercel deployment URL.
5. Click **Deploy → New deployment**:
   - Type: **Web App**
   - Execute as: **Me**
   - Who has access: **Anyone**
6. Copy the **Web App URL** and replace the `fetch()` endpoint inside `initRegistration()` in `src/js/app.js`.

---

## Path Changes Made

| File | Old path | New path |
|---|---|---|
| `index.html` | `robochipX/index.html` | `public/index.html` |
| `registration.html` | `robochipX/registration.html` | `public/registration.html` |
| `payment.html` | `robochipX/payment.html` | `public/payment.html` |
| `styles.css` | `robochipX/styles.css` | `src/css/styles.css` |
| `app.js` | `robochipX/app.js` | `src/js/app.js` |
| `firebase-config.js` | `robochipX/firebase-config.js` | `src/js/firebase-config.js` |
| `mailer.js` | `robochipX/mailer.js` | `src/js/mailer.js` |
| `firestore.rules` | `robochipX/firestore.rules` | `firebase/firestore.rules` |
| `firestore.indexes.json` | `robochipX/firestore.indexes.json` | `firebase/firestore.indexes.json` |
| `google-apps-script.gs` | `robochipX/google-apps-script.gs` | `scripts/google-apps-script.gs` |

HTML files reference CSS as `../src/css/styles.css` and JS as `../src/js/app.js`.  
`app.js` imports `firebase-config.js` as `./firebase-config.js` (same directory).
