# 🗺️ DIY: Bild-gemappte Geländekarte (3D-Karte aus OSM- und Satellitendaten)

Dieser Workflow beschreibt die Erstellung einer maßstabsgetreuen 3D-Karte aus **OpenStreetMap-Daten (OSM)**, **Satellitenbildern** und **Höhendaten**.

Alle verwendeten Tools und Datenquellen sind frei zugänglich oder Open Source.

---

## 🌟 Übersicht

| Kategorie | Tool / Quelle | Zweck |
| :--- | :--- | :--- |
| **Datenquellen** | Overpass Turbo, TouchTerrain, Copernicus Dataspace | Geodaten, Höhendaten, Satellitenbilder |
| **Bearbeitung** | Mapshaper, Affinity Designer (oder GIMP) | Datenreduktion, Texturvorbereitung |
| **3D-Modellierung**| Rhino 3D (oder Blender) | Zusammenführen von Modell und Textur |

---

## ⚙️ Schritt-für-Schritt-Workflow

### 1. OSM-Daten exportieren (Overpass Turbo)

1.  Öffne [Overpass Turbo](https://overpass-turbo.eu/).
2.  Füge die gewünschte Query ein (Beispiel: Relation 535929):

    ```overpass
    [out:json][timeout:60];
    rel(535929);
    out geom;
    ```
3.  Führe die Abfrage aus und exportiere das Ergebnis als **KML** oder **GeoJSON**.

### 2. Daten reduzieren (Mapshaper)

1.  Öffne [mapshaper.org](https://mapshaper.org/).
2.  Lade die exportierte KML/GeoJSON-Datei hoch.
3.  Bereinige und vereinfache die Geometrien.
4.  Exportiere die bereinigte Datei wieder als **KML**.

### 3. Konvertieren in Google Earth

1.  Öffne [Google Earth Web](https://earth.google.com/web/).
2.  Lade die reduzierte KML-Datei hoch.
3.  Stelle die gewünschte **Kamera-Ansicht und Höhe** ein.
4.  Kopiere den Link (enthält die Geo-Referenzierung):

    ```url
    [https://earth.google.com/web/@50.16980605,9.21375495,203.57461311a,12980.65898276d,30y,0h,0t,0r/data=](https://earth.google.com/web/@50.16980605,9.21375495,203.57461311a,12980.65898276d,30y,0h,0t,0r/data=)...
    ```

### 4. 3D-Geländemodell generieren (TouchTerrain)

1.  Besuche [TouchTerrain](https://touchterrain.geos.iastate.edu/).
2.  Wähle das Gebiet aus (manuell oder über Koordinaten/Link).
3.  Einstellungen:
    * **Auflösung:** z. B. 50 m / Pixel
    * **Format:** **OBJ** (für Textur-Mapping)
4.  Generiere und lade das 3D-Modell herunter.

### 5. Wolkenlose Satellitenkarte (Copernicus/LGLN)

1.  Lade ein **wolkenfreies Satellitenbild** des Gebiets herunter (z.B. von ESA Copernicus Dataspace oder LGLN Cloud-Free Districts).

### 6. Bildbearbeitung & Texturvorbereitung (Affinity Designer)

1.  Öffne das Satellitenbild.
2.  **Schneide** das Bild exakt auf die Abmessungen des 3D-Modells zu.
3.  *Optional:* Farbkorrektur, Upscaling (mit ImgUpscaler).
4.  Speichere das Bild als Textur (z.B. `texture_map.jpg`).

### 7. Zusammenführen (Rhino 3D)

1.  Importiere das 3D-Geländemodell (`.obj`) in **Rhino 3D**.
2.  Importiere die `texture_map.jpg` als Material/Textur.
3.  Wende **Planar Mapping** an, um die Textur korrekt auf das Gelände zu legen.
4.  Exportiere das finale texturierte Modell (z.B. als **.obj** oder **.glb**).

---

## ✨ Ergebnisse

* 3D-Geländemodell mit realer Höhenstruktur
* Texturierte Karte mit wolkenfreiem Satellitenbild

**Dateibeispiele:**
* `terrain_model.obj`
* `Bildschirmfoto 2025-10-29 um 22.18.52.png`
* `combined_3d_model.obj`

---

## ⚖️ Lizenz & Autor

Dieses Projekt steht unter der **Creative Commons Attribution 4.0 International (CC BY 4.0)** Lizenz.

* **Autor:** Maximilian Pfannkuch
* **Stand:** Oktober 2025
