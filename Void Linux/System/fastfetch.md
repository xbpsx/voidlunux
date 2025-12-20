

```text
{
    "$schema": "https://github.com/fastfetch-cli/fastfetch/raw/dev/doc/json_schema.json",
    "logo": {
        "source": "${XDG_CONFIG_HOME:-$HOME/.config}/fastfetch/miku.jpeg",
        "height": 18,
        "width": 60,
        "padding": {
            "top": 5,
            "left": 3
        }
    },
    "modules": [
  "break",
        {
            "type": "host",
            "key": "   ",
            "keyColor": "yellow"
        },
	{
	   "type": "display",
	   "key": "  ├󰍹",
 	   "keyColor": "yellow"
	},
        {
            "type": "cpu",
            "key": "  ├",
            "keyColor": "yellow"
        },
        {
            "type": "memory",
            "key": "  ├󰍛",
            "keyColor": "yellow"
        },
        {
            "type": "disk",
            "key": "  ├",
            "keyColor": "yellow"
        },
        {
            "type": "gpu",
            "key": "  └󰍛",
            "keyColor": "yellow"
        },
  "break",
        {
            "type": "os",
            "key": "   ",
            "keyColor": "green"
        },
        {
            "type": "kernel",
            "key": "  ├󰻀",
            "keyColor": "green"
        },
        {
            "type": "bios",
            "key": "  ├",
            "keyColor": "green"
        },
        {
            "type": "packages",
            "key": "  ├",
            "keyColor": "green"
        },
        {
            "type": "shell",
            "key": "  └",
            "keyColor": "green"
        },
        "break",
        {
            "type": "wm",
            "key": "   ",
            "keyColor": "blue"
        },
        {
            "type": "lm",
            "key": "  ├",
            "keyColor": "blue"
        },
        {
            "type": "de",
            "key": "  ├",
            "keyColor": "blue"
        },
        {
            "type": "wmtheme",
            "key": "  ├",
            "keyColor": "blue"
        },
        {
            "type": "terminal",
            "key": "  └",
            "keyColor": "blue"
        },
  "break",
        {
            "type": "command",
            "key": "  OS Age ",
            "keyColor": "cyan",
            "text": "birth_install=$(stat -c %W /); current=$(date +%s); time_progression=$((current - birth_install)); days_difference=$((time_progression / 86400)); echo $days_difference days"
        },
        {
            "type": "uptime",
            "key": "  Uptime ",
            "keyColor": "cyan"
        },
        {
            "type": "datetime",
            "key": "  DateTime ",
            "keyColor": "cyan"
        },
	"break",
	{
	   "type": "media",
	   "key": "   ",
	   "keyColor": "magenta"
	},
	"break",

//        {
//            "type": "colors"
//        },

        {
            "type": "colors",
            "paddingLeft": 2,
            "symbol": "circle"
        }

    ]
}
```

