# EvenCharge – Tanken oder Laden?

Die Web-App vergleicht die Energiekosten pro 100 km zwischen Verbrenner (Diesel, Super E5, E10) und Elektroauto. Sie berechnet außerdem, bis zu welchem Strompreis Laden günstiger ist als Tanken.

## Funktionen

- **Live-Spritpreis per PLZ:** Die App sucht die Koordinaten zur Postleitzahl (Zippopotam.us) und holt dann über die [Tankerkönig-API](https://creativecommons.tankerkoenig.de) den günstigsten Preis einer geöffneten Tankstelle im Umkreis.
- **Diesel oder Benzin** per Auswahlknopf, bei Benzin zusätzlich Super E5 oder E10.
- **Schieberegler** für Spritverbrauch, Stromverbrauch (Bordcomputer), Ladeverluste und Strompreis.
- **Ladeverluste** werden pauschal aufgeschlagen. Schnellwahl: DC-Schnelllader 5 %, Wallbox 10 %, Haushaltssteckdose 18 %.
- **Ergebnis:** Kosten pro 100 km, Ersparnis, Strompreis, bis zu dem Laden günstiger ist (Break-even), und ein Diagramm.

## Rechnung

```
Kosten Verbrenner = Verbrauch [L/100 km] × Spritpreis [€/L]
Bezahlter Strom   = Verbrauch Bordcomputer [kWh/100 km] × (1 + Ladeverlust)
Kosten Laden      = Bezahlter Strom × Strompreis [€/kWh]
Break-even        = Kosten Verbrenner ÷ Bezahlter Strom
```

Wer den WLTP-Normverbrauch eingibt, stellt den Ladeverlust auf 0 %. Im WLTP-Wert sind die Verluste schon enthalten.

## Einrichtung

1. Kostenlosen API-Key auf <https://creativecommons.tankerkoenig.de> beantragen.
2. In `index.html` den Platzhalter ersetzen:
   ```js
   const API_KEY = 'DEIN-API-KEY-HIER';
   ```
3. `index.html` im Browser öffnen oder über GitHub Pages veröffentlichen: Settings → Pages → Branch `main`, Ordner `/ (root)`.

Ohne gültigen Key rechnet die App mit einem Beispielpreis, den man auch von Hand überschreiben kann.

> **Hinweis:** In einer öffentlichen Seite kann jeder den API-Key im Quelltext lesen. Tankerkönig bittet außerdem, die API nicht öfter als nötig abzufragen, als Richtwert höchstens alle 5 Minuten.

## Datenquellen

- Spritpreise: Markttransparenzstelle für Kraftstoffe (MTS-K) über Tankerkönig, Lizenz CC BY 4.0
- Postleitzahl zu Koordinaten: [Zippopotam.us](https://zippopotam.us)
