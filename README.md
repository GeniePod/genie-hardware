# genie-hardware

Hardware documentation for **GeniePod Home V1**.

Current status: **MVP testing**. The working reference build uses
off-the-shelf development boards, hand wiring, and the current GeniePod
software stack. Custom PCB, enclosure, and product-design assets are planned,
but they are not the source of truth yet.

## Home V1 Target Hardware

GeniePod Home V1 is the first integrated home appliance target. The MVP in
this repo validates the stack with dev boards first; the custom Home V1
hardware is expected to consolidate those functions into a purpose-built
carrier, enclosure, and audio layout.

| Subsystem | Home V1 direction |
| --- | --- |
| Compute | Jetson Orin Nano-class SoM running the GeniePod voice stack, LLM runtime, and local services |
| Audio input | 4 analog microphones in a far-field array, with a dedicated audio ADC/front end and physical mute path |
| Audio output | 2-speaker playback path for voice responses, alerts, and room audio testing |
| Storage | Onboard M.2 NVMe SSD for the OS image, models, logs, configuration, and OTA staging |
| Security | TPM 2.0 security module for device identity and future sealed-storage / disk-encryption flows |
| Wireless | WiFi and BLE connectivity for setup, local network access, and device management |
| Thread / Matter | Thread border-router path using a radio co-processor connected to the Jetson host |
| Status lighting | RGBW LED status system for wake, listening, processing, muted, error, setup, and idle states |
| Physical controls | Hardware microphone mute, volume controls, and a setup/pairing control |
| External I/O | USB-C power, Ethernet, and hidden service/debug USB access; no public display output in V1 |
| Enclosure | Voice-first home form factor with top mic zone, separated speaker path, visible privacy/status cues, and rear/bottom I/O |

![Hero — GeniePod Home V1 MVP wiring](images/hero-mvp.jpg)

> **Verified MVP:** Jetson Orin Nano Super + ESP32-LyraT V4.3, tested with
> `genie-claw` alpha.7 on 2026-05-13.

## Scope

This repo is only about **GeniePod Home V1** hardware.

It currently documents:

1. **MVP testing build** — the board-level setup that works today.
2. **Home V1 interface board** — planned replacement for loose jumper wiring.
3. **Home V1 enclosure** — planned developer enclosure around the MVP stack.
4. **Home V1 product design** — planned industrial-design notes for this device.

It does not define other GeniePod products or future SKUs.

Everything here is licensed [CERN-OHL-S v2](LICENSE.md).

## MVP System

```mermaid
flowchart LR
    subgraph HW["GeniePod Home V1 MVP hardware"]
        LyraT["ESP32-LyraT V4.3<br/>ES8388 + onboard mics<br/>I2S slave"]
        ORIN["Jetson Orin Nano Super<br/>8 GB, CUDA 12.6<br/>SM 8.7"]
        SPK["USB / 3.5 mm speaker"]
        C6["ESP32-C6 sidecar<br/>optional Thread / Matter test"]
    end

    subgraph SW["GeniePod software"]
        CLAW["genie-claw<br/>voice loop, memory, tools"]
        RUNTIME["genie-ai-runtime<br/>Orin LLM runtime"]
    end

    LyraT -- "I2S (24 kHz S16 stereo)" --> ORIN
    C6 -- "UART /dev/ttyTHS1" --> ORIN
    ORIN -- "ALSA output" --> SPK
    ORIN --- CLAW
    CLAW -- "HTTP :8080" --> RUNTIME

    classDef hw fill:#1f2937,stroke:#111827,color:#f9fafb;
    classDef sw fill:#fb923c,stroke:#7c2d12,color:#1c1917;
    classDef opt stroke-dasharray: 5 5;
    class LyraT,ORIN,SPK,C6 hw;
    class CLAW,RUNTIME sw;
    class C6 opt;
```

## Folder Map

| Folder | Status | What it holds |
| --- | --- | --- |
| [`mvp/`](mvp/) | working MVP test build | BOM, wiring, and setup notes for the off-the-shelf reference build |
| [`schematic/`](schematic/) | planned | KiCad schematics for the Home V1 interface board |
| [`pcb/`](pcb/) | planned | PCB layouts, Gerbers, fab outputs, and renders |
| [`enclosure/`](enclosure/) | planned | CAD for the Home V1 MVP/developer enclosure |
| [`product-design/`](product-design/) | planned | Home V1 industrial-design and packaging notes |
| [`images/`](images/) | active | MVP photos and repo diagrams |

## MVP at a Glance

The current MVP test build:

| Component | Part | Approx USD |
| --- | --- | --- |
| Compute | Jetson Orin Nano Super Devkit (8 GB) | $499 |
| Mic frontend | ESP32-LyraT V4.3 (ES8388 + 3 onboard mics) | $30-40 |
| Storage | microSD A2 U3 64 GB+ | $15 |
| Audio out | USB-A headphone or 3.5 mm speaker | $5-30 |
| Wiring | 40-pin GPIO ribbon + Dupont jumpers | $5 |
| **Total core MVP** | | **~$550** |

Optional for testing: ESP32-C6 sidecar for Thread/Matter, upgraded speakers,
and HDMI display for first boot.

Full BOM: [`mvp/bom.md`](mvp/bom.md)  
Wiring: [`mvp/wiring.md`](mvp/wiring.md)

## Bring-Up Sequence

```mermaid
flowchart TD
    A[Order MVP BOM] --> B[Install JetPack 6.2.1<br/>L4T R36.4.7, CUDA 12.6]
    B --> C[First boot and SSH access<br/>enable I2S2 with jetson-io.py]
    C --> D[Flash LyraT<br/>lyrat_jp4_passthrough firmware]
    D --> E[Wire LyraT JP4 to Jetson 40-pin<br/>I2S signals + GND]
    E --> F["Run GeniePod setup script<br/>install services, models, AHUB routes"]
    F --> G["Voice-loop smoke test<br/>push-to-talk response"]

    classDef start fill:#10b981,color:#022c22;
    classDef step fill:#f3f4f6,stroke:#9ca3af,color:#111827;
    classDef done fill:#fb923c,stroke:#7c2d12,color:#1c1917;
    class A start;
    class B,C,D,E,F step;
    class G done;
```

Full software setup lives in the
[genie-claw README](https://github.com/GeniePod/genie-claw), with the alpha.7
verification notes in the
[Alpha.7 Verified Voice Cycle](https://github.com/GeniePod/genie-claw#alpha7-verified-voice-cycle-2026-05-13)
section.

## Roadmap

- **Now:** MVP testing hardware documented and reproducible.
- **Next:** Home V1 interface-board v0.1 to replace loose jumpers with a
  labelled captive connector.
- **Then:** 3D-printable Home V1 developer enclosure around the MVP stack.
- **Later:** manufacturable Home V1 hardware package after the MVP behavior is
  stable.

## Related Repos

| Repo | What it is |
| --- | --- |
| [GeniePod/genie-claw](https://github.com/GeniePod/genie-claw) | Rust runtime: voice loop, memory, tools, Home Assistant integration. |
| [GeniePod/genie-ai-runtime](https://github.com/GeniePod/genie-ai-runtime) | Orin-tuned C++/CUDA LLM inference runtime. |
| [GeniePod/genie-os](https://github.com/GeniePod/genie-os) | Jetson OS and image tooling for the target hardware. |
| [GeniePod/genie-app](https://github.com/GeniePod/genie-app) | Companion client for setup and device management. |
| [espressif/esp-adf](https://github.com/espressif/esp-adf) | Upstream LyraT firmware framework. |

## License

CERN Open Hardware Licence Version 2 — Strongly Reciprocal. See
[LICENSE.md](LICENSE.md).
