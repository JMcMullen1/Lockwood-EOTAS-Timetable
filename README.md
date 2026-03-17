# Lockwood EOTAS Timetable

A live, visual timetable tool for Lockwood Education EOTAS students. Editors can add, edit, reorder and remove timetable blocks; everyone else sees a read-only view that updates in real time.

![Lockwood Education](https://i.postimg.cc/SN0MKjhP/Lockwood-EOTAS-logo.png)

---

## Features

- **Live sync** — changes appear instantly for all viewers (requires Firebase)
- **Editor login** — password-protected editing, read-only for everyone else
- **Block-based editing** — add, edit, reorder and delete colour-coded timetable blocks
- **13 colour-coded categories** — Science, Maths, English, IT, Music, Business, OT, SEMH, Lunch, Break, Travel, Private, Other
- **Responsive** — works on desktop, tablet and mobile
- **Today highlight** — the current day column is visually highlighted
- **Single HTML file** — no build step, no dependencies beyond Firebase CDN

---

## Quick Start (Local Demo)

1. Open `index.html` in a web browser
2. The timetable loads with the default schedule in **local mode** (changes saved in browser only)
3. Click **Editor Login** and enter the password (`lockwood2025` by default) to make changes

---

## Enabling Live Sync with Firebase

To make the timetable update live across all devices (so you can share a single link):

### 1. Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **Add project** and follow the steps
3. Once created, go to **Build → Realtime Database** and click **Create Database**
4. Choose a location and start in **test mode** (you'll secure it next)

### 2. Get Your Config

1. In Firebase Console, go to **Project Settings** (gear icon)
2. Scroll to **Your apps** → click the web icon (`</>`) to register a web app
3. Copy the `firebaseConfig` object

### 3. Add Config to the Timetable

Open `index.html` and replace the empty `FIREBASE_CONFIG` object (~line 480) with your config:

```javascript
const FIREBASE_CONFIG = {
    apiKey: "AIzaSy...",
    authDomain: "your-project.firebaseapp.com",
    databaseURL: "https://your-project-default-rtdb.firebaseio.com",
    projectId: "your-project",
    storageBucket: "your-project.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123"
};
```

### 4. Secure Your Database

In Firebase Console → Realtime Database → **Rules**, set:

```json
{
  "rules": {
    "timetable": {
      ".read": true,
      ".write": true
    }
  }
}
```

> For production, consider restricting `.write` to authenticated users.

### 5. Deploy

The simplest option is **GitHub Pages**:

1. Push this repo to GitHub
2. Go to **Settings → Pages** → set source to your branch / `root`
3. Share the generated URL — everyone with the link sees the live timetable

---

## Changing the Editor Password

In `index.html`, find this line (~line 485):

```javascript
const EDITOR_PASSWORD_HASH = "lockwood2025";
```

Change `"lockwood2025"` to your preferred password.

---

## Customisation

| What | Where |
|---|---|
| Editor password | `EDITOR_PASSWORD_HASH` in `index.html` |
| Firebase config | `FIREBASE_CONFIG` in `index.html` |
| Default timetable | `getDefaultTimetable()` function in `index.html` |
| Colours / theming | CSS custom properties at top of `<style>` |
| Categories | `CATEGORIES` array in `index.html` |

---

## Hosting Options

| Option | Live Sync | Cost |
|---|---|---|
| GitHub Pages + Firebase | Yes | Free |
| Netlify + Firebase | Yes | Free |
| Open HTML file locally | No (browser only) | Free |

---

## Licence

Built for Lockwood Education. All rights reserved.
