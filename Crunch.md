**Crunch** — инструмент для генерации словарей паролей, также позволяет создавать кастомные словари с различными параметрами, такими как длина пароля, используемые символы, шаблоны и многое другое.

![[Pasted image 20241004201432.png]]

# Базовый синтаксис

crunch <min> <max> [<charset>] [-o <output_file>] 

<min>: Минимальная длина пароля.
<max>: Максимальная длина пароля.
<charset>: Набор символов (необязательно). - -o
<output_file>: Файл для сохранения словаря.

# Возможности
1. Генерация словарей с заданной длиной паролей: Установка минимальной и максимальной длины паролей.
2. Настройка используемых символов: Определение набора символов для генерации паролей.
3. Поддержка шаблонов: Создание словарей на основе шаблонов, включающих фиксированные части и переменные символы. 
4. Вывод в файл или стандартный вывод: Возможность сохранения словарей в файл или вывода непосредственно на экран.