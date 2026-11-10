# Glutfaden

Ein **Kreuzstich-Editor in Drachenhauch** mit GTK 3 als Oberfläche: Muster
zeichnen und bearbeiten, Garne aus 19 Herstellerpaletten, Teil- und
Rückstiche, Ebenen, Bilder in Muster umwandeln, Export als PDF, HTML und OXS,
Drucken, helles und dunkles Thema.

Glutfaden ist die Portierung von [PySticky](https://github.com/HasoSchno70/Pysticky)
(Python + PySide6) nach [Drachenhauch](https://github.com/HasoSchno70/Drachenhauch),
einem modernen BASIC. Das Dateiformat bleibt `.pxs`, PySticky und Glutfaden
lesen also dieselben Dateien.

Bis November 2026 lag Glutfaden in Drachenhauch unter `examples/glutfaden/`;
die Geschichte ist mitgekommen. Verweise wie `HasoSchno70/Drachenhauch#432` in
den Commits zeigen auf die Pull Requests von damals, die ausführliche
Entwicklungsgeschichte aller Stufen steht in Drachenhauch unter
[`geschichte/glutfaden.md`](https://github.com/HasoSchno70/Drachenhauch/blob/main/geschichte/glutfaden.md).

## Voraussetzungen

- **Drachenhauch 2026.45 oder neuer**: das Paket von der
  [Release-Seite](https://github.com/HasoSchno70/Drachenhauch/releases/latest)
  bringt `dhrt` mit.
- **GTK 3**: unter Linux fast immer vorhanden (`libgtk-3-0`), unter macOS über
  Homebrew (`brew install gtk+3`), unter Windows aus MSYS2 im PATH oder aus
  einem Programm, das es mitbringt (Inkscape, GIMP). Die Bibliotheksnamen in
  `gtk/gtk.dh` nennen diese Fundorte.

## Starten

```
dhrt run main.dh                     # Beispielmuster
dhrt run main.dh -- muster.pxs       # eine Datei öffnen
```

## Aufbau

```
main.dh     Fenster, Menüs, Hauptschleife
kern/       Muster, Ebenen, Garne, Paletten, Sticharten, Dateiformate
            (pxs, OXS, PCStitch, Pattern Maker), Bildimport, Export
ansicht/    Zeichenfläche, Seitenleiste, Dialoge, Druck, Plugins
gtk/        Deklarationen für GTK 3, GDK, Cairo, Pango und GLib
daten/      Paletten, Symbole, Beispielmuster, Übersetzung
tests/      Prüfsammlungen für `dhrt test`
```

## Prüfen

```
dhrt test tests/pruef
```

läuft alle Sammlungen (ein Teil öffnet echte GTK-Fenster, dafür braucht es
einen Bildschirm). Die CI (`.github/workflows/pruefen.yml`) prüft den Kern
ohne Fenster gegen die neueste Drachenhauch-Fassung.

**Plugins** nutzen die Bibliothek `dh_plugin.dh` aus der IDE von Drachenhauch.
Glutfaden findet sie in einer Installation von Drachenhauch, neben einer selbst
gebauten `dhrt` im Drachenhauch-Repo oder in einem Ordner `Drachenhauch`
neben diesem Repo.

## Lizenz

Wahlweise [MIT](LICENSE-MIT) oder [Apache 2.0](LICENSE-APACHE), wie Drachenhauch
selbst. Die Teile aus PySticky stehen unter dessen MIT-Lizenz
(`daten/LIZENZ-PySticky.txt`); zur Herkunft der Garnpaletten siehe
`daten/HERKUNFT-Paletten.txt`.
