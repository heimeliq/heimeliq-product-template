# Migrationsanleitungen

Wenn diese Vorlage auf eine neue **Major-Version** gehoben wird (z. B. `0.x.x` → `1.0.0`), beschreibt dieser Abschnitt, was bestehende Produkt-Repos tun müssen, um auf die neue Vorlagen-Version umzustellen.

Bestehende Repos werden nicht automatisch migriert – Stabilität geht vor.

## Reihenfolge bei einer Migration

1. Im Produkt-Repo einen Branch `migration-template-x.y.z` anlegen.
2. Diesem Dokument folgen.
3. Lokale Validierung laufen lassen (siehe `validate.yml`).
4. Im Produkt-Repo `heimeliq.toml` → `heimeliq-template-version` auf neue Version setzen.
5. Eintrag in `changelog.md` (klein, im Produkt-Repo) ergänzen.
6. Branch mergen, neuen SemVer-Tag setzen.

---

## 0.9.2 → 0.9.3

Kein Breaking Change. Die `docs/de/bom.md` bekommt einen Abschnitt für die Masse.

### Warum

Die Gesamtmasse steht als `mass` in der `okh.toml` und als Zeile in der
Datentabelle der `README.md`. Wie sie zustande kam, stand nur als Kommentar in
der `okh.toml` — und die wird am Ende von Phase 4 von Kommentaren befreit
(`instructions/helpers/okh-clean.py`). Ohne einen Ort für die Rechnung wäre die
Zahl danach unbelegt.

### Was zu tun ist

1. In `docs/de/bom.md` (und, falls vorhanden,
   `docs/de/parametrisch/bom.tpl.md`) nach den Bauteiltabellen den Abschnitt
   *Masse* einfügen: Gesamtmasse als Tabellenzeile, darunter die Rechnung —
   Volumen je Bauteil aus dem Modell × Rohdichte, plus Kleinteile, aufgerundet.
2. Die Rechnung aus dem Kommentar der `okh.toml` dorthin übernehmen, **bevor**
   `okh-clean.py` läuft.
3. `heimeliq-template-version = "0.9.3"` setzen.

---

## 0.9.1 → 0.9.2

Kein Breaking Change. Die `REUSE.toml` wird im Produkt-Repo angepasst — bisher
verlangte das keine Anweisung, weshalb sie dort noch der Vorlagenstand ist.

### Warum

Zwei Angaben stimmen im Produkt-Repo nicht. Die Copyright-Zeile steht noch auf
`FIXME-Jahr FIXME Vorname Nachname (FIXME-nickname) <FIXME@heimeliq.de>`. Und
die Pfadlisten sind die der Vorlage: `README.md`, `LICENSE` und `CHANGELOG.md`
des Produkts stehen dort unter MIT, obwohl es die Dateien des Möbels sind,
während unter CERN-OHL-S-2.0 `README.example.md`, `LICENSE.example` und
`changelog.md` stehen — Dateien, die es nach Phase 2 nicht mehr gibt.

### Was zu tun ist

1. Copyright-Zeile in beiden Blöcken setzen, Form `<Jahr> <Vorname Nachname>
   <Kontakt>` — dieselbe Angabe wie `licensor` in der `okh.toml` und wie die
   Copyright-Zeile im `LICENSE`. Kein Nickname.
2. MIT-Block auf das eindampfen, was nichts über das Möbel aussagt:
   `REUSE.toml`, `heimeliq.schema.json`, `.github/workflows/**`, `.gitignore`.
3. CERN-OHL-S-2.0-Block: `README.md`, `LICENSE`, `CHANGELOG.md`, `okh.toml`,
   `heimeliq.toml`, `docs/**`, `cad/**`, `media/**`, `**/.gitkeep`.
   Die `.example`-Pfade, `changelog.md` und `MIGRATIONS.md` entfallen.
4. **Gegenprobe, nicht Augenmaß:** Jede versionierte Datei wird von genau einem
   der beiden Blöcke erfasst, keine von beiden. `.gitkeep` als nackter Name
   trifft nichts, und `docs/**` deckt je nach Matcher keine Dateien ab, die mit
   einem Punkt beginnen — deshalb der eigene Eintrag `**/.gitkeep`.
5. `heimeliq-template-version = "0.9.2"` setzen.

---

## 0.9.0 → 0.9.1

Kein Breaking Change. Verweise auf Dateien, die es nur im privaten
Instructions-Repo gibt, verschwinden aus den öffentlichen Dokumenten.

### Warum

`docs/de/bom.md` schickte den Leser für die Frage, welche Teile aus einem Brett
kommen müssen, in die `INSTRUCTIONS.md`. Die liegt im privaten Repo; wer das
Produkt-Repo öffnet, kommt dort nie an. Die Antwort stand ohnehin in derselben
Datei, in der Tabellenzeile *Betroffene Teile*.

### Was zu tun ist

1. Im Abschnitt *Mindestkantenlänge* von `docs/de/bom.md` und
   `docs/de/parametrisch/bom.tpl.md` den Verweis auf die `INSTRUCTIONS.md`
   durch den Verweis auf die Tabellenzeile *Betroffene Teile* ersetzen. Im
   Fußnotensatz zu Sägezugabe und Besäumung den Pfad
   `instructions/helpers/zuschnitt.py` streichen — die 4 mm bleiben.
2. In `README.md`, `heimeliq.toml` und `heimeliq.schema.json` die Zeiger auf
   `instructions/reference/produkt-modell.md` streichen.
3. Damit fällt die Stelle weg, die das Baugruppen-Kriterium richtiggestellt
   hätte. Deshalb in `README.md` und in den Kommentaren über `[[assemblies]]`
   das alte Kriterium („starre, fest gefügte Einheit — was sich nicht zerlegen
   lässt, ohne Leim zu brechen") durch das geltende ersetzen: Eine Baugruppe
   ist, was sich als Einheit gegenüber den anderen bewegt oder getrennt
   montiert wird. Ein Klappdeckel ist ein einzelnes Brett und trotzdem eine
   eigene Baugruppe; ein fest verschraubter Innenboden ist keine.
4. `heimeliq-template-version = "0.9.1"` setzen.

Nicht gestrichen werden Sätze, die sagen, dass Serienwerte, Typenliste und
Tag-Achsen zentral im Instructions-Repo liegen. Sie benennen den Ort der
Wahrheit, sie fordern niemanden auf, dort eine Datei zu öffnen.

---

## 0.8.0 → 0.9.0

Kein Breaking Change. Eine Rechnung in der Stückliste wird von einem Einzelfall
zur Regel.

### Warum

`docs/de/bom.md` schrieb `L_min = 2 × Außenhöhe + Außenbreite + Sägezugabe`.
Das ist die Summe für eine bestimmte Form und stimmte nicht einmal für die Box,
neben der sie entstand: Deren vier Gehrungszargen ergeben 2 × 230 + 2 × 160 =
780 mm, die Formel nur 530. Wer danach einkauft, hat 250 mm zu wenig Brett.

### Was zu tun ist

Im Abschnitt *Mindestkantenlänge* von `docs/de/bom.md` und
`docs/de/parametrisch/bom.tpl.md` die Formel durch die Regel ersetzen: Das
Brett muss so lang sein wie die unter *Durchgehende Maserung* benannten Teile
hintereinander, plus Sägezugabe je Schnitt. Die konkrete Rechnung des Produkts
gehört ausgeschrieben daneben.

Die Tabelle darunter fragt nicht mehr nach Außenhöhe, Außenbreite und Tiefe,
sondern nach den betroffenen Teilen, der Rechnung, den Zugaben und den beiden
Ergebnissen. Wer sie schon gefüllt hat: Die Zahlen bleiben, nur die Zeilen
ändern sich.

**Bei der Gelegenheit prüfen, ob die eigene Rechnung stimmt** — sie stand in
jedem Repo, das aus dieser Vorlage entstanden ist.

Danach `heimeliq-template-version = "0.9.0"` setzen.

---

## 0.7.0 → 0.8.0

Kein Breaking Change. Zwei optionale Felder kommen dazu, und einige Texte werden
richtiggestellt.

### Was zu tun ist

Nichts zwingend. Wer mitziehen will:

1. In der `heimeliq.toml` die Kommentare über `[[assemblies]]` gegen die
   aktuelle Fassung tauschen. Die alte behauptet, `A001` sei das ganze Produkt —
   das stimmt nicht: `A001` ist die erste starre Baugruppe, das Produkt ist das
   Repo und hat keine A-Nummer.
2. Prüfen, ob Beschläge an der richtigen Baugruppe hängen. Was ein angebautes
   Teil hält — Scharniere, Schienen, Drehpunkte — gehört zu diesem Teil, nicht
   zum Korpus.
3. Wo mehrere gleiche Bauteile einzeln aufgezählt sind, zu einem `[[part]]` mit
   `quantity` zusammenfassen.
4. `heimeliq-template-version = "0.8.0"` setzen.

### Was neu möglich ist

`[[variants.option]].bestueckung` nimmt auf, was kein Skalar ist: welche
Rasterpositionen einen Boden tragen, welches Fach eine Tür bekommt. Die Form ist
je Produkt frei. Die Sperre in `validate.yml` bleibt auf `parameter` beschränkt
und greift unverändert.

Die Begriffe — Serie, Produkt, Ausführung, Referenzausführung, Baugruppe,
Bauteil — stehen in der README des instructions-Repos, die Regeln in
`instructions/reference/produkt-modell.md`.

---

## 0.6.0 → 0.7.0

Kein Breaking Change. Nur die Stückliste ändert sich, und zwar in Richtung weniger
Arbeit: Der Abschnitt *Plattengrößen-Vergleich und Verschnitt* entfällt.

Er verglich drei Plattenlängen (2000, 2600, 3000 mm) gegen den Bedarf. Die Zahlen
standen für kein Angebot, und die Plattenbreite blieb ein Platzhalter — die Tabelle
konnte also für keine reale Platte stimmen. Welche Platte es wird, entscheidet sich
beim Einkauf anhand der Angebote, die dann gelten.

### Was zu tun ist

In `docs/de/bom.md` den Abschnitt *Plattengrößen-Vergleich und Verschnitt* durch
*Welche Platte es wird* aus der aktuellen Vorlage ersetzen. Dasselbe in
`docs/de/parametrisch/bom.tpl.md`. Das entfernt sechs FIXME.

`L_min` und `B_min` bleiben unverändert — sie folgen aus dem Produkt, nicht aus
dem Angebot.

Danach `heimeliq-template-version = "0.7.0"` setzen.

Wer die alte Tabelle bereits mit echten Zahlen gefüllt hat, darf sie behalten;
dann nur die Versionsnummer ziehen.

---

## 0.5.1 → 0.6.0

Breaking Change am Namensschema und am Varianten-Modell. Die Familie wird zur **Serie**
und trägt ab jetzt das Markenvokabular; Varianten dürfen sich in der Innenaufteilung und
der Bauteilauswahl unterscheiden.

### 1. Repo umbenennen

`<family>-<type>` → `<series>-<type>`, z. B. `wieke-sideboard` → `gehriq-sideboard`. Auf
GitHub in den Settings; die alte URL bleibt eine Weile als Redirect. Anschließend im
`heimeliq-website`-Repo den Eintrag in `product-repos.json` nachziehen.

Ein **drittes Segment** (`<series>-<type>-<zusatz>`) ist ab jetzt erlaubt, aber die
Ausnahme: nur wenn zwei eigenständige Konstruktionen derselben Serie denselben Typ
hätten. Es ist frei benannt und keine Laufnummer.

### 2. `heimeliq.toml` – Feld für Feld

| bisher | künftig |
| --- | --- |
| `[family]` mit `id`, `label` | `[series]` mit denselben Feldern; `id` ist der Serien-Slug aus dem Markenvokabular (`gehriq` statt `wieke`) |
| `slug = "<family>-<type>"` | `slug = "<series>-<type>"`, optional mit drittem Segment |
| `[[variants.option]]` mit `id`, `label`, `parameter` | zusätzlich `parts` (Pflicht): Liste der Bauteil-IDs dieser Variante |
| `[[variants.option]].id` musste mit einem Buchstaben beginnen | beliebiger Name, auch `1200x800` oder `3x4x3`; muss innerhalb des Produkts eindeutig sein |
| – | `[[assemblies]].bauform` neu (optional): benennt eine geteilte parametrische Quelle |
| `heimeliq-template-version = "0.5.1"` | `"0.6.0"` |

### 3. Varianten prüfen

Zwei Regeln gelten ab jetzt und werden von `validate.yml` erzwungen:

- **Alle Optionen haben denselben Satz von `parameter`-Schlüsseln.** Nur die Werte dürfen
  sich unterscheiden. Hat eine Option einen Schlüssel mehr, ist es kein Variante, sondern
  ein eigenes Produkt – dann ein eigenes Repo anlegen.
- **Options-IDs sind eindeutig** innerhalb des Produkts.

Im Gegenzug entfällt die alte Regel „identische Teileliste". Ändert sich die Anzahl
gleichartiger Innenteile zwischen zwei Größen, ist das jetzt eine Variante: die Anzahl
wird als Parameter geführt (`FaecherMitte = 4`), damit bleibt der Schlüsselsatz gleich
und die Teileliste darf länger werden.

Bauteilmaße und Stückzahlen gehören **nicht** in `parameter` – dort stehen nur die freien
Eingangswerte, alles Abgeleitete rechnet der Generator.

### 4. Tag-Achsen

Die Achsen in `[tags]` heißen jetzt genauso wie im zentralen Vokabular. Bisher
trugen nur `material` und `status` denselben Namen auf beiden Seiten:

| `heimeliq.toml` (unverändert) | `vocabulary/tags.toml` bisher |
| --- | --- |
| `joint` | `verbindung` |
| `species` | `holzart` |
| `tooling` | `werkzeug` |
| `effort` | `aufwand` |
| `property` | `eigenschaft` |

In der `heimeliq.toml` ändert sich dadurch **nichts** – die Schlüssel hießen dort
schon immer so. Wer Werte aus dem Vokabular übernommen hat, prüft nur, ob sie
unter der richtigen Achse stehen.

Die Achse `bauart` ist ersatzlos gestrichen. Ihre Marken-Werte
(`massiq`/`gehriq`/`keiliq`) stecken jetzt als Serie in der ID; `korpusbau` und
`rahmenbau` entfallen. Aus einem Produkt-Repo war die Achse ohnehin nie
schreibbar, weil das Schema keine unbekannten Achsen zulässt.

`vocabulary/typen.toml` heißt jetzt `types.toml`. Betrifft nur, wer die Datei
direkt referenziert – der `type`-Wert in der `heimeliq.toml` bleibt derselbe.

### 5. `okh.toml`

`repo` auf das neue Namensschema setzen. Keine weiteren Pflichtänderungen.

### 6. Instructions-Repo

Das zugehörige Produkt-Verzeichnis heißt jetzt `products/<series>-<type>/`, die Serie
liegt unter `series/<id>/`. `heimeliq-instruction-version` zeigt nach dem nächsten
Release auf einen Tag im neuen Namensschema (`gehriq-sideboard-v1.0.0`).

---

## 0.5.0 → 0.5.1

This is a PATCH release. No structural, schema, or directory changes are required.

1. **`heimeliq-template-version`** in `heimeliq.toml` erhöhen auf `"0.5.1"`.

Nur Terminologie: „Möbel" heißt in Vorlage und Doku jetzt durchgängig „Produkt".
Bestehende Repos validieren und funktionieren auch ohne diese Anpassung
unverändert weiter; die Übernahme der neuen Wortwahl in eigene Texte ist optional.

---

## 0.4.2 → 0.5.0

Zwei Breaking Changes: das Namensschema (`series`/`forest` → `type`/`theme`/`family`) und die neue Pflicht-Section `[variants]`. Es gibt genau ein bestehendes Produkt-Repo; es wird von Hand nachgezogen. Kein Migrationsskript, keine Rückwärtskompatibilität.

### 1. Repo umbenennen

`heimeliq-<series>-<forest>` → `<family>-<type>`, z. B. `heimeliq-massiq-hambach` → `wieke-sideboard`. Das `heimeliq-`-Präfix entfällt. Auf GitHub in den Settings; die alte URL bleibt eine Weile als Redirect.

### 2. `heimeliq.toml` – Feld für Feld

| bisher | künftig |
| --- | --- |
| `series = "…"` | entfällt ersatzlos |
| `[forest]` inkl. `[[forest.links]]` | entfällt ersatzlos |
| `type = "…"` | bleibt, ist jetzt Teil der ID; Wert ist ein Slug aus `vocabulary/typen.toml` (heißt ab 0.6.0 `types.toml`) |
| – | `theme = "…"` neu (Pflicht); muss in der `themen`-Liste des `type` stehen |
| – | `[family]` neu (Pflicht): `id` (lowercase, ASCII), `label` (Anzeigeform) |
| `tags = ["a", "b"]` | `[tags]` mit sieben Achsen: `joint`, `species`, `material`, `tooling`, `effort`, `property`, `status`. Alte Werte auf die passende Achse verteilen, Rest verwerfen. |
| `status = "published"` | als Wert in die Achse `tags.status` (`status = ["published"]`) |
| `slug = "<series>-<forest>"` | `slug = "<family>-<type>"` |
| – | `[variants]` neu (Pflicht): `reference` + mindestens eine `[[variants.option]]` mit `id`, `label`, `parameter`. Ohne Größenauswahl genau eine Option, deren `id` gleich `reference` ist. |
| `heimeliq-template-version = "0.4.2"` | `"0.5.0"` |

Die `parameter`-Schlüssel jeder Option müssen den Alias-Namen der FreeCAD-Spreadsheet-Zellen entsprechen.

### 3. `okh.toml`

- `repo` auf das neue Namensschema setzen.
- Keine weiteren Pflichtänderungen. Die `outer-dimensions` beschreiben ab jetzt ausdrücklich die Referenzvariante (Kommentar in der Datei).

### 4. Ordnerstruktur

- `media/variants/<id>/` je Varianten-ID anlegen (mindestens für die Referenzvariante), oder leer lassen – Fallback ist `media/gallery/`.
- `docs/de/parametrisch/` mit `build-guide.tpl.md` und `bom.tpl.md` aus dieser Vorlage übernehmen und an das Produkt anpassen.
- `docs/de/build-guide.md` und `docs/de/bom.md` mit dem Kopfhinweis versehen; sie enthalten die ausgerechnete Referenzvariante.

### 5. Validierung und Website

- Lokal `validate.yml` nachvollziehen. Häufige Fehler: fehlendes `theme`, `[family]` oder `[variants]`; `tags.status` statt Top-Level `status`; `variants.reference` zeigt auf keine Options-`id`.
- Im Website-Repo `product-repos.json`: die alte URL gegen die neue tauschen.
- `changelog.md` des Produkts (klein) ergänzen.

### Offene Punkte

- `vocabulary/typen.toml` im Instructions-Repo hat noch deutsche Schlüssel und wird separat nachgezogen.
- `validate.yml` prüft `type`/`theme` noch nicht gegen das Vokabular (braucht Lesezugriff auf das Instructions-Repo).

---

## 0.4.1 → 0.4.2

This is a PATCH release. No structural, schema, or directory changes are required.

1. **`heimeliq-template-version`** in `heimeliq.toml` erhöhen auf `"0.4.2"`.

Optional (empfohlen für Konsistenz, nicht erzwungen): bestehende `docs/de/bom.md` und `README.md` auf die Zuschnitt-Notation `L × B × S` umstellen (Materialstärke immer zuletzt) und – bei gehriq-Produkten – den Abschnitt „Hinweis zur Holzauswahl" ergänzen. Bestehende Repos validieren und funktionieren auch ohne diese Anpassung unverändert weiter.

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

1. **Assemblies in `heimeliq.toml` ergänzen**: Mindestens die Hauptbaugruppe `A001` als `[[assemblies]]`-Eintrag eintragen, mit `source` auf die FreeCAD-Datei und `optional = false`. Falls das Produkt Erweiterungen hat (z. B. eine Schublade), für jede Erweiterung eine eigene Sub-Baugruppe `A002`, `A003`, … mit `parent = "A001"` und `optional = true` ergänzen.

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

Diese Version führt das **Wald-Namensgeber-Konzept** ein und verschlankt das ID-Schema. Bestehende Produkt-Repos (typischerweise das v0.1.x-Pilotprodukt) sollten so migriert werden:

1. **Repo umbenennen** auf das neue Schema `heimeliq-<reihe>-<waldname>`. Beispiel: `heimeliq-massiq-sideboard-001` → `heimeliq-massiq-hambach`. Auf GitHub geht das in den Settings; die alte URL bleibt eine Weile als Redirect bestehen.

2. **`heimeliq.toml` anpassen**:
   - `slug` auf `<reihe>-<waldname>` setzen (z. B. `"massiq-hambach"`).
   - `type` bleibt erhalten, aber jetzt als Metadatenfeld (z. B. `"sideboard"`).
   - Optional: `tags = ["..."]` ergänzen.
   - Neue Pflicht-Section `[forest]` ergänzen – mindestens `id`, `name`, `region`, `country` ausfüllen. Optionale Felder (`forest_type`, `age_estimate_years`, `status`, `themes`, `links`, `note`) nach Möglichkeit ebenfalls befüllen.
   - `heimeliq-template-version` auf `"0.2.0"` heben.

3. **README im Produkt-Repo aktualisieren**: Den Wald-Namensgeber-Bereich aus der neuen `README.example.md` übernehmen und ausfüllen.

4. **Validate-Action lokal oder via Push prüfen**: Schlägt die Validierung an, fehlt vermutlich ein Pflichtfeld in `[forest]` oder der `slug` passt nicht zum neuen Pattern.

5. **`product-repos.json` im Website-Repo aktualisieren**: Die alte URL gegen die neue tauschen.

6. **CHANGELOG.md des Produkts** (klein, im Produkt-Repo) ergänzen mit einem Eintrag wie:

   ```
   ## [0.2.0] – Wald-Namensgeber ergänzt, Repo umbenannt
   - Repo-Name: heimeliq-massiq-sideboard-001 → heimeliq-massiq-hambach
   - [forest]-Section in heimeliq.toml ergänzt
   - Template-Version 0.2.0
   ```

---

## 0.x → 1.0 (noch nicht erschienen)

*Wird ergänzt, sobald die erste Major-Version veröffentlicht wird.*
