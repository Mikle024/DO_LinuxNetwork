# Linux_D02:

----------------------------------------------------------------------------

- [Linux\_D02:](#linux_d02)
    - [1. Инструмент ipcalc:](#1-инструмент-ipcalc)
    - [2. Статическая маршрутизация между двумя машинами:](#2-статическая-маршрутизация-между-двумя-машинами)
    - [3. Утилита iperf3:](#3-утилита-iperf3)
    - [4. Сетевой экран:](#4-сетевой-экран)
    - [5. Статическая маршрутизация сети:](#5-статическая-маршрутизация-сети)
    - [6. Динамическая настройка IP с помощью DHCP:](#6-динамическая-настройка-ip-с-помощью-dhcp)
    - [7. NAT:](#7-nat)
    - [8. Знакомство с SSH Tunnels:](#8-знакомство-с-ssh-tunnels)

----------------------------------------------------------------------------

## 1. Инструмент ipcalc:
- Выполнил команду от имени администратора `sudo` `apt install ipcalc`, что бы скачать утилиту ipcalc.
- Подтвердил действие паролем администратора.

> Установка ipcalc
>
> ![Установка ipcalc](screen%2Fscreen_1_01.png)
>

**1.1 Сети и маски:**
- Выполнил команду `ipcalc 192.167.38.54/13`.

> Вывод команды ipcalc 192.167.38.54/13
>
> ![Вывод команды ipcalc 192.167.38.54/13](screen%2Fscreen_1_02.png)
>

- 192.167.38.54/13:
  - Адрес сети: 192.160.0.0


- Выполнил команду `ipcalc 255.255.255.0`.

> Вывод команды ipcalc 255.255.255.0
>
> ![Вывод команды ipcalc 255.255.255.0](screen%2Fscreen_1_03.png)
>

- 255.255.255.0:
  - Префиксная запись: /24
  - Двоичная запись: 11111111.11111111.11111111.00000000


- Выполнил команду `ipcalc 0.0.0.0/15`.

> Вывод команды ipcalc 0.0.0.0/15
>
> ![Вывод команды ipcalc 0.0.0.0/15](screen%2Fscreen_1_04.png)
>

- 255.255.255.0:
  - Обычная запись: 255.254.0.0
  - Двоичная запись: 11111111.11111110.00000000.00000000


- Маска 11111111.11111111.11111111.11110000 содержит 28 единиц, поэтому префиксная запись выглядит как /28.
- Выполнил команду `ipcalc 0.0.0.0/28`.

> Вывод команды ipcalc 0.0.0.0/28
>
> ![Вывод команды ipcalc 0.0.0.0/28](screen%2Fscreen_1_05.png)
>

- 11111111.11111111.11111111.11110000:
  - Префиксная запись: /28
  - Обычная запись: 255.255.255.240


- Выполнил команду `ipcalc 12.167.38.4/8`.

> Вывод команды ipcalc 12.167.38.4/8
>
> ![Вывод команды ipcalc 12.167.38.4/8](screen%2Fscreen_1_06.png)
>

- Сеть 12.167.38.4 с маской /8:
  - Минимальный хост: 12.0.0.1
  - Максимальный хост: 12.255.255.254


- Маска 11111111.11111111.00000000.00000000 содержит 16 единиц, поэтому префиксная запись выглядит как /16.
- Выполнил команду `ipcalc 12.167.38.4/16`.

> Вывод команды ipcalc 0.0.0.0/16
>
> ![Вывод команды ipcalc 0.0.0.0/16](screen%2Fscreen_1_07.png)
>

- Сеть 12.167.38.4 с маской /16:
  - Минимальный хост: 12.167.0.1
  - Максимальный хост: 12.167.255.254


- Выполнил команду `ipcalc 12.167.38.4/255.255.254.0`.

> Вывод команды ipcalc 0.0.0.0/255.255.254.0
>
> ![Вывод команды ipcalc 0.0.0.0/255.255.254.0](screen%2Fscreen_1_08.png)
>

- Сеть 12.167.38.4 с маской /255.255.254.0:
  - Минимальный хост: 12.167.38.1
  - Максимальный хост: 12.167.39.254


- Выполнил команду `ipcalc 12.167.38.4/4`.

> Вывод команды ipcalc 0.0.0.0/4
>
> ![Вывод команды ipcalc 0.0.0.0/4](screen%2Fscreen_1_09.png)
>

- Сеть 12.167.38.4 с маской 4:
  - Минимальный хост: 0.0.0.1
  - Максимальный хост: 15.255.255.254

**1.2. localhost:**

*Диапазон адресов 127.0.0.0/8 называется диапазоном адресов внутреннего хоста (Internal host loopback). IPv4-адреса такой формы используются для обращения к самому хосту. Если вы запросите любой из этих адресов на любом сетевом устройстве, вы должны получить ответ.*

- Выполнил команду `ipcalc 127.0.0.0/8`.

> Вывод команды ipcalc 127.0.0.0/8
>
> ![Вывод команды ipcalc 127.0.0.0/8](screen%2Fscreen_1_10.png)
>

- Диапазон 127.0.0.0/8:
  - Минимальный хост: 127.0.0.1
  - Максимальный хост: 127.255.255.254

| Адрес | Диапазон                          | Приложение на localhost  с данным ip                    |
| -------- |-----------------------------------|---------------------------------------------------------|
| 194.34.23.100:    | Адрес не в диапазоне 127.0.0.0/8. | Нельзя обратиться к приложению на localhost с этого IP. |
| 127.0.0.2:     | Адрес из диапазона 127.0.0.0/8.   | Можно обратиться к приложению на localhost с этого IP.  |
| 127.1.0.1:    | Адрес из диапазона 127.0.0.0/8.   | Можно обратиться к приложению на localhost с этого IP.  |
| 128.0.0.1:    | Адрес не в диапазоне 127.0.0.0/8. | Нельзя обратиться к приложению на localhost с этого IP. |

----------------------------------------------------------------------------

## 2. Статическая маршрутизация между двумя машинами:

----------------------------------------------------------------------------

## 3. Утилита iperf3:

----------------------------------------------------------------------------

## 4. Сетевой экран:

----------------------------------------------------------------------------

## 5. Статическая маршрутизация сети:

----------------------------------------------------------------------------

## 6. Динамическая настройка IP с помощью DHCP:

----------------------------------------------------------------------------

## 7. NAT:

----------------------------------------------------------------------------

## 8. Знакомство с SSH Tunnels:

----------------------------------------------------------------------------