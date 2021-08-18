# VIM Libor Tutorial

- **Modes**
  - **Normal** - default, you can return t here by `Esc`
  - **Insert** - you can edit text here
  - **Visual** - work with marked text
  - **Command** - other commands load / save / open windows, etc.

### Navigation

- arrows
- Word
  - `w` moves to the beginning of the next word
  - `W`moves to the beginnin of the next WORD
  - `b`moves backward to the beginning of the previous word
  - `B`moves backward to the beginning of  the previous WORD
  - 'e' end of the word
  - 'E' end of the WORD
- Lines
  - `0`moves to the beginning of the line
  - `$`moves to the end of the line
- Document
  - `gg`moves to the top of the file
  - `G`moves to the bottom of the file

### Editace

- `i` start iunsert text where the cursor ist
- `a` start inserting text right after the coursor
- `I` start at the beginning of the line
- `A` start at the end of the line
- `o` insert a new line after where I am and switch to insert mode
- `O` insert a new line before where I am and switch to insert mode

### Completing words

- `Ctrl-N` insert the next matching word
- `Ctrl-P` insert the

- Numbers
  - `Ctrl-A` increment number
  - `Ctrl-X ` decrement number

### Operators

- Operators wait for another command when used (eg not enough to use `c` but `cw` as change word)

- `c` - change
- `d` - delete
- `y` - yank into register (does not change the text)
- `~` - swap case (only if `tildeop`is set)
- `g~` - swap case
- `gu` - change lowercase
- `GU` - change uppercase
- `!` -  filter through an external program

### Operator combination and navigation

- `y2as`- yank two sentences into register

### Basic commands

- `:w`- save file
- `:q` - quit
- `:wq` - write and quit (save and quit)
- `:r` - read filename (can autocomplete with tabs)
- `:q! `- quit without saving changes
- `vim filename`- open file in vim
- `:e filename` - edit file1
- `u` - undo
- `U`- undo all the latest changes on the line where I was

### Search

- `/pattern`- moves the coursor to the first occurence
- `?pattern`- search back
- `?<CR> `- another occurence backwards

### Search within a line

- `f{char}`- char right
- `F{char}` - char left
- `t{char}` - sign right
- `T{char}`- sign left

### Clipboard :help yank / :help registers

- `yw`- copy word
- `yy`- copy linee
- `dd`- delete line
- `p`- paste after cursor
- `P`- paste before cursor

### Single repeat

- `.`- repeat the last change