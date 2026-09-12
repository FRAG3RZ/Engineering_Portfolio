<h1 align="center">🤖 Rover Showcase & Operator Guide</h1>

<p align="center">
  Setup, demonstration, Bluetooth control, and maintenance guide for the
  <b>Autonomous Line-Following Rover</b>.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Showcase-Operator%20Guide-0969DA?style=flat-square">
  <img src="https://img.shields.io/badge/Bluetooth-Manual%20Control-8250DF?style=flat-square">
  <img src="https://img.shields.io/badge/Modes-Slow%20%7C%20Fast-2EA043?style=flat-square">
  <img src="https://img.shields.io/badge/Firmware-Full%20%7C%20Line%20Following-F5822A?style=flat-square">
</p>

<p align="center">
  <img src="../images/rover-final.jpg"
       alt="Autonomous line-following rover"
       width="800">
</p>

## 📌 Overview

This guide is intended for operating the rover during **university showcases,
demonstrations, and manual testing**.

The rover supports autonomous line following, Bluetooth manual control,
runtime debug telemetry, and two selectable speed modes.

> [!NOTE]
> Two pre-built firmware versions are included with the showcase files:
>
> * **Full functionality** — includes the complete rover feature set
> * **Line-following only** — simplified demonstration build focused on autonomous line following

---

## 🚦 Selecting Slow or Fast Mode

The rover has two operating-speed configurations:

| MCU Switch Position | Mode      |
| ------------------- | --------- |
| **Left**            | Slow mode |
| **Right**           | Fast mode |

The mode is selected using the switch on the **bottom-left of the MCU board**.

> [!IMPORTANT]
> Set the switch position **before powering on the rover**.
> The operating mode is selected during startup.

---

## 📡 Bluetooth Control

The Bluetooth module remains active in all operating modes and can accept
manual-control commands at any time.

The rover also transmits debug information over the serial connection
approximately every **100 ms**.

### Bluetooth Details

| Setting         | Value          |
| --------------- | -------------- |
| **Device Name** | `TEAM_2_ROVER` |
| **PIN**         | `1234`         |

### Connecting

1. Pair your computer with `TEAM_2_ROVER`.
2. Connect to the Bluetooth serial port.
3. Open the appropriate serial terminal for your operating system.

### Windows

Open a serial terminal using the Bluetooth COM port assigned by Windows.

Common ports during development were:

```text
COM4
COM5
```

The exact port may differ depending on the computer.

### macOS

Open a serial terminal using the Bluetooth serial device.

The device used during development was:

```text
/dev/tty.cu.TEAM_2_ROVER
```

---

## 🎮 Manual-Control Commands

The rover accepts individual character commands through the Bluetooth serial
connection.

| Command   | Action                                                                    |
| --------- | ------------------------------------------------------------------------- |
| `w`       | Slow forward                                                              |
| `s`       | Slow reverse                                                              |
| `a`       | Slow left                                                                 |
| `d`       | Slow right                                                                |
| `W`       | Full-speed forward                                                        |
| `S`       | Full-speed reverse                                                        |
| `A`       | Full-speed left                                                           |
| `D`       | Full-speed right                                                          |
| `z` / `Z` | Coast to a stop and wait for another command                              |
| `q` / `Q` | Full stop / brake                                                         |
| `x` / `X` | Exit manual control and resume autonomous line following from `SEEK` mode |

### Coast

```text
z / Z
```

Removes the active drive command and allows the rover to **coast to a full
stop**. The rover then waits for another input.

### Brake / Full Stop

```text
q / Q
```

Commands a **full stop using braking**.

The rover remains stopped until it is restarted or another valid control
input is received.

### Return to Autonomous Operation

```text
x / X
```

Exits manual-control mode and returns the rover to autonomous line following,
starting from the **SEEK** state.

---

## 🔧 Accessing the Rover

To access the internal power pack for recharging or replacement:

1. Remove the **four enclosure screws**.
2. Disconnect the two cables leading to the modules on the **right-hand side** of the rover:

   * the four-wire connection between the side module and the PCB
   * the four-wire connection entering the top of the colour-sensing module
3. For the colour-sensor connection, disconnect the cable from the **module side rather than the MCU-board side**. This is easier during servicing.
4. Remove the internal power pack. It is secured to the bottom of the rover using **Velcro**.
5. Recharge or replace the power pack as required.
6. Reinstall the pack and reconnect both right-side module connections:

   * ultrasonic sensing
   * colour sensing
7. Refit the enclosure and screws.

> [!IMPORTANT]
> Before operating the rover again, verify that both right-side sensor
> connections have been reconnected correctly.

---

## 🛠️ Troubleshooting

### Rover Starts in an Incorrect State

Occasionally the rover may initialise in an incorrect control state.

A typical symptom is the rover continuously **spinning in circles immediately
after startup**.

If this occurs:

1. Turn the rover off.
2. Turn it back on.
3. Verify that normal autonomous behaviour resumes.

If the behaviour continues, repeat the restart before beginning the
demonstration.

---

### Bluetooth Disconnects

The Bluetooth connection can occasionally disconnect during use.

The most reliable recovery procedure found during development is:

1. Turn the rover off.
2. Disconnect the computer from the Bluetooth module.
3. Power the rover back on.
4. Reconnect to `TEAM_2_ROVER`.
5. Reopen the serial terminal.

---

## 💻 Serial Terminal Options

Several serial-terminal options can be used.

### macOS — `tio`

During development, `tio` was used frequently on macOS and provides a simple
terminal interface for the Bluetooth serial connection.

### PlatformIO

If using VS Code with PlatformIO, the serial monitor can also be opened with:

```text
pio monitor
```

### VS Code Serial / Debug Terminal

The VS Code terminal can also be used, although some configurations require
pressing **Enter** after each character command.

---

## 🎮 Game Controller Support — Windows

For demonstrations on Windows, **AntiMicroX** can be used to map a game
controller to the rover's keyboard commands.

A compatible AntiMicroX configuration file is included with the showcase
files.

### Setup

1. Open **AntiMicroX**.
2. Load the included configuration file.
3. Connect the game controller.
4. Confirm that the controller appears in AntiMicroX.
5. Open and select the rover's Bluetooth serial terminal.
6. Controller inputs should now generate the corresponding keyboard commands
   in the terminal.

This provides a convenient way to demonstrate manual rover control using a
game controller rather than entering commands directly from the keyboard.

---

## ✅ Showcase Checklist

Before a demonstration:

* Confirm that the desired **slow / fast mode** is selected before startup.
* Confirm that the required firmware build is loaded.
* Check that the rover starts in the expected autonomous state.
* Pair with `TEAM_2_ROVER` if Bluetooth control will be demonstrated.
* Open the correct serial port and confirm debug output is being received.
* Verify manual directional commands if required.
* Confirm that the ultrasonic and colour-sensor connections are secure.
* Check that the rover can return to autonomous operation using `x` / `X`.

---

<p align="center">
  <a href="../../README.md">← Back to Autonomous Line-Following Rover</a>
</p>
