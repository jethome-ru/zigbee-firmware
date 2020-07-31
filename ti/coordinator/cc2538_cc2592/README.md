# Прошивки для ZigBee модулей на основе SoC TI CC2538

## Поддерживаемые устройства

### ZigBee модуль JetHome ZB3CX

Модуль основан на референс дизайне TI [CC2538-CC2592EM](https://www.ti.com/tool/CC2538-CC2592EM-RD)

### USB стик MODKAM_V3

[Описание устройства](https://modkam.ru/?p=1112)

Стик основан на готовых модулях CC2538 SZ12 китайского производства, которые также используют референс дизайн TI [CC2538-CC2592EM](https://www.ti.com/tool/CC2538-CC2592EM-RD)

## Прошивка JetHome версия 20200729

Отличия от версии 20200427
* Включена возможность перепрошивки по UART с помощью Serial Bootloader (SBL). Вход в режим загрузчика осуществляется по низкому логическому уровню на выводе PA7; 
* Добавлен вариант прошивки с интерфейсом связи по UART;
* Изменено значение версии прошивки (параметр `CODE_REVISION_NUMBER`) на 20200729.

Процесс прошивки по UART хорошо описан в данной [статье](https://mysku.ru/blog/aliexpress/79984.html).

Для прошивки по UART в Linux можно использовать программы:
* [cc2538-prog](https://github.com/1248/cc2538-prog)
* [cc2538-bsl](https://github.com/JelmerT/cc2538-bsl)

Для прошивки по UART в Windows можно использовать программу:
* [FLASH-PROGRAMMER-2](https://www.ti.com/tool/download/FLASH-PROGRAMMER-2)

## Прошивка JetHome версия 20200427

Основана на прошивке MODKAM_V3. Отличия от оригинальной прошивки MODKAM_V3:
* Уменьшено максимальное количество устройств подключаемых к координатору напрямую со 100 до 80: `NWK_MAX_DEVICE_LIST=80`;
* Изменено значение версии прошивки (параметр `CODE_REVISION_NUMBER`) на 20200427.

## Прошивка MODKAMRU_V3 версия от 20200327

[Оригинальные прошивки и патч для стика MODKAM_V3](https://github.com/reverieline/CC2538-CC2592-ZNP)

### Отличия MODKAM V3 от оригинальной версии TI ZNP (Z-Stack 3.0.2)

* Добавлено 4 светодиода для индикации режима работы;
* Увеличена область NV_RAM c 6 до 12 страниц;
* Добавлена поддержка frontend чипа CC2592;
* Сигнал UART RTS переназначен с вывода PD3 на PD1;
* В версии протокола связи ZNP (MT_VERSION) изменено значение Product ID с 0 на 2;
* Изменено значение версии прошивки (параметр `CODE_REVISION_NUMBER`) на 20200327;
* Добавлена возможность получать сообщения с Group ID отсутствующем в таблице координатора;
* Сообщения для 10 и 11 конечных точек перенаправляются на конечную точку 1;
* Отключено старение детей;
* Размер таблицы Broadcast изменен с 9 на 12 (параметр `MAX_BCAST=12`);
* Размер UART буферов RX и TX увеличен с 170 байт до 1024 байт;
* Добавлена обработка событий `HAL_UART_RX_FULL`, `HAL_UART_RX_ABOUT_FULL`, `HAL_UART_RX_TIMEOUT`;
* Выходная мощность передатчика изменена с 19 на 22 dBm;
* Изменен(добавлен) ряд параметров:
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
