# BLETHR
Receiving and displaying data from an external thermometer operating in the [BTHome v2](https://bthome.io/) format on the display of another BLE thermometer.

![foto_zy-zth02pro.jpg](https://raw.githubusercontent.com/pvvx/pvvx.github.io/refs/heads/master/blethr/img/zy-zth02pro.jpg)

Получение и отображение данных с внешнего термометра работающего в формате [BTHome v2](https://bthome.io/) на экране другого BLE термометра.

Программа настройки **BLETHR**: [blethr.html](https://pvvx.github.io/blethr/blethr.html).

#### Поддерживаемые модели для **BLETHR**:
* LYWSD03MMC
* [LKTMZL02(TS0201_TZ3210_ncw88jfq)](https://pvvx.github.io/LKTMZL02/)
* [ZY-ZTH02Pro(TS0201_TZ3000_v1w2k9dd)](https://pvvx.github.io/ZY-ZTH02Pro)

#### Поддерживаемые **термометры-датчики** - все передающие температуру и влажность в формате BTHome v2:
* [ATC_MiThermometer](https://github.com/pvvx/ATC_MiThermometer)
* [THB2](https://github.com/pvvx/THB2)
* [BZdevice](https://github.com/pvvx/BZdevice)

 
## Описание

Исходники пока не публикуются. Для этого требуется произвести наработку коэффициентов и алгоритмов синхронизации связи... Так же, возможно, что для дальнейшего уменьшения потребления от батареи будет необходимо встроить дополнительную опцию в прошивки датчиков...

![img](https://raw.githubusercontent.com/pvvx/pvvx.github.io/refs/heads/master/blethr/img/blethr.jpg)

Устройство с прошивкой **BLETHR** принимает маяк от **термометра-датчика** и отображает на экране.
Основное предназначение – приклеить LYWSD03MMC на дверь или где в холле, или на окне, а датчик расположить на улице. За счет дублирования данных внешнего датчика происходи увеличение дистанции приема до BT адаптера сервера HA находящегося в помещении.

**BLETHR** дублирует принятые данные о температуре, влажности и уровню батареи (в процентах) полученные от **термометра-датчика**. Состояние своей батареи передается в виде напряжения в милливольтах. Дополнительно передается счетчик сбоев связи, служащий для оценки качества связи между устройствами.

![img](https://raw.githubusercontent.com/pvvx/pvvx.github.io/refs/heads/master/blethr/img/ha_bthome.jpg)

## Прошивка

Прошить программу в поддерживаемый BLE термометр с экраном возможно с помощью [TelinkMiFlasher.html](https://pvvx.github.io/ATC_MiThermometer/TelinkMiFlasher.html).

* [Файл прошивки **BLETHR** для LYWSD03MMC](https://github.com/pvvx/BLETHR/raw/refs/heads/master/ATC_bthr_v11.bin)
* [Файл прошивки **BLETHR** для LKTMZL02](https://github.com/pvvx/BLETHR/raw/refs/heads/master/LKTMZL02_bthr_v11.bin)
* [Файл прошивки **BLETHR** для ZY-ZTH02Pro](https://github.com/pvvx/BLETHR/raw/refs/heads/master/ZYZTH02P_bthr_v11.bin)

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

Поиск и синхронизация потребляет довольно много энергии от батареи.
По этой причине введено ограничение попыток поиска и синхронизации до 255.
Если за такое количество попыток не удалось получить сигнал от **термометра-датчика** то это означает что связи практически нет и **BLETHR** прекратит бесполезную трату батарейки.
Активировать новый старт возможно двумя вариантами – передергивания батарейки или путем BLE соединения. 

При нескольких подряд сбоях связи возникает новый отсчет попыток поиска и синхронизации. 
Если это происходит часто – это говорит о плохой связи с **термометром-датчиком**.
При нормальной связи, малом уровне помех и интервале приема маяка в 5 секунд среднее потребление от батареи CR2032 находится в пределах 20 мкА.

При работе **BLETHR** передает счетчик потерь связи и поиска.
По нему можно судить о качестве связи между двумя устройствами.
Прыжки счета на много единиц говорят о потере связи и возобновлению поиска. Это особенно критично для долгой жизни батарейки.

![foto_blethr.jpg](https://raw.githubusercontent.com/pvvx/pvvx.github.io/refs/heads/master/blethr/img/foto_blethr.jpg)

