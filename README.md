# Pattern - a reimplementation of pattern\_create/pattern\_offset in Python
Metasploit comes with multiple very convenient scripts and utilities. Among
the most valuable for me are pattern_create and pattern_offset. I found it
increasingly annoying that both have a relatively long startup time.

So after I overheard one of my colleagues complaining about this as well,
I quickly hacked together a Python version that basically does the same.
## Usage
```
$ ./pattern
Usage: pattern (create | offset) <value> <buflen>
```
So, to create a 2048 byte pattern you run
```
$ ./pattern create 2048
Aa0Aa1Aa2[...snip...]p7Cp8Cp9Cq0Cq1Cq
```
and it outputs a unique pattern of said length. To find an offset in the
buffer, let's say f9Cg, you run
```
$ ./pattern offset f9Cg
1738
```
and the program returns the offset until the requested series. You can also
look for memory values. The values need to be little-endian and prefixed
with 0x:
```
$ ./pattern offset 0x67433966
1738
```
To make sure the program works as close to the Metasploit version as possible,
the offset mode searches through a 8192 byte pattern, just like pattern_offset.
If your pattern is longer than that, append the pattern length:
```
$ ./pattern offset 9Mc0
Not found
$ ./pattern offset 9Mc0 10000
9419
```
## Todo
- bad characters support for pattern creation
- partial matches

