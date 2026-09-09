# LG Smart TV (webOS) Pi-hole Blocklist

Blocks ads, tracking, ACR, telemetry, firmware updates, ThinQ, voice search and home-screen recommendations on LG webOS smart TVs. Hosts-format adlists for Pi-hole, AdGuard Home or any DNS blocker, plus a regex layer that kills every subdomain and CDN alias.

## Adlists

**Aggressive** (everything, LG Content Store included):

```
https://raw.githubusercontent.com/nesdeq/lg-smart-tv-pihole-blocklist/main/aggressive.txt
```

**Working app store** (same list minus the hosts the LG Content Store needs to install and update apps; firmware updates and everything else stay blocked):

```
https://raw.githubusercontent.com/nesdeq/lg-smart-tv-pihole-blocklist/main/workingappstore.txt
```

Paste the URL into Pi-hole under Adlists, then run `pihole -g`.

## Regex layer (aggressive, optional)

Adlists match exact hostnames only. The matching regex below also catches every subdomain, country prefix and CDN alias (`*.aws-prd.net`, `*.edgekey.net`) of the same domains. Pi-hole web UI: Domains, then the Regex filter tab, paste the one line, Add to denylist. Or on the Pi-hole:

```
pihole --regex '<paste the regex>'
```

With `aggressive.txt`:

```
((\.|^)((lge|lgtvcommon|lgappstv|lgsmartplatform|lgsmartad|lgeapi|lgthinq|lgthinqhome|lgtviot|lgwebostv|lgtvsdp|nextlgsdp|wiselg|lggalleryplus|lgsmartweb)\.com|(lgtvcommon|lgsmartad)\.es|(aws-prd|aws-thinq-prd|esi-prd)\.net|lgads\.tv)(\.|$))|((^|[.-])(lge|lgtvcommon|lgappstv|lgsmartplatform|lgsmartad|lgeapi|lgthinq|lgthinqhome|lgtviot|lgwebostv|lgtvsdp|nextlgsdp|wiselg|lggalleryplus|lgsmartweb)-(com|es)\.)|((\.|^)((smartclip|yumenetworks|thetake|mindfieldonline|ueiwsp|cjpowercast)\.com|smartclip\.net|(castoola|alphonso)\.tv|iltrovatore\.it|kbbtv\.tech)(\.|$))|((\.|^)(lg-channelplus-[a-z0-9-]+\.xumo\.com|app-lgwebos\.pluto\.tv)$)|((\.|^)(api\.us-east-1\.aiv-delivery\.net|blacknut-prod-images-cdn\.b-cdn\.net|canvas\.tubitv\.com|cdn77\.utomik\.com|cf-trickplay\.aux\.pv-cdn\.net|developers\.google\.com|discovery\.meethue\.com|eligibility-panelresearch\.googlevideo\.com|enabler\.msf\.cdn\.mediaset\.net|ht\.la7\.it|i\.ibb\.co|images\.pluto\.tv|images\.redbox\.com|img\.nvidiagrid\.net|mediaservices\.cdn-apple\.com|nevoai-iothub-54-prod\.azure-devices\.net|s3-iad-2\.cf\.dash\.row\.aiv-cdn\.net|service\.idsync\.analytics\.yahoo\.com|threeplr-avuypkjypveaj-0\.api\.amazonvideo\.com|unagi-na\.amazon\.com|vjs\.zencdn\.net|vod08\.msf\.cdn\.mediaset\.net|www\.la7\.it)$)
```

With `workingappstore.txt` (never touches `lgtvsdp.com`, `lgappstv.com`, `nextlgsdp.com`, the `ngfts` download servers or `lge.com` beyond the update hosts):

```
((\.|^)((lgtvcommon|lgsmartplatform|lgsmartad|lgeapi|lgthinq|lgthinqhome|lgtviot|lgwebostv|lggalleryplus|lgsmartweb)\.com|(lgtvcommon|lgsmartad)\.es|lgads\.tv)(\.|$))|((\.|^)(snu|su|su-ssl|nsu|snu-dev|su-dev|lgtvonline)\.lge\.com(\.|$))|((\.|^)(rdx2|security|smartshare)\.lgtvsdp\.com(\.|$))|((\.|^)(ad|ibs|ibis|lgrecommends)\.lgappstv\.com(\.|$))|((\.|^)(ibs|ibsstat|rdx2)\.nextlgsdp\.com(\.|$))|(^([a-z]{2,3}\.)?tv\.wiselg\.com$)|((^|[.-])(lgtvcommon|lgsmartplatform|lgsmartad|lgeapi|lgthinq|lgthinqhome|lgtviot|lgwebostv|lggalleryplus|lgsmartweb)-(com|es)\.)|((\.|^)((smartclip|yumenetworks|thetake|mindfieldonline|ueiwsp|cjpowercast)\.com|smartclip\.net|(castoola|alphonso)\.tv|iltrovatore\.it|kbbtv\.tech)(\.|$))|((\.|^)(lg-channelplus-[a-z0-9-]+\.xumo\.com|app-lgwebos\.pluto\.tv)$)|((\.|^)(api\.us-east-1\.aiv-delivery\.net|blacknut-prod-images-cdn\.b-cdn\.net|canvas\.tubitv\.com|cdn77\.utomik\.com|cf-trickplay\.aux\.pv-cdn\.net|developers\.google\.com|discovery\.meethue\.com|eligibility-panelresearch\.googlevideo\.com|enabler\.msf\.cdn\.mediaset\.net|ht\.la7\.it|i\.ibb\.co|images\.pluto\.tv|images\.redbox\.com|img\.nvidiagrid\.net|mediaservices\.cdn-apple\.com|nevoai-iothub-54-prod\.azure-devices\.net|s3-iad-2\.cf\.dash\.row\.aiv-cdn\.net|service\.idsync\.analytics\.yahoo\.com|threeplr-avuypkjypveaj-0\.api\.amazonvideo\.com|unagi-na\.amazon\.com|vjs\.zencdn\.net|vod08\.msf\.cdn\.mediaset\.net|www\.la7\.it)$)
```

Verify a match with `pihole-FTL regex-test "eic.recommend.lgtvcommon.com" '<regex>'`. Regex entries apply to every client, so if you use the LG ThinQ app elsewhere on the network, put the regex in a Pi-hole group that contains only the TV.

Two endpoints from the Gamers Nexus report cannot be blocked by DNS: the hardcoded firmware fallback `156.147.69.32:8080` and the live telemetry endpoint `54.186.247.229:443`. Block those at the firewall.

## Sources

Merged and deduplicated from:

- [Huskynarr / lg-smart-tv-blocklist-adlist-pihole](https://gist.github.com/Huskynarr/82736c23c9c8ddf0ad084aef63f41510)
- [mcrumm / LG Smart-TV Blocklist Adlist (for PiHole)](https://gist.github.com/mcrumm/972070dfe67d44ed61c4247563cbf07c)
- [hugobatista / lg-tv-ad-block](https://github.com/hugobatista/lg-tv-ad-block) (`list` and `list-store`)
- [samsapti / LG-webOS-Blocklist](https://github.com/samsapti/LG-webOS-Blocklist)
- [Gamers Nexus, 216,000,000 Spy TVs](https://www.youtube.com/watch?v=6IFVTcM28KA), via the report's companion guide by Wendell of Level1Techs: [LG TV Block Mini-How-to](https://forum.level1techs.com/t/lg-tv-block-mini-how-to/255178) (hosts observed live on a 2025 G5 running webOS 25)
