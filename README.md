# BLETHR
Receiving and displaying data from an external thermometer [BTHome](https://bthome.io/) on Xiaomi LYWSD03MMC.

Получение и отображение данных с внешнего термометра работающего в формате [BTHome](https://bthome.io/) на экране Xiaomi LYWSD03MMC.

![img](https://raw.githubusercontent.com/pvvx/pvvx.github.io/refs/heads/master/blethr/img/blethr.jpg)

LYWSD03MMC с прошивкой **BLETHR** принимает маяк от **термометра-датчика** и отображает на экране.

## Прошивка

Прошить программу в Xiaomi LYWSD03MMC возможно с помощью [TelinkMiFlasher.html](https://pvvx.github.io/ATC_MiThermometer/TelinkMiFlasher.html).

[Файл прошивки **BLETHR**](https://github.com/pvvx/BLETHR/raw/refs/heads/master/blethr_v10.bin).

Если в дальнейшем потребуется перепрошивка устройства на другую версию программы, тогда используйте [OTA Flasher](https://pvvx.github.io/ATC_MiThermometer/TelinkOTA.html).

## Настройка

### 1. Настройка **термометра-датчика**:

1. Установить интервал маяка от 5 до 10 секунд.
2. Записать MAC адрес

### 2. Настройка BLETHR:

1. Произвести соединение с **BLETHR** в [blethr.html](https://pvvx.github.io/blethr/blethr.html).
2. Установить и сохранить интервал маяка **термометра-датчика**.
3. Установить и сохранить MAC адрес **термометра-датчика**.
4. Отключиться от устройства.

**BLETHR** начнет отсчет попыток поиска и синхронизации с **термометром-датчиком**.

Поиск и синхронизация потребляет довольно много энергии от батареи. По этой причине введено ограничение попыток поиска и синхронизации до 255. Активировать новый старт возможно двумя вариантами – передергивания батарейки или BLE соединения. 

При сбое связи возникает новый отсчет попыток поиска и синхронизации. 

Если это происходит часто – это говорит о плохой связи с **термометром-датчиком**.

При нормальной связи, малом уровне помех и интервале приема маяка в 5 секунд среднее потребление от батареи CR2032 находится в пределах 20 мкА.

При работе BLETHR передает счетчик потерь связи и поиска. По нему можно судить о качестве связи между двумя устройствами.

**BLETHR** дублирует принятые данные о температуре, влажности и уровню батареи в процентах полученные от **термометра-датчика**. Но передаваемое напряжение в милливольтах – это напряжение батареи BLETHR.

![img](https://raw.githubusercontent.com/pvvx/pvvx.github.io/refs/heads/master/blethr/img/ha_bthome.jpg)

![foto_blethr.jpg](https://raw.githubusercontent.com/pvvx/pvvx.github.io/refs/heads/master/blethr/img/foto_blethr.jpg)
