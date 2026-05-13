# MVP — Minimum Viable Product

The current shippable GenieClaw hardware stack, built from off-the-shelf
boards. Anyone with these parts and the wiring in this folder can have a
working local home AI assistant in an afternoon.

## What's here

- `bom.md` — bill of materials for the MVP build (~$500-700 USD).
- `wiring.md` — pin-by-pin connections between every component.
- `setup-checklist.md` — first-boot, flash, audio-route, voice-loop smoke test.

## What's NOT here

- Schematics for any custom interface board (those live in `../schematic/`).
- Custom PCB layouts (`../pcb/`).
- 3D-printable enclosures (`../enclosure/`).

The MVP is intentionally board-level. The repo's other folders graduate
it to integrated hardware later.

## Status

`alpha.7` — verified end-to-end on 2026-05-12 + 2026-05-13. See the
[alpha.7 verified voice cycle](https://github.com/GeniePod/genie-claw#alpha7-verified-voice-cycle-2026-05-13)
section in genie-claw's README.
