Linux is an open-source Unix -like operating system based on the Linux kernel.

**REPL - Read Evaluate Print Loop**
Note- For any linux command you can check its usage and different input flags it expects by running the command followed by "--help"

**Commands** - 
1. `pwd` - Shows the current directory you are in.
     In mac-os we can use man pwd as an alternative to --help
2. `ls` - prints the content of all the files and folders in the current directory.
      `ls -a` : This display hidden folders present inside the directory.
      `ls -l` : This gives a more detailed view of all the files and folders (information about the owner, permissions allowed to the filed , date created etc. all are mentioned.)
      `ls -lh` : This also gives size of the files in addition to all the information provided by ls -l
3. cd - cd stands for change directory. Used to move in or out of an folder.
     To move outside the current folder do cd ..
     To move two jumps back do cd ../..
     To move to the home directory from any directory use  cd ~

Relative path - It describes the location of the file/folder w.r.t to the current folder.
Absolute path - It describes the location of the file/folder w.r.t to the home/root directory.
Root directory - The directory having no parent is called root directory.
    To go to the root directory use cd /

4. `mkdir folder-name` - It is used to create a new folder.
5. `touch file-name.extension` - It is used to create a new file.
6. `cat filename` - It prints the entire content of the file.
7. `rm filename`  - Used to remove a file.
8. `rmdir folder-name` - Used to remove the entire directory.
Note- Anything deleted directly from the terminal is deleted all together (it doesn't go to the trash.)
This command does not work if their is some content present in the folder.
To delete the subfolder along with all of its content used the command 
rm -r folder-name - It first recursively deletes all the contents of the folder then its deletes the folder .
9. **Do not use the rm -rf command - It is sort of like a force full delete of the folder along with all of its content . It rm -rf / is executed as / refers to the root directory it will start deleting all the content of the root folder .**
10. `|`  - This is called the piping operator and is used to transfer the result of the given command to the next command as an input.
        Ex - ls | grep web
       So the grep command sort of performs a sort of substring search to the input of the ls command and displays the result for all the folder containing the string web.

 11. `ps aux` - This lists all the running process in the terminal.
 12. `tail -n 3 filename` - It shows the last 3 lines of the file.
13. `tail filename` - It shows some of the last lines of the file.
14. `head -n 3 filename` - It shows the first 3 lines of the file.
15. `tail filename`- It shows some of the first lines of the file.
16. `tail -f filename` - It prints some of the last lines but stays inside the file to monitor the changes . If any data is being added to the file then it updates automatically.Press control c to exit the file.
17. `echo "something"` - It prints the data inside the double quotes onto the terminal.
18. `ls > dump.txt` -It dumps the result of ls command into the dump.txt file.
       Note - In order to  append  the content then use the >> opetator.
19. `&&` - This operator is used to club the commands in linux. 
       Ex- first command && second command - The second command will be executed only when the first command is executed successfully.
 20. `cp file1 file2` - This copies the content of first file to the second one.
 21. `mv file1 file2` - This moves(cut & pastes)  the file from the path of the file1 to the mention destination path.
        Note - A file can be renamed by moving the file1 form its source to the source only.
        Ex- mv newfile.txt 1.txt
 22. In order to archive the files tar -cf command is used. 
        Syntax :-   `tar -cf archive.zip file1  file2` 
        In order to compress the archive as well -zcf flag is used.
 23. In order to display the content of the archive tar -xvzf archive-name is used
 24. `tar -xf archive-name -C (path of destination folder)`
 25. `curl` - It is used to make an network request.Ex- curl www.google.com
 26. `sudo lsof -i -P -n  | grep LISTEN` - Used to get a detailed description of the process running along with the PORT number being used.
