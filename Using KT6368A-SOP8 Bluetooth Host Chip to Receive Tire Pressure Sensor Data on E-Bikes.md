# Using KT6368A-SOP8 Bluetooth Host Chip to Receive Tire Pressure Sensor Data on E-Bikes

![Image](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062400.png)

## 1. Introduction
The KT6368A Bluetooth chip now supports host mode, enabling it to scan nearby tire pressure sensors (TPMS). In this setup, the KT6368A acts as an observer, since testing has shown that the TPMS modules operate in broadcast-only mode (non-connectable, discoverable advertising).

## 2. TPMS Overview
From testing, we verified that TPMS modules can be discovered via Bluetooth advertising but do not support connection. This aligns with the technical documentation provided with the TPMS device:

![TPMS Documentation](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062402.png)

## 3. Sample Data Received
When the Bluetooth chip receives data from the TPMS and forwards it via UART (serial), the raw data format is as follows:

![Data Format](https://github.com/blevoice/pic/blob/489878ee15153e8f0120921c328efd281c0a282d/062403.png)

```hex
4C 43 54 50 4D 53 2C 3A 85 92 3B CD FB 2C 07 3B 92 85 3A 83 4D B7 10 20 6D