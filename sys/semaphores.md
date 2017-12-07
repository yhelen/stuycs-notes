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
semget( <KEY>, <AMOUNT>, <FLAGS>)
```

* `KEY`: Unique semaphore identifier (use ftok)
* `AMOUNT`: Semaphores are stored as sets of one or more. The number of
  semaphores to create/get.
* `FLAGS`: Includes permissions for the Semaphore, combine with bitwise or
    - `IPC_CREAT`
    - `IPC_EXCL`

# 12/07 Aim: What's a semaphore? - To control resources!

#### `semctl`

* `DATA`:
    * Variable for seting/storing semaphore metadata
    * Type `union semun`:
        * You have to declare this union in your main c file on linux machines
```c
union semun {
    int val;                // used for SETVAL
    struct semid_ds * buf;  // used for IPC_STAT and IPC_SET
    unsigned short *array;  // used for SETALL
    struct seminfo *__buf;
}
```
    * `union`?
        * A c structure designed to hold only one value at a time from
          a group of potential values.

#### `semop`

Perform an atomic semaphore operation.

You can Up/Down a semaphore by any integer value, not just 1

```c
semop( <DESCRIPTOR>, <OPERATOR>, <AMOUNT>)
```

* `AMOUNT`: The amount of semaphores you want to operate on in the
  semaphore set.
* `OPERATOR`: A pointer to a `struct sembuf`
```c
struct sembuf {
    short sem_op;
    short sem_num;
    short sem_flag;
}
```

* `sem_num`: The inex of the semaphore you want to work on.
* `sem_op`:
    * `Down(S)`: Any negative number
    * `Up(S)`: Any positive number
    * `0`: Block until the semaphore reaches 0
* `sem_flag`:
    * `SEM_UNDO`: Allow the OS to undo the given operator. Useful in the
      event that a program exits before it could release a semaphore.
    * `IPC_NOWAIT`: Instead of waiting for teh semaphore to be available,
      return an err
