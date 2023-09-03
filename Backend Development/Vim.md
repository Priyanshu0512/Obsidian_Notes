In order to exit the vim editor press escape key and then type :q to exit the editor.
Press i to go into insert  mode.
To go back to the normal mode press esc key.
Navigation -
1. l - in normal mode press l to move cursor to the right.
2. h - in normal mode press l to move cursor to the left.
3. j - in normal mode press l to move cursor to the down.
4. k - in normal mode press l to move cursor to the up.
Note - normal arrow keys also work fine.

**Commands**
1. vim filename.extension - opens the file if it is already existing or it creates a new one and opens its.
2. :wq - Saves the changes and exits the editor.
3. :q! - To exit without save the changes to the file.
4. dd - Press dd in normal mode to delete the current line.
5. gg - Press gg in normal mode to make the cursor go on the first line.
6. G - Press G in normal mode to make the cursor go on the last line.
7. w - Press w in normal mode to jump one word. Press 2w to jump 2 words and so on. 
8. d2w - To delete 2 words.
9. :%s/foo/bar - In normal mode it replaces all the occurences of foo with bar.
    Note - In order too replace only in the current  line omit the usage of %sign.
10. yw - In normal mode it copies one word.
11. yy - In normal mode it copies entire line.
12. p - For pasting in normal mode.
