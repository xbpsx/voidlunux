```bash
Установка пакетов:
sudo xbps-install -S pipewire pipewire-devel wireplumber
libpulseaudio pulseaudio-utils alsa-pipewire

Для настройки звука можно использовать pavucontrol wpctl или easyeffects - он фичастей

Копирование конфигов:
sudo mkdir -p /etc/alsa/conf.d
sudo ln -s /usr/share/alsa/alsa.conf.d/50-pipewire.conf /etc/alsa/conf.d
sudo ln -s /usr/share/alsa/alsa.conf.d/99-pipewire-default.conf /etc/alsa/conf.d

В автозапуск:
wireplumber
pipewire-pulse
pipewire

Во избежании тупки всяких вайбаров лучше всего ВМ через скрипт запускать с задержкой.
```


