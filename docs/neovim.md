# Neovim

My cheatsheet for neovim

## Installation

!!! code ""

    ```bash
    sudo apt install neovim
    ```

### [Lazyvim](https://www.lazyvim.org/installation)

!!! code "Make a backup of your current Neovim files"

    ```bash
    # required
    (
      mv ~/.config/nvim{,.bak}

      # optional but recommended
      mv ~/.local/share/nvim{,.bak}
      mv ~/.local/state/nvim{,.bak}
      mv ~/.cache/nvim{,.bak}
      git clone https://github.com/LazyVim/starter ~/.config/nvim
      rm -rf ~/.config/nvim/.git
      nvim
    )
    ```

!!! tip

    It is recommended to run `:LazyHealth` after installation. This will load all plugins and check if everything is working correctly.

## Logic

- `A|a` - Append / Around

    - `a`ppend text after the cursor
    - `A`ppend text after the line
    
- `B|b` - Back / Beginning

    - move `b`ackwards one word
    - move `B`ackwards "big" word

- `C|c` - Change

    - `c`hange in <motion>
    - `C`hange from here
    
- `D|d` - Delete

    - `d`elete code enclosed in <X>
    - `D`elete from here | `DD` delete line

- `E|e` - End

    - `e`nd of a word
    - `E`nd of a "big" word | `E`nd of line2

- `F|f` - Find

    - `f`ind a character
    - `F`ind backwards

- `G|g` - Find

    - `g`o to || `gg g`o to end of document
    - `G`o to | `GG G`o to beginning

- `I|i` - Insert

    - `i`nsert text before cursor
    - `I`nsert text before line

- `m` - Mark

    - `m`ark position to register

- `N|n` - Next

    - `n`ext result forward
    - `N`ext result backward

- `O|o` - Open Line

    - `o`pen line bef`o`re
    - `O`pen line ab`O`ve

- `P|p` - Past / Paragraph

    - `p`aste after cursor | <motion> in `p`aragraph
    - `P`aste before cursor

- `q` - Re'q'ord Ma'q'ros

    - re`q`ord a macro to <register>

- `R|e` - Replace | Redo

    - `r`eplace under the cursor
    - `R`eplace until stopped
    - `R`edo (CTRL+R)

- `S|s` - Switch

    - `s`witch character (and keep on)
    - `S`witch line

- `T|t` - To

    -  (do something) `t`o character
    - `T`o character (backwards)

- `U|u` - 

## Moving Inside a File

You can move the cursor within a file by single characters, words, tokens, or lines.

According to Vim, a word can be a group of letters, numbers, and underscores. On the other hand, a token is anything separated by whitespace and can include punctuation.

Additionally, you can move to different parts of a text by screen view.

### Moving by Characters, Words and Tokens

The basic keys for moving the cursor by one character are:

- h – move the cursor left
- j – move the cursor down
- k – move the cursor up
- l – move the cursor right

You can also use these keys with a number as a prefix to move in a specified direction multiple times. For example, if you run 5j the cursor moves down 5 lines.

- b – move to the start of a word
- B – move to the start of a token
- w – move to the start of the next word
- W – move to the start of the next token
- e – move to the end of a word
- E – move to the end of a token

For instance, you have the noun phrase “step-by-step” as part of a text and the cursor is placed at the end of it. The first time you press b, the cursor  moves back to “step-by-step”. However, if you use B, the cursor moves all the way back to: “step-by-step” since there is no whitespace between these characters.

### Moving by Lines

- 0 (zero) – jump to the beginning of the line
- $ – jump to the end of the line
- ^ – jump to the first (non-blank) character of the line
- #G / #gg / :# – move to a specified line number (replace # with the line number)

### Moving by Screens

The following commands are used as a quick way to move within the text without scrolling.

- Ctrl + b – move back one full screen
- Ctrl + f – move forward one full screen
- Ctrl + d – move forward 1/2 a screen
- Ctrl + u – move back 1/2 a screen
- Ctrl + e – move screen down one line (without moving the cursor)
- Ctrl + y – move screen up one line (without moving the cursor)
- Ctrl + o – move backward through the jump history
- Ctrl + i – move forward through the jump history
- H – move to the top of the screen (H=high)
- M – move to the middle of the screen (M=middle)
- L – move to the bottom of the screen (L=low)

## Inserting Text

- i – switch to insert mode before the cursor
- I – insert text at the beginning of the line
- a – switch to insert mode after the cursor
- A – insert text at the end of the line
- o – open a new line below the current one
- O – open a new line above the current one
- ea – insert text at the end of the word
- Esc – exit insert mode; switch to command mode

Some of these commands switch between command and insert mode. By default, Vim launches in command mode, allowing you to move around and edit the file. To switch to command mode, use the Esc key.

### Editing Text

- `r` – replace a single character (and return to command mode)
- `cc` – replace an entire line (deletes the line and moves into insert mode)
- `C / c$` – replace from the cursor to the end of a line
- `cw` – replace from the cursor to the end of a word
- `s` – delete a character (and move into insert mode)
- `J` – merge the line below to the current one with a space in between them
- `gJ` – merge the line below to the current one with no space in between them
- `u` – undo
- `Ctrl + r` – redo
- `.` – repeat last command

### Cutting, Copying And Pasting

- `yy` – copy (yank) entire line
- `#yy` – copy the specified number of lines
- `dd` – cut (delete) entire line
- `#dd` – cut the specified number of lines
- `p` – paste after the cursor
- `P` – paste before the cursor

## Marking Text (Visual Mode)

Apart from command mode and insert mode, Vim also includes visual mode. This mode is mainly used for marking text.

Based on the chunk of text you want to select, you can choose between three versions of visual mode: character mode, line mode, and block mode.

- `v` – select text using character mode
- `V` – select lines using line mode
- `Ctrl+v` – select text using block mode
- `o` – move from one end of the selected text to the other
- `aw` – select a word
- `ab` – select a block with ()
- `aB` – select a block with {}
- `at` – select a block with <>
- `ib` – select inner block with ()
- `iB` – select inner block with {}
- `it` – select inner block with <>

### Visual Commands

Once you have selected the desired text in visual mode, you can use one of the visual commands to manipulate it. Some of them include:

- `y` – yank (copy) the marked text
- `d` – delete (cut) the marked text
- `p` – paste the text after the cursor
- `u` – change the market text to lowercase
- `U` – change the market text to uppercase

## Search in File

- `*` – jump to the next instance of the current word
- `#` – jump to previous instance of the current word
- `/pattern` – search forward for the specified pattern
- `?pattern` – search backward for the specified pattern
- `n` – repeat the search in the same direction
- `N` – repeat the search in the opposite direction

## Saving and Exiting File

- `:w` – save the file
- `:wq` / :x / ZZ – save and close the file
- `:q` – quit
- `:q!/ ZQ` – quit without saving changes
- `:w new_file_name` – save the file under a new name and continue editing the original
- `:sav` – save the file under a new name and continue editing the new copy
- `:w !sudo tee %` – write out the file using sudo and tee command

## Working with Multiple Files

- `:e file_name`  – open a file in a new buffer
- `:bn`  – move to the next buffer
- `:bp` – go back to previous buffer
- `:bd`  – close buffer
- `:b#`  – move to the specified buffer (by number)
- `:b` file_name – move to a buffer (by name)
- `:ls` – list all open buffers
- `:sp file_name`  – open a file in a new buffer and split viewport horizontally
- `:vs file_name`  – open a file in a new buffer and split viewport vertically
- `:vert ba`  – edit all files as vertical viewports
- `:tab ba`  – edit all buffers as tabs
- `gt` – move to next tab
- `gT` – move to previous tab
- `Ctrl+ws` – split viewport
- `Ctrl+wv` – split viewport vertically
- `Ctrl+ww` – switch viewports
- `Ctrl+wq` – quit a viewport
- `Ctrl+wx` – exchange current viewport with next one
- `Ctrl+=` – make all viewports equal in height and width

## Marks and Jumps

- m[a-z] – mark text using character mode (from a to z)
- M[a-z] – mark lines using line mode (from a to z)
- `a - jump to position marked a
- `y`a – yank text to position marked >a>
- `. – jump to last change in file
- `0 – jump to position where Vim was last exited
- `` – jump to last jump
- :marks – list all marks
- :jumps – list all jumps
- `:changes` – list all changes
- `Ctrl+i` – move to next instance in jump list
- `Ctrl+o` – move to previous instance in jump list
- `g,` – move to next instance in change list
- `g;` – move to previous instance in change list

## Macros

- `qa`  – record macro a
- `q`  – stop recording macro
- `@a`  – run macro a
- `@@`  – run last macro again

## Enabling Vim Color Schemes

- `:colorscheme [colorscheme_name]`  – change to specified scheme
- `:colorscheme [space]+Ctrl+d` – list available Vim color scheme

## References

- <https://phoenixnap.com/kb/vim-commands-cheat-sheet>
- <https://youtu.be/RZ4p-saaQkc?si=Lx1eJVe8P5eTpkNi>
