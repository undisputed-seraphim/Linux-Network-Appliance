# PPP Connection

Connecting to my ISP requires a PPP connection.

[Debian reference](https://wiki.debian.org/PPPoE)

1. Install `pppoeconf`
2. Run `pppoeconf`
3. Input the username and password supplied by my ISP as required.
4. Check that `/etc/network/interfaces` has a section that looks like:

```
auto dsl-provider
iface dsl-provider inet ppp
pre-up /bin/ip link set enp1s0 up # line maintained by pppoeconf
provider dsl-provider
```

where `enp1s0` is the Internet-facing port.