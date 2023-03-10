How to kill a zombie process on Linux
=====================================

To kill a zombie process, you must remove its name from the process list.

By

[Anderson Silva](/users/ansilva) (Alumni, Red Hat)

October 31, 2021 | [0 Comments](#comments) | %t min read

  
![Full moon on a hazy night](/sites/default/files/lead-images/ganapathy-kumar-unsplash.jpg "Full moon on a hazy night")

Image by:

Happy Halloween Open SOURCE-rers!

Here's a tale as old as _epoch_ time. Since there has been C and Unix, and (later on) Linux, we've had _zombies_. Specifically, there are processes that get marked as _a zombie process_. Misunderstood by some, ignored by others, and immune to the efforts of so many of us trying to `kill` these processes without much success. Why is that?

What is a process in Linux?
---------------------------

It all begins when a program in Linux gets executed, and when it does, its running instance is called a process. You can see all processes on your Linux environment with the [`ps` command](https://opensource.com/article/21/8/linux-procps-ng).

$ ps \-ax  
        PID TTY         STAT   TIME COMMAND  
        1 ?     Ss      0:01 /usr/lib/systemd/systemd rhgb \--switched-root \--sys  
        2 ?     S       0:00 \[kthreadd\]  
        3 ?     I<      0:00 \[rcu\_gp\]  
        4 ?     I<      0:00 \[rcu\_par\_gp\]

Sometimes a process starts another process, making the first process the parent of the second. The `pstree` command is a great tool that allows you to see the processes' "genealogy" on your system.

$ pstree \-psn  
systemd(1)─┬─systemd-journal(952)  
        ├─systemd-udevd(963)  
        ├─systemd-oomd(1137)  
        ├─systemd-resolve(1138)  
        ├─systemd-userdbd(1139)─┬─systemd-userwor(12707)  
        │                     ├─systemd-userwor(12714)  
        │                     └─systemd-userwor(12715)  
        ├─auditd(1140)───{auditd}(1141)  
        ├─dbus-broker-lau(1164)───dbus-broker(1165)  
        ├─avahi-daemon(1166)───avahi-daemon(1196)  
        ├─bluetoothd(1167)

Every process gets assigned a number in the system. Process ID number 1 gets assigned to the very first process executed during the boot process, and every subsequent process after PID 1 is a descendant of it. The PID 1 process is the _init_, which on most newer versions of Linux is just a symbolic link to the `systemd` program.

Ending a process with the kill command
--------------------------------------

You can terminate processes in a Linux system with the `kill` command_._ Despite the name, the `kill` command and a set of others such as `pkill` and `killall` got written/designed to send SIGNALS to one or more processes. When not specified, the default SIGNAL it sends is the SIGTERM signal to terminate the process.

When a parent process dies or gets killed, and its child process doesn't follow its parent's demise, we call that process an _orphan process_.

How to kill a zombie process
----------------------------

Zombie processes, on the other hand, cannot be killed! Why might you ask? Well, because they are already dead!

Every child process, when terminated, becomes a zombie process and then removed by the parent. When the process exits its existence and releases the resources it had used, its name is still on the OS process table. It is then the parent's process job to remove its name from the process table. When that fails, we have the zombie process, which isn't really a process anymore, but just an entry on the process table of the OS.

This is why trying to do a `kill` command even with the `-9` (SIGKILL) option on a defunct (zombie) process doesn't work, because there is nothing to kill.

So, to kill a zombie process, as in to remove its name from the process list (the process table), you have to kill its parent. For instance, if PID 5878 is a zombie process, and its parent is PID 4809, then to kill the zombie (5878) you end the parent (4809):

`$ sudo kill -9 4809  #4809 is the parent, not the zombie`

My final word of warning about zombies. Be very careful when killing parent processes. If the parent of a process is PID 1 and you kill that, you'll reboot yourself!

And that will be an even scarier story to tell!
