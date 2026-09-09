# media/variants/

Variantenspezifische Bilder. Ein Unterordner je Varianten-ID aus
`heimeliq.toml` → `[[variants.option]]`:

```
media/variants/
  klein/
  mittel/
  gross/
```

## Fallback

Sucht ein Renderer ein Bild für eine bestimmte Variante, gilt: zuerst
`media/variants/<id>/`, sonst `media/gallery/`. Ein Bild, das für alle
Varianten passt, liegt in `media/gallery/` und wird hier nicht dupliziert.

## Dateinamen

Laufende Nummer als Präfix für die Reihenfolge, danach ein sprechender Name
in kebab-case, ohne Umlaute:

```
01-front.jpg
02-detail-gehrung.jpg
```

## Nicht ins Git

Shop-Bilder in voller Auflösung gehören nicht in dieses Repository. Wie sie
verwaltet werden, ist noch offen und hier bewusst nicht gelöst.
