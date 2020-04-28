Updated April 2020

# Linux-Network-Appliance

This repository describes the steps needed to configure a nearly-full-featured router with Debian. (I say nearly because all administration must be done through the command-line, there will be no GUI)

## Hardware Setup

I purchased this [mini PC from China.](http://inctel.com.cn/product/detail/408.html)

- Intel 3865U CPU (dual core Kaby Lake based, 1.8 GHz)
- 6 Intel gigabit ethernet ports
- 2 DDR4 SODIMM slots supporting up to 32GB
- Half-length mini PCIE, full length mSATA
- Pre-cut holes for wifi antennas

## Operating System

I narrowed down my choices to between OpenWRT or Debian.

I went with Debian because it was easier to install, had more packages and community support, and overall more flexible. However, I intend to try out OpenWRT again some day.

## Organization of Documents

The markdown files scattered in this repository do not have a numbering, so that I can insert or remove documents as I please without having to update the numberings of every file. Instead the order shall be kept in this section on this file.

1. The PPP connection to my ISP (`wvdial`)
2. The bridge (`bridgeutils`)
3. The DHCP server (`isc-dhcp-server`)
4. The wifi access point (`hostapd`)
5. DNS server over HTTPS (UNDER RESEARCH - I would like to use `bind9`)
6. Pihole (UNDER RESEARCH - How can I fit Pihole into the DNS server?)
7. OpenVPN (On hold indefinitely - I can't seem to find a tutorial that works)
8. Samba server
9. Miscellaneous

To allow these files to be individually useful to a more general audience, I will try to make each guide independent of post or prior steps; however, some dependency is unavoidable.