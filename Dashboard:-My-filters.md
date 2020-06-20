- [Back to Wiki Home](./)
    - [Static filter syntax](./Static-filter-syntax)
        - [Procedural cosmetic filters](./Procedural-cosmetic-filters)
        - [Resources Library](./Resources-Library)

***

![my-filters](https://user-images.githubusercontent.com/585534/85202191-a0ddfb00-b2d2-11ea-8f93-a360c338ded7.png)

uBO uses [CodeMirror's widget](https://codemirror.net/index.html) to freely edit your filters as plain text.

The following keyboard shortcuts are available during editing -- most of them are handled by CodeMirror by default (I mostly lazily transcribed [CodeMirror's own documentation](https://codemirror.net/doc/manual.html#commands)):

|`____PC____`|`___Mac___`| Function |
|----|-----|:---------|
| <kbd>Ctrl</kbd>-<kbd>A</kbd> | <kbd>Cmd</kbd>-<kbd>A</kbd> | Select the whole content of the editor.
| <kbd>Ctrl</kbd>-<kbd>D</kbd> | <kbd>Cmd</kbd>-<kbd>D</kbd> | Deletes the whole line under the cursor, including newline at the end.
| <kbd>Ctrl</kbd>-<kbd>Z</kbd> | <kbd>Cmd</kbd>-<kbd>Z</kbd> | Undo the last change.<br>Note that, because browsers still don't make it possible for scripts to react to or customize the context menu,<br>selecting undo (or redo) from the context menu in a CodeMirror instance does not work.
| <kbd>Ctrl</kbd>-<kbd>Y</kbd> | <kbd>Cmd</kbd>-<kbd>Y</kbd> | Redo the last undone change.
| <kbd>Ctrl</kbd>-<kbd>U</kbd> | <kbd>Cmd</kbd>-<kbd>U</kbd> | Undo the last change to the selection, or if there are no selection-only changes at the top of the history, undo the last change.
| <kbd>Alt</kbd>-<kbd>U</kbd> | <kbd>Shift</kbd>-<kbd>Cmd</kbd>-<kbd>U</kbd> | Redo the last change to the selection, or the last text change if no selection changes remain.
| <kbd>Ctrl</kbd>-<kbd>Home</kbd> | <kbd>Cmd</kbd>-<kbd>Home</kbd> | Move the cursor to the start of the document.
| <kbd>Ctrl</kbd>-<kbd>End</kbd> | <kbd>Cmd</kbd>-<kbd>End</kbd> | Move the cursor to the end of the document.
| <kbd>Home</kbd> | <kbd>Home</kbd> | Move to the start of the text on the line, or if we are already there, to the actual start of the line (including whitespace).
| <kbd>End</kbd> | <kbd>End</kbd> | Move to the end of the line.
- <kbd>Up</kbd>, Mac: <kbd>Ctrl</kbd>-<kbd>P</kbd>: Move the cursor up one line.
- <kbd>Down</kbd>, Mac: <kbd>Ctrl</kbd>-<kbd>N</kbd>: Move down one line.
- <kbd>Page Up</kbd>, Mac: <kbd>Shift</kbd>-<kbd>Ctrl</kbd>-<kbd>V</kbd>: Move the cursor up one screen, and scroll up by the same distance.
- <kbd>Page Down</kbd>, Mac: <kbd>Ctrl</kbd>-<kbd>V</kbd>: Move the cursor down one screen, and scroll down by the same distance.
- <kbd>Left</kbd>, Mac: <kbd>Ctrl</kbd>-<kbd>B</kbd>: Move the cursor one character left, going to the previous line when hitting the start of line.
- <kbd>Right</kbd>, Mac: <kbd>Ctrl</kbd>-<kbd>F</kbd>: Move the cursor one character right, going to the next line when hitting the end of line.
- <kbd>Ctrl</kbd>-<kbd>Left</kbd>, Mac: <kbd>Alt</kbd>-<kbd>Left</kbd>:  Move to the left of the group before the cursor. A group is a stretch of word characters, a stretch of punctuation characters, a newline, or a stretch of more than one whitespace character.
- <kbd>Ctrl</kbd>-<kbd>Right</kbd>, Mac: <kbd>Alt</kbd>-<kbd>Right</kbd>: Move to the right of the group after the cursor (see above).
- <kbd>Backspace</kbd>, Mac: <kbd>Ctrl</kbd>-<kbd>H</kbd>: Delete the character before the cursor.
- <kbd>Delete</kbd>, Mac: <kbd>Ctrl</kbd>-<kbd>D</kbd>: Delete the character after the cursor.
- <kbd>Ctrl</kbd>-<kbd>Backspace</kbd>, Mac: <kbd>Alt</kbd>-<kbd>Backspace</kbd>: Delete to the left of the group before the cursor.
- <kbd>Ctrl</kbd>-<kbd>Delete</kbd>, Mac: <kbd>Alt</kbd>-<kbd>Delete</kbd>: Delete to the start of the group after the cursor.
- <kbd>Ctrl</kbd>-<kbd>]</kbd>, Mac: <kbd>Cmd</kbd>-<kbd>]</kbd>: Indent the current line or selection by one indent unit.
- <kbd>Ctrl</kbd>-<kbd>[</kbd>, Mac: <kbd>Alt</kbd>-<kbd>[</kbd>: Dedent the current line or selection by one indent unit.
- uBO-specific: <kbd>Tab</kbd>: Toggle prepending the current line or the lines in the current selection with `! ` (to quickly toggle the commenting out of filters).
- <kbd>Ctrl</kbd>-<kbd>S</kbd>, Mac: <kbd>Cmd</kbd>-<kbd>S</kbd>: Save and apply the changes, if any.
- <kbd>Ctrl</kbd>-<kbd>F</kbd>, Mac: <kbd>Cmd</kbd>-<kbd>F</kbd>: Find a string. Wrap around `/` to search against a regular expression.
- <kbd>Ctrl</kbd>-<kbd>G</kbd>, Mac: <kbd>Cmd</kbd>-<kbd>G</kbd>: Find next occurrence after the current cursor position.
- <kbd>Shift</kbd>-<kbd>Ctrl</kbd>-<kbd>G</kbd>, Mac: <kbd>Shift</kbd>-<kbd>Cmd</kbd>-<kbd>G</kbd>: Find previous occurrence before the current cursor position.
