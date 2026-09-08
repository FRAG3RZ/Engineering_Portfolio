# Autonomous Line-Following Rover

Autonomous embedded rover developed as a third-year engineering team project, combining custom electronics, C++ control software, multiple sensors, and system-level integration.

> **Tech:** C++ · Mbed OS · NXP KL25Z · State-Based Control · Ultrasonic Sensing · Colour Sensing · Bluetooth · Custom PCBs

## Overview

The rover was designed to navigate a marked course autonomously while responding to line position, obstacles, and colour cues. The final system integrates motor control, line sensing, ultrasonic ranging, colour sensing, Bluetooth manual control, and debug telemetry around a central embedded controller.

I led the project team and focused on the core electronics, control software, and overall system architecture and integration.

## Highlights

- Led the design, implementation, and integration of the autonomous rover system.
- Designed core electronics for **motor control and line sensing**.
- Developed the main embedded control software in **C++ on Mbed OS**.
- Implemented line following, line reacquisition, obstacle avoidance, colour sensing, and manual Bluetooth control.
- Built the control flow around explicit operating states and obstacle-avoidance substates.
- Integrated periodic sensor updates, shared sensor state, debouncing, and timed transitions into the runtime architecture.

## System Architecture

```text
Line Sensors ───────────┐
                       │
Ultrasonic Sensors ─────┤
                       │
Colour Sensor ──────────┼──> KL25Z MCU ──> Motor Control ──> Drive Motors
                       │
Bluetooth Control ──────┤
                       │
Debug / Telemetry ──────┘
```

The system is structured so that sensing, control decisions, and actuator commands remain logically separated while sharing the same embedded runtime.

## Control Software

The core controller uses a state-driven architecture for autonomous behaviour. Major states include line following, line seeking/reacquisition, alignment, braking, obstacle avoidance, stopping, and manual Bluetooth control.

Obstacle avoidance uses additional substates to manage timed manoeuvres and reacquisition of the line after passing an obstacle.

Periodic tasks are scheduled using Mbed tickers. Sensor data is shared with the control loop through protected shared state so that asynchronous updates can be consumed safely by the main controller.

## Sensing & Behaviour

The rover combines several sensing modes:

- **Line sensing** for closed-loop path following and line reacquisition.
- **Ultrasonic ranging** for obstacle detection and avoidance.
- **RGB colour sensing** for course-state decisions.
- **Bluetooth serial control** for manual driving and debugging.

A configurable line-follow-only mode was also retained for isolated testing of the core line-control behaviour.

## Hardware

The electronics include custom circuitry for the motor-control and line-sensing subsystems, alongside the KL25Z development platform and external sensor modules.

Project hardware work included:

- schematic and PCB design;
- motor-driver and sensor electronics;
- hardware assembly and integration;
- sensor calibration and debugging;
- final system bring-up.

## Repository Structure

```text
TDP3_Rover/
├── README.md
├── Rover_KL25Z/             # Main C++ / Mbed firmware
├── Rover_Guide/             # Operator guide and supporting files
├── Rover_Guide.zip          # Historical archive
└── Rover_Schematics_&_PCBs.zip
```

The repository is being cleaned up for public presentation, so some original project archives are still retained alongside the source tree.

## What I Learned

This project strengthened my experience in **embedded C++, state-driven control, sensor integration, hardware/software debugging, and technical leadership**. The biggest engineering challenge was integrating several imperfect real-world sensors and behaviours into one predictable autonomous system rather than solving each subsystem independently.
