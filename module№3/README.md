# *Demo2025 - Модуль 3*

> Предупреждение - 3 модуль делался поверх 2 модуля

### Содержание

1. **[Выполните миграцию на новый контроллер домена BR-SRV с HQ-SRV, являющийся наследием](https://github.com/Vafla1/Demo2025A/edit/main/module%E2%84%963/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-1)**
    
2. **[Выполните настройку центра сертификации на базе HQ-SRV](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%963/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-2)**

3. **[Перенастройте ip-туннель с базового до уровня туннеля,обеспечивающего шифрование трафика](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%963/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-3)**

4. **[Настройте межсетевой экран на маршрутизаторах HQ-RTR и BR-RTR на сеть в сторону ISP](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%963/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-4)**

5. **[Настройте принт-сервер cups на сервере HQ-SRV](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%963/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-5)**
    
6. **[Реализуйте логирование при помощи rsyslog на устройствах HQ-RTR,BR-RTR, BR-SRV](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%963/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-6)**

7. **[На сервере HQ-SRV реализуйте мониторинг устройств с помощью открытого программного обеспечения. Обеспечьте доступность по URL - https://mon.au-team.irpo](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%963/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-7)**

8. **[Реализуйте механизм инвентаризации машин HQ-SRV и HQ-CLI через Ansible на BR-SRV](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%963/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-8)**

9. **[Реализуйте механизм резервного копирования конфигурации для машин HQ-RTR и BR-RTR, через Ansible на BR-SRV](https://github.com/Vafla1/Demo2025A/edit/main/module%E2%84%963/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-9)**
<br/>

<br/>

<p align="center">
  <img width=auto height=auto src="https://github.com/user-attachments/assets/fa3a32f2-3a63-468d-bb4d-86261bf7f9c8"
<p\>
<p align="center"><strong>Топология сети</strong></p>

<br/>

## Задание 1

### Выполните миграцию на новый контроллер домена BR-SRV с HQ-SRV, являющийся наследием

- Для экспорта напишите сценарий, используйте для выгрузки файл.csv

- Произведите экспорт и последующий импорт на новый домен пользователей, сохранив логины, описание в виде: ФИО, пароли, подключенные сетевые диски

- Произведите экспорт и последующий импорт групп и членов групп, кроме стандартных

- Произведите экспорт и последующий импорт подразделений, и входящих в них пользователей и групп

- Произведите экспорт и последующий импорт общих папок и разрешения к ним

- Реализуйте автоматическое монтирование общих папок на HQ-CLI
<br/>

<details>
<summary>Не решено</summary>

<br/>

</details>

<br/>

## Задание 2

### Выполните настройку центра сертификации на базе HQ-SRV

- Необходимо использовать отечественные алгоритмы шифрования

- Сертификаты выдаются на 365 дней

- Обеспечьте доверие сертификату для HQ-CLI

- Выдайте сертификаты веб серверам

- Перенастройте ранее настроенные веб сервера, moodle, wiki, реверсивный прокси nginx на протокол https

- На HQ-CLI настройте автомонтирование в папку /mnt/nfs

- При обращении к веб серверам по их доменным именам у браузера клиента не должно возникать предупреждений

<br/>

<details>
<summary>Не решено</summary>
  
<br/>

</details>

<br/>

## Задание 3

### Перенастройте ip-туннель с базового до уровня туннеля, обеспечивающего шифрование трафика

- Настройте защищенный туннель между HQ-RTR и BR-RTR

- Внесите необходимые изменения в конфигурацию динамической маршрутизации, протокол динамической маршрутизации должен возобновить работу после перенастройки туннеля

- Выбранное программное обеспечение, обоснование его выбора и его основные параметры, изменения в конфигурации динамической маршрутизации отметьте в отчёте

<br/>

<details>
<summary>Не решено</summary>
  
<br/>

</details>

<br/>

## Задание 4

### Настройте межсетевой экран на маршрутизаторах HQ-RTR и BR-RTR на сеть в сторону ISP

- Обеспечьте работу протоколов http, https, dns, ntp, icmp или дополнительных нужных протоколов

- Запретите остальные подключения из сети Интернет во внутреннюю сеть

<br/>

<details>
<summary>Не решено</summary>

<br/>

</details>

<br/>

## Задание 5

### Настройте принт-сервер cups на сервере HQ-SRV

- Опубликуйте виртуальный pdf-принтер

- На клиенте HQ-CLI подключите виртуальный принтер как принтер по умолчанию

<br/>

<details>
<summary>Решение</summary>

<br/>

#### Настройка cups

![image](https://github.com/user-attachments/assets/8a2fe813-7684-448e-ad3f-94fe0bad28ef)

<br/>

![image](https://github.com/user-attachments/assets/b963daa0-3291-44dc-b061-21291595b019)

<br/>

![image](https://github.com/user-attachments/assets/5aa887bb-7458-40d8-98b1-e8b02b6a60c9)

<br/>

![image](https://github.com/user-attachments/assets/19705807-5fb9-495d-a3af-9ef6639b62cb)

<br/>

![image](https://github.com/user-attachments/assets/88f6e99d-4f9a-48fb-9029-3469906be4d1)

<br/>

![image](https://github.com/user-attachments/assets/dacfeb2a-91b6-4d49-b63a-279d5713547f)

<br/>

![image](https://github.com/user-attachments/assets/62bacc42-8c54-4095-9b42-ba3e0cac561e)

<br/>

![image](https://github.com/user-attachments/assets/36cb03f9-33b7-4083-861a-9918521f164d)

<br/>

![image](https://github.com/user-attachments/assets/c2b4b0e3-5f47-4286-97e5-410ad3452a79)


<br/>

![image](https://github.com/user-attachments/assets/7fe0bab3-7aa8-4b1d-ac85-427d69a6269c)

</details>

<br/>

## Задание 6

### Реализуйте логирование при помощи rsyslog на устройствах HQ-RTR, BR-RTR, BR-SRV

- Сервер сбора логов расположен на HQ-SRV, убедитесь, что сервер не является клиентом самому себе

- Приоритет сообщений должен быть не ниже warning

- Все журналы должны находиться в директории /opt. Для каждого устройства должна выделяться своя поддиректория, которая совпадает с именем машины

- Реализуйте ротацию логов:

  - Ротация производится один раз в неделю
 
  - Логи необходимо сжимать
 
  - Минимальный размер логов для ротации – 10 МБ

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка syslog

![image](https://github.com/user-attachments/assets/dd1b7a8a-741c-49d6-b659-f938516cbe14)

<br/>

![image](https://github.com/user-attachments/assets/4790c3eb-5695-46a9-aa4b-d06338f6b0f0)

<br/>

![image](https://github.com/user-attachments/assets/e3f08017-d77b-464e-85ba-8a19a30ec990)

<br/>

![image](https://github.com/user-attachments/assets/d5119ab2-88e7-4dcf-ab68-0398f0882c45)

<br/>

![image](https://github.com/user-attachments/assets/3bbd1970-3812-453b-9f7f-132dfadac9d8)

<br/>

![image](https://github.com/user-attachments/assets/3a6fa072-79da-4f45-8967-e9904798dcc6)

<br/>

![image](https://github.com/user-attachments/assets/c8fe8b42-d783-42d7-91d4-4e324d785b27)

<br/>

![image](https://github.com/user-attachments/assets/c8aad9d9-d61c-4680-86dd-7e6fd781f25c)

<br/>

![image](https://github.com/user-attachments/assets/d08c0da8-e227-4913-b1c2-cf66e99f2d1b)

</details>

<br/>

## Задание 7

### На сервере HQ-SRV реализуйте мониторинг устройств с помощью открытого программного обеспечения. Обеспечьте доступность по URL - https://mon.au-team.irpo

- Мониторить нужно устройства HQ-RTR, HQ-SRV, BR-RTR и BR-SRV

- В мониторинге должны визуально отображаться нагрузка на ЦП, объем занятой ОП и основного накопителя

- Логин и пароль для службы мониторинга admin P@ssw0rd!!

- Выбор программного обеспечения, основание выбора и основные параметры с указанием порта, на котором работает мониторинг, отметьте в отчёте

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Конфигурация Zabbix

<br/>
![image](https://github.com/user-attachments/assets/f9fd24df-6f0a-482b-a6da-38bbae78026f)

<br/>
<br/>
<br/>
<br/>


</details>

<br/>

## Задание 8

### Настройте веб-сервер nginx как обратный прокси-сервер на HQ-RTR 

- При обращении к HQ-RTR по доменному имени moodle.au-team.irpo клиента должно перенаправлять на HQ-SRV на стандартный порт, на сервис moodle
  
- При обращении к HQ-RTR по доменному имени wiki.au-team.irpo клиента должно перенаправлять на BR-SRV на порт, на сервис mediwiki 


<br/>

<details>
<summary>Решение</summary>
<br/>

**Так как на HQ-RTR нет утилиты nginx, обратным-прокси будет выступать ISP**

#### Установка и настройка nginx

Установка пакета:
```yml
apt-get install nginx
```

<br/>

Настройка **`конфигурационного файла /etc/nginx/nginx.conf`**. Нужно в httpd{} добавить:
```yml
server {
        server_name moodle.au-team.irpo;
        location / {
            proxy_pass http://172.16.4.2:80/moodle/;
            proxy_redirect      off;
            proxy_set_header    Host    $host;
            proxy_set_header    X-Real-IP       $remote_addr;
            proxy_set_header    X-Forwaded-For  $proxy_add_x_forwarded_for;
        }
}

server {
        server_name wiki.au-team.irpo;
        location / {
            proxy_pass http://172.16.5.2:80/;
            proxy_redirect      off;
            proxy_set_header    Host    $host;
            proxy_set_header    X-Real-IP       $remote_addr;
            proxy_set_header    X-Forwaded-For  $proxy_add_x_forwarded_for;
        }
}
```

<br/>

Добавим в автозагрузку:
```yml
systemctl enable --now nginx
```

<br/>

#### Доработка на BR-SRV

Чтобы клиент видел по имени wiki и moodle необходимо на br-srv:
```yml
samba-tool computer add wiki --ip-address=172.16.5.1
samba-tool computer add moodle --ip-address=172.16.4.1
```

<br/>

#### Доработка wiki

Чтобы wiki работал по имени wiki.au-team.irpo. Нужно редактировать строки файла LocalSettings на BR-SRV:
```yml
$wgServer = "http://wiki.au-team.irpo:80";
```

<br/>

Перезагрузим wiki:
```yml
docker compose -f wiki.yml stop
docker compose -f wiki.yml up -d
```

<br/>

#### Доработка moodle

Чтобы moodle работал по имени moodle.au-team.irpo. Нужно редактировать строки файла /var/www/webapps/moodle/config.php на HQ-SRV:
```yml
$CFG->wwwroot   = 'http://moodle.au-team.irpo';
```

Перезагрузим moodle:
```yml
systemctl restart httpd2
```

<br/>
<br/>
<br/>
<br/>
#### Пример:
![image](https://github.com/user-attachments/assets/3f421750-aff8-43c0-a48f-be9851324fc1)

<br/>

#### Теперь при обращении на moodle.au-team-irpo или на wiki.au-team.irpo будет выходить

<p align="center">
  <img width="600" src="https://github.com/user-attachments/assets/8433d0a1-fe50-4bfc-8748-4e2959fcd866"
</p>

<br/>

<p align="center">
  <img width="600" src="https://github.com/user-attachments/assets/2d83447d-2a50-4122-b190-0caf1191ded8"
</p>

<br/>

</details>

## Задание 9

### Удобным способом установите приложение Яндекс Браузере для организаций на HQ-CLI 

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Установка Яндекс Браузера

Установка пакета:
```yml
apt-get install yandex-browser-stable
```
</details>

<br/>
