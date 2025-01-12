The Linux File Hierarchy Structure or the Filesystem Hierarchy Standard (FHS) defines the directory structure and directory contents in Unix-like operating systems. It is maintained by the Linux Foundation. 

![linux-file-struct.png](linux-file-struct.png)

---
### 1. root (/)
Primary hierarchy root and root directory of the entire file system hierarchy.

- Every single file and directory starts from the root directory.
- The only root user has the right to write under this directory.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image.png)
In the beginning, every user is under under `~` (user) directory, we need to use `cd /` to go back to the root directory

---
### 2. /boot
it contains the files needed to boot the system, such as the Linux kernel itself etc.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%201.png)

---
### 3. /bin
it contains binaries executables that are essential to the entire operating system. Users can run them from the terminal at any time.

commands such as `cat`, `ls`, `curl`, `vim` etc.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%202.png)

![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%203.png)
To check where binary lives! Just use `which` command.

---
### 4. /sbin
It contains system binaries that can be executed by the root user only.

commands such as `mount`, `deluser`, `reboot`, `init` etc.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%204.png)

---
### 5. /lib
many binaries(/bin or /sbin) share common libraries, which are stored in this directory.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%205.png)

---
### 6. /dev
stands for device files, here users can interact with hardware or drivers as if they are regular files. We can create disk partitions and many more.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%206.png)

---
### 7. /home
as an OS linux can support many users. In this directory, we can directories of registered users. It contains files, config, software for that particular system.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%207.png)

---
### 8. /usr
Secondary hierarchy for read-only user data; contains the majority of (multi-)user utilities and applications.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%208.png)
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%209.png)

---
### 9. /var
it contains variable files that will change as a user uses the OS. It contains `log`, `crash`, `cache` files.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%2010.png)

---
### 10. /opt
it contains optional application software packages. User barely interact with them
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%2011.png)

---
### 11. /tmp
it contains temporary files created by system and users.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%2012.png)

---
### 12. /etc
Contains configuration files required by all programs. also contains startup and shutdown shell scripts used to start/stop individual programs.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%2013.png)

---
### 13. /proc
this directory does not actually exist on disk but is created in memory on the fly by the system(linux kernel) to keep track of the running processes.
![image.png](public/Linux%20File%20structure%201415cb8f372280aeb4b3ddb0deaaa02b/image%2014.png)