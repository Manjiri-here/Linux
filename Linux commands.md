$ ls 

$ cd

$ pwd

$ mkdir

$ rmdir  ... removes directory if it is empty

$rm  .. removes file    

$ rm -r .. removes directory recursively   # these -r, -f are flags

$ rm -rf .. removes files/directory forcefully. f=forceflly, r=recursive

% rmdir

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


27 November 2025 

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
