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



