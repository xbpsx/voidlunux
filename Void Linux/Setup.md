Скачиваем образ с `xcfe` и устанавливаем **Void Linux.**

Для начала, давайте посмотрим в каких группах состоит пользователь с помощью `groups` и узнаем, что они значут.

[[groups]]

Какие-то мы включаем сразу, какие-то после установки некоторых служб. Кстати, давате посмотрим, как пользоваться службами, что бы увидеть все службы

```bash
sv status /var/service/*
```

[[service]]

Так же давайте сразу посмотрим, какие пакеты мы установили уже с помощью 

```bash
xbps-query -m
```

и что они значат

[[packages]]

После мы устанвливаем драйвера для **Nvidia**. Для этого нужно включить дополнительный репозиторий

```bash
sudo xbps-install void-repo-nonfree
```

И установить видеодрайвер

```bash
sudo xbps-install nvidia
```

Далее прописываем nvidia в **GRUB**

```bash
sudo nano /etc/default/grub

GRUB_CMDLINE_LINUX_DEFAULT="loglevel=4 nvidia-drm.modeset=1"

# Обновляем
sudo update-grub
```

Настраиваем звук [[pipewire]]
Настраиваем обои [[swaybg]]







