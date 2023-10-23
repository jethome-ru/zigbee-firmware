# Прошивки для трехканального модуля дискретных входов WS7

Описание устройства: [Трехканальный Zigbee Модуль дискретных входов JetHome WS7](https://docs.jethome.ru/ru/zigbee/switches/ws7.html)

## Структура репозитария

  * client - директория с прошивками, поставляемых с устройством;
  * ota - прошивки, подготовленные для обновления устройства с помощью механизма OTA.

## Версии прошивок
  
  * ws7_20210922_f123_f001_00000008 - базовая прошивка
  * ws7_20220630_f123_f001_00000009 - добавлен прямой биндинг устройства (кластер on/off), добавлена поддержка групп
  * ws7_20230627_f123_f001_0000000a - отключен "Insecure Rejoin" (решение проблемы с самопроизвольным выходом из сети). Снижено энергопотребление.   
  * ws7_20230627_f123_f001_0000000b - решена проблема при возникновении которой устройство переставало функционировать. Оставалась реакции (вспышка светодиода) только на однократное нажатие кнопки. 
  
## Инструкция по обновлению устройства с помощью механизма OTA

Устройства JetHome WS7 поддерживают механизм обновления OTA, однако в текущей стабильной версии Zigbee2MQTT данный механизм не включен для устройств JetHome WS7. Ниже приводится инструкция по обновлению устройства JetHome WS7 с спользованием механизма OTA. Механизм проверен на следующей конфигурации:

Zigbee2MQTT version: 1.32.1  
Coordinator type: zStack3x0  
Coordinator revision: 20220524  
Frontend version: 0.6.129

1. В директории, в которую установлен Zigbee2MQTT, отредактируйте файл `zigbee2mqtt/node_modules/zigbee-herdsman-converters/devices/jethome.js` (https://github.com/Koenkk/zigbee-herdsman-converters/blob/master/devices/jethome.js). В данный файл необходимо добавить две строки:

- Подключить библиотеку *OTA*, для чего добавить строку: `const ota = require('../lib/ota');`
```
...
const exposes = require('../lib/exposes');
const fz = require('../converters/fromZigbee');
const reporting = require('../lib/reporting');
const utils = require('../lib/utils');
const e = exposes.presets;
const ota = require('../lib/ota');
...
```

- В описании устройства WS7 включить поддержку механизма Zigbee OTA для данного устройства, для чего добавить строку: `ota: ota.zigbeeOTA,`
```
...
module.exports = [
    {
        fingerprint: [{modelID: 'WS7', manufacturerName: 'JetHome'}],
        model: 'WS7',
        vendor: 'JetHome',
        description: '3-ch battery discrete input module',
        ota: ota.zigbeeOTA,
...
```

2. Перезапустите службу zigbee2mqtt.

3. Откройте WEB-интерфейс (frontend) Zigbee2MQTT и перейдите в раздел: `Settings/OTA updates` 
  В поле `OTA index override file name` укажите ссылку на новый файл с описанием OTA прошивок для устройств JetHome: `https://github.com/jethome-ru/zigbee-firmware/raw/master/ti/ws7/jethome_ota_index.json`  
  Нажмите кнопку ***'Submit'***.

4. Перейдите в раздел `OTA`. Нажмите кнопку ***'Check for new update'*** напротив устройства JetHome WS7. На обновляемом устройстве Jethome WS7 нажмите кнопку переключения режимов (кнопка на корпусе устройства). Подождите появления кнопки ***'Update device firmware'*** в WEB-интерфейсе Zigbee2MQTT. Нажмите на нее. 

5. Так как устройство JetHome WS7 питатся от батарейки и большую часть времени находится в спящем режиме, то на нем необходимо с периодом ~2 сек нажать 3-4 раза на кнопку переключения режимов, чтобы вывести устройство из спящего режима. Начнется процесс обновления. Время обновления может достигать до 60 минут. 

Если производилось обновление прошивки устройства с версии ws7_20220630_f123_f001_00000008 или более ранней, то устройство необходимо заново переподключить к координатору, так как в новых прошивках были добавлены дополнительные кластеры для обеспечения работы прямого биндинга устройства.

Настройка биндинга устройства может быть произведена в Web-интерфейсе (frontend) Zigbee2MQTT. Документация по настройке биндинга на сайте Zigbee2MQTT: https://www.zigbee2mqtt.io/guide/usage/binding.html
