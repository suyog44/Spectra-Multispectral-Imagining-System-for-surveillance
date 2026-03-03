# Contributing

Thanks for your interest in improving the multispectral camera project!

## Getting Started

1. Fork this repo
2. Clone your fork: `git clone https://github.com/suyog44/Spectra-Multispectral-Imagining-System-for-surveillance.git`
3. Create a branch: `git checkout -b feature-name`
4. Make changes
5. Run tests: `make test`
6. Commit and push
7. Open a Pull Request

## Development Setup

```bash
# On RPi 5
make install

# On any machine (for processing code only)
pip install -e ".[dev]" --break-system-packages
```

## Code Style

- Python 3.9+
- Linting: `make lint` (uses ruff)
- Keep modules focused: cameras, processing, output are separate
- Document filter-specific behaviour (these broadband filters have quirks)

## Areas for Contribution

- **Filter characterisation:** Measured transmission curves for the Edmund filters
- **ESP32-P4 firmware improvements:** Better UVC exposure/gain control
- **Image registration:** Sub-pixel alignment between the 4 cameras
- **Additional indices:** EVI, SAVI, MCARI, etc.
- **Web dashboard:** Live preview and monitoring interface
- **3D-printable mounts:** Camera bracket and filter holder STL files
- **Documentation:** Tutorials, application guides, field deployment tips

## Bug Reports

Please include:
- Output of `python3 -m src.diagnostics`
- RPi model and OS version
- Camera modules used
- Error messages / logs
