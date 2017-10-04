---
layout:     post
title:      HTTP Basics
author:     Nia
tags: 		  CS50
subtitle:  	Daily Review
category:   daily
---

Continued with [CS50](https://niamurrell.github.io/search/#CS50) today and final a topic that's review woo! Just to track my notes from the lecture...

### HTTP Basics

**DHCP** software (dynamic host configuration protocol) runs on a router an assigns an IP address to each device on that accesses that router.

**IPV4** is the original type of IP address which takes the format `0.73.145.255` where each number is between 0-255, i.e. 8 bits each, i.e 32 bits total (max 4 billion device IP addresses).

**IPV6** has 8 places of 16 bit hexadecimal characters and allows for a bajillion more IP address (to paint a picture...).

A **DNS** (domain name system) converts IP addresses to domain names.

**TCP** (transmission control protocol) is coupled with **IP** (internet protocol); IP gives an address of where a packet of information should go; TCP breaks data into packets, and tracks and guarantees delivery. If a packet doesn't make it through, TCP will request the missing packet.

**UDP** (user datagram protocol) is similar to TCP but used (for example) for streaming live events; after buffering TCP would wait for all the data before displaying, and you would progressively get behind 'live' whereas UDP will just skip whatever was buffering to ensure you always go with the latest packets (and stat live).

**Port** numbers are included with TCP packets to determine how they should be handled:
* 21 - FTP
* 22 - SSH (encrypted shell)
* 25 - SMTP (email)
* 53 - DNS
* 80 - HTTP
* 443 - HTTPS

**Firewalls** block IP addresses that are determined by the network admin. You can also block entire ports (no FTP allowed, for example).

**HTTP**: hyper text transfer protocol. It includes a **get** request as the first line. The server will return a status code:
* 200 - OK
* 301 - moved permanently
* 302 - found
* 304 - not modified
* 401 - unauthorized
* 403 - forbidden
* 404 - not found
* 500 - internal sever error

**HTML entities** are special codes which represent text symbols. Example: `&#169` = &#169


### Other Stuff

We also learned some terminal commands I didn't know about:
* `nslookup www.google.com` will return the IP address of the domain name
* `traceroute -q 1 www.google.com` will return the pathway *1 **q**uery* at a time until it gets to the destination...you can see how your request to a serve thousands of miles away is routed across the globe, step by step

### Up Next

Watch next two CS50 lectures this weekend so that I have only the assignments to think about over the next couple of weeks. Continue work on [value app](https://niamurrell.github.io/search/#ValueApp).