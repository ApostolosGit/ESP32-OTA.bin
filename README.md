# ESP32-C3 Boiler OTA binaries

Public hosting for ESP32-C3 Boiler firmware binaries only.

## Latest public Boiler OTA: v1.05 (4 independent DS18B20 sensors)

- **Application-only OTA firmware:** [Boiler_ESP32C3_V1_05.bin](./Boiler_ESP32C3_V1_05.bin), **1,342,768 bytes**.
- **Active OTA manifest:** [manifest-boiler.txt](./manifest-boiler.txt) with version=1.05.
- **MD5:** 8179b77b60513629a3bb7437c139bc63
- **SHA256:** f209a79ff3333b2a5ea26df8704be8a2e094f1d348ca9444a922344d19b69e29
- Exact private [Arduino core 3.2.1 compilation and release](https://github.com/ApostolosGit/ESP32-C3-BOILER/releases/tag/boiler-merged-v1.05-test.7).

The Boiler now reads **four separate DS18B20 buses**, each with its own 4.7 kΩ DQ pull-up to **3V3**:

| MQTT.app | GPIO | Firmware MQTT key |
|---|---:|---|
| Θ1 | GPIO5 | temp_1 |
| Θ2 | GPIO6 | temp_2 |
| Θ3 | GPIO7 | temp_3 |
| Θ4 | GPIO21 | temp_4 |

The OLED stays on SDA GPIO3/SCL GPIO4. Boiler remains **MONITOR ONLY, with no actuator outputs**. MQTT.app v5.79 shows all four live measurements. This upgrade retains the previous two-channel LittleFS history format and existing credential record; the additional channels Θ2 and Θ4 are **live only**, not yet stored as individual historical series. Static Boiler IP remains **192.168.1.82**.

**Safety:** Published for explicit user-initiated MQTT OTA after SHA256/MD5 verification and successful compilation, but **not yet hardware OTA-tested**. Do not begin an unattended upgrade without local recovery access. The remote OTA download currently does not verify a trusted TLS certificate or digital image signature; MD5 is only a checksum, not origin authentication.

**Never upload the 4 MB FULL MERGED USB image over OTA.** A full-chip USB flash at 0x0 overwrites settings/history; only the 1,342,768-byte application binary is for MQTT OTA.

## Historical public OTA: Boiler v1.04 (verified build, not hardware OTA-tested)

- Latest application-only OTA: [Boiler_ESP32C3_V1_04.bin](./Boiler_ESP32C3_V1_04.bin), **1,343,216 bytes**. MD5: 4df6cd97ccb14cbc767b9eddb704834a. SHA256: 6869ce9286da6009f3b28847aa019fc2c40730039adfca062d433554058496ef.
- Active [manifest-boiler.txt](./manifest-boiler.txt) version **1.04**. [Private source compilation and binary release](https://github.com/ApostolosGit/ESP32-C3-BOILER/releases/tag/boiler-merged-v1.04-test.1).
- Updated EnergyMeter-style Network Debug, Network Setup with credential preservation, Wi-Fi/MQTT status, and confirmed OTA-ONLY Recovery/Exit. Boiler LAN static IP: **192.168.1.82**, EnergyMeter ESP8266 5.58: **.80**, Ventilation: **.81**. First-use Boiler AP: **192.168.4.1**.
- Remains MONITOR ONLY; no relay pins are enabled. SH1106 OLED uses SDA GPIO3/SCL GPIO4; all three DS18B20 share GPIO5.
- **OTA caution:** Firmware compiled and its bytes verified; real-device MQTT OTA and OTA recovery have NOT been tested. No automatic installation is initiated by this release. Do not flash unattended. The HTTPS OTA path currently lacks verified TLS certificates or signed image authentication; MD5 is only an integrity check.
- Upload only the **application-only** Boiler_ESP32C3_V1_04.bin via OTA. **Never upload the 4 MB FULL MERGED file via OTA.** Merged files are for USB at offset 0x0 and overwrite LittleFS settings and history.

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
