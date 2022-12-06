Todo: The first couple lectures

# 2. Download, Install and Configure

## 19. Linux Installation (CentOS)

- chose GUI server in the mode, the minimal installation does not install the GUI
- ethernet **ON**
- in **network & hostname** click on configure and check automatically connect

## 26. Linux Desktop GUI

- linux will be installed with **GNOME** or **KDE**

## 27. Oracle VM management

- most corporates run on Virtual environment
- setup **bridged adapter likely**

## 28. Linux vs Windows

- Linux
  - free
  - not user friendly
  - very reliable
  - often runs for months or years
  - mostly enterprise level software
  - best for multi-tasking
  - very secure
- Windows
  - user friendly
  - not free
  - often requires reboot
  - much larger selection of software
  - multi tasking is available but with very high cpu or memory resources
  - no open source

## 29. Who uses Linux

- US government and Agencies

## 30. Keyboard Keys used in Linux

- **Escape**
  - escape editors or previously pressed keys
- **~** 
  - takes you to your home directory
- **`** 
  - backword
- **!**
  - bang
- **@**
  - at
- **#**
  - hashtag
  - used to coment out things not used
- **$**
  - variable in scrypts
- **^**
  - cap
  - carrot
  - anything at the beginning of something
- **&**
  - put something in the background
- asterisk
- **{**
  - open parenthesis
- **_**
- **-**
  - hyphen
  - dash
- **tab**
  - skips few spaces
- **{}**
  - curly braces
- **:**
  - :wq saves the file
- **|**
  - pipe
  - used to combine commands together
  - take the output from first command and give it to the second command
- \
  - backslash
  - to specify the path
- **< and >**
  - input and output
  - first means appending to the file
  - second overwrites the file
- **/**
  - used in linux to access to path
- **Right control key**
  - release mouse from the window

# 3. System Access and File System

## 34. Command prompts

`username@hostnamePromptsymbol` 

- Hashtag at the end means youre logged as root
- other users see a dollar sing
- to get prompt back press **ctrl + C**
- `whoami` gets username
- `hostname` shows the host

## 35. Accessing Linux System

- Each OS has a different client or protocol
- Windows has **Remote Desktop (RDP)**
- VMware ESX has vSphere client
- Linux has **Putty, SecoureCRT**
  - Putty has a terminal
  - SSH from Linux to Linux
    - if youre already in a linux machine
    - you can just use SSH followed by the ip address
    - Port 22 is for SSH

## 36. Install Putty

- on a linux you can just connect through a terminal and a command
  - `ssh -l [username] [ipaddress]`

## 37. New Network Commands

- `ifconfig` used in CentOS
- `ip` replaced ifconfig because `ifconfig` has been depricated
- `ip addr` lists all the available IPs you have
- to use `ifconfig` install **net-tools** package
- `ifup enp0s3` activates the host only connection under root when we have host only active in virtualbox
- put the ip address to the putty

## 39. Important Things to remember in Linux

- linux has super user account **root**
  - can remove and delete accounts and make changes to system config files
  - linux is case sensitive system
  - avoid using spaces when creating files and directories
  - linux kernel is not an operating system. It is a small software within linux that takes commands from you and passes them to hardware and peripherals
  - Linux is mostly CLI not GUI
  - Linux is very flexible compared to other systems

## 40. Introduction to Linux File system

- / - root
  - **boot** - files used by the bootloader (grub.cfg) - first thing the system looks for
  - **root** - root user home directory (its not the same as /)
  - **dev** - system devices (disk, speakers, flashdrive, keyboard, etc.)
  - **etc** - configuration files. Anytime you change something here make a backup
  - **bin or /usr/bin** in new versions. Everyday user commands
  - **sbin or /usr/sbin** - system or filesystem commands
  - **opt** - optional add-on applications (not part of OS apps)
  - **proc** - Running processes (only exists in Memory). When you shut down the system this will be empty.
  - **lib or usr/lib** - where all C programming library files needed by commands and apps
  - **tmp** - directory for temporary files
  - **home** - directory for user
  - **var** - used for system logs
  - **run** - system demons that start very early to store temporary runtime files like PID files
  - **mnt** - used to mount external filesystem (e.g. NFTS)
  - **/media** - for cdrom mounts (or shared folders)

## 42. File System Navigation Commands

- `cd` - change directory
- `pwd` - print working directory
- `ls` - list
  - anything that starts with _ is a folder, anything starting with **d** is a directory
- `su -` - to become root
- `clear` - clear the screen
- `cd` - puts you to user directory

## 43. What is root?

There are 3 types of root on linux

1. Root account: the most powerful acc. Like admin acc that has access to all commands and files
2. Root as directory (/) - the very first directory in Linux.
3. Root home directory - the root user account also has a directory located in /root

## 44. Absolute and Relative Paths

- absolute path always begins with a /. It starts at the root directory.

## 45. Directory listing attributes

- when doing `ll`
  - first field is a type
    - **d** is a directory
    - **l** is a link
    - **-** regular file
  - second field tells you about the number of links of that directory
  - third one is the **owner**
  - 4th one is a group owning a directory
  - size
  - month
  - day
  - time
  - name

## 46. Creating Files and Directories

- Files
  - **touch**
  - **cp**
  - **vi**
- Directories
  - **mkdir**

- `ls -ltr` lists everything in the directory in the order in which it was created
- `touch [filename]` create a filename
- `cp [filename] [newfilename]` 
- `vi [filename]` - create a file 
- `touch [filename1] [filename2] [filename3]` 
- `mkdir [dirname]`
- `mkdir [filename1] [filename2] [filename3]`

## 47. Copt directories

- **cp -R**
- `cp -R [dirname] [newdirname]`

## 48. Linux file types

1. **-** a regular file
2. **d** directory
3. **l** link
4. **c** special file or device
5. **s** socket
6. **p** named pipe
7. **b** block device

## 49. Finding files and directories

- **find**
- **locate**

- `find . -name "filename"`
  - look for a file with a name starting from local directory
- `locate [filename]`

## 50. Difference between find and locale

- **locale** 
  - uses prebuilt db which should be regularly update
  - can be innacurate if its not updated
  - much faster
  - `updatedb` command updates the db. Otherwise os updates it itself after some time.
- **find** 
  - iterates over a filesystem to locate files

## 51. Changing password

- you should change the initial password as soon as you login
- `passwd userid` 
  - if asks you for your old password
  - then it asks you for your new password
  - reconfirm the new password
  - if you just type it without the userid it changes passwd of the current user

## 52. Wildcards

- ***** - represents zero or more characters
- **?** - represents a single character
- **[]** - represents a range of characters
- \ - escape character
- **^** - beginning of the line
- **$** - end of the line
- `touch abc{1...9}-xyz`
  - creates 9 files named accordingl
- `ls -l abc*`
  - list all the files starting with abc
- `rm abc*`
  - removes all the files starting with abc
- rm *xzy`
  - remove all files ending with xyz
- `ls -l *[cd]*`
  - list everything that has c or d in the name

## 53. Soft and Hard Links

- **inode** - pointer or number of a file on the hard disk
- **soft link** - link will be removed if file is removed or renamed
- **hard link** - deleting renaming or moving the original file will not affect the hard link
  - hard links only work within the same partition
- you cannot create a link within the same directory with the same name
- `ln` creates hard link
- `ln -s` creates a soft link
- `echo "hulk is a  superhero" > hulk`
  - write phrase hulk is a superhero to a file hulk
- `echo '123' >> hulk` 
  - append a phrase, do not overwrite
- `ls -li` list inedoes

# 4. Linux fundamentals

## 57. Linux command syntax

- usually **command option(s) argument(s)**
- **options** 
  - modify the way the command works
  - usually consists of a dash followed by a single letter
  - some commands accept multiple options which can usually be grouped together after a single hyphen
- **arguments**
  - most commands are used together with one or more arguments
  - some commands assume a defualt argument if none is supplied
  - arguments are optional for some commands and required by others
- `ls -lt` 
  - list all the content by the time
- `ls -ltr`
  - list all the newest files at the bottom
- `ls -l bart`
  - list a file bart
  - **bart** is an argument here
- `man [command]` will always list all the oiptions etc.

## 58. File and directory permissions

- **File permissions**
  - UNIX is a multi-user system thats why the protection is necessary
  - to access a directory you need to have executable right
  - Permission for a file or directory may be restricted to by types
    - **r** - read right
    - **w** - write right
    - **e** - execute right
  - each permission can be controlled at three levels
    - **u** - user level
    - **g** - group level
    - **o** other (everyone on the system)
  - command to change permission
    - **chmod**
  - `chmod g-w jerry` 
    - remove the write right for the group for the file jerry
  - `chmod a-r jerry`
    - remove read permission for the file jerry for all
  - `chmod u+rw jerry`
    - give the user right for read and write
  - `chmod o+r jerry`
    - give the oether right to read

## 59. File Permissions: Using numeric mode

- `chmod ugo+r [file]` == `chmod 444 [file]`
- **Permission types**
  - 0 - no permission
  - 1 - execute
  - 2 - write
  - 3 - execute + write
  - 4 - read
  - 5 - read + execute
  - 6 - read + write
  - 7 - read write execute

## 60. File Ownership

- there are 2 owners of a file or directory
- **user** and a **grouo**
- **chown**
  - changes the ownership of a file
- **chgrp**
  - changes the group ownership of the file
- **-R** 
  - do the same for the recursive directories.
- `chown root [filename]`
  - changes the ownership to root
- `chgrp root [filename]`
  - change the group to root
- reardless of the file rights, if you own the parent directory you have the rights for that directory anyways

## 61. Access Control List (ACL)

- additional, more flexible permission mechanism for file systems. It allows you to give permissions for any user or group to any disc resource.
- classic for scenarios when member is not a member of a group but still needs access.
- **setfacl** and **getfacl**
- `setfacl -m u:user:rwx /path/to/file` 
  - add permission for user
- `setfacl -m g:group:rw /path/to/file`
  - add permission for a group
- `setfacl -Rm 'entry' /path/to/dir`
  - allow all files or directories to inherit acl entries from the directory it is within
- `setfacl -x u:user /path/to/file` 
  - remove a specific entry for a specific user
- `setfacl -b path/to/file`
  - remove all entries
- ass you assign ACL permission, it will add + sign at the end of the permission
- setting w permission with ACL does not allow to remove a file

## 62. Help commands

- `whatis [command]`
- `[command] --help`
- `man [command]`

## 63. Tab completion and arrow keys

- **Tab** completes the available commands, files or directories
- **Up arrow key** returns the last ran command
- `date` gives you  date of your system

## 64. Adding Text to Files (Redirects)

- **vi** - vi editor. It is a command that is used to create a file and add text to it.
- redirect command output **>** or **>>**
- **echo >** or **>>**
- `echo [phrase] > [filename]` write the phrase to that name
- `cat [filename]` read the file
- `echo [phrase] >> [filename]` append the line to the file
- `ll > [filename]` collect the output of the command and parse it to the file
- `date >> [filename]` append the output of a command to a file

## 65. Input and output redirects

- **stdin** standard input - number is 0
  - input is used when feeding file contents to a file
  - e.g. `cat < [filename]`
  - `mail -s "office memo" addres@gmail.com < [filename]`
- **stdout** standard output - number is 1
  - by default when running a command the output goes to terminal
  - it can be routed to a file using **>** sign
- **stderr** standard error - number is 2
  - when a command is executed we use a keyboard that is also considered stdin (0)
  - that command output goes to the monitor and that output is stdout (1)
  - if the command produced error on the screen, then its considerred stderr (2)
  - we can use redirects to route errors from the screen
  - e.g. `ls -l /root 2> [errorfilename]`
- `ls -la` give all the contents of the current directory including the hidden files (those that have .. in front of it)



## 66. Stdout to a file (using <u>tee</u> command)

- **tee** is used to store and view the output of a any command
- it coppies the the output of a program to a file and at the same time displays it
- `echo [phrase] | tee [filename]` display output and store it to a filename
- `echo [phrase] | tee -a [filename]` append the output instead\

## 67. Pipes

- used by a shell to connect the output of one command directly to the input of another command
- `command [arguments] | command2 [arguments]`
- `ll | more`
  - **more** makes a long output as pages
- `ll | tail -1`
  - **tail** returns the last x lines of a output

## 68. File Maintanance commands

- **cp** - copies a file
  - `cp [oldfilename] /path/filename`
- **rm** - remove
- **mv** - move a file
  - `mv [filename] [newfilename]` rename a file
- **mkdir** - make a directory
- **rmdir** or **rm -r** or **rm -Rf**
- **chgrp** - change group ownership
  - `chgrp [newowner] [file]`
- **chown** - change ownership at the user level
  - `chown [newowner] [filename]`


## 69. File display Commands

- **cat** - views the entire content
- **more** - views the content as a one page at a time
  - `more [filename]`
- **less** - views the content one page at a time in a reverse order
  - `less [filename]`
- **head** - view just top couple of lines
  - `head -2 [filename]` sees the first two lines
- **tail** - view just bottom couple of lines
  - `tail -2 [filename]` sees the last two lines of the file

## 70. Filters / Text Processors Commands

- **cut** cuts the output
- **awk** lists by the columns
- **grep** and **egrep** searches by a keyword
- **sort** sortys the output in alphabetical order
- **uniq** does not show any duplicates if there are any duplicates
- **wc** word count command

## 71. cut command

- cuts a parts of lines or piped data by position, delimiter and characters
- `cut -c1 [filename]` prints only first characters
- `cut -c1,2,3 [filename]` prints only first, second and third characters
- `cut -c1-3 [filaneme]` the same
- `cut -c1-3,6-8 [filename]`
- `cut -d:- -f 6 [filename]`
  - delimiter will be dash and we want sixth field
- `ls -l | cut -c2-4`
  - take the ouput of the list as an input

## 72. awk command

- utility designed for data extraction, usually fields.
- `awk '{print $1}' [filename]`
  - print first column of a file
- `ls -l | awk '{print $1, $3}'`
- `ls -l | awk '{print $NF}'`
  - get the last column of the output
- `awk '/[word]/ {print}' filename`
  - print first occurrence of the word
- `awk -F: '{print $%1}' [filename]`
  - outputs ony first field of a file
- `echo "Hello Tom" | awk '{$2="Adam"; print $0}'` 
  - replace the second column with Adam and print everything you find
- `awk 'length($0) > 15' [filename]`
  - print lines with more than 15 bytes
- `ls -l | awk '{print NF}'`
  - print number of columns

## 73. Grep Command

- global regex print
- processes text line by line and prints lines that match the pattern
- its basically a search
- `grep [phrase] [file]` searches the phrase in the file
- `grep -c [phrase] [file]` returns the count of the findings
- `grep -i [phrase] [file]` ignore case
- `grep -n [phrase] [title]` return line numbers
- `grep -v [phrase] [title]` lines that do not include the phrase
- `ls -l | grep Desktop` only search for Desktop file
- **egrep** when you want to search two words from a file
- `egrep i "[phrase1|phrase2]" [file]` searches for either phrase one or phrase two

## 73. sort / uniq commands

- **sort** 

  - sorts in alphabetical order
  - `sort [file` sorts lines alphabetically]
  - `sort -r [file]` sorts in reverse order
  - `sort -k2 [file]` sorts by second column
  - `ls -l | sort -k9` sort by the last column

- **uniq**

  - filters repeated or duplicated lines
  - `sort [file] | uniq` eliminate duplicates

  - **always sort** the file before the uniq applicatio
  - `sort [file] | uniq -c` give me the count
  - `sort [file] | uniq -d` give me the duplicate lines

## 75. wc command (word count)

- reads input or list of files and generates **newline count, word count and byte count**
- `wc [file]` - return newline count, word count and byte count
- `wc -l [file]` 
- `wc -w [file]` 
- `wc -c [file]` - return bytes
- **wc** is not allowed on directory
- `ll | wc -l` return the number of files and directories (-1)

## 76. Compare files (diff and cmp)

- **diff**
  - compares two files line by line
  - `diff [file] [file2]` return the difference
- **cmp**
  - compare two files byte by byte
  - `cmp [file] [file2]`

## 77. Compressing and uncompressing files

- **tar**
  - take a bunch of files and put them in one container
  - `tar cvf [name].tar .` - put everything in the directory into name.tar file
  - `tar xvf [name].tar` - extract the file
- **gzip**
  - compresses a file
  - `gzip [fi;e]` compress the file into gz
- **gzip -d** or **gunzip**
  - `gzip -d [file]` uncompress it

## 78. Truncate file size

- **truncate**
  - shrink or extend the size of a file to the specified size
  - it chops the file into the specified size
  - `truncate -s 10 [file`] - reduce the file to the 10 bytes size
    - this can also be used to make it bigger

## 79. Combining and splitting files

- multiple files can be combined into one
- one file can be split into multiple files
- `split -l 2 [file] [filename]` split file into filenamea, filenameb, filenamec, etc for every two lines
- `cat [file1] [file2] [file3] > [file4]` combines files

## 80. Linux vs Windows commands

- **dir / ll**
- **ren** / **mv**
- **copy / cp**
- **move / mv**
- **cls / clear**
- **del rm**
- **fc / diff**
- **find / grep**
- **command / ?** / **man command**
- **chdir / pwd**
- **time / date**

# 5. System Administration

## 84. File Editor

- vi
- ed
- ex
- emacs
- pico
- vim
- **vi**
  - **i** - insert
  - **Esc** - escape out of any mode
  - **r** - replace
  - **u** - bring back changes
  - **x** - remove character
  - **d** - delete
  - **/phrase** - search for the phrase
  - **a** - advance to the next space
  - **o** - create a new line
  - **:q!** - quit without saving
  - **:wq!** - quit and save
    - also can be done with **shift + zz**

## 85. Difference between vi and vim editors

- learning vim is much easier
- **vim** has extra
  - completion
  - spell check
  - comparison
  - merging
  - unicode
  - regex
  - scripting languages
  - plugins 
  - gui
  - folding
  - syntax highlighting
- **vim interactive learning tools**
  - www.openvim.com
  - www.vimgenius.com
  - www.vim-adventures.com - teaches through games


## 86. sed command

- replace a string in a file with a newstring'
  - `sed -i's/[phrasetoreplace]/[replacingphrase]/g [file]`
    - s for substitute
    - g for global
    - i for insert into the file
  - `sed -i 's/[phrasetoremove]//g' [file]`
    - to remove words
- find and delete a line
- remove empty lines
- remove n lines in a file
- replace tabs with spaces
- show defined lines from a file
- substitute within vi editor
- ...

## 87. User Account Management (useradd, groupadd, usermod, userdel, groupdel)

- **useradd**
  - `useradd -g superheroes -s /bin/bash -c "user description" -m -d /home/spiderman spiderman`
    - g to add a group
    - s to give shell environment
    - c for user description
    - m and d to define home directory and the user itself
  - `id [user]` checks whether the user is created
    - you can also verify by checking the home directory
- **groupadd**
  - `groupadd [groupname]` adds a group
  - `cat /etc/group` checks the groups
- **userdel**
  - `userdel [user]` deletes user
  - `userdel -r [user]` deletes the user and its home dir
- **groupdel**
  - `groupdel [group`]
- **usermod**
  - modifies the users
  - `usermod -G [groupname] [username]` adds user to the group
    - verify by `grep [username] /etc/group`
- `passwd [user]` lets you specify a password for an user

Files

- **/etc/passwd**
- **/etc/group**
- **/etc/shadow** 
  - for passwords etc

## 88. Enable Password Aging

- `chage [-m mindays] [-M maxdays] [-d lastday] [-I inactive] [-E expiredate] [-W warndays] user`
  - min is minimum number of days between password changes
  - max is maximum amount of days, the user has to change the passwd afterwords
  - Warn is the number of days before password is to expire that user is warned that his/her password must be changed
  - Inactive - the number of days after password expires that account is disabled
  - expire - days since Jan 1, 1970 that account is disabled when the login may no longer be used
- **/etc/login.defs** is a file where you can set defautl aging values when you create new values
  - UMASS specifies default permission when user creates a file
  - PASS_MAX_DAYS
  - PASS_MIN_DAYS
  - PASS_MIN_LEN
  - PASS_WARN_AGE
- **chage** command
  - used to set parameters around the password

## 89. Switch users and sudo access (su, sudo)

- sudo access is a command that allows ordinary user run root level commands
- `su - [user]` - switches from one user to another
- `sudo [command]`- run command if you dont wanna become a root
- `visudo` - edits the **etc/sudoers** config file that allows user add or remove rights for certain commands
- root can switch to another user without authentication0

## 90. Monitor Users

- **who**
  - how many people are loggin, their id and the time of the login
- **w**
  - works the same as who but gives a bit more information
- **last**
  - details of users logged in since the day 1
- **finger**
  - program you have to add
  - traces a user
  - `yum install finger -y`
  - 
- **id**
  - `id [user]`returns the info about the user. (including the groups etc)

## 91. Talking to Users

- **users**
- **wall**
  - broadcast to all users logged in
  - `wall`, press enter, write a message, send with ctrl + D
- **write**
  - broadcast to a one user
  - `write [user]`, hit enter, write a message, send with enter.

## 92. Linux Account Authentication

- Types of Accounts
  - Local accounts
    - created in linux machine
  - Domain/Directory accounts
    - authenticated via server
- Windows has **active directory**
  - you create an account there and it gets authenticated
- Usually you use SSH to connect, or LDAP.

## 93. Difference between Active Directory, LDAP, IDM, WinBIND, OpenLDAP, etc.

- **Active Directory** 
  - for Microsoft
  - the information is not saved on the linux machine, but in some sort od db that is connected to the linux
- **IDM**
  - Identity manager
- **WinBIND**
  - Used in Linux to communicate with windows active directory
- **OpenLDAP** (open source)
- **IBM Directory Server**
  - developed by IBM and sold to the customers
- **LDAP**
  - lightweight Directory Access Protocol
  - just a protocol
  - you need protocol to communicate with any aforementioned services

## 94. Utility commands (date, uptime, hostname, uname, which, call, bc)

- **date**
  - show date and time of the system
- **uptime**
  - how long the system has been up and load average
- **hostname**
  - identify the system you are logged into
- **uname**
- **which**
  - gives you location of a command
  - `which pwd`
- **cal**
  - give me calendar
- **bc**
  - binary calculator

## 95. Processes, Jobs and Scheduling

- **Application**
  - Service that runs for your computer, like Powerpoint, Apache etc.
- **Script**
  - list of instructions
- **Process**
  - Starting application generates processs.
- **Daemon**
  - Something that continuously runs until interrupted.
  - It is also process.
- **Thread**
  - Every process could have multiple threads associated with it
- **Job**
  - Something that is supposed to run at a scheduled time

- for processes and services
  - we have **systemctl** or **service**
  - **ps** command
    - allows you to see processes running in Linux systems
  - **top** command
    - see all the processes running in  the system based on the load and memory, cpu information
  - **kill** command
    - kills the process by name or id
  - **crontab**
    - used to schedule services
  - **at**
    - like crontab, difference is that at is scheduled for one time bases.

## 96. systemctl command

- system control command
- used to start applications
- something like double click in linux
- `systemctl start|stop|status servicename.service` (firewall for example)
- `systemctl enable servicename.service`
- `systemctl restart|reload servicename.service`
- `systemctl list-units --all`
  - show all the processes that we can manage
- to add a service under systemctl management
  - create a unit file in **/etc/systemd/system/servicename.service**

## 97. Ps command

- process status
- kind of equivalent to the task manager in windows
- display all currently running processes in the linux system
- `ps` - shows the processes of the current shell
  - **PID** - the unique process ID
  - **TTY** - terminal type that the user logged-in to
  - **TIME** - amount of CPU in minutes and seconds that the process has been running
  - **CMD** - name of the command
- `ps -e` - shows all processes
- `ps aux`- shows all running processes in BSD format
- `ps -ef` - shows all processes in full format listing
- `ps -u [username]`= shows all processes by username

## 98. top command

- show linux processes and their real time view of the system
- refreshes the information every 3 seconds
- summary of information and list of processes managed by the Kernel
- you can exit the interactive mode by hitting **q**
- **PID** - process id
- **USER** - owner of the task
- **PR** - priority of a task
- **NI** - nice value of the task - negative value 
- **VIRT** - total virtual memory used by the task
- **RES** - memory consumed by the process in RAM
- **SHR** - represents the amount of shared memory used by a task
- **S** - shows the process state in a single letter form
- **CPU** - cpu usage
- **MEM** - memory usage
- `top -u [user]`- shows task/processes owned by a user
- `top and then press c`- gives absolute path of the processes running
- `top and press k`- kill process by pid within a session
- `top and press M and P`- list processes by memory usage

**99. Kill command**

- used to terminate processes manually
- sends a signal to kill a particular processes or group of processes
- **kill [OPTION] [PID]**
  - Option - signal name or signal number
  - pid - process id
  - [OPTION] is skippable to kill process directly
- `kill -l`- get a list of all signal names or numbers
- `kill [pid]`- kill process
- `kill -1`restart
- `kill -2`- interrupt from the keyboard like CTRL + c
- `kill -9`- forcefully kill the process
- `kill -15`- kill a process gracefully
- `killall`- kill all related process as well
- `pkill`- kills process by name

## 100. crontab command

- used to schedule tasks
- usage:
  - `crontab -e`lets you edit the crontab
  - `crontab -l`list the crontab entries
  - `crontab -r`remove the crontab
  - `crond`- ccrontab daemon/service that manages scheduling
  - `systemctl status crond`to manage the crond service
  - stopping the service means the cron does not execute them
  - columns:
    - minute
    - hour
    - day of the month
    - month
    - day of the week
    - command to execute

## 101. at command

- allows you to schedule a task but only once

- exit interactive mode by **Ctrl + D**

- Usage

  - **at HH:MM PM** = Schedule a job
  - **atq** = List the entries
  - **atrm #** = remove at entry
  - **atd status atd** = To manage the atd service

- Example

  - **at 4:45 PM -> enter** 

    **echo "This is my first at entry">  at -entry**

  - **at 2:45 AM 101621** = schedule a job to run on october 16 2021 at 2:45
  
  - **at 4PM + 4 days**
  
  - **at now + 5 hours**
  
  - **at 8:00 AM Sun**
  
  - **at 10:00 AM next month**

## 102. Additional Cron Jobs

- by default there are 4 different types of cronjobs
  - hourly
  - daily
  - weekly
  - monthly
- All the above crons are setup in **/etc/cron.__** (directory)
- timing of each are set in **/etc/anacrontab** (except hourly)

## 103. Process Management (bg, fg, nice)

- backgounrd = **ctrl-z** to stop a process, **jobs** to list jobs, and **bg** to move the process in the background
- foregrounf = **fg**
- Run process even after exit = **nohup process &**
  - nohup means dont send any kind of signal to stop it
  - or **nohup process > /dev/null 2>&1 &**
- **pkill** kills a process by name
- **nice** - process priority - e.g. **nice -n 5 [process]**
  - the scale goes from -20 to 19. The lower te number the more priority that task gets.
- process monitoring = **top**
- list processes = **ps**

## 104. System monitoring commands

- **top**
- **df** 
  - disk partition information
  - tells things file system
  - **df -h** - human readable
- **dmesg**
  - gives output of the system error messages
- **iostat 1**
  - what is going in and out
- **netstat**
  - shows connections and stuff
  - **netstat -rnv** for gateway information
- **free**
  - gives physical and virtual memory
- **cat /proc/cpuinfo**
- **cat /proc/meminfo**

## 105. System logs monitoring (/var/logs)

- another and the most important way of system administration
- **/var/log** = log directory
- **boot**
  - log when system boots up / reboots
- **chronyd**
- **cron**
- **maillog**
- **secure**
  - all login logout activity
- **messages**
  - everything
- **httpd**

## 106. System maintenance commands

- **shutdown**
- **init 0-7**
  - 0 to shutdown
  - 6 to reboot
  - 3 to multiuser mode
- **reboot**
- **halt**
  - shuts down the computer right away

## 107. Changing System Hostname

- `hostnamectl set-hostname newhostname`
- /etc/hostname is the file used to store hostname

## 108. Finding system Information

- **cat /etc/redhat-release**
  - gives info about os (version and distro)
- **uname -a**
  - also kernel version, version (64bit etc, build date, etc)
- **dmidecode**
  - info about processes, memory, etc

## 109. Finding system architecture

- differences between 32-bit and 64-bit CPU
  - number of calculations per second they can perform. 64 come in dual core.
  - usually prgrams operate more sufficiently on 64-bit processors.
- **arch**

## 110. Terminal control keys

- holding ctrl and pressing a key
- **u** = erase everything youve typed on the lcommand line
- **c** = stops / kills a command
- **z** = suspend a command
- **d** = exit from an interactive program

## 111. Terminal Commands

- `clear`= clears your screen
- `exit`= exit out of shell, terminal or user session
- `script`= stores terminal activities in a log file that can be named by a user.
- `script file-name.log`
  - `exit`exits the script process
  - useful when troubleshooting an issue or creating a script or smth.

## 112. Recover root password

- restart your computer
- edit grub
- change password
- reboot

## 113. SOS Report

- to collect and package diagnostic and support data
- package name that has to be installed
  - **sos-version**
  - `sosrepport`command to perform this report

## 114. Environment variables

- Dynamic named value that can affect the way running processes behave on a computer. They are part of environment in which a process runs.
- Its a set of defined rules and values to build an envronment
- to view all env variables run
  - ` printenv` or ` env` 
  - `echo $SHELL` to view one environment variable
- to set environment varlabies
  - `export TEST=1`
  - `echo $TEST` 
- to set environment variable permanently
  - `vi .bashrc`
  - `TEST='123'`
  - `export TEST` (also written in the file)
- to set global environment variable permanently
  - `vi /etc/profile or /etc/bashrc`
  - `Test='123'`
  - `export TEST`

## 115. Special Permissions with setuid, setgid and stick bit

- all permissions on a file or directory are referred as bits.
- they can be changed by **chmod** command
- **setuid **= tells linux to run a program with the effective user id of the owner instead of the executor.
- **setgid** = tells linux to run a program with the effective gid of the owner instead of the executor (e.g. **locate, wall**)
- **sticky bit** = a bit set on files / dirs that allows only the owner or root to delete those files
- To assign special permissions at the user level
  - **chmod u+s xys.sh**
- To assign a special permission at the group level
  - **chmod g+s xys.sh**
- To remove special permissions at the user or group level
  - **chmod u-s xys.sh**
  - **chmod g-s xys.sh**
- To find all executables in Linux with setuid and setgid permissions
  - **find / -perm /6000 -type f**
- these bits work on c programming executables. Not on bash shell scripts.
- **sticky bit**
  - assigned to the last bit of permissions
  - Why?
    - cannot delete the content of the directory with assigned sticky bit

# 6. Shell Scripting

## 119. Linux Kernel

- its an interface between hw and sw
- its a program that is stored inside of the OS that keeps running and takes commands from shell
- Shell and Kernel together form the operating system
- Shell and application together is Software

## 121. What is Shell

- its like a container
- interface between users and Kernel/OS
- CLI is a Shell
- to find shell you can
  - **echo $0**
  - **cat /etc/shells** = available shell
  - **/etc/passwd** = your shell
- Windows GUI is a shell
- Linux KDE GUI is a shell
- Linux sh, bash etc. is a shell

## 121. Types of Shell

- **Gnome** and **KDE** are GUIs and shell as well. You execute commands with your mouse.
- **sh** = a shell
- **bash** = a built upon sh, its sh with additional things. means **born again shell**
- **csh** and **tcsh** = using c syntax
- **ksh** = kornshell, most of the time used in solaris
- if you wanna know a list of shells you have available type **cat /etc/shells**

## 122. Shell scripting

- Shell script is an executable file containing multiple shell commands that are executed sequentially
- The file can contain
  - **Shell** (#!/bin/bash)
  - **Comments** (# comments)
  - **Commands** (echo, cp, grep, etc.)
  - **Statements** (if, while, for, etc.)
- shell script should have executable permission (e.g. -rwx r-x r-x)
- shell script has to be called from absolute path (e.g. /home/userdir/script.bash)
- if called from current location then **./script.bash**

## 123. Basics scripts

- **Output to screen**

```bash
#!/bin/bash

echo Hello World
```

- **Small tasks**

```bash
#!/bin/bash
# Define small tasks

whoami
echo
pwd
echo
hostname
echo
ls -ltr
echo
```

- **creating variables**

```bash
#!/bin/bash
# Example of defining variables

a=Honza
b=Ranostaj
c="Linux Class"

echo "My first name $a"
echo "My surname is $b"
echo "I study $c"
```

## 124. Input and Output of the script

- **read** - input
- **echo** - output

```bash
#!/bin/bash
# Author
# Date
# Desc
#

a=`hostname` # The ticks have to be here for a command
echo Hello, my server name is $a
echo
echo What is your name?
read namevar
echo Hello $namevar
echo
```

## 125. If-then scripts

```bash
#!/bin/bash

count=100
if [ $count -eq 100 ]
then
	echo Count is 100
else
	echo Count is not 100
fi
```

```bash
#!/bin/bash

clear
if [ -e /home/honza/error.txt ]
then
	echo "file exists"
else
	echo "file does not exist"
fi
```

## 126. For loops

```shell
#!/bin/bash

for i in 1 2 3 4 5
do
echo "Welcome $i times"
done
```

```bash
#!/bin/bash
for i in eat run jump prey
do
echo See honza $i
done
```

## 127. do-while scripts

- demons usually have **do-while scripts**

```bash
#!/bin/bash

count=0
num=10
while [ $count -lt 10 ]
do
echo
echo $num seconds left to stop this process $1
echo
sleep 1
num=`expr $num - 1`
count=`expr $count + 1`
done
echo
echo $1 process is stopped!!!
echo
```

## 128. Case Statement Scripts

```bash
#!/bin/bash

echo
echo Please chose one of the options below
echo
echo 'a = Display Date and Time'
echo 'b = List file and directories'
echo 'c = List users logged in'
echo 'd = Check system uptime'
echo
read choices
case $choices in

a) date;;
b) ls;;
c) who;;
d) uptime;;
*) echo invalid choice - Bye
esac # ends case statement
```

## 129. Check Other Servers Connectivity

```bash
#!/bin/bash
# Author: Honza
# Description: This script will ping a remote host and notify

hosts="/home/honza/ps/hosts"

for ip in $(cat $hosts)

do
        ping  -c1 $ip &> /dev/null
        if [ $? -eq 0 ]
        then
        echo $ip is OK
        else
        echo $ip is NOT OK
        fi
done
```

## 130. Aliases

​	Once you log off these aliases will be removed

- `alias l='ls -al'`
  - creates alias **l**
- `alias pl="pwd; ls"`
- `alias tell="whoami; ` 
- `alias tell="whoami; hostname; pwd"`
- ...
- `alias`
  - gives all the created aliases
- `unalias [aliasName]`
  - remove the alias

## 131. User and Global Alias

- **User** - applies only to a specific user profile
  - `/home/user/.bashrc`
- **Global** - applies to everyone who has account on the system
  - `/etc/bashrc/`

## 132. Shell history

Saved at **/home/user/.bash_history**

- `history`
  - get all the listings of the command ran by a specific user
- `history | more`
  - show as page
- `![number]` 
  - rerun a command [number] from history

## 135. Homework

- progress: 7 sections and 2 scripts

# 7. Networking, Services, System updates

## 136. Enable Internet on Linux VM

- to enable internet switch to **bridged adapter**



## 137. Network Components

- **IP** - internet protocol. Identifies computer in the site
- **Subnet mask** - 32-bit number that masks an IP address and divides the the IP into network address and host address.
- **Gateway** - which route to pick to send traffic in and out
  - the IP address of the modem is the gateway
- **Static vs DHCP**
  - static address is assigned dedicated IP address. Does not change on reboot
  - DHCP the address changes randomly every time the system reboots.
- **Interface**
  - its a port where you connect cable
  - this interface always has **MAC address** that never changes

## 138. Network Files and Commands

- Interface detection - cable.
- Interface config files
  - /etc/nsswitch.conf
    - tells the system where it should resolve the hostname
  - /etc/hosts
    - define system IPaddress and system hostname
  - /etc/sysconfig/network
    - specify your hostname here
  - /etc/sysconfig/network-scripts/ifcfg-nic
    - you can change BOOTPROTO to static and then define address and this way the IP address never changes
  - /etc/resolv.conf
    - specifies a DNS server

**Commands**

- **ping** - ping [IP] pings a server
- **ifconfig** - lists your interfaces in the system]
- **ifup** or **ifdown** - to bring interface up or down
- **netstat** - tells your gateway, traffic, interface, etc.
- **tcpdump** - traces transaction from and to your machine



## 141. NIC Information

- Network interface card (port where you connect the internet), the port is called NIC
- Examples:
  - `ethtool enp0s3`
- Other **NIC**s
  - **lo** - loopback device that your computer uses to communicate with itself. Mainly for diagnostics and troubleshooting and to connect to servers running on the local machine.
  - **virb0** - virtual bridge 0 used for Network Address Translation. Venv sometimes use it to connect outside network

## 142. NIC Bonding

- NIC Bonding (Network bonding) is aggregation or combination of multiple NIC into a single bond interface to provide high availability and redundancy.
- you can combine two interfaces together (via lectures, long procedure)
- `systemctl network restart` restarts the service 

## 143. New Network Utilities

- **Network manager**
  - service that provides a set of tools to manage networking config on Linux and is default network management service on RedHat 8
  - It makes network management easier
  - Provides easy setup of connection to the user
    - `nmtui` - **most important**
      - Network manager text user interface. Can be run within any terminal and allows changes to be made by making menu selections and entering data
    - `nmcli`
      - network manager command line interface, useful when access to GUI is not available and to make network config changes
      - `ncmli device status`- shows status of the device connection
      - `nmcli connection show --active`- shows status of the device active connections
      - `nmcli connection modify enp0s3 +ipv4.addresses 10.0.0.211/24`
      - `nmcli connection reload` - reload connection
      - `systemctl reboot`- reboot the system
      - `ip address show` - show IP addresses belonging to the interfaces
    - `nm-connection-editor`
      - Full graphical management tool providing access to most of Network Manager config options. It can only be accessed through the desktop or console
      - only available in the gui
    - **GNOME Settings**
      - The network screen of the GNOME desktop that allows basics network settings

## 144. Downloading Files or Apps (wget)

- **wget** - get from www.
  - `wget http://website.com/filename`
  - can be used to download packages for **yum** for example

## 145. curl and ping commands

- `curl http://www.google.com`
- `curl -O file.tar.gz`
  - downloads a file
- `ping http://www.google.com`
- `ping http:/www.google.com`

## 146. FTP - File Transfer Protocol

- **protocol** is a set of rules that tells computer how to communicate
- **default FTP port** is 21
- you have to install and configure FTP on the remote server
  - become root
  - `rpa -qa | grep ftp`
  - `ping www.google.com`
  - `yum install vsftpd
  - `vi /etc/vsftpd/vsftpd.conf`
    - **anonymous_enable=NO**
    - **ascii_upload_enable=YES**
    - **ascii_download_enable=YES**
    - **ftpd_banner=Welcome to UNIXMENT FTP service**
    - **use_localtime=YES**
  - `systemctl start vsftpd`
  - `systemctl enable vsftpd`
  - `systemctl stop firewalld`
  - `systemctl disable firewalld`
  - `useradd honza`
  - install FTP client on the server
    - become root
    - `yum install ftp`
    - `su - honza`
    - `touch fileName`
    - `ftp 192.168.1.x`
    - Enter username and password
    - bi
    - hash
    - put kruger
    - bye

## 147. SCP - Secure Copy Protocol

- transfer the files securely from local to a remote. Similar to FTP but adds security and authentication.
- default port is **22** (same as SSH).
- login as yourself
- `touch jack`
- `scp jack honza@192.168.1.x:/home/honza` 
- Enter username and password

## 148. rsync - Remote Synchronization

- utility for efficiently transferring and synchronizing files within the same computer or to a remote computer by comparing the modification times and sizes of files
- its a lot faster than ftp or scp
- mostly used to backup the files and directories from one server to another
- default port is **22** (same as SSH)
- basic syntax of the rsync command
  - `rsync [options] [source] [destination]`
- install rsync in your Linux machine
  - `yum install rsync` 
  - `apt-get install rsync`
- rsync a file on a local machine
  - `tar cvf backup.tar`  (tar the entire home directory)
  - `mkdir /tmp/backups`
  - `rsync -zvh backup.tar /tmp/backups/`
- rsync a file to a remote machine
  - `mkdir /tmp/backups`
  - `rsync -avz backup.tar honza@192.168.1.x:/tmp/backups`

## 148. System Updates and Repos (npm, yum)

- **yum** (CentOS)
  - go online and get the package
- **apt-get**
- **rpm** 
  - redhat package manager
  - when you already have the package downloaded and wanna install it locally



## 149. System upgrade / Patch Management

- two types of upgrades
  - Major version = 5, 6, 7
  - Minor version = 7.3 to 7.4
    - can be done through **yum update**
    - example: **yum update -y**
- yum update vs yum upgrade
  - **upgrade** deletes packages
  - **update** preserves the old package

## 150. Create a local repository

- **repository** is something where all your packages are stored
- if you dont have an internet access you can create a local repository

## 151. Advanced Package Management

- installing packages
- upgrading
- deleting
- view package details
  - `rpm -qf /usr/bin/pwd`- tells which package the command is associated with



## 152. Rollback Updates and Patches

- create a snapshot before updating or making significant changes if youre using VM
- in case of physical machines 
  - rollback a package or a patch
    - `yum install <package-name>`
    - `yum history undo <id>`
  - rollback an update
    - downgrading a system to a minor version is not recommended as this might leave the system in an undesired or unstable state.
  - `yum update`- will preserve packages
  - `yum upgrade`- will delete obsolete packages
  - `yum history undo <id>` - undoes a specific task you did



## 153. SSH and Telnet

- **Telnet** - old and unsecure connection between two computers
- **SSH** - secured, newer connection.
  - `ssh [ip]`connects to the computer
- Two types of packages for most of the services
  - client package
  - server package
- stopping **sshd** will prevent the server from receiving any more sessions

## 154. DNS

- **Domain Name System**
  - Hostname to IP (a record)
  - IP to Hostname (PTR Record)
  - Hostname to Hostname (CNAME Record)
- Files
  - **/etc/named.conf**
    - name is the name of the process of the DNS
  - **/var/named**
    - all the files where you define connections
- Service
  - **systemctl restart named**

Download, Install, Configure DNS

- Setup:
  - Master DNS
  - Secondary or Slave DNS
  - Client
- Domain Name = lab.local
- IP address = local on **enp0s3**
- Install DNS package
  - `yum install bind bind-utils -y`
- Configure DNS (Summary)
  - Modify **/etc/named.conf**
  - Create two zone files (**forward.lab** and **reverse.lab**)
  - modify DNS file permission and start the service

## 155. Hostname or IP Lookup

- **nslookup**
  - brings up own menu. You can type in address and it will return the IP.
- **dig**