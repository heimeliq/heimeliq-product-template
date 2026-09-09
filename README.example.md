# FIXME Produktname

> FIXME ein- bis zweisätzige Beschreibung – was ist es, was macht es besonders.

[![Lizenz: CERN-OHL-S-2.0](https://img.shields.io/badge/Lizenz-CERN--OHL--S--2.0-blue)](LICENSE)
[![heimeliq](https://img.shields.io/badge/heimeliq-FIXME--familie-green)](https://heimeliq.de/produkte/FIXME-familie)
[![Status](https://img.shields.io/badge/Status-FIXME--status-orange)](#)

![Hauptbild](media/hero.jpg)

---

## Überblick

FIXME 2–4 Sätze: Welcher Typ, welche Familie? Welche Konstruktion? Welches Material? Für wen ist es gedacht?

Vollständige Hintergrundgeschichte und Materialherkunft: siehe [docs/de/story.md](docs/de/story.md).

---

## Typ und Familie

Dieses Produkt ist ein **FIXME Typ** und gehört zur Familie **FIXME Familie**.

FIXME 2–4 Sätze zur Familie: welche Formensprache, welches Verbindungsprinzip, was die Produkte dieser Familie verbindet.

Maschinenlesbar in [heimeliq.toml](heimeliq.toml) unter `type`, `theme` und `[family]`. Die konstruktiven Werte der Familie liegen zentral im Instructions-Repo unter `families/FIXME-familie/`.

---

## Gesamtmaße

*Maße der Referenzvariante (`[variants]` → `reference` in [heimeliq.toml](heimeliq.toml)). Baut das Produkt in mehreren Größen, sind die weiteren Varianten dort unter `[[variants.option]]` gelistet.*

| Eigenschaft | Maß |
| --- | --- |
| Breite | FIXME mm |
| Tiefe | FIXME mm |
| Höhe | FIXME mm |
| Materialstärke Korpus | FIXME mm |
| Materialstärke Einbauten | FIXME mm |
| Materialstärke Rückwand | FIXME mm |
| Masse (gesamt) | FIXME kg |

Maschinenlesbar in [okh.toml](okh.toml) unter `outer-dimensions` und `mass`.

---

## Material

| Element | Material | Herkunft |
| --- | --- | --- |
| Korpus | FIXME Massivholz-Art | FIXME regional |
| Einbauten | FIXME | FIXME |
| Rückwand | FIXME Sperrholz | FIXME |
| Verbinder | FIXME (z. B. Lamellos, Dübel) | – |
| Oberfläche | FIXME (z. B. Hartwachs-Öl) | – |

**Was nicht verwendet wird**: keine Spanplatten, keine synthetischen Leime, keine übermäßige Oberflächenbehandlung. Konsequent regional und naturbelassen.

---

## Stückliste

Vollständige Stückliste: siehe [docs/de/bom.md](docs/de/bom.md).
Maschinenlesbar in [okh.toml](okh.toml) (`[[part]]`) und [heimeliq.toml](heimeliq.toml) (`[[external_parts]]`).

### Eigene Bauteile (Self)

*Maße als Zuschnitt: **L × B × S** (Länge × Breite × Stärke). Die Stärke (S) steht immer zuletzt – unabhängig von der Einbaulage –, damit gleich starke Bretter vergleichbar bleiben.*

| ID | Bezeichnung | Maße (L × B × S, mm) | Anzahl |
| --- | --- | --- | --- |
| S001 | FIXME | FIXME | FIXME |
| S002 | FIXME | FIXME | FIXME |

### Externe Teile

| ID | Bezeichnung | Norm / Hersteller | Anzahl |
| --- | --- | --- | --- |
| E001 | FIXME | FIXME | FIXME |

---

## Konstruktionsdetails

FIXME: Zentrale konstruktive Merkmale, in 3–6 Stichpunkten oder Tabellen.

### Verbindungen

- **FIXME**: z. B. Korpus mit Gehrung verbunden
- **FIXME**: z. B. Zwischenwände gedübelt
- **FIXME**: Rückwand in umlaufender Nut

### Nuten und Aussparungen

| Eigenschaft | Maß |
| --- | --- |
| FIXME | FIXME |

Bauanleitung Schritt für Schritt: siehe [docs/de/build-guide.md](docs/de/build-guide.md).

---

## Aufbau zu Hause

Wenn du das Produkt von heimeliq in fertiger Form bekommst, hilft dir [docs/de/assembly.md](docs/de/assembly.md) bei der Montage.

---

## Pflege

Siehe [docs/de/care.md](docs/de/care.md).

---

## Dateien

### 3D-Modelle und Zeichnungen

- **FreeCAD-Quelle**: [`cad/source/`](cad/source/) (Originaldatei, frei bearbeitbar)
- **STEP**: [`cad/exports/`](cad/exports/) (neutraler Austausch, mit jedem CAD-System öffenbar)
- **STL**: [`cad/exports/`](cad/exports/) (für 3D-Druck und Vorschau)
- **GLB**: [`cad/exports/`](cad/exports/) (Web-3D-Viewer)
- **Technische Zeichnungen**: [`cad/drawings/`](cad/drawings/) (PDF)

### Software

- **FreeCAD** – Open Source, kostenlos – <https://www.freecad.org/>
- **Version** verwendet: FIXME (z. B. 1.0.x)

---

## Versionierung

Aktuelle Version: siehe `version` in [heimeliq.toml](heimeliq.toml).
Versionshistorie: [CHANGELOG.md](changelog.md).

Versionsschritte folgen [Semantic Versioning](https://semver.org/lang/de/):

- **MAJOR** – Konstruktion grundlegend geändert.
- **MINOR** – Neue Option (z. B. weitere Holzart) oder zusätzliche Detailzeichnung.
- **PATCH** – Tippfehler in Anleitung, besseres Foto, Klarstellung.

---

## Kaufen

Dieses Produkt kann auch fertig gebaut bei heimeliq bestellt werden: <https://heimeliq.de/produkte/FIXME-slug>

---

## Open Source / Selber bauen

Du darfst dieses Produkt nach den Plänen in diesem Repository **selbst bauen oder bauen lassen**, **modifizieren** und **weitergeben**. Die einzige Auflage: Wenn du Änderungen weitergibst, müssen sie wieder unter derselben Lizenz (CERN-OHL-S-2.0) verfügbar sein. Damit bleibt das Wissen frei.

Wenn du dieses Produkt gebaut hast – ob nach Original oder mit Änderungen – freue ich mich über ein Foto und eine Rückmeldung: FIXME@heimeliq.de.

---

## Lizenz

Dieses Produkt und seine Dokumentation stehen unter [CERN-OHL-S-2.0](LICENSE).

**Keine Gewährleistung für die Richtigkeit der Maße – vor dem Zuschnitt bitte nachmessen.**

---

## Verwandte Links

- heimeliq-Webseite: <https://heimeliq.de>
- Familie FIXME-familie: <https://heimeliq.de/produkte/FIXME-familie>
- Open Know-How Standard: <https://github.com/iop-alliance/OpenKnowHow>
- CERN Open Hardware Licence: <https://ohwr.org/cern_ohl_s_v2.txt>