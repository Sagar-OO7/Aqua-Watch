# 💧 AquaWatch — Smart Water Tank Monitor

A real-time IoT dashboard for monitoring water tank levels, turbidity, and pump control — built with Firebase Realtime Database, Arduino, and deployed on Vercel.

![AquaWatch Dashboard](https://img.shields.io/badge/status-live-00d4ff?style=for-the-badge)
![Firebase](https://img.shields.io/badge/Firebase-RTDB-orange?style=for-the-badge&logo=firebase)
![Vercel](https://img.shields.io/badge/Deployed-Vercel-black?style=for-the-badge&logo=vercel)

---

## 🚀 Features

- **Live water level** — animated SVG tank with wave effect
- **Turbidity monitoring** — NTU index with color-coded clarity status
- **Motor/pump control** — ON/OFF commands sent via Firebase → Arduino
- **Sparkline charts** — scrolling history for both sensors
- **Activity log** — timestamped event stream
- **PWA ready** — installable on mobile as an app
- **Particle background** — animated network of glowing dots

---

## 🗂 Project Structure

```
aquawatch/
├── index.html       ← Main dashboard (all HTML + CSS + JS)
├── manifest.json    ← PWA manifest
├── vercel.json      ← Vercel deployment config
├── robots.txt       ← SEO robots file
├── .gitignore
└── README.md
```

---

## ⚙️ Hardware Setup

| Component | Details |
|---|---|
| Microcontroller | Arduino Uno / Nano |
| Water Level Sensor | Ultrasonic / Float sensor |
| Turbidity Sensor | Analog (A0) |
| Motor Relay | Digital Pin 7 |
| Serial | COM9, 9600 baud |

**Arduino sends** comma-separated data every 1 second:
```
water_level,turbidity,motor_status
50,300,OFF
```

**`upload.py`** runs on your PC, reads serial, syncs to Firebase, and sends motor commands back.

---

## 🔥 Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Create a project → Enable **Realtime Database**
3. Set rules to allow read/write (for development):
```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```
4. Your config is already baked into `index.html`

**Database structure:**
```
/tank
  water_level: "50"
  turbidity: "300"
  status: "OFF"

/motor_control: "OFF"
```

---

## 🐍 Running the Python Bridge

```bash
pip install pyserial firebase-admin
python upload.py
```

Make sure `aquawatch.json` (Firebase service account key) is in the same folder.

---

## 📦 Deploy to Vercel (Step by Step)

### 1. Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit — AquaWatch dashboard"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/aquawatch.git
git push -u origin main
```

### 2. Connect to Vercel

1. Go to [vercel.com](https://vercel.com) → **Add New Project**
2. Import your GitHub repo `aquawatch`
3. Framework preset: **Other** (static site)
4. Root directory: `/` (leave as default)
5. Click **Deploy** ✅

Vercel auto-detects `vercel.json` and deploys it as a static site.

### 3. Your live URL

```
https://aquawatch.vercel.app
```

Every `git push` to `main` will auto-redeploy. 🎉

---

## 📱 Install as Mobile App (PWA)

On your phone browser, open the live URL → tap **"Add to Home Screen"** → AquaWatch installs as a native-looking app with the cyan water drop icon.

---

## 🛠 Tech Stack

| Layer | Tech |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JS |
| Database | Firebase Realtime DB |
| Hardware | Arduino + Python (pyserial) |
| Hosting | Vercel (static) |
| Fonts | Google Fonts (Orbitron + Rajdhani) |

---

## 📄 License

MIT — free to use and modify.
