# 1. Ведение

**Cisco Packet Tracer (далее — CPT)** - симулятор сети передачи данных, разработанный компанией Cisco как раз для учебного пользования

# 2. Коммутатор. Основы Cisco IOS

- [[Хаб]]
- [[Коммутатор (switch)]]

## Основы Cisco IOS

### Способы подключения:

- [[консольный кабель]];
- Telnet/[[SSH]];
- [[Web]];
- специализированное ПО (SDM — Security Device Manager, CSM — Cisco Security Manager, IME — IPS Manager Express).

### Алгоритм действий для первоначальной настройки:

1. Подключитесь через консольный кабель.
2. Задайте пароль для привилегированного режима.
3. Создайте пользователя.
4. Установите авторизацию на подключение к консоли.
5. Задайте IP-адрес устройства.
6. Разрешите подключение по SSH/Telnet.
7. Включите авторизацию при удалённом подключении.

## Уровни привилегий

### Level 0

Доступны следующие комманды:

- logout
- enable
- disable
- help
- exit

### Level 1

Позволяет перейти в User Exec mode, лимитированный досутп только на чтение

### Levels 2-14

Настраиваемые уровни доступа

### Level 15

Privileged Exec mode, полный доступ

## Полезные комманды

### Прерывание текущей операции

```
Ctrl Shift 6
```

### enable

Вход в привилегированный режим

### enable [0-15]

Вход с указанным уровнем привелегий

### show running-config

Просмотр текущей конфигурации

### line console [0-15]

Настройка консольной линии

### configure terminal

Вход в режим конфигурации терминала

#### write mem

Сохранение конфигурации

#### enable secret [password]

Созданиие зашифрованного пароля

#### service password-encryption

Включение шифрования паролей

#### username [Username] privilege [n:0-15] password [password]

Создания пользователя ```Username``` с максимальным уровнем привилегий ```n``` и паролем ```password```

#### line vty [0-14] или line vty [n] [m]

Конфигурирование терминальных линий (виртуальной консоли)

n - номер линии от
m - номер линии до

##### transport input [none|all|telnet|ssh]

включение\отключение ```telent``` и ```ssh```

##### end

Выход из режима конфигурации терминальных линий

# 3. [[VLAN]]

## Типы портов:

- Access Port — для конечных устройств;
- Trunk Port — транзитный (между коммутаторами).

## Защита порта

### switchport port-security

- aging — задаётся временной интервал, после которого динамический MАС-адрес может быть переписан;
- mac-address — при помощи этой ветки можно:
    - задать разрешённый MAC-адрес;
    - задать запрещённый MAC-адрес;
    - включить порт в режиме обучения;
- maximum — указывает лимит разрешённых адресов.
- violation — задаёт действие из перечисленных ранее.

После настройки применить изменения с помощью комманды ```switchport port-security``` без параметров

## Полезные комманды

### vlan [n]

Создать VLAN под номером ```n```

#### name [name]

Присвоть VLAN имя ```name```

### interface [type] [number]

Перейти в режим конфигурации интерфейся типа ```tye``` под номером ```number```

Например: ```interface fastEthernet 0/1```

#### switchport mode [access|trunc|dynamic]

Установить режим работы интерфейса:

- ```access``` режим безусловного доступа
- ```trunc``` режим безусловного транка
- ```dynamic``` атоматически определять режим

#### switchport access vlan [n]

Установить доступ на порте для VLAN под номером ```n```

#### switchport trunk allowed vlan [n,m...]

Установить транк с доступом для VLAN с номерами ```n,m...```

# 4. Методы организации отказоустойчивых каналов связи. Spanning Tree Protocol (STP)

## Методы

- [[Резервирование каналов]]
- [[Агрегирование каналов связи]]

## [[Резервирование каналов]]

Используется специальный протокол [[STP]]
#### Алгоритм работы

1. Выбираем корневой коммутатор. Порты корневого коммутатора становятся назначенными и переходят в состояние передачи.
1. Выбираем корневой порт на некорневом коммутаторе; он выбирается из расчёта стоимости пути от некорневого коммутатора к корневому (по количеству прыжков и скорости канала связи).
![[Pasted image 20241007112549.png]]
3. Самым последним выбираем назначенный порт — это порт, который висит в режиме ожидания.

**Если «стоимость» канала на всех линиях связи одинаковая — система выбирает корневые коммутаторы и порты по наименьшему MAC-адресу устройств.**

#### Состояния портов:

- блокировка;
- прослушивание;
- обучение;
- передача.

*Протокол STP включён на всём оборудовании Cisco по умолчанию. Если смоделировать вышеуказанный пример, то настройка произойдёт автоматически.*

### Определение корневого коммутатора

1. ```enable```
1. ```show spanning-tree```

Елси вы на корневом коммутадоре то увидите строку ```This bridge is the root```

## [[Агрегирование каналов связи]]

### Статическое агрегирование каналов
![[Pasted image 20241007112604.png]]
1. Перед соединением коммутаторов настроить порты учавствующие в аггрегации
    1. Войти в конфигурационный терминал<br>```conf terminal```
    1. Конфигурация портов (используется range для индентичной настройки сразу двух и более портов)<br>
    ```interface range GigabitEthernet 0/1-2```
    1. Задаем группу логических каналов<br>```channel-group 1 mode on```<br>
    Если успешно пример вывода:<br>
    > Creating a port-channel interface Port-channel 1
    >
    > %LINK-5-CHANGED: Interface Port-channel 1, changed state to up
    > LINEPROTO-5-UPDOWN: Line protocol on Interface Port-channel 1, changed state to up
1. Седините коммутаторы на портах ```GigabitEthernet 0/1``` и ```GigabitEthernet 0/2``` соответвенно
![[Pasted image 20241007112616.png]]
### Динамическое агрегирование каналов LACP
![[Pasted image 20241007112624.png]]
1. настройка L3 Cisco 3560
    1. ```conf terminal```
    1. Конфигурируем первую пару портов<br>
    ```int range fa0/1-2```<br>
    *скоращенная форма комманд: int - interface, fa - fastEthernet*
        1. Устанавливаем протокол LACP<br>
        ```channel-protocol lacp```
        1. Создаем группу 1 логического порта<br>
        ```channel-group 1 mode active``` 
    1. Повторяем аналогично для второй группы портов ```fa0/3-4``` с группой ```2```
    1. Созраняем ```wr mem```
1. Настраиваем L2 коммутаторы
    1. ```conf t```<br>
    *Тоже самое, что и configure terminal*
    1. Конфигурация потов fastEthernet0/1 и fastEthernet0/2<br>
    ```int range fa0/1-2```
        1. ```channel-protocol lacp```
        1. Создаем логическую группу интерфейсов 1 в пассивном режиме (в активном на L3; рекомендуется с одной стороны в активном, с другой в пассивном)<br>
        ```channel-group 1 mode passive```
    1. ```wr mem```
    1. Повторяем то же самое на 2м L2
![[Pasted image 20241007112634.png]]
#### Статус EtherChannel

```show etherchannel```

```show etherchannel summary```

# 5. [[L3-коммутаторы]]


## Комманды

### ip routing

включение пересылки пакетов между сегментами сети.


### switchport trunk encapsulation dot1q

инкапсуляция протокола VLAN.

# 6. [[Маршрутизаторы]]

### interface fa0/0.2

создание подинтерфейса для VLAN.

# 7. [[Статическая маршрутизация]]

# 8. [[DHCP]]


## Комманды

### ip dhcp pool [name]

Создает DHCP пул для адресов под именем ```name```

#### network [net] [mask]

Создает сеть ```net``` для DHCP с количество адресов определнным ```mask```

#### default-router [ip]

Задает шлюз по умолчанию на адресе ```ip```

#### dns-server [ip]

Задает DNS сервер ```ip```

### ip dhcp excluded-address [ip]

Исключает ```ip``` из пула DHCP адресов

### interface [name]

#### ip helper-address [ip]

Устанавливает ```ip``` вспомогательного сервера (например DHCP)

#### ip dhcp snooping trust

устанавливает интерфейс как доверенный для DHCP пакетов

#### ip dhcp snooping limit rate 10

устанавливает частота получаемых клиентских запросов DHCP

### ip dhcp snooping vlan [id]

Устанавливает dhcp snooping на vlan ```id```

# 7. [[NAT]]

## Комманды

### int [interface]

#### ip nat outside

устанавливает на интерфейсе nat наружу

#### ip nat inside

устанавляивает на интерфейсе nat внутрь

### ip access-list [standard|extended] [name]

Добавляет access list под именем ```name```

#### permit [ip] [wildcard-mask]

Разрешающее правило для ip адреса или сети ```ip``` с ```wildcard-mask```

### ip nat inside source list [list name] interface [int] overload

добавляет перегруженный нат на интерфейс ```int``` для access-list ```list name```

# 8. [[Динамическая маршрутизация OSPF]]

### Настройки

На роутере применяются следующие настройки:

#### 1. interface loopback 0

Настройка ip на loopback интерфейсе

##### 1.1. ip address [ip] [mask]

Задаем ip адрес. Должна быть наибольшая подсеть!

##### 1.2. no shutdown

Не выключать

#### 2. router ospf 1

Настройка ospf

##### 2.2. network [net] [wildcard-mask] area [n]

Включение ospf для сети ```net``` поределяемый маской ```wildcard-mask``` в зоне под номером ```n```

Повторить для каждой сеседней сети

Пример: ```network 10.90.89.0 0.0.0.255 area 0```

#### show ip ospf neighbors

Показывает список "соседей" по ospf

# 9. [[EIGRP|Динамическая маршрутизация EIGRP]]

## Настройка

На роутере
### 1. interface loopback 0

Настройка ip на loopback интерфейсе

#### 1.1. ip address [ip] [mask]

Задаем ip адрес. Должна быть наибольшая подсеть!

#### 1.2. no shutdown

Не выключать

### 2. Настраиваем интерфейсы и сетя на роутере

#### 2.1. interface [int]

Настройка интерфейса ```int```

##### 2.1.1. ip address [ip] [mask]

Ставим ip

##### 2.1.2. duplex auto

##### 2.1.3. speed auto

### 3. route eigrp 1

Найстраиваем eigrp

#### 3.1. network [net] [wildcard-mask]

Добавляем сеть для автомаршрутизации

### 4. no auto-summary

Отключаем суммирование маршрутов, это зачастую помогает с решением проблем

# 10. [[Списки доступа Access List]]

### Комманды

#### show ip access-lists

Выводит список имеющихся списков доступа

#### ip access-list [type] [name]

Создать или настроить access-list типа ```type``` под именем ```name```

```type```:
- ```extended```
- ```standard```

##### no [n]

Удаляет правило под номером ```n```. Номер из списка с комманды ```show ip access-lists```

##### permit [ip] [mask]

Разрешить сеть\ip ```ip``` с маской ```mask```. Испольщуется wildcard mask.

##### deny [ip] [mask]

Запретить сеть\ip ```ip``` с масской ```mask```. Испольщуется wildcard mask.

#### deny ip any [ip_to] [mask]

Запретить с любого ip доступ на ```ip_to``` ```mask```

# 11. [[Межсетевой экран Cisco ASA]]
## Настройка

### Настройка интерфейса

#### int [interface]

Режим настройки интерфейса

##### nameif [name]

Задает имя ```name``` порту

##### security-level [0-100]

Задает security lvl

##### ip address [ip] [mask]

### route [int_name] 0.0.0.0 0.0.0.0 [ip]

Задаем маршрут по усолчанию на интерфейс ```int_name```

### Включение инспекции трафика

#### class-map inspection_default

Редактирование политики инспекции

##### match default-inspection-traffic

Инспектировать весь трафик

#### policy-map globalpolicy

Создаем новую политику

##### class inspection_default

Применяем политику к выбранному трафику

##### inspect [proto]

Указываем протокол ```proto``` для инспектирования (например ```icmp```, ```http``` и т.д.)

#### service-policy globalpolicy global

Определяем направление работы политики

## Настройка NAT

### object network [name]

Создаем объект безопасности сети ```name```

#### subnet [net] [mask]

Добавляем сеть

#### nat [name] dynamic interface

Задаем направление

# 12. Демилитаризованная зона [[DMZ]]

# 13. Виртуальные частные сети [[VPN]]


# 14. [[Логирование Syslog и NTP-серверы]]


## Настройка

- Для работы потребуется сервер времени — NTP (Network Time Protocol)
- Для сбора логов в сети нам потребуется сервер c включенным Syslog

### logging on

Включаем логирование

### logging console [0-7]

Устанавливает уровень логгирования

### logging buffered [n]

Задаём размер буфера ```n```

### logging monitor [0-7]

Уровень логирование при telnet и ssh

### logging trap [0-7]

Настроить уровень логирования в system log

### logging [ip]

Задаем ```ip``` сервера логгирования
### service timestamps log datetime msec

Задаем формат времени для логов в миллисекундах

### ntp server [ip]

Указываем NTP сервер

# 15. Сервер учетных записей [[AAA сервер|ААА]]

## Настройки

### enable secret cisco

### username admin privilege 15 secret cisco

### aaa new-model

Создаём модель взаимодействия

### aaa authentication login default group radius local

Авторизация через ААА-сервер осуществляется по умолчанию через протокол RADIUS, если сервер не доступен, используйте локальную базу

### radius-server host [ip] key [key]

Задаем наш радиус-сервер на маршрутизаторе

# 16. Удалённая загрузка файлов [[TFTP]]

## Виды конфигурации Cisco

- running config — текущая конфигурация устройства;
- startup config — загрузочная конфигурация устройства.

## Использование

### copy tftp: flash

Скачиваем файл с сервера

#### Address or name of remote host []? [ip]

Указываем адрес сервера

#### Source filename []? [name.bin]

Указываем имя скачиваемого файла

#### Destination filename [name.bin]?

казываем имя сохраняемого файла

### boot system flash:/[name.bin]

Указываем, какой файл прошивки использовать

### reload

Перезагружаем для применения изменений