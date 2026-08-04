# Custom Flight Controller
A custom STM32-based flight controller designed from the ground up for quadcopters. This project includes PCB design using KiCad and embedded firmware using Ardupilot.

## Features
- STM32 Microcontroller
- 6-axis IMU
- Barometer
- USB-C
- PWM
- I2C and SPI

## Hardware
| Component | Part |
|-----------|------|
| MCU | STM32F405 |
| IMU | ICM-42688-P |
| Barometer | MS5611 |

## Status

- [ ] Hardware
  - [x] Select MCU
  - [x] Select IMU
  - [x] Select Barometer
  - [ ] Select connectors
  - [ ] Complete schematic
  - [ ] PCB layout
  - [ ] Design review
  - [ ] Order PCB
  - [ ] Assemble board
        
- [ ] Firmware
  - [ ] Configure Ardupilot
  - [ ] Build Ardupilot
  - [ ] Flash firmware

- [ ] Testing
  - [ ] Mission Planner
  - [ ] Flight test

![PCB Progress - IMU](images/IMU-layout.png)
![PCB Progress - Schematic](images/FC_Schematic1_8-04.png)
![PCB Progress - Schematic](images/FC_Schematic2_8-04.png)

## Design Decisions

### Why STM32F405?

The STM32F405 was selected because it provides:
- Sufficient processing power for flight control
- Compatibility with ArduPilot
- Large community support

### Why SPI for IMU?

SPI was selected over I2C due to:
- Higher bandwidth
- Lower latency
- Noise immunity

## Lessons Learned

- SPI facilitates DMA, which offloads data transfers from the main MCU. This prevents processor lag. SPI needs pull up resistors for CS since it sets CS low to select devices. Use GPIO for CS instead of built-in NSS so that ArduPilot can handle CS lines through software.
-  IMU enhances GPS reliability in tunnels or areas with EM interference.
-  Each principal axis (pitch, roll, yaw) translates to accelerometer, gyroscope, and magnetometer.
-  Place smallest decoupling capacitors closest to pin to minimize trace inductance. Smaller capacitors filter high frequency noise, and inductive impedance is proportial to frequency.
-  Vref serves as a precise baseline voltage for ADCs and DACs, isolating noise and maintaining consistent voltage.
  
## Goals

The objective of this project is to design a flight controller from scratch while learning PCB design, embedded systems, and hardware debugging.
