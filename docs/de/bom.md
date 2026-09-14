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

Das Brett muss in Faserrichtung mindestens so lang sein wie die abgewickelte
Außenkante über diese drei Teile:

> **L_min = 2 × Außenhöhe + Außenbreite + Sägezugabe**

- **Brettbreite (quer zur Faser)** muss mindestens der **Produkttiefe**
  entsprechen: B_min = Tiefe + Besäumung.
- **Aufrunden:** L_min und B_min für den Einkauf auf das nächste
  100-mm-Maß aufrunden.

Für diese Variante:

| Größe | Wert |
| --- | --- |
| Außenhöhe | FIXME mm |
| Außenbreite | FIXME mm |
| Tiefe | FIXME mm |
| Sägezugabe (gesamt) | FIXME mm |
| **L_min (Faserrichtung)** | **FIXME mm** |
| **B_min (Brettbreite)** | **FIXME mm** |

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
