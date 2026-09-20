# EcoCore — ESP32-P4 LVGL 9 visual HMI boilerplate

![EcoCore conceptual visual](Splash%20Ecocore.png)

EcoCore is an ESP-IDF firmware boilerplate for the Waveshare ESP32-P4-WIFI6-Touch-LCD-7B: an ESP32-P4 touchscreen target with a 7-inch, 1024×600 MIPI DSI display. It combines LVGL 9, the board BSP, and a ForgeUI One runtime baseline with an EcoCore visual direction for embedded UI/HMI work.

This repository provides a configurable ESP32-P4/LVGL baseline for developing and evaluating a touchscreen interface. Its EcoCore material is visual demonstration content: it does not implement energy measurement, environmental sensing, electrical-equipment control, solar or battery management, or carbon/emissions calculations.

## ForgeUI Ecosystem

ForgeUI is developed by [RTechAI](https://github.com/RTechAI).

The [ForgeUI website](https://forgeui.co.nz) is the official home of the ForgeUI embedded UI/HMI development ecosystem. ForgeUI Studio is the current visual embedded UI/HMI development environment for supported ESP32 hardware. [ForgeUI Hosted Studio](https://studio.forgeui.co.nz) is the hosted, browser-based ForgeUI Studio application and is available for public registration.

RTechAI's GitHub organization hosts ForgeUI public repositories, hardware references, framework baselines, examples, and related open development work. EcoCore is a public, board-specific ForgeUI baseline that preserves an earlier ForgeUI One runtime and ESP32-P4 UI Studio export lineage.

## Overview

The application starts the Waveshare display BSP and LVGL, then initializes the generated Studio export. The active export supplies a textured visual background and has update hooks for a clock and Wi-Fi-status label. The runtime also includes optional service modules for hosted Wi-Fi, RTC, SD storage, and audio; their compile-time switches are defined in `main/00_ForgeUI_Config.h`.

The checked-in configuration enables RTC, ESP-Hosted Wi-Fi, and SD storage; audio is present in the source tree but disabled by default. There are no EcoCore-specific sensor widgets or live eco/energy data sources in the application source.

## Hardware Target

- Board: Waveshare ESP32-P4-WIFI6-Touch-LCD-7B
- SoC: Espressif ESP32-P4
- Display: 7-inch 1024×600 EK79007 MIPI DSI panel
- Touch: GT911 capacitive touch controller
- Wireless path: ESP-Hosted over SDIO to the board's ESP32-C6, using `esp_wifi_remote`
- Optional peripherals represented by the runtime: DS3231 RTC and SD card

The repository documentation and configuration describe this as a tested ForgeUI baseline. This checkout contains no physical-hardware photo or test log; the splash image above is conceptual artwork, not physical-validation evidence.

## Software Stack

- ESP-IDF 5.5.4 (locked in `dependencies.lock`)
- LVGL 9.2.2
- Waveshare `esp32_p4_wifi6_touch_lcd_7b` BSP 1.0.2
- `esp_lvgl_port` 2.7.2
- ESP-Hosted 2.9.7 and `esp_wifi_remote` 1.3.0
- Native C application and ForgeUI One runtime modules

## What This Project Demonstrates

- ESP32-P4 display and touch bring-up through the Waveshare BSP
- An LVGL 9 screen initialized from a generated ForgeUI Studio export
- A single-page visual HMI starting point with background artwork
- An ESP-Hosted Wi-Fi architecture for the ESP32-C6 companion radio
- RTC persistence, SD-card mounting/testing, and optional audio runtime code

## EcoCore UI and Demonstration Content

EcoCore identifies the repository's green, nature-oriented visual/theme direction. The local `Splash Ecocore.png` image is conceptual/generated-style artwork with an ESP32-P4 target message; it is neither a UI screenshot nor a hardware photograph. Setup images under `docs/setup/` are configuration screenshots, while `docs/images/` contains theme and icon assets.

No live energy, power, solar, battery, carbon, temperature, humidity, or other environmental values are implemented or displayed by the checked-in generated UI source. Any such interpretation of the EcoCore name or artwork would be outside this repository's demonstrated functionality.

## Hardware and Runtime Baseline

`main/main.c` brings up NVS, starts the display, creates the ForgeUI screen, and then conditionally initializes Wi-Fi and SD storage. The current configuration selects the DS3231 RTC backend. For the hosted Wi-Fi + SD arrangement, the source documents a Wi-Fi-first, SD-second startup order.

The generated screen source (`main/90_Studio_Export.c`) identifies itself as a ForgeUI Studio export and creates the visual background. It is useful as a customization starting point; add application widgets and connect them to verified data sources for a product-specific HMI.

## Project Structure

```text
.
├── CMakeLists.txt                 ESP-IDF project entry point
├── sdkconfig.defaults             ESP32-P4 and LVGL baseline settings
├── dependencies.lock              Resolved managed-component versions
├── main/
│   ├── main.c                     Application boot and service order
│   ├── 00_ForgeUI_Config.h        Runtime feature switches
│   ├── 01_FG_Runtime.c            LVGL screen startup
│   ├── 20_RTC.c                   RTC/NVS timekeeping service
│   ├── 30_WIFI.c                  ESP-Hosted Wi-Fi service
│   ├── 40_SD.c                    SD-card storage service
│   └── 90_Studio_Export.c         Generated LVGL export
├── components/bsp_extra/          Additional board-support component
├── docs/                          Setup screenshots, architecture notes, assets
└── Splash Ecocore.png             Conceptual EcoCore visual
```

## Build and Flash

Install and activate an ESP-IDF 5.5.4 environment, clone the repository, then run from the project root:

```bash
idf.py set-target esp32p4
idf.py build
idf.py flash monitor
```

`sdkconfig.defaults` selects the `esp32p4` target and a 16 MB QIO flash configuration. Before connecting optional peripherals or changing the Wi-Fi/SD startup sequence, review the associated runtime configuration and board documentation.

## Historical ForgeUI Context

The source and previous project documentation identify this boilerplate as an export from the historical [ESP32-P4 UI Studio](https://github.com/RTechAI/esp32p4-ui-studio), powered by the earlier [ForgeUI One](https://github.com/RTechAI/ForgeUI-One) runtime. Those are historical lineage references for this codebase, not claims that the current Hosted Studio generated it.

## Current ForgeUI Studio

The [ForgeUI website](https://forgeui.co.nz) is the official home of the ForgeUI embedded UI/HMI development ecosystem. ForgeUI Studio is the current visual embedded UI/HMI development environment for supported ESP32 hardware. [ForgeUI Hosted Studio](https://studio.forgeui.co.nz) is the hosted, browser-based ForgeUI Studio application and is available for public registration.

## Related ForgeUI Projects

- [ForgeUI One](https://github.com/RTechAI/ForgeUI-One) — historical embedded runtime lineage
- [ESP32-P4 UI Studio](https://github.com/RTechAI/esp32p4-ui-studio) — historical visual export lineage
- [ForgeUI P4](https://github.com/RTechAI/ForgeUI-P4) — ESP32-P4 ForgeUI work
- [ESP32-P4 LVGL Boilerplate 3](https://github.com/RTechAI/ESP32-P4-LVGL-Boilerplate-3) — related ESP32-P4/LVGL baseline

## About ForgeUI

[ForgeUI](https://forgeui.co.nz) is developed by [RTechAI](https://github.com/RTechAI). ForgeUI Studio provides visual embedded UI/HMI development workflows for supported ESP32 hardware, while [ForgeUI Hosted Studio](https://studio.forgeui.co.nz) provides the hosted, browser-based Studio application. RTechAI is the GitHub home for ForgeUI public repositories and reference work.

## License and Third-Party Software

ForgeUI-owned code in this repository is governed by the [ForgeUI Source Available License](LICENSE). It is not an MIT license. ESP-IDF, LVGL, managed components, BSP code, and other upstream software remain subject to their respective licenses; see [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md) and the relevant component sources before redistribution or productization.

## Support

For ForgeUI ecosystem information, visit [forgeui.co.nz](https://forgeui.co.nz). For repository issues and public ForgeUI reference work, use [RTechAI on GitHub](https://github.com/RTechAI).
