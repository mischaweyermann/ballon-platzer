# Ballon-Platzer 🎈

Gratis Bewegungsspiel für den Fernseher. Das Handy ist die Kamera, der Körper ist der Controller.

- **TV / Laptop:** `index.html` – 3D-Szene, Spiel, QR-Code zum Verbinden
- **Handy:** `controller.html` – Kamera + Körpererkennung (MediaPipe), sendet nur Körperpunkte an den TV

Kein eigener Server nötig. Die Verbindung läuft direkt zwischen Handy und TV (WebRTC über den kostenlosen PeerJS-Vermittlungsserver).

## Online stellen mit GitHub Pages (gratis, mit HTTPS)

1. Neues Repository auf GitHub anlegen, z. B. `ballon-platzer`.
2. Alle Dateien aus diesem Ordner hochladen (Ordnerstruktur beibehalten).
3. Im Repo: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `(root)`** → Save.
4. Nach ca. einer Minute läuft das Spiel unter `https://<dein-name>.github.io/ballon-platzer/`.

HTTPS ist Pflicht, sonst gibt der Handy-Browser die Kamera nicht frei. GitHub Pages, Cloudflare Pages und Netlify liefern das automatisch.

## Spielen

1. Seite auf dem TV (oder Laptop per HDMI) öffnen → QR-Code erscheint.
2. QR-Code mit dem Handy scannen → **Kamera starten**.
3. Handy hinstellen (2–3 m Abstand, man muss ganz im Bild sein).
4. Beide Arme über den Kopf → Countdown → 60 Sekunden Ballone platzen.

## Charakter

8 fertige Figuren (Mia, Leo, Opa Ruedi, Nala, Kai, Zoe, Ben, Königin Lu) plus Zufall. Alles lässt sich einzeln ändern:
Hautfarbe, Frisur (7), Haarfarbe, Kopfbedeckung (Cap, Mütze, Fischerhut, Partyhut, Krone), Brille, Bart, Oberteil (T-Shirt, Pulli, Hoodie, Jacke), Hose (lang/Shorts) und Schuhe – jeweils mit Farben.

- **Auf dem Handy:** Karte «Dein Charakter» unten auf der Seite. Änderungen erscheinen sofort auf dem TV.
- **Auf dem TV/Laptop:** Button «Charakter anpassen» oder Taste `C`.
- Die Wahl wird im Browser gespeichert. Figur und Kleidung werden komplett im Code erzeugt (`js/avatar.js`), es braucht keine 3D-Dateien.

Die Figur übernimmt nur die *Richtungen* deiner Arme und Beine, die Längen kommen von der Figur. So bleibt der Chibi-Look erhalten, egal wie gross du bist. Ballone platzen mit den Händen und mit dem Kopf.

## Punkte

| Objekt | Punkte |
|---|---|
| Ballon | +10 |
| Goldener Ballon | +50 |
| Gewitterwolke | −20, Combo weg |
| Combo (Treffer kurz hintereinander) | ×2 ab 4, ×3 ab 9, ×4 ab 14 |

**Tasten auf dem TV/Laptop:** `D` Maus-Testmodus · `C` Charakter · `F` Vollbild · `M` Ton an/aus · `Leertaste`/`OK` Start

## Lokal testen

```bash
npx serve .            # oder: python3 -m http.server 8080
```

Am Laptop `http://localhost:8080` öffnen und **«Ohne Handy testen (Maus)»** klicken. Für den Handy-Test braucht es HTTPS, also am einfachsten direkt über GitHub Pages.

## Technik

| Teil | Bibliothek |
|---|---|
| 3D | Three.js 0.170 (CDN) |
| Körpererkennung | MediaPipe Pose Landmarker lite 0.10.14 (läuft auf dem Handy) |
| Verbindung | PeerJS 1.5.4 (WebRTC) |
| QR-Code | qrcode-generator 1.4.4 |
| Sound | eigene WebAudio-Synth (`js/audio.js`), keine Dateien |

**Performance:** Die TV-Seite reduziert automatisch Auflösung und Schatten, wenn das Gerät ruckelt. Eingebaute Smart-TV-Browser sind oft schwach. Am flüssigsten läuft es auf einem Laptop, Chromecast/Google TV oder Fire-TV-Stick.

**Datenschutz:** Das Kamerabild verlässt das Handy nie. Übertragen werden nur 15 Körperpunkte (x/y-Koordinaten) pro Bild.

## Ideen für später

- Weitere Spiele: «Loch in der Wand», Torwart, Tanz-Posen
- Eigene 3D-Modelle aus Blender (als `.glb` laden)
- Mehrspieler: zwei Handys, geteilter Bildschirm
- Eigener PeerJS-Server, falls der Gratis-Server einmal überlastet ist (`?peer=host:port`)
