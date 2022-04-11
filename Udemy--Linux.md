## 19. Linux Installation (CentOS)

- chose GUI server in the mode, the minimal installation does not instal the GUI
- ethernet **ON**
- in **network & hostname** click on configure and check automatically connect

## 26. Linux Desktop GUI

- linux will be installed with **GNOME** or **KDE**

## 27. ORacle VM management

- most corporates run on Virtual environment
- setup **bridget adapter likely**

## 28. Linux vs Windows

- Linux
  - free
  - not user friendly
  - very reliable
  - often runs for months or years
  - mostly enterprise level softwares
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