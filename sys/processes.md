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
