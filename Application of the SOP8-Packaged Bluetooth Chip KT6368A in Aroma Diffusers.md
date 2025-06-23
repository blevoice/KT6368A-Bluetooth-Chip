# Application of the SOP8-Packaged Bluetooth Chip KT6368A in Aroma Diffusers

## I. Introduction

The KT6368A Bluetooth chip is the latest product developed by JieLi (杰理) using an SOP8 package, based on a 40nm process technology and 12-inch wafer. This advanced manufacturing process brings not only improved performance, but also lower cost.

Internally, the chip integrates a Bluetooth SoC and a built-in 25Q20 SPI flash using stacked packaging.
Although this combination significantly reduces cost, its power consumption performance still lags behind foreign brands such as Nordic and Dialog.
However, in typical use cases, ultra-low power is not a strict requirement — this is where the cost-performance advantage of KT6368A becomes very compelling.

The SOP8 packaging also helps customers reduce both development and manufacturing costs.

![KT6368A Chip](https://github.com/blevoice/pic/blob/7f3d823eb40ec2a3930740e7d57e275a3e3db376/062301.png)

## II. Hardware Overview

### 2.1 Minimal System Hardware Description
![Minimal System](https://github.com/blevoice/pic/blob/7f3d823eb40ec2a3930740e7d57e275a3e3db376/062203.png)

The chip uses an SOP8 package and requires 3.3V power supply.

It connects to an external 24MHz crystal oscillator with specifications: [24M - 12pF - 10ppm], forming the minimal system.

Pin 2 is used as a Bluetooth connection status indicator.

Pins 7 and 8 are used for UART communication (configurable baud rate).

The Bluetooth antenna and RF section do not require user-side design. Just follow our provided reference layout for the PCB.

If custom antenna requirements exist, our documentation also includes comprehensive reference designs.

### 2.2 Chip Version and Feature Guide
![Version Comparison](https://github.com/blevoice/pic/blob/7f3d823eb40ec2a3930740e7d57e275a3e3db376/062303.png)

When ordering samples, you can choose the version based on your specific application needs.

Please note:

- Different versions have different default Bluetooth names.
- Functional differences also exist between versions — be sure to select appropriately based on your requirements.

## III. Aroma Diffuser Application Example

This example PCBA integrates:

- A Cortex-M0 CPU
- The KT6368A Bluetooth chip
- A voice playback chip
- A motor driver

The Bluetooth functionality is controlled via a WeChat Mini Program, making it very user-friendly and convenient.

Due to business confidentiality, detailed functional logic is not disclosed here.

![Application 1](https://github.com/blevoice/pic/blob/7f3d823eb40ec2a3930740e7d57e275a3e3db376/062304.png)

![Application 2](https://github.com/blevoice/pic/blob/7f3d823eb40ec2a3930740e7d57e275a3e3db376/062305.png)