# Arduino PDM Microphone Example

This example is the Arduino equivalent of `hello_pdm_microphone` from pico-sdk:

- Reads PDM microphone samples
- Converts them to PCM via Arduino's PDM stack
- Prints signed sample values over Serial

## Requirements

- Arduino IDE
- Raspberry Pi Pico / Pico 2 board package installed
- `PDM` library available in your selected core

![Live plot example](../../hardware/resources/img/connect.png)

## Wiring (default)

| Board GPIO | PDM Microphone |
| ---------- | -------------- |
| 3.3V | VCC |
| GND | GND |
| GND | SEL |
| GPIO 4 | DAT (DIN) |
| GPIO  5 | CLK |

For arduino-pico RP2040/RP2350 core, pins are set in the sketch with:

- `PDM.setDIN(4)`
- `PDM.setCLK(5)`

## Build with Arduino IDE

1. Open Arduino IDE
2. Go to **File** > **Preferences** > **Additional Board Manager URLs**
3. Add: `https://github.com/earlephilhower/arduino-pico/releases/download/global/package_rp2040_index.json`
4. Go to **Tools** > **Board** > **Boards Manager**
5. Search for "rp2040" and install the arduino-pico core
6. Select your board: **Tools** > **Board** > **Raspberry Pi Pico** (or **Pico 2**)
7. Open `examples/arduino_pdm_microphone`
8. Click **Upload**

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

