# Parti-Scouts — Website

Statische, mehrsprachige Website für das Projekt Parti-Scouts (Albatros gGmbH,
in Kooperation mit der Stiftung DFK). Reines HTML/CSS/JS, kein Build-Schritt,
lauffähig direkt über GitHub Pages.

## Struktur

```
index.html        Startseite
about.html         Über das Projekt, Albatros sozial & Stiftung DFK
workshops.html     Workshops, inkl. Beispiel „Die Farbe der Jacke“
activities.html    Aktivitäten / gemeinsame Freizeitgestaltung
team.html          Team (4 Platzhalter-Profile — bitte ersetzen)
contact.html       Kontakt & Nachrichtenformular
css/style.css      Gemeinsames Stylesheet (Farben aus dem Logo)
js/i18n.js         Übersetzungen: Deutsch, Englisch, Türkisch, Arabisch, Persisch
js/main.js         Sprachumschaltung, mobiles Menü, Scroll-Animationen
assets/logo.svg    Logo (vollständig, aus der Original-PDF vektorisiert)
assets/icon.svg    Logo-Bildmarke ohne Schriftzug (Favicon)
CNAME              Für GitHub Pages: parti-scouts.de
```

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

## Vor der Veröffentlichung noch zu erledigen

- **Team-Seite**: Die vier Profile sind Platzhalter. Echte Namen, Rollen,
  Kurzbeschreibungen und optional Fotos einsetzen (`team.html`, Texte in
  `js/i18n.js` unter den Schlüsseln `team.*`).
- **Kontaktformular**: `contact.html` nutzt aktuell `mailto:` als
  Formular-Ziel (öffnet das E-Mail-Programm der Besucherin/des Besuchers,
  funktioniert ohne Server). `REPLACE_WITH_EMAIL@parti-scouts.de` durch die
  echte Adresse ersetzen. Für eine Inline-Zustellung ohne E-Mail-Programm
  empfiehlt sich ein Formular-Dienst wie Formspree oder Netlify Forms.
- **E-Mail-Adresse** im Kontaktbereich (`contact.email_placeholder` in
  `js/i18n.js`, für jede Sprache) ergänzen.
- Adresse und Telefonnummer stammen von der öffentlichen Albatros-Seite zu
  Parti-Scouts — bitte gegenprüfen, falls sich diese geändert haben.

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
