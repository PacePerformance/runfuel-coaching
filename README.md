# Matze Performance – Website

Das ist der Code für **matzeperformance.de**. Die Seite ist eine einfache, „statische“ Website: keine App-Installation, kein Build-Schritt. Jede Datei wird genau so ausgeliefert, wie sie hier liegt.

> **Kurz gesagt:** Datei ändern → speichern → im Browser prüfen → zu GitHub hochladen (pushen). Nach 1–2 Minuten ist die Änderung online.

---

## 1. Was liegt wo?

| Datei / Ordner | Wofür | Live? |
|---|---|---|
| `index.html` | **Die Startseite.** Alles in einer Datei: Aussehen, Inhalt und Verhalten. | ✅ ja |
| `admin.html` | Dein Admin-Bereich (Login, Buchungen ansehen, freie Termine eintragen). Erreichbar unter `matzeperformance.de/admin.html`. | ✅ ja |
| `img/` | **Bilder der aktuellen Startseite** (klein und fürs Web optimiert). | ✅ |
| `fonts-mp/` | Die Schriften der Startseite (Archivo, Instrument Sans, JetBrains Mono). Nicht anfassen. | ✅ |
| `favicon.svg` | Kleines Logo im Browser-Tab. | ✅ |
| `LOGOMP.png` | Logo als Bild (Original). | – |
| `CNAME` | Sagt GitHub, dass die Seite unter `matzeperformance.de` läuft. **Nicht löschen oder ändern!** | ✅ |
| `bilder/` | Große Original-Fotos, nur von den alten Seitenversionen benutzt. | alt |
| `Realindex.html`, `Workedindex.html`, `indexV2.0.html`, `index-alt-2026-09.html` | **Alte Versionen** der Startseite (Backup). Sie sind trotzdem online erreichbar, wenn man den Dateinamen kennt. | alt |
| `fonts` (Datei ohne Endung) | Alte Schrift-Einstellung, wird von der aktuellen Seite nicht benutzt. | alt |

---

## 2. Wie ist `index.html` aufgebaut?

Die Datei hat drei Teile. In der Datei steht vor jedem Bereich ein erklärender Kommentar.

1. **`<style>` – das Aussehen** (ca. ab Zeile 80)
   Farben, Schriften, Abstände, Handy-Darstellung.
2. **`<body>` – der Inhalt** (ca. ab Zeile 760)
   Abschnitte von oben nach unten: Menü → Hero → Stärken → Methode → Coaching → App → Über mich → Road to Sub 2:30 → FAQ → Kontakt → Footer → Impressum/Datenschutz.
3. **`<script>` – das Verhalten** (ganz unten)
   Handy-Menü, Angebotsfilter, Buchungsformular mit Kalender, Formkurve, Fortschrittslinie „km 0 bis 42,2“.

**Kommentare** sehen so aus und sind für Besucher unsichtbar:
- im Inhalt: `<!-- Notiz -->`
- im Aussehen und im Skript: `/* Notiz */` oder `// Notiz`

---

## 3. Häufige Änderungen (Rezepte)

Tipp: In VS Code (oder einem anderen Editor) mit **Strg+F** nach dem Suchbegriff suchen.

### Text ändern
Text steht zwischen `>` und `<`, zum Beispiel:
```html
<p class="lead muted">Hier steht der Text, den du ändern kannst.</p>
```
Nur den Text ändern, nicht die Teile in spitzen Klammern. Ein `&` schreibt man im HTML als `&amp;`.

### Neues Rennen in die Formkurve eintragen
Suchbegriff: **`race-data`**. Unten eine Zeile anhängen:
```html
<li><span>Valencia 2026</span><span>2:33h</span></li>
```
Die Kurve, die Kennzahlen und der rote Bestzeit-Punkt aktualisieren sich **automatisch**.
Das Ziel (2:30) steht im Skript bei **`goal=150`** (in Minuten: 150 = 2:30).

### Neue Bestzeit
Die Bestzeit steht an mehreren Stellen. Suche nach **`2:35`** und passe jede Stelle an:
Zahlenleiste (`proof`), Tokyo-Kachel, Text in der Tokyo-Kachel, Road to Sub 2:30 (`gap230` und Zeitleiste) und `<meta name="description">` ganz oben.

### Preis ändern
Ein Preis steht an **zwei** Stellen:
1. Angebotskarte im Abschnitt **`COACHING`**: `ab <b>150 €</b>`
2. Kontaktformular, Suchbegriff **`data-svc`**: `data-price="150"` und der Text `ab 150 €`

### Neues Angebot
1. Unter `COACHING` eine komplette `<article class="offer"> … </article>` kopieren und die Texte ändern.
2. `data-goals="first pb fit"` bestimmt, bei welchem Filter die Karte sichtbar bleibt.
3. Im Kontaktformular einen passenden `chip` kopieren. **`data-pick` der Karte = `data-val` des Chips.**

### Neue FAQ-Frage
Suchbegriff **`FAQ`**, dann eine Zeile kopieren:
```html
<details><summary>Deine Frage?</summary><p>Deine Antwort.</p></details>
```

### Bild austauschen
1. Das neue Bild in den Ordner `img/` legen. Am besten JPG mit ca. 1200–1600 px Breite und unter 400 KB, Dateiname ohne Leerzeichen und Umlaute.
2. In `index.html` bei `src="img/…"` den Dateinamen eintragen.
3. `alt="…"` passend beschreiben.
4. Wenn der Ausschnitt nicht passt: `object-position:50% 25%` anpassen (erste Zahl links↔rechts, zweite Zahl oben↔unten).

### Farben ändern
Suchbegriff **`:root`**. Dort ist jede Farbe einmal festgelegt, zum Beispiel `--signal:#E30A17` für das Rot.
Die Dunkelmodus-Farben stehen direkt darunter (in zwei Zeilen) und müssen ggf. auch angepasst werden.

### Fotos immer farbig statt schwarz-weiß
In `<style>` jedes `filter:grayscale(1)` durch `filter:none` ersetzen.

### Menüpunkt hinzufügen
Zwei Stellen: `nav class="main"` (Computer) und `id="overlay"` (Handy-Menü).
`href="#xyz"` springt zum Abschnitt mit `id="xyz"`.

### Jahreswechsel
Im Footer `© 2026` anpassen. Ggf. auch „Ziel 2027“ in Road to Sub 2:30 und „Stand:“ in der Datenschutzerklärung.

---

## 4. Buchungen & freie Termine

```
Besucher füllt Formular aus (index.html)
        │  speichert
        ▼
Supabase-Datenbank, Tabelle "bookings"  ──►  du siehst sie in admin.html
        ▲
        │  liest freie Termine
Supabase, Tabelle "settings" (Eintrag "availability")  ◄──  du trägst sie in admin.html ein
```

- **Freie Termine** stellst du in `admin.html` ein, nicht in `index.html`.
- Der Schlüssel `SUPABASE_KEY` im Code ist der **öffentliche** Schlüssel. Er darf sichtbar sein. Die Sicherheit regeln die Datenbank-Regeln (RLS) in Supabase.
  **Niemals** den geheimen `service_role`- bzw. `secret`-Schlüssel in eine HTML-Datei schreiben, die Dateien sind öffentlich.

### Sicherheit im Admin-Bereich
- **Kundendaten immer mit `esc(...)` anzeigen.** Alles aus dem Buchungsformular (Name, E-Mail, Nachricht …) kann jeder frei eintippen, auch Schadcode. Wenn du in `admin.html` einen neuen Wert per `${...}` ins HTML einbaust, schreib ihn so: `${esc(b.fname)}` statt `${b.fname}`. Dann erscheint er nur als Text.
- **Vor dem Bestätigen den Betrag prüfen.** Der Betrag (`paid`) kommt aus dem öffentlichen Formular und könnte manipuliert sein (z. B. 1 € statt 150 €). Er landet im PayPal-Link der Bestätigungs-Mail. Also kurz checken, ob Leistung und Betrag zusammenpassen.

### Typische Änderungen in `admin.html`
| Was | Suchbegriff |
|---|---|
| Farben der Admin-Seite | `:root` |
| Bestätigungs-Mails aktivieren (EmailJS-IDs eintragen) | `EMAILJS_SERVICE_ID` |
| Inhalt der Bestätigungs-Mail (Werte für die Vorlage) | `templateParams` |
| Auswahl der Termin-Länge (30/60/90/120 Min) | `slot-dur` |
| Standardzeit für neue Zeitfenster (09:00–12:00) | `'09:00','12:00'` |
| Uhrzeit-Schritte in den Zeitfeldern (30 Min) | `step="1800"` (900 = 15 Min) |
| Texte der Status-Etiketten | `function statusBadge` |
| Menü-Texte links | `nav-item` |
| Hinweis-Meldungen und deren Anzeigedauer | `showNotif` |

---

## 5. Änderungen testen und veröffentlichen

**Lokal testen:** `index.html` per Doppelklick im Browser öffnen. Bitte auch schmal ziehen (Handy-Ansicht) und dunklen Modus prüfen.
Hinweis: Kalender und Buchung funktionieren lokal nur, wenn Internet da ist (Supabase).

**Veröffentlichen** (im Ordner `Rebrand/launch`):
```bash
git pull
```
```bash
git add -A
```
```bash
git commit -m "Kurz beschreiben, was geändert wurde"
```
```bash
git push
```
Erst `git pull`: Falls auf GitHub direkt etwas geändert wurde, holst du es so vorher ab.

**Etwas kaputt gemacht?**
- Noch nicht gespeichert/committet: `git restore index.html` setzt die Datei auf den letzten Stand zurück.
- Schon gepusht: In GitHub unter „Commits“ siehst du jede Version, oder frag Claude, den letzten Commit rückgängig zu machen.
