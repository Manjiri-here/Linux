<img width="1152" height="1440" alt="image" src="https://github.com/user-attachments/assets/e0492829-e946-4824-9339-82c39207b201" />


Difference between lsblk and df -h:

$ lsblk      #Show me all disks and partitions.Block devices — physical or virtual storage hardware. It does NOT show usage.

$ df -h      # Mounted filesystems and their disk usage.Show me how much space is used/available on mounted partitions.

lsblk = lists disks/partitions (hardware).
df -h = shows mounted filesystems and their usage (space).

If you attach a new EBS volume:

lsblk will show it immediately.
df -h will NOT show it until you: format it and mount it

$ cut -d':' -f1

Explanation: 
cut → command to slice text.

-d':' → tells it use colon as the delimiter.

-f1 → tells it print only field 1 (the text before the first colon).

Example:
Input: user1:x:1000:/home/user1
Command prints: user1

✅ 1. Tasks
Tasks: 104 total, 1 running, 103 sleeping, 0 stopped, 0 zombie


104 total → Total number of processes on the system.

1 running → Only 1 process is actively using CPU.

103 sleeping → These processes are idle, waiting for input or events.

0 stopped → Nothing is paused.

0 zombie → Good. No defunct processes waiting for parent cleanup.

If you ever see zombies > 0 → it means parent didn't reap the child.

✅ 2. CPU Usage
%Cpu(s): 0.0 us, 0.0 sy, 0.0 ni, 100.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st


Breakdown:

us (user) = 0.0% → CPU used by your applications.

sy (system) = 0.0% → CPU used by kernel.

ni (nice) = 0.0% → CPU used by nice-priority processes.

id (idle) = 100.0% → CPU doing nothing.

wa (iowait) = 0.0% → CPU waiting for disk I/O.

hi (hardware interrupts) = 0.0%

si (software interrupts) = 0.0%

st (steal time) = 0.0% → Good. Hypervisor isn't stealing CPU cycles.

👉 Your CPU is basically idle. Nothing is using it.

✅ 3. Memory (RAM)
MiB Mem : 914.0 total, 219.7 free, 200.8 used, 493.5 buff/cache


Interpretation:

914 MB total RAM

200.8 MB used by apps

493.5 MB used for cache/buffers (this is NOT “wasted”—Linux caches aggressively)

219.7 MB actually free

👉 Key point:
Linux uses extra RAM for caching to speed things up.
If an app needs RAM, cache will shrink automatically.

So “used” doesn’t mean a problem unless available Mem is low.

✅ 4. Available Memory
546.7 avail Mem


This is the real number you care about.

546 MB is available to applications immediately.

👉 No memory pressure at all.


----

lsblk — Shows BLOCK DEVICES

It lists hardware-level devices: disks, partitions, LVM volumes.

It does not care whether they are mounted.

It tells you what exists physically/logically, not what is being used.

Think of it as: “What storage devices do I even have?”

Example output:

NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0 100G  0 disk
├─sda1   8:1    0   1G  0 part /boot
└─sda2   8:2    0  99G  0 part /

df -h — Shows FILESYSTEM USAGE

It lists mounted filesystems only.

Shows how much space is used/free.

Works at the filesystem layer, not hardware layer.

Think of it as: “How full are the mounted filesystems?”

Example output:

Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        99G   70G   20G  78% /

----

| Feature                                | `lsblk` | `df -h`   |
| -------------------------------------- | ------- | --------- |
| Shows hardware?                        | Yes     | No        |
| Shows filesystem usage?                | No      | Yes       |
| Shows unmounted devices?               | Yes     | No        |
| Shows actual disk layout?              | Yes     | No        |
| Good for troubleshooting mount issues? | Yes     | Partially |
| Good for checking free space?          | No      | Yes       |


----

Linux architecture

<img width="1690" height="1552" alt="image" src="https://github.com/user-attachments/assets/ebde1c94-ac67-4c93-914a-d69dce7af36a" />

<img width="1594" height="896" alt="image" src="https://github.com/user-attachments/assets/c7a00ac1-be97-410e-af30-2291f656b873" />


OS : Software which you load on your hardware to make it do things.

Kernel: The Linux kernel acts as a bridge between hardware and applications, managing crucial system tasks like CPU scheduling, memory allocation, device I/O, and process execution.

Shell: Interface between user and OS. On CLI you can give one or couple of instrucations at a time.

Root (/) Root of all file system. All files/folders start from here. It is super user and has access to entire file system.

/bin All the binaries for essential command which are needed for OS to run are stored here.So ls, curl, cd all these commands the code is kept in bin.

/sbin Contains system binaries that are used by root user only. (fdisk, shutdown)

/lib When your system is starting/booting there are certain set of s/w needed for booting OS thise logics are kept in library.

/home Linux can have multiple users, so the user data is stored in home directory. So, per user data is stored here. Each user gets a folder where, for example, your path will be /home/ubuntu, where ubuntu is your user. Verdict: Correct. /home indeed holds personal directories for each user, e.g., /home/ubuntu.

/etc It contains system-wise files and details. Our username, password, and configuration files for user and system-wide are stored here. It is like settings in windows. It also has network configuration and mount config. /etc holds host-specific system configuration files — including user and hostname data, network, and mount configurations like /etc/fstab. Think of it as the system’s central settings hub. But people encountered a situation to keep some files which can be a config file or a data file or a socket file or some other files. So they implemented a folder to keep all these files in it and they named it as /etc(As said earlier etcetera). As time passed the meaning of this folder has changed but not the name “etc”. Now /etc folder means a central location for all your configuration files are located and this can be treated as nerve centre of your Linux/Unix machine.

/opt If you want to install Chrome, third-party tools or software that you are installing, those will be coming under opt directory. Opt means optional. Verdict: Correct. /opt is used for optional, add-on software packages and third-party apps.

/var Variable data. Whatever events you are doing, the logs of it are stored in this directory. The system and application logs are stored here. It is an important directory for debugging and error solving. Cache emails are also stored here. Verdict: Correct. /var stores variable data—logs, caches, emails, spools—that change frequently. This is a key location for troubleshooting.

/tmp It is a temporary directory. It can be used by all users. There are some restrictions, but it is a common directory for all the users created in the system. Anything here can be deleted after reboot as it is temporary. Verdict: Correct. /tmp is for temporary files, accessible by all users, and generally cleared on reboot.

/usr Unix system resources. It keeps the binaries or software that are only a certain set of users. For example, you have installed Chrome, then your custom software are stored here. Vim etc. will also be coming here. Binaries that are stored here. Verdict: Mostly correct: /usr is a secondary hierarchy for (mostly) read-only system software and utilities, shared among all users. Your examples like Vim fit well here.

/dev Represents devices as files. For example, /dev/sda. /dev/tty means terminal. Verdict: Correct. The /dev directory contains device files corresponding to hardware like disks (/dev/sda) and terminals (/dev/tty).

/mnt and /media Places where external devices, USBs get mounted. Verdict: Correct. /mnt is commonly used for manually mounted filesystems, while /media is for automatically mounted removable media like USB drives.

/proc and /sys These are special virtual directories that shows system info, like running processes, CPU, memory, etc. Verdict: Correct. /proc and /sys are virtual filesystems: /proc shows process and kernel info, /sys provides device and kernel parameters.

Linux file system- In simple terms, the Linux file system is like a giant tree that holds all the files and folders in the computer, starting from a single place called the root, written as /.

How It Works One Big Tree: Imagine a tree with a trunk (the root /). Branches grow from it, like main folders (/home for users, /etc for settings), and leaves are the files.

No Drive Letters: Unlike Windows with C: and D:, Linux puts everything together into this one tree. Hard drives, USB sticks, and more--all their files fit under this same root.

Everything is a File: In Linux, not just documents are files, but things like printers and parts of the computer itself act like files too.

Folders for Jobs: Each important folder has a special job, like /home for personal stuff, /bin for programs, /tmp for temporary files, and /etc for computer settings

$ ls 

$ cd

$ pwd

$ mkdir

$ rmdir  ... removes directory if it is empty

$rm  .. removes file

$ rm -r .. removes directory recursively

$ rm -rf .. removes files/directory forcefully. f=forceflly, r=recursive

$ cp  .. copies file or directory

$ mv .. copies file or directory

$ cat .. displays content of a file
$ cat file1 file2  -- prints the contents of both the file on the terminal but keeps them as separate files(does not copy contents of them in any of the files)
$ cat file1 file2 > file3  -- prints contents of file1 and file2 and copies it to file3
$ cat file1 file2 >> file3  -- appends the contents of file3 means keeps the existing file contents same and then adds new on top of the contents

$ touch ... used to create a file

$ more file.txt  .. views contents of a file page by page

$ less ...same as more but allows backwards navigation and few more advantages. Hence **less** is preferred over **more**

$ head -n filename   ... displays first few lines of a file. By default it displays first 10 lines of a file, but you can specify number using -3, etc

$ tail -n filename       -- here -n means number of lines

$ nano filename   ... text editor like vi

$ vi filename .. text editor

$ uname .. displays kernel version , machine name
$ uname -r ... shows kernel version
$ uname -a .. shows kernel version
$ man uname

$ top ... shows list of system processes, Use top when the server is slow right now, or you need to see which process is currently abusing CPU or RAM.

You use <u>top</u> when:
1) You want to see which process is eating the CPU right now when the system has high latency (means when it is slow)
2) To check memory leak or RAM pressure
3) Debug a hung server
4) Check which user/process is consuming resources.

❌ When NOT to use top

Don’t use top for:
Historical data
Deep performance analysis
Network debugging
Disk forensic analysis
Memory leak root cause
App-level debugging

For these you use:
htop, ps, pidstat, vmstat, iostat, strace, dmesg.

$ df ... shows disk space usage of file system

$ df -h  ....shows disk space usage of file system in human readable format

$ free  -- shows memory usage

$ free -h 

$ uptime .. shows how long the system has been running

$ hostname .. shows the hostname

# 25 November 2025

>> Note: It is good practice to name log file with .log extension

Note: The default delimiter for awk is space or tab. If we want to any other symbol as delimiter then provide -F flag. For ex: awk -F ':' '{print $3 "\t" $5}'

1) head -n 5 file.log    # This prints the first 5 lines of the file
2) less file.log      # to read file, less command is easy to scroll up and down than more
3) awk '' file.log     # inside '' we write the operation we want to perform on file
For eg- $ awk '{print}' file.log    # this prints the whole file
$ awk '{print $1, $3, $4}' file.log  # prints only column 1, 3 and 4 of the file.
$ awk '/INFO/ {print $1 $3}' file.log     # prints lines which contains info
$ awk '/INFO/ {print $1 $3}' file.log > INFO.txt    # to send the output to INFO.txt file
$ awk '/INFO/ {count++} END {print "the count of INFO is: ", count}' file.log         .... prints the number of time INFO occurs in file.log
or we can also use:
$ awk '/INFO/' file.log| wc -l
$ awk '$2 >= "08:51:00" && $2 <= "08:51:59" {print $3}' file.log  -- Here we are putting filter on column 2 and then printing column 3(event) for it.
% awk '$2 >= "08:51:00" && $2 <= "08:51:59" {print $3, $2, $4}' file.log
% awk 'NR >= 2 && NR <= 10 {print $2}' file.log     -- here NR= number of rows..... It will print the second column ($2) of the file, but only for lines 2 through 10.
% awk 'NR >= 2 && NR <= 10' file.log   -- if we dont use print statement then it prints all rows

>> Note: AWK needs formated values, means either csv or tsv, column by column. If data is not formatted then use sed.

# SED (Stream Editor)

Syntax is similar: sed '' file.log

% sed -n '/INFO/p' file.log    # -n is used to match the exact INFO word or pattern, p is used to print

awk works on records which are structured (csv, tsc), while sed works line by line on any structured or unstructured data.

For eg. if you want to replace 'INFO' by 'LOG' then:

% sed 's/INFO/LOG/g' file.log   # here g is to replace word globally means throughout the file, while s is substring as we are replacing on a word from a string 

% sed -n -e '/INFO/=' -e '/INFO/p' file.log    # Here -e is for expression, it is used whenever we are using expression like '=' and -n is for exact match. It finds the lines with INFO word in it and also prints the line as well as line number (= is used to find line number)

% sed '1,10 s/INFO/LOG/g' file.log   # we want to replace string with INFO from lines 1 to 10 only, the we give range 1,10 as comma separated

% sed '1,15 s/INFO/LOG/g'; 1,10p; 11q file.log # means do the operation and also print the lines from 1 to 10 and quit from 11th line.

>> grep - global regular expression pattern , used when you want to match a word line or pattern from whole system or file then this is used

% grep INFO file.log   

% grep -i info file.log # -i is flag for case insensitive 

% grep -i -c info file.log  # also prints the count of lines which had info in them

# 27 November 2025

$ date 

$ ls -l

$ clear

$ echo "hello dosto" > demofile.txt   # the '>' redirects the output to demofile.txt 

$ echo "hello dosto" >> demofile.txt # the double '>>' modifies, means let the contents of demofile.txt be as it is and adds the text on top of it.

Note: In case you give a file name that doesnt exist then it will create a file and write contents in it.

$ zcat             # It is used to see the contents under zip file

Note: rmdir does not delete non-empty directores, it deletes only empty directories. So to delete non-empty directories rm -rf is used

% cp demo/file1 cloud/   # this copies file1 under demo folder to cloud folder

% cp -r demo/ cloud/   # this copies demo folder and its contents to cloud folder, hence -r flag is used to copy recursively.

% mv file1 ../demo     # If I want to copy a file to one directory behind

% mv cloud cloud_for_all   # rename file or even folder name in the same way , here folders are renamed. 

% wc file1                      # wc= word count, it gives you how many lines are there , how many words are there and what is size of file (in bytes generally)
6      20     107 file1         # here 6 lines, 20 words and 107 is the file size


# Soft link and hard link : Links are pointers to a file in different location.

Note: Soft link and hard links are like shortcuts in windows which we have on desktop. Similarly in linux soft link is the one where if we delete the main/source file then the soft link also gets deleted while hard link does not get deleted even when main file is deleted.

% ln -s linux/demo/file1 softlink_file1       # here softlink of file1 is created in softlink_file1 and when you try to print it you get exact same content. Like below. (-s = soft link)

You see l for softlink here in column 1:
lrwxr-xr-x@  1 manjiri  staff    16 27 Nov 13:25 softlink_file1 -> linux/demo/file1

 % cat softlink_file1
Today is sunny day
It is winter and November
Tomorrow I might have two interviews
hello hi

hello hi again

No if you change contents fo file in the main location or folder than it also gets reflected in the link created:

demo% echo "this file is changed" > file1
Devops% cat softlink_file1
this file is changed

Now if we delete the source file then the softlink will also be deleted, the file may exist in the list but it will error if you try to acces it - "cat: softlink_file1: No such file or directory"

$ ln linux/demo/file1 hardlink_file1       # This command creates hardlink
  Now even if you delete source file the link will not be deleted.

---

cut:remove sections from each line of files

% cut -b 1-2 hardlink_file1      # this cuts bytes(that is why -b flag) 1-2 or 1-4 and prints it.

% echo "hello there" | tee hello.txt      # Tee prints as something on screen as well puts in into a file, in case file does not exist it also creates the file.

% sort file1       # it sorts the contents aplhabetically

$ diff file1 file2     # It gives you difference between two files, and it can take only 2 files as input

$ rm -r .. removes directory recursively   # these -r, -f are flags

systemd -  The **service manager itself** (the engine)
systemctl`- The **command you use to control systemd** 


We can view two files side by side as below:

Command used: vi inventory_vars.yaml inventory.ini -O

<img width="1703" height="679" alt="image" src="https://github.com/user-attachments/assets/b401d307-40a4-4746-baa3-73ab7c551ecf" />

# 28 November 2025

$ df    # it is used to check how much storage is free and how much is occupied

$ du .   # disk utility, it is used to know which folder, folder under folder and files under it consume how much space/bytes

$ top      # gives all processes

$ ps     # gives info about only bash (sh) processes running

$ fuser   # try practicing this command

$ kill -9 <PID>     # you will get PID of processes using top

$ free -h    # gives information about RAM, how much used, how much free, etc

$ nohup df -h   # it saves output of this command to nohup file. Now even if you save something else or save output after an interval to nohup then it appends the file and doesnt replace its contents

$ head -n 5 nohup

$ tail -n 5 nohup

$ vmstat         # gives virtual machine stats, it gives RAM information

$ vmstat -a      # gives active and non-active ram as well

-----

29 November 2025

-----

$ uname          #gives you kernel 

| Command    | What it shows    | Why you care           |
| ---------- | ---------------- | ---------------------- |
| `uname`    | Kernel name      | Basic system check     |
| `uname -a` | Everything       | Full system identity   |
| `uname -r` | Kernel version   | Driver & compatibility |
| `uname -m` | CPU architecture | x86_64 vs arm64        |
| `uname -n` | Hostname         | Network identity       |

 % uptime                                                             # 
10:00  up 3 days, 11:27, 2 users, load averages: 2.39 3.45 3.54

% who      # gives list of users and who logged in and when, gives multiple user list and more details

% whoami    # gives the current that is effective username/id only. SO returns only 1 user only

% which terraform                 # gives the location of the application
/usr/local/bin/terraform

% id                       # gives you list of users and groups on the system
uid=502(manjiri) gid=20(staff) groups=20(staff),12(everyone),61(localaccounts),79(_appserverusr),80(admin),81(_appserveradm),701(com.apple.sharepoint.group.1),33(_appstore),98(_lpadmin),100(_lpoperator),204

Note: su = super user

So sudo is like making super user do the task as you do not have the permission. It gives you super user permission

% sudo cd root 

manjiri@Abhis-MacBook-Pro /var % shutdown
shutdown: NOT super-user

But we need to ask papa (the sudo) hence '% sudo shutdown' will work

$ reboot   # it wont reboot as it needs sudo permission

% sudo reboot   # will reboot now

apt, dnf, yum, pacman, portage

$ which docker   # it will answer your question of where dpcker is installed

$ sudo apt update

$ sudo apt update docker.io    # it is very necessary to run sudo apt update before you try to download any new application, else it will give error like ''
apt= application package manager

$ apt install docker.io    # this gives some error as it needs root permission
$ sudo apt update docker.io -y 

Similarly like apt is package installer for ubuntu, dnf is package manager for dnf for centos and rhel and fedora, yum is for centos and redhat, and pacman is for arch linux and manjaro  and portage is for gentoo flavour of linux

RHEL world → dnf / yum
Arch world → pacman
Gentoo world → portage
Redhat -> rpm

>> One of the reasons linux got famous is because we could add multiple users in it

Like in below image, there is a ghar/house which is like our system. sudo is the papa of the system, we need their permission to do anything. And ubuntu and jethalal are its users. We can create multiple users

<img width="972" height="585" alt="Screenshot 2025-11-29 at 19 07 39" src="https://github.com/user-attachments/assets/2bd706a4-37a2-4681-aaec-c6b1e12a6c02" />

How to create new user in linux: (User management in linux)

$ sudo useradd -m jethalal     # here -m is make a directory of this user, as linux follows file system heavily. So only when we provide -m the path like /home/jethalal will be created. Hence important to give that flag

# Now when we go to home directory and do ls we see list of users here

/home$ ls
jethalal  ubuntu

Now if we want to set password to this user then we can do it as below: 'we use passwd'

$ sudo passwd jethalal
New password:
Retype new password:
passwd: password updated successfully

Now if we want to switch user to jethalal then we do 'su' like below:

% su jethalal # and then it will as for password
Password:      # enter the password you set
$ whoami
jethalal

$ exit    # is used to exit the user

Now if you do 'cat /etc/passwd' the you will get the list of users and their id's, here id is 1001 for jethalal

ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
jethalal:x:1001:1001::/home/jethalal:/bin/sh

**Now in the below way you see id of users and the groups they are a part of** 

ubuntu@ip-172-31-71-36:~$ id

uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu),4(adm),24(cdrom),27(sudo),30(dip),105(lxd)
ubuntu@ip-172-31-71-36:~$ su jethalal
Password:
$ id
uid=1001(jethalal) gid=1001(jethalal) groups=1001(jethalal)

Now if we want to delete a user then below is way:

ubuntu@ip-172-31-71-36:~$ sudo userdel jethalal
ubuntu@ip-172-31-71-36:~$ su jethalal
su: user jethalal does not exist or the user entry does not contain all the required fields

** Now suppose we want to create 5 new users and assign 3 of them to dev group and 2 in QA group then follow below steps:

First of all create the users as below:

sudo useradd jethalal
sudo useradd babita
sudo useradd tappu
sudo useradd daya
sudo useradd bhide

cat /etc/passwd     # to get the list of users 
cat /etc/group      # and we can see groups using below command/path

sudo groupadd dev        # adding group
cat /etc/group         # to get the list of groups
  
sudo groupadd qa
cat /etc/group

% sudo gpasswd -a jethalal dev     # -a flag is to append the users and add user to group, so here we are adding jethalal to 'dev' group

   67  cat /etc/group                       
   69  sudo gpasswd -M babita,tappu  dev      # to add single user we use -a flag but to add multiple users we use -M
   70  cat /etc/group
       
   72  sudo gpasswd -M daya,bhide qa
   73  cat /etc/group
   74  sudo gpasswd -aG jethalal qa
   
   75  sudo usermod -aG dev jethalal          # if there exists some members in dev group and you want to add another user without deleting the list the this is also a way

   % sudo groupdel qa     # to delete a group

   # User permission:

   others : are users which are neither users nor the part of the group

   % umask   # used to check default file permission of a system

   If we have to change owner:

   ubuntu@ip-172-31-71-36:~$ sudo chown jethalal file1       # here we are changing owner of file1 to jethalal
   ubuntu@ip-172-31-71-36:~$ ls -l
   total 0
   -rw-rw-r-- 1 jethalal ubuntu 0 Nov 30 04:03 file1

ubuntu@ip-172-31-71-36:~$ sudo chgrp dev file1    # here we changed group to dev for file1
ubuntu@ip-172-31-71-36:~$ ls -l
total 0
-rw-rw-r-- 1 jethalal dev 0 Nov 30 04:03 file1

ubuntu@ip-172-31-71-36:~$ ls
file1  file2.txt  heythere
ubuntu@ip-172-31-71-36:~$ zip -r  zip.file heythere/                       # if 
  adding: heythere/ (stored 0%)
ubuntu@ip-172-31-71-36:~$ ls -l
total 12
-rw-rw-r-- 1 jethalal dev       0 Nov 30 04:03 file1
-rw-rw-r-- 1 ubuntu   ubuntu   37 Nov 30 04:11 file2.txt
drwxrwxr-x 2 ubuntu   ubuntu 4096 Nov 30 04:10 heythere
-rw-rw-r-- 1 ubuntu   ubuntu  168 Nov 30 04:12 zip.file
ubuntu@ip-172-31-71-36:~$ zip zip.file2 file1
  adding: file1 (stored 0%)
ubuntu@ip-172-31-71-36:~$ ls -l
total 16
-rw-rw-r-- 1 jethalal dev       0 Nov 30 04:03 file1
-rw-rw-r-- 1 ubuntu   ubuntu   37 Nov 30 04:11 file2.txt
drwxrwxr-x 2 ubuntu   ubuntu 4096 Nov 30 04:10 heythere
-rw-rw-r-- 1 ubuntu   ubuntu  168 Nov 30 04:12 zip.file
-rw-rw-r-- 1 ubuntu   ubuntu  160 Nov 30 04:13 zip.file2

1 Dec 2025

grep by default = basic regular expressions (BRE) → old, limited syntax
grep -E = extended regular expressions (ERE) → modern, powerful syntax
grep -E is exactly the same as the command egrep (which is now deprecated)

aws --version | grep -E "aws-cli/2"even plain grep "aws-cli/2" would work, but everyone writes grep -E out of habit because 90 % of the time they also use  or + in the same line. So yes — keep using grep -E. It’s the standard today.

with egrep you can search for more than one strings at the same time. 
For eg: egrep "key1|key2?\key3" node.sh

Command,What it removes,Does it delete config files?,Typical use case
sudo apt remove awscli,Only the program binaries and files,No,Keep config if you plan to reinstall later
sudo apt remove --purge awscli,Program + all configuration files,Yes,You want a completely clean slate (most common)
sudo apt purge awscli (shorter version),Exactly the same as remove --purge,Yes,"Same as above, just shorter"


# zip and unzip: (Remember: zip utility needs to be installed separately)

~$ zip zip_demo  demo/
  adding: demo/ (stored 0%)

$ unzip zip_demo.zip
Archive:  zip_demo.zip
   creating: demo/

$ zip -r demo_zip demo         # here we are zipping a folder named demo and naming that zip file as demo_zip, we use -r flag for recursive as we are zipping a folder resursively

 Note: gzip and gunzip does the same work of compressing and expanding files or list of files. In gzip the file extension is gzip and in zip and unzip the extension is zip 

ubuntu@ip-172-31-68-151:~$ tar -cvzf demo.tar.gz demo/        # here c,z,v,f are flags.                                                                   c=compress, v= verbose, z= zip, f=file
demo/
ubuntu@ip-172-31-68-151:~$ ls
aws  awscliv2.zip  demo  demo.tar.gz  zip_demo.zip

We need to give the name of compressed file we want plus the .tar.gz extension. 

ubuntu@ip-172-31-68-151:~/demo1$ tar -xvzf demo.tar.gz
demo/
ubuntu@ip-172-31-68-151:~/demo1$ ls
demo  demo.tar.gz
ubuntu@ip-172-31-68-151:~/demo1$

Here in above commands to extract we use -x flag. -v is to print the info on screen while zipping or extracting.

# SCP utility: used to copy files bwtween remote machines

<img width="791" height="263" alt="image" src="https://github.com/user-attachments/assets/67e83635-c872-4141-ab66-889a538c483a" />

$ scp -i "path of .pem key" secret_file.txt(source) ubuntu@ec2-3-15-221-86.us-east-2.compute.amazonaws.com: home/ubuntu(destination: which folder to copy in destination)

% scp -i "path to .pem file" -r ubuntu@ec2-3-15-221
-86.us-east-2.compute.amazonaws.com:/home/ubuntu/linux_for_devops

 % scp -i "/Users/manjiri/Documents/Devops/new-aws-account.pem" /Users/manjiri/Documents/Devops/shell-scripting/quick_installation.sh ubuntu@ec2-18-207-160-88.compute-1.amazonaws.com:/home/ubuntu/scp_test
quick_installation.sh                                                                                                           100% 9469    46.5KB/s   00:00

>> Its important to provide the path in which you want to copy the contents in destination server, means the part after :

% rsync   

Note: rsync is command used to rsync the folder which is already copied to the remote machine but now as there are changes in local we want to rsync it. Google its syntax.

3 Dec 2025

---
Question: Difference between ping, curl and wget

Say if application is not running, then we try to ping the ec2 server first. It tells if data is being transferred to and from from the server.

Zombie process: A child process finishes execution. The OS keeps: PID, Exit code, Resource usage. Parent process is supposed to call wait() to collect that. Parent does NOT call wait().
Result: Zombie process (state = Z).
In short- The process is dead. The record of its death is what’s still alive.

What zombies DO and DO NOT do

✅ They do occupy a PID
❌ They do NOT use CPU
❌ They do NOT use memory (except 1 tiny table entry)
❌ They do NOT execute code

So:

One or two zombies = harmless
Thousands of zombies = PID exhaustion → system can’t spawn new processes → outage

% ps aux | awk '$8=="Z"'

% ps -el | grep Z

---
5 December 2025

---

** ping  **

What ping actually does

Ping sends ICMP Echo Request packets to a target (ICMP = Internet Control Message Protocol.)
and waits for ICMP Echo Reply packets in return.

That’s it.

No TCP, no ports, no “checking server health.”
Just: “Hey, are you there?” → “Yes.”

What ping proves

If ping succeeds:

Network path exists between you and target.

ICMP is allowed by firewalls/security groups.

The target network stack is alive.

Round-trip latency (ms).

What ping does NOT prove

This is where people get it wrong.

Ping does NOT guarantee:

The machine is fully healthy

Any application/port is running

CPU/memory are fine

Disk isn’t full

Website works

SSH will be accessible

Load balancer is OK

AWS EC2 status checks are passed

Ping only checks ICMP replies, nothing more.

Why ping often fails (even when the server is fine)

Because:

Firewalls block ICMP

AWS security groups block ICMP by default

Corporate networks drop ICMP

Some operating systems rate-limit ICMP

Some hosts disable ICMP for “security”

So “no ping” does not always mean “server is down.”

# Netstat:  

Netstat: Show you what network connections, ports, and sockets your system is actually using.

What netstat actually does

It tells you:

Which ports are open

Which processes are using those ports

All active TCP/UDP connections

Routing table

Network interface stats

In short:
It tells you who is talking to whom, on which port, and over what protocol.

% netstat -tulnp
t → TCP

u → UDP

l → Listening only

n → Show numbers (no DNS resolution)

p → Which process owns the port

% netstat -ant   # shows active connections

ubuntu@ip-172-31-65-67:~$ netstat
Command 'netstat' not found, but can be installed with:
sudo apt install net-tools

ubuntu@ip-172-31-65-67:~$ netstat 

Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 ip-172-02-99-01.e:38906 ec2-23-13-65-63.co:http TIME_WAIT
tcp        0     52 ip-172-00-00-97.ec2:ssh 175.43.234.123.ha:55918 ESTABLISHED
Active UNIX domain sockets (w/o servers)
Proto RefCnt Flags       Type       State         I-Node   Path
unix  3      [ ]         SEQPACKET  CONNECTED     3848
unix  3      [ ]         STREAM     CONNECTED     4184     /run/systemd/journal/stdout
unix  2      [ ]         DGRAM                    6448     /run/user/1000/systemd/notify
unix  2      [ ]         DGRAM      CONNECTED     3827
unix  3      [ ]         STREAM     CONNECTED     4041

netstat -tulnp | grep 9095     # to chek if port is already being used and to check if your servce is actually listening

On modern Ubuntu, netstat is deprecated in favor of ss, which is faster and more accurate.

Equivalent command:
% ss -tulnp 
Netid                       State                        Recv-Q                       Send-Q                                                 Local Address:Port                                             Peer Address:Port                      Process
udp                         UNCONN                       0                            0                                                          127.0.0.1:323                                                   0.0.0.0:*

% ss   # can also be run separately

$ sudo lsof -i :8080    -- this gives the application and the port it is using

% ifconfig   # is interface configuration: Shows your network interface details (IP, MAC, status). Show me my network cards and their IP addresses.”

ifconfig is deprecated.
The modern replacement is:
% ip a

But people still use ifconfig because it’s simple and familiar.

% curl ifconfig.me    # this gives public IP address of the system

✔ Private IP ranges (always private)

If the IP starts with any of these, it's private:

10.0.0.0 – 10.255.255.255
172.16.0.0 – 172.31.255.255
192.168.0.0 – 192.168.255.255

✔ Everything else is public.
How to check quickly Just look at the IP shown under inet.

% traceroute linkedin.com  % gives 

% traceroute linkedin.com

Note: Both commands show the exact network path (hops) your packet takes from your machine to a destination (like google.com). They help you see where latency, packet loss, or routing issues are happening.

% mtr google.com      # it is combination of ping+ traceroute , MTR= my trace route. It is used for network troubleshooting.

Why you use mtr (It traces the route to a destination (like traceroute). It continuously pings every hop on that route.)

Use it when:

Sites load slowly and you want to see which hop is causing latency.
You suspect routing changes or ISP issues.
You're debugging packet loss on a server.
You're checking if the problem is your system, your ISP, or the destination.

# nslookup

nslookup is a DNS-debug tool.

1. Convert domain → IP (forward lookup)
nslookup google.com


Output:

DNS server used

IP address of google.com

Use this when:

You want to check if DNS is resolving correctly.

A website isn’t loading and you want to confirm the IP is reachable.

2. Convert IP → domain (reverse lookup)
nslookup 8.8.8.8


This resolves PTR records.

Use this when:

You want to identify who owns an IP.

Debugging server misconfigurations, email issues, logging, etc.

~$ nslookup trainwithshubham.com
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	trainwithshubham.com
Address: 15.197.225.128               # this is actual IP address of website
Name:	trainwithshubham.com
Address: 3.33.251.168

# Telnet - Does the same task as nslookup

Helps to connect with website, domain and port of an IP. difference is that we add port number in the command.

$ telnet trainwithshubham.com 80
Trying 15.197.225.128...
Connected to trainwithshubham.com.

% hostname: gives you IP address of your server

$ cat /etc/hosts - Has all the hosts list

$ ip address show    - shows the IP addresses, Private as well as public.

$ ip # is also command which can be used with flags 

$ iwconfig  # used to see wirless atachments to the server.

Even if we are using wifi it does not show any extensions as we are using EC2. Tr to do it on your server and you can see WiFi extension

$ iwconfig
lo        no wireless extensions.

ens5      no wireless extensions.

~$ dig trainwithshubham.com           # get in detail network info using 'dig'

; <<>> DiG 9.18.39-0ubuntu0.22.04.2-Ubuntu <<>> trainwithshubham.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 14832
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;trainwithshubham.com.		IN	A

;; ANSWER SECTION:
trainwithshubham.com.	300	IN	A	15.197.225.128
trainwithshubham.com.	300	IN	A	3.33.251.168

;; Query time: 4 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Fri Dec 05 08:07:54 UTC 2025
;; MSG SIZE  rcvd: 81

whois -- This command gives domain information.

$ whois trainwithshubham.com                 
   Domain Name: TRAINWITHSHUBHAM.COM
   Registry Domain ID: 2658723068_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.godaddy.com
   Registrar URL: http://www.godaddy.com
   Updated Date: 2024-12-04T06:25:14Z
   Creation Date: 2021-12-01T11:33:03Z
   Registry Expiry Date: 2026-12-01T11:33:03Z
   Registrar: GoDaddy.com, LLC
   Registrar IANA ID: 146

% arp -- # ADdress resolution protocol, it is used to find MAC address of a server

% ifplugstatus  # tells us if your internet interfaces are working or not

$ ifplugstatus
lo: link beat detected
ens5: link beat detected

# curl 

CURL is used to call API. 

$ curl -X GET https://dummy.restapiexample.com/api/v1/employees    # GET is used to get the information from an API

jq is plugin tool to butify the curl output.

curl -X GET https://dummy.restapiexample.com/api/v1/employees | jq

# wget

Is used td download a file from internet.

$ wget https://imgs.search.brave.com/dzH3dPFS7ktS-zQ4jlDdVkI91zmnx1OWnJLEthgXCQQ/rs:fit:500:0:1:0/g:ce/aHR0cHM6Ly9ibG9n/LmxpcHN1bWh1Yi5j/b20vd3AtY29udGVu/dC91cGxvYWRzLzIw/MjQvMTIvc2FtcGxl/LWR1bW15LWFwaS1m/b3ItdGVzdGluZy1s/aXBzdW1odWIuanBn

# Ip tables: 

iptables is the firewall rule engine on Linux. It decides what network traffic is allowed, blocked, or modified. (For more info refere manual and internet while using the comman)

Three core chains matter:

INPUT → traffic coming into the machine

OUTPUT → traffic leaving the machine

FORWARD → traffic passing through the machine (router case)

If a packet matches a rule → the action (ACCEPT, DROP, REJECT) is applied.
If no rule matches → default policy decides (ACCEPT or DROP).

$ sudo iptables --list-rules
-P INPUT ACCEPT
-P FORWARD ACCEPT
-P OUTPUT ACCEPT

# watch

You can write it before any command if you want to watch its output every 2 seconds.

You can also change the interval of watch from 2s to 5s using:

$ watch -n 5 top

$ watch top

$ watch -n 5 mtr trainwithshubham.com

#nmap

%nmap -v trainwithshubham    # it will scan the network, tell if there are any open ports, -v = verbose

ps aux gives PPID as well. The two commands differ slightly in output columns. 

ps aux → human readable
ps -ef → scripting + parent-child tracing

You get:

CPU%

MEM%

COMMAND (full command)

TTY

STAT

Example output is compact and easier to scan visually.

Best for:

Quickly spotting high CPU processes

Finding zombies (STAT = Z)

Checking memory hogs

Seeing interactive programs tied to terminals

Use cases

ps aux | grep nginx

ps aux --sort=-%cpu

ps aux | grep Z

----

ps -ef is System V style.

You get:

UID

PID

PPID

Start time

Full command

Exact process hierarchy (parent-child relationships)

It’s more consistent for scripting because fields don’t shift around.

Best for:

kill scripts

finding parent processes

process tree investigation

Use cases

ps -ef | grep java

ps -ef | awk '{print $2}'

ps -ef | grep cron

ps -ef | grep defunct

-----

 # xargs takes input from STDIN and turns it into arguments for another command. Use xargs whenever a command expects arguments but your data comes from a pipe.

 1) Delete many files
find . -name "*.log" | xargs rm

2) Kill many PIDs
ps | grep something | awk '{print $1}' | xargs kill

3) Pass URLs to curl
cat urls.txt | xargs curl -O

----

Some more commands:

du -h| sort -rh| head -10 | tee large_files.txt   # Find the first 10 biggest files in the file system and write the output to a file.
OR
du -h| sort -rh| head -10 > large_files.txt

ps -ef| grep defunct| tee zombie.txt| awk '{print $3}' | xargs -r kill -9     # command to find and all all the zombie processes

----

ubuntu@ip-172-31-69-95:~$ top       (number of zombie process can also be checked here as highlighted below)
top - 03:14:50 up 20 min,  1 user,  load average: 0.00, 0.00, 0.00
Tasks:  99 total,   1 running,  98 sleeping,   0 stopped,  ** 0 zombie**
%Cpu(s):  0.2 us,  0.0 sy,  0.0 ni, 99.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :    914.0 total,    239.9 free,    204.3 used,    469.8 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    551.9 avail Mem

----
6 December 2025
----
To get the OS or kernel details use below commands:

$ hostnamectl
$ hostname -a

-----

ps aux      # report a snapshot of the current processes, active processes. If you want a repetitive update of the selection and the displayed information, use top instead.

df -h       # gives report file system disk space usage

free -h     # free displays the total amount of free and used physical and swap memory in the system, as well as the buffers and caches used by the kernel

# du -h       ... Summarize disk usage of the set of FILEs, recursively for directories


----

10 Dec 2025

---

Think of the Linux kernel as a car's engine 🚗. The engine is the core component that makes the car run and controls all essential functions. But a car isn't just an engine; it needs a body, seats, and a dashboard to be a complete vehicle. That's what a distribution provides.

+----------------------------------------------------+
| User Applications (Vim, Docker, Apache, etc.)     |
+----------------------------------------------------+
| Shell (Bash, Zsh, Fish, etc.)                     |  <-- Part of the OS
+----------------------------------------------------+
| System Libraries (glibc, libc, OpenSSL, etc.)     |  <-- Part of the OS
+----------------------------------------------------+
| System Utilities (ls, grep, systemctl, etc.)      |  <-- Part of the OS
+----------------------------------------------------+
| Linux Kernel (Process, Memory, FS, Network)       |  <-- Core of the OS
+----------------------------------------------------+
| Hardware (CPU, RAM, Disk, Network, Peripherals)   |
+----------------------------------------------------+

User Applications and System Utilities:

User Applications: End-user programs like web browsers, text editors (Vim), DevOps tools (Docker, Ansible), and servers (Apache). Interact with the OS via system calls through the shell or GUI.

System Utilities: Core commands (e.g., ls, grep, systemctl) for system interaction, provided by the GNU Project.

File System: Organizes data in a hierarchical structure; everything is a file.

Processes: Running instances of programs, managed by the kernel.

Init System: Manages system startup and services (systemd, SysVinit).

<img width="541" height="736" alt="image" src="https://github.com/user-attachments/assets/2161bbef-cca5-493f-8ea9-17eb577abaca" />

sudo apt update         # Update package lists
sudo apt upgrade -y     # Upgrade installed packages
sudo apt install nginx  # Install a package
sudo apt remove nginx   # Remove a package
sudo apt autoremove     # Remove unused dependencies
sudo apt search nginx   # Search for a package

>> Always update before installing: sudo apt update && sudo apt upgrade -y

Task: Run uname -r to check the kernel version on either instance. Compare it to the latest stable version on kernel.org. Why might cloud providers like AWS use older kernels?
Hint: Consider stability, compatibility with cloud tools, and enterprise support.

----
11 Dec 2025

----
1) To know which shell you are using use:
$ echo $SHELL
/bin/bash

2) This gives list of all internal/default shell commands (on ubuntu): compgen -b

3) $ which date          # here we get to see where the command binaries are stored using which, you can do it for any command.
/usr/bin/date

4) $ date
Thu Dec 11 07:24:29 UTC 2025

5) $ file /usr/bin/date               # we get to see the file details for date.
/usr/bin/date: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=ee56cbd6cac8377f099282a93e1a2a56f8bf8492, for GNU/Linux 3.2.0, stripped

-----

This gives list of all internal/default shell commands: compgen -b
To know which shell you are using use: echo $SHELL   

There are 2 types of commands on linux: 1) Internal commands 2) External commands

External commands have their programs stored on linux , when you do $ which date, you see the path at which the program is stored.
You do not see directory in which programs are stored for internal commands when you do $which ls.

Some commands are both internal as well as external, so we see its program when we do $which pwd. For eg: $ pwd

<img width="1706" height="786" alt="Command Syntax" src="https://github.com/user-attachments/assets/179fa722-d708-417d-976a-50abbe5a54b4" />


<img width="1706" height="573" alt="Pasted Graphic 15" src="https://github.com/user-attachments/assets/107b1316-1ffd-41e9-a28d-bb193a63ab95" />


$ who              # who will give you how many users currently logged into system.
ubuntu   pts/0        2025-12-11 07:13 (116.75.134.171).        - pts is shell session, if user has logged in using shell. SO currently there are 2 users which are logged in through shell in linux.
ubuntu   pts/1        2025-12-11 07:38 (116.75.59.98)

% whoami           # tells you the users logged in current.

Can be written as $ who am I

tty= teli type terminal

$ cal    # gives you calendar, you will need to install its utility.
$ cal 2025
Command 'cal' not found, but can be installed with:
sudo apt install ncal

Install cal using above command and run below commands:
$ cal 2025
$ cal -m may 
$ cal -m may 2024
$ cal 2025
ubuntu@ip-172-31-69-95:~$ cal -m December 2025
   December 2025
Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31

$ echo hello good day!      # echo is used to print, that’s it, nothing else.
hello good day!
 As below using ’type’ we can see whether the command is internal (builtin) or external(hashed)
ubuntu@ip-172-31-69-95:~$ type date
date is /usr/bin/date
ubuntu@ip-172-31-69-95:~$ type pwd
pwd is a shell builtin
ubuntu@ip-172-31-69-95:

$ which date 				# to find where the date command’s program is saved.

$ sleep 5				# for next 5 seconds the command prompt will do nothing, it is used in scripts mainly, not on commands.

<img width="1706" height="459" alt="Pasted Graphic 16" src="https://github.com/user-attachments/assets/d2b5b1e1-690c-414c-841e-07e9efd22b45" />

￼
 Ctrl + C —> Is used to abort or stop the execution
Ctrl + l —> Clear the console (on ubuntu) On Mac Command + R is used to clear.

Ctrl + Shift +C —> Shortcut to copy on ubuntu
Ctrl + Shift +V —> Shortcut to paste on ubuntu
---
12 Dec 2025
---

$ man -k pass   # this command is used to find relevant command. Means if you dot know a command then you can search for it using the relaveant keyword. Here I wanted to search for password change, hence using pass

$ man -k password

Below are man shortcuts:
<img width="1453" height="951" alt="image" src="https://github.com/user-attachments/assets/045fe482-3ee6-46b1-9330-fdadd6edcd93" />

Redirection:

Process : running aspect of a program, it is running inside the memory which is stored inside the storage.

<img width="1607" height="925" alt="image" src="https://github.com/user-attachments/assets/204c37e6-5233-43f9-8170-0396a2192b1d" />

Like in below diagram, stdin is by default connected to the keyboard, so it reads our input from keyboard. And stdout and stderr are by default connected to console/terminal, so it displays the ouput there.
That is why we always get the output or else error for the command we enter on console.

<img width="1424" height="785" alt="image" src="https://github.com/user-attachments/assets/8b19c140-5413-44c4-a078-c1e99b8fd9e2" />

Note: Every command is a program and program becomes process. So Operatng system loader loads the say date program into the memory and converts it into process. And process prints output and once done process gets exited.

> This overrites the file
>> This appends the file

Now if we want to redirect the error then that can be done using: 2> sign.
For eg: dat 2> date_error.txt     # Now we know that dat is not a command so this command will give an error. But instead of printing that error on terminal we can redirect it to file.

Remember it will write to that file when the command runs into error.

If you want to disacrd or completely ignore the error and not to print it on console or print it in file we can do that using: 2> /dev/null:
For eg: dat 2> /dev/null       /dev/null is like black hole in linux.

We can combine the redirect output and redirect error commands like below:

$ > file1 2> file2 - This command redirects stdout to file1 and stderr to file2

$ > file1 2> &1   = This command redirects stdout and stderr to file1

$ >> file1 2> &1   - Thos command redirects stdout and stderr to append to the sme file (file1)

Below diagram shows how pipe (pipeline) command works:

<img width="1424" height="785" alt="image" src="https://github.com/user-attachments/assets/54aa860d-9568-49d2-846a-57be95630aa9" />

Pipe command in Linux. Pipeline allows the output of a process to be manipulated and formatted by another process before it outputs to the terminal. It allows chaining multiple commands to perform complex tasks in a single operation.

The pipe operator is represented by a vertical bar |.

Syntax:
command1 | command2

command1 is the first command whose output is passed, and command2 is the second command that receives the output of command1 as its input.

Why use pipes?

To process data in steps without intermediate files.
No need to create temporary files to store data.
To combine the functionality of multiple commands.
To create concise and efficient command-line workflows.

echo $USER
whoami gives username on terminal but if we want to use it as variable value then we use $USER

---

17 December 2025

----
To check logs:

sudo journalctl -u jenkins -xe

sudo journalctl -u jenkins --no-pager | tail -100
 
sudo cat /var/log/jenkins/jenkins.log     # If Jenkins is installed via apt

----

To uninstall packages/applications:

% sudo apt-get purge nginx

% sudo apt-get autoremove
