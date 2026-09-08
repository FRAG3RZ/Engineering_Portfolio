# Formula Student Driver Display

Custom embedded driver display developed for **UGRacing Formula Student**, combining a custom PCB, STM32 firmware, CAN communication, and an 800×480 touchscreen interface.

> **Tech:** STM32F767 · Embedded C · CAN · SSD1963 · GT911 · FMC / Intel 8080-style parallel interface · Altium Designer

## Overview

The goal of this project was to design and integrate a compact dashboard-mounted display for a Formula Student race car. The system combines custom electronics with low-level firmware and a purpose-built graphical interface for displaying live vehicle information.

My work covered the project end-to-end: PCB design and assembly, STM32 firmware, display communication, CAN integration, UI development, debugging, and final system integration.

## Highlights

- Designed and assembled a **custom SMD PCB** for the dashboard-mounted embedded system.
- Developed firmware in **C on the STM32F767** platform.
- Implemented an **Intel 8080-style parallel interface** to an 800×480 SSD1963-based display.
- Added **CAN communication** with other race-car subsystems.
- Developed a custom embedded graphics/UI layer with reusable layout and widget abstractions.
- Integrated and tested the completed hardware and firmware as part of the Formula Student dashboard.

## System Architecture

```text
Vehicle CAN Bus ───────┐
                       │
Local Inputs / ADC ────┼──> STM32F767 ──> FMC / Parallel Bus ──> SSD1963 ──> 800×480 LCD
                       │
Touch Controller ──────┘
```

The firmware is split into peripheral-level modules and higher-level display logic. The project includes dedicated code for CAN, ADC, FMC, touch input, graphics primitives, text rendering, and dashboard UI behaviour.

## Firmware

The display software is implemented in low-level C and organized around reusable drawing and layout primitives rather than a single monolithic screen routine.

The dashboard layer includes abstractions for:

- screen regions and layout geometry;
- vertical telemetry bars;
- numeric display blocks;
- text and graphics rendering;
- threshold-based status colouring;
- touch-sensitive UI areas;
- vehicle data presentation.

This made it easier to iterate on the interface while keeping hardware-specific display code separated from higher-level UI behaviour.

## Hardware

The hardware portion includes a custom PCB designed around the requirements of the dashboard installation and STM32-based control electronics.

Key work included:

- schematic and PCB design;
- SMD assembly and rework;
- microscope soldering;
- bring-up and debugging with bench instrumentation;
- integration with the display and vehicle electronics.

See [`PCB_V2/`](PCB_V2/) for the hardware design files.

## Repository Structure

```text
Dashboard_Screen_2026/
├── README.md
├── PCB_V2/              # PCB design files
├── SSD1963_LCD_CODE/    # STM32 firmware and display software
├── Extra_Stuff/         # Supporting project material
└── Zips/                # Archived project files
```

The repository is being cleaned up for public presentation, so some historical development files remain alongside the final project sources.

## What I Learned

This project gave me practical experience taking an embedded system from **schematic and PCB design through firmware, debugging, communication interfaces, UI development, and final vehicle integration**. It also reinforced the importance of designing hardware and software together when working under real mechanical and electrical constraints.
