```
USERCHROOT(1)                     User Manuals                     USERCHROOT(1)

NAME
       userchroot - switch root, change directory, drop privileges and exec

SYNOPSIS
       userchroot <new-root> <new-working-dir> <executable> [arguments]

DESCRIPTION
       A  simple  program to aid in launching chroot/--rbound programs using the
       original user credentials. This program is supposed to be used with suid-
       bit set (chmod u+s).

       Arguments.

       new-root
              [mandatory] new root (must start with abs-path)

       new-working-dir
              [mandatory] new working dir, relative to post-chroot

       executable
              [mandatory]  executable name (related to new working directory) to
              execve(2)

       arguments
              [optional] additional parameters passed to target executable

SEE ALSO
       chroot(8)

Linux                             NOVEMBER 2016                    USERCHROOT(1)
```
