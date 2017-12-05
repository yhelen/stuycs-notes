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

---

# 12/04 Aim: Memes

## Shared memory (cont.)

#### `shmdt`

Detach a variable from a shared memory segment.

Returns 0 upon success or -1 upon failure.

```c
shmdt( pointer )
```

* `pointer`: The address used to access the segment.

#### `shmctl`

Perform operations on the shared memory segment. Each shared memory segment
has metadata that can be stored in a struct (`struct shmid_ds`)

Some of the metadata stored: last access, size, pid of creator, pid of
last modification.

```c
shmctl( descriptor, command, buffer )
```

* `descriptor`: Return value of shmget
* `commands`:
    - `IPC_RMID`: Remove a shared memory segment
    - `IPC_STAT`: Populate the buffer (`struct shmid_ds`) with segment metadata
    - `IPC_SET`: Set some of the segment metadata from buffer

---

# 12/05 Aim: How do you flag down a resource?

**DN**: How would you control access to a shared resource like a file, pipe,
or shared memory, such that you could ensure no read/write conflicts
occurred?

## Semaphores

(Created by Edsger Dijkstra)

IPC construct used to contro laccess to a shared resource (like a file
or shpared memory). Most commonly, it's used as a counter representing
how many processes can access a resource at a given time.

If a semaphore has a value of 3, then it can have 3 active "users". If
it has a value of 0, then it is unavailable.

Most semaphore operators are "atomic", meaning they will not be split
up into multiple processor instructions.

### Semaphore operations

1. Create a semaphore
2. Set an initial value
3. Remove a semaphore
4. `Up(S) / V(S)` - atomic:
    - Release the semaphore to signal you are done with its associated
      resource
    - Pseudocode: `S++`
5. `Down(S) / P(S)` - atomic:
    - Attempt to take the semaphore
    - If the semaphore is 0, wait for it to be available
    - Pseudocode:
        - `while (S == 0) {block} S--;`

### Semaphores in C - `<sys/types.h> <sys/ipc.h> <sys/sem.h>`

#### `semget`

Create/Get access to a semaphore. This is not the same as `Up(S)` or `Down(S)`,
it does not modify the semaphore.

Returns a semaphore descriptor or -1 (errno).

```c
semget( <KEY>, <AMOUNT>, <FLAGS>
```

* `KEY`: Unique semaphore identifier (use ftok)
* `AMOUNT`: Semaphores are stored as sets of one or more. The number of
  semaphores to create/get.
* `FLAGS`: Includes permissions for the Semaphore, combine with bitwise or
    - `IPC_CREAT`
    - `IPC_EXCL`
