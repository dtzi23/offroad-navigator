# Off-road Navigator — Handleiding

## Wat doet de app?
Quad trip planner en GPS tracker als Progressive Web App (PWA). Op de laptop plan je een route en bekijk je off-road wegen. Op de telefoon volg je de route live met GPS tracking.

---

## App openen

**Lokaal (laptop + telefoon op zelfde WiFi):**
- Laptop: `http://localhost:8009/OFF-ROAD-NAVIGATOR.html`
- Telefoon: `http://192.168.1.99:8009/OFF-ROAD-NAVIGATOR.html`
  *(Let op: GPS tracking vereist HTTPS — werkt alleen via Netlify URL)*

**Online (GPS + alle functies):**
`https://dtzi23.github.io/offroad-navigator/`

**Installeren op telefoon:**
Ga naar de GitHub Pages URL in Safari → Deel → Zet op beginscherm

---

## Tab: Planning (laptop)

### Off-road overlay (standaard geladen)
Bij het opstarten worden automatisch **58 off-road wegen** in de Achterhoek geladen, gekleurd op rijdbaarheid:

| Kleur | Betekenis |
|-------|-----------|
| 🟢 Groen | `highway=track` — voertuigspoor, geschikt voor quad |
| 🟠 Oranje | `highway=path/footway` — voetpad, twijfelachtig voor quad |
| 🔴 Rood | `access=no/private` — verboden toegang |
| ⬜ Grijs | Overige wegen |

**Overlay knoppen (verschijnen na laden):**
- **👁 Overlay verbergen/tonen** — overlay aan/uit schakelen
- **🎯 Zoom naar data** — kaart inzoomen op de overlay

### Zandwegen importeren
Upload extra GPX of GeoJSON bestanden (bijv. Overpass Turbo exports):
1. Klik **📁 Upload GPX/GeoJSON** of **sleep een bestand op de kaart**
2. Het bestand wordt automatisch verwerkt en ingekleurd
3. GPX wordt automatisch omgezet naar GeoJSON (geen conversie nodig)
4. Overpass-exports: punten worden automatisch gefilterd, alleen wegen zichtbaar
5. Kaart zoomt automatisch naar de geüploade data

### Route plannen
1. Klik op het **potlood-icoon** linksboven op de kaart (Leaflet Draw)
2. Klik op de kaart om waypoints te plaatsen
3. Dubbelklik om de route af te sluiten
4. De **Route afstand** in de sidebar update automatisch

Klik **Wissen** om de huidige route te verwijderen.

### Trips beheren
| Knop | Functie |
|------|---------|
| 💾 Opslaan | Sla route op in de browser (localStorage) |
| 📂 Laden | Laad een eerder opgeslagen route |
| ⬇️ Export GPX | Download route als `.gpx` bestand |
| 📱 Deel via QR | Genereer QR-code om route naar telefoon te sturen |

### Route delen naar telefoon via QR
1. Teken een route op de laptop
2. Klik **📱 Deel via QR**
3. Scan de QR-code met je telefoon
4. De app opent op je telefoon met de route direct geladen
5. Druk op **▶ Start tracking** en rij

### Kaartlagen wisselen
Klik op het **lagenicoon** rechtsboven op de kaart:
- **OpenStreetMap** — standaard wegenkaart
- **Satellite** — satellietbeelden (Esri)

---

## Tab: Tracking (telefoon)

> ⚠️ **GPS vereist HTTPS** — gebruik de Netlify URL, niet het lokale IP-adres.

### GPS tracking starten
1. Ga naar de **🎯 Tracking** tab
2. Tik **▶ Start tracking**
3. Geef toestemming voor locatie als de browser daarom vraagt
4. Jouw positie verschijnt als stip op de kaart
5. De gereden track wordt als lijn bijgehouden

### Stats
Linksonder op het scherm zie je live:
- **Afstand** — totaal gereden kilometers
- **Snelheid** — huidige snelheid in km/u

### Tracking stoppen
Tik **⏹ Stop tracking** — de track blijft zichtbaar op de kaart.

### Vergelijken met geplande route
Als je via QR een route hebt geladen, zie je beide lijnen over elkaar — de geplande route en de gereden track.

---

## Tips

- **Offline:** Kaarttiles die je eerder hebt bekeken zijn gecached via de service worker.
- **GPS werkt niet:** Controleer of je de Netlify URL gebruikt (HTTPS vereist voor locatie).
- **Safari cache:** Als de app na een update niet goed laadt, sluit alle tabbladen en open opnieuw.
- **Grote GPX-bestanden:** Routes met 100+ punten kunnen een langere QR-code genereren. Bij problemen: gebruik GPX export en importeer handmatig op de telefoon.
- **Meer gebieden toevoegen:** Upload extra Overpass Turbo GeoJSON exports via de Upload-knop. Meerdere overlays stapelen.

---

## Technische info

| Onderdeel | Details |
|-----------|---------|
| Bestandslocatie | `/Users/dennisdietz/Desktop/claude test/Off-road Navigator/` |
| Hoofdbestand | `OFF-ROAD-NAVIGATOR.html` (77KB, standalone) |
| Standaard overlay | 58 off-road wegen Achterhoek (ingebakken, 23KB) |
| Data opslag | Browser localStorage (per apparaat) |
| Kaartbibliotheek | Leaflet.js v1.9.4 + Leaflet.Draw v1.0.4 |
| GPX conversie | @tmcw/togeojson v5.8.1 |
| QR generatie | qrcodejs v1.0.0 |
| GPS | Browser Geolocation API (HTTPS vereist) |
| PWA | Service worker (offroad-v4) + manifest.json |
| Browser | Chrome of Safari (iOS 16+) |
| GitHub Pages URL | https://dtzi23.github.io/offroad-navigator/ |
