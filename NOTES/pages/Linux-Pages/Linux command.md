
### `echo`
prints a string of text, or value of a variable to the terminal.

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image.png)

---
### `date`
Display current date & time

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%201.png)

---
### `pwd`
show current working directory

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%202.png)

---
### `ls`
show the list of contents in working directory

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%203.png)

#### `ls <folder_name>`
list down all folder and files from `<folder_name>` 

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%204.png)

#### `ls -a`
list down all the files and folder including hidden

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%205.png)

#### `ls -l`
list down all details of file or folder such as directory, read/write operations, owner, subgroups, size, time

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%206.png)

#### `ls -lt`
list down all files and folder according to update or create time(new update first)

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%207.png)

### `ls -lr`

list down all files and folder according to update or create time(new update first)

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%208.png)

#### `ls -S`
**lists files and directories in a directory and sorts them by size in descending order, from largest to smallest**

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%209.png)
#### `ls -R`
it’s use to get all details of all folder or directory

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%2010.png)

---
### `cd`
it stands for change directory & as name suggested it’s use to change the directory

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%2011.png)
#### `cd ..`
return back to prev directory

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%2012.png)

---
### `mkdir`
it stands for make directory.

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%2013.png)

#### `mkdir -p`
create a chain of directory

```bash
mkdir -p <directory1/directory2/….>
```

### `touch`
it use to create a new file

![image.png](public/Linux%20command%201415cb8f372280e4ae2ad2d296f15ddc/image%2014.png)

### `cat`
it used to open file in read only mode in terminal but it can be used to update files

![image.png](image%2015.png)
here `vi` is a terminal based text editor, I use it to write the text inside the `test.txt` file.

#### `cat >>`
append text into file

![image.png](image%2016.png)

#### `cat >`
add new text & remove all of the previous text

![image.png](image%2017.png)

---
### `wc`
wc stands for **word count**. As the name implies, it is mainly used for counting purpose. It is used to find out **number of lines**, **word count**, **byte and characters count** in the files specified in the file arguments.

```bash
wc <flags> <path>
```

![image.png](image%2018.png)
1st column → number of lines, 2nd column → number of words, 3rd column → number of characters

#### `wc -l`
this option prints the **number of lines** present in a file

![image.png](image%2019.png)

#### `wc -w`
This option prints the **number of words** present in a file

![image.png](image%2020.png)

#### `wc -m`
This option prints the **number of characters** present in a file

![image.png](image%2021.png)

---
### `head`
head used to print lines from the top of the file, by default, head prints 10 lines 

![image.png](image%2022.png)

#### `head -n <number>`
Prints the first `<number>` lines instead of the first 10 lines.

![image.png](image%2023.png)

#### `head -c <number>`
Prints the first `<number>` bytes from the file.

![image.png](image%2024.png)

#### `head -v`
By using this option, data from the specified file is always preceded by its file name. 

![image.png](image%2025.png)

---
### `tail`
used to print lines from the top of the file, by default, head prints 10 lines.

![image.png](image%2026.png)
rest of the command same as head
```bash
tail -n <number>
tail -c <number>
tail -v 
```

---
### `mv`
it stands for move. it used to move files or  directory from one place to another.

```bash
mv <source_path> <destination_path>
```

![image.png](image%2027.png)
Now with the help of `mv`, we can easily rename the file or directory name.

```bash
rename  - `mv <old_name> <new_name>`
```

![image.png](image%2028.png)

---
### `cp`
it stands for copy. It use to cope files or directory

1. copy file - 
    
    ```bash
    copy <source_path> <destination_path>
    ```
    ![image.png](image%2029.png)
    in command I use `.` in place of `<destination_path>`, it means root path or the current path where we are standing.
    
2. copy directory - 
    ```bash
    copy -r <source_path> <destination_path>
    ```
    ![image.png](image%2030.png)
    
---
### `rm`
it stands for remove. If we use `rm` to remove any file or directory, it can’t be found in the recycle bin, and those files or directories are gone totally.

1. remove file
    ```bash
    rm <path>
    ```
    ![image.png](image%2031.png)
    
2. remove directory
    ```bash
    rm -r <path>
    ```
    ![image.png](image%2032.png)
    
---
### `grep`
The `grep` command in Unix/Linux is a powerful tool used for searching and manipulating text patterns within files. Its name is derived from the ed (editor) command g/re/p (globally search for a regular expression and print matching lines), which reflects its core functionality. `grep` is widely used by programmers, system administrators, and users alike for its efficiency and versatility in handling text data. In this article, we will explore the various aspects of the `grep` command.

```bash
grep <flags> <”word”> <path>

# flags
1. -c ⇒ count
2. -h ⇒ all match lines
3. -i ⇒ all matches case(upper, lower, ..)
4. -n ⇒ line number
5. -w ⇒ only those words (it will give use only “one“ word but if we don't use it  this → “colone” word can be check)
 . . . . and many more
```

---
### `sed`
The sed's substitute command has the following structure: 's/pattern/replacement/' 

``` bash
#1 
	`sed 's/ERROR/CRITICAL/' log.txt` 
#2. 
	`sed -ibackup 's/ERROR/CRITICAL/’ log.txt'
#3. 
	`sed ‘3 s/ERROR/CRITICAL/’ log.txt`
#4.
	`sed ‘3,5 s/ERROR/CRITICAL/' log.txt'
#5.
	`sed -n ‘3,/ERROR/ p’ log.txt`
```

---
### `awk`
awk [options] script file 

How patterns are define: ‘(pattern) {action}’ 

```bash

#1. 
	awk ‘/ERROR/{print $0}’ log.txt
#2. 
	awk ‘{gsub(/ERROR/, "CRITICAL")} {print}’ log.txt
#3. 
	awk 'BEGIN {print "LOG SUMMARY\n"} {print} END {print \nEND OF LOG SUMMARY"} log.txt
#4.
	awk '{print $1, $2}’ log.txt
#5.
	awk -F “,”  ‘{print $1, $2}’ log.txt
#6. 
	awk ‘{count[$2]++} END {print count["ERROR"]}' log.txt
#7 
	awk '{ if ($1> 1598863888) {print $8} } log.txt

```
---
### `chmod`


---
### `--help`
it’s used to get all the info about a command.

```bash
<command_name> --help
#try -
cd --help
ls --help
```

---
### `which`
To check where binary or command lives! Just use `which` command.

```bash
which <command_nmae>
#try -
which ls
which mv
which cp
```

---
### `history`
it’s used to retrieve the history of commands that were used on the system previously

```bash
history
```
