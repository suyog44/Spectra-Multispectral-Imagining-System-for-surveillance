# Spectra-Multispectral-Imagining-System-for-surveillance

**Low-cost 4-band multispectral imaging system built with Raspberry Pi 5, OV5640 cameras, and Edmund Optics filters.**

2× MIPI CSI-2 + 2× USB UVC (ESP32-P4) &nbsp;|&nbsp; NDVI, GNDVI, VARI vegetation indices &nbsp;|&nbsp; ~$200 total build

---

## Architecture

```
  RPi 5 CSI-0 ─── OV5640 + Edmund Blue    (#43-936)  ▒▒ 380-520 nm
  RPi 5 CSI-1 ─── OV5640 + Edmund Green   (#43-930)  ▒▒ 480-600 nm
  RPi 5 USB-A ─── ESP32-P4 ─── OV5640 + Edmund Red   (#43-942)  ▒▒ 580-700 nm
  RPi 5 USB-A ─── ESP32-P4 ─── OV5640 + Edmund IR    (#43-948)  ▒▒ 720-1000 nm
```

All 4 cameras capture in parallel — CSI and USB are on independent buses.


## Hardware

| Part | Qty | ~Cost |
|---|---|---|
| Raspberry Pi 5 (4GB+) | 1 | $60 |
| OV5640 MIPI CSI module | 2 | $20 |
| OV5640 DVP module | 2 | $16 |
| ESP32-P4-Function-EV board | 2 | $30 |
| Edmund Blue filter #43-936 | 1 | $19 |
| Edmund Green filter #43-930 | 1 | $19 |
| Edmund Red filter #43-942 | 1 | $19 |
| Edmund IR filter #43-948 | 1 | $19 |
| FPC cables, USB cables, white ref card | — | $15 |
| **Total** | | **~$200** |

See [HARDWARE.md](HARDWARE.md) for the complete build guide, wiring diagrams, and filter mounting.

## Filters

We use [Edmund Optics Optical Cast Plastic Color Filters](https://www.edmundoptics.com/f/optical-cast-plastic-color-filters/12257/) (#1917 family) — affordable broadband absorptive filters on Thermoset ADC substrate.

| Band | Filter | Type | Passband | Eff. Wavelength |
|---|---|---|---|---|
| Blue | #43-936 (~47B) | Bandpass | 380–520 nm | 460 nm |
| Green | #43-930 (#58) | Bandpass | 480–600 nm | 530 nm |
| Red | #43-942 (#25) | Longpass* | 580–700 nm | 640 nm |
| IR | #43-948 | Longpass | 720–1000 nm | 850 nm |

*Red becomes a bandpass when paired with the OV5640's built-in IR-cut filter (580–700 nm).

> **Important:** The NIR camera's OV5640 IR-cut filter must be physically removed. The other 3 cameras should keep theirs.

### Computed Indices

| Index | Formula | Use |
|---|---|---|
| NDVI | (NIR−Red)/(NIR+Red) | Vegetation health / chlorophyll |
| GNDVI | (NIR−Green)/(NIR+Green) | Dense canopy analysis |
| VARI | (Green−Red)/(Green+Red−Blue) | Visible vegetation fraction |
| SR | NIR / Red | Simple ratio — robust with broadband filters |

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Issues and PRs welcome.

## License

MIT — see [LICENSE](LICENSE).
