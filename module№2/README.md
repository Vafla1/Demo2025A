# *Demo2025 - Модуль 2*

> Предупреждение - модуль 1 и 2 не совпадают по IP-адресам. Также могут быть отличия от этого стенда

### Содержание

1. **[Настройте доменный контроллер Samba на машине BR-SRV](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%962/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-1)**
    
2. **[Сконфигурируйте файловое хранилище](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%962/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-2)**

3. **[Настройте службу сетевого времени на базе сервиса chrony](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%962/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-3)**

4. **[Сконфигурируйте ansible на сервере BR-SRV](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%962/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-4)**

5. **[Развертывание приложений в Docker на сервере BR-SRV](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%962/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-5)**
    
6. **[На маршрутизаторах сконфигурируйте статическую трансляцию портов](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%962/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-6)**

7. **[Запустите сервис moodle на сервере HQ-SRV](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%962/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-7)**

9. **[Удобным способом установите приложение Яндекс Браузере для организаций на HQ-CLI](https://github.com/Vafla1/Demo2025A/edit/main/module%E2%84%962/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-9)**
<br/>

<br/>

<p align="center">
  <img width=auto height=auto src="https://github.com/user-attachments/assets/fa3a32f2-3a63-468d-bb4d-86261bf7f9c8"
<p\>
<p align="center"><strong>Топология сети</strong></p>

<br/>

## Задание 1

### Настройте доменный контроллер Samba на машине BR-SRV

- Создайте 5 пользователей для офиса HQ: имена пользователей фомата user№.hq. Создайте группу hq, введите в эту группу созданных пользователей

- Введите в домен машину HQ-CLI

- Пользователи группы hq имеют право аутентифицироваться на клиентском ПК

- Пользователи группы hq должны иметь возможность повышать привилегии для выполнения ограниченного набора команд: cat, grep, id. Запускать другие команды с повышенными привилегиями пользователи не имеют права

- Выполните импорт пользователей из файла users.csv. Файл будет располагаться на авиртуальной машине BR-SRV в папке /opt

<br/>

<details>
<summary>Решено не полностью</summary>
<br/>

Так как HQ-CLI войдет в домен нужно добавить ему DNS нашего будущего samba(BR-SRV) на HQ-RTR перенастроим DHCP:
```yml
dhcp-server 1
dns 192.168.3.10, 192.168.1.10
```

<br/>

Сохраним:
```yml
wr mem
```
#### Пример:
![image](https://github.com/user-attachments/assets/f67c7da5-ef9f-4294-8274-111921226e5b)

![image](https://github.com/user-attachments/assets/45c79f79-38ad-4ba2-8899-35413f765cac)

![image](https://github.com/user-attachments/assets/2380b73c-9262-46d4-988d-d533ab8ef00f)

<br/>

Установим samba на BR-SRV:
```yml
apt-get update && apt-get install task-samba-dc
```

<br/>

Создадим и очистим некоторые папки:
```yml
rm /etc/samba/smb.conf
rm -rf /var/lib/samba/
rm -rf /var/cache/samba/
mkdir -p /var/lib/samba/sysvol/
```

<br/>

Настройка DNS. На интерфейсе в resolv.conf нужно указать себя. Потом перезагрузить сеть:
```yml
nameserver 127.0.0.1
search au-team.irpo
```
#### Пример:
![image](https://github.com/user-attachments/assets/df8f7ef4-b84b-414b-b3c6-da876b1d7dbb)

<br/>

Настроем samba (если выйдет ошибка снова удалите smb.conf):
```yml
samba-tool domain provision --realm=au-team.irpo --domain=au-team --adminpass='P@ssw0rd' --dns-backend=SAMBA_INTERNAL --option="dns forwarder = 192.168.1.10" --server-role=dc --use-rfc2307
```

<br/>

Скопируем файл krb5.conf и добавим samba в автозагрузку:
```yml
cp /var/lib/samba/private/krb5.conf /etc/krb5.conf
systemctl enable --now samba
```

<br/>

Проверим (если все хорошо, то samba настроен корректно):
```yml
apt-get install bind-utils
host -t SRV _kerberos._udp.au-team.irpo
```

<br/>

Переходим на клиента HQ-CLI и устанавливаем пакетик жиес:
```yml
apt-get update && apt-get install task-auth-ad-sssd admc gpui
```

<br/>

Чтобы добавить клиента в домен переходим на рабочем столе в Menu -> Contorl Center -> System managment center -> Authentication

![image](https://github.com/user-attachments/assets/1a88dddb-2bd2-407c-84c8-07e5c3cbcb5c)

Применяем. Вводим пароль Администратора домена:

![image](https://github.com/user-attachments/assets/b319352b-1ee9-4bac-9425-41e0fcee8de0)

Через некоторое время должно выйти " Добро пожаловать в au-team.irpo ". Потом необходимо перезагрузить машину

<br/>

Создаем пользователей на BR-SRV:
```yml
samba-tool user add user1.hq
samba-tool user add user2.hq
samba-tool user add user3.hq
samba-tool user add user4.hq
samba-tool user add user5.hq
```

<br/>

Создаем группу hq и добавляем в нее пользователей:
```yml
samba-tool group add hq
samba-tool group addmembers hq user1.hq,user2.hq,user3.hq,user4.hq,user5.hq
```

<br/>

Разрешаем использовать sudo всем
```yml
control sudo public
```

<br/>

Настройка прав пользователей группы hq. Редактируем файл /etc/sudoers:
```yml
%hq ALL=(root) /usr/bin/id, /bin/grep, /bin/cat
```
#### Пример:
![image](https://github.com/user-attachments/assets/70b6c999-c7bd-4a75-949e-f72fb88279f5)

</details>

<br/>

## Задание 2

### Сконфигурируйте файловое хранилище

- При помощи трех дополнительных дисков, размером 1Гб каждый, на HQ-SRV сконфигурируйте дисковый массив уровня 5

- Имя устройства - md0, конфигурация массива размещается в файле /etc/mdadm.conf

- Обеспечьте автоматическое монтирование в папку /raid5

- Создайте раздел, отформатируйте раздел, в качестве файловой системы используйте ext4

- Настройте сервер сетевой файловой системы (nfs), в качестве папки общего доступа выберите /raid5/nfs, доступ для чтения и записи для всей сети в сторону HQ-CLI

- На HQ-CLI настройте автомонтирование в папку /mnt/nfs

- Основные параметры сервера отметьте в отчете

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Создание RAID

Просматриваем имена добавленных дисков:
```yml
lsblk
```
> Вывод:
> ```yml
> sdb  8:16  0  1G  0  disk
> sdc  8:32  0  1G  0  disk
> sdd  8:48  0  1G  0  disk
> ```

<br/>

Устанавливаем mdadm и nfs:
```yml
apt-get update && apt-get install mdadm nfs-server
```

<br/>

Создаем **RAID**:
```yml
mdadm --create /dev/md0 -l 5 -n 3 /dev/sd{b,c,d}
```
> **/dev/md0** - название RAID после сборки
>
> **-l 5** - уровень RAID
>
> **-n 3** - количество дисков, из которых собирается массив
>
> **/dev/sd{b,c,d}** - диски, из которых выполняется сборка

<br/>

Проверяем:
```yml
lsblk
```
> Вывод:
> ```yml
> sdb  8:16  0  1G  0  disk
>   md0  9:0  0  2G  0  raid5
> sdc  8:32  0  1G  0  disk
>   md0  9:0  0  2G  0  raid5
> sdd  8:48  0  1G  0  disk
>   md0  9:0  0  2G  0  raid5
> ```

<br/>

#### Создание файла `mdadm.conf`

Заполняем файл информацией:
```yml
echo "DEVICE partitions" > /etc/mdadm/mdadm.conf
mdadm --detail --scan | awk '/ARRAY/ {print}' >> /etc/mdadm/mdadm.conf
```

<br/>

Создаем файловую систему из созданного **RAID**:
```yml
mkfs -t ext4 /dev/md0
```

<br/>

#### Создание файловой системы и монтирование RAID-массива

Создаем директорию для монтирования массива:
```yml
mkdir /raid5
```

<br/>

Смотрим имя диска md0:
```yml
blkid /dev/md0
```

<br/>

Добавляем строку в **`/etc/fstab`**:
```yml
UUID=09994f40-ef75-439c-9f13-20f3a0014ca3  /raid5  ext4  defaults  0  0
```

<br/>

Монтируем:
```yml
mount -a
```

<br/>

Проверяем монтирование:
```yml
df -h
```
> Вывод:
> ```yml
> /dev/md0  2.0G  24K  1.9G  1%  /raid5
> ```

<br/>

#### Настройка NFS

Создаем директорию для общего доступа:
```yml
mkdir /raid5/nfs
```

<br/>

Добавляем строку в **`/etc/exports`**:
```yml
/raid5/nfs 192.168.2.0/28 (sync,rw,no_root_squash)
```
> **/mnt/raid5/nfs** - общий ресурс
>
> **192.168.2.0/28** - клиентская сеть, которой разрешено монтирование общего ресурса
>
> **sync** — синхронный режим доступа
>
> **rw** — разрешены чтение и запись
>
> **no_root_squash** — отключение ограничения прав **root**

<br/>


Запускаем и добавляем в автозагрузку **NFS-сервер**:
```yml
systemctl enable --now nfs-server
```

<br/>

Чтобы клиент видел по имени hq-rtr и br-rtr необходимо на br-srv:
```yml
samba-tool computer add hq-rtr --ip-address=192.168.2.1
samba-tool computer add br-rtr --ip-address=192.168.3.1
samba-tool computer add hq-srv --ip-address=192.168.1.10
```

<br/>

#### Настройка клиента

Устанавливаем требуемые пакеты для **NFS-клиента**:
```yml
apt-get install -y nfs-{utils,clients}
```

<br/>

Создаем директорию для общего ресурса:
```yml
mkdir /mnt/nfs
```

<br/>

Выдаем права этой директории:
```yml
chmod 777 /mnt/nfs
```

<br/>

Добавляем строку в **`/etc/fstab`** для автоматического монтирования общего ресурса:
```yml
hq-srv:/raid5/nfs  /mnt/nfs  nfs  defaults  0  0
```

<br/>

Монтируем общий ресурс:
```yml
mount -a
```

<br/>

Проверяем монтирование:
```yml
df -h
```
> Вывод:
> ```yml
> hq-srv:/mnt/raid5/nfs  2,0G  0  1,9G  0%  /mnt/nfs
> ```
</details>

<br/>

## Задание 3

### Настройте службу сетевого времени на базе сервиса chrony

- В качества сервера выступает HQ-RTR

- На HQ-RTR настройте сервер chrony, выберите стратум 5

- В качестве клиентов настройте HQ-SRV, HQ-CLI, BR-RTR, BR-SRV

<br/>

<details>
<summary>Решение</summary>
<br/>

**Так как на HQ-RTR нет утилиты chrony и возможность выбора стратума, NTP-сервером будет выступать ISP**

#### Конфигурация NTP-сервера (ISP)

Скачиваем пакет **chrony**:
```yml
apt-get install -y chrony
```

<br/>

Приводим начало файла **`/etc/chrony.conf`** к следующему виду:
```yml
# Use public servers from the pool.ntp.org project.
# Please consider joining the pool (https://www.pool.ntp.org/join.html
#pool pool.ntp.org iburst

server 2.ru.pool.ntp.org iburst prefer
hwtimestamp *
local stratum 5
allow 0/0
```
> **server 2.ru.pool.ntp.org** - указываем сервером синхронизации самого себя
> > **iburst** - принудительно отправляет пакеты для точности синхронизации
> > 
> > **prefer** - отдает приоритет этому серверу
>
> **hwtimestamp** * - указывает сетевой интерфейс как собственный источник времени и синхронизирует клиентов с ним
>
> **local stratum 5** - указание иерархического уровня
>
> **allow 0/0** - разрешает подключение с любого IP-адреса

<br/>

Запускаем и добавляем в автозагрузку утилиту **chronyd**:
```yml
systemctl enable --now chronyd
```

<br/>

#### Конфигурация NTP-клиента EcoRouter

Указываем IP-адрес **NTP-сервера**:
```yml
ntp server 172.16.4.1
```

<br/>

Указываем часовой пояс:
```yml
ntp timezone utc+5
```

<br/>

Сохраняемся:
```yml
wr mem
```

<br/>

#### Конфигурация NTP-клиента Alt Linux

Скачиваем пакет **chrony**:
```yml
apt-get install chrony
```

<br/>

Приводим начало файла **`/etc/chrony.conf`** к следующему виду:
```yml
#pool pool.ntp.org iburst
server 172.16.4.1 iburst prefer
```
> **iburst** - принудительно отправляет пакеты для точности синхронизации
>
> **prefer** - отдает приоритет этому серверу

<br/>

Указываем timezone void бы оценил)
```yml
timedatectl set-timezone Asia/Yekaterinburg
```

<br/>

Запускаем утилиту **chrony** и добавляем ее в автозагрузку:
```yml
systemctl enable --now chronyd
```

</details>

<br/>

## Задание 4

### Сконфигурируйте ansible на сервере BR-SRV

- Сформируйте файл инвентаря, в инвентарь должны входить HQ-SRV, HQ-CLI, HQ-RTR и BR-RTR

- Рабочий каталог ansible должен располагаться в /etc/ansible

- Все указанные машины должны без предупреждений и ошибок отвечать pong на команду ping в ansible посланную с BR-SRV

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Конфигурация SSH Alt Linux

Затронутые строки в конфигурационном файле **SSH** **`/etc/openssh/sshd_config`** должны выглядеть следующим образом:
```yml
Port 2024
MaxAuthTries 2
PubkeyAuthentication yes
PasswordAuthentication yes
Banner /etc/openssh/bannermotd
AllowUsers  sshuser
```
> Первоначальная настройка **SSH** производилась в задании **[Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-5)** из **[Модуля 1](https://github.com/Vafla1/Demo2025A/tree/main/module%E2%84%961)**

<br/>

#### Конфигурация Ansible

Устанавливаем необходимые пакеты:
```yml
apt-get install -y ansible sshpass
```

<br/>

Нужно задать интерпретатор в **конфигурационном файле `/etc/ansible/hosts`**:
```yml
[defaults]
interperter_python=/usr/bin/python3 
```

<br/>

Редактируем указанные строки в **файле `/etc/ansible/hosts`**:
```yml
[local:vars]
ansible_user=sshuser
ansible_password=P@ssw0rd
ansible_python_interpreter=/usr/bin/python3
ansible_port 2024

[local]
hq-srv
hq-cli

[ecorouter:vars]
ansible_user=net_admin
ansible_password=P@$$word
ansible_connection=network_cli
ansible_network_os=ios
ansible_python_interpreter=/usr/bin/python3

[ecorouter]
hq-rtr
br-rtr
```

<br/>

Зайдите по ssh на HQ-CLI и HQ-SRV, чтобы внести их в доверенные устройства:
```yml
ssh -p 2024 ssh@name
```

<br/>

Чтобы разрешить подключение по ssh на ecorouter нужно выполнить:
```yml
security none
```

<br/>

Сохраним:
```yml
wr mem
```

<br/>

Выполняем команду для **ping**`а всех машин:
```yml
ansible -m ping all
```
> **-m (--module-name)** - параметр для указания модуля
>
> **ping** - модуль
>
> **all** - выполнить модуль для всех виртуальных машин, указанных в инвентарном файле

<br/>

</details>

<br/>

## Задание 5

### Развертывание приложений в Docker на сервере BR-SRV

- Создайте в домашней директории пользователя файл wiki.yml для приложения MediaWiki

- Средствами docker compose должен создаваться стек контейнеров с приложением MediaWiki и базой данных

- Используйте два сервиса

- Основной контейнер MediaWiki должен называться wiki и использовать образ mediawiki

- Файл LocalSettings.php с корректными настройками должен находиться в домашней папке пользователя и автоматически монтироваться в образ

- Контейнер с базой данных должен называться mariadb и использовать образ mariadb

- Разверните

- Он должен создавать базу с названием mediawiki, доступную по стандарнтому порту, пользователя wiki с паролем WikiP@ssw0rd должен иметь права доступа к этой базе данных

- MediaWiki должна быть доступна извне через порт 8080

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Конфигурация файла Docker-Compose

Останавливаем службу **httpd**, которая занимает порт **8080**:
```yml
systemctl disable —now httpd
```
> **httpd** - модуль для веб-интерфейса, который предназначен для управления настройками web-сервера, обеспечивающего работоспособность **Центра управления системой**

<br/>

Устанавливаем **docker** и **docker-compose**:
```yml
apt-get install -y docker-engine docker-compose
```

<br/>

Включаем и добавляем в автозагрузку **docker**:
```yml
systemctl enable --now docker
```

<br/>

В домашней директории пользователя создаем файл **`wiki.yml`** и прописываем следующее:
```yml
# MediaWiki with MariaDB
#
# Access via "http://localhost:8080"
services:
  wiki:
    image: mediawiki
    restart: always
    ports:
      - 8080:80
    links:
      - mariadb
    volumes:
      - images:/var/www/html/images
      # After initial setup, download LocalSettings.php to the same directory as
      # this yaml and uncomment the following line and use compose to restart
      # the mediawiki service
      # - ./LocalSettings.php:/var/www/html/LocalSettings.php
  mariadb: # <- This key defines the name of the database during setup
    image: mariadb
    restart: always
    environment:
      # @see https://phabricator.wikimedia.org/source/mediawiki/browse/master/include>
      MYSQL_DATABASE: mediawiki
      MYSQL_USER: wiki
      MYSQL_PASSWORD: WikiP@ssw0rd
      MYSQL_RANDOM_ROOT_PASSWORD: 'yes'
    volumes:
      - db:/var/lib/mysql

volumes:
  images:
  db:
```
> **services** - основной раздел, в котором описываются сервисы
>
> **container_name** - имя контейнера
>
> **image** - имя образа
>
> **restart** - перезапуск контейнера, если он остановлен
>
> **ports** - проброс портов
>
> **links** - ссылка на контейнер
> 
> **volumes** - проброс папок
>
> **environment** - переменные окружения

<br/>

Собираем стек контейнеров:
```yml
docker compose -f wiki.yml up -d
```
> **-f** - указание на файл
>
> **up** - запуск
>
> **-d** - запуск в фоновом режиме

<br/>

#### Установка MediaWiki в веб-интерфейсе

На **HQ-CLI** в браузере вводим **`http://br-srv:8080`** и начинаем установку **MediaWiki**, нажав на **set up the wiki**:
<p align="center">
  <img width="600" src="https://github.com/user-attachments/assets/52ef6b9b-ba3e-428d-af07-0992be7c01a2"
</p>

<br/>

Выбираем язык:
<p align="center">
  <img width="400" src="https://github.com/user-attachments/assets/c59c1003-75e6-4dbb-bfa2-9808fa31d51f"
</p>

<br/>

Проверяем внешнюю среду и нажимаем **далее**:
<p align="center">
  <img width="600" src="https://github.com/user-attachments/assets/b09a45e6-eb92-4d8f-b2c4-4a280352bdf0"
</p>

<br/>

Заполняем параметры для базы данных в соответствии с заданными переменными окружения в **wiki.yml**:
<p align="center">
  <img width="250" src="https://github.com/user-attachments/assets/b3da0131-f70c-40e9-b0ab-5d818195dc3f"
</p>

<br/>

Оставляем галочку и жмем **далее**:
<p align="center">
  <img width="550" src="https://github.com/user-attachments/assets/2ebdc0e0-027d-4aff-9d00-4c1b4e38c358"
</p>

<br/>

Заполняем информацию об учетной записи администратора:
<p align="center">
  <img width="500" src="https://github.com/user-attachments/assets/0b60037a-7e9f-4f0f-9290-a4d0b2f457fb"
</p>

<br/>

Подтверждаем установку **MediaWiki**:
<p align="center">
  <img width="500" src="https://github.com/user-attachments/assets/d338a392-ce13-414c-ba16-2e45743d1d4f"
</p>

<br/>

После окончания установки нажимаем **далее**:
<p align="center">
  <img width="450" src="https://github.com/user-attachments/assets/158beb5a-9715-46cc-8af5-1e3e0b05176d"
</p>

<br/>

Получаем конфигурационный файл, который нужно передать на **BR-SRV**:
<p align="center">
  <img width="800" src="https://github.com/user-attachments/assets/923ad086-0244-4b4b-be83-1973c193f355"
</p>

<br/>

#### Правка файла Docker-Compose

Перемещаем файл **`LocalSettings.php`** в домашнюю директорию пользователя **sshuser**:
```yml
mv /home/user/Downloads/LocalSettings.php /home/sshuser
```
> В моем случае, ранние действия выполнялись из под пользователя **user**, поэтому загруженный файл оказался именно в его папке

<br/>

Передаем файл с **HQ-CLI** на **BR-SRV**:
```yml
scp -P 2024 /home/sshuser/LocalSettings.php sshuser@br-srv:/home/sshuser
```
> **-P** - указание порта SSH
>
> **/home/sshuser/LocalSettings.php** - файл, который будет передан
>
> **sshuser@br-srv:/home/sshuser** - имя-пользователя@IP-адрес:директория-назначения

<br/>

На **BR-SRV** перемещаем файл в домашнюю директорию **root**:
```yml
mv /home/sshuser/LocalSettings.php ~
```
> Если файл **wiki.yml** создавали в домашней директории другого пользователя - перемещаем туда

<br/>

В файле **wiki.yml** расскоментируем следующие строки:
```yml
volumes:
  - ./LocalSettings.php:/var/www/html/LocalSettings.php
```

<br/>

Перезапускаем запущенные **Docker**`ом сервисы:
```yml
docker compose -f wiki.yml stop
docker compose -f wiki.yml up -d
```

</details>

<br/>

## Задание 6

### На маршрутизаторах сконфигурируйте статическую трансляцию портов

- Пробросьте порт 80 в порт 8080 на BR-SRV на маршрутизаторе BR-RTR, для обеспечения работы сервиса wiki

- Пробросьте порт 2024 в порт 2024 на HQ-SRV на маршрутизаторе HQ-RTR

- Пробросьте порт 2024 в порт 2024 на BR-SRV на маршрутизаторе BR-RTR

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Конфигурация BR-RTR

Проброс портов с 80 на 8080 для работы сервиса **wiki**:
```yml
ip nat source static tcp 192.168.3.10 8080 172.16.5.2 80
```

<br/>

Проброс портов с 2024 на 2024:
```yml
ip nat source static tcp 192.168.3.10 2024 172.16.5.2 2024
```

<br/>

#### Конфигурация HQ-RTR

Проброс портов с 2024 на 2024:
```yml
ip nat source static tcp 192.168.1.10 2024 172.16.4.2 2024
```

</details>

<br/>

## Задание 7

### Запустите сервис moodle на сервере HQ-SRV

- Используйте веб-сервер apache

- В качестве системы управления базами данных используйте mariadb

- Создайте базу данных moodledb

- Создайте пользователя moodle с паролем P@ssw0rd и предоставьте ему права доступа к этой базе данных

- У пользователя admin в системе обучения задайте пароль P@ssw0rd

- На главной странице должен отражаться номер рабочего места в виде арабской цифры, других подписей делать не надо

- Основные параметры отметьте в отчеты

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Конфигурация базы данных

Устанавливаем необходимые пакеты:
```yml
apt-get install -y moodle moodle-apache2 moodle-base moodle-local-mysql phpMyAdmin
```

<br/>

Добавляем в **автозагрузку** базу данных:
```yml
systemctl enable --now mariadb
```

<br/>

Изменяем строку, отвечающую за количество входных переменных по пути **`/etc/php/8.2/apache2-mod_php/php.ini`**:
```yml
max_input_vars = 5000
```

<br/>

Добавляем в **автозагрузку** веб-сервер:
```yml
systemctl enable --now httpd2
```

<br/>

Авторизуемся в **MySQL**:
```yml
mariadb -u root
```

<br/>

Создаем базу данных:
```yml
create database moodledb default character set utf8 collate utf8_unicode_ci;
```

<br/>

Создаем **пользователя** для базы данных и выдаем ему права:
```yml
grant all on moodledb.* to moodle@localhost identified by 'P@ssw0rd';
```

<br/>

Переходим на **`hq-srv.au-team.irpo/moodle`** и выбираем язык:
<p align="center">
  <img width="600" src="https://github.com/user-attachments/assets/0e8cdfda-6466-416e-afab-e7f61fcf1b3a"
</p>

<br/>

Подтверждаем пути директорий:
<p align="center">
  <img width="400" src="https://github.com/user-attachments/assets/548b1126-3b5a-4104-a692-b0aafdd0617a"
</p>

<br/>

Выбираем систему управления базы данных:
<p align="center">
  <img width="300" src="https://github.com/user-attachments/assets/d21aa42f-8988-44f6-bcab-67e0fa9cae08"
</p>

<br/>

Заполняем данные о базе данных и пользователе:
<p align="center">
  <img width="400" src="https://github.com/user-attachments/assets/1c5414a6-5aba-4ffd-8d4a-32e49bcb770b"
</p>

<br/>

Соглашаемся с условиями:
<p align="center">
  <img width="300" src="https://github.com/user-attachments/assets/055ed45c-f87c-44ec-9f3e-0f32737f38c7"
</p>

<br/>

Убеждаемся в успешной проверке:
<p align="center">
  <img width="400" src="https://github.com/user-attachments/assets/7ddc9e35-3c96-4623-94d0-9f57e2803b3c"
</p>

<br/>

После установки настраиваем учетную запись администратора:
<p align="center">
  <img width="400" src="https://github.com/user-attachments/assets/337888dc-1542-4bdd-90c2-b43dcf14e7fa"
</p>

> Заполняем в соответствии с условиями задания

<br/>

Указываем название сайта, часовой пояс и электронную почту:
<p align="center">
  <img width="400" src="https://github.com/user-attachments/assets/494d4a54-dad8-4e60-adc8-f415671bef4a"
</p>
<p align="center">
  <img width="400" src="https://github.com/user-attachments/assets/eca69476-dedd-4fc6-9198-4c7c27d7a428"
</p>

<br/>

После успешного создания попадаем на главную страницу:
<p align="center">
  <img width="600" src="https://github.com/user-attachments/assets/992d766a-e632-402b-8051-b051bd62c80a"
</p>

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

<br/>
