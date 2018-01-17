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

---

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

```
type size fragment_info ttl protocol header checksum
 2B   2B       4B       1B    1B          2B
```

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

---

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

---

# 01/17 Aim: Cisco in an hour IV: A New Hope

## Transport Layer

Computer to computer connection over a network.
Unconcerned with the individual hops of layer 3 traffic.
Network ports are used at the transport layer.
TCP and UDP are transport layer protocols.

## Application Layer

Everything else...

## Data Encapsulation

As data crosses from an upper layer to a lower one, layer-specific metadata
is added to help aid transmission.

### Application &rarr; Transport

UDP or TCP headers are added, including network port info.

### Transport &rarr; Network

Data (including Transport headers) is packaged into IP packets.

### Network &rarr; Link

Packets (including IP and Transport headers) are packaged into Ethernet
Frames.

## Data decapsulation

When data crosses back up a layer, the packaging for the lower layer is
removed.
