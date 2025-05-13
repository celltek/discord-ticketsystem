```diff
- Source files are not published
```

# 🎫 Discord Ticket Bot mit WebUI

Ein moderner Discord-Bot zur Ticketverwaltung mit integrierter Web-Oberfläche und Audit-Logging.

![image](https://github.com/user-attachments/assets/f6495386-a196-4e10-ba67-d42d1ac1b7bb)


## ✨ Features

- 🎫 **Ticket-System in Discord**
  - Button zum Erstellen im festgelegten Channel
  - Automatische Channel-Erstellung mit UUID
  - Benutzer kann direkt Fragen stellen
  - Begrüßungstext per JS (`getGreeting()`)

- 🎤 **Sprachkanal-Funktion**
  - Mods oder definierte Rollen können per Button einen Voice-Channel erstellen
  - Voice-Channel erhält den gleichen Namen wie das Ticket
  - Wird automatisch gelöscht beim Schließen

- 🔒 **Moderation**
  - „Ticket schließen“-Button nur für Mods sichtbar
  - Separate Nachricht für Moderatoren mit Rolle-Mention
  - Audit-Log (`audit.log.jsonl`) speichert wer wann welches Ticket geschlossen hat

- 🖥️ **WebUI mit Tailwind CSS**
  - Übersicht über offene & bearbeitete Tickets
  - Discord-Farben & Responsive Design
  - Discord-Login via OAuth2 (Avatar + Name nach Login)
  - Ticketverlauf inkl. Anhänge einsehbar im Modal
  - Tickets per Button im Web schließen (nur Mods)
  - Auto-Refresh alle 10 Sekunden
  - Sound & Toast-Benachrichtigung bei neuen Tickets

- 🔁 **Synchronisierung**
  - Ticket wird beim Schließen im Web auch im Discord gelöscht (inkl. Voice)
  - Änderungen an Tickets werden in `tickets.json` gespeichert

- 📡 **REST-API (mit API-Key)**
  - `GET /api/tickets` – alle offenen Tickets
  - `GET /api/tickets/:id` – einzelnes Ticket
  - `POST /api/tickets/:id/close` – Ticket schließen inkl. Discord-Löschung

- ⚙️ **Konfiguration via `config.json` & `.env`**
  - `modRoleIds`, `ticketCategoryId`, `ticketButtonChannelId`, `voiceSupportRoleIds`
  - `.env`: Discord OAuth2-Keys, API-Key, Guild-ID

- 🔔 **Benachrichtigungen**
  - Ton beim Eingang neuer Tickets (auch bei Hintergrund-Tab)
  - Visueller Toast unten rechts

- 🧾 **Auditseite (`audit.html`)**
  - Bearbeitete Tickets klickbar einsehbar
  - Vollständiger Verlauf + Anhang-Vorschau
  - Rücklink zur Hauptübersicht

- 🔐 **Rechteverwaltung**
  - WebUI nur für eingeloggte Mods sichtbar
  - Logout bei fehlender Rolle


## 🔌 API (für externe Tools)
Authentifizierung erfolgt über einen API-Key im HTTP-Header:
```
Authorization: Bearer <TICKET_API_KEY>
```
Setze den Key in .env als:
```
TICKET_API_KEY=dein-geheimer-api-key
```

## 📋 GET /api/tickets
Ruft alle offenen Tickets ab.

## 📋 GET /api/tickets/:id
Ruft ein einzelnes Ticket mit Verlauf & Anhängen ab. 

## ❌ POST /api/tickets/:id/close
Schließt ein Ticket per API (inkl. Kanal-/Voice-Channel-Löschung und Auditlog).
- ✅ Ticket wird entfernt
- 🔇 Discord-Channel wird gelöscht
- 🗂️ Eintrag landet im audit.log.jsonl

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
SESSION_SECRET=
GUILD_ID=
MOD_ROLE_IDS=role1,role2
TICKET_API_KEY=
```

## 🚀 Start

```bash
npm install
node bot.js
```
