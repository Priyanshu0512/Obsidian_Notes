Linux is an open-source Unix -like operating system based on the Linux kernel.

**REPL - Read Evaluate Print Loop**
Note- For any linux command you can check its usage and different input flags it expects by running the command followed by "--help"

**Commands** - 
-  `pwd` - Shows the current directory you are in.
     In mac-os we can use man pwd as an alternative to --help
-  `ls` - prints the content of all the files and folders in the current directory.
     -  `ls -a` : This display hidden folders present inside the directory.
      - `ls -l` : This gives a more detailed view of all the files and folders (information about the owner, permissions allowed to the filed , date created etc. all are mentioned.)
      - `ls -l /(directory-name` : List all the files with the directory all with extended informations.
      - `ls -R /(directory-name)` : List all the files within the subdirectories. `R stands for recursively.`
      - `ls -t /(directory-name)` : List all the last modified files.
      - `ls -s /(directory-name)` : List all the files by their size
      - `ls -lh` : This also gives size of the files in addition to all the information provided by ls -l
      - `ls ..` : List all the files in the parent directory.
      - `ls *.js` : Lists all the files with .js extension.
      - `ls (Wildcard)*` - List all the files with the mentioned wildcard.
-  cd - cd stands for change directory. Used to move in or out of an folder.
     To move outside the current folder do cd ..
     To move two jumps back do cd ../..
     To move to the home directory from any directory use  cd ~

Relative path - It describes the location of the file/folder w.r.t to the current folder.
Absolute path - It describes the location of the file/folder w.r.t to the home/root directory.
Root directory - The directory having no parent is called root directory.
    To go to the root directory use cd /

- `mkdir folder-name` - It is used to create a new folder. Note- use the `-p` flag to recursively create directories.
-  `touch file-name.extension` - It is used to create a new file.
-  `cat filename` - It prints the entire content of the file.
-  `cat > filname` - to write contents into the file. Use `>>` to append data to the file
-  `rm filename`  - Used to remove a file.
-  `rmdir folder-name` - Used to remove the entire directory.
Note- Anything deleted directly from the terminal is deleted all together (it doesn't go to the trash.)
This command does not work if their is some content present in the folder.
To delete the subfolder along with all of its content used the command 
rm -r folder-name - It first recursively deletes all the contents of the folder then its deletes the folder .
-  **Do not use the rm -rf command - It is sort of like a force full delete of the folder along with all of its content . It rm -rf / is executed as / refers to the root directory it will start deleting all the content of the root folder .**
-  `|`  - This is called the piping operator and is used to transfer the result of the given command to the next command as an input.
        Ex - ls | grep web
       So the grep command sort of performs a sort of substring search to the input of the ls command and displays the result for all the folder containing the string web.

-  `ps aux` - This lists all the running process in the terminal.
-  `tail -n 3 filename` - It shows the last 3 lines of the file.
-  `tail filename` - It shows some of the last lines of the file.
- `head -n 3 filename` - It shows the first 3 lines of the file.
-  `tail filename`- It shows some of the first lines of the file.
-  `tail -f filename` - It prints some of the last lines but stays inside the file to monitor the changes . If any data is being added to the file then it updates automatically.Press control c to exit the file.
- `echo "something"` - It prints the data inside the double quotes onto the terminal.
- `ls > dump.txt` -It dumps the result of ls command into the dump.txt file.
       Note - In order to  append  the content then use the >> opetator.
-  `&&` - This operator is used to club the commands in linux. 
       Ex- first command && second command - The second command will be executed only when the first command is executed successfully.
-  `cp file1 file2` - This copies the content of first file to the second one.
-  `mv file1 file2` - This moves(cut & pastes)  the file from the path of the file1 to the mention destination path.
        Note - A file can be renamed by moving the file1 form its source to the source.
        Ex- mv newfile.txt 1.txt
        Also the file can be renamed while moving if in the path the filename specified.
-  In order to archive the files tar -cf command is used. 
        Syntax :-   `tar -cf archive.zip file1  file2` 
        In order to compress the archive as well -zcf flag is used.
-  In order to display the content of the archive tar -xvzf archive-name is used
-  `tar -xf archive-name -C (path of destination folder)`
-  `curl` - It is used to make an network request.Ex- curl www.google.com
-  `sudo lsof -i -P -n  | grep LISTEN` - Used to get a detailed description of the process running along with the PORT number being used.
-  **`d`**: Indicates that this is a directory.
- **`rwxr-xr-x`**: Represents the file permissions for the owner, group, and others:
    - `rwx`: The owner (user) has read, write, and execute permissions.
    - `r-x`: The group has read and execute permissions.
    - `r-x`: Others have read and execute permissions.
- **`@`**: Indicates that the file or directory has extended attributes. You can view these attributes using the `xattr` command on macOS or the `ls -l@` command.
- `chmod` : This function is used to change the file/directory permissio.
     - `ugo` - u stand for user, g stands for group and o stands for others .
     - Also while adding the permissions we need to specify whether permissions are being added or removed by using the `+/-` after `ugo`.
     - Ex - `chmod u+w a.txt`- This gives the write permission to the user for a.txt file.
     - Permission can also be represented in numbers  `2` write, `4` read ,`1` execute.
     -  `7` (4 + 2 + 1) gives read, write, and execute permissions.
     - `6` (4 + 2) gives read and write permissions.
     - `5` (4 + 1) gives read and execute permissions.
     - `4` gives read-only permissions.
    - `0` gives no permissions.

- `wc filename` - This gives details about the file like the no. of lines, no. of words& characters.
- `grep` - grep performs a substring search of a sort and displays all the matching words(etc.)
- `grep -c "one" a.txt` - This prints the number of occurrences of all the "one" in the a.txt file. `-h` prints all the lines where the occurrences did occur. `hi` ignores the case sensitiveness.
- use `hir` to find occurrences across a directory.
- `hin` - n gives the line numbers of the occurrences.
- `hinw` - w prints the occurrence it if matches the complete word and not a part of some word.
-  `-o` This flag only gives and the matched parts.
- 