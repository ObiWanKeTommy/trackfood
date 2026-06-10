# Kcal Dagboek

Local-first PWA om voeding te fotograferen en dagelijkse kcal bij te houden.
Geen backend, geen login: alle data (incl. foto's) staat in IndexedDB op het
toestel zelf. Werkt offline na de eerste keer laden.

## Bestanden

| Bestand                  | Doel                                          |
|--------------------------|-----------------------------------------------|
| `index.html`             | De volledige app (HTML + CSS + JS)            |
| `manifest.webmanifest`   | Maakt de app installeerbaar op het beginscherm|
| `sw.js`                  | Service worker: offline cache van de app-schil|
| `icons/`                 | App-iconen (180/192/512)                      |
| `staticwebapp.config.json` | Azure Static Web Apps configuratie          |

## Deployen naar Azure Static Web Apps

1. Maak een GitHub-repo en push deze map.
2. Azure Portal → *Create a resource* → **Static Web App** → plan **Free**.
3. Koppel de GitHub-repo. Build details: preset **Custom**,
   *App location* `/`, *Api location* leeg, *Output location* `/` (leeg).
4. Azure voegt automatisch een GitHub Actions workflow toe; elke push naar
   `main` deployt vanaf dan vanzelf.
5. (Optioneel) *Custom domains* → eigen subdomein toevoegen, CNAME in
   Cloudflare zetten (DNS only / grijze wolk tijdens validatie).

## Installeren op iPhone

Open de URL in **Safari** → deelknop → **Zet op beginscherm**.
De app opent dan fullscreen als een native app en werkt offline.

## Releases

Verhoog `CACHE_VERSION` in `sw.js` bij elke wijziging, anders blijven
geïnstalleerde clients de oude versie uit cache serveren.

## Backup

Data staat enkel op het toestel. Via de ⋯-knop in de app kan een
JSON-backup geëxporteerd en (op een ander toestel) geïmporteerd worden.
