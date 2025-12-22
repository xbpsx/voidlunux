Поскольку VSCode не является полностью свободным ПО, Nix заблокирует его установку по умолчанию. Вам нужно разрешить «unfree» пакеты одним из способов:

**Постоянная настройка:**  
Создайте или отредактируйте файл `~/.config/nixpkgs/config.nix` и добавьте туда следующее:

```nix
{ allowUnfree = true; }
```

**Установка через Nix**

В зависимости от того, какую версию Nix вы используете («классическую» или новую с flakes), выполните команду:

- **Классический вариант (nix-env):**

```bash
nix-channel --update
nix-env -iA nixpkgs.vscode
```

Если вы не хотите менять переменные окружения, можно просто «пробросить» ссылку на папку с ярлыками Nix в стандартную директорию пользователя.

```bash
mkdir -p ~/.local/share/applications
```

Создайте симлинк:

```bash
ln -s ~/.nix-profile/share/applications/code.desktop ~/.local/share/applications/code.desktop
```

Это подтверждает, что ваша оболочка (shell) просто не знает, где искать программы, установленные через Nix. В Void Linux при установке Nix пути в

`$PATH` не всегда добавляются автоматически для всех сессий.

Постоянная настройка (чтобы работало всегда и в fuzzel)

Чтобы пути Nix подгружались автоматически при каждом входе в систему, добавьте настройки в ваш .bashrc (или .zshrc, если используете zsh):

```bash
nano ~/.bashrc
```

```bash
# Подключение путей Nix
if [ -e ~/.nix-profile/etc/profile.d/nix.sh ]; then
  . ~/.nix-profile/etc/profile.d/nix.sh
fi
```

Добавьте Nix в PATH для **Fish**

Добавьте путь к бинарникам Nix в конфигурацию fish. Выполните в терминале:

```bash
set -Ux fish_user_paths $HOME/.nix-profile/bin $fish_user_paths
```

_Эта команда добавит путь в «универсальные переменные», и он будет сохраняться даже после перезагрузки_

**Подключите переменные окружения Nix**

Nix требуется больше, чем просто PATH (например, для работы иконок и библиотек). Поскольку стандартный скрипт `nix.sh` в fish не сработает, добавьте в ваш конфигурационный файл `~/.config/fish/config.fish` (создайте папку и файл, если их нет) следующее:

- Откройте конфиг: `nano ~/.config/fish/config.fish`
- Вставьте туда:

```bash
if test -e ~/.nix-profile/etc/profile.d/nix.sh
    # Используем встроенную функцию fish для выполнения bash-скриптов
    # Если плагин не установлен, просто добавим основные пути
    set -gx NIX_PATH $HOME/.nix-defexpr/channels
    set -gx XDG_DATA_DIRS $HOME/.nix-profile/share $XDG_DATA_DIRS
end
```

**Настройка Desktop-файла для Fuzzel**

Чтобы **Fuzzel** запускал VSCode правильно в среде Wayland (Niri), отредактируйте ваш `.desktop` файл:

```bash
nano ~/.local/share/applications/code.desktop
```

```bash
Exec=/home/ВАШ_ЛОГИН/.nix-profile/bin/code --ozone-platform-hint=auto --unity-launch %F
```

```bash
# Иконки лежат
.local/share/applications/icons
```

