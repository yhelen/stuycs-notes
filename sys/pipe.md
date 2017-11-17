# 11/17 Aim: Ceci n'est pas une pipe

## Pipe

A conduit between two separate processes on the same computer.

Pipes have 2 ends a read end and a write end.

Pipes are unidirectional (a single pipe must be eitehr read or write
only in a process).

Pipes act just like files.

You can transfer any data you like through a pipe using read/write.

Unanamed pipes have no external identifier.

### `pipe - <unistd.h>`

Create an unnamed pipe.

Returns 0 if the pipe was created, -1 if not.

Opens both ends of the pipe as files.

```c
pipe( int descriptors[2] )
```

* `descriptors`: Array that will contain the descriptors for each end
  of the pipe.

#### Example

```c
int f;
int fds[2];
pipe(fds);
f = fork();

if (f==0) {
    close(fds[READ]);
    char s[10] = "hello";
    sleep(2);
    write(fds[WRITE], s, siezeof(s));
} else {
    close(fds[WRITE];
    char s[10];
    read(fds[READ], s, sizeof(s));
    printf("parent received: [%s]\n", s);
}
```
