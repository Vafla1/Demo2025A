![image](https://github.com/user-attachments/assets/c213ab0a-f7f1-4d3c-ad3e-9052cca12148)![image](https://github.com/user-attachments/assets/1d8af385-cf05-40f9-b784-125fcc45c61e)# *Demo2025 - Модуль 1*

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

#### Полное доменное имя можно посмотреть в таблице 2

<br/>

#### Настройка имен устройств на ALTLinux
```yml
hostnamectl set-hostname <name>; exec bash
```

#### Пример настройки на HQ-SRV:
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
ip domain-name au-team.irpo
```

#### Пример настройки на HQ-RTR:
![image](https://github.com/user-attachments/assets/acc01573-1cb2-4e6b-b0d9-35637146e347)

> `<name>` - неполное имя устройства

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
    <td align="center">ToISP</td>
    <td align="center">172.16.4.2</td>
    <td align="center">/28</td>
    <td align="center" rowspan="4">172.16.4.1</td>
  </tr>
  <tr>
    <td align="center">ToHqSRV</td>
    <td align="center">10.0.100.1</td>
    <td align="center">/26</td>
  </tr>
  <tr>
    <td align="center">ToHqCLI</td>
    <td align="center">10.0.200.1</td>
    <td align="center">/28</td>
  </tr>
  <tr>
    <td align="center">Managment</td>
    <td align="center">10.0.99.1</td>
    <td align="center">/29</td>
  </tr>
  <tr>
    <td align="center" rowspan="2">BR-RTR</td>
    <td align="center">ToISP</td>
    <td align="center">172.16.5.2</td>
    <td align="center">/28</td>
    <td align="center" rowspan="2">172.16.5.1</td>
  </tr>
  <tr>
    <td align="center">ToBrSRV</td>
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
#### Пример (на HQ-SRV):
![image](https://github.com/user-attachments/assets/266a2619-c68d-4aa3-9819-21ab59b78204)

> **`ipv4address`**
```yml
10.0.100.2/26
```
![image](https://github.com/user-attachments/assets/f7996d25-dc69-4526-a14f-71451a4ba614)

> **`ipv4route`**
```yml
default via 10.0.100.1
```
![image](https://github.com/user-attachments/assets/04195ac8-c671-4cee-818d-9aa35f63ed61)

Необходимо перезагрузить службу
```yml
systemctl restart network
```
<br/>

#### Настройка IP-адресации на EcoRouter

Настраиваем интерфейс на **HQ-RTR**, который смотрит в сторону **ISP**:

- Создаем логический интерфейс:
```yml
interface ToISP
  description "to isp"
  ip address 172.16.4.2/28
```
#### Пример:
![image](https://github.com/user-attachments/assets/a40e027d-3948-4fdc-8e93-089ca2ba1399)

- Настраиваем физический порт и объединеняем с интерфейсом:
```yml
port te0
  service-instance te0/ToISP
    encapsulation untagged
    connect ip interface ToISP
```
#### Пример:
![image](https://github.com/user-attachments/assets/da29e355-e38a-40d7-b196-48b9a46d86e1)

<br/>

Настраиваем интерфейсы на **HQ-RTR**, которые смотрят в сторону **HQ-SRV** и **HQ-CLI** (с разделением на VLAN):

- Создаем три интерфейса:
```yml
interface ToHqSRV
  description "to hq-srv"
  ip address 10.0.100.1/26
!
interface ToHqCLI
  description "to hq-cli"
  ip address 10.0.200.1/28
!
interface Managment
  description "management"
  ip address 10.0.99.1/28
```
#### Пример:
![image](https://github.com/user-attachments/assets/5e9909d1-832c-42e2-bc8f-7c132457fb93)

- Настраиваем порт и объединяем с интерфейсами:
```yml
port te1
  service-instance te1/ToHqSRV
    encapsulation dot1q 100
    rewrite pop 1
    connect ip interface ToHqSRV
  service-instance te1/ToHqCLI
    encapsulation dot1q 200
    rewrite pop 1
    connect ip interface ToHqCLI
  service-instance te1/Managment
    encapsulation dot1q 999
    rewrite pop 1
    connect ip interface Managment
```
#### Пример:
![image](https://github.com/user-attachments/assets/412a544f-71e2-4a47-be72-160c8d3a7954)

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
iptables -t nat -A POSTROUTING -o ens18 -j MASQUERADE
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

#### Пример (на HQ-SRV):
![image](https://github.com/user-attachments/assets/44e2294a-7fae-4e5b-8b84-3c6fb0dedcf1)

![image](https://github.com/user-attachments/assets/a775d23e-aa49-47ab-8e4e-deaffa702690)

<br/>

Добавляем строку в **`/etc/sudoers`**:
```yml
sshuser ALL=(ALL) NOPASSWD:ALL
```
#### Пример (на HQ-SRV):
![image](https://github.com/user-attachments/assets/d9f088ab-098e-4677-8cf6-2ed2a7002ce8)

> Позволяет запускать **sudo** без аутентификации 

<br/>

#### В режиме конфигураций создаем пользователя `net_admin` на Ecorouter

Создаем самого пользователя:
```yml
username net_admin
```

Задаем пароль:
```yml
password P@$$word
```

Присваиваем привилегии администратора:
```yml
role admin
```
### Пример (на HQ-RTR):
![image](https://github.com/user-attachments/assets/766eb9ff-b9b6-4608-aa1a-bb2a1d971bc6)

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
<summary>Выполняется автоматический</summary>
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
Banner /etc/openssh/banner
AllowUsers  sshuser
```
#### Пример (на HQ-SRV):
![image](https://github.com/user-attachments/assets/f13552a5-8be8-4b32-a658-68f7a025f402)

> В параметре **AllowUsers** вместо пробела используется **`Tab`**

<br/>

Создаем файл **`banner`**:
```yml
----------------------
Authorized access only
----------------------
```
#### Пример (на HQ-SRV):
![image](https://github.com/user-attachments/assets/92f893b8-1de5-4e63-8afb-f63b61f38442)

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
des
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

#### Пример (на HQ-RTR):
![image](https://github.com/user-attachments/assets/8d27409b-828d-4aae-b7d9-939c5be99f43)

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
  router-id 10.10.10.1
  passive-interface default
  no passive-interface tunnel.0
  network 10.10.10.0/30 area 0
  network 10.0.100.0/26 area 0
  network 10.0.200.0/28 area 0
  network 10.0.99.0/29 area 0
```

Создание парольной защиты для **OSPF**:
```yml
int tunnel.0
ip ospf authentication message-digest
ip ospf message-digest-key 1 md5 ecorouter
```
#### Пример:
![image](https://github.com/user-attachments/assets/2479ce46-b8e7-4917-a4d1-1ffa9fe3d585)

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

#### Настройка NAT на HQ-RTR

Указываем **внутренние** и **внешние** интерфейсы:
```yml
int ToISP
  ip nat outside
!
int ToHqSRV
  ip nat inside
!
int ToHqCLI
  ip nat inside
```

#### Пример:
![image](https://github.com/user-attachments/assets/66a213d3-0651-49af-8faa-62b9eafbabd5)

<br/>

Создаем пул:
```yml
ip nat pool NAT_POOL 192.168.100.1-192.168.100.62,192.168.200.1-192.168.200.14
```

#### Пример:
![image](https://github.com/user-attachments/assets/dd763ea1-731e-4a8e-b4d3-620cf25ce01d)

<br/>

Создаем **правило** трансляции адресов, указывая внешний интерфейс:
```yml
ip nat source dynamic inside-to-outside pool NAT_POOL overload interface ToISP
```

#### Пример:
![image](https://github.com/user-attachments/assets/687ebd11-e29c-40d4-a560-7db9598df5c5)

<br/>

#### Настройка NAT на BR-RTR

Конфигурация:
```yml
int ToISP
  ip nat outside
!
int ToBrSRV
  ip nat inside
!
ip nat pool BR 10.0.0.1-10.0.0.30
!
ip nat source dynamic inside-to-outside pool BR overload interface ToISP
```

#### Пример:
![image](https://github.com/user-attachments/assets/be3d6c0f-d983-4f14-8d38-5cdb03ba061b)

![image](https://github.com/user-attachments/assets/068c2418-221b-4b19-a582-f143b0790723)

![image](https://github.com/user-attachments/assets/64fe0bec-ff97-4ed5-8602-bd1b1b3b07e4)

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
ip pool HQ 10.0.200.2-10.0.200.62
```

<br/>

Настраиваем сам **DHCP-сервер**:
```yml
dhcp-server 1
  pool HQ 1
    mask 28
    gateway 10.0.200.1
    dns 10.0.100.2
    domain-name au-team.irpo
```
> **`pool HQ 1`** - привязка **пула**

> **`mask 28`** - указание **маски** для выдаваемых адресов из пула

> **`gateway 10.0.200.1`** - указание **шлюза по умолчанию** для клиентов

> **`dns 10.0.100.2`** - указание **DNS-сервера** для клиентов

> **`domain-name au-team.irpo`** - указание **DNS-суффикса** для офиса **HQ**

<br/>

Привязываем **DHCP-сервер** к интерфейсу (смотрящий в сторону **CLI**):
```yml
interface ToHqCLI
  dhcp-server 1
```

#### Пример:
![image](https://github.com/user-attachments/assets/ebdd3bfb-c40b-44a5-ba96-0b6199ea5812)

#### Для работы HQ-CLI нужно настроить на его интерфейсе DHCP

Удалить старый:
```yml
su -
nmcli connection delete System\ ens18
```

#### Пример:
![image](https://github.com/user-attachments/assets/10a96309-80ee-4db9-b8d9-12992fbdc744)

![image](https://github.com/user-attachments/assets/5e4bc06f-88db-4f73-854b-9573b5ec9058)

И настроить новый через граф.интерфейс:

![image](https://github.com/user-attachments/assets/d676154c-458b-42d2-9740-5a4be82cbf8d)

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
listen-on { 127.0.0.1; 10.0.100.2; };

forwarders { 8.8.8.8; };

allow-query { 127.0.0.1; 10.0.100.0/26; 10.0.200.0/28; 10.0.99.0/29; 10.0.0.0/27; };

allow-recursion { 10.0.100.0/26; 10.0.200.0/28; 10.0.99.0/29; 10.0.0.0/27; };
```
> **`listen-on`** - сетевые интерфейсы, которые будет прослушивать служба
>
> **`forwarders`** - DNS-сервер, на который будут перенаправляться запросы клиентов
>
> **`allow-query`** - IP-адреса и подсети от которых будут обрабатываться запросы
> 
> **`allow-recursion`** — это параметр в конфигурационном файле DNS-сервера, который указывает, каким клиентам можно посылать рекурсивные запросы. 
<br/>

Изменяем **`resolv.conf`** на интерфейсе:
```yml
search au-team.irpo
nameserver 127.0.0.1
```

<br/>

Изменяем **`resolv.conf`** всех интерфейсов на всех устройствах кромен ISP и HQ-CLI и HQ-SRV:
```yml
search au-team.irpo
nameserver 10.0.100.2
```

<br/>

#### Создание и настройка прямой зоны

Прописываем ее в **`/etc/bind/local.conf`**:
```yml
zone "au-team.irpo" {
  type master;
  file "au-team.irpo";
};
```

<br/>

Задаем пользователя и права на файл:
```yml
chown root:named /etc/bind/zone/au-team.irpo
```

<br/>

Копируем шаблон прямой зоны:
```yml
cp /etc/bind/zone/empty /etc/bind/zone/au-team.irpo
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
        IN      A       10.0.100.2
hq-srv          A       10.0.100.2
hq-cli          A       10.0.200.2
br-srv          A       10.0.0.2
hq-rtr          A       10.0.100.1
br-rtr          A       10.0.0.1
moodle          CNAME   hq-rtr
wiki            CNAME   hq-rtr
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
zone "0.10.in-addr.arpa" {
  type master;
  file "0.10.in-addr.arpa";
};
```

<br/>

Копируем прямую зону для обратной зоны:
```yml
cp /etc/bind/zone/au-team.irpo /etc/bind/zone/0.10.in-addr.arpa
```

<br/>

Задаем пользователя и права на файл:
```yml
chown root:named /etc/bind/zone/0.10.in-addr.arpa
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
100.2           PTR     hq-srv.au-team.irpo.
200.2           PTR     hq-cli.au-team.irpo.
100.1           PTR     hq-rtr.au-team.irpo

<br/>

Проверяем на ошибки:
```yml
named-checkconf -z
```

<br/>

Запускаем и добавляем в автозагрузку **`bind`**:
```yml
systemctl enable --now bind
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
