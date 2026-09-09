# heimeliq Product Template

Vorlage zur Erstellung neuer Produkt-Repositories für das [heimeliq](https://heimeliq.de)-Projekt.

Jedes Holz-Möbel oder -Accessoire von heimeliq lebt in einem eigenen Git-Repository. Diese Vorlage definiert die einheitliche Struktur, die alle Produkt-Repos verwenden, und stellt sicher, dass jedes Repo dem [Open Know-How (OKH) Standard](https://github.com/iop-alliance/OpenKnowHow) entspricht.

## Versionen

| Komponente | Version |
| --- | --- |
| OKH-Manifest | `2.4` |
| Lizenz dieses Templates | `MIT` |
| Lizenz daraus erzeugter Produkt-Repos | `CERN-OHL-S-2.0` |

Die Template-Version wird in jedem aus dieser Vorlage erzeugten Produkt-Repo in der `heimeliq.toml` festgehalten (`heimeliq-template-version`). Damit ist nachvollziehbar, auf welchem Vorlagen-Stand das Produkt-Repo basiert.

## Zwei Lizenzen, zwei Welten

Diese Vorlage trennt bewusst zwei Lizenzen:

- **Das Template selbst** (Struktur, Schemas, Workflow-Dateien, Beispiel-Markdown-Vorlagen) steht unter **MIT**. Andere können daraus eigene Hardware-Doku-Templates ableiten – auch ohne Bezug zu heimeliq.
- **Produkt-Repos**, die aus dieser Vorlage erzeugt werden, stehen unter **CERN-OHL-S-2.0** (strongly reciprocal Open Hardware Licence). Wer ein Möbel weiterentwickelt, muss die Weiterentwicklung wieder offen unter derselben Lizenz teilen.

Konkret heißt das im Repo:

| Datei im Template | Wird im Produkt-Repo zu | Lizenz |
| --- | --- | --- |
| `LICENSE` | _entfällt_ | MIT (gilt nur fürs Template) |
| `LICENSE.example` | `LICENSE` | CERN-OHL-S-2.0 |
| `README.md` | _entfällt_ | MIT (diese Datei hier) |
| `README.example.md` | `README.md` | CERN-OHL-S-2.0 |

## Was ist heimeliq?

heimeliq baut Holz-Möbel oder -Accessoires aus regionalen Naturmaterialien – Massivholz, Stahl, Sperrholz – und veröffentlicht jedes Stück vollständig als Open Source: 3D-Modelle, Stücklisten, Bauanleitungen. Diese Vorlage ist Teil der digitalen Infrastruktur dahinter.

Jedes Produkt gehört zu einer **Familie** (eine Formensprache, die einen Vornamen trägt) und hat einen **Typ** (was es ist – `sideboard`, `tablett`, `werkbank`). Familie und Typ bilden in dieser Reihenfolge die Repo-ID. Details im Abschnitt [Familien-Konzept](#familien-konzept).

## Ein neues Produkt-Repo aus dieser Vorlage erzeugen

1. Auf GitHub den Knopf **„Use this template"** → **„Create a new repository"** klicken.
2. Repo-Name nach Schema: `<family>-<type>`, zum Beispiel `wieke-sideboard`.
3. Repo lokal klonen.
4. **Lizenz umstellen**: `LICENSE` löschen, `LICENSE.example` zu `LICENSE` umbenennen.
5. **README umstellen**: `README.md` löschen, `README.example.md` zu `README.md` umbenennen.
5. **CHANGELOG umstellen**: `CHANGELOG.md` löschen, `changelog.md` zu `CHANGELOG.md` umbenennen.
5. **MIGRATIONS löschen**: `MIGRATIONS.md` löschen.
6. Platzhalter ersetzen (siehe nächster Abschnitt).
7. Erste Inhalte ergänzen, committen, pushen.
8. Wenn das Produkt auf der Website erscheinen soll: im `heimeliq-website`-Repo den Eintrag in `product-repos.json` ergänzen.

> Tipp: Die Schritte 4–6 werden später vom angedachten `heimeliq-cli` automatisiert (`heimeliq init`). Bis dahin manuell.

## Platzhalter ersetzen

Alle Stellen, die noch ausgefüllt werden müssen, sind mit `FIXME` markiert. Die GitHub-Action `validate.yml` bricht ab, solange noch ein `FIXME` im Repo ist UND die Tag-Achse `status` den Wert `published` enthält – damit kann kein halbfertiges Repo unbemerkt veröffentlicht werden.

Mindestens zu ersetzen:

- In `okh.toml`: `name`, `repo`, `function`, `licensor`, `image`-Pfade.
- In `heimeliq.toml`: `type`, `theme`, `slug`, `[family]`, `[variants]`.
- In `LICENSE` (nach Umbenennung aus `LICENSE.example`): Copyright-Zeile.
- In `README.md` (nach Umbenennung aus `README.example.md`): alle FIXMEs.
- `media/hero.jpg.placeholder` → eine echte `media/hero.jpg` legen.
- Inhalte in `docs/de/*.md` ausfüllen.

## Struktur

```
heimeliq-product-template/
├── README.md                  ← diese Datei (erklärt das Template, MIT)
├── README.example.md          ← wird im Produkt-Repo zu README.md (CERN-OHL-S)
├── LICENSE                    ← MIT (für das Template)
├── LICENSE.example            ← wird im Produkt-Repo zu LICENSE (CERN-OHL-S-2.0)
├── CHANGELOG.md               ← Versions-Historie dieser Vorlage
├── MIGRATIONS.md              ← Anleitung zum Migrieren älterer Produkt-Repos
├── REUSE.toml                 ← Datei-Lizenzangaben (reuse.software-konform)
├── okh.toml                   ← OKH-Manifest (Standard-Metadaten)
├── heimeliq.toml              ← heimeliq-spezifische Erweiterungen
├── heimeliq.schema.json       ← JSON-Schema für heimeliq.toml-Validierung
├── changelog.md               ← Versions-Historie des Möbels (klein!)
├── docs/de/
│   ├── story.md               ← Hintergrund, Inspiration, Material
│   ├── build-guide.md         ← Werkstatt-Bauanleitung (Referenzvariante, erzeugt)
│   ├── assembly.md            ← Endkunden-Montage (für Käufer)
│   ├── bom.md                 ← Lesbare Stückliste (Referenzvariante, erzeugt)
│   ├── care.md                ← Pflegehinweise
│   ├── parametrisch/          ← Vorlagen mit {{ … }}, aus denen build-guide.md und bom.md entstehen
│   └── *.images/              ← Bilder, die zur jeweiligen .md gehören
├── cad/
│   ├── source/                ← FreeCAD-Originaldateien (.FCStd)
│   ├── exports/               ← STEP, STL, GLB
│   └── drawings/              ← technische Zeichnungen (.pdf)
├── media/
│   ├── hero.jpg               ← Hauptbild (Pflicht)
│   ├── gallery/               ← weitere Bilder für Außenwirkung
│   ├── variants/<id>/         ← variantenspezifische Bilder, Fallback auf gallery/
│   └── process/               ← Bautagebuch, Prozessdokumentation
└── .github/workflows/
    └── validate.yml           ← Validiert okh.toml und heimeliq.toml bei jedem Push
```

## Welches Bild gehört wohin?

- `media/hero.jpg` – das eine Hauptbild für Shop und Suchergebnisse.
- `media/gallery/*` – weitere Außenwirkungs-Bilder (Studio-Fotos, Detailaufnahmen für Marketing); zugleich Fallback für Varianten.
- `media/variants/<id>/*` – Bilder, die nur für eine Größenvariante gelten. Fehlt ein Bild hier, gilt das entsprechende aus `media/gallery/`.
- `media/process/*` – Bautagebuch: Fotos vom Baum, von der Werkstatt, vom Bauprozess.
- `docs/de/*.images/*` – Bilder, die direkt in einer Markdown-Datei eingebettet werden (z. B. Schrittfotos einer Verbindung).

Dateinamen in allen Medienordnern: laufende Nummer als Präfix, danach ein sprechender Name in kebab-case, ohne Umlaute – `01-front.jpg`. Jeder Medienordner hat eine `README.md` mit der Konvention.

Faustregel: **Außenwirkungs-Bilder zentral in `media/`, Doku-Bilder lokal neben ihrer Markdown-Datei.**

## ID-Konvention

| Ebene | Schema | Beispiel |
| --- | --- | --- |
| Produkt-Repo | `<family>-<type>` | `wieke-sideboard` |
| Hauptbaugruppe | `A001` | `A001` |
| Sub-Baugruppe | `A002`, `A003`, … | `A002` (z. B. Schublade) |
| Eigenes Bauteil (Self) | `<Baugruppe>.S###` | `A001.S001`, `A002.S001` |
| Externes Bauteil | `<Baugruppe>.E###` | `A001.E001`, `A002.E001` |
| Möbel-Version | SemVer | `1.2.0` |

Bauteil-IDs sind innerhalb des jeweiligen Produkt-Repos eindeutig und immer voll qualifiziert mit Assembly-Präfix. Außerhalb adressiert man sie als `<repo>/<part-id>`.

Die ID besteht aus **Familie** und **Typ**. Die Familie (`family.id`, z. B. `wieke`) sagt, welcher Formensprache es folgt; der Typ (`type`, z. B. `sideboard`, `werkbank`) sagt, was das Möbel ist. Beide Segmente sind lowercase und ASCII. Zusätzliche `[tags]` bleiben Metadaten für Filter und Suche und sind **kein** Teil der ID.

## Familien-Konzept

Jedes Produkt gehört zu genau einer **Familie**. Eine Familie trägt einen Vornamen und bezeichnet eine Formensprache: alle Produkte derselben Familie teilen Fasen, Radien und Verbindungsprinzip. Der Familienname ist zugleich der Produktname (`wieke-sideboard` → „Wieke").

Die konstruktiven Werte einer Familie liegen zentral in `families/<id>/` im Instructions-Repo, **nicht** im Produkt-Repo. Das Produkt-Repo nennt in `heimeliq.toml` nur `family.id` (lowercase, ASCII) und `family.label` (Anzeigeform).

Der **Typ** kommt aus dem zentralen Vokabular `vocabulary/typen.toml` im Instructions-Repo. Jeder Typ ist genau einem primären **Thema** zugeordnet (`theme`, z. B. `kueche`, `bad`, `wohnen`, `buero`, `werkstatt`); der in `heimeliq.toml` gesetzte `theme`-Wert muss in der `themen`-Liste des gewählten Typs stehen. Auch dieses Vokabular wird nicht ins Produkt-Repo kopiert, sondern nur referenziert.

Marken-Vokabular wie massiq, gehriq oder keiliq beschreibt Bauart und Formensprache auf der Website, ist aber **kein** Feld in `heimeliq.toml` – es wäre redundant zu den Tag-Achsen `joint` und `material`.

## Varianten

Ein Produkt kann in mehreren Größen oder anderen Holzarten gebaut werden – bei identischer Bauweise und **identischer Teileliste**. Das sind Varianten. Sie bekommen **kein eigenes Repo**, sondern sind Daten in `heimeliq.toml`.

Abgrenzung: gleiche Teileliste, nur andere Zahlen = Variante. Sobald ein Teil dazukommt, wegfällt oder sich eine Verbindungsart ändert = eigenes Produkt.

Daraus folgt eine dreistufige Dokumentation:

1. **Parametrische Quelle** – `docs/de/parametrisch/*.tpl.md`. Benannte Werte statt Zahlen, gilt für alle Varianten. Die Vorlagen enthalten keine Logik; abgeleitete Maße werden als fertiger benannter Wert eingesetzt, nicht im Template gerechnet.
2. **Referenzvariante** – genau **eine** Variante, ausgerechnet und committet unter `docs/de/build-guide.md` und `docs/de/bom.md`. Sie hält das Repo auch ohne Generator lesbar. `heimeliq.toml` → `[variants]` → `reference` benennt sie explizit (nicht implizit die erste Option). `okh.toml` → `outer-dimensions` und alle Zahlen in den `docs/de/*.md` beziehen sich auf sie.
3. **Weitere Varianten** – später als Release-Artefakt aus der parametrischen Quelle erzeugt. Nicht Teil des Repos.

Ein Produkt ohne Größenauswahl hat genau eine `[[variants.option]]`, die zugleich `reference` ist (n = 1). Kein Sonderfall.

Die Schlüssel in `[[variants.option]].parameter` sind **identisch mit den Alias-Namen der Zellen im FreeCAD-Spreadsheet**. Derselbe Name adressiert dieselbe Größe in CAD und Doku.

Einen Generator gibt es noch nicht. Bis dahin werden die Referenzvarianten-Dateien von Hand gepflegt; ihr Kopfhinweis („nicht von Hand ändern") gilt für die Zeit danach.

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

Verbesserungsvorschläge an diesem Template sind willkommen. Issues und Pull Requests direkt am Template-Repo. Änderungen am Template laufen über Versionierung (siehe `CHANGELOG.md`); bestehende Produkt-Repos werden dadurch nicht automatisch migriert.

## Lizenz

Dieses Template steht unter [MIT](LICENSE). Daraus erzeugte Produkt-Repos stehen unter [CERN-OHL-S-2.0](LICENSE.example).
