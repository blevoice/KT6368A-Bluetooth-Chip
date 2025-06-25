# Engineer's Hands-on Review of the KT6368A Bluetooth Chip

**Categories**: Bluetooth Technical | Audio Products | AIoT Solutions | Bluetooth Wireless Engineerings | Embedded Systems | Voice chips | Bluetooth Chips | Bluetooth Audio Chips | Sound Playback

![KT6368A Chip](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062501.png)

Not long ago, someone in a tech group shared info about a SOP8 Bluetooth chip priced at just $1.06 USD, sparking a heated discussion. Of course, I couldn't contain my excitement and immediately placed an order for a few pieces.  
[AliExpress Link](https://www.aliexpress.com/item/3256808888424851.html)

The chip model is **KT6368A**, which is the product of Shenzhen Qingyue Electronics Co., Ltd. According to the official description:

> KT6368A is a dual-mode Bluetooth data chip, supporting Bluetooth 5.1. Its highlights include ultra-small size, extremely low price, and straightforward transparent transmission and UART AT command functionality—greatly reducing the difficulty and cost of embedding Bluetooth into other products. It supports both SPP and BLE, though only one protocol can be used at a time.  
> **Note**: The biggest strengths of this chip are low cost, simple usage, and easy production—and nothing else. It also supports low power consumption.

## Ultra-Simple Circuit Design

This chip's circuit is shockingly simple:

![Circuit Diagram](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062502.png)

Just provide power, connect a crystal oscillator, and attach an antenna—then you're ready to transmit and receive data via UART.

## PCB and Soldering

I originally planned to design a PCB myself. But just as I was about to start, a friend had already finished his board design, soldered it, and completed debugging. So I asked him for two spare blank boards and did the soldering myself using a soldering iron.

![Soldered Board](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062503.jpg)

The board is based on the schematic mentioned above. Here are a few reminders:

- The crystal oscillator should be **24 MHz**; you can buy it along with the Bluetooth chip on AliExpress — $1.38 USD for 10 pcs.
  
  ![Crystal Oscillator](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062504.png)

- Capacitors C3 and C4 are **not needed**.
- Likewise, C2 and L2 are **not needed**.
- The PCB antenna can directly copy the footprint provided by the manufacturer.
- Although pin 7 and pin 8 are labeled USBDP and USBDM, they are actually **UART TX and RX**.

## Connecting the Chip

After soldering, I used a USB-to-TTL adapter to power the board and connect to the serial port.

### 1) Check for Boot Info Output

![Boot Info](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062505.jpg)

### 2) Modify Bluetooth Name and MAC Address

This can be done using AT commands.

![AT Commands](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062506.png)

### 3) Soft Reset

Use the command: `AT+CZ\r\n`

### 4) Mobile-to-Board Data Transmission

- On iPhone, download the app **LightBlue**.
- For Android, there's also a version: [LightBlue_1.1.2.apk](https://example.com/LightBlue_1.1.2.apk).
- Turn on Bluetooth, open LightBlue, and search for nearby devices.
- Find and connect to the KT6368A Bluetooth device.

![Device Connection](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062507.jpg)

Once connected, the status looks like this:

![Connection Status](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062508.jpg)

#### a) Sending Data from Phone to Board

![Phone to Board 1](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062509.jpg)  
![Phone to Board 2](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062510.jpg)  
![Phone to Board 3](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062511.jpg)

On the computer side, you can see the data received via the serial terminal:

![Serial Terminal Output](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062512.jpg)

#### b) Sending Data from Board to Phone

On the phone, first tap **Notify** to enable data reception:

![Enable Notify 1](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062513.jpg)  
![Enable Notify 2](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062514.jpg)  
![Enable Notify 3](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062515.jpg)

On the PC, send data via a serial port debugging tool:

![Serial Port Debugging](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062516.jpg)

The phone receives the corresponding data:

![Phone Data Reception](https://github.com/blevoice/pic/blob/afbc0a5253e99c8898fbb6f054948c58529f99bc/062517.jpg)

## Final Thoughts

This chip is truly a testament to **Made in China** engineering—designed with engineers in mind: simple, user-friendly, and extremely affordable. Compared to common Bluetooth SoCs, it is far easier to use. It is already widely adopted in products like:

- Selfie sticks
- Anti-lost devices
- BMS protection boards
- Aroma diffusers
- Car tire pressure monitoring systems (TPMS)

In today's market, where Bluetooth chips tend to be expensive and complicated, the **KT6368A** clearly aims to deliver maximum cost-performance—making it an excellent alternative for Bluetooth applications.