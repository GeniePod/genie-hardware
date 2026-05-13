# Enclosure

Mechanical CAD for the physical box that holds the Jetson, mic frontend,
speaker, and wiring.

## Status

`empty` — nothing here yet. The first iteration will be a 3D-printable
"developer kit" enclosure: cosmetic but functional, prints in PLA on a
hobby printer, no fasteners beyond M3 inserts.

## What goes here

```
enclosure/
├── README.md                            (this file)
├── developer-kit-v0p1.f3d               (Fusion 360 source)
├── developer-kit-v0p1.step              (neutral exchange format)
├── developer-kit-v0p1-top.stl           (ready to slice)
├── developer-kit-v0p1-bottom.stl
├── developer-kit-v0p1-mic-grille.stl
├── developer-kit-v0p1-speaker-grille.stl
└── renders/
    ├── developer-kit-v0p1-exploded.png
    ├── developer-kit-v0p1-section.png
    └── developer-kit-v0p1-photo.jpg     (printed unit, on a desk)
```

## Mechanical constraints to honor

- **Jetson Orin Nano Super Devkit:** ~103 × 90.5 × 34 mm. Active fan
  intake under the heatsink wants ≥ 10 mm of vertical clearance plus a
  side vent.
- **LyraT V4.3:** ~80 × 60 mm. Three onboard mics on its top face —
  the enclosure must NOT block them.
- **Speaker port** sized for whichever speaker the BOM settles on
  (currently a small powered USB speaker).
- **Cable strain relief** for: power, USB, Ethernet, optional HDMI.
- **Status indicator hole** for the Jetson's onboard LEDs.
- **Mic-distance**: keep mics ≥ 8 cm from any speaker driver to give
  the half-duplex gate / future AEC a fighting chance (see genie-claw
  issues #15 and #23).

## Conventions

- **Tool:** Fusion 360 source (`.f3d`), STEP for neutral exchange,
  STL for direct slicing. Keep all three in sync — STEP is the
  interchange truth, STL is derived.
- **Print orientation** documented in a sidecar `.print.md` per part.
- **Licensing:** CERN-OHL-S v2 inherits to mechanical designs in this
  folder. STL files are the "preferred form for modification" only
  when STEP/F3D are also present in the repo.

## Related

- [`../pcb/`](../pcb/) — board outlines and connector positions must
  match enclosure cutouts.
- [`../product-design/`](../product-design/) — industrial design
  language (color, finish, surface treatment) lives there. Enclosure
  CAD here is the functional implementation of that language.
