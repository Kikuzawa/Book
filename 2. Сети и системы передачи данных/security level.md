**Security Level** - это число, принимаемое значение от 0 до 100. Соответственно чем выше уровень безопасности, присвоенный ему значение уровня из диапазона от 0 до 100, тем более доверительно относится к интерфейсу устройство и наоборот, чем меньше уровень безопасности, тем меньше доверят интерфейсу устройство.

#### Контролирует следующее поведение:

- Доступ к сетям - существуют не явные разрешения к хостам, подключенным к интерфейсу с более низким уровнем безопасности, с хостов подключенных к интерфейсу с более высоким уровнем безопасности (Исходящий трафик). Cisco ASA запомнит хосты инициализирующие сессию и разрешит хождение трафика в пределах этой сессии в обоих направлениях, если с помощью списков доступа (access list) не определены запреты.
- Внутреннее взаимодействие - так же не явным образом запрещено взаимодействовать с хостами подключенными к интерфейсам с одинаковым уровнем безопасности в обоих направлениях, в случае если с помощью списков доступа (access list) не определены запреты. Источник: Allowing Communication Between VLAN Interfaces on the Same Security Level (англ.)
- Инспектирование трафика - некоторые инструменты ряда приложений зависят от уровня безопасности. Для некоторых интерфейсов проводиться проверка трафика в обоих направлениях.
- Проверка NetBIOS имен - производиться только для исходящих соединений.
- Фильтрация - по умолчанию HTTP(S) и FTP фильтрация применяется только на исходящие соединения.
- NAT контроль - при использовании контроля NAT трафика, необходимо конфигурировать NAT для внутренних хостов, при получении доступа к внешним хостам.

# [[Примеры получения доступа хостами подключенными к интерфейсам с разными уровнями безопасности]]

