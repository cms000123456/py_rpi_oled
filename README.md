# 🔥 py_rpi_oled

> Turn your Raspberry Pi into a cyberpunk system monitor with SSD1306 OLED displays

[![Python](https://img.shields.io/badge/Python-3.7+-3776AB?logo=python&logoColor=white)](https://python.org)
[![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-C51A4A?logo=raspberrypi&logoColor=white)](https://raspberrypi.org)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

<p align="center">
  <img src="https://img.shields.io/badge/I2C-Supported-brightgreen?style=for-the-badge" />
  <img src="https://img.shields.io/badge/SPI-Supported-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/GPIO-Interactive-orange?style=for-the-badge" />
</p>

## ✨ What is this?

A collection of Python scripts to drive **SSD1306 OLED displays** (128x32 or 128x64) on Raspberry Pi. Whether you want a sleek system monitor or an interactive control panel with physical buttons, this repo has you covered.

### 🎬 Demo Scenarios

- **System Dashboard** - Real-time CPU, memory, disk usage & IP address
- **Interactive Menu** - Physical button control with reboot/shutdown functionality
- **Custom Graphics** - Draw shapes, text, and bitmaps using PIL

## 🚀 Quick Start

### Hardware Requirements

- Raspberry Pi (any model with I2C/SPI)
- SSD1306 OLED display (128x32 or 128x64)
- Jumper wires
- Optional: Push button + LED for interactive mode

### Wiring (I2C)

```
OLED VCC → Pi 3.3V
OLED GND → Pi GND
OLED SCL → Pi GPIO 3 (SCL)
OLED SDA → Pi GPIO 2 (SDA)
```

### Installation

```bash
# Enable I2C interface
sudo raspi-config
# Interface Options → I2C → Enable

# Install dependencies
pip install adafruit-blinka adafruit-circuitpython-ssd1306 pillow

# For interactive mode (disp.py)
pip install RPi.GPIO Adafruit-GPIO Adafruit_SSD1306
```

## 📁 What's Inside

| File | Description | Interface |
|------|-------------|-----------|
| `stats.py` | Real-time system monitor | I2C |
| `disp.py` | Interactive menu with button control | I2C + GPIO |
| `adafruit_ssd1306.py` | CircuitPython/MicroPython driver | I2C/SPI |
| `slkscr.ttf` | Silkscreen pixel font (regular) | - |
| `slkscrb.ttf` | Silkscreen pixel font (bold) | - |

## 🎮 Usage

### System Monitor
```bash
python stats.py
```

Displays:
- IP Address
- CPU Load
- Memory Usage
- Disk Usage

### Interactive Control Panel
```bash
python disp.py
```

Features:
- Press button (GPIO 20) to wake display
- Hold 5s → Reboot menu
- Hold 10s → Shutdown menu
- LED indicator (GPIO 23)

## 🛠️ Customization

### Change Display Size

```python
# In stats.py or your script
disp = adafruit_ssd1306.SSD1306_I2C(128, 64, i2c)  # For 128x64 display
```

### Custom Fonts

```python
# Use bundled Silkscreen font
font = ImageFont.truetype('slkscr.ttf', 8)

# Or system fonts
font = ImageFont.truetype('/usr/share/fonts/truetype/dejavu/DejaVuSans.ttf', 9)
```

### Draw Custom Graphics

```python
from PIL import Image, ImageDraw

image = Image.new('1', (width, height))
draw = ImageDraw.Draw(image)

# Draw shapes
draw.rectangle((0, 0, width, height), outline=0, fill=0)
draw.text((x, y), "Hello World", font=font, fill=255)

# Update display
disp.image(image)
disp.show()
```

## 🔌 Pin Configuration (disp.py)

| Function | GPIO Pin |
|----------|----------|
| Info Button | GPIO 20 |
| Status LED | GPIO 23 |

## 📜 License

MIT License - See [adafruit_ssd1306.py](adafruit_ssd1306.py) for full copyright notice.

---

<p align="center">
  Made with 💜 for the Raspberry Pi community
</p>
