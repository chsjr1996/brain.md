#texteditor
## Configurações
```json
// Zed settings
//
// For information on how to configure Zed, see the Zed
// documentation: https://zed.dev/docs/configuring-zed
//
// To see all of Zed's default settings without changing your
// custom settings, run `zed: open default settings` from the
// command palette (cmd-shift-p / ctrl-shift-p)
{
  "vim_mode": true,
  "relative_line_numbers": true,
  "ui_font_size": 18,
  "buffer_font_size": 18,
  "tab_bar": {
    "show": false
  },
  "centered_layout": {
    "left_padding": 0.15,
    "right_padding": 0.15
  },
  "theme": {
    "mode": "system",
    "light": "Rosé Pine Dawn",
    "dark": "Rosé Pine Moon"
  },
  "format_on_save": "off",
  "languages": {
    "PHP": {
      "language_servers": ["intelephense", "!phpactor", "..."],
      "formatter": "language_server"
    }
  },
  "lsp": {
    "intelephense": {
      "initialization_options": {
        "globalStoragePath": "/home/user/.local/share/intelephense"
      }
    }
  }
}
```

## Atalhos
```json
// Zed keymap
//
// For information on binding keys, see the Zed
// documentation: https://zed.dev/docs/key-bindings
//
// To see the default key bindings run `zed: open default keymap`
// from the command palette.
[
  {
    "context": "Workspace",
    "bindings": {
      // "shift shift": "file_finder::Toggle"
    }
  },
  {
    "context": "Editor",
    "bindings": {
      // "j k": ["workspace::SendKeystrokes", "escape"]
      "ctrl-b": "workspace::ToggleLeftDock",
      "ctrl-j": "workspace::ToggleBottomDock",
      "alt-c": "pane::CloseActiveItem",
      "z x": "workspace::ToggleCenteredLayout"
    }
  }
]
```