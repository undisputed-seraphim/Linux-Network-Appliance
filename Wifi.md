# Wifi Access Point

We use `hostapd` as a wifi access point.

[Debian reference](https://wiki.debian.org/hostap)

[Manual for hostapd configuration](https://w1.fi/cgit/hostap/plain/hostapd/hostapd.conf)

- We want to be able to use state-of-the-art protocols due to ongoing vulnerability discoveries (WPA3, etc)
- Some wifi cards require driver workarounds or additional configuration before host AP mode can be achieved.
- Many 802.11ac cards can't advertise host AP on the 5 GHz range. Don't expect 802.11ac cards to be able to act as 802.11ac host APs.

The only file of interest here is `/etc/hostapd/hostapd.conf`, after installing `hostapd` from apt.

```
# System
bridge=br0
driver=nl80211
interface=wlp7s0

# Radio
ssid=My_SSID_Here
hw_mode=g
channel=acs_survey # If this doesn't work, fall back to '6'
country_code=JP
ap_max_inactivity=300

# 802.11
wmm_enabled=1
ieee80211n=1
ieee80211ac=1

# Authorization
auth_algs=1
wpa=2
wpa_key_mgmt=WPA-PSK-SHA256 SAE
wpa_pairwise=TKIP
rsn_pairwise=CCMP
wpa_passphrase=My_Preshared_Key_here
```

TODO: Increase security. Especially important when configuring the Raspberry Pi AP for use in airports.

- Set a rekey interval? `wpa_group_rekey`, `wpa_strict_rekey`, `wpa_gmk_rekey` (Defend against key reinstallation attacks?)
- Change default cipher? `wpa_pairwise=CCMP-256` and remove `rsn_pairwise` (causing it to default to `wpa_pairwise`)
- MACsec: `macsec_replay_protect`, etc

