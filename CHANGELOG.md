# Changelog – heimeliq Furniture Template

Versionierung folgt [Semantic Versioning](https://semver.org/lang/de/).

- **MAJOR** (`x.0.0`): Breaking Change. Bestehende Möbel-Repos brauchen Migration.
- **MINOR** (`0.x.0`): Neues optionales Feld oder Ordner. Bestehende Repos funktionieren weiter.
- **PATCH** (`0.0.x`): Tippfehler, Klarstellungen, Bug-Fixes, kein strukturelles Update.

## [0.4.1] – Brand name normalization and schema relaxation

**Changed:**

- Brand name unified to lowercase `heimeliq` across all template files (was `heimeliQ`).
- `heimeliq.schema.json`: `slug` pattern relaxed from a hardcoded series enum to a generic lowercase alphanumeric pattern, allowing new series without schema changes.
- `heimeliq.schema.json`: `series` changed from a fixed enum (`massiq`, `workaholiq`, `keiliq`) to an open lowercase pattern – new series can be added without a schema update.
- `README.md`: setup steps now include renaming `CHANGELOG.md` and deleting `MIGRATIONS.md` when initializing a new furniture repo.
- `README.example.md`: shop URL updated to `/reihe/FIXME-slug`; removed managed-shop note.

**Migration:** see `MIGRATIONS.md` for the steps 0.4.0 → 0.4.1.

## [0.4.0] – Instruction-Version

Jedes heimeliq-Möbel trägt jetzt eine Referenz auf den Instructions-Stand, mit dem es produziert wurde. Das Feld `heimeliq-instruction-version` wird in Phase 2 automatisch vom Bot gesetzt und bleibt im Template leer.

**Neu:**

- Pflichtfeld `heimeliq-instruction-version` in `heimeliq.schema.json` und als leerer Platzhalter in `heimeliq.toml`.

**Migration:** siehe `MIGRATIONS.md` für die Schritte 0.3.x → 0.4.0.

## [0.3.0] – Baugruppen-Hierarchie und qualifizierte Bauteil-IDs

heimeliq-Möbel sind jetzt als Hierarchie von Baugruppen modelliert. `A001` ist konventionell die Hauptbaugruppe (= das Möbel), Sub-Baugruppen wie Schubladen oder Türen bekommen `A002`, `A003`, … Bauteil-IDs sind voll qualifiziert mit Assembly-Präfix (`A001.S001`, `A002.E001` usw.). Damit lassen sich optionale Erweiterungen sauber abbilden, und der spätere Shop kann sie als konfigurierbare Varianten mit Aufpreis anbieten.

**Neu:**

- Pflicht-Section `[[assemblies]]` in `heimeliq.toml` mit mindestens der Hauptbaugruppe `A001`. Felder: `heimeliq-assembly-id`, `name`, optional `description`, `source`, `parent`, `optional`.
- Bauteil-IDs sind jetzt voll qualifiziert: `<Baugruppe>.S###` für eigene Teile, `<Baugruppe>.E###` für externe Teile. Tieferes Nesting (z. B. `A002.A003.S001`) ist technisch erlaubt.
- OKH-`[[part]]`-Einträge bekommen ein neues Feld `heimeliq-assembly`, das die Baugruppe explizit verlinkt.
- Konvention für FreeCAD-Dateien: eine `.FCStd` pro Baugruppe, benannt nach `A###-<Name>.FCStd`.
- `heimeliq.schema.json` validiert die Assembly-Struktur und die präfixierten IDs.
- README erklärt das Baugruppen-Konzept; Migrations-Anleitung in `MIGRATIONS.md`.

**Migration:** siehe `MIGRATIONS.md` für die Schritte 0.2.x → 0.3.0.

## [0.2.0] – Wald-Namensgeber, schlankeres ID-Schema

Jedes heimeliq-Möbel trägt den Namen eines real existierenden Waldes. Der Waldname ist möbel-eindeutig: kein zweites Möbel trägt denselben Wald. Damit wird die Marke um eine inhaltliche Schicht erweitert – jedes Möbel verweist auf einen Ort und macht bei bedrohten Wäldern deren Situation sichtbar. Da der Waldname allein eindeutig ist, entfällt das `<typ>`-Segment in der ID.

**Neu:**

- ID-Schema umgestellt von `heimeliq-<reihe>-<typ>-<nr>` auf `heimeliq-<reihe>-<waldname>`.
- `heimeliq.toml` bekommt eine `[forest]`-Section mit Pflichtfeldern (`id`, `name`, `region`, `country`) und optionalen Feldern (`forest_type`, `age_estimate_years`, `status`, `themes`, `links`, `note`).
- `type` bleibt erhalten, jetzt aber als Metadatenfeld für Filter/Suche – nicht mehr als Teil der ID.
- Neues optionales `tags`-Array für zusätzliche Schlagworte.
- `heimeliq.schema.json` validiert `forest` als Pflicht-Section und prüft den `slug`-Pattern auf `<reihe>-<waldname>`.
- README erklärt das Wald-Konzept und die Typ/Tags-Logik.
- `README.example.md` enthält einen prominenten Wald-Namensgeber-Bereich.

**Migration für bestehende Möbel-Repos (z. B. das v0.1.x-Pilotmöbel):**

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
- OKH 2.4 als Standard für Möbel-Metadaten.
- **Lizenz-Trennung**: Template selbst unter MIT, daraus erzeugte Möbel-Repos unter CERN-OHL-S-2.0.
- `LICENSE.example` und `README.example.md` als Vorlagen.
- Doku-Struktur unter `docs/de/` mit co-located `.images/`-Ordnern.
- `heimeliq.toml` für projektspezifische Erweiterungen.
- `heimeliq.schema.json` für strenge Validierung.
- GitHub-Action `validate.yml` mit kontextabhängigen Checks.
- REUSE-konforme Datei-Lizenzangaben.
