+++
date = "2023-02-03"
title = "Re-routing a nasty VPN connection"
tags = ["VPN", "Networking", "Security"]
categories = ["Networking", "Security"]
+++

Using a [VPN][] is usually a good thing, as it allows a secure connection between you and some secret / sensitive _things_. Those might be single devices (machines, servers etc.) or directly expose you to a whole (sub)network.

So it's a quite natural solution to deploy a VPN setup when some of you workforce works from outside your sacred office (where you can physically control things). It might be that you employees are working some days from the home office or they might be sales persons who work, by design, "outside".

## The problem

I once got myself in a situation where I was forced to use a VPN to access some ressources, which is usually not a bad thing, but the VPN was configured in a way, that it routes _**all traffic**_ through this VPN connection.

No just the IP-Range required to access the protected ressource. All of it. No matter if private or work related traffic. Even my online-banking traffic was routed through the VPN.

Making things worse: The VPN was breaking up the SSL chain and doing [deep packet inspection][DPI] and dediced wether or not I was allowed to access various services.

## Idea of a solution

I'm per se not a hardcode network engineer but for our solution we only need to know a few basic things:

- Your computer has a routing table that defined how / where network is passed to
- This routing table can contain specific rules that, for example, say _"route all traffic to `10.0.0.0/8` through my VPN connection"_
- But it also contains a `default` route that is used as fallback
- DNS servers are used to resolve human readable names (like `michaelcontento.de`) to machine addressable IP addresses (like `10.23.24.1`)

With this knowledge in mind we can go and try to understand how the VPN will change our system. Once we know what the VPN client changes, we can find some counter measures 😎

## Analysing the mess

I came up with the following strategy to analyse "the mess" the VPN client was producing

1. Take a snapshot of the routing table **before** we estable a VPN connection
2. Take a snapshot of the routing table **after** we have a VPN connection established
3. Compare the two states and see what / who we can do about it

Luckily those three steps are pretty easy under macOS (the system I'm using) but same should be true for Linux and Windows.

1. Before snapshot: `netstat -rn > before`
2. After snapshot: `netstat -rn > after`
3. Comparing both `diff before after`

Pretty easy and this left me with a diff that looks like this:

```
5c5,6
< default            192.168.32.1       UGScg             en7
---
> default            10.231.225.26      UGScg           utun3
> default            192.168.32.1       UGScIg            en7
6a8,22
> 10.231.225.26/32   127.0.0.1          UGSc              lo0
> 13.107.6.152/31    192.168.32.1       UGSc              en7
> 13.107.18.10/31    192.168.32.1       UGSc              en7
> 13.107.64/18       192.168.32.1       UGSc              en7
> 13.107.128/22      192.168.32.1       UGSc              en7
> 13.107.136/22      192.168.32.1       UGSc              en7
> 23.103.160/20      192.168.32.1       UGSc              en7
> 40.96/13           192.168.32.1       UGSc              en7
> 40.104/15          192.168.32.1       UGSc              en7
> 40.108.128/17      192.168.32.1       UGSc              en7
> 52.96/14           192.168.32.1       UGSc              en7
> 52.104/14          192.168.32.1       UGSc              en7
> 52.112/14          192.168.32.1       UGSc              en7
> 52.120/14          192.168.32.1       UGSc              en7
> 104.146.128/17     192.168.32.1       UGSc              en7
8a25,29
> 131.253.33.215/32  192.168.32.1       UGSc              en7
> 132.245            192.168.32.1       UGSc              en7
> 150.171.32/22      192.168.32.1       UGSc              en7
> 150.171.40/22      192.168.32.1       UGSc              en7
> 154.14.194.89      192.168.32.1       UGHS              en7
10a32,33
> 172.27.2.112       10.231.225.26      UGHS            utun3
> 172.27.2.113       10.231.225.26      UGHS            utun3
```

Looks bad on the first glimpse, but basically it can be read as this:

- The old `default` route via `192.168.32.1` gets inactivated
- A new `default` route is created that routes everyting through `10.231.225.26`
- Some IP blocks are actively routed through the old default route (`192.168.32.1`)
    - I've checked some of the IP ranges and they all belong to Microsoft
    - So I suspect this is some whitelisted traffic for MS Teams and other things

## The solution

So to achieve our goal, we just need to somewhat "invert" the routing table. Right now we route **EVERYTHING** through the VPN (except for the whitelisted stuff) but we actually want to route **ONLY SELECTED** IP ranges.

So for my case the solutions was as simple as this:

1. Establish the VPN connection as usual
2. Remove the VPN based `default` route
    - `sudo route -n delete default 10.231.224.9`
3. Instanciate our local `default` route again
    - `sudo route -n add default 192.168.32.1`
4. Whitelist the traffic we want to route through the VPN
    - `sudo route -n add 172.27.16.88/32 10.231.224.9`
5. Enjoy your free, private and unwachted internet traffic

{{< giphy id="KtyTa7XH5ueJLYwmaG" >}}

  [DPI]: https://en.wikipedia.org/wiki/Deep_packet_inspection
  [VPN]: https://en.wikipedia.org/wiki/Virtual_private_network
