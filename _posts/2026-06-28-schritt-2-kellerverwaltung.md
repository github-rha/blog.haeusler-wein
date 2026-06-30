---
layout: post
title: "KI Liegestütze, Schritt 2: Kellerverwaltung"
date: 2026-06-28
---

Im [letzten Beitrag](/2026/05/15/schritt-1-website/) war Schritt 1 die Fingerübung: die Webseite von der KI bauen lassen, statisches HTML, kein Zustand. Schritt 2 verlangt mehr. Wir lassen uns eine App coden, die unseren Weinkeller inventarisiert — auf dem iPhone, offline, in unserer eigenen Hand. Hintergrund war, dass die App, mit der ich bisher den Weinkeller inventarisiert habe, meine wichtigste KPI nicht mehr angezeigt hat: den Gesamtbestand an Flaschen...

Was [Kellerverwaltung](https://github.com/github-rha/kellerverwaltung) heute kann:

* den Bestand sehen — Flaschen total und pro Wein
* gezielt suchen — nach Sorte, Produzent, Land
* Flaschen erfassen und beim Kaufen oder Trinken hoch- und runterzählen
* ein Foto vom Etikett ablegen
* den ganzen Keller in ein privates GitHub-Repo sichern

<img src="{{ '/assets/kellerverwaltung-1-dashboard.png' | relative_url }}" alt="Dashboard der Kellerverwaltungs-App mit Flaschenzahl und Weinliste" width="300" style="display:block;margin:1.5rem auto">

*Das Dashboard: 206 von 331 Flaschen, gefiltert auf Rotwein. Oben der Sync-Knopf, die Sortenfilter als Fläschchen, rechts der Sommelier.*

<img src="{{ '/assets/kellerverwaltung-2-filters.png' | relative_url }}" alt="Filterpanel: Suche nach Produzent, Land und Flaschenzahl" width="300" style="display:block;margin:1.5rem auto">

*Gezielt suchen: nach Produzent — hier «Jauslin» — nach Land oder nach den fast leeren Fächern («Single bottle», «Finito»).*

Machen wir es interessant. Die technischen Vorgaben:

* kein App Store — eine Portable Web Application (PWA), in Safari über «Zum Home-Bildschirm» installiert.
* offline-first: die Daten liegen auf dem Telefon, das Netz braucht es nur zum Sichern.
* alles privat: Synchronisation in ein eigenes GitHub-Repo, kein fremder Server.

Gleiche Methode wie bei der Webseite, mehr System: wieder ein paar kurze Dokumente im Repo —

* [`vision.md`](https://github.com/github-rha/kellerverwaltung/blob/main/docs/vision.md)
* [`architecture.md`](https://github.com/github-rha/kellerverwaltung/blob/main/docs/architecture.md)
* [`operations.md`](https://github.com/github-rha/kellerverwaltung/blob/main/docs/operations.md)
* [`roadmap.md`](https://github.com/github-rha/kellerverwaltung/blob/main/docs/roadmap.md)

Am schärfsten ist die Liste dessen, was die App *nicht* sein soll. Beispiel:

> ## Non-goals
> - Social features, community ratings, tasting notes, rankings.
> - Full wine metadata cataloging (keep fields minimal).
> - Cellar location tracking (racks/bins).
> - Multi-user or collaborative workflows.

Der Stack ist ein anderer als bei der statischen Seite, das Prinzip dasselbe:

* **SvelteKit** als App, statisch ausgeliefert über **GitHub Pages** — kein Server, automatischer Deploy bei jedem Commit.
* **IndexedDB** im Browser als Datenspeicher — alles bleibt auf dem Gerät.
* **GitHub** als Sicherung — der Keller landet als eine Datei plus Etikettenfotos im privaten Repo.

Der eigentliche Unterschied zur Fingerübung: bei der Webseite hat die KI gebaut. Hier baut sie nicht nur, sie steckt drin. 

Wir hatten relativ viel Zeit verlocht mit dem Versuch, mit konventionellem OCR weiterzukommen. Am Ende haben wir aufgegeben und stattdessen einen Claude Haiku Call implementieren lassen. Resultat: Die Treffsicherheit ist genial.

Zwei Funktionen bedienen sich bei Claude APIs:

* **Etikett lesen** — ein Foto vom Etikett, und Claude liest Produzent, Name, Jahrgang und Land heraus und füllt das Formular aus.
* **Sommelier** — ein Gericht in Worten beschreiben, und die App schlägt aus dem eigenen Keller die passenden Weine vor, geordnet nach Eignung.

<video src="{{ '/assets/kellerverwaltung-4-etikett.mp4' | relative_url }}" width="300" style="display:block;margin:1.5rem auto;border:1px solid rgba(166, 42, 23, 0.2)" autoplay loop muted playsinline></video>

*Etikett lesen: Foto vom Rücketikett, «Crop & Read», und das Formular füllt sich selbst — Bodegas Vi Rei, Prensal Blanc Cosecha Propia, 2024. Der Bestand wächst von 331 auf 332.*

<img src="{{ '/assets/kellerverwaltung-3-sommelier.jpeg' | relative_url }}" alt="Sommelier-Funktion: Weinvorschläge zu einem Gericht" width="300" style="display:block;margin:1.5rem auto">

*Der Sommelier: «kalbskotelett» eingetippt, als Vorschläge kommen ein Château Palmer 2019, ein Gevrey-Chambertin, eine Romanée-Saint-Vivant — und ein Margaux 2017 mit «Drink now»-Hinweis. Die KI hat einen kostspieligen Geschmack!*

Damit ist die KI vom Werkzeug zum Bestandteil geworden. Bei der Webseite haben wir gelernt, wie man sie bauen lässt; hier, wie man sie in etwas Laufendes einbaut.

Im nächsten Beitrag: Schritt 3 — die Rebbergverwaltung, die Daten aus dem Rebberg auswerten und den Rebberg als Ganzes wieder sichtbar machen soll. Der eigentliche Grund für die ganze Übung.
