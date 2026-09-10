<!--
  Vorlage für docs/de/build-guide.md. Aus dieser Datei wird die Bauanleitung
  der Referenzvariante erzeugt.

  Regeln:
  - Platzhalter ausschließlich als {{ name }}. Keine Logik – keine Schleifen,
    keine Bedingungen, keine Rechenausdrücke.
  - Zuschnittmaße und daraus abgeleitete Werte werden nicht hier gerechnet,
    sondern als fertiger benannter Wert eingesetzt. Dasselbe gilt für
    Stückzahlen: in heimeliq.toml stehen nur die freien Eingangswerte, alles
    Abgeleitete rechnet der Generator.
  - {{ … }} füllt der Generator aus den Variantenparametern. FIXME füllt ein
    Mensch (Prosa, Werkzeugliste, Zeitangaben, Beschreibung der Schritte).
-->
# Bauanleitung – {{ product_name }}

*Referenzvariante: {{ variant_label }}. Diese Anleitung richtet sich an einen
Tischler oder eine Tischlerin mit Werkstatt-Erfahrung. Sie geht davon aus,
dass übliche Werkzeuge und Maschinen vorhanden sind und übliche Verbindungen
beherrscht werden.*

## Vorbereitung

### Material

Komplette Stückliste siehe [bom.md](bom.md). Hier nur die Übersicht:

- FIXME Holzart, Brettstärken
- FIXME externe Teile (Schrauben, Beschläge)

### Werkzeuge

FIXME: Welche Werkzeuge sind erforderlich? Was ist gut zu haben?

### Geschätzter Zeitaufwand

FIXME: Stunden, gegliedert nach Phasen (Zuschnitt, Bearbeitung, Montage,
Oberfläche).

## Zuschnitt

Zuschnittliste der Variante {{ variant_label }} (L × B × S, mm):

| Bauteil | Länge | Breite | Stärke | Anzahl |
| --- | --- | --- | --- | --- |
| FIXME | {{ s001_length }} | {{ s001_width }} | {{ s001_thickness }} | {{ s001_quantity }} |
| FIXME | {{ s002_length }} | {{ s002_width }} | {{ s002_thickness }} | {{ s002_quantity }} |

FIXME: Reihenfolge, Bezugskanten, Aufmaße.

## Bearbeitung der Einzelteile

FIXME: Verbindungen herstellen, Aussparungen, Bohrungen. Bilder unter
`build-guide.images/` ablegen.

Nut für die Rückwand: {{ groove_width }} mm breit, {{ groove_depth }} mm
tief, {{ groove_offset }} mm von der Hinterkante.

## Probemontage (Trockenpassung)

FIXME: Was wird in der Probemontage geprüft? Welche Stellen sind kritisch?

## Oberflächenbehandlung

FIXME: Vor oder nach der Montage? Welches Mittel?

## Endmontage

FIXME: Reihenfolge der Endmontage, Klebstoffeinsatz, Zwingen-Setup.

## Qualitätsprüfung

Fertigmaße der Variante {{ variant_label }}: {{ outer_width }} × {{ outer_depth }}
× {{ outer_height }} mm (B × T × H).

FIXME: Was wird sonst geprüft? Funktion, Oberfläche.
