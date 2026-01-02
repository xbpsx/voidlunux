```bash
sv status /var/service/*

run: /var/service/NetworkManager: (pid 734) 4018s; run: log: (pid 727) 4018s
run: /var/service/agetty-tty1: (pid 738) 4018s
run: /var/service/agetty-tty2: (pid 721) 4018s
run: /var/service/agetty-tty3: (pid 720) 4018s
run: /var/service/agetty-tty4: (pid 737) 4018s
run: /var/service/agetty-tty5: (pid 722) 4018s
run: /var/service/agetty-tty6: (pid 733) 4018s
run: /var/service/bluetoothd: (pid 732) 4018s; run: log: (pid 725) 4018s
run: /var/service/chronyd: (pid 731) 4018s; run: log: (pid 726) 4018s
run: /var/service/dbus: (pid 742) 4018s; run: log: (pid 740) 4018s
run: /var/service/dhcpcd: (pid 743) 4018s; run: log: (pid 741) 4018s
down: /var/service/dhcpcd-eth0: 0s, normally up, want up; run: log: (pid 724) 4018s
run: /var/service/elogind: (pid 736) 4018s; run: log: (pid 729) 4018s
run: /var/service/seatd: (pid 728) 4018s; run: log: (pid 723) 4018s
run: /var/service/udevd: (pid 739) 4018s; run: log: (pid 735) 4018s
```

Давайте разберем каждую из них

**`NetworkManager`** - управление сетью. Управление проводными и беспроводными соединениями, VPN, мобильный широкополосный доступ.

```bash
# Установка
sudo xbps-install NetworkManager
# Включаем службу
sudo ln -s /etc/sv/NetworkManager /var/service/
# Запустить утилиту
sudo nmtui
```

**`agetty-tty[1-6]`** - виртуальные консоли. Входит в util-linux (уже в базовой системе). 

**`bluetoothd`** - Bluetooth. Управление Bluetooth-устройствами.

```bash
# Установка
sudo xbps-install bluez blueman
# Включаем службу
sudo ln -s /etc/sv/bluetoothd /var/service/
# Запустить утилиту, 1 в автозагрузку
blueman-applet & blueman-manager
```

**`chronyd`** - синхронизация времени. Точная синхронизация системного времени через NTP.

```bash
# Установка
sudo xbps-install chrony
# Включаем службу
sudo ln -s /etc/sv/chronyd /var/service/
```

**`dbus`** - система межпроцессного взаимодействия. Система обмена сообщениями между приложениями (необходима для многих служб).

```bash
# Установка
sudo xbps-install dbus
# Включаем службу
sudo ln -s /etc/sv/dbsus /var/service/
```

**`dhcpcd`** - DHCP клиент. Получение IP-адреса по DHCP (базовый клиент). При установки можно выбрать. У вас есть `dhcpcd-eth0` в состоянии `down` - это, вероятно, дополнительный экземпляр для конкретного интерфейса.

**`elogind`** - управление сеансами входа. Управление пользовательскими сеансами, блокировка экрана, приостановка системы (альтернатива systemd-logind).

```bash
# Установка
sudo xbps-install elogind
# Включаем службу
sudo ln -s /etc/sv/elogind /var/service/
```

**`seatd`** - управление графическими сеансами. Управление доступом к графическим устройствам для `Wayland`-композиторов.

```bash
# Установка
sudo xbps-install seatd
# Включаем службу
sudo ln -s /etc/sv/seatd /var/service/
# Добавляем в группу 
sudo usermod -aG _seatd $USER
```

**`udevd`** - управление устройствами ядра. Динамическое создание/удаление файлов устройств в `/dev`, загрузка прошивок.














