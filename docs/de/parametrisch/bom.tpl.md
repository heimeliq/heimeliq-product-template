<!--
  Vorlage für docs/de/bom.md. Aus dieser Datei wird die Stückliste der
  Referenzvariante erzeugt.

  Regeln:
  - Platzhalter ausschließlich als {{ name }}. Keine Logik – keine Schleifen,
    keine Bedingungen, keine Rechenausdrücke.
  - Abgeleitete Maße (Zuschnittlängen, Mindestbrettlänge) werden nicht hier
    gerechnet, sondern als fertiger benannter Wert eingesetzt. Wie der Wert
    entsteht, ist Sache des Generators.
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

## Hinweis zur Holzauswahl

### Mindestkantenlänge (in Faserrichtung)

Das Brett muss in Faserrichtung mindestens so lang sein wie die abgewickelte
Außenkante über diese drei Teile:

> **L_min = 2 × Außenhöhe + Außenbreite + Sägezugabe**

- **Brettbreite (quer zur Faser)** muss mindestens der **Produkttiefe**
  entsprechen.
- **Aufrunden:** L_min und B_min für den Einkauf auf das nächste 100-mm-Maß.

Für diese Variante:

| Größe | Wert |
| --- | --- |
| Außenhöhe | {{ outer_height }} mm |
| Außenbreite | {{ outer_width }} mm |
| Tiefe | {{ outer_depth }} mm |
| Sägezugabe (gesamt) | {{ saw_allowance }} mm |
| **L_min (Faserrichtung)** | **{{ board_length_min }} mm** |
| **B_min (Brettbreite)** | **{{ board_width_min }} mm** |

### Plattengrößen-Vergleich und Verschnitt

Gängige Leimholz-/Massivholzplatten gegen den Bedarf prüfen (Maße und
Verfügbarkeit sind anbieterabhängig – vor dem Kauf bestätigen). „Reicht?"
heißt: Plattenlänge ≥ L_min **und** Plattenbreite ≥ B_min.

| Plattenmaß (L × B, mm) | Stärke (mm) | Reicht? | Verschnitt Länge (mm) | Bemerkung |
| --- | --- | --- | --- | --- |
| 2000 × {{ plate_a_width }} | {{ plate_a_thickness }} | {{ plate_a_fits }} | {{ plate_a_waste_length }} | FIXME |
| 2600 × {{ plate_b_width }} | {{ plate_b_thickness }} | {{ plate_b_fits }} | {{ plate_b_waste_length }} | FIXME |
| 3000 × {{ plate_c_width }} | {{ plate_c_thickness }} | {{ plate_c_fits }} | {{ plate_c_waste_length }} | FIXME |

FIXME: gewählte Platte(n) und kalkulierten Gesamt-Verschnitt eintragen.
Reicht keine Standardlänge, zwei Bretter mit bewusst gesetztem
Maserungs-Übergang einplanen.
