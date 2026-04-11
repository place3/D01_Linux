# proj DO1_Linux

## Part 1. Просмотр файла /etc/passwd

- ![image.png](img/image.png) — вывод команды `cat /etc/passwd`

## Part 2. Создание пользователя

- ![image.png](img/image%201.png) — добавление нового пользователя
- ![image.png](img/image%202.png) — добавление пользователя в группу
- ![image.png](img/image%203.png) — вывод команды `cat /etc/passwd` с новым пользователем

## Part 3. Настройка сети ОС

- ![image.png](img/image%204.png) — задание имени машины командой `hostnamectl set-hostname`
- ![image.png](img/image%205.png) — установка временной зоны командой `timedatectl set-timezone`
- ![image.png](img/image%206.png) — вывод сетевых интерфейсов командой `ip a`. Интерфейс **lo** (loopback) — виртуальный интерфейс с адресом 127.0.0.1, через который компьютер общается сам с собой без выхода в сеть. Используется для тестирования и локального общения приложений.
- ![image.png](img/image%207.png) — получение IP от DHCP сервера. DHCP (Dynamic Host Configuration Protocol) — протокол автоматической выдачи сетевых настроек.
- ![image.png](img/image%208.png) — получение внутреннего IP шлюза командой `ip route`
- ![image.png](img/image%209.png) — получение внешнего IP шлюза через внешний сервис `curl ifconfig.me`
- ![image.png](img/image%2010.png) — конфигурация статического IP в файле `/etc/netplan/00-installer-config.yaml`
- ![image.png](img/image%2011.png) — применение настроек командой `netplan apply`
- ![image.png](img/image%2012.png) — проверка IP после перезагрузки
- ![image.png](img/image%2013.png) — проверка шлюза после перезагрузки
- ![image.png](img/image%2014.png) — проверка DNS после перезагрузки
- ![image.png](img/image%2015.png) — пинг ya.ru, вывод содержит `0% packet loss`
- ![image.png](img/image%2016.png) — пинг 1.1.1.1, вывод содержит `0% packet loss`

## Part 4. Обновление ОС

- ![image.png](img/image%2017.png) — вывод команды `sudo apt upgrade` после обновления, сообщение об отсутствии новых обновлений

## Part 5. Использование команды sudo

- ![image.png](img/image%2018.png) — выдача прав пользователю diman командой `sudo usermod -aG sudo diman`
- ![image.png](img/image%2019.png) — переключение на пользователя diman и изменение hostname от его имени с использованием sudo
- **sudo** — утилита которая позволяет обычному пользователю выполнять команды с привилегиями суперпользователя (root), не зная его пароля и не входя в систему под ним. Повышает безопасность системы: каждое привилегированное действие требует подтверждения паролем, все действия логируются в `/var/log/auth.log`, а права гибко настраиваются через файл `/etc/sudoers`.

## Part 6. Установка и настройка службы времени

- ![image.png](img/image%2020.png) — включение NTP синхронизации командой `timedatectl set-ntp on` и проверка статуса службы
- ![image.png](img/image%2021.png) — вывод команды `timedatectl show`, содержит `NTPSynchronized=yes`

## Part 7. Установка и использование текстовых редакторов

- ![image.png](img/image%2022.png) — установка редакторов vim, nano, joe

### Создание файлов и сохранение

- ![image.png](img/image%2023.png) — файл test_vim.txt в редакторе vim. Для сохранения и выхода: Esc, затем `:wq` (w — write, q — quit)
- ![image.png](img/image%2024.png) — файл test_nano.txt в редакторе nano. Для сохранения: `Ctrl+O`, Enter. Для выхода: `Ctrl+X`
- ![image.png](img/image%2025.png) — файл test_joe.txt в редакторе joe. Для сохранения и выхода: `Ctrl+K`, затем `X`

### Редактирование без сохранения

- ![image.png](img/image%2026.png) — редактирование в vim без сохранения. Для выхода: Esc, затем `:q!`
- ![image.png](img/image%2027.png) — редактирование в nano без сохранения. Для выхода: `Ctrl+X`, затем `N`
- ![image.png](img/image%2028.png) — редактирование в joe без сохранения. Для выхода: `Ctrl+C`, затем подтвердить отказ

### Поиск и замена

- ![image.png](img/image%2029.png) — поиск в vim: `/искомое_слово`, следующее вхождение — клавиша `n`
- ![image.png](img/image%2030.png) — замена в vim: `:%s/старое/новое/g` (% — весь файл, s — substitute, g — все вхождения)
- ![image.png](img/image%2031.png) — поиск в nano: `Ctrl+W`
- ![image.png](img/image%2032.png) — замена в nano: `Ctrl+\`, ввести заменяемое слово, затем новое, затем `A` для замены всех вхождений
- ![image.png](img/image%2033.png) — поиск в joe: `Ctrl+K`, затем `F`
- ![image.png](img/image%2034.png) — замена в joe: `Ctrl+K`, затем `F`, затем `R`

## Part 8. Установка и базовая настройка сервиса SSHd

- ![image.png](img/image%2035.png) — установка SSHd командой `sudo apt install openssh-server`
- ![image.png](img/image%2036.png) — добавление автостарта командой `sudo systemctl enable ssh`
- ![image.png](img/image%2037.png) — изменение порта на 2022 в файле `/etc/ssh/sshd_config`
- ![image.png](img/image%2038.png) — вывод команды `ps -aux | grep sshd`, подтверждает наличие процесса sshd
  - `ps` — утилита для просмотра запущенных процессов
  - `-a` — процессы всех пользователей
  - `-u` — подробная информация (пользователь, CPU, память)
  - `-x` — процессы без терминала (фоновые службы и демоны)
  - `| grep sshd` — фильтрация строк содержащих sshd
- ![image.png](img/image%2039.png) — вывод команды `netstat -tan`, содержит строку `tcp 0 0 0.0.0.0:2022 0.0.0.0:* LISTEN`
  - `-t` — только TCP соединения
  - `-a` — все соединения включая LISTEN
  - `-n` — адреса и порты цифрами
  - **Proto** — протокол (tcp/udp)
  - **Recv-Q** — байты полученные но не обработанные
  - **Send-Q** — байты отправленные но не подтверждённые
  - **Local Address** — адрес и порт на котором слушает служба
  - **Foreign Address** — адрес удалённого подключения
  - **State** — состояние соединения
  - **0.0.0.0** — все сетевые интерфейсы сервера, SSH принимает подключения на любом IP адресе машины

## Part 9. Установка и использование утилит top и htop

- ![image.png](img/image%2040.png) — установка htop командой `sudo apt install htop`
- ![image.png](img/image%2041.png) — вывод команды `top`
  - uptime: 1:05
  - количество авторизованных пользователей: 1
  - средняя загрузка системы: 0.00, 0.00, 0.00
  - общее количество процессов: 93
  - загрузка CPU: 0.0 us, 0.3 sy, 99.7 id
  - загрузка памяти: total 1971.6, free 1533.9, used 145.3 MiB
  - PID процесса с максимальным потреблением памяти: 655
- ![image.png](img/image%2042.png) — вывод top отсортированный по CPU (Shift+P), PID процесса с максимальным потреблением CPU: 10
- ![image.png](img/image%2043.png) — вывод htop с добавленными метриками Hostname, Clock, Uptime
- ![image.png](img/image%2044.png) — htop отсортированный по PID (F6)
- ![image.png](img/image%2045.png) — htop отсортированный по PERCENT_CPU (F6)
- ![image.png](img/image%2046.png) — htop отсортированный по PERCENT_MEM (F6)
- ![image.png](img/image%2047.png) — htop отсортированный по TIME (F6)
- ![image.png](img/image%2048.png) — htop отфильтрованный по процессу sshd (F4)
- ![image.png](img/image%2049.png) — поиск процесса syslog в htop (F3)

## Part 10. Использование утилиты fdisk

- ![image.png](img/image%2050.png) — вывод команды `sudo fdisk -l`
  - название диска: /dev/sda
  - размер: 25 GiB
  - количество секторов: 52428800
  - размер swap: 2.0 GiB
- ![image.png](img/image%2051.png) — вывод команды `swapon --show`, подтверждает размер swap

## Part 11. Использование утилиты df

- ![image.png](img/image%2052.png) — вывод команды `df`. Единица измерения — килобайты (1K-blocks). Корневой раздел (/):
  - размер: 11758760 KB
  - занятое пространство: 4804324 KB
  - свободное пространство: 6335328 KB
  - процент использования: 44%
- ![image.png](img/image%2053.png) — вывод команды `df -Th`. Корневой раздел (/):
  - размер: 12G
  - занятое пространство: 4.6G
  - свободное пространство: 6.1G
  - процент использования: 44%
  - тип файловой системы: ext4

## Part 12. Использование утилиты du

- ![image.png](img/image%2054.png) — вывод базовой команды `du`
- ![image.png](img/image%2055.png) — размер папки /home в байтах (`sudo du -b /home`)
- ![image.png](img/image%2056.png) — размер папки /var в байтах (`sudo du -b /var`)
- ![image.png](img/image%2057.png) — размер папки /var/log в байтах (`sudo du -b /var/log`)
- ![image.png](img/image%2058.png) — размер папки /home в человекочитаемом виде (`sudo du -sh /home`)
- ![image.png](img/image%2059.png) — размер папки /var в человекочитаемом виде (`sudo du -sh /var`)
- ![image.png](img/image%2060.png) — размер папки /var/log в человекочитаемом виде (`sudo du -sh /var/log`)
- ![image.png](img/image%2061.png) — размер каждого элемента внутри /var/log (`sudo du -h /var/log/*`)

## Part 13. Установка и использование утилиты ncdu

- ![image.png](img/image%2062.png) — установка ncdu командой `sudo apt install ncdu`
- ![image.png](img/image%2063.png) — вывод `ncdu /home`
- ![image.png](img/image%2064.png) — вывод `ncdu /var`
- ![image.png](img/image%2065.png) — вывод `ncdu /var/log`

## Part 14. Работа с системными журналами

- ![image.png](img/image%2066.png) — вывод `/var/log/dmesg` — сообщения ядра: загрузка системы, обнаружение оборудования, драйверы
- ![image.png](img/image%2067.png) — вывод `/var/log/syslog` — все системные события: запуск служб, ошибки, предупреждения
- ![image.png](img/image%2068.png) — поиск последней авторизации командой `sudo grep "LOGIN" /var/log/auth.log`
  - время последней авторизации: Apr 9 22:31:33
  - имя пользователя: place
  - метод входа: login (вход через физическую консоль TTY с вводом пароля)
- ![image.png](img/image%2069.png) — перезапуск SSHd командой `sudo systemctl restart ssh`
- ![image.png](img/image%2070.png) — вывод лога с сообщением о перезапуске службы SSH

## Part 15. Использование планировщика заданий CRON

- ![image.png](img/image%2071.png) — задание в crontab (`crontab -e`): `*/2 * * * * uptime >> /home/place/uptime.log`
  - `*/2` — каждые 2 минуты
  - `uptime` — выполняемая команда
  - `>>` — добавлять вывод в файл без перезаписи
  - `/home/place/uptime.log` — файл куда записывается результат
- ![image.png](img/image%2072.png) — вывод логов о выполнении задания (минимум две строки с интервалом 2 минуты), список текущих заданий командой `crontab -l`
- ![image.png](img/image%2073.png) — список заданий после удаления командой `crontab -r`: задания отсутствуют
