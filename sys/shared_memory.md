# 12/01 Aim: Sharing is caring!

## Shared Memory

```
<sys/shm.h> <sys/ipc.h> <sys/types.h>
```

A segment of heap memory that can be accessed by multiple processes.

Shared memory is accessed via a key that is known by any process that
needs to access it.

Shared memory does not get released when a program exits.

### 5 Shared Memory Operations:
1. Create the segment (happens once)
2. Access the segment (happens once per process)
3. Attach the segment to a variable (once per process)
4. Detach the segment from a variable (once per process)
5. Remove the segment (happens once)

#### `shmget`

Create or access a shared memory segment.

Returns a shared memory descriptor (similar concept to a file descriptor),
or -1 if it fails. (errno)

```c
shmget( key, size, flags )
```

* `key`: Unique integer identifier for teh shared memory segment (like
  a file name)
* `size`: How much memory to request.
* `flags`: Includes permissions for the segment, combined with bitwise or
    - `IPC_CREAT`: Create the segment. If the segment is new, will set
      value to all 0s
    - `IPC_EXCL`: Fail if the segment already exists and `IPC_CREAT` is on

#### `schmat`

Attach a shared memory segment to a variable.

Returns a pointer to the segment, or -1 (errno).

```c
shmmat( descriptor, address, flags )
```

* `descriptor`: the return value of `shmget`
* `address`: If 0, the OS will provide the appropriate address.
* `flags`: Usually 0, there is only one useful flags.
    - `SHM_RDONLY`: makes the memory read only
