# heimeliq Product Template

Vorlage zur Erstellung neuer Produkt-Repositories für das [heimeliq](https://heimeliq.de)-Projekt.

Jedes Holz-Produkt oder -Accessoire von heimeliq lebt in einem eigenen Git-Repository. Diese Vorlage definiert die einheitliche Struktur, die alle Produkt-Repos verwenden, und stellt sicher, dass jedes Repo dem [Open Know-How (OKH) Standard](https://github.com/iop-alliance/OpenKnowHow) entspricht.

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
- **Produkt-Repos**, die aus dieser Vorlage erzeugt werden, stehen unter **CERN-OHL-S-2.0** (strongly reciprocal Open Hardware Licence). Wer ein Produkt weiterentwickelt, muss die Weiterentwicklung wieder offen unter derselben Lizenz teilen.

Konkret heißt das im Repo:

| Datei im Template | Wird im Produkt-Repo zu | Lizenz |
| --- | --- | --- |
| `LICENSE` | _entfällt_ | MIT (gilt nur fürs Template) |
| `LICENSE.example` | `LICENSE` | CERN-OHL-S-2.0 |
| `README.md` | _entfällt_ | MIT (diese Datei hier) |
| `README.example.md` | `README.md` | CERN-OHL-S-2.0 |

## Was ist heimeliq?

heimeliq baut Holz-Produkte oder -Accessoires aus regionalen Naturmaterialien – Massivholz, Stahl, Sperrholz – und veröffentlicht jedes Stück vollständig als Open Source: 3D-Modelle, Stücklisten, Bauanleitungen. Diese Vorlage ist Teil der digitalen Infrastruktur dahinter.

Jedes Produkt gehört zu einer **Serie** (einer Produktlinie aus dem Markenvokabular – `gehriq`, `keiliq`, `workaholiq`, `uhriq`) und hat einen **Typ** (was es ist – `sideboard`, `tablett`, `werkbank`). Serie und Typ bilden in dieser Reihenfolge die Repo-ID. Details im Abschnitt [Serien-Konzept](#serien-konzept).

## Ein neues Produkt-Repo aus dieser Vorlage erzeugen

1. Auf GitHub den Knopf **„Use this template"** → **„Create a new repository"** klicken.
2. Repo-Name nach Schema: `<series>-<type>`, zum Beispiel `gehriq-sideboard`.
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
- In `heimeliq.toml`: `type`, `theme`, `slug`, `[series]`, `[variants]`.
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
├── changelog.md               ← Versions-Historie des Produkts (klein!)
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
| Produkt-Repo | `<series>-<type>[-<zusatz>]` | `gehriq-sideboard` |
| Hauptbaugruppe | `A001` | `A001` |
| Sub-Baugruppe | `A002`, `A003`, … | `A002` (z. B. Schublade) |
| Eigenes Bauteil (Self) | `<Baugruppe>.S###` | `A001.S001`, `A002.S001` |
| Externes Bauteil | `<Baugruppe>.E###` | `A001.E001`, `A002.E001` |
| Produkt-Version | SemVer | `1.2.0` |

Bauteil-IDs sind innerhalb des jeweiligen Produkt-Repos eindeutig und immer voll qualifiziert mit Assembly-Präfix. Außerhalb adressiert man sie als `<repo>/<part-id>`.

Eine **Bauteil-ID bezeichnet eine Bauform, keine Instanz.** Dieselbe ID bedeutet in jeder Variante dasselbe Bauteil; was sich zwischen Varianten unterscheidet, sind nur ihre Zahlen – Maße und Anzahl. Kommen mehrere Größen desselben Bauteils *gleichzeitig* in einem Produkt vor (drei verschieden breite Schubladen), sind das eigene IDs; dass sie nach demselben Bauplan entstehen, sagt das Feld `bauform`.

Die ID besteht aus **Serie** und **Typ**. Die Serie (`series.id`, z. B. `gehriq`) sagt, zu welcher Produktlinie es gehört; der Typ (`type`, z. B. `sideboard`, `werkbank`) sagt, was das Produkt ist. Beide Segmente sind lowercase und ASCII. Zusätzliche `[tags]` bleiben Metadaten für Filter und Suche und sind **kein** Teil der ID.

Ein **drittes Segment** ist erlaubt, aber die Ausnahme: es wird nur gesetzt, wenn zwei eigenständige Konstruktionen derselben Serie denselben Typ hätten (`gehriq-sideboard-vinyl`). Es ist frei benannt und **keine Laufnummer** – im Regelfall bleibt es weg. Namen werden nach dem Prinzip „wer zuerst kommt" vergeben; Konflikte klärt der Pull Request.

## Serien-Konzept

Jedes Produkt gehört zu genau einer **Serie**. Eine Serie ist eine Produktlinie aus dem Markenvokabular – `gehriq`, `keiliq`, `workaholiq`, `uhriq` – und bezeichnet eine Gruppe von Produkten, die in Optik und Bauweise zusammenpassen.

Was eine Serie im Einzelnen bedeutet, entscheidet die Serie selbst: mal eine Bauart (`gehriq` = Gehrungs-Ecken), mal eine Domäne (`uhriq`). Es gibt bewusst **kein** übergreifendes Kriterium, dem alle Serien folgen müssen. Verbindlich beschrieben ist eine Serie in ihrer `SERIES.md` im Instructions-Repo.

Die konstruktiven Werte einer Serie liegen zentral in `series/<id>/` im Instructions-Repo, **nicht** im Produkt-Repo. Das Produkt-Repo nennt in `heimeliq.toml` nur `series.id` (lowercase, ASCII) und `series.label` (Anzeigeform).

Der **Typ** kommt aus dem zentralen Vokabular `vocabulary/types.toml` im Instructions-Repo. Jeder Typ ist genau einem primären **Thema** zugeordnet (`theme`, z. B. `kueche`, `bad`, `wohnen`, `buero`, `werkstatt`); der in `heimeliq.toml` gesetzte `theme`-Wert muss in der `themes`-Liste des gewählten Typs stehen. Auch dieses Vokabular wird nicht ins Produkt-Repo kopiert, sondern nur referenziert.

Das Markenvokabular ist damit **die ID** und keine Tag-Achse mehr: es aus dem ersten Segment abzulesen ist eindeutiger, als es zusätzlich zu pflegen.

## Varianten

Ein Produkt kann in mehreren Größen, Innenaufteilungen oder Holzarten gebaut werden. Das sind Varianten. Sie bekommen **kein eigenes Repo**, sondern sind Daten in `heimeliq.toml`.

Varianten gibt es auf zwei Ebenen, und die Regeln sind bewusst verschieden streng:

| Ebene | Was darf sich unterscheiden | Wie benannt |
| --- | --- | --- |
| **Produktvariante** | Maße, Innenaufteilung, Bauteilauswahl | frei gewählter Name, eindeutig innerhalb des Produkts |
| **Bauteilvariante** | **nur die Zahlen** (Maße, Anzahl) | keine eigene ID – dieselbe Bauteil-ID in mehreren Produktvarianten |

Die Produktvariante darf frei sein, weil sie Bauteile **auswählt**, statt sie zu verändern. Ihre `parts`-Liste sagt, welche Bauteile sie enthält. Der Name ist dir überlassen: `1200x800` (Außenmaße), `3x4x3` (Aufteilungsraster – drei Fächer links, vier in der Mitte, drei rechts) oder `klein` sind gleichermaßen zulässig. Einzige harte Regel: innerhalb eines Produkts darf kein Name zweimal vorkommen.

**Die Abgrenzung zum eigenen Produkt** liegt nicht mehr bei der Teileliste, sondern beim Parameter-Schlüsselsatz:

> Alle Optionen eines Produkts haben **denselben Satz von `parameter`-Schlüsseln**. Nur die Werte unterscheiden sich. Kommt ein Schlüssel dazu oder fällt einer weg, ist es ein eigenes Produkt.

`validate.yml` prüft das. Eine **Anzahl ist dabei eine Zahl wie jede andere**: `FaecherMitte = 4` ist ein gültiger Parameter. Ein breiteres Sideboard mit einer Zwischenwand mehr bleibt damit eine Variante – die Teileliste wird länger, der Schlüsselsatz nicht.

Daraus folgt eine dreistufige Dokumentation:

1. **Parametrische Quelle** – `docs/de/parametrisch/*.tpl.md`. Benannte Werte statt Zahlen, gilt für alle Varianten. Die Vorlagen enthalten keine Logik; abgeleitete Maße werden als fertiger benannter Wert eingesetzt, nicht im Template gerechnet.
2. **Referenzvariante** – genau **eine** Variante, ausgerechnet und committet unter `docs/de/build-guide.md` und `docs/de/bom.md`. Sie hält das Repo auch ohne Generator lesbar. `heimeliq.toml` → `[variants]` → `reference` benennt sie explizit (nicht implizit die erste Option). `okh.toml` → `outer-dimensions` und alle Zahlen in den `docs/de/*.md` beziehen sich auf sie.
3. **Weitere Varianten** – später als Release-Artefakt aus der parametrischen Quelle erzeugt. Nicht Teil des Repos.

Ein Produkt ohne Größenauswahl hat genau eine `[[variants.option]]`, die zugleich `reference` ist (n = 1). Kein Sonderfall.

Die Schlüssel in `[[variants.option]].parameter` sind **identisch mit den Alias-Namen der Zellen im FreeCAD-Spreadsheet**. Derselbe Name adressiert dieselbe Größe in CAD und Doku. Dort stehen nur die freien **Eingangswerte** – Bauteilmaße und Stückzahlen leitet der Generator daraus ab und werden nicht doppelt gepflegt.

Einen Generator gibt es noch nicht. Bis dahin werden die Referenzvarianten-Dateien von Hand gepflegt; ihr Kopfhinweis („nicht von Hand ändern") gilt für die Zeit danach.

## Baugruppen-Konzept

Jedes heimeliq-Produkt ist als Hierarchie von Baugruppen modelliert:

- Eine **Baugruppe** ist, was sich als Einheit gegenüber den anderen bewegt oder getrennt montiert wird — Korpus, Tür, Schublade, Deckel. Nicht „was verleimt ist": Ein Klappdeckel ist ein einzelnes Brett und trotzdem eine eigene Baugruppe, weil er sich bewegt; ein fest verschraubter Innenboden ist keine, sondern ein Bauteil des Korpus.
- **`A001`** ist die erste davon, nicht „das Produkt". Das Produkt ist das Repo und hat keine A-Nummer: Bei einer Box mit Klappdeckel ist `A001` der Korpus, `A002` der Deckel, und das Produkt ist beides zusammen.
- Vergeben wird in Entstehungsreihenfolge, nie umnummeriert. Sub-Baugruppen referenzieren ihre Eltern-Baugruppe über das Feld `parent`.
- **Eine Variante ist nie eine Baugruppe.** Ein Sideboard in 1200 und eines in 1600 sind dieselbe Konstruktion mit anderen Zahlen — sie teilen Baugruppen, Bauteile und Bauanleitung. Varianten stehen unter `[variants]`, nicht unter `[[assemblies]]`.
- Jedes Bauteil gehört zu genau einer Baugruppe und trägt deren Präfix in der ID (`A001.S001`, `A002.E001` usw.).
- **Beschläge gehören dem angebauten Teil**: Die Tür bringt ihre Scharniere mit, die Schublade ihre Schienen, der Deckel seine Dübel. So folgt die Stückzahl dem Bauteil, statt von Hand mitgezählt zu werden.
- `optional = true` markiert eine Baugruppe als Erweiterung. Solche Baugruppen werden später im Shop zu konfigurierbaren Varianten mit Aufpreis.
- `bauform` ist optional und benennt eine geteilte parametrische Quelle. Baugruppen mit derselben `bauform` sind dasselbe Ding in anderen Größen **innerhalb eines Produkts**: Enthält ein Sideboard drei verschieden breite Schubladen, sind das `A002`, `A003`, `A004` mit `bauform = "schublade"`, und die Bauanleitung beschreibt die Schublade einmal. Das ist kein Varianten-Mechanismus.

**Konvention für FreeCAD-Dateien**: Jede Baugruppe ist eine eigene `.FCStd`-Datei, benannt nach Schema `A001-<Name>.FCStd`, `A002-<Name>.FCStd`. Beispiel:

```
cad/source/
├── A001-Sideboard.FCStd
└── A002-Schublade.FCStd
```

Im OKH-`[[part]]`-Array zeigt das `source`-Feld jedes Bauteils auf die Assembly-Datei, in der das Bauteil definiert ist. Zusätzlich verlinkt das Feld `heimeliq-assembly` die Baugruppe explizit.

In der Praxis sind zwei Hierarchie-Ebenen (Produkt + direkte Erweiterungen) der Normalfall. Tieferes Nesting (z. B. `A002.A003.S001`) ist technisch erlaubt, aber selten nötig.

## Mitwirken

Verbesserungsvorschläge an diesem Template sind willkommen. Issues und Pull Requests direkt am Template-Repo. Änderungen am Template laufen über Versionierung (siehe `CHANGELOG.md`); bestehende Produkt-Repos werden dadurch nicht automatisch migriert.

## Lizenz

Dieses Template steht unter [MIT](LICENSE). Daraus erzeugte Produkt-Repos stehen unter [CERN-OHL-S-2.0](LICENSE.example).
