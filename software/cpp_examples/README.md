# Arduino PDM Microphone Example

Arduino implementation of the classic `hello_pdm_microphone` example from the pico-sdk. The sketch captures audio from the **UNIT DevLab PDM MP34DT05TR Microphone** and streams signed 16-bit PCM samples over Serial.

![Wiring](../../hardware/resources/img/connect.png)

---

## How it works

1. The **arduino-pico** `PDM` library configures the RP2040/RP2350 PIO-based PDM peripheral.
2. An interrupt callback (`onPdmData`) fills a 256-sample buffer every time new audio data is ready.
3. The `loop()` safely copies the buffer and prints each sample as a signed integer over Serial at **115200 baud**.
4. The companion Python script reads those samples and renders a live waveform + histogram.

---

## Wiring

| Pico GPIO | PDM Microphone pin |
|-----------|--------------------|
| 3.3 V     | VCC                |
| GND       | GND                |
| GND       | SEL (L = slave)    |
| GPIO 4    | DAT / DIN          |
| GPIO 5    | CLK                |

> The pins are defined in the sketch as `kPdmDinPin = 4` and `kPdmClkPin = 5`. Change them to match your wiring if needed.

---

## Requirements

- **Arduino IDE 2.x**
- **arduino-pico** board package (earlephilhower)
  - Board manager URL: `https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json`
- `PDM` library — included with the arduino-pico core, no extra install needed

---

## Upload with Arduino IDE

1. Open Arduino IDE.
2. Go to **File › Preferences › Additional Board Manager URLs** and add the URL above.
3. Go to **Tools › Board › Boards Manager**, search for `rp2040`, and install the **arduino-pico** core.
4. Select your board: **Tools › Board › Raspberry Pi Pico** (or **Pico 2**).
5. Open `pdm_microphone/pdm_microphone.ino`.
6. Select the correct port under **Tools › Port**.
7. Click **Upload**.
8. Open the Serial Monitor at **115 200 baud** — you should see a stream of signed integers.

---

## Live viewer — Python

The `serial_live_samples.py` script reads the Serial stream and shows:

- A rolling waveform plot (matplotlib)
- An amplitude histogram
- Real-time statistics (min / max / mean / RMS)

### Install dependencies

```sh
pip install pyserial matplotlib
```

### Run

```sh
# Auto-detect port, plot mode (default)
python3 pdm_microphone/serial_live_samples.py

# Specify port and baud rate
python3 pdm_microphone/serial_live_samples.py --port /dev/ttyACM0 --baud 115200

# Keep 2 seconds of samples in the rolling window
python3 pdm_microphone/serial_live_samples.py --seconds 2.0

# Text-only mode (no matplotlib required)
python3 pdm_microphone/serial_live_samples.py --mode text
```

| Argument | Default | Description |
|----------|---------|-------------|
| `--port` | auto-detect | Serial port (`/dev/ttyACM*` or `/dev/ttyUSB*`) |
| `--baud` | `115200` | Baud rate |
| `--sample-rate` | `8000` | Expected audio sample rate (Hz) |
| `--seconds` | `1.0` | Rolling window duration in seconds |
| `--mode` | `plot` | `plot` for live graph, `text` for terminal output |

Press **Ctrl + C** to stop.

---

## Troubleshooting

| Symptom | Solution |
|---------|----------|
| `PDM microphone initialization failed!` | Check DIN / CLK wiring; ensure arduino-pico core is selected |
| No samples in Serial Monitor | Verify baud rate is **115 200**; check the correct COM/tty port is selected |
| Python: `No module named serial` | Run `pip install pyserial` |
| Python: `No module named matplotlib` | Run `pip install matplotlib` or use `--mode text` |
| Noisy / clipping signal | Normal at 8 kHz; try `kSampleRate = 16000` for a lower noise floor |

