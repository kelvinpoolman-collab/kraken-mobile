# 🐙 Kraken Terminal Mobile

Mobile companion app voor Kraken Bot v5 — gebouwd met Capacitor, automatisch gebouwd via GitHub Actions.

## 📱 Wat is dit?

Een Android app die verbinding maakt met je Kraken Bot dashboard op je PC. De bot draait gewoon op je PC (zoals nu), maar je kunt vanaf je telefoon overal ter wereld:

- 📊 Live posities bekijken
- 💰 Win rate, P&L, expectancy zien
- 📈 Performance chart in real-time
- 🛑 Posities sluiten (handmatig)
- ⏸️ Bot pauzeren/resumeren
- 📜 Trades + activity feed
- 🔔 Telegram notifications (al actief)

## 🏗️ Architectuur

```
📱 Android App (Capacitor)
         ↕  HTTPS
🌐 Tailscale VPN (gratis, versleuteld)
         ↕
💻 PC (Windows) — bot + dashboard:5000
```

## 🚀 Setup vanaf 0 (eenmalig, ~30 min)

### Stap 1: GitHub account aanmaken

1. Ga naar https://github.com/signup
2. Maak gratis account
3. Verifieer email

### Stap 2: Code naar GitHub uploaden

**Optie A: Via website (makkelijkst)**

1. Klik op "+" rechtsbovenin → "New repository"
2. Naam: `kraken-mobile` (of wat je wilt)
3. **Privacy: Public** (anders geen gratis Actions minutes)
4. NIET aanvinken: "Add README", "Add .gitignore" (we hebben al)
5. Klik "Create repository"
6. Op de empty repo pagina: klik "uploading an existing file"
7. Sleep alle bestanden uit deze zip naar de browser
8. Commit message: "Initial mobile app"
9. Klik "Commit changes"

**Optie B: Via Git (als je Git kent)**

```bash
cd kraken-mobile
git init
git add .
git commit -m "Initial mobile app"
git branch -M main
git remote add origin https://github.com/JOUW-USERNAME/kraken-mobile.git
git push -u origin main
```

### Stap 3: GitHub Actions activeren

1. Ga naar je nieuwe repo
2. Klik tab "Actions"
3. Klik "I understand my workflows, go ahead and enable them"
4. De build start automatisch! ⚡

### Stap 4: Wachten op build (~5 min)

1. Klik op de lopende workflow
2. Wacht tot alle stappen groen ✓ zijn
3. Bij errors: zie troubleshooting onderaan

### Stap 5: APK downloaden

1. Ga naar tab "Releases" (rechtsboven, of /releases)
2. Klik op de nieuwste release "v1"
3. Download `KrakenTerminal-v1.0.apk`
4. Stuur naar je telefoon (email/WhatsApp/Drive)

## 📲 Installatie op telefoon

### Stap 1: APK installeren

1. Open de APK op je Android
2. "Install from unknown sources" → toestaan
3. Tap "Install"
4. App verschijnt in app drawer

### Stap 2: Tailscale setup

**Op PC (Windows):**

1. Download Tailscale: https://tailscale.com/download/windows
2. Installeer + log in (Google/Microsoft account)
3. Open `cmd`: `tailscale ip` → noteer het IP (bv `100.64.0.1`)
4. Tailscale draait nu in achtergrond

**Op telefoon:**

1. Play Store → installeer "Tailscale"
2. Log in met zelfde account
3. Verbinding actief

### Stap 3: Bot toegankelijk maken

Op je PC, edit `dashboard_api.py` regel ~9XX (waar Flask runt):

```python
# Verander van:
app.run(host="127.0.0.1", port=5000)

# Naar:
app.run(host="0.0.0.0", port=5000)
```

Restart bot: `start.bat`

### Stap 4: App configureren

1. Open Kraken Terminal app
2. Eerste keer vraagt voor API URL
3. Voer in: `http://100.64.0.1:5000` (jouw Tailscale IP!)
4. App verbindt + toont je posities ✨

## 🔄 Updates

Wanneer je iets wilt veranderen:

1. Edit bestanden lokaal
2. Push naar GitHub
3. Actions bouwt automatisch nieuwe APK
4. Download nieuwe APK + installeer over oude

## 🎨 App icoon aanpassen

Edit `resources/icon.svg` of vervang met PNG (1024x1024). Volgende push genereert automatisch alle Android resoluties.

## 🛠️ Troubleshooting

### Build fail: "Gradle error"

→ Check Actions log. Meestal Java/SDK versie probleem. Issue openen.

### App connect fails

→ Check:
- Bot draait op PC (`tasklist | findstr python`)
- Dashboard luistert op 0.0.0.0 (niet 127.0.0.1)
- Tailscale verbonden op beide devices
- Windows Firewall: `netsh advfirewall firewall add rule name="Kraken Dashboard" dir=in action=allow protocol=TCP localport=5000`

### App icon werkt niet

→ Check `android/app/src/main/res/` na sync. Run `npx cap sync android` lokaal als je ontwikkelt.

## 📁 Project structuur

```
kraken-mobile/
├── src/
│   └── index.html              ← Mobile-optimized UI
├── resources/
│   ├── icon.svg                ← App icon (1024x1024)
│   └── splash.svg              ← Splash screen
├── .github/workflows/
│   └── build-apk.yml           ← GitHub Actions cloud build
├── capacitor.config.json       ← Capacitor configuratie
├── package.json                ← npm dependencies
└── README.md                   ← Dit bestand
```

## 💰 Kosten

- GitHub: GRATIS (public repo, 2000 build minutes/maand)
- Tailscale: GRATIS (tot 100 devices)
- Apple Developer: NIET nodig (Android only)
- **Totaal: €0**

## 🔒 Veiligheid

- ✅ Tailscale = end-to-end encrypted (WireGuard)
- ✅ Geen Kraken API keys op telefoon (bot blijft op PC)
- ✅ Verbinding alleen tussen jouw devices
- ✅ Geen cloud storage van persoonlijke data
- ⚠️ APK is debug-signed (niet voor Play Store, alleen sideload)

## 📞 Support

- Bot issues: zie Kraken Bot v5 documentatie
- Mobile app issues: GitHub Issues op deze repo
- Tailscale issues: https://tailscale.com/kb/

---

🚀 **Made with ❤️ for Kelvin's Kraken Bot v5**
