# Arduino PDM Microphone Example

This example is the Arduino equivalent of `hello_pdm_microphone` from pico-sdk:

- Reads PDM microphone samples
- Converts them to PCM via Arduino's PDM stack
- Prints signed sample values over Serial

## Requirements

- Arduino IDE or `arduino-cli`
- Raspberry Pi Pico / Pico 2 board package installed
- `PDM` library available in your selected core

## Wiring (default)

| Board GPIO | PDM Microphone |
| ---------- | -------------- |
| 3.3V | VCC |
| GND | GND |
| GND | SEL |
| GPIO 11 | DAT (DIN) |
| GPIO 10 | CLK |

For arduino-pico RP2040/RP2350 core, pins are set in the sketch with:

- `PDM.setDIN(11)`
- `PDM.setCLK(10)`

## Build with arduino-cli

Install board core (example with arduino-pico by Earle Philhower):

```sh
arduino-cli core update-index --additional-urls https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json
arduino-cli core install rp2040:rp2040 --additional-urls https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json
```

Compile (example FQBN for Pico 2):

```sh
arduino-cli compile --fqbn rp2040:rp2040:rpipico2 examples/arduino_pdm_microphone
```

Upload:

```sh
arduino-cli upload -p /dev/ttyACM0 --fqbn rp2040:rp2040:rpipico2 examples/arduino_pdm_microphone
```

Adjust FQBN/port for your board.

## Live Serial Viewer (Python)

If you prefer a cleaner live view, use the Python script that keeps a rolling
sample window and clears previous output on each refresh.

Install dependency:

```sh
pip install pyserial
```

For live plots:

```sh
pip install matplotlib
```

Run:

```sh
python3 examples/arduino_pdm_microphone/serial_live_samples.py --port /dev/ttyACM0 --baud 115200 --sample-rate 8000 --seconds 1.0
```

Live plot mode (default):

```sh
python3 examples/arduino_pdm_microphone/serial_live_samples.py --mode plot
```

Text mode:

```sh
python3 examples/arduino_pdm_microphone/serial_live_samples.py --mode text
```

If `--port` is omitted, the script tries `/dev/ttyACM*` and `/dev/ttyUSB*` automatically.

Buffer notes:

- By default, the viewer keeps at least `1.0` second of samples.
- At `8000 Hz`, `1.0` second means `8000` samples in the rolling window.
- You can increase to 2 seconds with `--seconds 2.0`.
- `--window` still works as an explicit override in samples.

Press `Ctrl+C` to stop.

## Troubleshooting

If you see `PDM microphone initialization failed!`:

1. Confirm DIN and CLK wiring matches the table.
2. Confirm your board package includes RP2040/RP2350 PDM support.
3. Try a safer sample rate (e.g. `16000`) if your board/core is heavily loaded.
