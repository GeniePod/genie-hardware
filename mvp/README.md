# GeniePod Home V1 MVP

The current **GeniePod Home V1** MVP test hardware stack, built from
off-the-shelf boards. Anyone with these parts and the wiring in this folder can
reproduce the current board-level test build.

## What's here

- `bom.md` — bill of materials for the MVP build (~$500-700 USD).
- `wiring.md` — pin-by-pin connections between every component.
- `setup-checklist.md` — first-boot, flash, audio-route, voice-loop smoke test.

## What's NOT here

- Schematics for any custom interface board (those live in `../schematic/`).
- Custom PCB layouts (`../pcb/`).
- 3D-printable enclosures (`../enclosure/`).

The MVP is intentionally board-level. The repo's other folders graduate this
same GeniePod Home V1 hardware path toward an integrated board and enclosure.

## Status

`alpha.7` — verified end-to-end on 2026-05-12 + 2026-05-13. See the
[alpha.7 verified voice cycle](https://github.com/GeniePod/genie-claw#alpha7-verified-voice-cycle-2026-05-13)
section in genie-claw's README.
