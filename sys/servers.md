# 12/11 Aim: Creating a handshake agreement

Do Now: Consider a program that uses pipes in order to communicate
between 2 separate executable files.

One file is a "server" that is always running. The other is a "client".

Design a process by which both files can connect to each other and
verify that each can send and receive data. Try to keep it as simple
as possible.

## Handshake

A procedure to ensure that a connection has been established between 2
programs.

Both ends of the connection must verify that they can send and receive data
to and from each other.

### 3 way handshake

1. Client sends a message to the server.
2. Server sends a response to the client.
3. Client sends a response back to the server.

### Basic server/client design pattern

1. Setup:
    1. Server creates a FIFO (Well Known Pipe) and waits for a connection
    2. Client creates a "private" FIFO.
2. Handshake:
    1. Client connects to server and sends the private FIFO name. Client
       waits for a response.
    2. Server receives client's message and removes the WKP.
    3. Server connects to client FIFO, sending an initial acknowledgement
       message.
    4. Client receives server's message, removes its private FIFO.
    5. Client sends response to server.
3. Operation: Server and client send information back and forth.
4. Reset:
    1. Client exists, server closes any connections to the client.
    2. Server recreats the WKP & waits for another client.

# 12/15 Aim: Always tip your servers


