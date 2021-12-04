# level14 solve

Well, we got nothing on the folder... But well, we learn about the binary search, so why not trying it on the getflag.

```
$ gdb getflag
$ layout asm
```

And we got... Amont of line, well, let's find the first cmp we spot, and that time it's a ` test ` on ` 0x804898e ` and he continued on more check too, let's find an another way to go.

After scrolling down the file we can see multiple ft_des like the binary of the last level.

Ok I got a theory, maybe all ft_des are the values of each getflag, let's count of many we got, 1, 2, 3, .. 13, and 14! And each on the row, one after one.

Ok, maybe that all ft_des are the flag of each level, lets try the last ft_des, going a little up for letting him preparing is own value, so going to the ` 0x8048de5 `

Doing the same manipulation of the last level

```
$ break *0x804898e
> Breakpoint 1, 0x804898e in main ()
$ run
$ jump *0x8048de5
> Continuing at 0x8048de5
> 7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ
```

Ok that maybe the flag...

```
$ su flag14
> 7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ
> Congratulation. Type getflag to get the key and send it to me the owner of this livecd :)
$ getflag
> Check flag.Here is your token : 7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ
```

Wait, can we go other flag doing the same manipulation on other flag?
Yeah that works too, that will be easier than do all levels...

> <a href="../flag">flag</a> - <a href="../../level13">previous level</a> 
