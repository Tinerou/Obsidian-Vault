### Insert

`i` - insert mode before your cursor
`a` - enter insert mode after your cursor
`esc` - to leave insert mode

**Inserting at Line Ends:**
`A` - enter insert mode at the *beginning* of a line
`I` - enter insert mode at the *end* of a line


---

### Movement

**Basic Movement**
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
`0` - move to the *beginning* of a line
`$` - move to the *end* of a line
`_` - move to the  *first word*  in a line

**Find**
`f` `char` - move *forward* to the *next occurrence* of {char} within the line
`F` `char` - move *backward* to *previous occurrence* of {char} within the line
`;` - repeat the last find motion

**Till**
`t` `char` - move *forward* till the *next occurrence* of {char} within the line
`T` `char` - move *backward* till the *previous occurrence* of {char} within the line
`;` - repeat the last till motion
### Undo/Redo

`u` - undo
`ctrl+r` - redo

### Opening new lines

`o` - open a new line *below* the cursor
`O` - open a new line *above* the cursor
**
### Small edits

`x` - delete the character *under* the cursor
`s` - delete the character *under* your cursor and enter inset mode
`r` - replace the character *under* your cursor with next character you type

### Operators

`esc` - delete the in progress operator

**Delete Words**
`d` `w` - delete word
`d` `W` - delete a WORD

**Delete Lines**
`d` `d` - delete the *current line*
`D` - delete from the cursor to the *end of the line*
`d` `j` - delete the current line and the line *below*
`d` `k` - delete the current line and the line *above*
`3` `d` `d` - delete 3 lines

**Copy/Paste Lines**
`y` `y` - yank (copy) the *current line*
`Y` - alt for `y` `y`
`p` - put (paste) *below* the cursor
`P` - put (paste) *above* the cursor


*Operators* are commands that perform actions on text. Think of them as verbs in Vim's language.

![[Pasted image 20250923221528.png]]

[Vim Cheatsheet](https://devhints.io/vim)