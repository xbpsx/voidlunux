Установка 

```bash
sudo xbps-install fish-shell starship
```

Установка fish как оболочки по умолчанию

```bash
chsh -s /usr/bin/fish
fish
curl -sL https://git.io/fisher | source && fisher install jorgebucaran/fisher
fisher install jorgebucaran/nvm.fish
```

`starship.toml`

```toml
# Отключаем пустую строку в начале
add_newline = true

# Настройка формата:
# [ закругление ][ Логотип + Ник ][ закругление ] [ путь ]
format = """
[](#b4befe)\
[ void ](bg:#b4befe fg:#1e1e2e)\
[](#b4befe) \
$directory\
$git_branch\
$git_status\
$character"""

[directory]
style = "bold #89b4fa"
format = "[$path ]($style)"
truncation_length = 3

[character]
success_symbol = "[❯](bold #b4befe)"
error_symbol = "[❯](bold #f38ba8)"

[git_branch]
symbol = " "
style = "bold #f5c2e7"

[git_status]
style = "bold #f38ba8"
```

`config.fish`

```fish
  GNU nano 8.6                                                     config.fish                                                               
if status is-interactive
    # Отключаем стандартное приветствие
    set -g fish_greeting ""

    # Инициализация Starship
    starship init fish | source

    # Функция Transience (сокращение промпта после нажатия Enter)
    function starship_transient_prompt_func
      echo -n (set_color b4befe)"xbpsx "(set_color normal)"> "
    end
end
```

`fish_variables`

```bash
# This file contains fish universal variable definitions.
# VERSION: 3.0
SETUVAR VIRTUAL_ENV_DISABLE_PROMPT:true
SETUVAR __fish_initialized:3800
SETUVAR _fisher_jorgebucaran_2F_fisher_files:\x7e/\x2econfig/fish/functions/fisher\x2efish\x1e\x7e/\x2econfig/fish/completions/fisher\x2efish
SETUVAR _fisher_jorgebucaran_2F_nvm_2E_fish_files:\x7e/\x2econfig/fish/functions/_nvm_index_update\x2efish\x1e\x7e/\x2econfig/fish/functions>
SETUVAR _fisher_plugins:jorgebucaran/fisher\x1ejorgebucaran/nvm\x2efish
SETUVAR _fisher_upgraded_to_4_4:\x1d
SETUVAR fish_color_autosuggestion:585b70
SETUVAR fish_color_cancel:f38ba8
SETUVAR fish_color_command:b4befe
SETUVAR fish_color_comment:7f849c
SETUVAR fish_color_cwd:f9e2af
SETUVAR fish_color_cwd_root:red
SETUVAR fish_color_end:fab387
SETUVAR fish_color_error:f38ba8
SETUVAR fish_color_escape:f5c2e7
SETUVAR fish_color_history_current:\x2d\x2dbold
SETUVAR fish_color_host:b4befe
SETUVAR fish_color_host_remote:yellow
SETUVAR fish_color_keyword:f38ba8
SETUVAR fish_color_normal:cdd6f4
SETUVAR fish_color_operator:f5c2e7
SETUVAR fish_color_param:89b4fa
SETUVAR fish_color_quote:a6e3a1
SETUVAR fish_color_redirection:fab387
SETUVAR fish_color_search_match:\x2d\x2dbackground\x3d313244
SETUVAR fish_color_selection:\x2d\x2dbackground\x3d313244
SETUVAR fish_color_status:red
SETUVAR fish_color_user:b4befe
SETUVAR fish_color_valid_path:\x2d\x2dunderline
SETUVAR fish_greeting:\x1d
SETUVAR fish_key_bindings:fish_default_key_bindings
SETUVAR fish_pager_color_background:\x1d
SETUVAR fish_pager_color_completion:cdd6f4
SETUVAR fish_pager_color_description:6c7086
SETUVAR fish_pager_color_prefix:f5c2e7
SETUVAR fish_pager_color_progress:6c7086
SETUVAR fish_pager_color_secondary_background:313244
SETUVAR fish_pager_color_secondary_completion:\x1d
SETUVAR fish_pager_color_secondary_description:\x1d
SETUVAR fish_pager_color_secondary_prefix:\x1d
SETUVAR fish_pager_color_selected_background:\x2dr
SETUVAR fish_pager_color_selected_completion:\x1d
SETUVAR fish_pager_color_selected_description:\x1d
SETUVAR fish_pager_color_selected_prefix:\x1d
```

Еще можно добавить в стиле `catppuccin` тему в терминале `kitten themes`


`Catppuccin Laime:`

```toml
# Отключаем пустую строку в начале
add_newline = true

# Настройка формата:
format = """
[](fg:#a6e3a1)\
[ void ](bg:#a6e3a1 fg:#11111b)\
[](fg:#a6e3a1) \
$directory\
$git_branch\
$git_status\
$character"""

[directory]
# Путь будет светло-зеленым (лаймовым)
style = "bold #a6e3a1"
format = "[$path ]($style)"
truncation_length = 3

[character]
# Символ ввода (лаймовый при успехе, розовый при ошибке)
success_symbol = "[❯](bold #a6e3a1)"
error_symbol = "[❯](bold #f38ba8)"

[git_branch]
symbol = " "
style = "bold #94e2d5" # Цвет тил (бирюзовый), хорошо сочетается с лаймом

[git_status]
style = "bold #f38ba8"
```


`.config/fish/conf.d ❯ cat fish_frozen_theme.fish `

```fish
# This file was created by fish when upgrading to version 4.3, to migrate
# theme variables from universal to global scope.
# Don't edit this file, as it will be written by the web-config tool (`fish_config`).
# To customize your theme, delete this file and see
#     help interactive#syntax-highlighting
# or
#     man fish-interactive | less +/^SYNTAX.HIGHLIGHTING
# for appropriate commands to add to ~/.config/fish/config.fish instead.
# See also the release notes for fish 4.3.0 (run `help relnotes`).

set --global fish_color_autosuggestion 585b70
set --global fish_color_cancel f38ba8
set --global fish_color_command a6e3a1 --bold
set --global fish_color_comment 7f849c
set --global fish_color_cwd a6e3a1
set --global fish_color_cwd_root red
set --global fish_color_end fab387
set --global fish_color_error f38ba8
set --global fish_color_escape f5c2e7
set --global fish_color_history_current --bold
set --global fish_color_host a6e3a1
set --global fish_color_host_remote yellow
set --global fish_color_keyword f9e2af
set --global fish_color_normal cdd6f4
set --global fish_color_operator f5c2e7
set --global fish_color_param 94e2d5
set --global fish_color_quote a6e3a1
set --global fish_color_redirection fab387
set --global fish_color_search_match --background=313244
set --global fish_color_selection --background=313244
set --global fish_color_status red
set --global fish_color_user a6e3a1
set --global fish_color_valid_path a6e3a1 --underline
set --global fish_pager_color_background
set --global fish_pager_color_completion cdd6f4
set --global fish_pager_color_description 6c7086
set --global fish_pager_color_prefix f5c2e7
set --global fish_pager_color_progress 6c7086
set --global fish_pager_color_secondary_background 313244
set --global fish_pager_color_secondary_completion
set --global fish_pager_color_secondary_description
set --global fish_pager_color_secondary_prefix
set --global fish_pager_color_selected_background -r
set --global fish_pager_color_selected_completion
set --global fish_pager_color_selected_description
set --global fish_pager_color_selected_prefix
```

`config.fish`

```fish
if status is-interactive
    # Отключаем стандартное приветствие
    set -g fish_greeting ""

    # Инициализация Starship
    starship init fish | source
end
```

