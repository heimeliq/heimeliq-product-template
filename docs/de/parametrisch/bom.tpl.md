<!--
  Vorlage für docs/de/bom.md. Aus dieser Datei wird die Stückliste der
  Referenzvariante erzeugt.

  Regeln:
  - Platzhalter ausschließlich als {{ name }}. Keine Logik – keine Schleifen,
    keine Bedingungen, keine Rechenausdrücke.
  - Abgeleitete Maße (Zuschnittlängen, Mindestbrettlänge) werden nicht hier
    gerechnet, sondern als fertiger benannter Wert eingesetzt. Wie der Wert
    entsteht, ist Sache des Generators. Dasselbe gilt für Stückzahlen: in
    heimeliq.toml stehen nur die freien Eingangswerte, alles Abgeleitete
    rechnet der Generator.
  - {{ … }} füllt der Generator aus den Variantenparametern und daraus
    abgeleiteten Werten. FIXME füllt ein Mensch (Prosa, Materialangaben).
-->
# Stückliste – {{ product_name }}

*Variante: {{ variant_label }}. Lesbare Stückliste für Menschen. Die
maschinenlesbare Variante ergibt sich aus den `[[part]]`-Einträgen in
`okh.toml` (eigene Teile) und den `[[external_parts]]`-Einträgen in
`heimeliq.toml` (Drittteile).*

## Eigene Bauteile (Self)

*Maße als Zuschnitt: **L × B × S** (Länge × Breite × Stärke). Die Stärke (S)
steht immer zuletzt – unabhängig von der Einbaulage –, damit gleich starke
Bretter direkt vergleichbar sind.*

| ID | Bezeichnung | Material | Maße (L × B × S, mm) | Anzahl |
| --- | --- | --- | --- | --- |
| A001.S001 | FIXME | FIXME | {{ s001_length }} × {{ s001_width }} × {{ s001_thickness }} | {{ s001_quantity }} |
| A001.S002 | FIXME | FIXME | {{ s002_length }} × {{ s002_width }} × {{ s002_thickness }} | {{ s002_quantity }} |

## Externe Teile (Extern)

| ID | Bezeichnung | Norm/Hersteller | Maße | Anzahl |
| --- | --- | --- | --- | --- |
| A001.E001 | FIXME | FIXME | FIXME | {{ e001_quantity }} |

## Masse

| Größe | Wert |
| --- | --- |
| **Masse (gesamt)** | **{{ mass }} g** |

*Gerechnet, nicht gewogen: Volumen je Bauteil aus dem Modell
(FreeCAD `Shape.Volume`) × Rohdichte des Materials, plus die Kleinteile.
Aufgerundet. Dieselbe Zahl steht als `mass` in der `okh.toml` und in der
Datentabelle der `README.md` — hier steht, wie sie zustande kam.*

FIXME: Rechnung ausschreiben, z. B. „2,912 dm³ Eiche (Zargen und Boden) plus
0,008 dm³ für 8 Runddübel, zusammen 2,920 dm³ × 700 kg/m³ = 2044 g".

## Hinweis zur Holzauswahl

### Mindestkantenlänge (in Faserrichtung)

Manche Teile müssen aus **einem** Brett kommen, damit die Maserung
durchläuft. Welche das sind, steht unten in der Tabelle unter *Betroffene
Teile*. Das Brett muss in Faserrichtung mindestens so lang sein wie diese
Teile hintereinander, plus Sägezugabe je Schnitt:

> **L_min = Summe der benannten Teile + Sägezugabe**

Welche Summe das ist, entscheidet das Produkt — die Rechnung gehört hier
ausgeschrieben, nicht die allgemeine Formel. Zwei Beispiele:

- *Betrifft: Zargen* an einem vierseitigen Gehrungsrahmen →
  `2 × Außenbreite + 2 × Tiefe + Sägezugabe`
  (Front und hinten sind so lang wie die Außenbreite, beide Seitenzargen so
  lang wie die Tiefe — die Gehrung schneidet auf das Außenmaß.)
- *Betrifft: Seiten und Front* an einer U-Form →
  `2 × Außenhöhe + Außenbreite + Sägezugabe`

Dazu gehört:

- **Brettbreite (quer zur Faser)**: das größte Quermaß der benannten Teile,
  zzgl. Besäumung.
- **Aufrunden:** L_min und B_min für den Einkauf auf das nächste 100-mm-Maß.
- **Was nicht dazugehört, ausdrücklich nennen.** Ein Boden oder eine Rückwand
  ist eine eigene Platte und nicht Teil der durchgehenden Maserung.

Für diese Variante:

| Größe | Wert |
| --- | --- |
| Betroffene Teile | {{ grain_parts }} |
| Rechnung L_min | {{ grain_formula }} |
| Sägezugabe (gesamt) | {{ saw_allowance }} mm |
| Besäumung (Brettbreite) | {{ trim_allowance }} mm |
| **L_min (Faserrichtung)** | **{{ board_length_min }} mm** |
| **B_min (Brettbreite)** | **{{ board_width_min }} mm** |

*Sägezugabe und Besäumung sind Richtwerte (4 mm je Schnitt) — mit der
tatsächlichen Maschine prüfen.
Die Rohwerte vor dem Aufrunden mit angeben, damit die Rechnung nachvollziehbar
bleibt.*

### Welche Platte es wird

Steht hier bewusst nicht. Welche Formate lieferbar sind und was sie kosten,
ändert sich laufend und ist vom Anbieter abhängig — eine Tabelle mit
angenommenen Maßen wäre falsch, sobald sie geschrieben ist.

`L_min` und `B_min` oben sind die Bedingung: die Platte muss in Faserrichtung
mindestens `L_min` lang und quer dazu mindestens `B_min` breit sein. Womit sie
erfüllt wird, entscheidet der Zuschnitt anhand der Angebote, die zum Zeitpunkt
des Einkaufs gelten.

Reicht keine angebotene Länge, werden zwei Bretter mit **bewusst gesetztem**
Maserungs-Übergang eingeplant — die Fuge liegt dann dort, wo sie gestalterisch
verantwortbar ist, nicht dort, wo das Material zufällig endet.
