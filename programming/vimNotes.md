### Insert

`i` - insert mode before your cursor
`a` - enter insert mode after your cursor
`esc` - to leave insert mode

**Inserting at Line Ends:**
`A` - enter insert mode at the beginning of a line
`I` - enter insert mode at the end of a line


---

### Basic Movement

`h` -  left
`j` - down
`k` - up
`l` - right

**Moving By Words**
`w` - next word
`e` - end of word
`b` - move back a word

**Moving by WORDS**
`W` - next WORD
`E` - end of WORD
`B` - move back a WORD



**Moving to line ends**
`0` - move to the **beginning** of a line
`$` - move to the **end** of a line
`_` - move to the **first word** in a line

**Find**
`f` `char` - move forward to the **next occurrence** of {char} within the line
`F` `char` - move backward to **previous occurrence** of {char} within the line
`;` - repeat the last find motion

### Undo/Redo

`u` - undo
`ctrl+r` - redo

### Opening new lines

`o` - open a new line below the cursor
`O` - open a new line above the cursor

### Small edits

`x` - delete the character **under** the cursor
`s` - delete the character **under** your cursor and enter inset mode
`r` - replace the character **under** your cursor with next character you type