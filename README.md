# Linux

$ ps -ef    ....to check the runing processes

$ nproc  ...... command to check the number of CPU cores available 

ubuntu@ip-172-31-24-109:~$ nproc

1

ubuntu@ip-172-31-24-109:~$ free

               total        used        free      shared  buff/cache   available
Mem:          980368      433736       91160         936      638084      546632
Swap:              0           0           0


$ df

Filesystem     1K-blocks    Used Available Use% Mounted on

/dev/root        7034376 5506464   1511528  79% /

tmpfs             490184       0    490184   0% /dev/shm

tmpfs             196076     920    195156   1% /run

tmpfs               5120       0      5120   0% /run/lock

/dev/xvda16       901520  152308    686084  19% /boot

/dev/xvda15       106832    6250    100582   6% /boot/efi

tmpfs              98036      12     98024   1% /run/user/1000


$ top

top - 04:23:51 up 2 days, 12:12,  1 user,  load average: 0.00, 0.00, 0.00

Tasks: 108 total,   1 running, 107 sleeping,   0 stopped,   0 zombie

%Cpu(s):  0.3 us,  0.3 sy,  0.0 ni, 95.3 id,  0.0 wa,  0.0 hi,  0.0 si,  4.0 st

MiB Mem :    957.4 total,     89.0 free,    423.2 used,    623.5 buff/cache

MiB Swap:      0.0 total,      0.0 free,      0.0 used.    534.2 avail Mem


    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
  65565 root      20   0 1727996  24004   9600 S   0.3   2.4   1:53.53 containerd
  
  75481 ubuntu    20   0   14992   7072   5120 S   0.3   0.7   0:00.05 sshd
      1 root      20   0   22676  12928   8704 S   0.0   1.3   0:10.88 systemd  
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.01 kthreadd
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release
      
     
Blackers faced and its solution:

1) Error: Docker containers were not getting created due to insufficient space.

Troubelshooting steps:

Checked disk space: df -h -> /dev/root was 100% used
Then to find what is consuming the space ran: du -xh / --max-depth=1 | sort -rh -> This command checks in root (/) which directories are consuming highest size and lists them.

.minikube and .kube were consuming the most space. Almost 90%. -> I was not actively using minikube hence deleted it, removed its dependent directories.

Then containerd in /var/lib folder was consuming lot of space around 2.9G, deleted it using - docker system prune -a --volumes -> THis freed lot of space.

Note: To get into var , containerd, etc root permissions are needed. You can go into root using : sudo -i
