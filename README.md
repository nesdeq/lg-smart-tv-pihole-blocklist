# LG Smart TV (webOS) Pi-hole Blocklist

Blocks ads, tracking, telemetry and home-screen recommendations on LG webOS smart TVs. One consolidated hosts-format adlist for Pi-hole, AdGuard Home or any DNS blocker.

**Paste this URL into Pi-hole under Adlists:**

```
https://raw.githubusercontent.com/nesdeq/lg-smart-tv-pihole-blocklist/main/blocklist.txt
```

Merged and deduplicated from:

- [Huskynarr / lg-smart-tv-blocklist-adlist-pihole](https://gist.github.com/Huskynarr/82736c23c9c8ddf0ad084aef63f41510)
- [mcrumm / LG Smart-TV Blocklist Adlist (for PiHole)](https://gist.github.com/mcrumm/972070dfe67d44ed61c4247563cbf07c)
- [hugobatista / lg-tv-ad-block](https://github.com/hugobatista/lg-tv-ad-block) (`list` and `list-store`)
- [samsapti / LG-webOS-Blocklist](https://github.com/samsapti/LG-webOS-Blocklist)

The list is aggressive: it includes LG Content Store and firmware update hosts. Whitelist `snu.lge.com` and the `ngfts.lge.com` hosts if you want updates.
