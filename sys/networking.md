# 1/02 Aim: Socket To Me

## Socket

A connection between 2 programs over a network.

A socket corresponds to an IP (internet protocol) Address / Port pair.

### To use a socket

1. Create the socket
2. Bind it to an address and port
3. Listen/initiate a connection
4. Send/receive data

## IP Addresses

All devices connected to the internet have an IP address.
IP address come in 2 flavors IPv4 and IPv6.
Addresses are allocated in blocks to make routing easier.
* IPv4: 4 byte addresses of the form:
    * [0-255].[0-255].[0-255].[0-255]
    * Each group is called an octet
    * At most there are 2^32 or ~4.3 billion IPv4 addresses
* IPv6: 16 byte addresses of the form:
    * [0-ffff]:[0-ffff]:[0-ffff]:[0-ffff]:[0-ffff]:[0-ffff]:[0-ffff]:[0-ffff]
    * Each group is known as a hextet (not as standard as octet)
    * Leading 0s are ignored
    * Any number of consecutive all 0 hextets can be replaced with : :
        * 0000:0000:0000:0000:004f:12c2:0009:a2d2
        * ::4f:13c2:9:a2d2
    * IPv4 Addresses can be represented as 5 0-hextets, 1 ffff hextet, and the IP, ::ffff:129.89.150.000
    * There are 2^128 IPv6 addresses

## Network Ports

Allow a single computer to run multiple services.
A socket combines an IP address and port.
Each computer has 2^16 (65536) ports.

Some ports are reserved for specific services.
* 80: http
* 22: ssh
* 443: ssl

You can select any port, as long as it wont conflict with a service
running on the desired computer.
* ports < 1024 are reserved and should generally not be used
* `etc/services` will have a list of registered ports for local system

## Network Connection Types

### Stream Sockets

Reliable 2 way connection.
Must be connected on both ends.
Data is received in the order it is sent. (not as easily done as it sounds)
Most use the Transmission Control Protocol (TCP).

### Datagram Sockets

"Connectionless" - an established connection is not required.
Data sent may be received out of order (or not at all).
Uses the User Datagram Protocol.

---

# 1/05 Aim: Stop. Collaborate, and listen

## `socket - <sys/socket.h>`

Creates a socket. Returns a socket descriptor (int that works like a
file descriptor).

```c
socket(domain, type, protocol)
```

* `domain`: type of address
    * `AF_INET` or `AF_INET6`
* `type`: `SOCK_STREAM` or `SOCK_DGRAM`
* `protocol`: Combination of domain and type settings
    * If set to `0` the OS will set to the correct protocol

```c
// example
int sd = socket(AF_INET, SOCK_STREAM, 0);
```

System library calls use a `struct addrinfo` to represent network addresses
(containing information like IP address, port, protocol)

### `struct addrinfo`

#### .ai_family
* `AF_INET`: IPv4
* `AF_INET6`: IPv6
* `AF_UNPSEC`: IPv4 or IPv6

#### .ai_socktype
* `SOCK_STREAM`
* `SOCK_DGRAM`

#### .ai_flags
* `AI_PASSIVE`: Automatically set to any incoming IP address

#### .ai_addr
Pointer to a `struct sockaddr` containing the IP address

#### .ai_addrlen
Size of the address in bytes

## `getaddrinfo - <sys/types.h> <sys/socket.h> <netdb.h>`

Lookup information about the desired network address and get one or more
matching `struct addrinfo` entries.

```c
getaddrinfo(node, service, hints, results);
```

* `node`: String containing an IP address or hostname to lookup
    * If `NULL`, use the local machine's IP address
* `service`: String with a port number or service name (if the service
  is in `/etc/services`
* `hints`: Pointer to a `struct addrinfo` used to provide settings for
  the lookup (type of address, etc)
* `results`: Pointer to a `struct addrinfo` that will be a linked list
  containing entries for each matching address.

`getaddrinfo` will allocate memory for these structs

### Using `getaddrinfo`
```c
struct addr info *hints, *results;
hints = (struct addrinfo *)calloc(1, sizeof(struct addrinfo));
hints->ai_family = AF_INET;
hints->ai_socktype = SOCK_STREAM; // TCP socket
hints->ai_flags = AI_PASSIVE; //only needed on server
getaddrinfo(NULL, "80", hints, &results);
// client: getaddrinfo("149.89.150.100", "9845", hints, &results);
// do stuff...
free(hints)
freeaddrinfo(results);
```

## `bind` (server only) - `<sys/socket.h>`

Binds the socket to an address and port. Returns 0 (success) or -1 (failure).

```c
bind(socket descriptor, address, address length)
```

* `socket descriptor`: return value of `socket`
* `address`: pointer to a `struct sockaddr` representing the address
* `address length`: size of the address, in bytes

`address` and `address length` can be retrieved from `getaddrinfo`

### Using `bind`
```c
// create socket
ind sd;
sd = socket(AF_INET, SOCK_STREAM, 0);

struct addrinfo * hints, * results;
// use getaddrinfo (not shown)

bind(sd, results->ai_addr, results->ai_addrlen);
```

## `listen` (server only) - `<sys/socket.h>`

Set a socket to passively wait for a connection. Needed for stream sockets.
Does not block.

```c
listen(socket descriptor, backlog)
```

* `socket descriptor`: return value of `socket`
* `backlog`: Number of connections that can be queued up. Depending on
  the protocol, this may not do much.
