# Firmware for TI CC2538 based devices

## Common information

* SBL (UART flashing) is enabled by default. No need to apply extra patches.

## Supported devices

* JetHome ZB3CX module for JetHub based on  [CC2538-CC2592EM](https://www.ti.com/tool/CC2538-CC2592EM-RD) reference. **Use UART firmware version for it.**
* USB stick MODKAM_V3 [device information](https://modkam.ru/?p=1112). **Use USB firmware version for it.**

## Changelog:

### Firmware version 20201010

* NV flash incremented from 12 pages to  24 pages. (`HAL_NV_PAGE_CNT`)
* Changed FLASH and NV memory boundaries
* Work with devices which are not support APS encryption (`zgApsAllowR19Sec = TRUE`)
* Didabled TCLK (`requestNewTrustCenterLinkKey = FALSE`)
* `CODE_REVISION_NUMBER` changed to `20201010`

### Firmware version 20200729

* Enabled Serial Bootloader (SBL). Use low logic level on `PA7` input to enter SBL
* Added `UART` mode firmware
* `CODE_REVISION_NUMBER` changed to `20200729`

UART(SBL) firmware update mode is desribed [here](https://mysku.ru/blog/aliexpress/79984.html).

UART flash programs:
* [cc2538-prog](https://github.com/1248/cc2538-prog)
* [cc2538-bsl](https://github.com/JelmerT/cc2538-bsl) (works on Linux, MacOS)
* [FLASH-PROGRAMMER-2](https://www.ti.com/tool/download/FLASH-PROGRAMMER-2) (Windows)

## Firmware version 20200427

Based on MODKAM_V3 firmware. 
Differences from MODKAM_V3:
* Decremented number of direct children from 100 to 80: (`NWK_MAX_DEVICE_LIST=80`)
* `CODE_REVISION_NUMBER` changed to `20200427`

## Firmware version 20200327

[Original firmware MODKAM_V3](https://github.com/reverieline/CC2538-CC2592-ZNP)

### MODKAM V3 differences form the original TI ZNP (Z-Stack 3.0.2)

* Added 4 LEDs
* NV_RAM area changed form 6 to 12 pages
* Added frontend CC2592
* UART RTS signal changed from `PD3` to `PD1`
* ZNP (`MT_VERSION`) oroduct ID changed from `0` to `2`
* Added possiblity to receive messages when `Group ID` is missing in the coordinator
* Messages for `10` and `11` endpoints are forwared to endpoint `1`
* Disable children aging
* Broadcast table size changed fron `9` to `12` (`MAX_BCAST=12`)
* UART buffer size changed form `170` to `1024` bytes
* Handling `HAL_UART_RX_FULL`, `HAL_UART_RX_ABOUT_FULL`, `HAL_UART_RX_TIMEOUT` events
* Output power changed from `19` to `22` dBm
* `CODE_REVISION_NUMBER` changed to `20200327`
* Added new parameters:
```
-DMODKAMRU_V3
-DINCLUDE_REVISION_INFORMATION
-DMT_SYS_KEY_MANAGEMENT=1
-DTP2_LEGACY_ZC
-DMULTICAST_ENABLED=FALSE

/* Large netrowk optimizations (MTO, Source Routing) */
-DINT_HEAP_LEN=12288
-DZDSECMGR_TC_DEVICE_MAX=200
-DNWK_MAX_DEVICE_LIST=100
-DCONCENTRATOR_ENABLE=TRUE
-DCONCENTRATOR_DISCOVERY_TIME=120
-DMAX_RTG_SRC_ENTRIES=400
-DMAX_NEIGHBOR_ENTRIES=100
-DSRC_RTG_EXPIRY_TIME=10
-DCONCENTRATOR_ROUTE_CACHE=TRUE
-DMTO_RREQ_LIMIT_TIME=5000

-DLINK_DOWN_TRIGGER=6
-DNWK_ROUTE_AGE_LIMIT=12
-DBCAST_DELIVERY_TIME=100
-DMAX_BCAST=12
//-DDEF_NWK_RADIUS=15
//-DDEFAULT_ROUTE_REQUEST_RADIUS=8
-DROUTE_DISCOVERY_TIME=13
//-DZDNWKMGR_MIN_TRANSMISSIONS=0
-DNWK_LINK_STATUS_PERIOD=60
```
```
// Maximums for the data buffer queue
#ifdef MODKAMRU_V3
 #define NWK_MAX_DATABUFS_WAITING    180 // Waiting to be sent to MAC
 #define NWK_MAX_DATABUFS_SCHEDULED  150 // Timed messages to be sent
 #define NWK_MAX_DATABUFS_CONFIRMED  150 // Held after MAC confirms
 #define NWK_MAX_DATABUFS_TOTAL      255 // Total number of buffers
#else
 #define NWK_MAX_DATABUFS_WAITING    8   // Waiting to be sent to MAC
 #define NWK_MAX_DATABUFS_SCHEDULED  5   // Timed messages to be sent
 #define NWK_MAX_DATABUFS_CONFIRMED  5   // Held after MAC confirms
 #define NWK_MAX_DATABUFS_TOTAL      12  // Total number of buffers
#endif
```
