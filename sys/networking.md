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

## `accept` (server only) - `<sys/socket.h`

Accept the next client in the queue of a socket in the listen state
Used for stream sockets.
Performs the server side of the 3 way handshake.
Creates a new socket for communicating with the client, the listening
socket is not modified.
Returns a descriptor to the new socket.
Blocks until a connection attempt is made.

```c
accept(socket descriptor, address, address length);
```

* `socket descriptor`: descriptor for the listening socket
* `address`: Pointer to a `struct sockaddr_storage` that will contain
  information about the new socket after `accept` succeeds.
* `address length`: Pointer to a variable that will contain the size
  of the new socket after `accept` succeeds

### Using `listen` and `accept`

```c
// create socket
int sd;
sd = socket(AF_INET, SOCKSTREAM, 0);

// use getaddrinfo and bind

listen(sd, 10);
int client_socket;
socklen_t sock_size;
struct sockaddr_storage client_address;

client_socket = accept(sd,
                (struct sockaddr_storage *)&client_address, &sock_size);
```

## `connect` (client only) - `<sys/socket.h> <sys/types.h>`

Connect to a socket currently in the listening state.
Used for stream sockets.
Performs the client side of the 3 way handshake.
Binds the socket to an address and port.
Blocks until a connection is made (or fails).

```c
connect(socket descriptor, address, address length)
```

* `address`: Pointer to a `struct sockaddr` representing the address
* `address length`: Size of address, in bytes

Retrieved from `getaddrinfo()`

Note that the arguments mirror those of `bind()`

### Using `connect`

```c
// create socket
int sd;
sd = socket(AF_INET, SOCK_STREAM, 0);

struct addrinfo *hints, *results;
// use getaddrinfo (not shown)

connect(sd, results->ai_addr, results->ai_addrlen);
```

# 01/11 Aim: Cisco in an hour

## Layer Models of Networking

Due to the complexity of network communications, the topic is often
conceptualized into distinct layers so people can work on specific
components rather than everything at once.

The bottom layer is the most concrete, with each subsequent layer
becoming more abstract (relying less on the physical connections and
more on code).

There are various competing modes including the OSI (Open Systems
Interconnections) and TCP/IP models.

### TCP/IP Model Layers

1. Application
2. Transport
3. Internet
4. Link

### Link Layer

Point-to-point transmission between devices on the same (local) network.

Combines physically connecting computers with basic addressing and
transmission protocols.

## Physical Connection

How to transmit bits between two computers

### Link Layer

A brief history of physical connections

#### Thicknet

A single coaxial cable runs along the network. "Vampire taps" cut into
the cable and connect to a computer.

#### Thinnet
A single coaxial cable runs along the network. T-Connectors connect
computers to the main cable.

#### Token Ring

Each computer is connected in a ring to each other. Only one computer has
command of network resources at a time. This is called "having the token."
The network sends a "token" throughout the ring, which contains the
identity of the computer allowed to use the network. All other computers
must wait to use the network.

#### Ethernet

Multiple computers connect to a single hub or switch.

* Hub: Broadcasts the data to all computers
* Switch: Sends data to specific computer

# 01/12 Aim: Cisco in an hour 2: Electric Boogaloo

## Link Layer (cont)

In order for data to be sent between computers. Each computer needs a
unique address (MAC Address). The data needs to be sent in a standardized
format (Frames).

### MAC (Media Access Control) Address

6-byte hex address: `2a:00:1e:b9:70:f6`. MAC addresses only need to be
unique on the same local network.

### Ethernet Frames

Each frame has the following format:

```
prefix dest source type data checksum
  8B    6B    6B    2B          4B
```

* `prefix`: 10101010 x 7 + 10101011
* `dest` & `source`: MAC addresses
* `data`: MCU (Maximum transmission unit) of 1500B
* `checksum`: ensures data integrity

## Internet Layer

Transmission of data between two separate networks. Major features of
this layer are addressing and routing. Routers are physical devices
used to connect different local networks. Internet layer traffic
ignores the specifics of link layer traffic.

### IP Packets

Data sent over the internet layer is formatted into IP packets.

#### IPv4 packet header

type size fragment_info ttl protocol header checksum
 2B   2B       4B       1B    1B          2B

* `type`: IPv4/v6, length of header
* `size`: total size of packet
* `fragment info`: full payloads may be broken into multiple fragments. Each
  packet will count the number of fragments and its individual fragment
  number.
* `ttl (time-to-live)`: Maximum number of hops a packet can make before
  reaching its destination.
* `protocol`: TCP/UDP...
* `header checksum`: only a checksum of the header, not the full packet
* `source` and `destination`: IPv4 addresses
* `data`: MTU is 65,535 Bytes

# 01/16 Aim: Cisco in an hour 3: In 3-D

### Routing

Routers may break IPv4 packets into fragments. When a router receives a
packet, it has 2 options:
1. Send that packet to the attached local network.
2. Forward that packet to a different router.

### IPv4/IPv6 Differences

* Address space: 2\^32 vs 2\^128
* Packet format: In addition to address size change, IPv6 packet headers
  have less information. They do not include a checksum or fragment info.
* MTU: IPv6 can allot for an MTU of 2^32 (these are called jumbograms)

IPv6 puts more work onto link layer devices and individual hosts (computers).
IPv6 does not fragment packets at all, relying on other devices to
potentially take advantage of jumbograms.
IPv6 has no checksum, assuming link layer devices and hosts will check for
data integrity if needed.
