# Migrationsanleitungen

Wenn diese Vorlage auf eine neue **Major-Version** gehoben wird (z. B. `0.x.x` → `1.0.0`), beschreibt dieser Abschnitt, was bestehende Möbel-Repos tun müssen, um auf die neue Vorlagen-Version umzustellen.

Bestehende Repos werden nicht automatisch migriert – Stabilität geht vor.

## Reihenfolge bei einer Migration

1. Im Möbel-Repo einen Branch `migration-template-x.y.z` anlegen.
2. Diesem Dokument folgen.
3. Lokale Validierung laufen lassen (siehe `validate.yml`).
4. Im Möbel-Repo `heimeliq.toml` → `heimeliq-template-version` auf neue Version setzen.
5. Eintrag in `changelog.md` (klein, im Möbel-Repo) ergänzen.
6. Branch mergen, neuen SemVer-Tag setzen.

---

## 0.4.1 → 0.4.2

This is a PATCH release. No structural, schema, or directory changes are required.

1. **`heimeliq-template-version`** in `heimeliq.toml` erhöhen auf `"0.4.2"`.

Optional (empfohlen für Konsistenz, nicht erzwungen): bestehende `docs/de/bom.md` und `README.md` auf die Zuschnitt-Notation `L × B × S` umstellen (Materialstärke immer zuletzt) und – bei gehriq-Möbeln – den Abschnitt „Hinweis zur Holzauswahl" ergänzen. Bestehende Repos validieren und funktionieren auch ohne diese Anpassung unverändert weiter.

---

## 0.4.0 → 0.4.1

This is a PATCH release. No structural changes are required.

1. **`heimeliq-template-version`** in `heimeliq.toml` erhöhen auf `"0.4.1"`.

That's it — schema, `heimeliq.toml` structure, and directory layout are unchanged.

---

## 0.3.x → 0.4.0

Diese Version führt das Pflichtfeld **`heimeliq-instruction-version`** ein.

1. **`heimeliq.toml` ergänzen**: Direkt nach `heimeliq-template-version` das Feld eintragen:

   ```toml
   heimeliq-instruction-version = ""
   ```

   Der Wert bleibt leer – er wird in Phase 2 vom Bot gesetzt.

2. **`heimeliq-template-version`** auf `"0.4.0"` heben.

3. **Validate-Action prüfen**: Das Feld muss vorhanden sein; ein leerer String reicht für den Schema-Check.

---

## 0.2.x → 0.3.0

Diese Version führt das **Baugruppen-Konzept** ein. Bauteil-IDs werden voll qualifiziert mit Assembly-Präfix.

1. **Assemblies in `heimeliq.toml` ergänzen**: Mindestens die Hauptbaugruppe `A001` als `[[assemblies]]`-Eintrag eintragen, mit `source` auf die FreeCAD-Datei und `optional = false`. Falls das Möbel Erweiterungen hat (z. B. eine Schublade), für jede Erweiterung eine eigene Sub-Baugruppe `A002`, `A003`, … mit `parent = "A001"` und `optional = true` ergänzen.

2. **FreeCAD-Dateien umbenennen** nach Schema `A001-<Name>.FCStd`, `A002-<Name>.FCStd`. Optional: pro Baugruppe einen eigenen Unterordner in `cad/exports/` anlegen.

3. **Bauteil-IDs umstellen**:
   - In `okh.toml`: alle `heimeliq-part-id` von `S001` → `A001.S001` (bzw. `A002.S001` für Bauteile der Schublade etc.).
   - In `okh.toml`: neues Feld `heimeliq-assembly = "A001"` pro Bauteil ergänzen.
   - In `okh.toml`: `source` aller Bauteile auf die jeweilige Assembly-Datei zeigen lassen.
   - In `heimeliq.toml`: alle `external_parts[].heimeliq-part-id` von `E001` → `A001.E001` (bzw. `A002.E001`).

4. **Dokumentation aktualisieren**: `docs/de/bom.md` und ggf. `README.md` mit den neuen IDs befüllen.

5. **`heimeliq-template-version`** auf `"0.3.0"` heben.

6. **Validate-Action prüfen**: Lokal oder via Push prüfen, dass das neue Schema erfüllt ist. Häufige Fehler nach der Migration: fehlende `[[assemblies]]`-Section, oder Bauteil-IDs ohne Präfix.

---

## 0.1.x → 0.2.0

Diese Version führt das **Wald-Namensgeber-Konzept** ein und verschlankt das ID-Schema. Bestehende Möbel-Repos (typischerweise das v0.1.x-Pilotmöbel) sollten so migriert werden:

1. **Repo umbenennen** auf das neue Schema `heimeliq-<reihe>-<waldname>`. Beispiel: `heimeliq-massiq-sideboard-001` → `heimeliq-massiq-hambach`. Auf GitHub geht das in den Settings; die alte URL bleibt eine Weile als Redirect bestehen.

2. **`heimeliq.toml` anpassen**:
   - `slug` auf `<reihe>-<waldname>` setzen (z. B. `"massiq-hambach"`).
   - `type` bleibt erhalten, aber jetzt als Metadatenfeld (z. B. `"sideboard"`).
   - Optional: `tags = ["..."]` ergänzen.
   - Neue Pflicht-Section `[forest]` ergänzen – mindestens `id`, `name`, `region`, `country` ausfüllen. Optionale Felder (`forest_type`, `age_estimate_years`, `status`, `themes`, `links`, `note`) nach Möglichkeit ebenfalls befüllen.
   - `heimeliq-template-version` auf `"0.2.0"` heben.

3. **README im Möbel-Repo aktualisieren**: Den Wald-Namensgeber-Bereich aus der neuen `README.example.md` übernehmen und ausfüllen.

4. **Validate-Action lokal oder via Push prüfen**: Schlägt die Validierung an, fehlt vermutlich ein Pflichtfeld in `[forest]` oder der `slug` passt nicht zum neuen Pattern.

5. **`furniture-repos.json` im Website-Repo aktualisieren**: Die alte URL gegen die neue tauschen.

6. **CHANGELOG.md des Möbels** (klein, im Möbel-Repo) ergänzen mit einem Eintrag wie:

   ```
   ## [0.2.0] – Wald-Namensgeber ergänzt, Repo umbenannt
   - Repo-Name: heimeliq-massiq-sideboard-001 → heimeliq-massiq-hambach
   - [forest]-Section in heimeliq.toml ergänzt
   - Template-Version 0.2.0
   ```

---

## 0.x → 1.0 (noch nicht erschienen)

*Wird ergänzt, sobald die erste Major-Version veröffentlicht wird.*
