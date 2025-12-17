Для установки на **Void Linux**

```bash
sudo xbps-install -S swaybag
```

Для работы, нужно добавить в автозагрузку системы (**Niri, Hyprland и тд.**)

```bash
#niri
spawn-at-startup "swaybg" "-i" "/home/xbpsx/.wallpapers/2.png" "-m" "fill"
```

