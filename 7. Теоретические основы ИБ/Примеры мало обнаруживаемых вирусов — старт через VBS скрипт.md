- VBS скрипт (в макросе файла, в IExplorer) запускает легитимный инструмент удаленного доступа RMS (Remote Manipulator System).
- Загрузка трояна NanoCore (адрес расположения: \LANSubsystem\lanss.exe).
- Загрузка Empire агентов, полностью работающих в оперативной памяти и не обнаруживаемых антивирусным ПО и СОВ на скриптовом языке.
- Далее имеется несколько Empire агентов, которые запускает нарушитель:
- Кейлоггеры — получение пароля с клавиатуры.
- Mimikatz — получение паролей из памяти компьютера.
- Antivirusproduct — получение список антивирусов на компьютере.
- Sherlock — проверка CVE-уязвимостей.
- Bloodhound3 (путь к файлу) — передача файлов с атакуемой машины себе.