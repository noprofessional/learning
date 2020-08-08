# fork and exec

> [quato](https://pubs.opengroup.org/onlinepubs/009604599/functions/fork.html)
>
> There are two reasons why POSIX programmers call `fork()`:
> 1. Create a new thread of control within the same program<br>
>    (which was originally only possible in POSIX by creating a new process)
> 2. Create a new process running a different program.<br>
>    In this case, the call to `fork()` is soon followed by a call to one of the `exec` functions.

So to sum up:

    * fork is used to create new process
    * exec is used to change the program which the process is running

# FD_CLOEXEC and O_CLOEXEC

When use `fork` to create new process. `fork` will do a [almost complete duplicate](https://www.man7.org/linux/man-pages/man2/fork.2.html)
of the current process. 

In the procedure, **fd** as **file descriptors** will be duplicated as well.

The `exec` call will release the memory that holds the file descriptors without `close` them

So you have to close them before `exec` call.

Since it's usually hard to keep track all the fds that need to be closed,

unix provide the fd_flag `FD_CLOEXEC` to mark fd as need to close if `exec` call are successful.

In oder to set this flag in linux older than 2.6.23, you need set flag after fd creation

```c
//get fd
int fd=open("foo.txt",O_RDONLY);
//below is set flag
int flags = fcntl(fd, F_GETFD);  
flags |= FD_CLOEXEC;  
fcntl(fd, F_SETFD, flags);  
```

While in linux 2.6.23 and newer version, you can pass the O_CLOEXEC when creating the fd

```c
//get fd
int fd=open("foo.txt",O_RDONLY|O_CLOEXEC);
```

