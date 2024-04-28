# Multicast Snooping

Linux bridge interfaces, by default, have multicast snooping enabled by default.  This turns out to be problematic when it comes to receiving external IPv6 Neighbor Discovery (ND) packets and forwarding them as a general network switch should do, consequently disrupting IPv6 communications between two network hosts through the switch.

Disabling Multicast Snopping on the bridge interface allows for the IPv6 Network Discovery to flood out all network connections to bridge interface, (in my case to dual-stacked IPv4/IPv6 KVM guests attached to the bridge).



Here is how to see the current Multicast Snooping settings:

```
nmcli connection show <bridge0> | grep multicast-snooping
```
root@ubuntu:~# nmcli connection show bridge-0 | grep multicast-snooping
bridge.multicast-snooping:              yes



To disable multicast-snooping:

```
nmcli connection modify archie0 multicast-snooping no
```
