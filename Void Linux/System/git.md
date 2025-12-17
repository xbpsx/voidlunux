### **Установка Git**

Если Git не установлен, выполните в терминале:

```bash
sudo xbps-install -S git
```

### **Настройка Git**

Укажите ваше имя и email (используются для коммитов):

```bash
git config --global user.name "Ваше Имя"
git config --global user.email "ваш_email@example.com"
```

Проверьте настройки:

```bash
git config --list
```

### **Создание SSH-ключа**

Для безопасного подключения к GitHub создайте SSH-ключ:

```bash
ssh-keygen -t ed25519 -C "ваш_email@example.com"
```

- Нажмите `Enter` для сохранения ключа в стандартной папке (`~/.ssh/`).

- По желанию установите пароль (рекомендуется).

### **Добавление SSH-ключа в GitHub**

1. Скопируйте публичный ключ:

```   bash
cat ~/.ssh/id_ed25519.pub
```

- Войдите в GitHub → **Settings** → **SSH and GPG keys** → **New SSH Key**.

- Вставьте ключ в поле `Key` и сохраните.

### **Проверка подключения**

Выполните в терминале:

```bash
ssh -T git@github.com
```

Если видите приветствие с вашим именем на GitHub — ключ работает.

