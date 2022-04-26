---
title: "Networking"
date: 2020-09-24T14:31:33-04:00
draft: false
---

In this section, you will find resources on Networking and everything that it encompasses.  This guide will show you the basics, get you familiar with popular networking technologies, and also provide you with resources for further research.

#### What is Networking?

Networking is how computers communicate with each other whether that be inside the same local network or across the world via the internet. A basic understanding of networking will be critical to having success in a cybersecurity related field. This portion of the guide provides resources for learning about the OSI model, different protocols, and their associated ports. 


#### Networking Basics

Below are a few primer reads to this section, once you understand a few things come back here to really start to get into the meat of things.

+ [OSI Model](https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/)
+ [Protocols and Ports](https://docs.microsoft.com/en-us/learn/modules/network-fundamentals/)
+ [Common Protocols List](https://www.interserver.net/tips/kb/common-network-protocols-ports/)

Now that you know a bit about the abstractions around networking and some common ports and protocols, lets start to dive into what each of these things actually are.  We will only look at Layer 3 and lower for a bit, and then we will go higher into the layers.

A quick note that while we had you view the OSI Model, we will be using the TCP/IP model to discuss networking.  The TCP/IP model is essentially the same as the OSI model except that it utilizes five layers instead of seven.  The five layers are as follows

    1. Physical Layer
    2. Ethernet or Data Link Layer
    3. Internet Protocol Layer
    4. Transport Layer
    5. Application Layer

##### Addresses

The logical place to start talking about networking is addresses.  When talking about networking there are a variety of different addresses, Internet Protocol (IP) addresses are very common, but there are also Media Access Control (MAC) addresses to consider.  Each of these addresses correlates to a different layer of the OSI or IP models.  IP addresses are commonly known as Layer 3 addresses while MAC addresses are known as Layer 2 addresses.

A common IP address looks like this ```64.233.160.23``` and is composed of four parts, called octets, separated by periods.  Each octet is at its core a binary number of 8 bits to add up to a total of 32 bits per IP address.  What this means is that each octet can be a decimal number ranging from 0 to 255. Now, we should make a distinction here, that address is specifically an IP version 4 address.  IP version 6 addresses exist and look like this ```2001:4860:4000:2800:9304:32f3:239f``` and are composed of a total of 128 bits.  IPv6 is slowly replacing IPv4 because there are a larger number of possible v6 addresses versus v4, but due to its complexity, we will not cover it here.

There are a few special IP addresses to be aware of, namely ```127.0.0.1``` also known as the loopback address.  This is always the IP address of your machine, but it is only reachable from your computer itself.  Another important address is called the broadcast address and is any address which ends in ```255```.  This address is important for how Layer 3 and Layer 2 actually work together.

There are also different classes of IP addresses, specifically public and private addresses.  Private IP addresses are any of the following: ```10.X.X.X``` or ```192.168.X.X``` or ```172.16.X.X```.  These addresses are not reachable from the internet, at least not directly anyways.  Most other valid IPv4 addresses are considered public addresses.


[Check out this video on IP addresses to learn more](https://www.youtube.com/watch?v=LIzTo6e4FgY)


A MAC address looks like this ```FB:74:26:76:DD:4C``` and is composed of six pairs of hexadecimal numbers.  A MAC address is a total of 48 bits and is meant to be a unique identifier for every networking interface in the world.


[Check out this video on MAC addresses to learn more](https://www.youtube.com/watch?v=UrG7RTWIJak)


##### Communication

Now that we know what these addresses are, what do they actually do?  Network addresses allow us to actually send information from one computer to another.  When your computer attempts to communicate on the internet, a lot happens, but lets look at it from Layer 3 and lower.  Whenever you are using the internet, your computer communicates with another computer somewhere in the world.  Every publicly accessible computer in the world has what is known as a public IP address. Your computer probably does not have a public IP address because it is probably behind a firewall or some other form of device in some way.  When your computer attempts to contact another computer, which we will call a server from now on, it must know the server's public IP address.  Your computer then sends what is known as a packet to that server.  You can think of a packet as a letter or some other form of communication. This packet contains the server's address as well as your IP address so that the server knows how to reach you.  This packet is then sent via the internet to the server, but how does it get there?

##### Layer 2 Communication
If your computer has an address of ```192.168.1.2``` and the server has an address of ```192.168.1.3```, then its actually very simple, well kind of anyways.  All of this occurs at Layer 2 using MAC addresses.  Your computer would send out via the broadcast address (```192.168.1.255``` in this case) asking for the MAC address of whoever has the IP address of ```192.168.1.3```.  Every device connected on the network with an address that begins with ```192.168.1.``` (also known as the network prefix) will then receive this special packet sent via the Address Resolution Protocol, or ARP.  Once a device with that address, specifically the server in this case, receives the packet, they then send back to your computer its MAC address.  Your computer then stores this information along with its IP address in its ARP table.  Your computer then *encapsulates* the packet into a frame which is the Layer 2 equivalent of a packet and sends the information via Layer 2.  No matter how your computer communicates, it will always use this flow of events via Layer 2 to send information between IP addresses.  All of networking relies on the concept of abstraction, so we will assume you understand this process now.

With that, this brings us to the concept of switches.  Switches are Layer 2 devices which have multiple ethernet ports and simply connect devices via Layer 2.  You can think of a switch simply as knowing how to send frames from one ethernet port to another based on MAC addresses.  We recommend watching the video below for an in-depth look at switches and Layer 2 as a whole.


[Check out this video on Layer 2 switches to learn more](https://www.youtube.com/watch?v=9yYqNqTNnqI)


##### Layer 3 Communication

Before we begin with Layer 3 communications, we need to introduce the concept of a subnet mask.  A subnet mask is a number ranging from 0 to 32 which defines how much of an IP address is used for the network address and how much is used for the host address.  A typical subnet mask would be 24 which can also be represented as ```255.255.255.0```.  What this means is that the first three octets of an IP address will be used to determine the network and the last octet of the IP address will be used to determine the host.  Another typical subnet mask is 16 or ```255.255.0.0``` which means that the first half of the IP address would be used for the network and the other half for hosts.  

You may be asking, why would we want to do this?  The answer is that by doing this, we are able to introduce the concept of subnets.  A subnet is simply a network address, such as ```192.168.1.0/24```.  With this network, we would be able to have a total of 254 different host IP addresses (keep in mind that you never have an octet ending in 0 or 255 as these are reserved).  The internet is broken into an insane amount of different subnets.  

With the concept of subnets and subnet masks in mind, understand that Layer 2 switching using ARP as we previously discussed only works on the same subnet.  This is because each subnet has its own unique broadcast address.  So how do you communicate between different subnets?

This brings us to routing and the concept of routers.  A router is a Layer 3 networking device that is able to send packets from one subnet to another.  Since a router is Layer 3, it understands IP addresses, and much more than that, its native language is IP addresses.  Now, a router also understands Layer 2 addresses as well, which presents that when a device operates at a certain network layer, it understands all of the layers below that layer as well.  Beyond this, routers have to use ARP and Layer 2 to actually communicate, but they use their knowledge of Layer 3 addressing to enhance this capability.

So what does a router actually do and how does it work?  Typically, a router has at least two network interfaces, typically ethernet ports (although they can be other technologies such as fiber optic as well).  For each network interface, the router has a different subnet so for the sake of example lets say one interface has the subnet ```192.168.1.0/24``` and the other has ```192.168.2.0/24```.  Now, say we have two hosts, each on one of these subnets.  These two hosts want to talk to each other, and luckily, our router will allow them to do so.  Each router interface has an IP address actually designated for that interface which corresponds to the subnet, so lets say ```192.168.1.1``` and ```192.168.2.1```.  Now, each host has to be configured to know its *default route* which actually tells it who to send its packets to when it needs to send packets outside of its subnet.  You can think of a subnet as a zipcode and a router as the post office.  Whenever you need to send a letter to another zipcode, it first goes to your post office, and then they decide where it needs to go from there to reach that zipcode.  Its essentially the same process with subnets and routers.  The host lets say ```192.168.1.2``` sends its message addressed to ```192.168.2.2``` (our other computer) to the router at ```192.168.1.1``` which is that computer's default route.  The router then receives this packet and looks at the destination subnet.  It does not need to actually look at the host address, the ```.2``` in this case, because it is not concerned with specific addresses, just networks.  It then determines that it knows that subnet, because its second interface is on that subnet.  So then it sends it to that interface, and from there Layer 2 takes over to send the packet to the right destination.

Now lets extend this concept.  Let's say that you wanted to send your packet to Google at the address ```8.8.8.8```.  Now the router receives this packet, and looks at it, but the router does not have an interface on the ```8.8.8.0``` subnet, the router does not really have any way of knowing where that subnet really is.  So how does the packet get there?  It uses the same concept as we used before, routers themselves have default routes.  The router sends this packet to its configured default route, say a router at ```192.168.2.254```.  This router then continues the process till the packet reaches its destination.  In this way, routers are strung together to form a chain, or network, or even a web.


[Check out this video on routers and Layer 3 to learn more](https://www.youtube.com/watch?v=LExExB6Xjks)


##### DHCP

Dynamic Host Configuration Protocol, or DHCP is a way to assign IP addresses *dynamically* to hosts on a network.  This is great for users because rather than having to manually configure your IP address, subnet mask, and default route; your DHCP server can automatically assign you all of this.  To do this, your computer sends a special message via the broadcast address which the DHCP server responds to with the necessary information.  Now, a router can usually provide DHCP, but a DHCP server does not need to be a router.  In fact, any computer can act as a DHCP server.  The DHCP server has a DHCP pool which tells it which addresses it can assign.  The DHCP server then provides devices with DHCP leases which is the ability to use the IP address for a set amount of time.  When that time expires, the device then contacts the DHCP server for a different address.


[Check out this video on DHCP to learn more](https://www.youtube.com/watch?v=S43CFcpOZSI)


##### The Transport Layer

You might be getting to this point and thinking, okay but when are we going to talk about websites and how I can access google.com and stuff like that.  Never fear, because we have transcended to Layer 4 known as the Transport Layer (Layer 2 and 3 are commonly referred to as such but Layers 4 and 5 are not).  The Transport Layer knows about IP addresses and MAC addresses, but it doesn't need to necessarily worry about how they work; it just relies on the fact that they do.  There are two key technologies to discuss when it comes to the Transport Layer: Transmission Control Protocol (TCP) and User Datagram Protocol (UDP).  

##### Ports

Now that we are at the Transport Layer, it is also important to know that the Transport Layer cares about this concept of a port.  Now a port is not a physical port, rather it is a software concept.  TCP and UDP both have different sets of ports which range from 0-65535.  Each port corresponds to an application, and the ports from 0-1023 are called *well-known ports* because there is a standardized list of services which correspond to these ports.  But we are getting ahead of ourselves to the Application Layer.  Lets focus on the Transport Layer for now.

##### User Datagram Protocol

UDP is a simple protocol.  It prioritizes speed over anything else.  UDP has messages, called datagrams which it sends between IP addresses and ports.  UDP takes a datagram and sends it to an IP address.  That is actually it.  UDP does not care if the datagram ever reaches its destination or that it did.  UDP just sends the datagram to it and continues on with whatever it needs to do.  We say that UDP does not do any error checking or correction.  You most usually see UDP used for realtime applications such as video streaming since it does not necessarily matter if you receive every single piece of information as long as you receive most of it, but its also important that you receive it quickly.

##### Transmission Control Protocol

TCP on the other hand cares about your data.  It prioritizes data integrity, ensuring that every packet reaches its destination intact.  TCP requires that two different computers form what is known as a TCP handshake which keeps a connection open between the computers for the entirety of a conversation.  When using TCP, a computer first ensures that the other computer is ready to communicate, and the second computer responds saying it is (hence the handshake).  The first computer then begins to send information.  After each packet, the second computer responds saying that the information is received.  If the second computer does not respond in a certain amount of time, the first computer then sends the information again and again until it receives a response.  When the conversation ends, the computers then close the TCP connection.


[Check out this video on the Transport Layer to learn more](https://www.youtube.com/watch?v=cA9ZJdqzOoU)


##### Application Layer

Now we have finally arrived at the fabled Application Layer.  The Application Layer is home sweet home. This is where all of our friendly protocols such as HTTPS (Hyper Text Transmission Protocol Secure) live.  The Application Layer takes full advantage of all the abstractions provided by the other four layers to simplify communication between applications on different devices.  

##### Sockets

To understand the Application Layer, we now have to understand the concept of a socket.  If you have done any web programming before, you might actually be familiar with a socket.  For instance, here is a TCP socket in Python:

    # Create the main socket object
    main_sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    # Bind to localhost and port 8080
    main_sock.bind(("127.0.0.1", 8080)) 

Sockets are pretty cool as they are the actual way the Application Layer communicates.  A typical socket utilizes three things: the socket type, the IP address, and the port.  In the above example, the socket type is a *stream socket* (which indicates TCP, UDP would be datagram socket), the IP is 127.0.0.1 (localhost), and the port is 8080.  A socket abstracts everything for an application so that it can focus on communication.

And that is pretty much how the Application Layer actually works, the Transport Layer takes care of most of the heavy lifting for networking for the Application Layer.  But that is not the end of the Application Layer, where the Application Layer truly shines is in the application protocols it supports, we will now examine a few protocols that might shed some more light on how the internet works.

##### Domain Name System

Domain Name System, or DNS is a way to use Domain Names such as ```google.com``` or ```liberty.edu``` to communicate on the internet without actually knowing the IP address of the server.  DNS works by having a server which maintains a list of DNS entries, called records for different domains, called zones.  Your computer then contacts this DNS server on UDP port 53 with the domain name, and the DNS server responds with the corresponding DNS record which contains the actual IP address of the server.  Your computer then continues using that IP address.  You may be asking how your computer knows which DNS server to contact, and the answer is you can either manually configure it to a server such as ```8.8.8.8``` (Google DNS) or ```1.1.1.1``` (Cloudflare DNS), or your DHCP server can provide you with a DNS server.  This is useful if you are on an internal network with special internal DNS records.  DNS is a very critical service to ensure the internet functions because without it, no one would know what servers to contact for what.


[Check out this video on DNS to learn more](https://www.youtube.com/watch?v=Rck3BALhI5c)


##### Hyper Text Transfer Protocol

The Hyper Text Transfer Protocol, or HTTP as it is commonly known is by far one of the most used and familiar protocols on the internet.  HTTP uses TCP port 80 by default (or 443 when using SSL/TLS which is described below).  HTTP does exactly what its name implies, it transfers Hyper Text Markup Language, or HTML files, from one computer to another.  When you visit an HTTP (or web) server, you use a HTML browser such as Google Chrome or Mozilla Firefox which interprets HTML to display the requested web page.  There is a lot more to HTTP so please see the video below to learn more.


[Check out this video on HTTP to learn more](https://www.youtube.com/watch?v=iYM2zFP3Zn0)


With that, we bring this section of the guide to a close.  You now know the fundamentals of networking.  If this seems interesting to you or you want to master networking, continue reading to learn about some more advanced topics.

#### Advanced Networking Topics

If you were intrigued by the last section, we hope you will continue to be intrigued in this section where we will cover such interesting topics as encryption, NAT, and firewalls.  These three technologies are crucial to understanding the internet as we know it today.  Some of the components that help these technologies to work are beyond the scope of this guide, so we encourage you to do a lot more research if one of these topics pique your interest. 

##### SSL/TLS

Secure Socket Layer and Transport Layer Security is a set of Application Layer protocols which add much needed encryption to TCP. While these two protocols are used almost synonymously, it is important to note that SSL is technically deprecated, and TLS is almost always used now.  Whenever you visit a website using HTTPS, you are using SSL/TLS which encrypts the traffic between your web browser and the web server.  This prevents attackers from conducting what is known as a Man-in-the-Middle (MITM) attack on your connection.  You should never enter passwords or sensitive information on a normal HTTP connection.  Most web servers use HTTPS now, and most web browsers prevent you from visiting insecure HTTP websites by default.

Now lets begin to understand what TLS actually does to provide you encryption.  We must first understand the concept of a certificate.  A certificate is technically just a form of an encryption key.  A web server which uses TLS will present to a client its certificate to prove its identity.  The way that it proves it is by demonstrating that the certificate is signed by what is known as a Certificate Authority.  A Certificate Authority is a verified third-party which provides its root certificates to web browser developers who embed it within web browsers.  You can also manually install your own certificates in most operating systems or web browsers as well.  

Once the client has verified the server is who it says it is, the client and server then perform some form of key exchange.  This ensures that the client and server can encrypt and decrypt traffic as needed, but only they can do this.  A popular protocol to do this is Diffie-Hellman key exchange.  Regardless, once this is done, the client and server then proceed with their conversation, being careful to encrypt all traffic between them.


[Check out this video on TLS to learn more](https://www.youtube.com/watch?v=0TLDTodL7Lc)


##### Network Address Translation

Network Address Translation, or NAT as it is commonly called, is an important Layer 3 system that you probably use everyday without even knowing it.  NAT is a method by which you can use a private IP address such as ```192.168.10.1``` but to servers on the internet you have a public IP address such as ```66.249.64.30``` and everything appears to work just the same to you.  There are actually a few different types of NAT which we will cover here.

##### Port Address Translation

Port Address Translation, or PAT is probably the form of NAT which you commonly use.  This type of NAT allows your public facing router to open a connection to a server pretending to be you.  When the server responds to the router, the router then forwards the packets to you.  The router is able to do this for any private IP address in its network, thus allowing multiple devices to appear to have the same public IP address.  It is able to do this by assigning each connection to a different port.  Thus, each port corresponds to a different private IP address.  Another important aspect of PAT is that you can configure port forwarding, i.e. one port is dedicated to forward to a port on one private IP address.  If you have ever done this for a game server before, PAT is what allows this to work.

##### One to One and Dynamic NAT

One to One NAT describes itself well.  It dedicates one public facing IP address to one private IP address.  All requests are then routed between the addresses by the router.  Dynamic NAT is similar, but instead pulls from a pool of public addresses and chooses one for each private address dynamically.


[Check out this video on NAT to learn more](https://www.youtube.com/watch?v=qij5qpHcbBk)


##### Firewalls

Firewalls are probably what you first think of when you think about network security.  What is a firewall though?  A physical firewall is a device which sits between two networks and filters traffic through it.  It does this typically at Layer 3 by inspecting IP addresses and ports.  Firewalls are able to typically do three different actions on each packet they receive: Pass, Block, or Drop.  When a firewall Passes or Allows a packet, it simply lets the traffic continue on its way.  It may still log traffic which it allows as well, which is one of the most powerful features of a good firewall.  Firewalls can also be software applications which run on your computer or server.  Both software and hardware firewalls essentially do the same thing, but hardware firewalls are typically more powerful and allow for much greater granularity in how it can be configured.


[Check out this video on firewalls to learn more](https://www.youtube.com/watch?v=9JQtyQEpQV8)



##### Stateful vs Stateless

There are two different kinds of firewalls whether it be hardware or software.  A firewall can be stateful or stateless.  What this means has to do with TCP connection states.  A stateless firewall does not care about TCP states and only allows or blocks traffic which is specifically declared in the firewall rules.  A stateful firewall remembers TCP states and can allow traffic based on these states.  A typical way this might work is that you allow SSH traffic in through your firewall on port 22.  You deny all outbound traffic except for related connections.  Then when an SSH connection is established, since the TCP state is created, it allows outbound traffic related to that TCP connection.  This is a powerful feature for a firewall to have and allows you to be stricter with your firewall rules by ensuring that only needed traffic is allowed.


[Check out this video on stateful firewalls to learn more](https://www.youtube.com/watch?v=gMvXruavqDI)


Now that you have a general concept of routers and firewalls, we will now go over a few of the most popular firewalls and routers which are commonly used.  It is also important to note that most firewalls actually will act as routers, so you will often find just firewalls deployed without any router.

#### PFSense and OPNSense 

[PFSense](https://www.pfsense.org/) is an open source firewall application built on top of FreeBSD.  The company Netgate develops it and sells pre-built hardware firewalls which run the operating system.  PFSense is popular because you can easily install it in a virtual machine for testing purposes or on any x86 based computer.  You can manage PFSense via the command line which actually runs bash and is just a normal FreeBSD shell.  You primarily manage PFSense via its web interface.  The web interface allows you to configure interfaces, firewall rules, and everything else.


[Check out this video on PFSense to learn more](https://www.youtube.com/watch?v=fsdm5uc_LsU)


[OPNSense](https://opnsense.org/) is a fork of PFSense and is very similar to it.  OPNSense is now based on HardenedBSD instead of FreeBSD, but it is not backed by any company.  Rather, OPNSense is similar to most Linux distributions in that it is completely community maintained.  The web interface for OPNSense is organized slightly differently from PFSense, but it still has the main features of PFSense.  Where OPNSense really shines is in its extra packages which PFSense does not have.  For instance, the popular VPN protocol Wireguard has had an OPNSense package for a long time, but PFSense is dependent on FreeBSD to develop a stable Wireguard kernel implementation.  Due to its additional features, OPNSense can be slightly more difficult to configure than PFSense, however.


[Check out this video on OPNSense to learn more](https://www.youtube.com/watch?v=dv13d6rfQPI)


#### Palo Alto 

Palo Alto is a proprietary firewall appliance series developed by Palo Alto Networks.  Palo Alto firewalls are available as physical devices but also as virtual machine appliances for VMWare ESXI.  The Palo Alto firewalls are actually based on CentOS Linux 7, but the administrative CLI is a custom shell developed by Palo Alto to perform specifically firewall related tasks.  It is very difficult to gain access to the underlying Linux OS of the firewall by design.  The main forms of administrative access for the Palo Alto are via the CLI, the web interface, and the XML/REST APIs.  The main features of Palo Alto firewalls is the advanced threat detection and filtering features.  The firewalls are able to examine files for malware and filter URL access for users.  The firewall can also be integrated into a Windows Active Directory environment and filter based upon different users in the AD domain.  Palo Alto firewalls have many more features than PFSense or OPNSense, but they are proprietary and difficult to obtain licensing for to actually try out the firewall.


[Check out this playlist on Palo Alto Firewalls to learn more](https://www.youtube.com/watch?v=YaaRNHbvyjw&list=PLqATPiC_Bcl8rtMY14kyOuRg4_E0DdnQy&index=7)


#### Cisco

Cisco Systems is a company which specializes in the development of networking equipment.  Chances are you have heard of Cisco and might have even used a Cisco device.  Cisco IOS is a typical operating system for Cisco switches, wireless access points, and routers.  Most Cisco devices can be managed via the CLI but most also provide some form of web interface.  

Cisco has developed an application known as Packet Tracer which allows anyone to practice networking and also practice utilizing Cisco networking equipment.  To download Packet Tracer visit [this link](https://www.netacad.com/courses/packet-tracer) and create a free Cisco Academy account.  Packet Tracer will allow you to practice the Cisco IOS CLI, but also test out different network topologies and protocols.


[Check out this series on Packet Tracer to learn more](https://www.youtube.com/watch?v=frUQMHXhnvs)


#### Wireshark

Wireshark is a popular tool for monitoring network traffic.  Wireshark allows you to see all of the traffic occurring on a network that you are connected on.  It is a powerful tool for debugging networking as well as intercepting traffic. [This resource](https://www.howtogeek.com/104278/how-to-use-wireshark-to-capture-filter-and-inspect-packets/) will help to get you started with Wireshark.


[Check out this video on Wireshark to learn more](https://www.youtube.com/watch?v=lb1Dw0elw0Q)


