## CC1352P2_CC2652P_launchpad_coordinator_20220524
### Compile
[Basic version 20220219](https://github.com/Koenkk/Z-Stack-firmware/tree/develop/coordinator/Z-Stack_3.x.0/)  
1. Build firmware for CC1352P2_CC2652P_launchpad_coordinator_20220219 according to [instructions](https://github.com/Koenkk/Z-Stack-firmware/blob/develop/coordinator/Z-Stack_3.x.0/COMPILE.md); 
2. Go to your CCS workspace and apply `firmware_20220524.patch`;
3. Build a project;

### Changelog
 * Changes for version 20220219 https://github.com/Koenkk/Z-Stack-firmware/blob/develop/coordinator/Z-Stack_3.x.0/CHANGELOG.md;
 
## CC1352P2_CC2652P_launchpad_coordinator_20211219
### Compile
[Basic version 20211217](https://github.com/Koenkk/Z-Stack-firmware/tree/develop/coordinator/Z-Stack_3.x.0/)  
1. Build firmware for CC1352P2_CC2652P_launchpad_coordinator_20211217 according to [instructions](https://github.com/Koenkk/Z-Stack-firmware/blob/develop/coordinator/Z-Stack_3.x.0/COMPILE.md); 
2. Go to your CCS workspace and apply `firmware_20211219.patch`;
3. Build a project;

### Changelog
 * Changes for version 20211217 https://github.com/Koenkk/Z-Stack-firmware/blob/develop/coordinator/Z-Stack_3.x.0/CHANGELOG.md;
 * Transmit power is set to 20dBm;
 * LED indication as in version [CC1352P2_CC2652P_launchpad_coordinator_20210218](https://github.com/jethome-ru/zigbee-firmware/tree/master/ti/coordinator/cc2652);

## CC1352P2_CC2652P_launchpad_coordinator_20210218
[Basic version 20210120](https://github.com/Koenkk/Z-Stack-firmware/blob/master/coordinator/Z-Stack_3.x.0/bin/CC1352P2_CC2652P_launchpad_coordinator_20210120.zip)  
Added LED function (DIO_6 red, DIO_7 green).
* Simultaneous double short blinking of the red and green LED - the stick has restarted;
* Green LED is on - the network is running;
* Flashing green LED - permit joining enable;
* Flashing red LED - APS frame received;
