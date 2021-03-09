Firmware for stick MODKAM СС2538 (with the FLASH button and without the FLASH button)

## Changelog
### jh_2538_router_20200520.hex
 * Fixed bug with Identify cluster;
 * Allowed Bootloader. Low on PA7;
 * Disabled constant light LED4;
 * NWK_MAX_DEVICE_LIST = 100;

### jh_2538_router_20200522.hex
 * Fixed a problem with switching to bootloader mode after holding the FLASH button (PA7) for a long time.
 * Added function to reset the device to factory settings by quickly pressing the RESET button 5 times. Pressing is considered fast if made before the LED1 is turned on;
 * NWK_MAX_DEVICE_LIST = 40;

### jh_2538_router_20210115.hex
 * NWK_LINK_STATUS_PERIOD = 15 sec;
 * Model Identifier - cc2538.router.v2;
 * Date Code - 20210115;
 * Added measurement and reporting of temperature from the internal sensor. Cluster Device Temperature Configuration (0x0002), CurrentTemperature attribute (0x0000). Reportin every 1 second;


## Basic version

`\Z-Stack 3.0.2\Projects\zstack\HomeAutomation\GenericApp\CC2538\`

## Indication 

**LED1** (blue, PB1) is used for indication.
* Blinking with a frequency of 1 Hz, glow duration 500 ms - **search mode** for an available network;
* Constant glow - **a device on the network**;
* LED goes out for 1 second. - **confirmation of pressing the **FLASH** button**;
* Blinking with a frequency of 1 Hz, the duration of the glow of 100 ms - mode **Identify**;
* Blinking with a frequency of 5 Hz, glow time 100 ms - to continue the reset, **release FLASH** (PA7);

## Control

* **Power on** starts the process of searching / joining the network;
* **Holding down** the FLASH button for more than 5 seconds resets the device to factory settings and a software RESET is performed. Since a low level at FLASH (PA7) is a condition for entering Bootloader mode after RESET, a quick blinking LED1 (frequency 5Hz) indicates that the condition for reset is met, but you must release it to continue button;
* A **short press** on the FLASH button sends ReportAttr (cluster 0x0 Basic, attribute 0x5 modelID);

## Simple Descriptor
```
Endpoint: 1
Profile: Home Automation (0x0104)
Application Device: Unknown (0x0100)
Input Cluster Count: 2
Input Cluster List
    Input Cluster: Basic (0x0000)
    
        Attribute: ZCL Version (0x0000)
        Data Type: 8-Bit Unsigned Integer (0x20)
        Uint8: 1 (0x01)
            
        Attribute: HW Version (0x0003)
        Data Type: 8-Bit Unsigned Integer (0x20)
        Uint8: 1 (0x01)
        
        Attribute: Manufacturer Name (0x0004)
        Data Type: Character String (0x42)
        String: jethome
    
        Attribute: Model Identifier (0x0005)
        Data Type: Character String (0x42)
        String: cc2538.router.v1    //(v2)
   
        Attribute: Date Code (0x0006)
        Data Type: Character String (0x42)
        String: 20200520 

    Input Cluster: Identify (0x0003)    
    Input Cluster: Device Temperature Configuration (0x0002) (only v2)
        Attribute: CurrentTemperature (0x0000)
        Data Type: 16-Bit Unsigned Integer (0x29)
        Uint16: temperature from internal sensor
Output Cluster Count: 1
Output Cluster List
    Output Cluster: Basic (0x0000)
```

## zigbee-herdsman-converters/devices.js
```
    //hethome
    {
        zigbeeModel: ['cc2538.router.v1'],
        model: 'cc2538.router.v1',
        vendor: 'jethome',
        description: 'zigbee router cc2538',
        fromZigbee: [],
        toZigbee: [tz.genIdentify],
        exposes: [],
    },

    {
        zigbeeModel: ['cc2538.router.v2'],
        model: 'cc2538.router.v2',
        vendor: 'jethome',
        description: 'zigbee router cc2538 with temperature sensor',
        fromZigbee: [fz.device_temperature],
        toZigbee: [tz.genIdentify],
        exposes: [e.temperature()],
    },
```
