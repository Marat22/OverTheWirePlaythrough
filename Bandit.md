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
