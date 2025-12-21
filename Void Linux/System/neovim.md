[[#Установка]]





---
# Установка

Обновите индексы репозиториев и систему:

```bash
sudo xbps-install -Syu
```

Установите **Neovim**

```bash
sudo xbps-install -y neovim
```

---

Нам нужно создать конфиг файл `lua`

```bash
#/home/xbpsx/.config/nvim
touch init.lua
```

Первоначальные установка в файле `init.lua`

```lua
set expandtab
set tabstop=2
set softtabstop=2
set shiftwidth=2
# будет ошибка
```

Нужно преоброзовать **vim в lua**

```lua
vim.cmd("set expandtab")
vim.cmd("set tabstop=2")
vim.cmd("set softtabstop=2")
vim.cmd("set shiftwidth=2")
```

Устанвока менеджера пакетов есть два популярных пакета `lazy.nvim` и `packer.nvim`. Мы выбираем **lazy**, нужно ставить код в `init.lua`

```lua
-- Путь, куда будет установлен lazy.nvim
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"

-- Автоматическая загрузка (bootstrap), если lazy.nvim не найден
if not (vim.uv or vim.loop).fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable", -- использование последней стабильной версии
    lazypath,
  })
end

-- Добавление пути lazy.nvim в runtime path (rtp)
vim.opt.rtp:prepend(lazypath)
```

Нужно вызывать функцию сетап для **lazy**

```lua
require("lazy").setup(plugins, opts)
```

Создаем пустые переменные 

```lua
local plugins = {}
local opts = {}
```

Если мы введем команду 

```lua
-- увидим графеский
:Lazy
```


---

Перый пакет который мы установим, будет цветовая Catppuccin

```lua
local plugins = {
	{ "catppuccin/nvim", name = "catppuccin", priority = 1000 }
}
```

Что бы тема заработало надо

```lua
require("catppuccin").setup()
vim.cmd.colorscheme "catppuccin"
```


---

```lua
vim.cmd("set expandtab")
vim.cmd("set tabstop=2")
vim.cmd("set softtabstop=2")
vim.cmd("set shiftwidth=2")


-- Путь, куда будет установлен lazy.nvim
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"

-- Автоматическая загрузка (bootstrap), если lazy.nvim не найден
if not (vim.uv or vim.loop).fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable", -- использование последней стабильной версии
    lazypath,
  })
end

-- Добавление пути lazy.nvim в runtime path (rtp)
vim.opt.rtp:prepend(lazypath)

local plugins = {
  { "catppuccin/nvim", name = "catppuccin", priority = 1000 }
}

local opts = {}

require("lazy").setup(plugins, opts)

require("catppuccin").setup()
vim.cmd.colorscheme "catppuccin"


-- цвет фона убирает
local function set_transparent_bg()
  local groups = { "Normal", "NormalFloat", "FloatBorder", "Pmenu", "SignColumn", "LineNr", "NonText" }
  for _, group in ipairs(groups) do
    vim.api.nvim_set_hl(0, group, { bg = "none" })
  end
end

-- Применяем сразу и при каждой смене цветовой схемы
set_transparent_bg()
vim.api.nvim_create_autocmd("ColorScheme", {
  callback = set_transparent_bg,
})
```

