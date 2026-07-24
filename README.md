# Staatenkunde

Ein Lernspiel für die 50 US-Bundesstaaten, als einzelne statische `index.html`-Datei.

## Lokal öffnen

Einfach `index.html` im Browser öffnen — keine Build-Schritte oder Abhängigkeiten nötig.

## Deployment

Statische Seite, deploybar auf Vercel ohne Build-Konfiguration (Root-Verzeichnis, kein Framework).

## Kartendaten

Die Umrisse für Österreich, Kanada, Australien, Italien, Schweden, Japan,
Thailand, Europa und die Welt (Länderansichten) stammen aus dem
[`@svg-maps`](https://github.com/VictorCazanave/svg-maps)-Projekt von Victor
Cazanave (CC-BY-4.0) — Europa und Welt nutzen das `@svg-maps/world`-Paket,
gefiltert auf 44 europäische bzw. 195 souveräne Länder weltweit (193
UN-Mitglieder plus Vatikanstadt und Palästina; abhängige Gebiete wie Grönland
oder Puerto Rico sind nicht enthalten). Schweiz und Deutschland basieren auf
vom Nutzer bereitgestellten SVG-Dateien, die USA-Geometrie war Teil der
ursprünglich hochgeladenen Spieldatei.
