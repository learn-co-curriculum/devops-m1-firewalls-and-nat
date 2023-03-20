# Firewalls and NAT

## Learning goals

- Understand the role NAT and firewalls play in securing network traffic
- Learn what the types of NAT and firewalls are and how they differ
- Learn the basics of `ufw` in Linux

## Introduction

When it comes to server management (and computing as a whole), securing and managing network traffic is crucial, especially in certain applications. In this lesson we will be covering *firewalls* and *NAT* and how they work in practice.

## Firewalls

A **firewall** is simply a security system that both monitors and controls incoming and outgoing network traffic based on predefined rules. 

![Firewall illustration](https://curriculum-content.s3.amazonaws.com/6685/devops-m1-firewalls-and-nat/firewalls.png)

A firewall acts as a *barrier* between an internal network and the rest of the internet. Firewalls can fall under several different types, the most common of which being a *packet-filtering* and/or *stateful* firewall.

A **packet-filtering** firewall is the simplest type; it examines each packet that enters or leaves a network, and then blocks it based on whatever rules are set. These rules may filter IP addresses, port numbers, certain protocols, etc.

A **stateful** firewall is a bit more advanced; it keeps track of the actual state of the connections, constantly monitoring the traffic and only allowing legitimate traffic through.

## Managing firewalls in Linux

Many *Linux* distributions like *Ubuntu* ship with some form of firewall out of the box. In most cases, this firewall is known as `ufw` (Uncomplicated FireWall).

As the name implies, it is a packet-filtering firewall, which is very easy and uncomplicated to use! In order to enable it, run the following command:

```bash
$ sudo ufw enable
```

Once it is enabled, you can add rules to allow/deny incoming/outgoing traffic based on the same rules we discussed earlier, for example:

```bash
$ sudo ufw allow 80/tcp
$ sudo ufw allow out to <IP Address>
```

Keep in mind when enabling `ufw` that it will deny all *incoming* traffic while allowing all *outgoing* traffic. From the point of enabling it, you have to manually allow the ports, protocols, or IPs you trust.

For the time being, let's keep it off:

```bash
$ sudo ufw disable
```

## NAT

**NAT** (Network Address Translation) is a technique that allows us to use *private/local* IP addresses internally on our network, and then when they want to communicate with the internet, *translates* them to public IP addresses. Not only does this provide an additional layer of security, but it can also help to conserve the number of public IPv4 addresses.

There are *three* types of NAT:

- **Static:** Simplest form of NAT; simply performs a *one-to-one* mapping of private IP addresses to public IP addresses
- **Dynamic:** Performs a *many-to-many* mapping of private IP addresses to a smaller pool of public IP addresses; typically used when a network has a large number of devices connected to it but only a limited amount of public addresses to distribute
- **Port Address Translation (PAT)**: Performs a *many-to-one* mapping, allowing multiple devices on a private network to share a single public address; works by translating the private IP address *and* port number to a unique port number on the public IP address

In most cases, you won't be managing the NAT of your network directly and it's up to your service provider or cloud server host. That being said, it's useful to know how it works in case you need to work around certain limitations or you *do* have control over it.

## Conclusion

Learning how to secure and manage network traffic is crucial, as it is often less secure than it may seem at first glance. As simple as they are, having a firewall can easily make the difference between being at risk of an attack and being properly secured, especially when you're running a server that only needs a couple of ports to fulfill its purpose.
