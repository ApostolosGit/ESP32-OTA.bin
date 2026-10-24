# ESP32-C3 Boiler OTA binaries

Public hosting for ESP32-C3 Boiler firmware binaries only.

## First-time USB installation — FULL MERGED v1.01 (4 MB)

The `Boiler_ESP32C3_V1_01.bin` in this public OTA repository is **application-only**; it must **not** be flashed at address `0x0`.

For a first-time ESP Tool USB installation at flash address **`0x0`**, use the exact [FULL MERGED 4MB test binary from the private Boiler firmware Release](https://github.com/ApostolosGit/ESP32-C3-BOILER/releases/download/boiler-merged-v1.01-test.1/Boiler_ESP32C3_V1_01_FULL_MERGED_0x0.bin).

- Merged file: `Boiler_ESP32C3_V1_01_FULL_MERGED_0x0.bin` (4,194,304 bytes).
- SHA256: `c2e0dbd515a0eb0074d2b96a76dca644f4645d0887ae7739723895915232112e`.
- This full image overwrites the 4MB flash, including existing settings and history. **Never use this merged file for MQTT OTA.**
- The source Release is private, so you must be signed into GitHub with access to `ESP32-C3-BOILER` to download it.

## Published ESP32-C3 Boiler v1.01 (TEST ONLY)

- Binary: [`Boiler_ESP32C3_V1_01.bin`](./Boiler_ESP32C3_V1_01.bin) (1,335,984 bytes).
- OTA manifest: [`manifest-boiler.txt`](./manifest-boiler.txt) (`meter=BOILER`, `version=1.01`).
- SHA256: `51e8d82369c4a64f8731372469ce6e0391a6b32c207e981accf5928204fe6e96`.
- MD5: `70e28224adb0a2f3de7f31e1930163e1`.
- Firmware v1.01 understands this repository's URL for **future** OTA updates, but the MQTT.app will not offer same-version v1.01 as an OTA upgrade. The first installation is by USB.
- This build has **not** been tested on hardware. Do not connect boiler loads. OTA authenticity is not secured by MD5 alone.


**Important:** The first `Boiler_ESP32C3_V1_01_TEST_ONLY.bin` is a **bench-test build**, not a certified production release. Do not connect any boiler loads or activate control outputs. The firmware remains measurement-only.

Files named `Boiler_ESP32C3_V*.bin` are **ESP32-C3 only**; they must never be installed on ESP8266.

Remote MQTT OTA is enabled only for a **newer matching version** with explicit operator confirmation and PIN. The first installation is through USB.

This repository is public. Only publish firmware that contains no Wi-Fi passwords, MQTT credentials, personal secrets or device-specific encryption keys. Firmware downloads must ultimately use HTTPS with certificate verification or signed-image validation. MD5 alone is not an authentication mechanism.

See the [private development firmware repository](https://github.com/ApostolosGit/ESP32-C3-BOILER).
