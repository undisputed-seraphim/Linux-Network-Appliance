# Bridge

We want to bridge connections on all other network interfaces to the Internet-facing interface.

[Debian reference](https://wiki.debian.org/BridgeNetworkConnections)

In my case, the Internet-facing interface is `enp1s0`, and all other physical interfaces are named from `enp2s0` to `enp6s0`.

The wireless AP will use the interface at `wlp7s0`.

1. Install `bridge-utils`.
2. `brctl addbr br0`
3. `brctl addif br0 enp2s0 enp3s0 enp4s0 enp5s0 enp6s0 wlp7s0`
4. Bring up all the interfaces.

Create a new file named `br0` at `/etc/network/interfaces.d/`, and fill it like so:

```
auto br0
iface br0 inet static
        address 192.168.1.1
        netmask 255.255.255.0
        bridge_ports enp2s0 enp3s0 enp4s0 enp5s0 enp6s0 wlp7s0
        bridge_fd 0			# no forwarding delay
        bridge_stp off		# disable Spanning Tree Protocol
        bridge_waitport 0	# no delay before a port becomes available
```

