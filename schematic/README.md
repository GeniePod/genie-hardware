# Schematics

Circuit schematics for any custom interface boards that sit between
off-the-shelf modules (Jetson carrier, LyraT, ESP32-C6) and integrated
GeniePod Home V1 hardware.

## Status

`empty` — nothing here yet. The current
[MVP](../mvp/) uses board-to-board jumper wiring straight off the Jetson
40-pin header. The first scheduled custom board is:

1. **home-v1-interface-board v0.1** — small breakout that:
   - Routes Jetson 40-pin I2S2 to a JST-PH connector to the LyraT JP4
     (so the cable is captive and labelled instead of loose Dupont
     jumpers).
   - Adds an optional ESP32-C6 footprint with proper UART level
     translation and a reset button.
   - Exposes 3.5 mm + USB audio passthrough.

When that lands, this folder will hold:
```
schematic/
├── README.md                  (this file)
├── home-v1-interface-board-v0p1.kicad_sch
├── home-v1-interface-board-v0p1.pdf   (rendered PDF for non-KiCad readers)
└── reference/
    ├── lyrat-v4.3-reference.pdf   (Espressif's published schematic for
    │                               reference / pin numbering)
    └── orin-nano-40pin.pdf
```

## Conventions

- **Tool:** KiCad 8.x. Project files committed alongside rendered PDFs
  so the design is readable without KiCad installed.
- **Net naming:** match the LyraT and Jetson SoC GPIO names verbatim
  (e.g. `JETSON_I2S2_LRCK`, `LYRAT_JP4_SCLK`). Makes
  [`../mvp/wiring.md`](../mvp/wiring.md) and the schematic line up word
  for word.
- **Licensing:** CERN-OHL-S v2 (this whole repo). KiCad files inherit.

## Related

- [`../pcb/`](../pcb/) — board layouts derived from these schematics.
- [`../enclosure/`](../enclosure/) — mechanical envelope these boards
  must fit inside.
