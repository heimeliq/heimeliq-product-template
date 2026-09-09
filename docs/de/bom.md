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

### Plattengrößen-Vergleich und Verschnitt

Gängige Leimholz-/Massivholzplatten gegen den Bedarf prüfen (Maße und
Verfügbarkeit sind anbieterabhängig – vor dem Kauf bestätigen). „Reicht?"
heißt: Plattenlänge ≥ L_min **und** Plattenbreite ≥ B_min.

| Plattenmaß (L × B, mm) | Stärke (mm) | Reicht? | Verschnitt Länge (mm) | Bemerkung |
| --- | --- | --- | --- | --- |
| 2000 × FIXME | FIXME | FIXME | FIXME | FIXME |
| 2600 × FIXME | FIXME | FIXME | FIXME | FIXME |
| 3000 × FIXME | FIXME | FIXME | FIXME | FIXME |

FIXME: gewählte Platte(n) und kalkulierten Gesamt-Verschnitt eintragen.
Reicht keine Standardlänge, zwei Bretter mit bewusst gesetztem
Maserungs-Übergang einplanen.
