## OSPF - протокол состояния канала

- работает поверх протокола IP
- для IPv6 разработывается 3я версия протокола
## <span style="color:green">Плюсы</span>

- автоматическое добавление маршрутов,
- организация отказоустойчивости на 3 уровне [[Модель OSI|модели OSI]].

## <span style="color:red">Минусы</span>

- загрузка вычислительных ресурсов (необходимо более дорогостоящее оборудование),
- менее предсказуемая сеть в диагностике,
- необходима более высокая квалификация инженеров

## Основные группы

1. Внешние — такие протоколы как [[EGP]] и [[BGP]].
1. Внутренние протоколы делятся на две категории:
    - дистанционно векторные протоколы [[RIP]], [[IGRP]], [[EIGRP]];
    - протоколы состояния каналов OSPF, [[IS-IS]]

[[AS]]




### Условия построения OSPFv2

- Должны быть настроены одинаковые Hello interval на тех роутерах, которые подключены друг к другу. Каждые 10 секунд оборудование говорит «соседям»: «Я жив».
- Одинаковыми должны быть Dead interval. Обычно это четыре интервала Hello, т.е. 40 секунд.
- Интерфейсы маршрутизаторов должны быть в одной подсети.
- OSPF позволяет снизить нагрузку на процессор, разделив AS на зоны.
- У каждого роутера есть свой уникальный ID. Обычно прибегают к хитрости — настройке наивысшего IP на интерфейсе loopback.
- Должны совпадать размеры MTU.