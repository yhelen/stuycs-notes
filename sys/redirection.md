# 11/27 Aim: Redirection; how does it ... SQUIRREL

## File Redirection

Changing the usual input/output behavior of a program.

### Command Line Redirection
* `>`
    * Redirects stdout to a file
    * Overwrites the contents of the file
    ```
    $ <COMMAND> > <FILE>
    $ ls > file_list
    ```
* `>>`
    * Redirects stdout to a file by appending
* `2>`
    * Redirects stderr to a file
    * Overwrites the file (`2>>` appends)
* `&>`
    * Redirect stdout and stderr (`&>>` appends)
* `<`
    * Redirects stdin from a file
* `|` (pipe)
    * Redirects stdout from one command to stdin of the next
    * `ls | wc`

### Redirection in c programs

#### `dup - <unistd.h>`

Duplicates an existing entry in the file table.

Returns a new file descriptor for the duplicate entry.

```c
dup( fd )
```

#### `dup2 - <unistd.h>`

```c
dup2(fd1, fd2)
```

Redirects fd2 to fd1

Duplicates the behavior for fd1 at fd2.

You will lose any reference to the origianl fd2, that file will be closed.

Effective redirection of stdout:

```c
int x = dup(1);
dup2(3, 1);

...

dup2(x, 1);
close(x);
```
