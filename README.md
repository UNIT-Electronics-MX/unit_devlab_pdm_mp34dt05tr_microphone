<div align="center">

<h1>UNIT DevLab &mdash; PDM MEMS Microphone MP34DT05TR</h1>

<p>
  Breakout board for the ST MP34DT05-A PDM MEMS microphone.<br>
  High SNR, low power, omnidirectional &mdash; designed for easy integration with RP2040 / RP2350 and other microcontrollers.
</p>

<a href="https://uelectronics.com/">
  <img src="hardware/resources/img/AR3631-%20UNIT%20MP34DT05TR-A%20M%C3%B3dulo%20Micr%C3%B3fono%20PDM%20(2)_1.jpg" width="500" alt="UNIT DevLab PDM MP34DT05TR Microphone"/>
</a>

<br><br>

<a href="https://wiki.uelectronics.com/wiki/unit_devlab_mspm0c1104sdsgr_development_board"><img src="https://img.shields.io/badge/Product%20Wiki-blue?style=for-the-badge" alt="Product Wiki"></a>
<a href="https://www.st.com/resource/en/datasheet/mp34dt05-a.pdf"><img src="https://img.shields.io/badge/Datasheet-green?style=for-the-badge" alt="Datasheet"></a>
<a href="https://uelectronics.com/"><img src="https://img.shields.io/badge/Buy%20Now-orange?style=for-the-badge" alt="Buy Now"></a>

</div>

---

## Features

| Parameter | Value |
|-----------|-------|
| Supply voltage | 1.8 V &ndash; 3.3 V |
| Output interface | PDM |
| Current consumption | 0.65 mA |
| SNR | 64 dB |
| Sensitivity | &minus;26 dBFS &plusmn; 3 dB |
| Directivity | Omnidirectional |
| Board dimensions | 14.0 &times; 12.6 &times; 1.6 mm |

---

## Repository structure

```
.
├── hardware/          # Schematics, PCB files, and images
├── software/          # Arduino examples and Python tools
│   └── cpp_examples/
│       └── pdm_microphone/
│           ├── pdm_microphone.ino
│           └── serial_live_samples.py
└── docs/              # Generated HTML documentation
```

---

## Clone and integrate

```sh
git clone https://github.com/UNIT-Electronics-MX/unit_devlab_pdm_mp34dt05tr_microphone.git
cd unit_devlab_pdm_mp34dt05tr_microphone
```

Open the Arduino sketch:

```sh
# Linux / macOS
open software/cpp_examples/pdm_microphone/pdm_microphone.ino

# Or navigate manually in Arduino IDE:
# File > Open > software/cpp_examples/pdm_microphone/pdm_microphone.ino
```

Run the live Python viewer after uploading the sketch:

```sh
pip install pyserial matplotlib
python3 software/cpp_examples/pdm_microphone/serial_live_samples.py
```

See [`software/README.md`](software/README.md) for full setup instructions.

---

## Resources

- [MP34DT05-A Datasheet](https://www.st.com/resource/en/datasheet/mp34dt05-a.pdf)
- [Microphone Library for Pico Pulsar (RP2040/RP2350)](https://github.com/UNIT-Electronics-MX/microphone-library-for-pico-pulsar)
- [UNIT PDM MEMS Microphone Breakout Guide UF2](https://github.com/UNIT-Electronics/UNIT-PDM-MEMS-Microphone-Breakout-Guide-UF2#readme)

---

## License

Released under the MIT License. See [LICENSE](license) for details.
