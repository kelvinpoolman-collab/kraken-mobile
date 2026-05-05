# 📱 INSTALLATIE GIDS — Kraken Terminal Mobile

## 🎯 Snelle samenvatting

```
1. GitHub account → maak repo → upload deze folder
2. GitHub Actions → bouwt APK in 5 min
3. Download APK → installeer op telefoon
4. Tailscale op PC + telefoon
5. Voer Tailscale IP in app → KLAAR!
```

---

## 📋 STAP-VOOR-STAP

### Deel 1: GitHub setup (10 min)

```
□ Maak GitHub account: https://github.com/signup
□ Klik "+" → "New repository"
□ Naam: kraken-mobile
□ Privacy: PUBLIC (gratis Actions)
□ Klik "Create repository"
```

### Deel 2: Code uploaden (5 min)

**Optie eenvoudig (web):**
```
□ Op de empty repo: klik "uploading an existing file"
□ Drag & drop ALLE bestanden uit kraken-mobile.zip
□ Commit message: "Initial mobile app"
□ Klik "Commit changes"
```

### Deel 3: Build wachten (5 min)

```
□ Klik tab "Actions" 
□ Klik op de workflow die loopt
□ Wacht tot alle ✓ groen zijn
□ Bij rode ✗: zie Troubleshooting
```

### Deel 4: APK downloaden (1 min)

```
□ Ga naar tab "Releases" (rechtsboven)
□ Klik op nieuwste release "v1"
□ Klik op "KrakenTerminal-v1.0.apk" → download
□ Stuur naar telefoon (email/Drive/WhatsApp)
```

### Deel 5: Tailscale (5 min)

**Op PC:**
```
□ Download: https://tailscale.com/download/windows
□ Installeer + log in (Google account is makkelijkst)
□ Open CMD: tailscale ip -4
□ NOTEER het IP (bv. 100.64.0.1)
```

**Op telefoon:**
```
□ Play Store → "Tailscale"
□ Log in met zelfde account
□ Toggle "Active" aan
```

### Deel 6: Bot bereikbaar (5 min)

Open `C:\Masterbot\dashboard_api.py` in Notepad.

Zoek de regel waar Flask runt (helemaal onderaan), pas aan:

```python
# WAS:
app.run(host="127.0.0.1", port=5000, debug=False)

# WORDT:
app.run(host="0.0.0.0", port=5000, debug=False)
```

Restart bot: dubbelklik `start.bat`

**Firewall toestaan (eenmalig):**

Plak in CMD (als Administrator):
```
netsh advfirewall firewall add rule name="Kraken Dashboard" dir=in action=allow protocol=TCP localport=5000
```

### Deel 7: APK installeren (2 min)

```
□ Open APK op telefoon
□ Toestaan: "Install from unknown sources"
□ Tap "Install"
□ Open app
□ Eerste keer: vul Tailscale IP in (bv http://100.64.0.1:5000)
□ Posities verschijnen ✨
```

---

## ⚠️ Troubleshooting

### Build faalt op GitHub

```
Probleem: Gradle / SDK / Java error
Oplossing: 
  1. Klik op de gefaalde stap in Actions log
  2. Check error message
  3. Meest voorkomend:
     - Network timeout → klik "Re-run failed jobs"
     - SDK version → check build-apk.yml settings
```

### App kan geen verbinding maken

```
□ Check Tailscale icoon GROEN op beide devices
□ PC firewall: rule toegevoegd?
□ Dashboard luistert op 0.0.0.0?
□ Bot draait? (kraken_bot.heartbeat recent geupdated?)
□ URL klopt? Begint met http:// (niet https://)
□ Poort 5000 erbij? bv 100.64.0.1:5000
```

### Test of Tailscale IP werkt vanaf telefoon

Open in mobile browser:
```
http://JOUW-TAILSCALE-IP:5000/api/health
```

Verwacht antwoord:
```json
{"status":"ok","timestamp":"..."}
```

Als dat niet werkt → Tailscale of firewall probleem.

### App opent maar lege schermen

```
□ Check of API URL correct is opgeslagen
□ Reset: tap ⚙ rechtsonder → vul nieuw IP in
□ Sluit app + open opnieuw
```

---

## 🎉 Wat je krijgt

```
✅ Native Android app (echte APK)
✅ Mooi cyan icoon op homescreen
✅ Volledige UI van je PC dashboard
✅ Touch-friendly (groot, mobiele layout)
✅ Pull-to-refresh
✅ Werkt overal (4G/5G/WiFi)
✅ Updates: push naar GitHub = nieuwe APK
```

🚀 **Veel succes!**
