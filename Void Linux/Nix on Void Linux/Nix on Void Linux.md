Для установки пакета `nix`

```bash
sudo xbps-install -S nix
```

Активируйте службу демона:

```bash
sudo ln -s /etc/sv/nix-daemon /var/service/
```

Добавьте своего пользователя в группу Nix:
*Это нужно, чтобы вы могли устанавливать пакеты без sudo.*

```bash
sudo usermod -aG nixbld $USER
```

Настройте окружение:
*Добавьте инициализацию Nix в ваш конфиг оболочки (например, .bashrc или .zshrc):*

```bash
echo '. /etc/profile.d/nix.sh' >> ~/.bashrc
source ~/.bashrc
```

**Настройка каналов (репозиториев)**

Чтобы Nix знал, откуда качать программы, нужно добавить канал `nixpkgs`.

```bash
nix-channel --add https://nixos.org/channels/nixpkgs-unstable nixpkgs
```

**Обновите каналы:**  
*Теперь Nix загрузит список доступных программ:*

```bash
nix-channel --update
```

Установите Obsidian:

```bash
nix-env -iA nixpkgs.obsidian
```

Если будет ошибка:

Эта ошибка возникает потому, что

> Obsidian имеет проприетарную лицензию («unfree»), а Nix по умолчанию блокирует установку несвободного ПО из соображений безопасности и идеологии.

**Самый быстрый способ (на одну сессию):**

```bash
export NIXPKGS_ALLOW_UNFREE=1
nix-env -iA nixpkgs.obsidian
```

### Правильный способ (навсегда):

Чтобы вам не приходилось вводить это каждый раз при обновлении или установке других программ (например, Discord или Google Chrome), создайте файл конфигурации:

1. **Создайте папку для конфига:**

```bash
mkdir -p ~/.config/nixpkgs
```

2. **Запишите разрешение в файл:**

```bash
echo "{ allowUnfree = true; }" > ~/.config/nixpkgs/config.nix
```

3. **Повторите установку:**

```bash
nix-env -iA nixpkgs.obsidian
```

---
### Как запустить после установки?

После завершения установки попробуйте ввести:

```bash
obsidian
```

Но из меню в `niri` не получается запустить, что-бы это исправить

**Создайте символическую ссылку на `.desktop`-файл**

Fuzzel ищет приложения в стандартных директориях, таких как `~/.local/share/applications`. Nix же хранит их глубоко в своем профиле. Выполните команду:

```bash
mkdir -p ~/.local/share/applications
ln -sf ~/.nix-profile/share/applications/obsidian.desktop ~/.local/share/applications/
```

После этого надо редактировать файл

```bash
nano ~/.local/share/applications/obsidian.desktop
```

Найдите строку `Exec=` и замените её на:

```bash
Exec=/home/xbpsx/.nix-profile/bin/obsidian %U
```

Пример правильного блока:

```bash
[Desktop Entry]
Name=Obsidian
Comment=Obsidian
Exec=/home/xbpsx/.nix-profile/bin/obsidian %U
TryExec=/home/xbpsx/.nix-profile/bin/obsidian
Icon=obsidian
Terminal=false
Type=Application
Categories=Office;
StartupWMClass=obsidian
```

чтобы появилась иконка

Обновите строку `Icon=` в файле, указав полный путь без расширения (или с расширением, если нужно):

```bash
Icon=/home/xbpsx/.nix-profile/share/icons/hicolor/256x256/apps/obsidian
```

Путь для ярлыка находится 

```bash
[xbpsx@voidlinux applications]$ pwd
/home/xbpsx/.local/share/applications
```

Чтобы появилась иконка , надо ее скачать и добавить по пути:

```bash
/home/xbpsx/.local/share/icons
```

и отредактировать файл 

```bash
Icon=/home/xbpsx/.local/share/icons/obsidian-icon.png
```

---
### Обновления пакетов

Обновление «каналов» (списка доступных версий)

Сначала нужно сказать **Nix**, чтобы он проверил наличие новых версий в интернете:

```bash
nix-channel --update
```

_Эта команда загрузит свежие описания пакетов из репозитория nixpkgs._

**Обновление самих пакетов**

После того как каналы обновлены, у вас есть два варианта:

**А) Обновить вообще всё сразу:**

```bash
nix-env -u
```

**Б) Обновить только конкретный пакет (например, Obsidian):**

```bash
nix-env -u obsidian
```

---
### Полезные команды для обслуживания:

- **Посмотреть, что установлено:**  
    Если вы забыли, какие именно пакеты ставили через Nix:

```bash
nix-env -q
```

```bash
[xbpsx@voidlinux ~]$ nix-env -q
obsidian-1.10.6
```


**Очистка старых версий (Мусор):**  
Nix не удаляет старые версии программ сразу после обновления (чтобы можно было откатиться). Со временем это занимает много места. Чтобы удалить старые «поколения» и очистить диск:

```bash
# Удалить старые версии программ
nix-env --delete-generations old

# Полностью очистить неиспользуемые файлы из хранилища /nix/store
nix-collect-garbage -d
```

---
### Как откатиться назад, если обновление что-то сломало?

Если после обновления Obsidian перестал запускаться, вы можете мгновенно вернуться к предыдущему состоянию системы:

```bash
nix-env --rollback
```

> Важно: Если вы устанавливали Obsidian с флагом NIXPKGS_ALLOW_UNFREE=1, то при обновлении через nix-env -u система может снова потребовать разрешение. Если вы уже создали файл ~/.config/nixpkgs/config.nix (как мы делали ранее), то обновление пройдет автоматически без лишних вопросов.







