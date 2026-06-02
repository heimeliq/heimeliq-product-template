# Stückliste – FIXME Möbelname

*Lesbare Stückliste für Menschen. Die maschinenlesbare Variante ergibt sich aus den `[[part]]`-Einträgen in `okh.toml` (eigene Teile) und den `[[external_parts]]`-Einträgen in `heimeliq.toml` (Drittteile).*

## Eigene Bauteile (Self)

*Maße als Zuschnitt: **L × B × S** (Länge × Breite × Stärke). Die Stärke (S) steht immer zuletzt – unabhängig davon, ob das Bauteil im Möbel senkrecht oder waagerecht sitzt –, damit gleich starke Bretter direkt vergleichbar sind.*

| ID | Bezeichnung | Material | Maße (L × B × S, mm) | Anzahl |
| --- | --- | --- | --- | --- |
| S001 | FIXME | FIXME | FIXME | FIXME |

## Externe Teile (Extern)

| ID | Bezeichnung | Norm/Hersteller | Maße | Anzahl |
| --- | --- | --- | --- | --- |
| E001 | FIXME | FIXME | FIXME | FIXME |

## Hinweis zur Holzauswahl

### Durchgehende Maserung (gehriq-Prinzip)

Bei gehriq-Möbeln sollen mindestens die **beiden Seitenteile und der Deckel** aus **einem** Brett kommen. Die drei Teile werden in Reihe – Seitenteil links → Deckel → Seitenteil rechts – aus einem langen Brett gesägt und an den Gehrungs-Ecken (45°) gestoßen. So läuft die Maserung über die Ecken durch und das Möbel wirkt wie aus einem Stück. Der Boden (und optional die Rückwand) darf aus separatem Material kommen.

### Mindestkantenlänge (in Faserrichtung)

Das Brett muss in Faserrichtung mindestens so lang sein wie die abgewickelte Außenkante über diese drei Teile:

> **L_min = Höhe Seitenteil links + Breite Deckel + Höhe Seitenteil rechts + Sägezugabe**
> = **2 × Außenhöhe + Außenbreite + Sägezugabe**

- **Außenhöhe / Außenbreite** = Außenmaße des Möbels (siehe README / `okh.toml` → `outer-dimensions`).
- **Sägezugabe** = Schnittfugen + Endbesäumung; FIXME mm je Trennschnitt, plus Besäumung beider Enden (grob FIXME mm gesamt).
- **Brettbreite (quer zur Faser)** muss mindestens der **Möbeltiefe** entsprechen: B_min = Tiefe + Besäumung.
- **Aufrunden:** L_min und B_min für den Einkauf auf das nächste **10-cm-Maß (100 mm)** aufrunden – Platten werden i. d. R. in 10-cm-Schritten angeboten.

Für dieses Möbel:

| Größe | Wert |
| --- | --- |
| Außenhöhe | FIXME mm |
| Außenbreite | FIXME mm |
| Tiefe | FIXME mm |
| **L_min (Faserrichtung)** | **FIXME mm** (= 2 × FIXME + FIXME + Sägezugabe, auf 10 cm aufgerundet) |
| **B_min (Brettbreite)** | **FIXME mm** (auf 10 cm aufgerundet) |

### Plattengrößen-Vergleich und Verschnitt

Gängige Leimholz-/Massivholzplatten gegen den Bedarf prüfen (Maße & Verfügbarkeit sind anbieterabhängig – Beispielwerte, vor dem Kauf bestätigen). „Reicht?" heißt: Plattenlänge ≥ L_min **und** Plattenbreite ≥ B_min.

| Plattenmaß (L × B, mm) | Stärke (mm) | Reicht für L_min × B_min? | Verschnitt Länge (mm) | Bemerkung |
| --- | --- | --- | --- | --- |
| 2000 × FIXME | FIXME | FIXME | FIXME | FIXME |
| 2600 × FIXME | FIXME | FIXME | FIXME | FIXME |
| 3000 × FIXME | FIXME | FIXME | FIXME | FIXME |
| 4000 × FIXME | FIXME | FIXME | FIXME | empf. Wahl? FIXME |

FIXME: gewählte Platte(n) und kalkulierter Gesamt-Verschnitt (Länge × Breite) eintragen. Reicht keine Standardlänge, zwei Bretter mit bewusst gesetztem Maserungs-Übergang einplanen.
