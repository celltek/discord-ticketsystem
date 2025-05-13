```diff
- Source files are not published
```

# 🎫 Discord Ticket Bot mit WebUI

Ein moderner Discord-Bot zur Ticketverwaltung mit integrierter Web-Oberfläche und Audit-Logging.

## 🚀 Features

- 🎟️ Ticket-Erstellung per Button in festem Channel
- 🧵 Neuer Textkanal pro Ticket (`ticket-xxxxx`)
- 🛡️ Moderatoren-Schließen über Button (nur mit definierter Rolle)
- 🎙️ Sprachchannel-Erstellung (nur für berechtigte Rollen)
- ✉️ Begrüßungstext beim Start (mit Saison- und Uhrzeit-basiertem Greeting)
- 📎 Nachrichtenspeicherung mit Anhängen
- ⏱ **Auto-Close nach Inaktivität** (24h ohne Nachricht)
- 🌐 WebUI mit:
  - Authentifizierung per Discord OAuth2
  - Ticket-Anzeige + Verlauf
  - Moderatoren-Schließen über Web
  - Audit-Log für alle geschlossenen Tickets
 
## 🔒 Rollenrechte
Nur User mit den Rollen in MOD_ROLE_IDS dürfen:
- Tickets im Web einsehen
- Tickets schließen (Web + Discord)
- den Button „Ticket schließen“ klicken
Voice-Channels können nur von Nutzern mit Rollen aus voiceSupportRoleIds erstellt werden.

## ⏱ Auto-Close bei Inaktivität
Ein Hintergrundprozess schließt Tickets automatisch, wenn:
- seit der letzten Nachricht mehr als 24 Stunden vergangen sind
- die Nachricht ⏱ Ticket wurde automatisch geschlossen wird in den Channel gepostet
- Eintrag ins Auditlog erfolgt

## ⚙️ Technologien

- [Node.js](https://nodejs.org/)
- [discord.js](https://discord.js.org/)
- [Express](https://expressjs.com/)
- [TailwindCSS](https://tailwindcss.com/)
- [Passport + Discord OAuth2](http://www.passportjs.org/)
- Plain JSON / JSONL-Dateien (statt Datenbank)

## 📁 Struktur

```bash
bot.js           # Discord-Bot inkl. Ticket- und Button-Logik
web.js           # Express-Webserver mit WebUI und Auth
greeting.js      # Gruß-Funktion für personalisierte Einstiegstexte
tickets.json     # Aktive Tickets
audit.log.jsonl  # Archivierte Tickets mit Metadaten
public/
  └── index.html # Übersicht aktive Tickets
  └── audit.html # Übersicht geschlossene Tickets
```
## 🛡 Voraussetzungen

- Node.js ≥ 18
- Discord Bot-Token
- Discord App mit aktivierter OAuth2 (Redirect URI: `/auth/callback`)
- `.env` mit:

```env
DISCORD_CLIENT_ID=
DISCORD_CLIENT_SECRET=
DISCORD_REDIRECT_URI=https://domain.xyz/auth/callback
SESSION_SECRET=...
GUILD_ID=
MOD_ROLE_IDS=role1,role2
```

## 🚀 Start

```bash
npm install
node bot.js
```
