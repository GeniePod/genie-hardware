# GeniePod Home V1 Product Design

Industrial design, packaging, and physical UX notes for GeniePod Home V1.
This is distinct from `../enclosure/`, which is the mechanical implementation.

## Status

`empty` — nothing here yet. Earliest deliverables expected:

1. **Design language brief** — surface treatment, materials, primary
   accent color, typography for any printed/laser-etched marks.
2. **Home V1 front renders** — clear shots of the MVP/developer hardware.
3. **Owner unboxing flow** — step-by-step photos / icons of: open box
   → seat Jetson → connect cables → run setup script → first voice exchange.
4. **Packaging dieline** — outer carton + foam tray spec.

## What goes here

```
product-design/
├── README.md                            (this file)
├── design-language.md                   (brand brief, accent palette)
├── identity/
│   ├── logo.svg
│   ├── logo-monochrome.svg
│   ├── wordmark.svg
│   └── palette.md                       (hex values, usage rules)
├── renders/
│   ├── hero-front.png
│   ├── hero-three-quarter.png
│   ├── hero-with-laptop.png             (in-context scale shot)
│   └── exploded.png
├── unboxing/
│   ├── step-01-open-box.png
│   ├── step-02-seat-jetson.png
│   ├── ...
│   └── quick-start-card.pdf
└── packaging/
    └── outer-carton-dieline.svg
```

## Conventions

- **Render source files** (Blender / KeyShot / Fusion-rendered) are
  preferred-form-for-modification under CERN-OHL-S. Keep them
  alongside the rendered PNG/JPG, or note where they're externally
  archived if too large.
- **Color profile:** sRGB for screen renders, CMYK for any printed
  artwork. Filename suffix tells the reader: `*-srgb.png`,
  `*-cmyk.tif`.
- **Trademark vs license:** the GeniePod logo and wordmark may be trademarked
  separately from the CERN-OHL-S license
  on the hardware. Trademark policy will live alongside `identity/`
  when the first owned mark exists.

## Related

- [`../enclosure/`](../enclosure/) — implements this design language
  in mechanical form.
- [genie-claw](https://github.com/GeniePod/genie-claw) — runtime docs that use
  Home V1 hardware photos.
