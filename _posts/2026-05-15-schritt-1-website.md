---
layout: post
title: "KI Fingerübung, Schritt 1: haeusler-wein.ch"
date: 2026-05-15
---

Vom Rebberg in die Flasche und aus dem Keller in den Verkauf — ohne diesen letzten Schritt geht es nicht. Mit der Übernahme des Rebbergs stehen wir auch vor der Aufgabe, neue Kundenkreise zu erschliessen. Was bisher fehlte, war eine Webseite, auf die man verweisen kann. Genau das ist [haeusler-wein.ch](https://haeusler-wein.ch).

Im [letzten Beitrag](/2026/05/08/willkommen/) haben wir den Dreisprung skizziert, mit dem wir uns das Rüstzeug für KI-gestützte Rebbergarbeit verschaffen. Schritt 1 war: die Webseite von der KI bauen lassen. Sozusagen eine kleine Fingerübung. Wir lernen, was solche Werkzeuge leisten, wo sie scheitern und wie unser Workflow mit ihnen aussieht, bevor wir sie auf wertvollere Daten loslassen.

Die selbstgegebene Vorgabe war eng:

* kein [WordPress](https://wordpress.com), kein [Duda](https://www.duda.co), kein [Wix](https://www.wix.com) — keine Plugin Updates, tiefe Kosten.
* statisches HTML. Ziel: Sicherheitsrisiken minimieren
* die KI baut, wir bestimmen Inhalt und Form.

Erster Anlauf, letztes Jahr, mit [Windsurf](https://windsurf.com). Das Ergebnis war... joah — eine statische HTML-Seite, lauffähig, schlicht. Das Vorgehen war naiv, Anweisungen geben, Resultate prüfen. Der Editor hatte die Tendenz, falsch abzubiegen und sich zu verirren.

Anfang Jahr dann neuer Anlauf mit Claude Code, Opus 4.5 und mehr System.

«Mehr System» heisst: drei kurze Dokumente im Repo — [`vision.md`](https://github.com/github-rha/haeusler-wein/blob/main/docs/vision.md), [`architecture.md`](https://github.com/github-rha/haeusler-wein/blob/main/docs/architecture.md), [`operations.md`](https://github.com/github-rha/haeusler-wein/blob/main/docs/operations.md). Mit der KI diskutiert, von der KI generiert, von uns justiert. Beispiel: 

> # Vision — haeusler-wein.ch
> 
> ## Overview
> The website for the Häusler family vineyard (haeusler-wein.ch). A small one-page presence that introduces the winery, lists the current wines with prices, and points visitors at an email address to order or get in touch.

Gleichzeitig haben wir den Stack gewechselt:

* **GitHub Pages** für das Hosting — kostenlos, statisch, automatischer Deploy bei jedem Commit.
* **Jekyll** als Generator — HTML aus Markdown und Liquid-Templates, ohne Server, ohne Datenbank.
* **Inhalt in YAML** (`_data/content.yml`) — Texte und Strukturen liegen sauber neben dem Code, lesbar auch ohne IDE.

Die Trennung Inhalt/Template macht künftige Änderungen mühelos: ein Satz im YAML reicht, GitHub Pages baut den Rest.

![Einfacher Guyot-Schnitt im Rebberg «Auf Offenburg», Mai 2026]({{ "/assets/rebberg-offenburg-guyot-schnitt.jpeg" | relative_url }})

*Im Rebberg, Mai 2026: ein einfacher Guyot-Schnitt mit einem Strecker und einer Reserve. Der Strecker ist ein Trieb vom letzten Jahr, gebogen und am Draht festgemacht; aus ihm und aus der Reserve schiessen die neuen Triebe. Im nächsten Schritt — beim **Erlesen** — werden sie ausgedünnt, bis eine überschaubare Anzahl ähnlich kräftiger Triebe stehen bleibt.*

Was heute auf haeusler-wein.ch steht: kurze Geschichte, Hinweis auf den Wein, Kontakt, Verlinkung zu diesem Blog. Mehr braucht es vorerst nicht.

Im nächsten Beitrag: KI Liegestütze, Schritt 2 — die Kellerverwaltungs-App, mit der wir unseren Weinkeller inventarisieren.
