# vscode-vim-bindings
Well at least it's a starting point LOL 😀, use this if your starting with VimMotions and NeoVim or Vim is too overwhelming

# VS Code Vim Keybindings – Clean & Minimalist Setup  
*(the one where `D`, `C`, `S` finally stop yanking garbage into your clipboard)*

A super-clean, opinionated VS Code + VSCodeVim configuration I actually use every day.

## Core Philosophy
- `Shift+D`, `Shift+C`, `Shift+S` → **NEVER yank** (they delete/change into the black-hole register `"_`)
- No clipboard pollution, ever
- Muscle memory stays 100% Vim-compatible
- Leader = `<space>` (the only sane choice in 2025)
- jk → Escape (yes, I’m that guy)
- Everything else is minimal but extremely useful

## Key Features & Mappings

### Normal & Visual Mode (the important ones)

| Key            | Action                                      | Description                                      |
|----------------|---------------------------------------------|--------------------------------------------------|
| `D`            | `"_d$`                                      | Delete to end of line → no yank                  |
| `C`            | `"_c$`                                      | Change to end of line → no yank                  |
| `S`            | `"_S`                                       | Substitute line → no yank                        |
| `Y`            | `"_Y`                                       | Yank line → no yank (consistent with above)      |
| `$`            | `g_`                                        | Go to last non-blank character (not EOL)        |
| `0`            | `^`                                         | Go to first non-blank character                  |
| `<leader>w`    | Save file                                   |                                                  |
| `<leader>q`    | Close current editor                        |                                                  |
| `<leader>x`    | Close window                                |                                                  |
| `<leader>y`    | `:%y`                                       | Yank entire buffer                               |
| `<leader>d`    | `:%d_`                                      | Delete entire buffer (black-hole)                |
| `<leader>a`    | `ggVG`                                      | Select all                                       |
| `<leader>e`    | Quick Open (`Ctrl+P`)                       |                                                  |
| `<leader>n` / `p` | Next/previous tab                        |                                                  |
| `<C-h/j/k/l>`  | Focus left/down/up/right editor group       | tmux-style navigation                            |
| `p` (visual)   | `"_dP`                                      | Paste without yanking the replaced text         |
| `Tab` / `<S-Tab>` (visual) | Indent / outdent lines              |                                                  |

### Insert Mode
| Key   | Action   |
|-------|----------|
| `jk`  | `<Esc>`  |

### Leader is Space
```json
"vim.leader": "<space>"
```

### Other Settings
- Relative line numbers
- Auto-save on focus change
- Clipboard is still enabled (`"vim.useSystemClipboard": true`) — you can still use `yy`, `*y`, `"+y`, etc. when you actually want to copy
- Theme: SynthWave '84 (because neon never dies)

## Full settings.json (copy-paste ready)

```json
{
  "vim.insertModeKeyBindings": [
    {
      "before": ["j", "k"],
      "after": ["<Esc>"]
    }
  ],
  "vim.visualModeKeyBindings": [
    {
      "before": ["p"],
      "after": ["\"", "_", "d", "P"]
    },
    {
      "before": ["<tab>"],
      "commands": ["editor.action.indentLines"]
    },
    {
      "before": ["$"],
      "after": ["g", "_"]
    },
    {
      "before": ["<S-tab>"],
      "commands": ["editor.action.outdentLines"]
    }
  ],
  "vim.visualModeKeyBindingsNonRecursive": [
    {
      "before": ["D"],
      "after": ["\"", "_", "d"]
    },
    {
      "before": ["C"],
      "after": ["\"", "_", "c"]
    },
    {
      "before": ["S"],
      "after": ["\"", "_", "S"]
    }
  ],
  "vim.normalModeKeyBindingsNonRecursive": [
    { "before": ["$"], "after": ["g", "_"] },
    { "before": ["0"], "after": ["^"] },
    { "before": ["<leader>", "w"], "commands": ["workbench.action.files.save"] },
    { "before": ["<leader>", "q"], "commands": ["workbench.action.closeActiveEditor"] },
    { "before": ["<leader>", "x"], "commands": ["workbench.action.closeWindow"] },
    { "before": ["<leader>", "y"], "after": [":", "%", "y", "<CR>"] },
    { "before": ["<leader>", "a"], "after": ["g", "g", "V", "G"] },
    { "before": ["<leader>", "d"], "after": [":", "%", "d", "_", "<CR>"] },
    { "before": ["<C-h>"], "commands": ["workbench.action.focusLeftGroup"] },
    { "before": ["<C-j>"], "commands": ["workbench.action.focusBelowGroup"] },
    { "before": ["<C-k>"], "commands": ["workbench.action.focusAboveGroup"] },
    { "before": ["<C-l>"], "commands": ["workbench.action.focusRightGroup"] },
, "workbench.action.focusRightGroup"] },
    { "before": ["<leader>", "n"], "commands": ["workbench.action.nextEditor"] },
    { "before": ["<leader>", "p"], "commands": ["workbench.action.previousEditor"] },
    { "before": ["<leader>", "e"], "commands": ["workbench.action.quickOpen"] },
    { "before": ["D"], "after": ["\"", "_", "d", "$"] },
    { "before": ["C"], "after": ["\"", "_", "c", "$"] },
    { "before": ["S"], "after": ["\"", "_", "S"] },
    { "before": ["Y"], "after": ["\"", "_", "Y"] }
  ],
  "vim.leader": "<space>",
  "editor.lineNumbers": "relative",
  "vim.useSystemClipboard": true,
  "workbench.colorTheme": "SynthWave '84",
  "files.autoSave": "onFocusChange"
}
```

Just drop the relevant parts into your own `settings.json` (or the whole thing if you want the exact experience).

Enjoy a yanking-free life.  
No more accidental clipboard overwrites in 2025. Ever.
