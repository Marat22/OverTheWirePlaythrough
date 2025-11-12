# Level 0
Entered:
```console
ssh bandit.labs.overthewire.org "2220" -l bandit0
```

# Level 1
```console
bandit0@bandit:~$ cat readme | grep pass
The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
bandit0@bandit:~$ 
```

password: `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

# Level 2
```console
bandit1@bandit:~$ cat "./-"
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

# Level 3
```console
bandit2@bandit:~$ cat "./--spaces in this filename--" 
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

password: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

# Level 4
```console
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls --all
.  ..  ...Hiding-From-You
bandit3@bandit:~/inhere$ cat "./...Hiding-From-You"
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

password: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

# Level 5
```console
bandit4@bandit:~$ file inhere/*
inhere/-file00: data
inhere/-file01: OpenPGP Public Key
inhere/-file02: OpenPGP Public Key
inhere/-file03: data
inhere/-file04: data
inhere/-file05: data
inhere/-file06: data
inhere/-file07: ASCII text
inhere/-file08: data
inhere/-file09: data
bandit4@bandit:~$ cat "inhere/-file07"
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

password: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

# Level 6
All non-executable files:
```console
bandit5@bandit:~$ find inhere/ -type f ! -executable | grep 07
inhere/maybehere07/.file2
inhere/maybehere07/spaces file2
inhere/maybehere07/-file2
```

All 1033 bytes files:
```console
bandit5@bandit:~$ du --bytes --all inhere/ | grep 1033
1033    inhere/maybehere07/.file2
bandit5@bandit:~$ cat inhere/maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

All human-readable files:
```console
bandit5@bandit:~/inhere$ file */{.,}* | grep "ASCII text" | grep -v 'with very long lines' 
maybehere10/.file2:       ASCII text
maybehere15/.file2:       ASCII text
maybehere01/-file2:       ASCII text
maybehere08/spaces file1: ASCII text
maybehere12/-file2:       ASCII text
maybehere15/spaces file2: ASCII text
maybehere18/-file2:       ASCII text
```

password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

# Level 7
We need:
- file, so we use `-type f`,
- owned by user `bandit7`, so we use `-user bandit7`,
- owned by user group `bandit6`, so we use `-group bandit6`,
- size of 33 bytes, so we use `-size 33c`

```console
bandit6@bandit:~$ find  / -type f -user bandit7 -group bandit6 -size 33c
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/2/task/2/fd’: Permission denied
find: ‘/proc/2/task/2/fdinfo’: Permission denied
find: ‘/proc/2/task/2/ns’: Permission denied
find: ‘/proc/2/fd’: Permission denied
find: ‘/proc/2/map_files’: Permission denied
find: ‘/proc/2/fdinfo’: Permission denied
find: ‘/proc/2/ns’: Permission denied
find: ‘/proc/79/task/79/fdinfo/6’: No such file or directory
find: ‘/proc/79/fdinfo/5’: No such file or directory
find: ‘/lost+found’: Permission denied
find: ‘/var/tmp’: Permission denied
find: ‘/var/spool/bandit24’: Permission denied
find: ‘/var/spool/cron/crontabs’: Permission denied
find: ‘/var/spool/rsyslog’: Permission denied
find: ‘/var/lib/update-notifier/package-data-downloads/partial’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/polkit-1’: Permission denied
find: ‘/var/lib/chrony’: Permission denied
find: ‘/var/lib/udisks2’: Permission denied
find: ‘/var/lib/snapd/cookie’: Permission denied
find: ‘/var/lib/snapd/void’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/ubuntu-advantage/apt-esm/var/lib/apt/lists/partial’: Permission denied
/var/lib/dpkg/info/bandit7.password
find: ‘/var/lib/amazon’: Permission denied
find: ‘/var/crash’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/pollinate’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/cache/apparmor/208b6430.0’: Permission denied
find: ‘/var/cache/apparmor/0fb44ac6.0’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/log’: Permission denied
find: ‘/sys/kernel/tracing/osnoise’: Permission denied
find: ‘/sys/kernel/tracing/hwlat_detector’: Permission denied
find: ‘/sys/kernel/tracing/instances’: Permission denied
find: ‘/sys/kernel/tracing/trace_stat’: Permission denied
find: ‘/sys/kernel/tracing/per_cpu’: Permission denied
find: ‘/sys/kernel/tracing/options’: Permission denied
find: ‘/sys/kernel/tracing/rv’: Permission denied
find: ‘/sys/kernel/debug’: Permission denied
find: ‘/sys/fs/pstore’: Permission denied
find: ‘/sys/fs/bpf’: Permission denied
find: ‘/drifter/drifter14_src/axTLS’: Permission denied
find: ‘/tmp’: Permission denied
find: ‘/snap’: Permission denied
find: ‘/home/bandit31-git’: Permission denied
find: ‘/home/leviathan4/.trash’: Permission denied
find: ‘/home/drifter8/chroot’: Permission denied
find: ‘/home/bandit29-git’: Permission denied
find: ‘/home/bandit27-git’: Permission denied
find: ‘/home/drifter6/data’: Permission denied
find: ‘/home/bandit5/inhere’: Permission denied
find: ‘/home/bandit28-git’: Permission denied
find: ‘/home/leviathan0/.backup’: Permission denied
find: ‘/home/ubuntu’: Permission denied
find: ‘/home/bandit30-git’: Permission denied
find: ‘/boot/efi’: Permission denied
find: ‘/boot/lost+found’: Permission denied
find: ‘/run/pam_pidns’: Permission denied
find: ‘/run/udisks2’: Permission denied
find: ‘/run/chrony’: Permission denied
find: ‘/run/user/11014’: Permission denied
find: ‘/run/user/11020’: Permission denied
find: ‘/run/user/11019’: Permission denied
find: ‘/run/user/11007’: Permission denied
find: ‘/run/user/12006’: Permission denied
find: ‘/run/user/11010’: Permission denied
find: ‘/run/user/11021’: Permission denied
find: ‘/run/user/11011’: Permission denied
find: ‘/run/user/11009’: Permission denied
find: ‘/run/user/11017’: Permission denied
find: ‘/run/user/11022’: Permission denied
find: ‘/run/user/12002’: Permission denied
find: ‘/run/user/11025’: Permission denied
find: ‘/run/user/11024’: Permission denied
find: ‘/run/user/11001’: Permission denied
find: ‘/run/user/11004’: Permission denied
find: ‘/run/user/11006/systemd/inaccessible/dir’: Permission denied
find: ‘/run/user/11023’: Permission denied
find: ‘/run/user/11013’: Permission denied
find: ‘/run/user/11000’: Permission denied
find: ‘/run/user/11005’: Permission denied
find: ‘/run/user/11012’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/run/screen/S-bandit16’: Permission denied
find: ‘/run/screen/S-bandit18’: Permission denied
find: ‘/run/screen/S-bandit1’: Permission denied
find: ‘/run/screen/S-bandit25’: Permission denied
find: ‘/run/screen/S-bandit23’: Permission denied
find: ‘/run/screen/S-bandit19’: Permission denied
find: ‘/run/screen/S-bandit20’: Permission denied
find: ‘/run/multipath’: Permission denied
find: ‘/run/cryptsetup’: Permission denied
find: ‘/run/lvm’: Permission denied
find: ‘/run/systemd/propagate/fwupd.service’: Permission denied
find: ‘/run/systemd/propagate/ModemManager.service’: Permission denied
find: ‘/run/systemd/propagate/polkit.service’: Permission denied
find: ‘/run/systemd/propagate/chrony.service’: Permission denied
find: ‘/run/systemd/propagate/systemd-logind.service’: Permission denied
find: ‘/run/systemd/propagate/irqbalance.service’: Permission denied
find: ‘/run/systemd/propagate/systemd-networkd.service’: Permission denied
find: ‘/run/systemd/propagate/systemd-resolved.service’: Permission denied
find: ‘/run/systemd/propagate/systemd-udevd.service’: Permission denied
find: ‘/run/systemd/inaccessible/dir’: Permission denied
find: ‘/run/lock/lvm’: Permission denied
find: ‘/etc/multipath’: Permission denied
find: ‘/etc/stunnel’: Permission denied
find: ‘/etc/credstore.encrypted’: Permission denied
find: ‘/etc/sudoers.d’: Permission denied
find: ‘/etc/xinetd.d’: Permission denied
find: ‘/etc/polkit-1/rules.d’: Permission denied
find: ‘/etc/credstore’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
find: ‘/root’: Permission denied
find: ‘/manpage/manpage3-pw’: Permission denied
find: ‘/dev/mqueue’: Permission denied
find: ‘/dev/shm’: Permission denied
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

password: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

# Level 8
```console
bandit7@bandit:~$ cat data.txt | grep millionth
millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

password: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

# Level 9
```console
bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

password: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

# Level 10
```console
bandit9@bandit:~$ strings data.txt | grep ==
========== the
========== password
f\Z'========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```
