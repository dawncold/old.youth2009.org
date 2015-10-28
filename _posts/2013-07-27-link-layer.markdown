---
layout: post
title: "link-layer"
date: 2013-07-27 00:03
comments: true
categories: study tcpip
---

##link layer

###link layer's usage

1. send and receive IP datagram
2. ARP request and reply
3. RARP request and reply

many different link layers, depending on the type of networking: ethernet, token ring, FDDI, RS232 serial lines, etc.

IEEE 802.2/3 format and Ethernet format

in 802 format, after 2 bytes length field, there are 3 bytes LLC and 5 bytes SNAP and data field(38~1492) but in Ethernet format, there will be data field(46~1500), the end field is 4 bytes CRC.

frame formats use 48-bits destination and source address

##SLIP: Serial Line IP

END -- 0xc0

SLIP ESC -- 0xdb

IP datagram will be terminated by a special character called END(0xc0), most implementations transmit an END at the beginning of the datagram.

if a byte of IP datagram equals:

0xc0 --> 0xdb, 0xdc

0xdb-->0xdb, 0xdd

##PPP

1. async link with 8bits of data and no parity(no checksum)
2. bit-oriented sync links

start and end with a flag byte whose value is 0x7e, and if a byte value appears in information field, it should be escaped.

batter than SLIP:(pay for 3 bytes addition)

1. multiple protocols on a serial line
2. CRC
3. IP network control protocol negotiate IP address for each end
4. header compress like CSLIP
5. link control protocol negotiate many data-link options

##Loopback

127.0.0.1 or localhost is the loopback interface, an IP datagram sent to this must not appear on any network.

datagrams sent to broadcast and multicast addtess are copied to the loopback interface and sent out on the Ethernet.

anything sent to one of the host's own IP addresses is ent to the loopback interface!

##MTU

if the length of data field in IP datagram is larger than MTU(1500 or 1492 in Ethernet and 802 format), it will be fragmented.