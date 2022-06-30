# WS7
Zigbee2MQTT version: 1.25.2  
Coordinator type: zStack3x0  
Coordinator revision: 20220524  
Frontend version: 0.6.103  

1. Отредактировать файл `/zigbee2mqtt/node_modules/zigbee-herdsman-converters/devices/jethome.js` (https://github.com/Koenkk/zigbee-herdsman-converters/blob/master/devices/jethome.js)

    * В строку 6 добавить: `const ota = require('../lib/ota');`
    * В строку 30 добавить: `ota: ota.zigbeeOTA,`

2. Перезапустить zigbee2mqtt

3. Открыть WEB-интерфейс zigbee2mqtt. Перейти в раздел: `Settings/OTA updates/` 
  В поле `OTA index override file name` указать: `https://github.com/jethome-ru/zigbee-firmware/raw/master/ti/ws7/jethome_ota_index.json`  
  Нажать ***'Submit'***.

4. Перейти в раздел `OTA`. Нажать кнопку ***'Check for new update'*** напротив WS7. На WS7 нажать кнопку переключения режимов. Подождать появления кнопки ***'Update device firmware'***. Нажать на нее. 

5. На WS7 с периодом ~2 сек нажать 3-4 раза на кнопку переключения режимов. Начнется процесс обновления. Время обновления около 80 минут. 
