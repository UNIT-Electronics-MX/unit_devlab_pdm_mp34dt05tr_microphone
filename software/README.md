<div align="center">

<h1>Software &mdash; UNIT DevLab PDM MP34DT05TR Microphone</h1>

<p>
  Example code for the <strong>UNIT DevLab PDM MP34DT05TR Microphone Breakout</strong>,<br>
  a digital MEMS microphone based on the ST MP34DT05-A sensor.<br>
  Targets the <strong>Raspberry Pi Pico / Pico 2 (RP2040 / RP2350)</strong> using the Arduino framework.
</p>

<img src="../hardware/resources/img/connect.png" width="480" alt="Wiring diagram"/>
<br/>
<img src="../hardware/resources/img/pdm_serial.png" width="700" alt="Serial live plot"/>

</div>

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

<details>
<summary><strong>Hardware</strong></summary>
<br>

| Item | Details |
|------|---------|
| Board | Raspberry Pi Pico or Pico 2 |
| UNIT DevLab PDM Mic | MP34DT05-A breakout |
| Cable | JST connector or breadboard wires |

</details>

<details>
<summary><strong>Software</strong></summary>
<br>

| Tool | Notes |
|------|-------|
| Arduino IDE | 2.x recommended |
| arduino-pico core | latest (earlephilhower) |
| Python | 3.9 or later |
| pyserial | `pip install pyserial` |
| matplotlib (optional) | `pip install matplotlib` |

</details>

---

## Available examples

| Example | Description |
|---------|-------------|
| [`cpp_examples/pdm_microphone`](cpp_examples/) | Capture PDM audio and stream PCM samples over Serial |

---

## Quick start

1. Clone the repository:

```sh
git clone https://github.com/UNIT-Electronics-MX/unit_devlab_pdm_mp34dt05tr_microphone.git
cd unit_devlab_pdm_mp34dt05tr_microphone
```

2. Wire the microphone to the Pico &mdash; see the wiring table in [`cpp_examples/README.md`](cpp_examples/README.md).
3. Install the **arduino-pico** board package in Arduino IDE.
4. Open `cpp_examples/pdm_microphone/pdm_microphone.ino` and click **Upload**.
5. Open the Serial Monitor at **115200 baud** &mdash; signed integer samples will print one per line.
6. (Optional) Launch the Python live plotter:

```sh
pip install pyserial matplotlib
python3 cpp_examples/pdm_microphone/serial_live_samples.py
```
