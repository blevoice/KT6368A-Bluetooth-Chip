# Using KT6368A-SOP8 Bluetooth Host Chip to Receive Tire Pressure Sensor Data on E-Bikes

![Image](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062400.png)

## 1. Introduction
The KT6368A Bluetooth chip now supports host mode, enabling it to scan nearby tire pressure sensors (TPMS). In this setup:
- KT6368A acts as an observer
- TPMS modules operate in broadcast-only mode (non-connectable, discoverable advertising)

## 2. TPMS Overview
- TPMS modules can be discovered via Bluetooth advertising
- Does not support connection
- Verified through testing and technical documentation

![TPMS Documentation](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062402.png)

## 3. Sample Data Received
Raw data format when received via UART:

![Data Format](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062403.png)

Payload structure:
1. `4C 43 54 50 4D 53` → Bluetooth device name ("LCTPMS")
2. `3A 85 92 3B CD FB` → Device MAC address
3. `07 3B 92 85 3A 83 4D B7 10 20` → Manufacturer Specific data (actual sensor data)
4. `6D` → XOR checksum

![Data Breakdown](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062404.png)

## 4. Bluetooth Scanning Strategy
- Scanning fully handled by Bluetooth chip
- MCU only needs to control power
- Recommended scanning frequency: 500ms-1s (search for "LCTPMS" devices)
- Power off chip when not scanning to save energy
- XOR checksum added for data validation

**XOR Checksum Generation (C Code):**
![Checksum Code](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062405.png)

## 5. Broadcast Cycle Observation
- Two broadcast cycles typically captured
- TPMS transmits for ~20 seconds before entering low-power mode

![Broadcast Cycle](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062406.png)

## 6. Testing Setup
- Front and back of TPMS shown
- Uses pressurized sprayer as simulated tire to trigger TPMS