# Распределенная система поиска простых чисел на GCloud

### Описание
Система состоит из трёх машин, на которых запущены сервера.
Взаимодействие пользователя с системой происходит через главный сервер, на который передается верхняя граница искомых чисел..
Главный сервер формирует страницу, с которой пользователь (js) отправляет асинхронные запросы на другие два сервера.
В запросе передаются границы диапазонов, в пределах которых нужно искать простые числа.
Полученные ответы выводятся на страницу.

####Шаги:
- Регистрируемся в *Google Cloud* 
https://console.cloud.google.com
- Создаем проект
- Заходим во вкладку *Compute Engine*
- Создаем три экземпляра: **main**, **i2**, **i3**.
Оставляем настройки по-умолчанию, кроме: 
**Профиль и API-доступ** : *Полный доступ ко всем Cloud API*,
**Брандмауэр** : *Разрешить трафик HTTP*, *Разрешить трафик HTTPS*.

Для каждого экземпляра:
- Открываем в окне браузера, нажав кнопку *SSH* в колонке *Подключиться*.
- Заходим с правами суперюзера:
```
sudo su
```
- Устанавливаем **PHP**:
```
apt-get install php
```
- Устанавливаем **Apache2**:
```
apt-get install apache2
```
- Устанавливаем **Vim**:
```
apt-get install vim
```
- Запускаем **Apache2**:
```
service apache2 start
```

Для **main** экземпляра:
- В код в файле *script.js* нужно внести изменения соответственно указаниям комментариев внутри этого файла.
- Загружаем исходники, нажав на значёк шестирёнки и выбрав пункт Загрузить файл в окне, в котором открыт терминал *main* экземпляра.
Загружаем все файлы из папки *main*. Файлы загрузятся в корневую папку ВМ. У меня корневой пакой была */home/petrorud1996*, поскольку аккаунт зарегистрирован на адресс *petrorud1996@gmail.com*.
- Копируем все загруженные файлы из корневой папки ВМ в корневую папку apache2 сервера */var/www/html*. 
Вместо *petrorud1996* нужно подставить своё значение:
```
cp /home/petrorud1996/index.php /var/www/html
cp /home/petrorud1996/script.js /var/www/html
cp /home/petrorud1996/jquery-3.1.1.js /var/www/html
```

Для **i2** экземпляра:
- Загружаем исходники, как и для *main* экземпляра, но в терминале *i2*. Загружаем файл *index.php* из папки *i2*.
- Копируем *index.php* из корневой папки ВМ в корневую папку apache2 сервера */var/www/html*. 
Вместо *petrorud1996* нужно подставить своё значение:
```
cp /home/petrorud1996/index.php /var/www/html
```

Для **i3** экземпляра:
- Всё те же действия, что и для *i2*.

После всех вышеуказанных настроек проверяем работаспособность:
- Переходим в браузере по внешнему IP-адресу главного экземпляра.
- Копируем *index.php* из корневой папки ВМ в корневую папку apache2 сервера */var/www/html*. 
Вместо *35.237.142.144* нужно подставить своё значение:
```
http://35.237.142.144/?number=1000
```
- Изменяя значение параметра *number*, мы выбираем до которого предела искать простые числа.