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

$ tail -n filename

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

manjiri@Abhis-MacBook-Pro ~ % df -h

Filesystem        Size    Used   Avail Capacity iused ifree %iused  Mounted on

/dev/disk1s1s1   466Gi    11Gi   398Gi     3%    426k  4.2G    0%   /

devfs            193Ki   193Ki     0Bi   100%     666     0  100%   /dev

/dev/disk1s3     466Gi   4.4Gi   398Gi     2%    3.6k  4.2G    0%   /System/Volumes/Preboot

/dev/disk1s5     466Gi   3.0Gi   398Gi     1%       3  4.2G    0%   /System/Volumes/VM

/dev/disk1s6     466Gi    70Mi   398Gi     1%     678  4.2G    0%   /System/Volumes/Update

/dev/disk1s2     466Gi    48Gi   398Gi    11%    640k  4.2G    0%   /System/Volumes/Data

map auto_home      0Bi     0Bi     0Bi   100%       0     0     -   /System/Volumes/Data/home

/dev/disk1s1     466Gi    11Gi   398Gi     3%    426k  4.2G    0%   /System/Volumes/Update/mnt1

/dev/disk3s1     726Mi   647Mi    76Mi    90%    1.0k  775k    0%   /Volumes/Brave Browser

manjiri@Abhis-MacBook-Pro ~ % uptime

18:51  up 16 days, 11:18, 3 users, load averages: 1.55 1.53 1.69

manjiri@Abhis-MacBook-Pro ~ % hostname

Abhis-MacBook-Pro.local

manjiri@Abhis-MacBook-Pro ~ % whoami
manjiri

# 25 November 2025

>> Note: It is good practice to name log file with .log extension

1) head -n 5 file.log    # This prints the first 5 lines of the file
2) less file.log      # to read file, less command is easy to scroll up and down than more
3) awk '' file.log     # inside '' we write the operation we want to perform on file
For eg- $ awk '{print}' file.log    # this prints the whole file
$ awk '{print $1, $3, $4}' file.log  # prints only column 1, 3 and 4 of the file.
$ awk '/INFO/ {print $1 $3}' file.log     # prints lines which contains info
$ awk '/INFO/ {print $1 $3}' file.log > INFO.txt    # to send the output to INFO.txt file
$ awk 'INFO {count++} END {print "the count of INFO is: ", count}' file.log
or we can also use:
$ awk '/INFO/' file.log| wc -l
$ awk '$2 >= "08:51:00" && $2 <= "08:51:59" {print $3}' file.log  -- Here we are putting filter on column 2 and then printing column 3(event) for it.
% awk '$2 >= "08:51:00" && $2 <= "08:51:59" {print $3, $2, $4}' file.log
% awk 'NR >= 2 && NR <= 10 {print $2}' file.log     -- here NR= number of rows
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


# Soft link and hard link

Note: Soft link and hard links are like shortcuts in windows which we have on desktop. Similarly in linux soft link is the one where if we delete the main/source file then the soft link also gets deleted while hard link does not get deleted even when main file is deleted.

% ln -s linux/demo/file1 softlink_file1       # here softlink of file1 is created in softlink_file1 and when you try to print it you get exact same content. Like below. (-s = soft link)

You see l for softlink here in column 1:
lrwxr-xr-x@  1 manjiri  staff    16 27 Nov 13:25 softlink_file1 -> linux/demo/file1

manjiri@Abhis-MacBook-Pro Devops % cat softlink_file1
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

% cut -b 1-2 hardlink_file1      # this cuts bytes(that is why -b flag) 1-2 or 1-4 and prints it.

% echo "hello there" | tee hello.txt      # Tee prints as something on screen as well puts in into a file, in case file does not exist it also creates the file.

% sort file1       # it sorts the contents aplhabetically

$ diff file1 file2     # It gives you difference between two files, and it can take only 2 files as input

$ rm -r .. removes directory recursively   # these -r, -f are flags

systemd -  The **service manager itself** (the engine)
systemctl`- The **command you use to control systemd** 

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

# Now in the below way you see id of users and the groups they are a part of

ubuntu@ip-172-31-71-36:~$ id
uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu),4(adm),24(cdrom),27(sudo),30(dip),105(lxd)
ubuntu@ip-172-31-71-36:~$ su jethalal
Password:
$ id
uid=1001(jethalal) gid=1001(jethalal) groups=1001(jethalal)


