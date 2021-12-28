## Firmware for EFR32MG21 based devices

"z4-*" - firmware files for USB Zigbee stick "JetStick Z4" - https://wiki.jethome.ru/jetstick_z4

"z4-bootloader-uart-xmodem-*" - The bootloader firmware files uses the established XMODEM-CRC protocol for data upload. The bootloader enables users to program device through a UART without the need for a debugger.

"z4-ncp-uart-sw-*" - Zigbee coordinator firmware files uses Silicon Labs Zigbee stack from their EmberZNet SDK.

Firmware file with "sw" uses software XON/XOFF flow control.
Baud rate specified in filename and can be 57600 or 115200. Default baud rate is 115200 if not specified in filename.

## Hardware

JetStick Z4 uses following pins of the microcontroller:
 * USART TX Pin - PA05;
 * USART RX PIN - PA06;
 * LED0 - PD02;
 * LED1 - PD03.
