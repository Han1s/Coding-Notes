## 19. Linux Installation (CentOS)

- cjose GUI server in the mode, the minimal installation does not instal the GUI
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