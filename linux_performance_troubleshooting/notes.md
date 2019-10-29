10/4/2019 - Linux Performance Optimization - Online O'Reilly Training


## General notes

- you need root to do proper performance analysis; you will never get a complete picture as a non-root user


## Common Tools

**top**

- uptime affects performance, especially memory. b/c linux uses buffer and cache, and they change depending on how long the system is running, bc it optimizes over time
    - so in `top`, buff/cache information might not be all that useful if the system hasn't been up long
- **load average**:     
    - what does "trouble" look like... depends on how many CPUs
    - general rule of thumb is that the load average should not be higher than the number of CPUs in the system
    - in top, press "1" to see all CPUs
    - if your load avg is higher than number of CPUs then you need to investigate... doesn't automatically mean you're in trouble
    - Then... you need to look at each CPU line after hitting "1" and look at those values
        - system: kernel, drivers, etc
        - user: activities, applications
        - on most systems, you should expect user space to be using more than system space
        - if system space is the culprit, you need to investigate b/c something is probably wrong... the only way user space affects system space is through system calls
        - idle: 0% idle means no time is spent on idle, and that is weird
        - wa: waiting for i/o... not as useful anymore b/c of move to SSD for disk and SAN type storage... if you see wa being high, that's weird and you need to investigate. probably higher than 20% is a potentially sign of trouble and you should investigate
        - ha, funny... I'm looking at our main jenkins server now and it's got 4 CPU; I'm seeing one of those CPUs with 40-80% `wa`... looks like yum, pip, audit, savscand the main culprits there
    - point: the numbers he's giving us are just recommendations meant as guides
- **process information**
    - highest consumers at the top
    - you can usse < and > to manipulate sorting; for example, you can use those to sort by memory instead of cpu
    - these just basically scroll across the column header and sort by whatever column is active... Question: how can you tell which column is sorting?

- **Memory**
    - swap is generally a good thing b/c inactive applications can go there
    - but for example, you should disable swap ona  kubernetes cluster... "everything I say in this course will have an exception"
    - buff/cache should be about 25% of total memory, as a guide, to get started
    - I notice that on our main jenkins server, it looks like we have swap disabled
    - "Anonymous inactive" memory is a sign you probably need more swap, because anonymous inactive memory should probably be in swap
    - first and foremost, follow the advice of the vendor, i.e. if oracle says "you should have XYZ swap for your oracle database, then just do it"
    - grep -i active / proc/meminfo to see active and inactive anonymous. here's what I see on jenkins:
        [root@awsdevjknl01 sys]# grep -i active /proc/meminfo
        Active:          7923112 kB
        Inactive:        4022796 kB
        Active(anon):    4223068 kB
        Inactive(anon):        8 kB
        Active(file):    3700044 kB
        Inactive(file):  4022788 kB
    - `vmstat` for virtual memory statistics
      - si / so == swap in, swap out
        - `vmstat 2 5000` will poll every 2 seconds, 5000 times
      - bi / bo == block in / block out
    - `free
- `k` in top to pull up the "kill" interface

**/proc/sys**
- hundreds of kernable tunables can be set through files in /proc/sys
- runtime-only mods
- use `sysctl` for persistent changes
- `/etc/sysctl.conf` is where you apply settings; distros may have a specific location for config files
- `sysctl -a` to see everything that's set
- `cat /etc/sysctl.conf`    to see everything set in that file
- also, there are /etc/sysctl.d/ directory for other config files

**/proc**
- /proc shows you a directory for all running processes, where you can get more info
- `ps -ef` and other `ps` flags show a lot of this info more conveniently

**cpuinfo**
- info on each cpu

**meminfo**
- info on all memory
- hmmm... not on our jenkins server
- `slabtop` shows memory stuff too

**interrupts**
- `cat /proc/interrupts` to see cool stuff related to interrupts

**/proc/sys**
- especially kernel, net, and vm

**rpm -ql**
rpm -ql process to see all the files associated with a package... NEAT!

[root@awsdevjknl01 sys]# rpm -ql sysstat | grep cron
/etc/cron.d/sysstat

**sar**

- it's just top data put in a historical perspective
- so to get a sense of what is meaningful, get familiar with what top shows you so you can start ot learn what is problematic


Look for the "Linux Performance" recorded video on oreilly'


**tuned**
- tuned-adm list
- tuned-adm profile network-latency
- this stuff looks pretty awesome, though it's not available at least on our rhel6 systems

## cgroups

- especially relevant in a containerized environment
- fully integrated into systemd
- distros prior to systemd have their own cgroup interface

- /etc/systemd/system.conf
- turn on CPUAccounting, MemoryAccounting, BlockIOAccounting
- then systemctl daemon-reload
- he has a git repo at sandervanvugt/performance with some utils, that he's showing us

- ha, RAD, he's showing how to use /sys/bus/cpu/devices to disable CPUs by changing the cpu0/online etc file to 0 instead of 1 which disabbles cpu
- showing how there's a 1/3 slice for system, 1/3 for user, and 1/3 for machine
- for cpu slicing
- showing how he creates 2 services, one with twice the cpu shares as the second, and in total, they'll take up their available share of system cpu
- with nothing else running, one takes up 66%, the other 33%
- as soon as he starts a user-space while loop, that loop takes up 50% and the others take up 33-some and 16-some (total 50% or so)
- ... cool demo to show how the slicing works
- and you can modify these slice allocations if you want
- he changes the sshd service to create an override file which sets a really low memory allocation, then restarts the service
- service won't restart
- systemctl status sshd.service shows stuff, but not why it won't restart
- journalctl -xe shows more, and shows it's out of memory


- systemd example:

```
[root@awsdevjenl04 esherm]# systemctl status docker.service
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since Fri 2019-09-06 09:22:50 EDT; 4 weeks 0 days ago
     Docs: https://docs.docker.com
 Main PID: 23650 (dockerd)
    Tasks: 19
   Memory: 2.5G
   CGroup: /system.slice/docker.service
           └─23650 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Oct 04 12:38:20 awsdevjenl04.cfpb.local e9f838f59d76[23650]: Built at: 10/04/2019 4:38:20 PM
Oct 04 12:38:20 awsdevjenl04.cfpb.local e9f838f59d76[23650]:               Asset      Size  Chunks             C...mes
Oct 04 12:38:20 awsdevjenl04.cfpb.local e9f838f59d76[23650]:        analytics.js  3.66 KiB       0  [emitted]  a....js
Oct 04 12:38:20 awsdevjenl04.cfpb.local e9f838f59d76[23650]:            index.js  18.1 KiB       1  [emitted]  i....js
Oct 04 12:38:20 awsdevjenl04.cfpb.local e9f838f59d76[23650]: permalinks-utils.js  3.21 KiB       2  [emitted]  p....js
Oct 04 12:38:20 awsdevjenl04.cfpb.local e9f838f59d76[23650]:       permalinks.js  4.55 KiB       3  [emitted]  p....js
Oct 04 12:38:20 awsdevjenl04.cfpb.local e9f838f59d76[23650]:   recent-notices.js  3.24 KiB       4  [emitted]  r....js
Oct 04 12:38:20 awsdevjenl04.cfpb.local e9f838f59d76[23650]:     regs3k-utils.js   1.8 KiB       5  [emitted]  r....js
Oct 04 12:38:20 awsdevjenl04.cfpb.local e9f838f59d76[23650]:     search-utils.js  1.94 KiB       6  [emitted]  s....js
Oct 04 12:38:20 awsdevjenl04.cfpb.local e9f838f59d76[23650]:           search.js  5.41 KiB       7  [emitted]  s....js
Hint: Some lines were ellipsized, use -l to show in full.
```

- I asked him if you can get sweet output like this on non-systemd systems such as RHEL6, and he says there isn't an easy way


`systemd-cgtop`
`systemd-cgls`
`systemctl cat [service]` looks cool... eg `systemctl cat docker` will show you the service config file

are pretty sweet


## IO performance

- `iotop` for seeing what's taking up io activity
- he tells a cool story about journaling (kjournald) being responsible for killing a system, and iotop showing it, which led them to tune journaling to be friendlier and bam problem solved
- throughout this whole preso he's been showing using `dd` to simulate activity, eg `dd if=dev/sero of=/dev/null`


If you're suffering bad io performance, you might:
- consider separate disks, i.e. database-writing disks on a separate disk from operating system disk
- filesystem choices are important, and the options for the filesystem are useful to know
eg in /etc/fstab, you could set ext4 to "noauto,data=writeback" to limit the ability for journaling to wreck your system, at the expense of high integrity


- IO problems are the most important problems to look at because they have compounding effects on CPU and Memory, so start there for troubleshooting
- Performance optimization, you're probably going to get the biggest gains out of tuning IO stuff
- Memory optimization next
- CPU optimization... you rarely need to care about this

- lsof for seeing listof open files for a given process
- cd /proc/[nuim]/fd and then ls, to see all the things a process is looking at


## Memory

- virtual vs resident memory
- there is a big difference between virtual mem and physical mem
  - this is why you will see many processes with like 4GB virtual mem (in `top`) even if the system only has 2GB physical memory
- **resident** memory is what the process is actually using
- virtually memory is just an address space

- memory leaks... use `valgrind`
  
  `valgrind --tool=memcheck ls`  - to see what it does; of course ls doesn't have memory leak
  - add --leak-check=full for more details


  ## Network performance
  - qperf to monitor bandwidth
  - ip -s link for packet statistics