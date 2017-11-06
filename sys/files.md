# 10/24 Aim: File this under useful information

What are the different kinds of file permissions?

## File permissions
* read|write|execute
* user|group|others

Permissions can be represented as 3-digit binary #s, or 1-digit octals.
* 100 <==> 4 => read, only
* 111 <==> 7, read, write, execute

There are 3 permission "areas": user, group, others. Each area can have its own
permissions.
* 0644 => user: read+write, group: read, other: read

## File Table
A list of all the files used by a program while it is running. Contains basic
information like the file's location & size.

The file table has a limited size, which is a power of 2 and commonly 256.
`getdtablesize()` will return this value.

*NOTE:* `getdtablesize()` *IS DEPRECATED*

Each file is given an integer index, starting at 0, this is referred to as the
file descriptor.

There are 3 files always open in the table:
* 0 or `STDIN_FILENO`: stdin
* 1 or `STDOUT_FILENO`: stdout
* 2 or `STDERR_FILENO`: stderr

---

# 10/25 Aim: Opening up a world of possibilities

## `open - <fcntl.h>`

Adds a file to the file table and returns its file dscriptor.
If open fails, -1 is returned, extra error information can be found
can be found in `errno`.
* `errno` is an int variable that can be found in `<errno.h>`, using
  strerror (in `string.h`) on errno will return a string description
  of the error.

`open( <PATH> , <FLAGS> , <MODE> )`

* mode
  - Only used when creating a file. Set the new file's permissions using a
    3 digit octal #
* flags
  - Determine what you plan to do with the file
  - Use only the following constants:
    * `O_RDONLY`
    * `O_WRONLY`
    * `O_RDWR`
    * `O_APPEND`
    * `O_TRUNC`
    * `O_CREAT`
    * `O_EXCL`: when combined with `O_CREAT`, will return an error if the file
      exists
  - Each flag is a number, to combine flags we use bitwise OR
    ```
    O_WRONLY = 1            00000001
    O_APPEND = 8            00001000
    O_WRONLY | O_APPEND =   00001001
    ```

---

# 10/26 Aim: Read your writes!

## `umask - <sys/stat.h>`

Set the file creation permission mask.

By default, created files are not given the exact permissions provided in
the mode argument to open. Some permissions are automatically off.

Umask is applied in the following way:
```
new_permissions = ~mask & mode
```
The default mask is `0002`.
```
mode = 666      110 110 110
umask = 022     000 010 010

~umask =        111 101 101
& mode =        110 110 110
                110 100 100
```
You can define the mask using a 3 digit octal #:
```
umask( <MASK> );
```

## `read - <unistd.h>`

Read in data from a file.
```
read( <FILE DESCRIPTOR>, <BUFFER>, <AMOUNT> )

read( fd, buff, n )
```

Read n bytes from the fd's file and put that data into buff. Returns
the number of bytes actually read. Returns `-1` and sets `errno` if unsuccessful.

`BUFFER` must be a pointer.

## `write - <unistd.h>`

Write data to a file.
```
write( <FILE DESCRIPTOR>, <BUFFER>, <AMOUNT>)

write( fd, buff, n )
```

Write n bytes from buff into fd's file. Returns the number of bytes actually
written. Returns `-1` and sets `errno` if unsuccessful.

`BUFFER` must be a pointer.

YOU CAN READ AND WRITE BINARY DATA.

---

# 10/30 Aim: Seek and ye shall find

C is pass-by-value!! If you want the fxn to modify the argument, pass a pointer.
(Which is why read/write take pointers)

## `lseek - <unistd.h>`

Set the current position in an open file.

```c
lseek( <FILE DESCRIPTOR>, <OFFSET>, <WHENCE> )
```

* offset: Number of bytes to move the position by. Can be negative.
* whence:
    - Where to measure the offset from.
        * `SEEK_SET` offset is evaluated from the beginning of the file
        * `SEEK_CUR` offset is relative to the current position in the file
        * `SEEK_END` offset is evaluated from the end of the file
    - Returns the number of bytes the current position is from the beginning
      of the file, or -1 (errno)

## `stat - <sys/stat.h>`

Get information about a file (metadata)

```
stat( <PATH>, <STAT BUFFER> )


struct stat sb;
stat("foo", &sb);
```

* STAT BUFFER
    - Must be a poitner to a struct stat
    - All teh file information gets put into the stat buffer
    - Some of the fields in struct stat:
        * `st_size` - file size in bytes
        * `st_uid`, `st_gid` - user id, group id
        * `st_mode` - file permissiosn
        * `st_atime`, `st_mtime` - last access, last modfiication
            - These are time_t variables. We can use functions in
              `time.h` to make sense of them:
                * `ctime( <TIME> )`
                    - TIME is type time_t *
                    - Returns the time as a string

---

# 11/01 Aim: Where do compsci priests keep their files? In directory!

## Directories

A *nix directory is a file containing the names of the files within the
directory along with basic information, like file type.

Moving files into/out of a directory means changing the directory file,
not actualy moving any data.

## `opendir - <dirent.h>`

Open a directory file.

This will not change the current working directory (cwd), it only allows
your program to read the contetns of the directory file.

```
opendir( <PATH> )
```

Returns a pointer to a directory stream (`DIR *`)

## `closedir - <dirent.h>`

Closes the directory stream and frees teh pointer associated with it.

```
closedir( <DIRECTORY STREAM *> )
```

## `readdir - <dirent.h>`

```
readdir( <DIRECTORY STREAM *> )
```

Returns a pointer to the next entry in a directory stream, or NULL if
all the entries have already been returned.

### `struct dirent - <sys/types.h>`

Directory struct that contains information stored in a directory file.

Some of the data members:
* `d_name`: Name of the file
* `d_type`: File type as an int

example:
```c
DIR * d;
d = opendir( "somedir" );
struct dirent *entry;
entry = readdir(d);
```
