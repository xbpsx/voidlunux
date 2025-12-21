посмотреть самое большое количество в `/home`

```bash
du -ah /home | sort -rh | head -n 10
```

чтобы удалить вручную из папки `trash`

```bash
rm -rf /home/xbpsx/.local/share/Trash/files/*
rm -rf /home/xbpsx/.local/share/Trash/info/*
```

