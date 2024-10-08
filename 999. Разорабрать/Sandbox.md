Sandbox (Песочница) — это среда безопасного тестирования. Решение изолирует непроверенные изменения в коде и эксперименты от производственной среды и хранилища в контексте разработки программного обеспечения. Включая веб-разработку и контроль версий.

Песочница обнаруживает угрозы в файлах, передаваемых по сети (почтовые сообщения, загрузка файлов из Интернет и т. д.) с помощью продвинутых технологий поведенческого анализа. Система помогает обнаруживать и предотвращать APT-угрозы до их проникновения на конкретный хост. Далее мы разберем как работает система, как запускать «sandboxie», что позволяет делать песочница и какое решение выбрать.

![[Pasted image 20241006114544.png]]

# Что можно сделать в среде песочницы?

1. Запустить код и оценивать его на основе деятельности, а не атрибутов.
2. Запустить исполняемые файлы и другие скрытые вредоносные программы. 
3. Разрешить и наблюдать за сетевым трафиком.
4. Безопасно выполнять вредоносный код или операции с диском. 
5. Безопасно изменять реестры / систему / конфигурацию и т. п.

# Как работает Sandbox?

- Эмуляция реального устройства Песочница имитирует физическое оборудование, обеспечивая глубокое представление о поведении и воздействии программы. Приложение для теста имеет доступ к тем же ресурсам, что и анализируемый код, включая ЦП, память и хранилище
- Эмуляция операционных систем Имитация операционной системы (ОС) конечного пользователя, но не аппаратного обеспечения машины. В случае виртуальной машины песочница изолирована от базового физического оборудования, но имеет доступ к установленной ОС
- Виртуализация сред Использование изолированной программной среды на основе виртуальной машины для хранения и проверки подозрительных программ. Не имеет доступа к физическим ресурсам, но может получить доступ к виртуализированному оборудованию.

# Три модели интеграции SandBox в инфраструктуру компании

- Самостоятельно. Купить готовый продукт и своими силами интегрировать его в сетевую инфраструктуру. Такой подход актуален для крупных IT-ориентированных компаний, у которых есть достаточное количество специалистов соответствующей компетенции.
- Опосредованно. От предыдущей модели этот вариант отличается тем, что интеграцией и настройкой занимаются внешние специалисты, представители поставщика ПО или другая компетентная компания. Такой метод, с позиции бизнеса, проще, но не решает вопрос того, кто будет работать с песочницей «на местах».
- Делегировано. То есть по SaaS-модели, где компания оплачивает подписку, а все операции с SandBox удаленно выполняет поставщик. Такой подход позволяет оптимизировать расходы (нет необходимости «разово» платить большую сумму за приобретение самой программы песочницы) и снижает нагрузку на штат ИБ компании.

![[Pasted image 20241006114654.png]]
![[Pasted image 20241006114725.png]]

# Как включить и использовать песочницу [[Windows Sandbox]] в [[Windows]] 10

1. Проверьте требования: Ваша версия должна быть Windows 10 Pro, Enterprise или Education. К сожалению, эта функция недоступна в домашних версиях Windows 10.
2. Включите песочницу Windows Sandbox: Шаг 1: В "Панели управления" выберите "Программы и компоненты" и затем "Включение или отключение компонентов Windows". Шаг 3: Прокрутите вниз и найдите "Песочница Windows", убедитесь, что он отмечен, и нажмите "OK". Это может потребовать перезагрузки системы
![[Pasted image 20241006114811.png]]

![[Pasted image 20241006114835.png]]

3. Запустите Windows Sandbox: Шаг 1: Нажмите левой кнопкой мыши на кнопке "Поиск". Шаг 2: Введите "Windows Sandbox" и запустите приложение. Шаг 3: В открывшемся окне Windows Sandbox вам будет предложено подождать несколько мгновений, пока будет создана изолированная среда. После завершения этого процесса вы увидите окно, похожее на обычную копию Windows.
![[Pasted image 20241006114850.png]]
![[Pasted image 20241006114903.png]]