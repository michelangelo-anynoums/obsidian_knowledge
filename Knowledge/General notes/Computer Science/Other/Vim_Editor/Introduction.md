==Vim is a powerful and efficient text editor== designed for navigating and editing text with the keyboard. ==It's well-known for its speed, flexibility, and the ability to handle large files with ease.== Although Vim has a steep learning curve, once mastered, it allows users to edit text and code quickly and precisely, ==without relying on the mouse.==

Vim operates in **different modes**:

- **Normal Mode**: The default mode for navigation and text manipulation.
    
- **Insert Mode**: The mode for typing text.
    
- **Visual Mode**: Used to select text.
    
- **Command Mode**: For executing commands, such as saving or searching.
    

While it’s often used by developers and system administrators, Vim is also useful for anyone who works with text—like those who write, take notes, or even manage documents in Markdown or similar formats. Its minimalistic design and keyboard-centric workflow make it an excellent choice for efficient, distraction-free writing and editing.

## Essential Vim Commands

### 1. **Opening Vim**

- To open Vim with a new file or an existing file:

```Bash
vim filename.txt
```
If the file doesn’t exist, ==Vim will create it== when you save.

### 2. **Vim Modes**

- **Normal Mode** (default mode): This is where you can navigate and issue commands.
    
- **Insert Mode**: This is for ==typing text==. You enter this mode from Normal Mode by pressing `i`.
    
- **Visual Mode**: For ==selecting text==. You enter this mode by pressing `v`.
    
- **Command Mode**: For ==issuing commands== like save, quit, etc. You enter this by pressing `:` from Normal Mode.
    

### 3. **Basic Navigation (Normal Mode)**

- **Move cursor**:
    
    - `h` – Left
        
    - `j` – Down
        
    - `k` – Up
        
    - `l` – Right
        
- **Move by word**:
    
    - `w` – Move to the start of the next word
        
    - `b` – Move to the beginning of the current/previous word
        
    - `e` – Move to the end of the current word
        
- **Move to beginning or end of line**:
    
    - `0` – Move to the start of the line
        
    - `$` – Move to the end of the line
        
- **Move by paragraph**:
    
    - `{` – Move up one paragraph
        
    - `}` – Move down one paragraph
        

### 4. **Editing Text (Insert Mode)**

- To start typing, you need to enter **Insert Mode** by pressing `i`.
    
- Other Insert Mode commands:
    
    - `a` – Append after the current cursor position.
        
    - `o` – Open a new line below the current line and enter Insert Mode.
        
    - `O` – Open a new line above the current line and enter Insert Mode.
        

To return to **Normal Mode**, press `Esc`.

### 5. **Saving Files**

- **Save the file** (from Normal Mode):
    
    - `:w` – Write (save) the current file.
        
- **Save and exit**:
    
    - `:wq` – Save and quit Vim.
        
- **Exit without saving**:
    
    - `:q!` – Quit without saving changes (use if you made changes but don’t want to keep them).
        

### 6. **Exiting Vim**

- **Quit** (if no changes were made):
    
    - `:q` – Quit Vim (only works if there are no unsaved changes).
        
- **Force Quit** (without saving):
    
    - `:q!` – Quit without saving changes.
        
- **Quit and save**:
    
    - `:wq` or `ZZ` (both save and exit).
        

### 7. **Deleting Text**

- **Delete a character**:
    
    - `x` – Delete the character under the cursor.
        
- **Delete a word**:
    
    - `dw` – Delete from the cursor to the beginning of the next word.
        
- **Delete a line**:
    
    - `dd` – Delete the entire current line.
        
- **Delete to the end of the line**:
    
    - `D` – Delete from the cursor position to the end of the line.
        

### 8. **Undo and Redo**

- **Undo last action**:
    
    - `u` – Undo.
        
- **Redo last undone action**:
    
    - `Ctrl` + `r` – Redo.
        

### 9. **Search and Replace**

- **Search for a string**:
    
    - `/text` – Search forward for "text".
        
    - `?text` – Search backward for "text".
        
- **Find next occurrence**:
    
    - `n` – Find the next match.
        
- **Find previous occurrence**:
    
    - `N` – Find the previous match.
        
- **Search and replace**:
    
    - `:%s/old/new/g` – Replace all instances of "old" with "new" in the entire file.
        
    - `:s/old/new/g` – Replace in the current line.
        

### 10. **Copy, Cut, and Paste**

- **Copy (yank) text**:
    
    - `yy` – Copy the current line.
        
    - `yw` – Copy the current word.
        
    - `y$` – Copy to the end of the line.
        
- **Cut (delete) text**:
    
    - `dd` – Cut (delete) the current line.
        
- **Paste text**:
    
    - `p` – Paste after the cursor.
        
    - `P` – Paste before the cursor.
        

### 11. **Visual Mode**

- **Enter Visual Mode**:
    
    - `v` – Select text character by character.
        
    - `V` – Select entire lines.
        
    - `Ctrl` + `v` – Select text in a block.
        
- **Cut/Copy in Visual Mode**:
    
    - After selecting text, press `d` to cut or `y` to copy.
        

---

### Summary of Key Commands:

- **Normal Mode**: Press `Esc` to go here.
    
- **Insert Mode**: Press `i` to start typing, then `Esc` to return to Normal Mode.
    
- **Save**: `:w`
    
- **Save and Quit**: `:wq`
    
- **Quit (no changes)**: `:q`
    
- **Quit (force, no save)**: `:q!`
    
- **Undo**: `u`
    
- **Redo**: `Ctrl` + `r`
    
- **Search**: `/text` (find), `n` (next), `N` (previous)
    
- **Delete**: `x` (char), `dd` (line)
    
- **Copy**: `yy` (line), `yw` (word)
    
- **Paste**: `p`


![[vimlogo.svg]]

---
Forgot **hotkeys**? Go to [Hotkeys](app://obsidian.md/Hotkeys)  