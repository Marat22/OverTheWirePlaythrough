# [Level 0](https://overthewire.org/wargames/bandit/bandit0.html)
## Task:
Log into the level with SSH.

Server: bandit.labs.overthewire.org

Port: 2220

Username: bandit0

Password: bandit0
## Solution:
```console
ssh bandit.labs.overthewire.org "2220" -l bandit0
```

# [Level 1](https://overthewire.org/wargames/bandit/bandit1.html)
## Task:
The password for the next level is stored in a file called readme located in the home directory.

## Solution:
```console
bandit0@bandit:~$ cat readme | grep pass
The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
bandit0@bandit:~$ 
```

password: `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

# [Level 2](https://overthewire.org/wargames/bandit/bandit2.html)
## Task:
Get the password from the file called ‘-’.

## Solution:
```console
bandit1@bandit:~$ cat "./-"
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

# [Level 3](https://overthewire.org/wargames/bandit/bandit3.html)
## Task:
The password for the next level is stored in a file called spaces in this filename located in the home directory.

## Solution:
```console
bandit2@bandit:~$ cat "./--spaces in this filename--" 
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

password: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

# [Level 4](https://overthewire.org/wargames/bandit/bandit4.html)
## Task:
The password for the next level is stored in a hidden file in the inhere directory.

## Solution:
```console
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls --all
.  ..  ...Hiding-From-You
bandit3@bandit:~/inhere$ cat "./...Hiding-From-You"
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

password: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

# [Level 5](https://overthewire.org/wargames/bandit/bandit5.html)
## Task:
The password for the next level is stored in the only human-readable file in the inhere directory.

## Solution:
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

# [Level 6](https://overthewire.org/wargames/bandit/bandit6.html)
## Task:
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

## Solution:
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

# [Level 7](https://overthewire.org/wargames/bandit/bandit7.html)
## Task:
Find a file somewhere on the server. Properties:
1. owned by user bandit7
2. owned by group bandit6
3. 33 bytes in size

## Solution:
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

# [Level 8](https://overthewire.org/wargames/bandit/bandit8.html)
## Task:
Get the password from a file, next to the word millionth

## Solution:
```console
bandit7@bandit:~$ cat data.txt | grep millionth
millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

password: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

# [Level 9](https://overthewire.org/wargames/bandit/bandit9.html)
## Task:
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once.

## Solution:
```console
bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

password: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

# [Level 10](https://overthewire.org/wargames/bandit/bandit10.html)
## Task:
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

## Solution:
`strings` displays printable strings:

```console
bandit9@bandit:~$ strings data.txt | grep ==
========== the
========== password
f\Z'========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

# [Level 11](https://overthewire.org/wargames/bandit/bandit11.html)
## Task:
The password for the next level is stored in the file data.txt, which contains base64 encoded data.

## Solution:
`base64` allows to decode files

```console
bandit10@bandit:~$ cat data.txt | base64 --decode
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```
# [Level 12](https://overthewire.org/wargames/bandit/bandit12.html)
## Task:
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

## Solution:
Using `tr` for translation and wikipedia to find description of ROT13 cipher...

![alt text](bandit_images/level12-rot13-table.png)

... I decoded `data.txt`

```console
bandit11@bandit:~$ cat data.txt | tr 'A-MN-Za-mn-z' 'N-ZA-Mn-za-m'
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

# [Level 13](https://overthewire.org/wargames/bandit/bandit13.html)
## Task:
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level, it may be useful to create a directory under /tmp in which you can work using mkdir.

## Solution:
Algorithm:
- use `xxd` and `cat` to anylise file. It can be:
  - if result of `xxd file` starts with `42 5A 68` -> add `.bz` file extention and use `bzip2 -d` to decode file
  - if result of `xxd file` starts with `1f 8b` -> add `.gz` file extention and use `gzip -d` to decode file
  - if result of `cat file` includes some human readable info -> add `.tar` file extention and use `tar -xf` to decode file

```console
bandit12@bandit:/tmp/tmp.GKXFU5WIyU$ xxd data8.bin 
00000000: 1f8b 0808 2e17 ee68 0203 6461 7461 392e  .......h..data9.
00000010: 6269 6e00 0bc9 4855 2848 2c2e 2ecf 2f4a  bin...HU(H,.../J
00000020: 51c8 2c56 70f3 374d 2977 2b4e 3648 4e4a  Q.,Vp.7M)w+N6HNJ
00000030: f4cc f430 c8b0 f032 4a0d cd2e 362a 4b09  ...0...2J...6*K.
00000040: 7129 77cc e302 003e de32 4131 0000 00    q)w....>.2A1...
bandit12@bandit:/tmp/tmp.GKXFU5WIyU$ mv data8.bin  data8.gz
bandit12@bandit:/tmp/tmp.GKXFU5WIyU$ gzip -d data8.gz 
bandit12@bandit:/tmp/tmp.GKXFU5WIyU$ ls
compressed_data.tar  data5.bin  data6.bin.out  data8  hexdump_data
bandit12@bandit:/tmp/tmp.GKXFU5WIyU$ cat data
data5.bin      data6.bin.out  data8          
bandit12@bandit:/tmp/tmp.GKXFU5WIyU$ cat data8
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

# [Level 14](https://overthewire.org/wargames/bandit/bandit14.html)
## Task:

## Solution:
1. Find ssh key
```console
bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$ cat sshkey.private 
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```
2. Copy ssh key to local machine
```console
$ scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit13@bandit.labs.overthewire.org's password: 
sshkey.private                                                                   100% 1679    17.7KB/s   00:00    
```
3. Try to connect:
```console
$ ssh bandit.labs.overthewire.org -p 2220 -l bandit13 -i sshkey.private
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for 'sshkey.private' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "sshkey.private": bad permissions
bandit13@bandit.labs.overthewire.org's password: 
```
4. Make `sshkey.private` read-only:
```console
$ chmod 400 ./sshkey.private 
```
5. Finally connect:
```console
$ ssh bandit.labs.overthewire.org -p 2220 -l bandit13 -i sshkey.private
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit13@bandit.labs.overthewire.org's password: 
```

# [Level 15](https://overthewire.org/wargames/bandit/bandit15.html)
## Task:

## Solution:

# [Level 16](https://overthewire.org/wargames/bandit/bandit16.html)
## Task:

## Solution:

# [Level 17](https://overthewire.org/wargames/bandit/bandit17.html)
## Task:

## Solution:

# [Level 18](https://overthewire.org/wargames/bandit/bandit18.html)
## Task:

## Solution:

# [Level 19](https://overthewire.org/wargames/bandit/bandit19.html)
## Task:

## Solution:

# [Level 20](https://overthewire.org/wargames/bandit/bandit20.html)
## Task:

## Solution:


