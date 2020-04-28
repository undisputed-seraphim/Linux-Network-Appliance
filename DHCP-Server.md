# DHCP Server

I will be using `isc-dhcp-server`. It's easier to configure than `dnsmasq`, which I have never successfully gotten to work.

For a very basic DHCP server, the main stanza of interest is in the subnet declaration in `dhcpd.conf`:

```
subnet 192.168.1.0 netmask 255.255.255.0 {
        range 192.168.1.1 192.168.1.254;
        option routers 192.168.1.1;
        option domain-name-servers 1.1.1.1, 208.67.222.222;
        option netbios-name-servers 192.168.1.1;
        option subnet-mask 255.255.255.0;
        default-lease-time 86400;
        max-lease-time 604800;
        authoritative;
}
```

Here we want to hand out addresses in the `192.168.1.*` range, where the router sits at `192.168.1.1` for simplicity.

We will coerce DNS resolution to either Cloudflare's (`1.1.1.1`) or OpenDNS (`208.67.222.222`).

We want to be as friendly to Windows machines as we can, so the router shall specify itself to be a NetBIOS name server.

This DHCP server shall only hand out addresses to the client interfaces; namely, `enp2s0 ... enp6s0` and `wlp7s0`. However, those ports are already bridged together by `br0`. So effectively, you only want to hand out addresses to `br0`.

Edit the line in `/etc/default/isc-dhcp-server` as so:

```
INTERFACESv4="br0"
INTERFACESv6=""
```

Remember to restart the service after editing the files.



**TODO**: Figure out IPv6 one of these days