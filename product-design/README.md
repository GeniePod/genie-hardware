# Product Design

Industrial design, brand identity, packaging, and UX of the physical
product. This is "what does the box look like and how does an owner
feel about it" — distinct from `../enclosure/` which is the mechanical
implementation.

## Status

`empty` — nothing here yet. Earliest deliverables expected:

1. **Design language brief** — surface treatment, materials, primary
   accent color, typography for any printed/laser-etched marks.
2. **Product front renders** — hero shots for the GenieClaw repo
   README and any marketing surface.
3. **Owner unboxing flow** — step-by-step photos / icons of: open box
   → seat Jetson → connect cables → run setup script → first voice
   exchange. Doubles as the printed quick-start card.
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
│   └── exploded-marketing.png
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
- **Trademark vs license:** the GenieClaw / GeniePod logo and
  wordmark may be trademarked separately from the CERN-OHL-S license
  on the hardware. Trademark policy will live alongside `identity/`
  when the first owned mark exists.

## Related

- [`../enclosure/`](../enclosure/) — implements this design language
  in mechanical form.
- [GenieClaw repo](https://github.com/GeniePod/genie-claw) — README
  hero image and product positioning live there; assets in this
  folder feed it.
