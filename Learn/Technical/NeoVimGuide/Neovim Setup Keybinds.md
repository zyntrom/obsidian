## 🗃️ File Operations

|Keybinding|Description|
|---|---|
|`<leader>w`|Save file|
|`<leader>q`|Quit file|
|`<leader>e`|Toggle NvimTree explorer|
|`a` (in NvimTree)|Create new file/directory|
|`r` (in NvimTree)|Rename file/directory|
|`d` (in NvimTree)|Delete file/directory|
|`c` (in NvimTree)|Copy file|
|`x` (in NvimTree)|Cut file|
|`p` (in NvimTree)|Paste file|

---
## 🔍 File Finding (Telescope)

| Keybinding   | Description  |
| ------------ | ------------ |
| `<leader>ff` | Find files   |
| `<leader>fg` | Live grep    |
| `<leader>fb` | List buffers |
| `<leader>fh` | Help tags    |

---

## 🧠 LSP

|Keybinding|Description|
|---|---|
|`gd`|Go to definition|
|`K`|Hover docs|
|`<leader>la`|Code action|
|`<leader>lr`|Rename symbol|

---

## 💻 Running Code (Terminal)

|Keybinding|Description|
|---|---|
|`<leader>r`|Run current file (via `run_file.lua`)|

---

## 🧩 Git (Gitsigns)

|Keybinding|Description|
|---|---|
|`<leader>gb`|Git blame current line|
|`<leader>gp`|Preview git hunk|
|`<leader>gr`|Reset git hunk|

---

## 🪟 Window Splits

|Keybinding|Description|
|---|---|
|`<leader>sv`|Vertical split|
|`<leader>sh`|Horizontal split|

---

## 🧭 Tab Navigation

|Keybinding|Description|
|---|---|
|`<leader>ot`|Open current file in new tab|
|`<leader>tn`|Next tab|
|`<leader>tp`|Previous tab|
|`<leader>tc`|Close current tab|
|`<leader>to`|Close other tabs|
|`<leader>t1-9`|Go to tab 1–9|
|`<leader>tr`|Next tab (→)|
|`<leader>tl`|Previous tab (←)|
|`<S-Tab>`|Previous tab (backup binding)|

---

## 🧭 NvimTree Navigation

|Keybinding|Description|
|---|---|
|`<leader><Tab>`|Jump from NvimTree to file window|
|`t`|Open file in new tab|
|`v`|Open file in vertical split|
|`s`|Open file in horizontal split|
|`Tab`|Preview file|
|`R`|Refresh|
|`H`|Toggle hidden files|

---

## 🖥️ Terminal (ToggleTerm)

|Keybinding|Description|
|---|---|
|`<leader>tt`|Toggle terminal|
|`<Esc>` (in terminal)|Exit terminal mode|

---

## 🔧 Resizing & Formatting

|Keybinding|Description|
|---|---|
|`<leader>+`|Increase window height|
|`<leader>-`|Decrease window height|
|`<Tab>` (visual)|Indent right|
|`<S-Tab>` (visual)|Indent left|

---

## 🔄 Misc

|Keybinding|Description|
|---|---|
|`Ctrl + b then Ctrl + s`|Save tmux session (tmux)|
|`Ctrl + b then Ctrl + r`|Restore tmux session (tmux)|

---

## 📝 Notes

- `S` in `<S-Tab>` means **Shift**
- `<leader>` is set to **Spacebar**
- All bindings are set in **normal mode** unless noted (`v` for visual, `t` for terminal)
- NvimTree handles internal file manipulation (copy/paste/rename) without affecting system clipboard by default.