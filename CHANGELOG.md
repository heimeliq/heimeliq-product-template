# Changelog – heimeliq Product Template

Versionierung folgt [Semantic Versioning](https://semver.org/lang/de/).

- **MAJOR** (`x.0.0`): Breaking Change. Bestehende Produkt-Repos brauchen Migration.
- **MINOR** (`0.x.0`): Neues optionales Feld oder Ordner. Bestehende Repos funktionieren weiter.
- **PATCH** (`0.0.x`): Tippfehler, Klarstellungen, Bug-Fixes, kein strukturelles Update.

## [0.7.0] – 2026-09-14 – Plate choice leaves the BOM template

`docs/de/bom.md` compared three plate lengths — 2000, 2600 and 3000 mm — against
the requirement. The numbers were invented: no supplier was behind them, and the
plate width was left as a placeholder, so the table could not be true for any
real offer. It has been removed.

**Changed:**

- `docs/de/bom.md` and `docs/de/parametrisch/bom.tpl.md`: the section
  *Plattengrößen-Vergleich und Verschnitt* is replaced by *Welche Platte es
  wird*, which states the requirement (`L_min`, `B_min`) and leaves the choice
  to the moment of purchase. Twelve `{{ plate_* }}` placeholders and four FIXME
  are gone from the template; the shipped `bom.md` loses sixteen FIXME.
- `L_min` and `B_min` stay where they are. They follow from the product, not
  from the supplier.

Nothing else changes. A product repo on 0.6.0 keeps working; adopting this is
optional and described in `MIGRATIONS.md`.

## [0.6.0] – 2026-09-10 – Series naming and free variants

The `family` becomes a **series** and carries the brand vocabulary (`gehriq`,
`keiliq`, `workaholiq`, `uhriq`). Variants may now differ in inner layout and
part selection, and the rule separating a variant from a separate product moves
from the parts list to the parameter key set.

**BREAKING:**

- `[family]` is renamed to `[series]`. Same fields (`id`, `label`), new meaning:
  a series is a product line from the brand vocabulary, not a first name. What a
  series means – a construction type like `gehriq` or a domain like `uhriq` – is
  decided per series and documented in its `SERIES.md` in the instructions repo.
- Repo and `slug` change from `<family>-<type>` to `<series>-<type>`. An optional
  third segment is now allowed (regex `^[a-z]+-[a-z]+(-[a-z0-9-]+)?$`), used only
  when two distinct constructions of the same series would share a type. It is
  freely named and is not a running number.
- `[[variants.option]]` gains a required `parts` array listing the fully
  qualified part IDs the variant contains. An assembly counts as included as
  soon as one of its parts is listed.
- `[[variants.option]].id` no longer has to start with a letter (regex
  `^[a-z0-9][a-z0-9-]*$`), so `1200x800` and `3x4x3` are valid names. Naming is
  entirely up to the author; the only hard rule is uniqueness within the product.
- The rule "identical parts list = variant" is gone. A variant is now defined by
  an **identical `parameter` key set** across all options – only the values may
  differ. A quantity is a number like any other (`FaecherMitte = 4`), so a wider
  cabinet with one more divider stays a variant.
- The tag axes in `heimeliq.toml` and `vocabulary/tags.toml` (instructions repo)
  now carry the same English IDs. Previously only `material` and `status`
  matched; `verbindung`/`holzart`/`werkzeug`/`aufwand`/`eigenschaft` are now
  `joint`/`species`/`tooling`/`effort`/`property`, and the translation no longer
  has to be carried in someone's head.
- The `bauart` axis is deleted, along with its values `korpusbau` and
  `rahmenbau`. Its brand values moved into the ID as the series; the schema's
  `additionalProperties: false` made the axis unwritable from a product repo
  anyway.
- `vocabulary/typen.toml` is renamed to `types.toml` and its keys are English:
  `[[thema]]`/`[[typ]]` become `[[theme]]`/`[[type]]`, `reihenfolge`/`themen`/
  `gattung` become `order`/`themes`/`category`. The vocabulary *values* stay
  German slugs – a `type` slug is the second segment of the product ID.

**Added:**

- `[[assemblies]].bauform` (optional): names a shared parametric source. Three
  drawers of different widths are `A002`, `A003`, `A004` with
  `bauform = "schublade"` – flat, stable IDs and one description in the build guide.
- `validate.yml` checks variant option IDs for uniqueness, enforces the identical
  parameter key set, and resolves every `parts` entry against `okh.toml [[part]]`
  and `heimeliq.toml [[external_parts]]`.

**Fixed:**

- Two open points carried since 0.5.0 are closed: the instructions vocabulary no
  longer uses German keys, and the template's own `heimeliq.toml` no longer fails
  its own schema check.
- Both schema checks in `validate.yml` now run only in product repos. The repo-kind
  detection moved ahead of them. The template itself is full of `FIXME` placeholders
  and zero values and can never validate against either schema, so the workflow was
  failing on the template repo by construction (`type = "FIXME"` against `^[a-z]+$`,
  and `mass = 0` against the OKH schema's exclusive minimum). The variant checks
  still run everywhere - the template's placeholders are internally consistent.

**Removed:**

- The schema's legacy `"series": false` guard from 0.5.0, replaced by a `"family": false`
  guard so the old field name is now rejected.
- All axis counts from documentation and comments. The number of axes is not a
  fact worth stating in five places: `tags.toml` can gain an axis without any
  other file having to agree on a count. Only `heimeliq.schema.json` must follow,
  and both files now say so.

**Migration:** see `MIGRATIONS.md` for the steps 0.5.1 → 0.6.0.

## [0.5.1] – 2026-09-09 – Terminology: "Möbel" → "Produkt"

PATCH release. Documentation and code comments now consistently say *Produkt*
instead of *Möbel*, matching the `heimeliq-product-template` rename in 0.5.0.
No schema, structure, or directory changes.

**Changed:**

- README, MIGRATIONS, `changelog.md`, `docs/de/*` templates, `heimeliq.schema.json`
  and `heimeliq.toml` comments: "Möbel" replaced with "Produkt" throughout,
  including inflected forms and the historical CHANGELOG entries.
- Grammatical artifacts from an earlier bulk replacement are fixed.

**Migration:** see `MIGRATIONS.md` for the steps 0.5.0 → 0.5.1.

## [0.5.0] – 2026-09-09 – Repository rename, type/theme/family and mandatory variants

The template repository is renamed to `heimeliq-product-template`, plus two
breaking changes to `heimeliq.toml`: a new naming schema and a mandatory
`[variants]` section. No compatibility alias, no migration script – the one
existing product repo is migrated by hand.

**BREAKING:**

- `series` and the whole `[forest]` section are gone. A product now has a
  `type` (what it is) and a `[family]` (a shape language carrying a first
  name). Repo and `slug` change from `heimeliq-<series>-<forest>` to
  `<family>-<type>` (regex `^[a-z]+-[a-z]+$`), dropping the `heimeliq-`
  prefix.
- New required top-level field `theme`, restricted to the themes the chosen
  `type` allows in `vocabulary/typen.toml` (instructions repo).
- The flat `tags` array becomes a `[tags]` table with seven closed axes
  (`joint`, `species`, `material`, `tooling`, `effort`, `property`,
  `status`) and open values per axis.
- The top-level `status` field moves into the `tags.status` axis; the
  `validate.yml` publish gate now reads `"published" in tags.status`.
- New required `[variants]` section: `reference` plus at least one
  `[[variants.option]]` (`id`, `label`, `parameter`). A product without a
  size choice has one option that is also the reference. `parameter` keys
  are the FreeCAD spreadsheet cell alias names verbatim.

**Added:**

- `docs/de/parametrisch/build-guide.tpl.md` and `bom.tpl.md`: logic-free
  parametric sources with `{{ name }}` placeholders. The rendered
  `docs/de/build-guide.md` and `docs/de/bom.md` describe the reference
  variant and carry a "generated, do not edit" header.
- `media/variants/<id>/` for variant-specific images, falling back to
  `media/gallery/`. Every media directory now has a `README.md`.
- README section on the three documentation stages and the reference-variant
  rule.
- `validate.yml` step checking that `variants.reference` points to an
  existing option id.

**Changed:**

- The template repository is renamed from `heimeliq-furniture-template` to
  `heimeliq-product-template`. heimeliq now covers accessories as well as
  furniture, and the docs speak of *products* throughout. GitHub keeps the old
  URL as a redirect; update any `git clone` URL or "Use this template"
  bookmark. The generated product repos are unaffected – they were never
  named after the template. The website list file `furniture-repos.json`
  is renamed to `product-repos.json` to match.
- `okh.toml`: comments on `[outer-dimensions]` and per-part
  `outer-dimensions` clarifying they describe the reference variant only.
  OKH knows no ranges and is deliberately not stretched; otherwise untouched.

**Open points (not addressed in this release):**

- `vocabulary/typen.toml` in the instructions repo still uses German keys
  (`thema`, `typ`, `gattung`, `themen`, `reihenfolge`); to be aligned
  separately.
- `validate.yml` does not yet check `type`/`theme` against
  `vocabulary/typen.toml` (needs read access to the instructions repo).
- The template's own `heimeliq.toml` does not validate against its own schema
  because the `FIXME` placeholders violate the field patterns. This predates
  0.5.0.

**Migration:** see `MIGRATIONS.md` for the steps 0.4.2 → 0.5.0.

## [0.4.2] – Bill-of-materials notation and wood-selection guidance

**Changed:**

- Bill-of-materials part dimensions now use a cut-list notation `L × B × S` (length × width × thickness) instead of `B × T × H`. Thickness is always last, independent of how the part sits in the furniture, so equally thick boards stay comparable. Affects `README.example.md` (Stückliste) and `docs/de/bom.md`.
- `README.example.md`: removed the redundant `Werkzeuge` section (tools are covered in the build guide), and fixed the changelog link and the series URL.

**Added:**

- `docs/de/bom.md`: new `Hinweis zur Holzauswahl` section covering the gehriq continuous-grain principle (both side panels and the lid cut from one board), the minimum board length in grain direction (`2 × Außenhöhe + Außenbreite + saw allowance`, board width ≥ depth, rounded up to the next 100 mm), and a plate-size comparison table with waste.

**Migration:** see `MIGRATIONS.md` for the steps 0.4.1 → 0.4.2.

## [0.4.1] – Brand name normalization and schema relaxation

**Changed:**

- Brand name unified to lowercase `heimeliq` across all template files (was `heimeliq`).
- `heimeliq.schema.json`: `slug` pattern relaxed from a hardcoded series enum to a generic lowercase alphanumeric pattern, allowing new series without schema changes.
- `heimeliq.schema.json`: `series` changed from a fixed enum (`massiq`, `workaholiq`, `keiliq`) to an open lowercase pattern – new series can be added without a schema update.
- `README.md`: setup steps now include renaming `CHANGELOG.md` and deleting `MIGRATIONS.md` when initializing a new furniture repo.
- `README.example.md`: shop URL updated to `/reihe/FIXME-slug`; removed managed-shop note.

**Migration:** see `MIGRATIONS.md` for the steps 0.4.0 → 0.4.1.

## [0.4.0] – Instruction-Version

Jedes heimeliq-Produkt trägt jetzt eine Referenz auf den Instructions-Stand, mit dem es produziert wurde. Das Feld `heimeliq-instruction-version` wird in Phase 2 automatisch vom Bot gesetzt und bleibt im Template leer.

**Neu:**

- Pflichtfeld `heimeliq-instruction-version` in `heimeliq.schema.json` und als leerer Platzhalter in `heimeliq.toml`.

**Migration:** siehe `MIGRATIONS.md` für die Schritte 0.3.x → 0.4.0.

## [0.3.0] – Baugruppen-Hierarchie und qualifizierte Bauteil-IDs

heimeliq-Produkte sind jetzt als Hierarchie von Baugruppen modelliert. `A001` ist konventionell die Hauptbaugruppe (= das Produkt), Sub-Baugruppen wie Schubladen oder Türen bekommen `A002`, `A003`, … Bauteil-IDs sind voll qualifiziert mit Assembly-Präfix (`A001.S001`, `A002.E001` usw.). Damit lassen sich optionale Erweiterungen sauber abbilden, und der spätere Shop kann sie als konfigurierbare Varianten mit Aufpreis anbieten.

**Neu:**

- Pflicht-Section `[[assemblies]]` in `heimeliq.toml` mit mindestens der Hauptbaugruppe `A001`. Felder: `heimeliq-assembly-id`, `name`, optional `description`, `source`, `parent`, `optional`.
- Bauteil-IDs sind jetzt voll qualifiziert: `<Baugruppe>.S###` für eigene Teile, `<Baugruppe>.E###` für externe Teile. Tieferes Nesting (z. B. `A002.A003.S001`) ist technisch erlaubt.
- OKH-`[[part]]`-Einträge bekommen ein neues Feld `heimeliq-assembly`, das die Baugruppe explizit verlinkt.
- Konvention für FreeCAD-Dateien: eine `.FCStd` pro Baugruppe, benannt nach `A###-<Name>.FCStd`.
- `heimeliq.schema.json` validiert die Assembly-Struktur und die präfixierten IDs.
- README erklärt das Baugruppen-Konzept; Migrations-Anleitung in `MIGRATIONS.md`.

**Migration:** siehe `MIGRATIONS.md` für die Schritte 0.2.x → 0.3.0.

## [0.2.0] – Wald-Namensgeber, schlankeres ID-Schema

Jedes heimeliq-Produkt trägt den Namen eines real existierenden Waldes. Der Waldname ist produkteindeutig: kein zweites Produkt trägt denselben Wald. Damit wird die Marke um eine inhaltliche Schicht erweitert – jedes Produkt verweist auf einen Ort und macht bei bedrohten Wäldern deren Situation sichtbar. Da der Waldname allein eindeutig ist, entfällt das `<typ>`-Segment in der ID.

**Neu:**

- ID-Schema umgestellt von `heimeliq-<reihe>-<typ>-<nr>` auf `heimeliq-<reihe>-<waldname>`.
- `heimeliq.toml` bekommt eine `[forest]`-Section mit Pflichtfeldern (`id`, `name`, `region`, `country`) und optionalen Feldern (`forest_type`, `age_estimate_years`, `status`, `themes`, `links`, `note`).
- `type` bleibt erhalten, jetzt aber als Metadatenfeld für Filter/Suche – nicht mehr als Teil der ID.
- Neues optionales `tags`-Array für zusätzliche Schlagworte.
- `heimeliq.schema.json` validiert `forest` als Pflicht-Section und prüft den `slug`-Pattern auf `<reihe>-<waldname>`.
- README erklärt das Wald-Konzept und die Typ/Tags-Logik.
- `README.example.md` enthält einen prominenten Wald-Namensgeber-Bereich.

**Migration für bestehende Produkt-Repos (z. B. das v0.1.x-Pilotprodukt):**

1. Repo umbenennen auf `heimeliq-<reihe>-<waldname>`.
2. In `heimeliq.toml`: `slug` anpassen, `[forest]`-Section ergänzen, ggf. `tags` setzen.
3. `heimeliq-template-version` auf `0.2.0` setzen.
4. Validate-Action laufen lassen.

## [0.1.1] – TOML-Reihenfolge-Bugfix in `okh.toml`

Behebt einen latenten Bug in der Beispiel-`okh.toml`: Einige Top-Level-Felder (`mass`, `manufacturing-instructions`, `bom`, `readme`) standen nach Section-Headern und wurden dadurch laut TOML-Spezifikation als Sub-Felder dieser Sections interpretiert. Dasselbe galt für `[part.outer-dimensions]`, das bei mehreren `[[part]]`-Einträgen mehrdeutig wird.

**Behoben:**

- Alle Top-Level-Felder stehen jetzt vor der ersten Section.
- `outer-dimensions` innerhalb `[[part]]` wird als Inline-Table notiert.
- Erklärender Kommentar zur TOML-Reihenfolge in der Datei ergänzt.

## [0.1.0] – initial

- Erste Version des Templates.
- OKH 2.4 als Standard für Produkt-Metadaten.
- **Lizenz-Trennung**: Template selbst unter MIT, daraus erzeugte Produkt-Repos unter CERN-OHL-S-2.0.
- `LICENSE.example` und `README.example.md` als Vorlagen.
- Doku-Struktur unter `docs/de/` mit co-located `.images/`-Ordnern.
- `heimeliq.toml` für projektspezifische Erweiterungen.
- `heimeliq.schema.json` für strenge Validierung.
- GitHub-Action `validate.yml` mit kontextabhängigen Checks.
- REUSE-konforme Datei-Lizenzangaben.
