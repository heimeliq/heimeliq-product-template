# heimeliq Furniture Template

Vorlage zur Erstellung neuer Möbel-Repositories für das [heimeliq](https://heimeliq.de)-Projekt.

Jedes Möbel von heimeliq lebt in einem eigenen Git-Repository. Diese Vorlage definiert die einheitliche Struktur, die alle Möbel-Repos verwenden, und stellt sicher, dass jedes Repo dem [Open Know-How (OKH) Standard](https://github.com/iop-alliance/OpenKnowHow) entspricht.

## Versionen

| Komponente | Version |
| --- | --- |
| OKH-Manifest | `2.4` |
| Lizenz dieses Templates | `MIT` |
| Lizenz daraus erzeugter Möbel-Repos | `CERN-OHL-S-2.0` |

Die Template-Version wird in jedem aus dieser Vorlage erzeugten Möbel-Repo in der `heimeliq.toml` festgehalten (`heimeliq-template-version`). Damit ist nachvollziehbar, auf welchem Vorlagen-Stand das Möbel-Repo basiert.

## Zwei Lizenzen, zwei Welten

Diese Vorlage trennt bewusst zwei Lizenzen:

- **Das Template selbst** (Struktur, Schemas, Workflow-Dateien, Beispiel-Markdown-Vorlagen) steht unter **MIT**. Andere können daraus eigene Hardware-Doku-Templates ableiten – auch ohne Bezug zu heimeliq.
- **Möbel-Repos**, die aus dieser Vorlage erzeugt werden, stehen unter **CERN-OHL-S-2.0** (strongly reciprocal Open Hardware Licence). Wer ein Möbel weiterentwickelt, muss die Weiterentwicklung wieder offen unter derselben Lizenz teilen.

Konkret heißt das im Repo:

| Datei im Template | Wird im Möbel-Repo zu | Lizenz |
| --- | --- | --- |
| `LICENSE` | _entfällt_ | MIT (gilt nur fürs Template) |
| `LICENSE.example` | `LICENSE` | CERN-OHL-S-2.0 |
| `README.md` | _entfällt_ | MIT (diese Datei hier) |
| `README.example.md` | `README.md` | CERN-OHL-S-2.0 |

## Was ist heimeliq?

heimeliq baut Möbel aus regionalen Naturmaterialien – Massivholz, Stahl, Sperrholz – und veröffentlicht jedes Stück vollständig als Open Source: 3D-Modelle, Stücklisten, Bauanleitungen. Diese Vorlage ist Teil der digitalen Infrastruktur dahinter.

heimeliq-Möbel sind organisiert in **Reihen**:

- **MassiQ** – Massivmöbel
- **WorkaholiQ** – Betriebs- und Werkstattmöbel
- **KeiliQ** – French Cleat und Keilsysteme

Jedes Möbel gehört zu genau einer Reihe.

## Ein neues Möbel-Repo aus dieser Vorlage erzeugen

1. Auf GitHub den Knopf **„Use this template"** → **„Create a new repository"** klicken.
2. Repo-Name nach Schema: `heimeliq-<reihe>-<waldname>`, zum Beispiel `heimeliq-massiq-hambach`.
3. Repo lokal klonen.
4. **Lizenz umstellen**: `LICENSE` löschen, `LICENSE.example` zu `LICENSE` umbenennen.
5. **README umstellen**: `README.md` löschen, `README.example.md` zu `README.md` umbenennen.
5. **CHANGELOG umstellen**: `CHANGELOG.md` löschen, `changelog.md` zu `CHANGELOG.md` umbenennen.
5. **MIGRATIONS löschen**: `MIGRATIONS.md` löschen.
6. Platzhalter ersetzen (siehe nächster Abschnitt).
7. Erste Inhalte ergänzen, committen, pushen.
8. Wenn das Möbel auf der Website erscheinen soll: im `heimeliq-website`-Repo den Eintrag in `furniture-repos.json` ergänzen.

> Tipp: Die Schritte 4–6 werden später vom angedachten `heimeliq-cli` automatisiert (`heimeliq init`). Bis dahin manuell.

## Platzhalter ersetzen

Alle Stellen, die noch ausgefüllt werden müssen, sind mit `FIXME` markiert. Die GitHub-Action `validate.yml` bricht ab, solange noch ein `FIXME` im Repo ist UND der Status auf `published` steht – damit kann kein halbfertiges Repo unbemerkt veröffentlicht werden.

Mindestens zu ersetzen:

- In `okh.toml`: `name`, `repo`, `function`, `licensor`, `image`-Pfade.
- In `heimeliq.toml`: `series`, `type`, `slug`.
- In `LICENSE` (nach Umbenennung aus `LICENSE.example`): Copyright-Zeile.
- In `README.md` (nach Umbenennung aus `README.example.md`): alle FIXMEs.
- `media/hero.jpg.placeholder` → eine echte `media/hero.jpg` legen.
- Inhalte in `docs/de/*.md` ausfüllen.

## Struktur

```
heimeliq-furniture-template/
├── README.md                  ← diese Datei (erklärt das Template, MIT)
├── README.example.md          ← wird im Möbel-Repo zu README.md (CERN-OHL-S)
├── LICENSE                    ← MIT (für das Template)
├── LICENSE.example            ← wird im Möbel-Repo zu LICENSE (CERN-OHL-S-2.0)
├── CHANGELOG.md               ← Versions-Historie dieser Vorlage
├── MIGRATIONS.md              ← Anleitung zum Migrieren älterer Möbel-Repos
├── REUSE.toml                 ← Datei-Lizenzangaben (reuse.software-konform)
├── okh.toml                   ← OKH-Manifest (Standard-Metadaten)
├── heimeliq.toml              ← heimeliq-spezifische Erweiterungen
├── heimeliq.schema.json       ← JSON-Schema für heimeliq.toml-Validierung
├── changelog.md               ← Versions-Historie des Möbels (klein!)
├── docs/de/
│   ├── story.md               ← Hintergrund, Inspiration, Material
│   ├── build-guide.md         ← Werkstatt-Bauanleitung (für Tischler)
│   ├── assembly.md            ← Endkunden-Montage (für Käufer)
│   ├── bom.md                 ← Lesbare Stückliste
│   ├── care.md                ← Pflegehinweise
│   └── *.images/              ← Bilder, die zur jeweiligen .md gehören
├── cad/
│   ├── source/                ← FreeCAD-Originaldateien (.FCStd)
│   ├── exports/               ← STEP, STL, GLB
│   └── drawings/              ← technische Zeichnungen (.pdf)
├── media/
│   ├── hero.jpg               ← Hauptbild (Pflicht)
│   ├── gallery/               ← weitere Bilder für Außenwirkung
│   └── process/               ← Bautagebuch, Prozessdokumentation
└── .github/workflows/
    └── validate.yml           ← Validiert okh.toml und heimeliq.toml bei jedem Push
```

## Welches Bild gehört wohin?

- `media/hero.jpg` – das eine Hauptbild für Shop und Suchergebnisse.
- `media/gallery/*` – weitere Außenwirkungs-Bilder (Studio-Fotos, Detailaufnahmen für Marketing).
- `media/process/*` – Bautagebuch: Fotos vom Baum, von der Werkstatt, vom Bauprozess.
- `docs/de/*.images/*` – Bilder, die direkt in einer Markdown-Datei eingebettet werden (z. B. Schrittfotos einer Verbindung).

Faustregel: **Außenwirkungs-Bilder zentral in `media/`, Doku-Bilder lokal neben ihrer Markdown-Datei.**

## ID-Konvention

| Ebene | Schema | Beispiel |
| --- | --- | --- |
| Möbel-Repo | `heimeliq-<reihe>-<waldname>` | `heimeliq-massiq-hambach` |
| Hauptbaugruppe | `A001` | `A001` |
| Sub-Baugruppe | `A002`, `A003`, … | `A002` (z. B. Schublade) |
| Eigenes Bauteil (Self) | `<Baugruppe>.S###` | `A001.S001`, `A002.S001` |
| Externes Bauteil | `<Baugruppe>.E###` | `A001.E001`, `A002.E001` |
| Möbel-Version | SemVer | `1.2.0` |

Bauteil-IDs sind innerhalb des jeweiligen Möbel-Repos eindeutig und immer voll qualifiziert mit Assembly-Präfix. Außerhalb adressiert man sie als `<repo>/<part-id>`.

Der Möbel-Typ (z. B. `sideboard`, `werkbank`) ist **kein** Teil der ID, sondern ein Metadatenfeld (`type`) in `heimeliq.toml`. Gleiches gilt für zusätzliche `tags`. Damit bleibt die ID schlank und die Klassifizierung filterbar.

## Wald-Konzept

Jedes heimeliq-Möbel trägt den Namen eines real existierenden Waldes. Der Waldname ist **möbel-eindeutig**: kein zweites Möbel trägt denselben Wald. Damit wird die Marke um eine inhaltliche Schicht erweitert – jedes Möbel verweist auf einen Ort, hat eine kleine Geschichte, und bei bedrohten Wäldern macht heimeliq deren Situation sichtbar.

Wald-Metadaten leben in der `[forest]`-Section der `heimeliq.toml`. Der Wald-Bereich auf der Produktseite wird beim Build daraus generiert. Es gibt **kein** separates Forest-Repository.

Beispiele für Waldnamen:
- Deutschland/DACH: `hambach`, `hainich`, `spessart`, `bayerischer-wald`, `pfaelzerwald`
- Europa: `bialowieza`, `sherwood`, `broceliande`
- Welt: `tongass`, `daintree`, `yakushima`, `atewa`

Die `id` im `[forest]`-Block muss URL-tauglich sein (lowercase, keine Umlaute) und mit dem letzten Segment des Repo-Namens übereinstimmen.

## Baugruppen-Konzept

Jedes heimeliq-Möbel ist als Hierarchie von Baugruppen modelliert:

- **`A001`** ist konventionell die **Hauptbaugruppe** = das ganze Möbel.
- Sub-Baugruppen (Schubladen, Türen, Erweiterungen) bekommen `A002`, `A003`, … und referenzieren ihre Eltern-Baugruppe über das Feld `parent`.
- Jedes Bauteil gehört zu genau einer Baugruppe und trägt deren Präfix in der ID (`A001.S001`, `A002.E001` usw.).
- `optional = true` markiert eine Baugruppe als Erweiterung. Solche Baugruppen werden später im Shop zu konfigurierbaren Varianten mit Aufpreis.

**Konvention für FreeCAD-Dateien**: Jede Baugruppe ist eine eigene `.FCStd`-Datei, benannt nach Schema `A001-<Name>.FCStd`, `A002-<Name>.FCStd`. Beispiel:

```
cad/source/
├── A001-Sideboard.FCStd
└── A002-Schublade.FCStd
```

Im OKH-`[[part]]`-Array zeigt das `source`-Feld jedes Bauteils auf die Assembly-Datei, in der das Bauteil definiert ist. Zusätzlich verlinkt das Feld `heimeliq-assembly` die Baugruppe explizit.

In der Praxis sind zwei Hierarchie-Ebenen (Möbel + direkte Erweiterungen) der Normalfall. Tieferes Nesting (z. B. `A002.A003.S001`) ist technisch erlaubt, aber selten nötig.

## Mitwirken

Verbesserungsvorschläge an diesem Template sind willkommen. Issues und Pull Requests direkt am Template-Repo. Änderungen am Template laufen über Versionierung (siehe `CHANGELOG.md`); bestehende Möbel-Repos werden dadurch nicht automatisch migriert.

## Lizenz

Dieses Template steht unter [MIT](LICENSE). Daraus erzeugte Möbel-Repos stehen unter [CERN-OHL-S-2.0](LICENSE.example).
