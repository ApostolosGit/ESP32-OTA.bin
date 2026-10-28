# ESP32-C3 firmware downloads

Public hosting for ESP32-C3 application OTA and full USB installation images.

## Boiler v2.01 — native setup AP repair, USB at 0x0000

[**Download Boiler v2.01 FULL MERGED (4MB)**](https://raw.githubusercontent.com/ApostolosGit/ESP32-OTA.bin/main/Boiler_ESP32C3_V2_01_FULL_MERGED_0x0000.bin)
for Espressif Flash Download Tool / esptool.

- Chip **ESP32-C3**, address **0x0000**, **DIO / 40 MHz / 4 MB (32 Mbit)**.
- Complete image size **4,194,304 bytes**; flashing replaces credentials/history.
- [Source `.ino` and partitions](https://github.com/ApostolosGit/ESP32-C3-BOILER/tree/main/Boiler_ESP32C3_V2_01)
  · [USB metadata](./Boiler_ESP32C3_V2_01_USB.json)
  · [SHA256](./Boiler_ESP32C3_V2_01_USB_SHA256SUMS.txt).

CommonPlatform **1.02** removes an unnecessary blank-AP start/stop cycle,
selects RAM Wi-Fi storage before initialization, explicitly configures an
open visible **channel1 / b-g-n / HT20** AP, validates native SDK state/config,
and monitors it every second. Lost AP state invalidates the portal status
and schedules the existing30-second retry. TX power is unchanged.

A physical Boiler2.00 board reported `AP SETUP/LOCAL` on the OLED while no
nearby client discovered its SSID. The repair addresses concrete port issues;
**the RF cause is not proven and2.01 still needs physical AP validation**.
SDK readback is not evidence that another device can receive beacons.
See the [AP port audit](https://github.com/ApostolosGit/ESP32-C3-CommonPlatform/blob/main/validation/AP-PORT-AUDIT.md).

On first setup join **`BOILER-BOILER-…`**, open **http://192.168.4.1/** and use
PIN **12134**. Four independent DS18B20 inputs stay GPIO5/6/7/21, OLED is
SH1106 on SDA3/SCL4, LAN stays **192.168.1.82**. The public Boiler app OTA
manifest stays **1.05**; this full USB image must not be used as app OTA.
All earlier sources, images and manifests remain available unchanged.

## Boiler v2.00 — historical first USB installation at 0x0000

[**Download Boiler v2.00 FULL MERGED (4MB)**](https://raw.githubusercontent.com/ApostolosGit/ESP32-OTA.bin/main/Boiler_ESP32C3_V2_00_FULL_MERGED_0x0000.bin)
for Espressif Flash Download Tool / esptool.

- File: `Boiler_ESP32C3_V2_00_FULL_MERGED_0x0000.bin`, **4,194,304 bytes**.
- Chip **ESP32-C3**, address **0x0000**, **DIO / 40 MHz / 4 MB (32 Mbit)**.
- SHA256: `247faa0218eb6a7467f4727c86c6e2bb6b0c729d0de7db2c51b007643ff55a5a`.
- [Source `.ino` and partitions](https://github.com/ApostolosGit/ESP32-C3-BOILER/tree/main/Boiler_ESP32C3_V2_00)
  · [USB release metadata](./Boiler_ESP32C3_V2_00_USB.json)
  · [SHA256 file](./Boiler_ESP32C3_V2_00_USB_SHA256SUMS.txt).

Boiler2.00 combines CommonPlatform1.01 with the measurements of the supplied
1.05: four independent DS18B20 buses at GPIO5/6/7/21, async12bit sampling,
SH1106 OLED at SDA3/SCL4, static LAN **192.168.1.82**, and monitor-only behavior.
Existing two-channel history remains TH1/TH3; TH2/TH4 are live readings only.
The common platform owns network/TLS, credentials, shared page/style/footer,
clock, diagnostics, Recovery and OTA services.

This complete USB image includes bootloader, partition table, OTA metadata
and application. It **replaces existing credentials and history**. The new
LittleFS geometry is0x330000/768KiB versus1.05's0x3D0000/128KiB. Configure
Wi-Fi/MQTT again through the `BOILER-BOILER-…` AP at **192.168.4.1**, PIN12134.

All five firmware profiles, seven Boiler host suites, common behavior suites,
RISC-V storage-ABI checks, desktop/mobile Chromium, and full-image layout
validation passed at publication. Subsequent physical use reported the AP
visibility failure described above; use2.01 for the pending repair validation.
The public `manifest-boiler.txt` remains **1.05**: this first2.00 release is for
USB, and does not activate app OTA. The application-only2.00 image remains
in the private source repository. Never send this full USB image through OTA.
All earlier Boiler/CommonPlatform files and manifests are retained unchanged.

## CommonPlatform v1.00 — ESP32-C3 Super Mini, USB at 0x0000

[**Download the full merged 4MB binary**](https://raw.githubusercontent.com/ApostolosGit/ESP32-OTA.bin/main/CommonPlatform_ESP32C3_V1_00_FULL_MERGED_0x0000.bin)
for **Espressif Flash Download Tool / esptool**.

- File: `CommonPlatform_ESP32C3_V1_00_FULL_MERGED_0x0000.bin`.
- Flash address **0x0000**, chip **ESP32-C3**, **DIO / 40MHz / 4MB (32Mbit)**.
- Size **4,194,304 bytes**, SHA256
  `3199c64b672184c4cb0a1e49068c7133afdadeb9a380bb30c384d9859a87d19b`.
- Includes bootloader at 0x0, partition table at 0x8000, boot_app0 at 0xe000,
  application at 0x10000 and erased remaining flash. Full USB flashing
  replaces existing settings/history on the board.

Default firmware has **no OLED**, sensors or actuator outputs. It provides
READY/time, Wi-Fi/DHCP, MQTT with CA-verified TLS, shared web/setup/PIN,
diagnostics and recovery services, ported from ESP8266 CommonPlatform 1.03.
After boot, join `ESP32-C3-COMMON_C3-…`, open **http://192.168.4.1/** and use
setup PIN **12134**. Configure Wi-Fi; the router then assigns the LAN address
by DHCP. Optional SSD1309 support remains available in the source.

[Source and instructions](https://github.com/ApostolosGit/ESP32-C3-CommonPlatform)
· [release metadata](./CommonPlatform_ESP32C3_V1_00.json)
· [SHA256 checksums](./CommonPlatform_ESP32C3_V1_00_SHA256SUMS.txt).
Both display builds, all five host suites and merged-image validation passed;
physical board/USB/Wi-Fi/OTA operation has not yet been tested.

The separate [APP binary](./CommonPlatform_ESP32C3_V1_00_APP.bin),
**1,425,184 bytes**, is for application-only OTA, **not first USB installation
at 0x0**. Its SHA256 is
`a7c6f6148e2b1ef9cb0cd5fd9804b6e766db65c8557322c1c28d76ae26e7ce49`.
No CommonPlatform app OTA manifest is activated: MQTT.app currently has no
generic platform device profile. The existing Boiler manifest and all
previously published binaries remain unchanged.

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
