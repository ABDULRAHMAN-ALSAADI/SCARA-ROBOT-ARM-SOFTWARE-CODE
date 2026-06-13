# SCARA Robot Arm — v10.22

<img width="4469" height="3839" alt="SCARA Robot Arm Hardware" src="https://github.com/user-attachments/assets/c458b0e9-8e46-4d0a-9d5a-0e3ad11cfd64" />

A full-stack SCARA robot arm control system running on an ESP32. The firmware handles forward and inverse kinematics, coordinated multi-axis motion, recipe-based automation, and persistent storage — all controllable through a browser-based interface over WebSocket.

---

## Overview

This project started as a custom-built SCARA arm and grew into a modular control system designed to be adapted for different arm geometries and configurations. The goal was a self-contained embedded system — no PC required during operation, no external dependencies. Just an ESP32, a browser, and your robot.

---

## Features

**Motion Control**
- Coordinated multi-axis movement with acceleration profiles
- Stepper motor integration via standard driver interfaces
- Full homing system with limit switch support

**Kinematics**
- Forward Kinematics (FK) — joint angles → end effector position
- Inverse Kinematics (IK) — Cartesian target → joint angles
- Joint-space and Cartesian-space positioning modes

**Recipe System**
- Create and save sequences of robot operations
- Execute repeatable automation routines
- Stored persistently on-device via LittleFS

**Web Interface**
- Real-time control from any browser on the local network
- Manual jogging, Cartesian positioning, and joint positioning
- Recipe creation, editing, and execution
- Live system status monitoring

<img width="1554" height="1580" alt="Web Interface" src="https://github.com/user-attachments/assets/4119ec38-079b-4bd7-a965-3a554a48a245" />

---

## Hardware

| Component | Details |
|-----------|---------|
| Controller | ESP32 |
| Actuators | Stepper motors + stepper drivers |
| Sensors | Limit switches, homing sensors |

---

## Software Architecture

```
Browser (WebSocket)
       │
       ▼
ESP32 Main Controller
 ├── Motion Control       — Stepper coordination, acceleration, homing
 ├── Kinematics           — FK / IK solver, coordinate transforms
 ├── Recipe Manager       — Sequence storage and execution
 ├── State Manager        — Robot state tracking
 ├── Storage (LittleFS)   — Persistent settings and recipes
 └── Communication Layer  — WebSocket server, command processing
       │
       ▼
Stepper Drivers + Sensors
```

---

## Project Structure

```
V10_22/
├── MotionControl/
├── Kinematics/
├── RecipeManager/
├── StateManager/
├── Communication/
├── Storage/
├── WebInterface/
├── Config/
└── Main/
```

---

## Getting Started

Read the documentation in this order:

1. [`BUILD_GUIDE.md`](docs/BUILD_GUIDE.md) — Mechanical assembly and wiring
2. [`CALIBRATION_GUIDE.md`](docs/CALIBRATION_GUIDE.md) — Configuring the arm for your geometry
3. [`SOFTWARE_ARCHITECTURE.md`](docs/SOFTWARE_ARCHITECTURE.md) — How the firmware is structured
4. [`KINEMATICS.md`](docs/KINEMATICS.md) — FK and IK implementation details

---

## Configuration

Before running the firmware on your own robot, update the following in `Config/`:

- Link lengths (arm segment dimensions)
- Motor directions and steps per revolution
- Joint limits (min/max angles)
- Homing parameters
- WiFi credentials

Full configuration instructions are in [`docs/CALIBRATION_GUIDE.md`](docs/CALIBRATION_GUIDE.md).

---

## Building Your Own

If you're printing or redesigning the arm:

1. Assemble the mechanical structure
2. Mount and wire the stepper motors
3. Install limit switches and homing sensors
4. Update link lengths and motor config
5. Run the calibration procedure
6. Verify FK output matches physical position
7. Verify IK solutions are reachable
8. Run a full motion test

---

## Documentation

| File | Description |
|------|-------------|
| `BUILD_GUIDE.md` | Hardware assembly and wiring |
| `CALIBRATION_GUIDE.md` | Geometry configuration and calibration |
| `SOFTWARE_ARCHITECTURE.md` | Firmware structure and module overview |
| `KINEMATICS.md` | FK and IK math and implementation |
| `TROUBLESHOOTING.md` | Common issues and fixes |

---

## Roadmap

- [ ] Closed-loop motor control
- [ ] Advanced trajectory planning
- [ ] Collision avoidance
- [ ] Vision system integration
- [ ] ROS2 bridge
