# AGENTS.md - Guidelines for AI Coding Agents

This repository contains Python scripts for controlling SSD1306 OLED displays on Raspberry Pi.

## Build/Lint/Test Commands

This project has no formal build system. It uses direct Python execution:

```bash
# Run a script (requires Raspberry Pi with OLED display attached)
python stats.py
python disp.py

# Check Python syntax
python -m py_compile stats.py
python -m py_compile disp.py
python -m py_compile adafruit_ssd1306.py

# Run pylint (if available)
pylint stats.py disp.py adafruit_ssd1306.py

# No test suite exists - test manually on Raspberry Pi hardware
```

## Code Style Guidelines

### Imports
- Group imports: stdlib first, then third-party, then local
- Use absolute imports
- Example:
```python
import time
import subprocess

from board import SCL, SDA
import busio
from PIL import Image, ImageDraw, ImageFont
import adafruit_ssd1306
```

### Formatting
- 4 spaces for indentation
- No strict line length limit, but keep lines reasonable (<100 chars)
- Two blank lines between top-level definitions
- One blank line between methods in a class

### Naming Conventions
- `snake_case` for functions, variables, and modules
- `PascalCase` for classes
- `UPPER_CASE` for constants
- Private methods/attributes use single leading underscore

### Types
- No type hints currently used
- Optional: can add type hints for new code

### Error Handling
- Use try/except for optional imports with fallback:
```python
try:
    import framebuf
except ImportError:
    import adafruit_framebuf as framebuf
```
- Avoid bare except clauses

### Comments
- Use docstrings for modules, classes, and public methods
- Use inline comments sparingly, explain "why" not "what"
- Keep the existing MIT license header in `adafruit_ssd1306.py`

### Hardware-Specific Considerations
- This code runs on Raspberry Pi with GPIO/I2C hardware
- `adafruit_ssd1306.py`: CircuitPython/MicroPython compatible driver
- `stats.py`: System monitoring display (I2C interface)
- `disp.py`: Interactive menu display with GPIO button input

### Dependencies
- `adafruit-blinka` (board, busio)
- `adafruit-circuitpython-ssd1306`
- `pillow` (PIL)
- `RPi.GPIO` (for disp.py)
- `Adafruit-GPIO`, `Adafruit_SSD1306` (legacy, for disp.py)

## Project Structure

```
py_rpi_oled/
├── adafruit_ssd1306.py   # OLED driver (CircuitPython)
├── stats.py              # System stats display
├── disp.py               # Interactive menu display
├── slkscr.ttf            # Silkscreen font (regular)
└── slkscrb.ttf           # Silkscreen font (bold)
```

## Notes for Agents

- Code targets Raspberry Pi hardware - cannot run on standard development machines
- Manual testing required on actual Pi with OLED display
- `disp.py` uses legacy Adafruit libraries; `stats.py` uses newer CircuitPython libraries
- GPIO pin usage: Button on GPIO 20, LED on GPIO 23
