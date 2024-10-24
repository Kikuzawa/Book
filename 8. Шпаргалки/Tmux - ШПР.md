## Запуск новой сессии:

```
tmux new -s имя_сессии
```

## Подключение к существующей сессии:

```
tmux attach -t имя_сессии
```

## Просмотр списка сессий:

```
tmux ls
```

## Завершение сессии:

```
tmux kill-session -t имя_сессии
```

## Отключение от сессии (сессия продолжит работу):

```
Ctrl + b, d
```

## Переименование текущей сессии:

```
Ctrl + b, $
```

## Создание нового окна:

```
Ctrl + b, c
```

## Переключение между окнами:

```
Ctrl + b, n (следующее окно) 
Ctrl + b, p (предыдущее окно) 
Ctrl + b, 0-9 (номер окна)
```

## Закрытие окна:

```
Ctrl + b, &
```

## Разделение окна по горизонтали:

```
Ctrl + b, "
```

## Разделение окна по вертикали:

```
Ctrl + b, %
```

## Переключение между панелями:

```
Ctrl + b, o (переключение на следующую панель)
```

## Закрытие панели:

```
Ctrl + b, x
```

## Перемещение панели:

```
Ctrl + b, { (влево) 
Ctrl + b, } (вправо)
```

## Увеличение панели:

```
Ctrl + b, z (развернуть/свернуть текущую панель)
```

## Синхронизация всех панелей (ввод одинаковых команд в несколько панелей):

```
Ctrl + b, :setw synchronize-panes on
```

## Отключение синхронизации панелей:

```
Ctrl + b, :setw synchronize-panes off
```

## Прокрутка вверх по истории в текущей панели:

```
Ctrl + b, [
```

## Поиск текста в панели:

```
Ctrl + b, / (введите текст для поиска)
```

## Перезагрузка конфигурации tmux (после изменения `.tmux.conf`):

```
Ctrl + b, :source-file ~/.tmux.conf
```

## Отправка команды на выполнение в конкретной сессии:

```
tmux send-keys -t имя_сессии 'команда' C-m
```