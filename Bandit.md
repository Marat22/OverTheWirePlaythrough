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
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level.

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
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

## Solution:
```console
└─$ ssh bandit.labs.overthewire.org -p 2220 -l bandit14 -i sshkey.private

bandit14@bandit:~$ cat /etc/bandit_pass/bandit14 | nc localhost 30000
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

```

# [Level 16](https://overthewire.org/wargames/bandit/bandit16.html)
## Task:
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

## Solution:
```console
bandit15@bandit:~$ openssl s_client -crlf -connect localhost:30001 
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
---
Certificate chain
 0 s:CN = SnakeOil
   i:CN = SnakeOil
   a:PKEY: rsaEncryption, 4096 (bit); sigalg: RSA-SHA256
   v:NotBefore: Jun 10 03:59:50 2024 GMT; NotAfter: Jun  8 03:59:50 2034 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFBzCCAu+gAwIBAgIUBLz7DBxA0IfojaL/WaJzE6Sbz7cwDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIU25ha2VPaWwwHhcNMjQwNjEwMDM1OTUwWhcNMzQwNjA4
MDM1OTUwWjATMREwDwYDVQQDDAhTbmFrZU9pbDCCAiIwDQYJKoZIhvcNAQEBBQAD
ggIPADCCAgoCggIBANI+P5QXm9Bj21FIPsQqbqZRb5XmSZZJYaam7EIJ16Fxedf+
jXAv4d/FVqiEM4BuSNsNMeBMx2Gq0lAfN33h+RMTjRoMb8yBsZsC063MLfXCk4p+
09gtGP7BS6Iy5XdmfY/fPHvA3JDEScdlDDmd6Lsbdwhv93Q8M6POVO9sv4HuS4t/
jEjr+NhE+Bjr/wDbyg7GL71BP1WPZpQnRE4OzoSrt5+bZVLvODWUFwinB0fLaGRk
GmI0r5EUOUd7HpYyoIQbiNlePGfPpHRKnmdXTTEZEoxeWWAaM1VhPGqfrB/Pnca+
vAJX7iBOb3kHinmfVOScsG/YAUR94wSELeY+UlEWJaELVUntrJ5HeRDiTChiVQ++
wnnjNbepaW6shopybUF3XXfhIb4NvwLWpvoKFXVtcVjlOujF0snVvpE+MRT0wacy
tHtjZs7Ao7GYxDz6H8AdBLKJW67uQon37a4MI260ADFMS+2vEAbNSFP+f6ii5mrB
18cY64ZaF6oU8bjGK7BArDx56bRc3WFyuBIGWAFHEuB948BcshXY7baf5jjzPmgz
mq1zdRthQB31MOM2ii6vuTkheAvKfFf+llH4M9SnES4NSF2hj9NnHga9V08wfhYc
x0W6qu+S8HUdVF+V23yTvUNgz4Q+UoGs4sHSDEsIBFqNvInnpUmtNgcR2L5PAgMB
AAGjUzBRMB0GA1UdDgQWBBTPo8kfze4P9EgxNuyk7+xDGFtAYzAfBgNVHSMEGDAW
gBTPo8kfze4P9EgxNuyk7+xDGFtAYzAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3
DQEBCwUAA4ICAQAKHomtmcGqyiLnhziLe97Mq2+Sul5QgYVwfx/KYOXxv2T8ZmcR
Ae9XFhZT4jsAOUDK1OXx9aZgDGJHJLNEVTe9zWv1ONFfNxEBxQgP7hhmDBWdtj6d
taqEW/Jp06X+08BtnYK9NZsvDg2YRcvOHConeMjwvEL7tQK0m+GVyQfLYg6jnrhx
egH+abucTKxabFcWSE+Vk0uJYMqcbXvB4WNKz9vj4V5Hn7/DN4xIjFko+nREw6Oa
/AUFjNnO/FPjap+d68H1LdzMH3PSs+yjGid+6Zx9FCnt9qZydW13Miqg3nDnODXw
+Z682mQFjVlGPCA5ZOQbyMKY4tNazG2n8qy2famQT3+jF8Lb6a4NGbnpeWnLMkIu
jWLWIkA9MlbdNXuajiPNVyYIK9gdoBzbfaKwoOfSsLxEqlf8rio1GGcEV5Hlz5S2
txwI0xdW9MWeGWoiLbZSbRJH4TIBFFtoBG0LoEJi0C+UPwS8CDngJB4TyrZqEld3
rH87W+Et1t/Nepoc/Eoaux9PFp5VPXP+qwQGmhir/hv7OsgBhrkYuhkjxZ8+1uk7
tUWC/XM0mpLoxsq6vVl3AJaJe1ivdA9xLytsuG4iv02Juc593HXYR8yOpow0Eq2T
U5EyeuFg5RXYwAPi7ykw1PW7zAPL4MlonEVz+QXOSx6eyhimp1VZC11SCg==
-----END CERTIFICATE-----
subject=CN = SnakeOil
issuer=CN = SnakeOil
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 2103 bytes and written 373 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 4096 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: FBEE3D45C8EFAA8DB85876038BA7379767E191D387B06B410D9868B6223904E6
    Session-ID-ctx: 
    Resumption PSK: 6DE60E10F5366B083BD43022FAD5CEF61300BEF9FBE1BBD72DD056A37C42F29B13096684214BB70D27BEA36056560469
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 4a 0e 15 35 be a8 10 25-34 ef f7 1f 66 fc 2d 4c   J..5...%4...f.-L
    0010 - dd 63 6b d7 4c d6 d6 9c-1a 4c 70 8e 20 3f 48 8a   .ck.L....Lp. ?H.
    0020 - cb ca 51 42 4d c5 cb 23-1f c1 61 78 22 6b 79 0f   ..QBM..#..ax"ky.
    0030 - 62 3c ff af a9 65 97 b1-d8 2c 35 07 bf 03 ba ee   b<...e...,5.....
    0040 - 09 d6 40 1e 2e fc 42 6e-3e aa 9f f9 8d f5 b1 cf   ..@...Bn>.......
    0050 - b1 f1 2e 34 2b e9 76 22-01 a6 1e 92 e8 5e 64 4c   ...4+.v".....^dL
    0060 - 66 c7 19 7e 33 f9 5b fd-90 70 ee 45 81 58 d1 18   f..~3.[..p.E.X..
    0070 - 9e 3e 19 f2 b1 1e b5 70-b9 7c 94 cc 46 7f 50 34   .>.....p.|..F.P4
    0080 - 39 f7 a7 2d 5f bc c5 3e-1a 7b 64 c8 b3 2d 2b 6f   9..-_..>.{d..-+o
    0090 - 96 bd 7e 14 a6 9d e7 12-61 76 45 b0 a1 60 a8 e0   ..~.....avE..`..
    00a0 - 34 77 7d ba 42 d4 fc 13-58 3a 43 42 58 27 7f c7   4w}.B...X:CBX'..
    00b0 - 5d 12 bf 9e cd 04 88 ef-3d 66 3d 80 34 c9 4b 04   ].......=f=.4.K.
    00c0 - fb 4f ce 3f d5 c2 cc fc-96 ce d6 7b 24 4c 75 d9   .O.?.......{$Lu.
    00d0 - 41 1b 7a 7b e8 8e 4a c8-d6 21 d6 da b2 ad 63 ac   A.z{..J..!....c.

    Start Time: 1765012827
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 3BEF92FC4167DD4C8D3CAD3144A5649A9C5C92CCE44B82CF32FCE8F4BE388BE8
    Session-ID-ctx: 
    Resumption PSK: 9FD8B7EFE707C7982406810A737EDD996308150616A9F8C1E68A3B0A68754BA5ABF75FAE17DF2FBC979C16D5751386FE
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 4a 0e 15 35 be a8 10 25-34 ef f7 1f 66 fc 2d 4c   J..5...%4...f.-L
    0010 - 65 f5 1c 2b 7b 21 97 51-cb 4c 47 d2 7f df ae 0a   e..+{!.Q.LG.....
    0020 - 54 e3 7b 90 8e 26 4e 0c-90 4e 67 2c cd 60 03 3a   T.{..&N..Ng,.`.:
    0030 - bf 0e 59 74 f9 40 68 00-ec a2 a5 cf ff e8 aa 07   ..Yt.@h.........
    0040 - 45 f7 f4 19 2b da 5d fc-29 6b fe 7f 02 d8 6d 01   E...+.].)k....m.
    0050 - 35 54 07 2b 53 c1 59 6b-a6 e8 72 bd 63 8d ed 27   5T.+S.Yk..r.c..'
    0060 - 29 aa d5 a3 cf ee 50 3e-8f 68 07 e3 7b 57 b7 65   ).....P>.h..{W.e
    0070 - f5 67 f1 88 a9 72 09 af-e5 5e 03 52 9b e5 3b ae   .g...r...^.R..;.
    0080 - 40 ae 51 2f 5d 7a 0e 45-dd 98 89 d8 6f 8b ae 62   @.Q/]z.E....o..b
    0090 - d5 28 ca 84 cc 8e 4d 56-a7 67 a5 80 60 50 19 eb   .(....MV.g..`P..
    00a0 - dc 9e 60 01 54 89 37 a0-45 00 d3 4b 82 c1 2d f9   ..`.T.7.E..K..-.
    00b0 - 73 45 4c 5d 4c d6 0b 38-9a 52 0f 54 3e c1 20 51   sEL]L..8.R.T>. Q
    00c0 - f5 02 d2 2e 73 44 d0 d7-fe 4b 97 cf 89 e7 a0 26   ....sD...K.....&
    00d0 - 69 8e 2f 25 60 54 71 9e-e8 5d a8 6f fb a3 4e 4e   i./%`Tq..].o..NN

    Start Time: 1765012827
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

closed
```

Password for next level: `kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx`

# [Level 17](https://overthewire.org/wargames/bandit/bandit17.html)
## Task:
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

## Solution:
```console
bandit16@bandit:~$ nmap -sV localhost -p 31000-32000
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-12-16 20:14 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00023s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
bandit16@bandit:~$ openssl s_client -crlf -ign_eof -connect localhost:31790
...
---
read R BLOCK
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

closed

```

Notes:
- for some reason `nmap -sV localhost -p 31000-32000` sometimes work and sometimes doesn't. Also, you need to wait to see the result.
- `openssl s_client -crlf -ign_eof -connect localhost:31790` doesn't work without `-ign_eof`, although it worked without `-ign_eof` in previous level.

# [Level 18](https://overthewire.org/wargames/bandit/bandit18.html)
## Task:
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

**NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19**

## Solution:
```console
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< BMIOFKM7CRSLI97voLp3TD80NAq5exxk
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

# [Level 19](https://overthewire.org/wargames/bandit/bandit19.html)
## Task:
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

## Solution:
- command `scp` allowes to receive or send file from/to remote desktop
- by `-P 2220` I specify the port of remote server
- with `bandit18@bandit.labs.overthewire.org:~/readme` I specify source file
- with `./res19.txt` I specify destination

```console
┌──(marat㉿marat)-[~/Documents/OverTheWirePlaythrough]
└─$ scp -P 2220 bandit18@bandit.labs.overthewire.org:~/readme ./res19.txt
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0
bandit18@bandit.labs.overthewire.org's password: 
readme                                                                                                                                                                                                   100%   33     0.2KB/s   00:00    
                                                                                                                                                                                                                                           
┌──(marat㉿marat)-[~/Documents/OverTheWirePlaythrough]
└─$ cat res19.txt         
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

# [Level 20](https://overthewire.org/wargames/bandit/bandit20.html)
## Task:

## Solution:

