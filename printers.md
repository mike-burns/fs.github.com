---
layout: default
---

Настройка принтеров
===================

HP M1120
--------

### Настройка в MacOSX

System preferences → Print & Fax → \[+\] → Add Other Printer or Scanner → IP

В строчке Protocol выбираем HP Jetdirect.

Вбиваем 10.0.0.201 в строчку Address, выбираем драйвер HP LaserJet M1120 (foomatic/foo2xqx) в строчке Print Using → Select Printer Software.

Если драйвера в системе еще нет -- скачиваем и устанавливаем с [http://dashboard.toa/printers/](http://dashboard.toa/printers/) (это нужно сделать один раз).

Говорят, что нормально работает и стандартный драйвер generic postscript, но с ним могут возникнуть проблемы с форматированием.

### Настройка в Linux

Пуск → Система → Администрирование → Печать → Добавить → Сетевой принтер → AppSocket/HP JetDirect.

Адрес 10.0.0.201, порт оставляем 9100, драйвер HP LaserJet M1120 (foomatic/foo2xqx)

### Настройка в Windows

Добавляем сетевой принтер, адрес 10.0.0.201 протокол LPR.

*ВАЖНО*: обязательно нужно в настройках порта поставить галку "Подсчет байтов" -- без этого принтер работать не будет.


Xerox 3119
----------

### Настройка в MacOSX
System preferences → Print & Fax → \[+\] → Add Other Printer or Scanner → IP

В строчке Protocol выбираем HP Jetdirect.

Вбиваем 10.0.0.200 в строчку Address, выбираем драйвер Xerox WorkCentre 3119 в строчке Print Using → Select Printer Software.

Если драйвера в системе еще нет -- скачиваем и устанавливаем c [http://dashboard.toa/printers/](http://dashboard.toa/printers/) (это нужно сделать один раз).

Говорят, что нормально работает и стандартный драйвер generic postscript, но с ним могут возникнуть проблемы с форматированием.

### Настройка в Linux

Пуск → Система → Администрирование → Печать → Добавить → Сетевой принтер → AppSocket/HP JetDirect.

Адрес 10.0.0.200, порт оставляем 9100, драйвер Xerox WorkCentre 3119
