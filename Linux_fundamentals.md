Linux architecture

<img width="845" height="776" alt="Screenshot 2025-08-27 at 7 03 49 PM" src="https://github.com/user-attachments/assets/9db838ae-c8c4-4c20-b84e-fab9703de354" />

OS : Software which you load on your hardware to make it do things.

Kernel: The Linux kernel acts as a bridge between hardware and applications, managing crucial system tasks like CPU scheduling, memory allocation, device I/O, and process execution.

Shell: Interface between user and OS. On CLI you can give one or couple of instrucations at a time, by using script you can giv multiple instructions at a time.

<img width="797" height="448" alt="Screenshot 2025-08-27 at 6 28 06 PM" src="https://github.com/user-attachments/assets/a4389a7b-2885-4257-8d52-a3f3826b266a" />

Root (/)
Root of all file system. All files/folders start from here. It is super user and has access to entire file system.

/bin
All the binaries for essential command which are needed for OS to run are stored here.So ls, curl, cd all these commands the code is kept in bin.

/sbin
Contains system binaries that are used by root user only. (fdisk, shutdown) 
 
/lib
When your system is starting/booting there are certain set of s/w needed for booting OS thise logics are kept in library.

/home
Linux can have multiple users, so the user data is stored in home directory. So, per user data is stored here. Each user gets a folder where, for example, your path will be /home/ubuntu, where ubuntu is your user.
Verdict: Correct. /home indeed holds personal directories for each user, e.g., /home/ubuntu. 

/etc
It contains system-wise files and details. Our username, password, and configuration files for user and system-wide are stored here. It is like settings in windows. It also has network configuration and mount config.
Verdict: Mostly correct. /etc holds host-specific system configuration files — including user and hostname data, network, and mount configurations like /etc/fstab. Think of it as the system’s central settings hub. 

/opt
If you want to install Chrome, third-party tools or software that you are installing, those will be coming under opt directory. Opt means optional.
Verdict: Correct. /opt is used for optional, add-on software packages and third-party apps.

/var
Variable data. Whatever events you are doing, the logs of it are stored in this directory. The system and application logs are stored here. It is an important directory for debugging and error solving. Cache emails are also stored here.
Verdict: Correct. /var stores variable data—logs, caches, emails, spools—that change frequently. This is a key location for troubleshooting.

/tmp
It is a temporary directory. It can be used by all users. There are some restrictions, but it is a common directory for all the users created in the system. Anything here can be deleted after reboot as it is temporary.
Verdict: Correct. /tmp is for temporary files, accessible by all users, and generally cleared on reboot. 

/usr
Unix system resources. It keeps the binaries or software that are only a certain set of users. For example, you have installed Chrome, then your custom software are stored here. Vim etc. will also be coming here. Binaries that are stored here.
Verdict: Mostly correct: /usr is a secondary hierarchy for (mostly) read-only system software and utilities, shared among all users. Your examples like Vim fit well here. 

/dev
Represents devices as files. For example, /dev/sda. /dev/tty means terminal.
Verdict: Correct. The /dev directory contains device files corresponding to hardware like disks (/dev/sda) and terminals (/dev/tty). 

/mnt and /media
Places where external devices, USBs get mounted.
Verdict: Correct. /mnt is commonly used for manually mounted filesystems, while /media is for automatically mounted removable media like USB drives. 

/proc and /sys
These are special virtual directories that shows system info, like running processes, CPU, memory, etc.
Verdict: Correct. /proc and /sys are virtual filesystems: /proc shows process and kernel info, /sys provides device and kernel parameters.

---
Linux file system-
In simple terms, the Linux file system is like a giant tree that holds all the files and folders in the computer, starting from a single place called the root, written as /.

How It Works
One Big Tree: Imagine a tree with a trunk (the root /). Branches grow from it, like main folders (/home for users, /etc for settings), and leaves are the files.

No Drive Letters: Unlike Windows with C: and D:, Linux puts everything together into this one tree. Hard drives, USB sticks, and more--all their files fit under this same root.

Everything is a File: In Linux, not just documents are files, but things like printers and parts of the computer itself act like files too.

Folders for Jobs: Each important folder has a special job, like /home for personal stuff, /bin for programs, /tmp for temporary files, and /etc for computer settings
