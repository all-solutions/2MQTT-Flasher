# 2MQTT-Flasher

2MQTT-Flasher is a desktop flasher for ESP8266 and ESP32 devices with a focus on keeping the workflow simple for end users.

The application is built around a GUI and is intended for typical 2MQTT use cases:

- flash a local `.bin` firmware file
- load current releases from all *2MQTT projects
- auto-detect serial ports and ESP devices
- show live serial logs after flashing
- display chip information

The actual flashing process uses Espressif's `esptool` under the hood.

## Features

- `Local` firmware mode for `.bin` files in the program directory or a manually selected firmware file
- `Release` firmware mode that loads current Flash2MQTT releases directly from `release.json`
- split release selection into `Repo Version` and `Variant`
- automatic serial port scan
- chip information view
- serial log viewer
- default flash speed 921600 for faster flashing, fallback to 115200 for unsupported ESP chips
- compact GUI with only the relevant options exposed

## GUI Overview

Main application window:

<img width="445" height="563" alt="image" src="https://github.com/user-attachments/assets/92af4b84-1b25-4034-89a0-1ba497e93525" />



Features:

https://github.com/user-attachments/assets/cb098669-20be-4987-a58e-68cc96a3c58c


## Firmware Sources

### Local

In `Local` mode, the program looks for `.bin` files in the program directory. If no files are found, the firmware selection shows:

`no local files in program directory`

You can still use the `Browse` button to select a firmware file manually.

### Release

In `Release` mode, the program downloads the current firmware index from all *2MQTT projects:

The selection is split into two steps:

1. choose `Repo Version`
2. choose the matching `Variant`

This keeps the release list easier to navigate when multiple device variants exist for the same firmware family.

## Typical Workflow

1. Connect your ESP device by USB.
2. Start `2MQTT-Flasher`.
3. Wait for auto-detection or choose the correct serial port manually.
4. Select your firmware source: `Local` or `Release`.
5. Choose the firmware.
6. Click `Flash ESP`.
7. After flashing, use `View Logs` or let the application reconnect automatically to the serial log.

## Installation

### Prebuilt Application

Use the release package for your operating system and start the application directly.


## Linux Notes

On many Linux systems, access to serial ports requires membership in the `dialout` group:

```bash
sudo usermod -a -G dialout $(whoami)
```

After that, log out and back in again.

## macOS Notes

Depending on the USB serial adapter in use, an additional driver may be required.

Silicon Labs VCP information:

`https://www.silabs.com/community/interface/forum.topic.html/vcp_driver_for_macosbigsur110x-krlP`

Silicon Labs VCP download:

`https://www.silabs.com/documents/public/software/Mac_OSX_VCP_Driver.zip`

## Troubleshooting

### No serial port available

- check USB cable quality
- check USB driver installation
- reconnect the device
- on Linux, verify `dialout` permissions

### Port is busy

Close other serial tools such as:

- Arduino IDE serial monitor
- PlatformIO monitor
- other flasher tools

### Antivirus warning on packaged binaries

PyInstaller-based desktop apps can trigger false positives on some antivirus products. If that happens, verify the source and build the binary yourself if needed.
