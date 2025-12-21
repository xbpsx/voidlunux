посмотреть самое большое количество в `/home`

```bash
du -ah /home | sort -rh | head -n 10
```

чтобы удалить вручную из папки `trash`

```bash
rm -rf /home/xbpsx/.local/share/Trash/files/*
rm -rf /home/xbpsx/.local/share/Trash/info/*
```

Чтобы в будущем не искать эти папки, установите маленькую утилиту, которая управляет корзиной из терминала правильно:

```bash
sudo xbps-install -S trash-cli
```

Теперь вы сможете просто писать `trash-empty` для полной очистки или `trash-list`, чтобы увидеть список файлов.