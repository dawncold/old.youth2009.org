---
layout: post
title: "internet protocol"
date: 2013-07-27 23:02
comments: true
categories: study tcpip
---

TCP, UDP, ICMP, IGMP need IP datagrams as data transmitting method.

IP is a unrealiable and connectionless delivery service.

* unrealiable: no guarantee that an IP datagram successfully get to its destination.
* connectionless: IP doesn't maintain any state of successive datagrams, it means there is no order in IP datagrams, latter sent IP datagram may arrived before former sent.

## Header

TOS: 3 bits precedence field(ignored today), 4 bits TOS(mini delay, max throughput, max relability, mini monetary cost), 1 bit always 0. TOS maynot supported by most TCP/IP implementations today, but some routing protocol such as OSPF and IS-IS are capable of making routing decisions based on this field.

Furthermore, a host isn't required to receive a datagram larger than 576 bytes. TCP and UDP will divide user data into small pieces, so one IP datagram will below that limit.

Some small IP datagram will be padded up to the mini length of frame, which maybe 46 or 38 bytes, so total length field is required when you want to know how long the IP datagram's length on earth.

TTL: set by sender, if this datagram pass a router, it will decrease 1, when it reaches 0, this datagram will thrown away, and sender will received an ICMP message. prevent routing loop.

Checksum: TCP, UDP, ICMP, IGMP use same algorithm to computing checksum. Since a router often cheages only TTL value, a router can incrementally update the checksum when it forwards a datagram, instead of calculating the checksum over the entire IP header again.

## IP routing

The fundamental difference is that a host never forward a datagram from one of its interface to another, while a router forwards datagram.

Router may reach a local optimum result, because every search route table, the router will get a closer next-hop router address, but it may not global optimum.

Frame's destination address(MAC address) may not the really destination address, it may the next-hop router's MAC address, because when it is routing, it can't be found in the current network, it must be routed to a next-hop router, so the destination address is the next-hop router's.

## Subnet addressing

Don't forget subtract 2, because all 0 bits and all 1 bits address for host address is invalid.

The advantage to using s single class B address with 30 subnets, compared to 30 class C addresses, is that subnetting reduces the size of the Internet's routing tables entry.

A special address: 127.x.x.x means loopback address, not only 127.0.0.1 can be loopback address!