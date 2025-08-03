---
date: '2025-08-03'
title: Some Infra Notes
subtitle: AlgoExpert infrastructure course
slug: algoexpert-infra
tags: 
  - Notes
---

## Networking

### Protocol

A protocol is a set of rules for formatting and processing data. It defines how data is transmitted over a network.

### Network

A network is a collection of devices that can communicate with each other. It can be as simple as two computers connected by a cable or as complex as the internet. Think of it as an undirected graph where nodes are devices and edges are connections.

### Data Link Layer

This layer is the protocol that transfers data between nodes on a network across the physical layer. It is responsible for node-to-node data transfer and error detection and correction.

### Socket

A socket is a pipe - a memory buffer on the file system through which one process can write data to another - except that rather than connecting two processes on the same machine, it connects a process on one machine to a process on another machine over a network.

Like a pipe, there's a system by which the writing process can write data into the pipe, and signal tha data is ready to be read, and the reading process can be signaled that data is ready to be read, and it can read the data from the pipe. Pipes are single-directional, but a process can attach to multiple pipes, so bi-directional data flow can occur simply by attaching to two pipes, one for each direction.

Sockets are endpoints that are usually exposed in the kernel, and different network protocolos can be used to transfer data through the socket. The most common protocol is TCP, which is a connection-oriented protocol that ensures reliable data transfer.

### TCP

A network protocol built on top of the IP protocol, allowing for ordered, reliable data delivery between machines over the public internet by creating a connection between two sockets. TCP is usually implemented in the kernel, which exposes sockets to applications that can use them to stream data though an open connection.

When we talk about connections, we mean that a socket on one machine is connected to a socket on another machine, and data can be sent back and forth between them. 

### Port

In order for multiple programs to listen for new network connections on the same machine without coliding with each other, each program listens on a different port. A port is an integer between 0 and 65535 (2^16 - 1) that identifies a specific process on a machine.

Typically, ports below 1024 are reserved for system processes, while ports above 1024 are available for user processes. Some examples of well-known ports are:
- 22: SSH
- 53: DNS
- 80: HTTP
- 443: HTTPS

### IP

Internet Protocol (IP) is a protocol that outlines how almost all machine-to-machine communications should occur in the world. Other protocols, such as TCP, UDP, and HTTP, are built on top of IP. IP is responsible for routing packets of data from one machine to another over the internet.

### Client

A machine or process that requests data or services from a server.

Note that a single machine or piece of software can be both a client and a server at the same time. For example, a web browser is a client when it requests a web page from a server, but it can also act as a server when it serves local files to other processes.

### Server

A machine or process thar provides data or services for a client, usually by listening for requests on a specific port and responding to them.

### HTTP

The Hypertext Transfer Protocol (HTTP) is a protocol that defines how clients and servers communicate over the internet. It is built on top of TCP and is used to transfer data between web browsers and web servers.

Request typically have the following schema:

```
host: string (example.com)
port: integer (80 or 443)
method: string (GET, POST, PUT, DELETE, etc.)
headers: pair list (example: { "Content-Type": "application/json" })
body: opaque sequence of bytes (example: { "name": "John Doe" })
```
Responses typically have the following schema:

```
status: integer (200, 404, 500, etc.)
headers: pair list (example: { "Content-Type": "application/json" } or { "Content-Length": "1234" })
body: opaque sequence of bytes (example: { "message": "Hello, world!" })
```

example request:

```
host: example.com
port: 80
method: GET
headers: { "Content-Type": "application/json" }
body: ""
```
example response:

```
status: 200
headers: { "Content-Type": "application/json", "Content-Length": "1234" }
body: { "message": "Hello, world!" }
```

### HTTPS

The Hypertext Transfer Protocol Secure (HTTPS) is an extension of HTTP that adds a layer of security by encrypting the data sent between the client and server using Transport Layer Security (TLS). It requires servers to have trusted certificates (usually SSL certificates) and uses the Transport Layer Security (TLS) protocol, a security protocol built on top of TCP, to encrypt the data sent between the client and server.

### DNS

The Domain Name System (DNS) is a system that translates human-readable domain names (like example.com) into IP addresses (like 192.0.2.1). This allows users to access websites using easy-to-remember names instead of having to remember numerical IP addresses.

### IP Address

An address given to each machine connected to the public internet. IPv4 addresses consist of four integers between 0 and 255, separated by dots (e.g., 192.0.2.1). Special values include:
- 127.0.0.1: Your own local machine. Also known as localhost.
- 192.168.*.*: Your private network. For example, your machine and all machines on your home network will have IP addresses in this range.

> A summary of the protocols, IP, TCP, HTTP, HTTPS <br><br>
> TCP builds on IP to provide reliable, ordered data transfer.
> HTTP builds on TCP to provide a way for clients and servers to communicate over the web.
> HTTPS builds on HTTP to add TLS, which builds on TCP, to provide a secure communication channel.
> DNS acts as resolver to translate human-readable domain names into IP addresses.