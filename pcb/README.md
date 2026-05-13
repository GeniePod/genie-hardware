# PCB Layouts

Production-grade board layouts, derived from the schematics in
[`../schematic/`](../schematic/).

## Status

`empty` — nothing here yet. The schematics arrive first; the layout
follows once the interface-board schematic stabilizes.

## What goes here

```
pcb/
├── README.md                            (this file)
├── interface-board-v0p1.kicad_pcb
├── interface-board-v0p1.gerbers/        (manufacturing output)
├── interface-board-v0p1.drl             (drill file)
├── interface-board-v0p1.pos             (pick-and-place)
├── interface-board-v0p1-bom.csv         (assembly BOM for JLCPCB/PCBWay)
└── renders/
    ├── interface-board-v0p1-top.png
    ├── interface-board-v0p1-bottom.png
    └── interface-board-v0p1-3d.png
```

## Conventions

- **Tool:** KiCad 8.x. Gerbers + drill + position file committed
  alongside `.kicad_pcb` so the board is manufacturable without a KiCad
  install. PNG renders make GitHub previews useful.
- **Layer stack:** 4-layer for any board carrying I2S clocks at 24-48
  kHz with ESD protection on USB. 2-layer is fine for the simplest
  passthrough.
- **DFM target:** JLCPCB defaults unless a board specifically needs
  tighter tolerances. Document any deviation in this README.
- **Licensing:** CERN-OHL-S v2. Manufacturers who improve the layout
  must share back under the same license — that's the whole point of
  "strongly reciprocal."

## Related

- [`../schematic/`](../schematic/) — every board here has a schematic
  there with the same base name.
- [`../enclosure/`](../enclosure/) — verify board outline + connector
  positions match the enclosure CAD before sending Gerbers off.
