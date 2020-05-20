Прошивка для стика modkam c кнопкой **FLASH**.

## Индикация 

Для индикации используется светодиод **LED1** (синий).
* Мигание с частотой 1 Гц, длительность свечения 500 мс - режим поиска доступной сети;
* Постоянное свечение - устройство в сети;
* Светодиод погас на 1 сек. - подтверждение нажатия на кнопку **FLASH**;
* Мигание с частотой 1 Гц, длительность свечения 100 мс - режим **Identify**;


## Управление

* Включение питания запускает процесс поиска/присоеденения к сети;
* Удержание кнопки **FLASH** более 5 секунд приводит к сбросу устройства на заводские установки;
* Короткое нажатие на кнопку **FLASH** приводит к отправке **ReportAttr** (кластер 0x0 Basic, атрибут 0x5 modelID);

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
        String: cc2538.router.v1
   
        Attribute: Date Code (0x0006)
        Data Type: Character String (0x42)
        String: 20200520

    Input Cluster: Identify (0x0003)
Output Cluster Count: 1
Output Cluster List
    Output Cluster: Basic (0x0000)
```