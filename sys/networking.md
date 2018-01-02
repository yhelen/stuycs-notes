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
    * Any number of consecutive all 0 hectets can be replaced with : :
        * 0000:0000:0000:0000:004f:12c2:0009:a2d2
        * ::4f:13c2:9:a2d2
    * IPv4 Addresses can be represented as 5 0-hextets, 1 ffff hextet, and the IP, ::ffff:129.89.150.000
    * There are 2^128 IPv6 addresses
