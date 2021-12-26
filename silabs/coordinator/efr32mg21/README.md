## Firmware for EFR32MG21 based devices

"z4-*" - firmware files for USB Zigbee stick "JetStick Z4" - https://wiki.jethome.ru/jetstick_z4

"z4-bootloader-uart-xmodem-*" - The bootloader firmware files uses the established XMODEM-CRC protocol for data upload. The bootloader enables users to program device through a UART without the need for a debugger.

"z4-ncp-uart-sw-*" - Zigbee coordinator firmware files uses Silicon Labs Zigbee stack from their EmberZNet SDK.


## Hardware
 * Baud rate - 115200;
 * USART TX Pin - PA05;
 * USART RX PIN - PA06;
 * Xon-Xoff;
 * LED0 - PD02;
 * LED1 - PD03;
