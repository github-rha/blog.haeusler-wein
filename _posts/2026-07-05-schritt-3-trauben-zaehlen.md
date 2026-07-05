---
layout: post
title: "KI 3, jetzt erst recht: Trauben zählen"
date: 2026-07-05
---

Schritt 1 war die [Webseite](/2026/05/15/schritt-1-website/), Schritt 2 die [Kellerverwaltung](/2026/06/28/schritt-2-kellerverwaltung/) — beide handlich, beide fertig. Schritt 3 ist der Rebberg selbst.

 Nach erfolglosen Versuchen, ein Inventar aus Videoaufnahmen der Rebzeilen zu erstellen (wir haben es dann manuell gemacht) und mässigen Versuchen, das Pflanzenstadium zu tracken, kommt jetzt eine neue spannende Aufgabestellung.

Wir filmen jede Rebzeile mit dem Telefon und lassen die KI die Trauben zählen, Stock für Stock. Dahinter steckt [SAM 3](https://github.com/facebookresearch/sam3), ein Modell von Meta, gemietet über Replicate: es erkennt jede Traube einzeln und verfolgt sie durchs Video, jede bekommt ihre eigene Farbe.

<img src="{{ '/assets/rebberg-trauben-overlay.jpg' | relative_url }}" alt="Rebzeile mit Trauben, jede Traube von der KI in einer eigenen Farbe markiert" style="display:block;margin:1.5rem auto;max-width:100%;width:600px">

*Zeile 6, Häusler Offenburg: die KI legt über jede Traube eine eigene Maske. Diese Zeile haben wir vor der Blüte entblättert — die Trauben hängen frei.*

Aus 19 Videos — zehn Zeilen Häusler Offenburg, neun Zeilen Schaffner Offenburg (unsere Nachbarparzelle) — wird eine Karte. Dunkler heisst mehr Trauben:

<img src="{{ '/assets/rebberg-trauben-heatmap.svg' | relative_url }}" alt="Heatmap des Traubenbehangs, jede Zelle ein Rebstock, dunkler gleich mehr Trauben" style="display:block;margin:1.5rem auto;max-width:100%">

*Jede Zelle ein Stock, jede Spalte eine Rebzeile in ihrer wahren Länge Zeile 1 rechts bis 19 links, Nord oben. Graue und grüne Zellen sind leere, tote oder junge Stöcke.*

Was wir sehen:

* Beide Zweigelt-Parzellen tragen praktisch gleich viel — rund sieben sichtbare Trauben pro Stock, Häusler wie Schaffner.
* Der Diolinoir trägt weniger, dafür grössere Trauben als der Zweigelt.
* Zeile 6, die entblätterte, hebt sich nicht ab. Die Entblätterung hinterlässt im Bild keine Spur.

Ehrlich bleiben muss man bei den Zahlen: wir filmen eine Seite, in einem Durchgang. Was hinter dem Laub oder auf der Rückseite hängt, sieht die Kamera nie — die KI zählt also zu wenig. Zum Vergleichen von Stock zu Stock reicht es, für den Ertrag in Kilo noch nicht.

Als Nächstes ordnen wir die Trauben den einzelnen Stöcken zu und bringen einen Massstab ins Bild, damit aus Pixeln Zentimeter werden: dann zählt die KI nicht mehr nur, sie misst mit.
