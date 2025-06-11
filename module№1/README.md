# *Demo2025 - Модуль 1*

### Содержание

1. **[Произведите базовую настройку устройств](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-1)**

2. **[Настройка ISP](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-2)**
  
3. **[Создание локальных учетных записей](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-3)**
  
4. **[Настройте на интерфейсе HQ-RTR в сторону офиса HQ виртуальный коммутатор](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-4)**
   
5. **[Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-5)**
  
6. **[Между офисами HQ и BR необходимо сконфигурировать IP-туннель](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-6)**

7. **[Обеспечьте динамическую маршрутизацию](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-7)**

8. **[Настройка динамической трансляции адресов](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-8)**

9. **[Настройка протокола динамической конфигурации хостов](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-9)**

10. **[Настройка DNS для офисов HQ и BR](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-10)**

11. **[Настройте часовой пояс на всех устройствах, согласно месту проведения экзамена](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-11)**

<br/>

<br/>

<p align="center">
  <img width=auto height=auto src="https://github.com/user-attachments/assets/fa3a32f2-3a63-468d-bb4d-86261bf7f9c8"
<p\>
<p align="center"><strong>Топология сети</strong></p>

<br/>

## Задание 1

### Произведите базовую настройку устройств

- Настройте имена устройств согласно топологии. Используйте полное доменное имя

- На всех устройствах необходимо сконфигурировать IPv4

- IP-адрес должен быть из приватного диапазона, в случае, если сеть локальная, согласно RFC1918

- Локальная сеть в сторону HQ-SRV(VLAN100) должна вмещать не более 64 адресов

- Локальная сеть в сторону HQ-CLI(VLAN200) должна вмещать не более 16 адресов

- Локальная сеть в сторону BR-SRV должна вмещать не более 32 адресов

- Локальная сеть для управления(VLAN999) должна вмещать не более 8 адресов

- Сведения об адресах занесите в отчёт, в качестве примера используйте Таблицу 3

<br/>

<details>
<summary>Решение</summary>
<br/>

### Полное доменное имя можно посмотреть в таблице 2

<br/>

#### Настройка имен устройств на ALTLinux
```yml
hostnamectl set-hostname <name>; exec bash
```

### Пример настройки на HQ-SRV:
![image](https://github.com/user-attachments/assets/be647407-d83c-4565-be03-c4c7efe203b3)

> `<name>` - полное имя устройства
> 
> `exec bash` - обновление оболочки

<br/>

#### Настройка имен устройств на EcoRouter

Переходим в режим конфигурации:
```yml
en
conf t
```
И прописываем следующее:
```yml
hostname <name>
```

### Пример настройки на HQ-RTR:
![image](https://github.com/user-attachments/assets/83a0ba98-b3b3-4b39-a11b-aac1d6af7874)

> `<name>` - полное имя устройства

<table align="center">
  <tr>
    <td align="center">Устройство</td>
    <td align="center">Запись</td>
    <td align="center">Тип</td>
  </tr>
  <tr>
    <td align="center">HQ-RTR</td>
    <td align="center">hq-rtr.au-team.irpo</td>
    <td align="center">A,PTR</td>
  </tr>
  <tr>
    <td align="center">BR-RTR</td>
    <td align="center">br-rtr.au-team.irpo</td>
    <td align="center">A</td>
  </tr>
  <tr>
    <td align="center">HQ-SRV</td>
    <td align="center">hq-srv.au-team.irpo</td>
    <td align="center">A,PTR</td>
  </tr>
  <tr>
    <td align="center">HQ-CLI</td>
    <td align="center">hq-cli.au-team.irpo</td>
    <td align="center">A,PTR</td>
  </tr>
  <tr>
    <td align="center">BR-SRV</td>
    <td align="center">br-srv.au-team.irpo</td>
    <td align="center">A</td>
  </tr>
  <tr>
    <td align="center">HQ-RTR</td>
    <td align="center">moodle.au-team.irpo</td>
    <td align="center">CNAME</td>
  </tr>
  <tr>
    <td align="center">BR-RTR</td>
    <td align="center">wiki.au-team.irpo</td>
    <td align="center">CNAME</td>
  </tr>
</table>

<p align="center"><strong>Таблица 2</strong></p>

<table align="center">
  <tr>
    <td align="center">Имя устройства</td>
    <td align="center">Интерфейс</td>
    <td align="center">IPv4/IPv6</td>
    <td align="center">Маска/Префикс</td>
    <td align="center">Шлюз</td>
  </tr>
  <tr>
    <td align="center" rowspan="3">ISP</td>
    <td align="center">ens18</td>
    <td align="center">От провайдера (DHCP)</td>
    <td align="center"></td>
    <td align="center"></td>
  </tr>
  <tr>
    <td align="center">ens19</td>
    <td align="center">172.16.4.1</td>
    <td align="center">/28</td>
    <td align="center"></td>
  </tr>
  <tr>
    <td align="center">ens20</td>
    <td align="center">172.16.5.1</td>
    <td align="center">/28</td>
    <td align="center"></td>
  </tr>
  <tr>
    <td align="center" rowspan="4">HQ-RTR</td>
    <td align="center">ens18</td>
    <td align="center">172.16.4.2</td>
    <td align="center">/28</td>
    <td align="center" rowspan="4">172.16.4.1</td>
  </tr>
  <tr>
    <td align="center">ens19</td>
    <td align="center">10.0.100.1</td>
    <td align="center">/26</td>
  </tr>
  <tr>
    <td align="center">ens20</td>
    <td align="center">10.0.200.1</td>
    <td align="center">/28</td>
  </tr>
  <tr>
    <td align="center">ens99</td>
    <td align="center">10.0.99.1</td>
    <td align="center">/29</td>
  </tr>
  <tr>
    <td align="center" rowspan="2">BR-RTR</td>
    <td align="center">ens18</td>
    <td align="center">172.16.5.2</td>
    <td align="center">/28</td>
    <td align="center" rowspan="2">172.16.5.1</td>
  </tr>
  <tr>
    <td align="center">ens19</td>
    <td align="center">10.0.0.1</td>
    <td align="center">/27</td>
  </tr>
  <tr>
    <td align="center">HQ-SRV</td>
    <td align="center">ens18</td>
    <td align="center">10.0.100.2</td>
    <td align="center">/26</td>
    <td align="center">10.0.100.1</td>
  </tr>
  <tr>
    <td align="center">BR-SRV</td>
    <td align="center">ens19</td>
    <td align="center">10.0.0.2</td>
    <td align="center">/27</td>
    <td align="center">10.0.0.1</td>
  </tr>
  <tr>
    <td align="center">HQ-CLI</td>
    <td align="center">ens18</td>
    <td align="center">10.0.200.2(DHCP)</td>
    <td align="center">/28</td>
    <td align="center">10.0.200.1(DHCP)</td>
  </tr>
</table>
<p align="center"><strong>Таблица адресации</strong></p>

> Адресация для **ISP** взята из следующего задания

<br/>

#### Наcтройка IP-адресации на **HQ-SRV**, **BR-SRV**, **HQ-CLI** (настройка IP-адресации на **ISP** проводится в [следующем задании](https://github.com/Vafla1/Demo2025A/blob/main/module%E2%84%961/README.md#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-2))

Приводим файлы **`options`**, **`ipv4address`**, **`ipv4route`** в директории **`/etc/net/ifaces/*имя интерфейса*/`** к следующему виду (в примере **HQ-SRV**):
> **`options`**

```yml
BOOTPROTO=static
TYPE=eth
CONFIG_WIRELESS=no
SYSTEMD_BOOTPROTO=static
CONFIG_IPV4=yes
DISABLED=no
NM_CONTROLLED=no
SYSTEMD_CONTROLLED=no
```
### Пример (на HQ-SRV):
![image](https://github.com/user-attachments/assets/266a2619-c68d-4aa3-9819-21ab59b78204)

> **`ipv4address`**
```yml
10.0.100.2/26
```

> **`ipv4route`**
```yml
default via 10.0.100.1
```

<br/>

#### Настройка IP-адресации на EcoRouter

Настраиваем интерфейс на **HQ-RTR**, который смотрит в сторону **ISP**:

- Создаем логический интерфейс:
```yml
interface ens18
  description "to isp"
  ip address 172.16.4.2/28
```
### Пример:
![image](https://github.com/user-attachments/assets/21ef0bd3-bd79-44ec-80da-308fe7b3a79b)

- Настраиваем физический порт и объединеняем с интерфейсом:
```yml
port te0
  service-instance te0/ens18
    encapsulation untagged
    connect ip interface ens18
```
### Пример(неверный service-instance):
![image](https://github.com/user-attachments/assets/6aabeb63-e49b-4c68-9669-a456a4b92a97)

<br/>

Настраиваем интерфейсы на **HQ-RTR**, которые смотрят в сторону **HQ-SRV** и **HQ-CLI** (с разделением на VLAN):

- Создаем три интерфейса:
```yml
interface ens19
  description "to hq-srv"
  ip address 10.0.100.1/26
!
interface ens20
  description "to hq-cli"
  ip address 10.0.200.1/28
!
interface ens99
  description "management"
  ip address 10.0.99.1/28
```

- Настраиваем порт и объединяем с интерфейсами:
```yml
port te1
  service-instance te1/ens19
    encapsulation dot1q 100
    rewrite pop 1
    connect ip interface ens19
  service-instance te1/ens20
    encapsulation dot1q 200
    rewrite pop 1
    connect ip interface ens20
  service-instance te1/ens99
    encapsulation dot1q 999
    rewrite pop 1
    connect ip interface ens99
```
### Пример(неверный service-instance):
![image](https://github.com/user-attachments/assets/77712011-dc75-47cb-8328-b47e02e82bcd)
![image](https://github.com/user-attachments/assets/f2dfbbaa-0538-4c9b-aff6-c2edd3e0802a)
![image](https://github.com/user-attachments/assets/cc5c7fb3-218e-4122-a9fc-92d508dd114f)

<br/>

#### Адресация на BR-RTR (без разделения на VLAN) настраивается аналогично примеру выше

<br/>

#### Добавление маршрута по умолчанию в EcoRouter (на HQ-RTR и на BR-RTR)

Прописываем следующее:
```yml
ip route 0.0.0.0 0.0.0.0 *адрес шлюза*
```
### Пример:
![image](https://github.com/user-attachments/assets/7bae2cc9-426c-4227-a34a-904daf8ec519)
![image](https://github.com/user-attachments/assets/c0f5cdf1-0665-4aa6-8ddb-433612faee4d)

</details>

<br/>

## Задание 2

### Настройка ISP

- Настройте адресацию на интерфейсах:

  - Интерфейс, подключенный к магистральному провайдеру, получает адрес по DHCP

  - Настройте маршруты по умолчанию там, где это необходимо

  - Интерфейс, к которому подключен HQ-RTR, подключен к сети 172.16.4.0/28

  - Интерфейс, к которому подключен BR-RTR, подключен к сети 172.16.5.0/28

  - На ISP настройте динамическую сетевую трансляцию в сторону HQ-RTR и BR-RTR для доступа к сети Интернет

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка интерфейсов, смотрящих в сторону HQ-RTR и BR-RTR происходит аналогично настройке в [Задании 1](https://github.com/damh66/demo2025/tree/main/module1#%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-1)

<br/>

#### Настройка динамической сетевой трансляций в сторону HQ-RTR и BR-RTR для доступа к сети Интернет

Необходимо установить iptables:
```yml
apt-get install iptables
```
Затем настроить его:
```yml
iptables -t nat -A POSTROUTING -o ens18 -j MASQURADE
```
Сохранить и внести в автозапуск
```yml
iptables-save -f /etc/sysconfig/iptables
systemctl enable --now iptables
```

<br/>

В файле **`/etc/net/sysctl.conf`** изменяем строку:
```yml
net.ipv4.ip_forward = 1
```

Изменения в файле **`sysctl.conf`** применяем следующей командой:
```yml
sysctl -p /etc/sysctl.conf
```

</details>

<br/>

## Задание 3

### Создание локальных учетных записей

- Создайте пользователя sshuser на серверах HQ-SRV и BR-SRV

  - Пароль пользователя sshuser с паролем P@ssw0rd

  - Идентификатор пользователя 1010

  - Пользователь sshuser должен иметь возможность запускать sudo без дополнительной аутентификации.

- Создайте пользователя net_admin на маршрутизаторах HQ-RTR и BR-RTR

  - Пароль пользователя net_admin с паролем P@$$word

  - При настройке на EcoRouter пользователь net_admin должен обладать максимальными привилегиями

  - При настройке ОС на базе Linux, запускать sudo без дополнительной аутентификации

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Создание пользователя `sshuser` на серверах

Создаем самого пользователя:
```yml
useradd sshuser -u 1010
```
> опция **`-u`** позволяет указать идентификатор пользователя сразу при создании

Задаем пароль:
```yml
passwd sshuser
```

Добавляем в группу **wheel**:
```yml
usermod -aG wheel sshuser
```

### Пример (на BR-SRV):
![image](https://github.com/user-attachments/assets/bf7e4bab-b5a0-4518-8052-0c8592e4c446)

<br/>

Добавляем строку в **`/etc/sudoers`**:
```yml
sshuser ALL=(ALL) NOPASSWD:ALL
```
> Позволяет запускать **sudo** без аутентификации 

<br/>

#### В режиме конфигураций создаем пользователя `net_admin` на Ecorouter

Создаем самого пользователя:
```yml
username net_admin
```

Задаем пароль:
```yml
password P@ssw0rd
```

Присваиваем привилегии администратора:
```yml
role admin
```
### Пример (на HQ-RTR):
 ![image](https://github.com/user-attachments/assets/2c4fb739-6d69-4a55-95c4-74a2dee462f4)

</details>

<br/>

## Задание 4

### Настройте на интерфейсе HQ-RTR в сторону офиса HQ виртуальный коммутатор

- Сервер HQ-SRV должен находиться в ID VLAN 100
- Клиент HQ-CLI в ID VLAN 200
- Создайте подсеть управления с ID VLAN 999
- Основные сведения о настройке коммутатора и выбора реализации разделения на VLAN занесите в отчёт

<br/>

<details>
<summary>В моем случае виртуальный коммутатор был настроен</summary>
<br/>



</details>

<br/>

## Задание 5

### Настройка безопасного удаленного доступа на серверах HQ-SRV и BR-SRV

- Для подключения используйте порт 2024
- Разрешите подключения только пользователю sshuser
- Ограничьте количество попыток входа до двух
- Настройте баннер «Authorized access only»

<br/>

<details>
<summary>Решение</summary>
<br/>

Приводим указанные строки в файле **`/etc/openssh/sshd_config`** к следующим значениям:
```yml
Port 2024
MaxAuthTries 2
PasswordAuthentication yes
Banner /etc/openssh/bannermotd
AllowUsers  sshuser
```
> В параметре **AllowUsers** вместо пробела используется **`Tab`**

<br/>

Создаем файл **`bannermotd`**:
```yml
----------------------
Authorized access only
----------------------
```

<br/>

Перезагружаем службу:
```yml
systemctl restart sshd
```

</details>

<br/>

## Задание 6

### Между офисами HQ и BR необходимо сконфигурировать IP-туннель

- Сведения о туннеле занесите в отчёт

- На выбор технологии GRE или IP in IP

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Создание туннеля на HQ-RTR

Создаем интерфейс **GRE**-туннеля на **HQ-RTR**:
```yml
int tunnel.0
```

<br/>

Назначаем **IP-адрес**:
```yml
ip add 172.16.0.1/30
```

<br/>

Выставляем параметр **MTU**:
```yml
ip mtu 1400
```
> В связи с добавлением служебного заголовка появляются новые требования к допустимому значению MTU при передаче пакета. Заголовок GRE имеет размерность 4 байта, 20 байт транспортный IP заголовок, заголовок IP пакета 20 байт, таким образом возникает необходимость задавать размер допустимого MTU на интерфейсах туннеля меньше стандартного значения.

<br/>

Задаем режим работы туннеля **GRE** и адреса **начала** и **конца** туннеля:
```yml
ip tunnel 172.16.4.2 172.16.5.2 mode gre
```

<br/>

#### GRE-туннель на BR-RTR настраивается аналогично примеру выше

</details>

<br/>

## Задание 7

### Обеспечьте динамическую маршрутизацию: ресурсы одного офиса должны быть доступны из другого офиса. Для обеспечения динамической маршрутизации используйте link state протокол на ваше усмотрение

- Разрешите выбранный протокол только на интерфейсах в ip туннеле

- Маршрутизаторы должны делиться маршрутами только друг с другом

- Обеспечьте защиту выбранного протокола посредством парольной защиты

- Сведения о настройке и защите протокола занесите в отчёт

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка OSPF на HQ-RTR

Создаем процесс **OSPF**, указываем **идентификатор маршрутизатора**, объявляем сети и указываем **пассивные** интерфейсы:
```yml
router ospf 1
  router-id 1.1.1.1
  network 172.16.0.0/30 area 0
  network 192.168.100.0/26 area 0
  network 192.168.200.0/28 area 0
  passive-interface default
  no passive-interface tunnel.0
```

<br/>

#### Маршрутизация OSPF на BR-RTR настраивается аналогично примеру выше

</details>

<br/>

## Задание 8

### Настройка динамической трансляции адресов

- Настройте динамическую трансляцию адресов для обоих офисов.

- Все устройства в офисах должны иметь доступ к сети Интернет

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка NAT на ISP

Добавляем правила **`iptables`** на ISP
```yml
iptables -t nat -A POSTROUTING -o ens224 -s 172.16.4.0/28 -j MASQUERADE
iptables -t nat -A POSTROUTING -o ens224 -s 172.16.5.0/28 -j MASQUERADE
```

<br/>

Сохраняем правила:
```yml
iptables-save > /etc/sysconfig/iptables
```

<br/>

Включаем и добавляем **`iptables`** в автозагрузку:
```yml
systemctl enable --now iptables
```

<br/>

#### Настройка NAT на HQ-RTR

Указываем **внутренние** и **внешние** интерфейсы:
```yml
int int1
  ip nat inside
!
int int2
  ip nat inside
!
int int0
  ip nat outside
```

<br/>

Создаем пул:
```yml
ip nat pool NAT_POOL 192.168.100.1-192.168.100.62,192.168.200.1-192.168.200.14
```

<br/>

Создаем **правило** трансляции адресов, указывая внешний интерфейс:
```yml
ip nat source dynamic inside-to-outside pool NAT_POOL overload interface int0
```

<br/>

#### Настройка NAT на BR-RTR

Конфигурация:
```yml
int int1
  ip nat inside
!
int int0
  ip nat outside
!
ip nat pool NAT_POOL 192.168.0.1-192.168.0.30
!
ip nat source dynamic inside-to-outside pool NAT_POOL overload interface int0
```

</details>

<br/>

## Задание 9

### Настройка протокола динамической конфигурации хостов

- Настройте нужную подсеть

- Для офиса HQ в качестве сервера DHCP выступает маршрутизатор HQ-RTR.

- Клиентом является машина HQ-CLI.

- Исключите из выдачи адрес маршрутизатора

- Адрес шлюза по умолчанию – адрес маршрутизатора HQ-RTR.

- Адрес DNS-сервера для машины HQ-CLI – адрес сервера HQ-SRV.

- DNS-суффикс для офисов HQ – au-team.irpo

- Сведения о настройке протокола занесите в отчёт

<br/>

<details>
<summary>Решение</summary>
<br/>

Создаем **пул** для **DHCP-сервера**:
```yml
ip pool hq-cli 192.168.200.14-192.168.200.14
```

<br/>

Настраиваем сам **DHCP-сервер**:
```yml
dhcp-server 1
  pool hq-cli 1
    mask 28
    gateway 192.168.200.1
    dns 192.168.100.62
    domain-name au-team.irpo
```
> **`pool hq-cli 1`** - привязка **пула**

> **`mask 28`** - указание **маски** для выдаваемых адресов из пула

> **`gateway 192.168.200.1`** - указание **шлюза по умолчанию** для клиентов

> **`dns 192.168.100.62`** - указание **DNS-сервера** для клиентов

> **`domain-name au-team.irpo`** - указание **DNS-суффикса** для офиса **HQ**

<br/>

Привязываем **DHCP-сервер** к интерфейсу (смотрящий в сторону **CLI**):
```yml
interface int2
  dhcp-server 1
```

</details>

<br/>

## Задание 10

### Настройка DNS для офисов HQ и BR

- Основной DNS-сервер реализован на HQ-SRV.

- Сервер должен обеспечивать разрешение имён в сетевые адреса устройств и обратно в соответствии с таблицей 2

- В качестве DNS сервера пересылки используйте любой общедоступный DNS сервер

<br/>

<table align="center">
  <tr>
    <td align="center">Устройство</td>
    <td align="center">Запись</td>
    <td align="center">Тип</td>
  </tr>
  <tr>
    <td align="center">HQ-RTR</td>
    <td align="center">hq-rtr.au-team.irpo</td>
    <td align="center">A,PTR</td>
  </tr>
  <tr>
    <td align="center">BR-RTR</td>
    <td align="center">br-rtr.au-team.irpo</td>
    <td align="center">A</td>
  </tr>
  <tr>
    <td align="center">HQ-SRV</td>
    <td align="center">hq-srv.au-team.irpo</td>
    <td align="center">A,PTR</td>
  </tr>
  <tr>
    <td align="center">HQ-CLI</td>
    <td align="center">hq-cli.au-team.irpo</td>
    <td align="center">A,PTR</td>
  </tr>
  <tr>
    <td align="center">BR-SRV</td>
    <td align="center">br-srv.au-team.irpo</td>
    <td align="center">A</td>
  </tr>
  <tr>
    <td align="center">HQ-RTR</td>
    <td align="center">moodle.au-team.irpo</td>
    <td align="center">CNAME</td>
  </tr>
  <tr>
    <td align="center">BR-RTR</td>
    <td align="center">wiki.au-team.irpo</td>
    <td align="center">CNAME</td>
  </tr>
</table>

<p align="center"><strong>Таблица 2</strong></p>

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка конфигурации bind

Устанавливаем необходимые пакеты:
```yml
apt-get install -y bind bind-utils
```

<br/>

Изменяем содержание перечисленных строк в **`/etc/bind/options.conf`** к следующему виду:
```yml
listen-on { 127.0.0.1; 192.168.100.62; };

forwarders { 77.88.8.8; };

allow-query { 192.168.100.0/26; 192.168.200.0/28; 192.168.0.0/27; };

```
> **`listen-on`** - сетевые интерфейсы, которые будет прослушивать служба
>
> **`forwarders`** - DNS-сервер, на который будут перенаправляться запросы клиентов
>
> **`allow-query`** - IP-адреса и подсети от которых будут обрабатываться запросы

<br/>

Конфигурируем ключи **rndc**:
```yml
rndc-confgen > /etc/rndckey
```
> Делаем вывод в файл, чтобы скопировать оттуда

<br/>

Приводим файл **`/etc/bind/rndc.key`** к следующему виду:
```yml
//key "rndc-key" {
//  secret "@RNDC_KEY@";
//};

key "rndc-key" {
  algorithm hmac-sha256;
  secret "VTmhjyXFDo0QpaBl3UQWx1e0g9HElS2MiFDtNQzDylo=";
};
```
> Первые строки закомментировали
>
> Вставили ключ **rndc**

<br/>

Проверяем на ошибки:
```yml
named-checkconf
```

<br/>

Запускаем и добавляем в автозагрузку **`bind`**:
```yml
systemctl enable --now bind
```

<br/>

Изменяем **`resolv.conf`** интерфейса:
```yml
search au-team.irpo
nameserver 127.0.0.1
nameserver 192.168.100.62
nameserver 77.88.8.8
search yandex.ru
```

<br/>

#### Создание и настройка прямой зоны

Прописываем ее в **`/etc/bind/local.conf`**:
```yml
zone "au-team.irpo" {
  type master;
  file "au-team.irpo.db";
};
```

<br/>

Копируем шаблон прямой зоны:
```yml
cp /etc/bind/zone/localdomain /etc/bind/zone/au-team.irpo.db
```

<br/>

Задаем пользователя и права на файл:
```yml
chown named. /etc/bind/zone/au-team.irpo.db
chmod 600 /etc/bind/zone/au-team.irpo.db
```

<br/>

Приводим его к следующему виду:
```yml
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; serial
                                12H             ; refresh
                                1H              ; retry
                                1W              ; expire
                                1H              ; ncache
                        )
        IN      NS      au-team.irpo.
        IN      A       192.168.100.62
hq-rtr  IN      A       192.168.100.1
br-rtr  IN      A       192.168.0.1
hq-srv  IN      A       192.168.100.62
hq-cli  IN      A       192.168.200.14
br-srv  IN      A       192.168.0.30
moodle  IN      CNAME   hq-rtr
wiki    IN      CNAME   hq-rtr
```

<br/>

Проверяем на ошибки:
```yml
named-checkconf -z
```

<br/>

#### Создание и настройка обратных зон

Прописываем их в **`/etc/bind/local.conf`**:
```yml
zone "100.168.192.in-addr.arpa" {
  type master;
  file "100.168.192.in-addr.arpa";
};

zone "200.168.192.in-addr.arpa" {
  type master;
  file "200.168.192.in-addr.arpa";
};

zone "0.168.192.in-addr.arpa" {
  type master;
  file "0.168.192.in-addr.arpa";
};
```

<br/>

Копируем шаблон обратной зоны:
```yml
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/100.168.192.in-addr.arpa
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/200.168.192.in-addr.arpa
cp /etc/bind/zone/127.in-addr.arpa /etc/bind/zone/0.168.192.in-addr.arpa
```

<br/>

Задаем пользователя и права на файл:
```yml
chown named. /etc/bind/zone/100.168.192.in-addr.arpa
chmod 600 /etc/bind/zone/100.168.192.in-addr.arpa
chown named. /etc/bind/zone/200.168.192.in-addr.arpa
chmod 600 /etc/bind/zone/200.168.192.in-addr.arpa
chown named. /etc/bind/zone/0.168.192.in-addr.arpa
chmod 600 /etc/bind/zone/0.168.192.in-addr.arpa
```

<br/>

Приводим их к следующему виду:
```yml
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; serial
                                12H             ; refresh
                                1H              ; retry
                                1W              ; expire
                                1H              ; ncache
                        )
        IN      NS      au-team.irpo.
1       IN      PTR     hq-rtr.au-team.irpo.
62      IN      PTR     hq-srv.au-team.irpo.
```
```yml
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; serial
                                12H             ; refresh
                                1H              ; retry
                                1W              ; expire
                                1H              ; ncache
                        )
        IN      NS      au-team.irpo.
14      IN      PTR     hq-cli.au-team.irpo.
```
```yml
$TTL    1D
@       IN      SOA     au-team.irpo. root.au-team.irpo. (
                                2024102200      ; serial
                                12H             ; refresh
                                1H              ; retry
                                1W              ; expire
                                1H              ; ncache
                        )
        IN      NS      au-team.irpo.
1      IN      PTR      br-rtr.au-team.irpo.
30     IN      PTR      br-srv.au-team.irpo.
```

<br/>

Проверяем на ошибки:
```yml
named-checkconf -z
```

<br/>

Перезапускаем **`bind`**:
```yml
systemctl restart bind
```

<br/>

Проверяем работоспособность:
```yml
nslookup **IP-адрес/DNS-имя**
```

</details>

<br/>

## Задание 11

### Настройте часовой пояс на всех устройствах, согласно месту проведения экзамена

<br/>

<details>
<summary>Решение</summary>
<br/>

#### Настройка часового пояса на Alt Linux

Меняем часовой пояс следующей командой:
```yml
timedatectl set-timezone Asia/Yekaterinburg
```

<br/>

Проверяем:
```yml
timedatectl status
```

<br/>

#### Настройка часового пояса на EcoRouter

Прописываем команду:
```yml
ntp timezone utc+5
```

<br/>

Проверяем:
```yml
show ntp timezone
```

</details>
