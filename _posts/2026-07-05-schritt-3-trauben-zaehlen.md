---
layout: post
title: "KI 3, jetzt erst recht: Trauben zählen"
date: 2026-07-05
---

Schritt 1 war die [Webseite](/2026/05/15/schritt-1-website/), Schritt 2 die [Kellerverwaltung](/2026/06/28/schritt-2-kellerverwaltung/) — beide handlich, beide fertig. Schritt 3 ist der Rebberg selbst, und der ist eine andere Nummer.

Der Wunsch am Anfang war einfach: die KI soll uns den Rebberg Stock für Stock zeigen. Wir filmen jede Rebzeile mit dem Telefon, laden das Video hoch, die Auswertung sagt uns, wie es um jeden einzelnen Stock steht. Aus Video statt aus Handarbeit.

Was wir dabei wollen:

* jeden Stock einzeln erfassen, nicht nur die Zeile im Schnitt
* vergleichen — Stock mit Stock, Zeile mit Zeile, Parzelle mit Parzelle
* über die Saison verfolgen, vom Austrieb bis zur Lese

Am Anfang wollten wir ein Rebinventar bauen: welcher Stock wo steht, welcher fehlt, welcher noch jung ist. Dies sollte die KI aus dem Video lesen. Die zur Verfügung stehenden Modelle konnten dies nicht leisten, also nahmen wir die Zeilen von Hand auf, Stock für Stock. Dieser Handbestand ist heute der Untergrund der Karte weiter unten.

Der nächste Versuch blieb vage: die KI sollte das Wachstumsstadium jedes Stocks bestimmen — wie weit der Austrieb, wie weit die Reife. Dafür haben wir Gemini verwendet und die Videos selber in Einzelbilder aufgestückelt zur Analyse. Die Resultate waren... ok. Besser gesagt: plausibel. Aber wenig aussagekräftig und möglicherweise fehlerbehaftet.

Mit dem Fortschreiten des Rebjahres ergaben sich andere interessante Fragen: wie viele Trauben hängen an jedem Stock, und wie gross sind sie? Ausserdem hatten wir neue Modelle zur Verfügung, die Objekte besser über die Frames tracken können.

Auch dieser Anlauf stolperte zuerst. Das erste Modell warf alle Trauben in eine einzige Maske — es sah zwar das Grün, zählte aber nichts. Das nächste, das jede Traube einzeln verfolgt, lief bei einer ganzen Rebzeile aus dem Speicher, selbst auf der grössten Grafikkarte, die wir mieten konnten. Erst als wir das Video in kurze Stücke zerlegten und Stück für Stück durchschickten, lief es sauber durch.

Was jetzt läuft: [SAM 3](https://github.com/facebookresearch/sam3), ein Modell von Meta, gemietet über Replicate. Es erkennt jede Traube einzeln und verfolgt sie durchs Video — jede bekommt ihre eigene Farbe:

<img src="{{ '/assets/rebberg-trauben-overlay.jpg' | relative_url }}" alt="Rebzeile mit Trauben, jede Traube von der KI in einer eigenen Farbe markiert" style="display:block;margin:1.5rem auto;max-width:100%;width:600px">

*Zeile 6, Häusler Offenburg: die KI legt über jede Traube eine eigene Maske. Diese Zeile haben wir vor der Blüte entblättert — die Trauben hängen frei.*

Aus 19 Videos — zehn Zeilen [Häusler Offenburg](https://github.com/github-rha/rebbergverwaltung), neun Zeilen Schaffner Offenburg — wird so eine Karte. Dunkler heisst mehr Trauben:

<img src="{{ '/assets/rebberg-trauben-heatmap.svg' | relative_url }}" alt="Heatmap des Traubenbehangs, jede Zelle ein Rebstock, dunkler gleich mehr Trauben" style="display:block;margin:1.5rem auto;max-width:100%">

*Jede Zelle ein Stock, jede Spalte eine Rebzeile in ihrer wahren Länge — Zeile 1 rechts bis 19 links, Nord oben. Der Untergrund ist unser Rebkataster: graue und grüne Zellen sind leere, tote oder junge Stöcke. Die Farbe der Trauben liegt vorerst entlang der Zeile, noch nicht auf den einzelnen Stock genau.*

Was wir sehen:

* Beide Zweigelt-Parzellen tragen praktisch gleich viel — rund sieben sichtbare Trauben pro Stock, Häusler wie Schaffner.
* Der Diolinoir trägt weniger, dafür grössere Trauben als der Zweigelt.
* Zeile 6, die entblätterte, hebt sich nicht ab — weder mehr noch weniger, weder grösser noch kleiner als ihre Nachbarn. Die Entblätterung hinterlässt im Bild keine Spur.

Ehrlich bleiben muss man bei den Zahlen. Wir filmen eine Seite, in einem Durchgang; was hinter dem Laub oder auf der Rückseite hängt, sieht die Kamera nie. Die KI zählt also zu wenig — zum Vergleichen von Stock zu Stock reicht es, für den Ertrag in Kilo noch nicht. Und die Grösse steckt vorerst in Pixeln, nicht in Gramm: ohne Massstab im Bild wissen wir nicht, ob eine Zeile grössere Trauben trägt oder nur näher gefilmt wurde.

Die nächsten Schritte liegen damit auf der Hand:

* pro Stock statt pro Zeile — die Trauben den einzelnen Stöcken zuordnen
* einen Massstab ins Bild, damit aus Pixeln Zentimeter werden
* der nächste Durchgang, wenn sich die Trauben färben

Dann zählt die KI nicht mehr nur, sie misst mit — Traube für Traube, über die ganze Saison.
