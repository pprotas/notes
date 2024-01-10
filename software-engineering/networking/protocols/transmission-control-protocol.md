---
id: transmission-control-protocol
aliases:
  - Transmission Control Protocol (TCP)
tags: []
---

# Transmission Control Protocol (TCP)

TCP is a protocol that ensures reliable transmission of data over the internet. When packets arrive at the destination, TCP is used to send acknowledgements back to the sender that the packets were received correctly. Any missing packets will be re-sent by the server, to ensure that the receiver has all the packets.

The packets don't have to be received in order, in fact the order of the packets coming in can never be guaranteed due to the architecture of the internet. TCP will re-order the packets to make sure that the resulting data is assembled the correct way.

## Transmission Control Protocol/Internet Protocol (TCP/IP)

TCP/IP is the underlying communication protocol used by most internet-based applications and services. It provides a reliable, ordered, and error-checked delivery of data between applications running on different devices.

### Three-Way Handshake

TCP uses a three-way handshake to set up a TCP/IP connection over an IP based network. This handshake is also called the TCP-handshake or the SYN-SYN-ACK handshake.

The three messages that are sent by TCP to negotiate and start a TCP/IP session are named SYN, SYN-ACK, and ACK. This stands for Synchronize, Synchronize-Acknowledge, and Acknowledge.

The host, generally the browser, sends a SYNchronize packet to the server. Once received, the server responds with a SYNchronize-ACKnowledgement packet. Once received by the host, an ACKnowledge is sent back to the server. The server receives this packet and now the TCP session is started.

### Port

Ports are used to identify an application or service running on a device. Ports are represented by numbers, such as 80. Multiple applications should all use different ports, otherwise there might be a conflict and the packets might not be router correctly.

### Socket

A socket is a combination of an IP address and a port number, representing a specific endpoint for communication. Sockets are used to specify which application on which device should receive the packets.

### Connection

A connection is established between two sockets when two devices want to communicate with each other.

### Data Transfer

Once a connection is established, data can be transferred between the applications running on each device.
