# Using KT6368A-SOP8 Bluetooth Host Chip to Receive Tire Pressure Sensor Data on E-Bikes

![Image](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062400.png)

## 1. Introduction
The KT6368A Bluetooth chip now supports host mode, enabling it to scan nearby tire pressure sensors (TPMS). In this setup, the KT6368A acts as an observer, since testing has shown that the TPMS modules operate in broadcast-only mode (non-connectable, discoverable advertising).

## 2. TPMS Overview
From testing, we verified that TPMS modules can be discovered via Bluetooth advertising but do not support connection. This aligns with the technical documentation provided with the TPMS device:

![TPMS Documentation](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062402.png)

## 3. Sample Data Received
When the Bluetooth chip receives data from the TPMS and forwards it via UART (serial), the raw data format is as follows:
4C 43 54 50 4D 53 2C 3A 85 92 3B CD FB 2C 07 3B 92 85 3A 83 4D B7 10 20 6D

![Data Format](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062403.png)

This payload contains four parameters, each separated by a comma (0x2C):
4C 43 54 50 4D 53: corresponds to the Bluetooth device name ("LCTPMS")
3A 85 92 3B CD FB: the device MAC address
07 3B 92 85 3A 83 4D B7 10 20: FF (Manufacturer Specific) data, i.e., the actual sensor data
6D: final byte is the XOR checksum

![Data Breakdown](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062404.png)

## 4. Bluetooth Scanning Strategy

The scanning process is fully handled by the Bluetooth chip.
The MCU only needs to control power to the chip.
Recommended scanning frequency: every 500ms or 1 second, searching for devices with names like "LCTPMS".
When scanning is not required, MCU can power off the chip to save energy and gain more control.
To ensure data stability between the Bluetooth chip and the MCU, a simple XOR checksum is added for validation.
XOR Checksum Generation (C Code):
u8 generate_xor_checksum(u8 *data, u8 length) {
    u8 checksum = 0;
    for (int i = 0; i < length; i++) {
        checksum ^= data[i];
    }
    return checksum;
}

![Checksum Code](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062405.png)

## 5. Broadcast Cycle Observation
Real-world testing shows that two broadcast cycles are typically captured, indicating that the TPMS transmits for about 20 seconds before entering low-power mode.

![Broadcast Cycle](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062406.png)

## 6. Testing Setup
Front and back of the TPMS are shown.
The test uses a pressurized sprayer as a simulated tire to trigger the TPMS.
When pressure is applied, the sensor wakes up automatically and begins broadcasting data.
