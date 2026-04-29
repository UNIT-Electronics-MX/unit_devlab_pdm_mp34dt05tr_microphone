# Software — UNIT DevLab PDM MP34DT05TR Microphone

This folder contains example code for the **UNIT DevLab PDM MP34DT05TR Microphone Breakout**, a digital MEMS microphone based on the ST MP34DT05-A sensor. Examples target the **Raspberry Pi Pico / Pico 2 (RP2040 / RP2350)** using the Arduino framework.

![Wiring diagram](../hardware/resources/img/connect.png)

![Serial live plot](../hardware/resources/img/pdm_serial.png)

---

## Folder structure

```
software/
└── cpp_examples/
    └── pdm_microphone/
        ├── pdm_microphone.ino      # Arduino sketch
        └── serial_live_samples.py  # Python live viewer / plotter
```

---

## Requirements

### Hardware

| Item | Details |
|------|---------|
| Board | Raspberry Pi Pico or Pico 2 |
| UNIT DevLab PDM Mic | MP34DT05-A breakout |
| Cable | JST connector or breadboard wires |

### Software

| Tool | Version |
|------|---------|
| Arduino IDE | 2.x recommended |
| arduino-pico core | latest (earlephilhower) |
| Python | 3.9 + |
| pyserial | `pip install pyserial` |
| matplotlib *(optional)* | `pip install matplotlib` |

---

## Available examples

| Example | Description |
|---------|-------------|
| [`cpp_examples/pdm_microphone`](cpp_examples/) | Capture PDM audio and stream PCM samples over Serial |

---

## Quick start

1. Wire the microphone to the Pico (see table in `cpp_examples/README.md`).
2. Install the **arduino-pico** board package in Arduino IDE.
3. Open `cpp_examples/pdm_microphone/pdm_microphone.ino` and upload.
4. Open the Serial Monitor at **115200 baud** — you should see signed integer samples printed one per line.
5. *(Optional)* Run the Python viewer for a live waveform plot:

```sh
python3 cpp_examples/pdm_microphone/serial_live_samples.py
```
