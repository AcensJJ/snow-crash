# level13 solve

To begin, when we get logged and trying to see if we got the file we can see we have one binary ` level13 `

```
$ ls
> level13
```

Try what he do

```
$ ./level13
> UID 2013 started us but we we expect 4242
```

So let's investigate what we can do with him on gdb, checking directly the code in asm

```
$ gdb ./level13
$ layout asm
```

And we see a cmp on the address ` 0x0804859a `, so we put a breakpoint on him seeing the ways he going to take

```
$ break *0x0804859a
$ run
$ stepi
$ ...
```

Running the binary and we see is going throw getuid@plt after the je invalid, it's probably going to the error we see before, so let's skip it and go to the jump equal on address ` 0x080485cb `

```
$ break *0x0804859a
> Breakpoint 1, 0x0804859a in main ()
$ run
$ jump *0x080485cb
> Continuing at 0x080485cb
> your token is 2A31L79asukciNyi8uppkEuSx
```

We got it!

Hmm is going throw ft_des, what is that...

> <a href="../flag">flag</a> - <a href="../../level12">previous level</a> - <a href="../../level14">next level</a>
