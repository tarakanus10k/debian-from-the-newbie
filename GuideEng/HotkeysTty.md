# Keyboard shortcuts in tty
##1. Process Management
- Ctrl + C: abort the process
- Ctrl + Z: pause the process

## 2. Moving the cursor
- Ctrl + A: move the cursor to the beginning of the line
- Ctrl + E: move the cursor to the end of the line
- Alt + F: move the cursor forward one word
- Alt + B: move the cursor one word back
- Ctrl + F: move the cursor forward one character
- Ctrl + B: move the cursor one character back

##3. Text Editing
- Ctrl + L: clear the screen (the `clear` command)
- Ctrl + D: delete the character under the cursor
- Alt + T: swap two words (the word under the cursor swaps places with the left word)
- Ctrl + T: swap two characters (the character under the cursor swaps places with the left character)
- Alt + L: lower case characters (start: the character under the cursor, end: the end of the word)
- Alt + U: convert characters to uppercase (start: the character under the cursor, end: the end of the word)

## 4. Cutting and pasting text
- Ctrl + K: cut the text from the cursor to the end of the line
- Ctrl + U: cut the text from the cursor to the beginning of the line
- Alt + D: cut the word from the cursor to its end
- Alt + Backspace: cut the word from the cursor to its beginning
- Ctrl + Y: paste the cut text from the clipboard to the cursor location

## 5. Team Addition
- Tab: add command text
- Alt + ?: display all the add-on options
- Alt + *: insert all add-on options into the command arguments

## 6. Search for commands in the history
- Ctrl + R: Start searching for commands in the history. Tap again to move up the story. Press Enter to execute the found command
- Ctrl + J: paste the found command into the terminal, without executing
- Ctrl + G: stop searching for commands in the history
- Ctrl + P: show the previous entry in the history
- Ctrl + N: show the next entry in the history
- Alt + <: go to the first entry in the history
- Alt + >: go to the last entry in the history
- Alt + N: search in direct order (enter a command and press Enter)
- Alt + P: search in reverse order (enter a command and press Enter)
- Ctrl + O: run a command from the history and proceed to the next one in the list (it only works in Ctrl+R search)
