<!--
  ERZEUGT aus docs/de/parametrisch/bom.tpl.md – NICHT von Hand ändern.
  Diese Datei zeigt die Referenzvariante (heimeliq.toml -> [variants] ->
  reference). Struktur- oder Textänderungen gehören in die Vorlage; die
  Zahlen setzt der Generator aus den Variantenparametern ein.
  Solange keine Referenzvariante ausgerechnet ist, stehen hier FIXME.
-->
# Stückliste – FIXME Produktname

*Variante: FIXME. Lesbare Stückliste für Menschen. Die maschinenlesbare
Variante ergibt sich aus den `[[part]]`-Einträgen in `okh.toml` (eigene
Teile) und den `[[external_parts]]`-Einträgen in `heimeliq.toml` (Drittteile).*

## Eigene Bauteile (Self)

*Maße als Zuschnitt: **L × B × S** (Länge × Breite × Stärke). Die Stärke (S)
steht immer zuletzt – unabhängig von der Einbaulage –, damit gleich starke
Bretter direkt vergleichbar sind.*

| ID | Bezeichnung | Material | Maße (L × B × S, mm) | Anzahl |
| --- | --- | --- | --- | --- |
| A001.S001 | FIXME | FIXME | FIXME × FIXME × FIXME | FIXME |
| A001.S002 | FIXME | FIXME | FIXME × FIXME × FIXME | FIXME |

## Externe Teile (Extern)

| ID | Bezeichnung | Norm/Hersteller | Maße | Anzahl |
| --- | --- | --- | --- | --- |
| A001.E001 | FIXME | FIXME | FIXME | FIXME |

## Hinweis zur Holzauswahl

### Mindestkantenlänge (in Faserrichtung)

Welche Teile aus **einem** Brett kommen müssen, steht in der `INSTRUCTIONS.md`
unter *Durchgehende Maserung*. Das Brett muss in Faserrichtung mindestens so
lang sein wie diese Teile hintereinander, plus Sägezugabe je Schnitt:

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
| Betroffene Teile | FIXME |
| Rechnung L_min | FIXME |
| Sägezugabe (FIXME Schnitte à FIXME mm) | FIXME mm |
| Besäumung (Brettbreite) | FIXME mm |
| **L_min (Faserrichtung)** | **FIXME mm** |
| **B_min (Brettbreite)** | **FIXME mm** |

*Sägezugabe und Besäumung sind Richtwerte (4 mm je Schnitt, wie in
`instructions/helpers/zuschnitt.py`) — mit der tatsächlichen Maschine prüfen.
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
