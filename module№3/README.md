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

![image](https://github.com/user-attachments/assets/9decab7d-c118-4d13-9299-390726150cc7)

<br/>

![image](https://github.com/user-attachments/assets/a55f7dfb-69d5-42a4-a095-cbca2c8a7eb6)

<br/>

![image](https://github.com/user-attachments/assets/b3a1d27b-28f2-4ab8-9af2-ab8f1fc29fcb)

<br/>

![image](https://github.com/user-attachments/assets/5a45186e-991f-4470-8758-44789d97a66a)

<br/>

![image](https://github.com/user-attachments/assets/55582917-f8bc-487b-ace1-e33b8f3bfc8e)

<br/>

![image](https://github.com/user-attachments/assets/65ec9b5c-a29d-47d1-b49d-9d5adffa56f9)

<br/>

![image](https://github.com/user-attachments/assets/f7d2fb27-f075-49c8-94a9-4b2e86d44917)

<br/>

![image](https://github.com/user-attachments/assets/443c44e5-6f97-4ed3-b88b-8c3b952ec0c1)

<br/>

![image](https://github.com/user-attachments/assets/695a5644-1208-4b38-8282-30cb9dfc70b1)

<br/>

![image](https://github.com/user-attachments/assets/1520edf4-78b7-475b-a831-e490a587f433)

<br/>

![image](https://github.com/user-attachments/assets/682fd2c2-51ba-48d0-9294-07af9a548efe)

<br/>

![image](https://github.com/user-attachments/assets/b86f8a5a-0750-4266-897f-4e3a1814730f)

<br/>

![image](https://github.com/user-attachments/assets/df1c141b-7792-4f39-8398-1b6c5588a2b9)

<br/>

![image](https://github.com/user-attachments/assets/7298ad50-06d2-41cc-a2e1-bbbbfed0c8da)

<br/>

![image](https://github.com/user-attachments/assets/f38c72b9-5794-43da-8bb7-846e3da68674)

<br/>

![image](https://github.com/user-attachments/assets/ad552db4-905a-4a2e-999c-96a4e1802cb8)

<br/>

![image](https://github.com/user-attachments/assets/28e91516-d04f-478e-aad3-b01b7791b34e)

<br/>

![image](https://github.com/user-attachments/assets/d09f7d59-5ec0-4169-aec6-61f7785ebb7d)
Также добавить cname в dnsmasq на hq-srv

<br/>

![image](https://github.com/user-attachments/assets/bccf30bf-cbb9-4b97-be05-7dcfb7cfd809)

<br/>

![image](https://github.com/user-attachments/assets/4376ce06-1b64-4f35-8a61-28f0739134ce)

<br/>

![image](https://github.com/user-attachments/assets/215f1d37-5d52-4886-901d-e477cd36773d)

<br/>

![image](https://github.com/user-attachments/assets/40cdf605-9375-447d-99a0-ee3f8cc2e4aa)

<br/>

![image](https://github.com/user-attachments/assets/54ec1b2e-4329-4809-834d-d8b658077def)

<br/>

![image](https://github.com/user-attachments/assets/5b6ddba1-9a69-4c52-a198-90dc5215f3d9)

</details>

<br/>

## Задание 8

### Реализуйте механизм инвентаризации машин HQ-SRV и HQ-CLI через Ansible на BR-SRV

- Плейбук должен собирать информацию о рабочих местах:
  
    - Имя компьютера
      
    - IP-адрес компьютера
 
    - Отчеты, собранные с машин, должны быть размещены в том же каталоге на сервере, где и плейбук, в папке PC_INFO, в формате .yml. Файл называется именем компьютера, который был инвентаризован

    - Рабочий каталог ansible должен располагаться в /etc/ansible


<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка anible

![image](https://github.com/user-attachments/assets/74a872ef-94d1-4d25-8fcb-e4870c1b0f7f)

<br/>

![image](https://github.com/user-attachments/assets/59229546-7d9c-4193-85ff-1c70b2064ca4)

<br/>

![image](https://github.com/user-attachments/assets/8872e95d-bdcd-40fc-80ab-775601963a38)

<br/>
<br/>

</details>

## Задание 9

### Реализуйте механизм резервного копирования конфигурации для машин HQ-RTR и BR-RTR, через Ansible на BR-SRV

- Плейбук должен собирать информацию о сетевых устройствах HQ-RTR и BR-RTR и делать резервную копию конфигурации (в случае использования EcoRouter – полную конфигурацию, в случае ОС на базе Linux – файлы конфигурации динамической маршрутизации, настроек межсетевого экрана, параметров настройки сети, настройки динамической конфигурации хостов). Информацию сохранять в папку NETWORK_INFO

<br/>

<details>
<summary>Не решено </summary>
<br/>

</details>

<br/>
