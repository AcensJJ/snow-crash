# level00 solve

First, we tried to find if we got some information about the flag00.

```
$ find / -user flag00 2> /dev/null
```

After running the command, two results appear.

```
> /usr/sbin/john
> /rofs/usr/sbin/john
```

They got the same value when we go through the file.

```
$ cat /usr/sbin/john
> cdiiddwpgswtgt
```

After some attempt, we see the password didn't work.
So we decide to go on the <a href="https://dcode.fr">dcode.fr</a> website, talked in the <a href="https://elearning.intra.42.fr/notions/snow-crash/subnotions/snow-crash/videos/snow-crash">school video</a>.

And after some research on the website, we find the decrypted part and try to unlock it.
The most rational word was:

` A=1, B=15, nottoohardhere `

Try again to log on the user flag00 with the new password

```
$ su flag00
$ nottoohardhere
> Don't forget to launch getflag!
$ getflag
> Check flag.Here is your token : x24ti5gi3x0ol2eh4esiuxias
```

We got it!

> <a href="../flag">flag</a> - <a href="../../level01">next level</a>
