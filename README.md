# 🎫 Discord Ticket Bot mit WebUI

Ein moderner Discord-Bot zur Ticketverwaltung mit integrierter Web-Oberfläche und Audit-Logging.

## ✅ Funktionen

- **Ticket-Erstellung via Button**  
  Benutzer können mit einem Klick ein Ticket eröffnen.  
  Der Bot erstellt automatisch einen privaten Text-Channel unter einer definierten Kategorie.

- **Begrüßung beim Ticketstart**  
  Der Bot begrüßt den Nutzer im Ticket mit einer dynamischen, tageszeitabhängigen Nachricht.

- **Anhänge und Nachrichtenverlauf**  
  Alle Nachrichten im Ticket (inkl. Anhänge) werden automatisch in `tickets.json` gespeichert.

- **Ticket schließen durch Moderatoren**  
  Moderatoren (definiert über Rollen-ID) können Tickets im Discord via Button schließen.  
  Dabei wird:
  - das Ticket archiviert
  - der Channel gelöscht
  - ein Eintrag im `audit.log.jsonl` gespeichert

- **WebUI (Node.js Express + Tailwind)**  
  Ein geschützter Adminbereich (nur für Mods) bietet:
  - Übersicht aller aktiven Tickets (`index.html`)
  - Historie geschlossener Tickets (`audit.html`)
  - Discord OAuth2-Login zur Authentifizierung
  - Direkte Schließung von Tickets über das Webinterface

- **Mehrrollen-Unterstützung**  
  Mehrere Mod-Rollen können in der `.env` konfiguriert werden.

- **Sicherheit**  
  - Sessions und Berechtigungen werden geprüft und automatisch beendet bei fehlenden Rechten

## ⚙️ Technologien

- [Node.js](https://nodejs.org/)
- [discord.js](https://discord.js.org/)
- [Express](https://expressjs.com/)
- [TailwindCSS](https://tailwindcss.com/)
- [Passport + Discord OAuth2](http://www.passportjs.org/)
- Plain JSON / JSONL-Dateien (statt Datenbank)
