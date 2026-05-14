# MVP Bill of Materials

Last verified: 2026-05-13. Prices and SKUs drift; treat this as a
hardware-class shopping list, not a commerce link sheet.

## Core (required)

| Part | Role | Approx USD | Notes |
| --- | --- | --- | --- |
| **NVIDIA Jetson Orin Nano Super Developer Kit (8 GB)** | Compute + iGPU for LLM, STT, TTS | $499 | SM 8.7, 102 GB/s LPDDR5, 67 TOPS GPU. Includes carrier + module + heatsink + power supply. |
| **ESP32-LyraT V4.3** | I2S capture frontend (ES8388 codec, onboard mic array) | $30-40 | Espressif dev board. Drives JP4 header → Jetson 40-pin. |
| **microSD card, 64 GB+, A2, U3** | Jetson root + model storage | $15 | SanDisk Extreme Pro or Samsung EVO Plus class. NVMe is faster if your carrier supports it. |
| **USB-A headphone or 3.5 mm-jack speaker** | TTS output | $5-30 | Anything ALSA can see. USB-C headset works with an adapter. |
| **Cooling: Jetson active heatsink + fan** | Sustained inference | $0 | Included in Super Devkit. |

## Wiring (required, cheap)

| Part | Role | Approx USD |
| --- | --- | --- |
| **40-pin GPIO ribbon cable + Dupont jumpers** | Jetson 40-pin header → LyraT JP4 (4 wires) | $5 |
| **USB-micro-B cable** | LyraT flash + power | $0 (have one) |
| **USB-C → USB-A or Ethernet** | Jetson networking during setup | $0 (have one) |

## Optional accessories

| Part | Role | Approx USD | Notes |
| --- | --- | --- | --- |
| **40-pin GPIO breakout / expansion board** | Wiring sanity | $5-10 | The Jetson 40-pin pins are too tightly spaced to keep loose Dupont jumpers reliable. A passive breakout (Raspberry Pi-style "GPIO header expansion board" works fine on the Jetson) turns it into a labelled terminal block. **Shown in the hero photo.** Strongly recommended even though it's listed as optional. |
| **ESP32-C6 dev board** | Thread/Matter sidecar | $10-15 | Connects via UART (`/dev/ttyTHS1`). Wires the assistant into a Thread/Matter home fabric. |
| **HDMI display + cable** | First-boot setup, NoMachine alternative | $0-100 | Headless install via SSH works fine; display only helps for first-flash. |
| **USB keyboard + mouse** | First-boot setup | $0 | Same — optional. |
| **HiFiBerry MiniAmp / similar I2S amp** | Higher-fidelity speaker output | $20 | If you outgrow USB audio. |
| **External speakers (powered or amplified)** | Loud TTS | $20-100 | Anything with a 3.5 mm or USB input. |

## Total

- **Bare minimum core (Jetson + LyraT + speaker + SD):** ~$550
- **With Thread/Matter sidecar + nicer speaker:** ~$600-700
- **With display + keyboard for first-boot:** add ~$100

## Notes

- ESP32-LyraT firmware: custom IDF example `lyrat_jp4_passthrough`,
  proposed for upstream inclusion in
  [espressif/esp-adf#1607](https://github.com/espressif/esp-adf/issues/1607).
  Until merged, build it from a local clone of
  [espressif/esp-adf](https://github.com/espressif/esp-adf). Flashing
  instructions live in `setup-checklist.md`.
- Don't substitute the LyraT with a generic USB conference mic for the
  reference build — the half-duplex gate and DFN tuning in genie-claw
  alpha.7 are validated against the LyraT I2S path specifically. USB mics
  work but expect to re-tune `post_tts_silence_ms` and acoustic isolation.
