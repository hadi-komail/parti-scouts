# Parti-Scouts — Website

Statische, mehrsprachige Website für das Projekt Parti-Scouts (Albatros gGmbH,
in Kooperation mit der Stiftung DFK). Reines HTML/CSS/JS, kein Build-Schritt,
lauffähig direkt über GitHub Pages.

## Struktur

Jede Unterseite liegt in einem eigenen Ordner als `index.html`, damit die
URLs ohne `.html`-Endung funktionieren (z. B. `parti-scouts.de/about/` statt
`parti-scouts.de/about.html`). Die alten `*.html`-Dateien im Root bleiben als
Weiterleitungen bestehen, damit bestehende Links/Lesezeichen nicht brechen.

```
index.html              Startseite (bereits ohne Endung unter "/" erreichbar)
about/index.html         Über das Projekt, Albatros Social & Stiftung DFK
workshops/index.html     Workshops, inkl. Beispiel „Die Farbe der Jacke“
activities/index.html    Aktivitäten / gemeinsame Freizeitgestaltung
team/index.html          Team (4 Profile)
contact/index.html       Kontakt & Nachrichtenformular
feedback/index.html      Feedback / Stimmen zum Projekt

about.html, workshops.html, activities.html, team.html, contact.html,
feedback.html            Weiterleitungen (301-artig per Meta-Refresh/JS) auf
                         die jeweilige /ordner/-Version, für alte Links

css/style.css      Gemeinsames Stylesheet (Farben aus dem Logo)
js/i18n.js         Übersetzungen: Deutsch, Englisch, Türkisch, Arabisch, Persisch
js/main.js         Sprachumschaltung, mobiles Menü, Scroll-Animationen
assets/logo.svg    Vollständiges Logo (Bildmarke + Schriftzug), aktuell ungenutzt
assets/icon.svg    Logo-Bildmarke ohne Schriftzug — Header & Favicon (helle Flächen)
assets/icon-light.svg  Bildmarke in Hell/Weiß — für dunkle Flächen (Footer)
CNAME              Für GitHub Pages: parti-scouts.de
```

Alle internen Links (Navigation, Footer, Karten) sowie CSS/JS/Bild-Referenzen
verwenden absolute Pfade ab Domain-Root (`/about/`, `/css/style.css`,
`/assets/...`) statt relativer Pfade — das ist nötig, weil die Seiten jetzt in
unterschiedlichen Ordnertiefen liegen, und funktioniert unverändert unter
GitHub Pages mit eigener Domain.

**Neue Unterseite anlegen:** Ordner mit `index.html` erstellen (Vorbild:
`feedback/index.html`), Navigation auf allen Seiten ergänzen (Header + Footer,
7 Dateien) und bei Bedarf eine `<name>.html`-Weiterleitung im Root anlegen.

## Sprachen

Standardsprache ist Deutsch. Über die Sprachleiste im Footer jeder Seite lässt
sich zwischen Deutsch, Englisch, Türkisch, Arabisch und Persisch wechseln.
Arabisch und Persisch werden automatisch rechtsbündig (RTL) dargestellt und
nutzen die Schriftart Vazirmatn, die beide Schriftsysteme sauber abdeckt.

Die Sprachwahl wird im Browser gespeichert (localStorage) und bleibt beim
Wechsel zwischen Seiten erhalten. Direktlinks mit `?lang=en`, `?lang=tr`,
`?lang=ar` oder `?lang=fa` funktionieren ebenfalls.

Alle Texte liegen zentral in `js/i18n.js`. Neue Sprache hinzufügen: Objekt in
`I18N` ergänzen und in `LANGUAGES` eintragen (Code, Label, `dir`).

## Wichtig: immer den kompletten Ordner neu hochladen

CSS und JavaScript sind mit einer Versionsnummer versehen
(`style.css?v=20260810`, `i18n.js?v=20260810` usw.), damit Browser und die
GitHub-Pages-CDN nach einem Update nicht versehentlich eine alte,
zwischengespeicherte Version ausliefern. **Trotzdem gilt:** Bei jedem Update
immer den gesamten Ordnerinhalt hochladen — nicht nur einzelne HTML-Dateien.
Wird z. B. nur `index.html` aktualisiert, aber `css/style.css` oder
`js/i18n.js` bleiben auf einem älteren Stand, entstehen Inkonsistenzen:
neue Textschlüssel bleiben unübersetzt, neue Layout-Regeln fehlen.

Bei zukünftigen Änderungen an `css/style.css` oder `js/*.js`: die Version in
der `?v=...`-Kennung in allen sechs HTML-Dateien hochzählen (z. B. auf das
aktuelle Datum), damit Browser die neue Version sicher laden.

## Team

Die vier Profile auf `team.html` sind mit echten Namen, Rollen und
E-Mail-Adressen befüllt (Majdy Aldoibal, Myriam Lagha, Hadi Komail, Yahya
Hawa). Die Avatare zeigen Initialen statt Fotos — echte Fotos können bei
Bedarf ergänzt werden (`.avatar` in `css/style.css` durch `<img>` ersetzen).

## Kontaktformular

`contact.html` sendet über den Formspree-Endpunkt
`https://formspree.io/f/xeajozkq` — funktioniert ohne eigenen Server direkt
auf GitHub Pages. Zugestellt wird an die im Formspree-Dashboard hinterlegte
Adresse. Die im Kontaktbereich angezeigte Adresse ist `partiscouts@albatrosggmbh.de`.

## Noch zu prüfen

- Adresse und Telefonnummer stammen von der öffentlichen Albatros-Seite zu
  Parti-Scouts — bitte gegenprüfen, falls sich diese geändert haben.
- Bei Bedarf echte Team-Fotos statt Initialen-Avatare ergänzen.

## Hosting auf GitHub Pages mit eigener Domain

1. Diesen Ordnerinhalt in ein GitHub-Repository pushen (Inhalt direkt im
   Root, nicht in einem Unterordner — z. B. `main`-Branch).
2. Im Repository unter **Settings → Pages**: Branch `main`, Ordner `/root`
   auswählen und speichern.
3. Die Datei `CNAME` (bereits enthalten, Inhalt `parti-scouts.de`) sorgt
   dafür, dass GitHub Pages die Domain kennt.
4. Beim Domain-Registrar für `parti-scouts.de` die DNS-Einträge auf GitHub
   Pages zeigen lassen:
   - `A`-Records der Root-Domain auf die vier GitHub-Pages-IPs, **oder**
   - `ALIAS`/`ANAME` auf `<username>.github.io`, falls der Provider das
     unterstützt.
   - Für `www.parti-scouts.de` zusätzlich ein `CNAME`-Record auf
     `<username>.github.io`.
   - Aktuelle IP-Adressen und Details: GitHub-Doku „Managing a custom domain
     for your GitHub Pages site".
5. Im Pages-Setting **„Enforce HTTPS"** aktivieren, sobald das Zertifikat
   ausgestellt wurde (kann nach dem DNS-Wechsel einige Stunden dauern).

## Hinweis

Diese Website ist ein unabhängig erstelltes Informationsangebot auf Basis
öffentlich zugänglicher Angaben. Vor der Veröffentlichung bitte durch
Albatros gGmbH / das Parti-Scouts-Team inhaltlich freigeben lassen.
