# 🧠 **Vim Modes**

|Mode|Enter With|Purpose|
|---|---|---|
|Normal|`Esc`|Navigation & commands|
|Insert|`i`, `a`, `o`|Typing/editing text|
|Visual|`v`, `V`, `Ctrl+v`|Text selection|
|Command/Ex|`:`|File, search, and settings|
|Replace|`R`|Overwrite text|

---

## 📝 **1. Insert Mode Entry Keys**

|Key|Meaning|
|---|---|
|`i`|Insert before cursor|
|`I`|Insert at start of line|
|`a`|Append after cursor|
|`A`|Append at end of line|
|`o`|Open new line below|
|`O`|Open new line above|

---

## 🧭 **2. Normal Mode Navigation**

### 🔼 Movement by Character, Word, Line:

|Key|Description|
|---|---|
|`h`|Move left|
|`l`|Move right|
|`j`|Move down|
|`k`|Move up|
|`0`|Start of line|
|`^`|First non-whitespace|
|`$`|End of line|
|`w`|Start of next word|
|`W`|Start of next WORD|
|`e`|End of word|
|`b`|Beginning of word|

### 📜 Movement by Screen/Paragraph:

|Key|Description|
|---|---|
|`H`|Top of screen|
|`M`|Middle of screen|
|`L`|Bottom of screen|
|`{`/`}`|Previous/Next paragraph|
|`gg`|Start of file|
|`G`|End of file|
|`:n`|Go to line `n`|

---

## 🔨 **3. Editing Commands (Normal Mode)**

|Key|Description|
|---|---|
|`x`|Delete character|
|`dd`|Delete line|
|`dw`|Delete word|
|`D`|Delete to end of line|
|`yy`|Yank (copy) line|
|`yw`|Yank word|
|`p`|Paste after cursor|
|`P`|Paste before cursor|
|`u`|Undo|
|`Ctrl+r`|Redo|
|`r<char>`|Replace one character|
|`J`|Join next line|
|`>>` / `<<`|Indent / unindent line|
|`~`|Toggle case|

---

## 🔍 **4. Searching and Replacing**

|Command|Description|
|---|---|
|`/word`|Search forward|
|`?word`|Search backward|
|`n` / `N`|Repeat search forward/backward|
|`:%s/old/new/g`|Replace all in file|
|`:%s/old/new/gc`|Replace with confirmation|
|`:noh`|Remove search highlighting|

---

## 👓 **5. Visual Mode (Selection)**

|Key|Description|
|---|---|
|`v`|Start character-wise visual mode|
|`V`|Start line-wise visual mode|
|`Ctrl+v`|Start block-wise visual mode|
|`y`|Yank selection|
|`d`|Delete selection|
|`>` / `<`|Indent / unindent selection|
|`~`|Toggle case on selection|

---

## 📂 **6. File & Buffer Management (Ex Mode)**

|Command|Description|
|---|---|
|`:w`|Save|
|`:w filename`|Save as|
|`:q`|Quit|
|`:q!`|Quit without saving|
|`:wq` or `ZZ`|Save and quit|
|`:e filename`|Open file|
|`:bn` / `:bp`|Next/Previous buffer|
|`:ls`|List open buffers|
|`:bd`|Delete buffer (close file)|

---

## 🔄 **7. Window Splits & Tabs**

|Command|Description|
|---|---|
|`:split` or `:sp`|Horizontal split|
|`:vsplit` or `:vsp`|Vertical split|
|`Ctrl+w` then `h/j/k/l`|Move between splits|
|`:tabnew`|Open new tab|
|`gt`, `gT`|Next/Previous tab|

---

## 🧩 **8. Macros and Repeats**

|Key|Description|
|---|---|
|`.`|Repeat last change|
|`q<letter>`|Start recording macro|
|`@<letter>`|Run macro|

---

## 🔧 **9. Useful Settings & Shortcuts**

|Command|Description|
|---|---|
|`:set number`|Show line numbers|
|`:set relativenumber`|Show relative line numbers|
|`:set hlsearch`|Highlight search results|
|`:set incsearch`|Incremental search|
|`:syntax on`|Enable syntax highlighting|

---

## 🎮 **10. Special Key Combos**

|Key Combo|Description|
|---|---|
|`Ctrl + o`|Go to older cursor position|
|`Ctrl + i`|Go to newer cursor position|
|`Ctrl + d` / `u`|Scroll half page down/up|
|`Ctrl + e` / `y`|Scroll screen down/up (without moving cursor)|
|`Ctrl + ^`|Toggle between last two files|
