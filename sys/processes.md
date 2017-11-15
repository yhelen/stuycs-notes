# 11/6 Aim: Are your processes running? Then you should catch them!

## Processes

Every running program is a process. A process can create subprocesses, but
these are no different from regular processes.

A processor can handle 1 process per cycle (per core).

"Multitasking" hears to happen because the processor switches between
all the active processes quickly.

### pid

Every process has a unique identifier called the `pid`.

`pid 1` is the init process.

Each entry in the `/proc` directory is a current pid.

---

# 11/8 Aim: Sending mixed signals

## Signals

Limited way of sending information to a process.

### `kill`

Command line utility to send a signal to a process.

```
$ kill <PID>
```

Sends signal 15 (`SIGTERM`) by default to PID

```
$ kill -<SIGNAL> <PID>
```

Sends `SIGNAL` to PID

### `killall [<SIGNAL>] <PROCESS>`

Sends `SIGTERM` (or `SIGNAL` if provided) to all processes with `PROCESS` as
the name

## Signal handling in c programs `<signal.h>`

### `kill`
```
kill(<PID>, <SIGNAL>)
```

Returns 0 on sucess or -1 (errno) on failure.

### `sighandler`

To intercept signals in a c program you must create a signal handling
function.

Some signals (like `SIGKILL`) cannot be caught.

```c
static void sighandler( int signo )
```

Must be static, must be void, must take a single int parameter.

`static`: the function can only be called from within the file it
is defined.

### `signal`

After you create the funtion, you attach the signal to it usin
the signal function:

```c
signal( SIGNUMBER, sighandler )
```

---

# 11/9 Aim: Time to make an executive decision

## The `exec` family - `<unistd.h>`

There are a number of c functions that can be used to run other programs
from within.

Replaces the current process with the new program.

---

# 11/13 Aim: What the fork?

## Managing Sub-Processes

### `fork() - <unistd.h>`

Creates a separate process based on the current one, the new process
is called a child, the original one is the parent.

The child process is a duplicate of the parent process.
All parts of the parent process are copied, including stack & heap
memory, and the file table.

Returns 0 to the child and the child's pid to the parent or -1 (errno).

---

# 11/14 Aim: Wait for it

## `wait - <unistd.h>`

Stops a parent process from running until any child has provided status
information to the parent via a signal. (usually the child has exited)

Returns the pid of the child that exited, or -1 (errno).

```c
wait( int *status )
```

The parameter (`status`) is used to store information about how the process
has exited.

---

# 11/15 Aim: Playing Favorites

## Endian-ness

### Big-Endian vs. Little-Endian

Order of the bytes:
* Little-endian: Least significant bytes are first.
* Big-endian: Most significant bytes are first.

Note: Order of the bits remain the same.

## `waitpid - <unistd.h>`

Waits for a specific child.

```c
waitpid(pid, status, options)
```

* `pid`: The pid of the specific child to look for. If -1, will look for any.
* `options`: Can set other behavior for wait, if 0, will work normally.
