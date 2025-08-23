# Linux

$ ps -ef    ....to check the runing processes

$ nproc  ...... command to check the number of CPU cores available 

ubuntu@ip-172-31-24-109:~$ nproc
1
ubuntu@ip-172-31-24-109:~$ free
               total        used        free      shared  buff/cache   available
Mem:          980368      433736       91160         936      638084      546632
Swap:              0           0           0
ubuntu@ip-172-31-24-109:~$ df
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/root        7034376 5506464   1511528  79% /
tmpfs             490184       0    490184   0% /dev/shm
tmpfs             196076     920    195156   1% /run
tmpfs               5120       0      5120   0% /run/lock
/dev/xvda16       901520  152308    686084  19% /boot
/dev/xvda15       106832    6250    100582   6% /boot/efi
tmpfs              98036      12     98024   1% /run/user/1000
ubuntu@ip-172-31-24-109:~$ top
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
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_g
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_p
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-slub_
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-netns
     10 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/0:0H-events_highpri
     12 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-mm_pe
     13 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_rude_kthread
     14 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_trace_kthread
     15 root      20   0       0      0      0 S   0.0   0.0   0:03.02 ksoftirqd/0
     16 root      20   0       0      0      0 I   0.0   0.0   0:03.90 rcu_sched
     17 root      rt   0       0      0      0 S   0.0   0.0   0:01.23 migration/0
     18 root     -51   0       0      0      0 S   0.0   0.0   0:00.00 idle_inject/0
     19 root      20   0       0      0      0 S   0.0   0.0   0:00.00 cpuhp/0
     20 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kdevtmpfs
     21 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-inet_
     23 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kauditd
     24 root      20   0       0      0      0 S   0.0   0.0   0:00.05 khungtaskd
     25 root      20   0       0      0      0 S   0.0   0.0   0:00.00 oom_reaper
     27 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-write
     28 root      20   0       0      0      0 S   0.0   0.0   0:08.67 kcompactd0
     29 root      25   5       0      0      0 S   0.0   0.0   0:00.00 ksmd
     30 root      39  19       0      0      0 S   0.0   0.0   0:00.00 khugepaged
     31 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-kinte
     32 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-kbloc
     33 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-blkcg
     34 root     -51   0       0      0      0 S   0.0   0.0   0:00.00 irq/9-acpi
     35 root      20   0       0      0      0 S   0.0   0.0   0:00.00 xen-balloon
     36 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-tpm_d
     37 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-ata_s
     38 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-md
     39 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-md_bi
