Устройство имеет 2 выхода (реле) с общим контактом и 2 входа (активный высокий, 220 В).
Каждый вход и выход имеет свою конечную точку. 

| EP | Описание |
| --- | ---- |
| 1 | реле 1. Управление через команды кластера onOff (0x0006) |
| 2 | реле 2. Управление через команды кластера onOff (0x0006) |
| 3 | вход 1. Кластер Multistate Input 0x0012. Значение 0x17 - кнопка нажата, 0x16 - кнопка отпущена |
| 4 | вход 2. Кластер Multistate Input 0x0012. Значение 0x17 - кнопка нажата, 0x16 - кнопка отпущена |

По умолчанию настроены report attributes для кластеров onOff (0x0006) и Multistate Input 0x0012.

### Настройка связи между кнопкой и реле.
Связь настраивается между:
```
    вход 1 - реле 1;
    вход 2 - реле 2;
```
В кластере OnOff (0x0006) (end point 1, 2) реализован дополнительный атрибут.

    ID: 0xF000
    Type: uint16 (0x21)
    Value:
        0 - кнопка и реле не связаны;
        1 - состояние реле повторяет состояние кнопки; (значение по умолчанию)
        2 - реле меняет своё состояние при нажатии на кнопку (по фронту);
        
        
## Состав устройства
Реализовано 4 конечных точки.
```
Active Endpoint List
    Endpoint: 1 - реле 1
    Endpoint: 2 - реле 2
    Endpoint: 3 - вход 1
    Endpoint: 4 - вход 2
```

#### Endpoint: 1
```
Simple Descriptor
    Endpoint: 1
    Profile: Home Automation (0x0104)
    Application Device: Unknown (0x0002)
    Application Version: 0x0001
    Input Cluster Count: 3
        Input Cluster List
            Input Cluster: Basic (0x0000)
                Attribute: ZCL Version (0x0000)
                Uint8: 2 (0x02)
                Attribute: HW Version (0x0003)
                Uint8: 1 (0x01)
                Attribute: Manufacturer Name (0x0004)
                String: JETHOME
                Attribute: Model Identifier (0x0005)
                String: jethome.double_relay.v2
                Attribute: Date Code (0x0006)
                String: May 14 2020 
            Input Cluster: Identify (0x0003)
            Input Cluster: On/Off (0x0006)
    Output Cluster Count: 1
        Output Cluster List
            Output Cluster: OTA Upgrade (0x0019)
```
#### Endpoint: 2
```
Simple Descriptor
    Endpoint: 2
    Profile: Home Automation (0x0104)
    Application Device: Unknown (0x0002)
    Application Version: 0x0001
    Input Cluster Count: 2
        Input Cluster List
            Input Cluster: On/Off (0x0006)
            Input Cluster: Basic (0x0000)
    Output Cluster Count: 0
```
#### Endpoint: 3
```
Simple Descriptor
    Endpoint: 3
    Profile: Home Automation (0x0104)
    Application Device: Unknown (0x0002)
    Application Version: 0x0001
    Input Cluster Count: 2
        Input Cluster List
            Input Cluster: Multistate Input (Basic) (0x0012)
            Input Cluster: Basic (0x0000)
    Output Cluster Count: 0
```
#### Endpoint: 4
```
Simple Descriptor
    Endpoint: 4
    Profile: Home Automation (0x0104)
    Application Device: Unknown (0x0002)
    Application Version: 0x0001
    Input Cluster Count: 2
        Input Cluster List
            Input Cluster: Multistate Input (Basic) (0x0012)
            Input Cluster: Basic (0x0000)
    Output Cluster Count: 0
```