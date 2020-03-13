![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of shame (2020-03-13)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
18.27.197.252|wholesomeserver.media.mit.edu|11
89.234.157.254|marylou.nos-oignons.net|9
104.244.76.189|tor-exit-node|9
144.217.255.89|ns542132.ip-144-217-255.net|9
51.75.144.43|ns3129517.ip-51-75-144.eu|9
178.165.72.177|178-165-72-177-kh.maxnet.ua|9
62.102.148.68|-|9
46.165.230.5|tor-exit.dhalgren.org|9
195.206.105.217|zrh-exit.privateinternetaccess.com|9
185.100.87.206|geri.enn.lu|9
162.247.74.74|-|8
118.70.216.153|-|8
171.25.193.77|tor-exit1-readme.dfri.se|8
171.25.193.78|tor-exit4-readme.dfri.se|8
185.107.47.171|tor-exit.r2.darknet.dev|8
104.244.72.115|tor-exit-hermes.greektor.net|8
176.10.104.240|tor1e1.digitale-gesellschaft.ch|8
46.165.245.154|-|8
157.230.123.253|-|8
45.33.70.146|ssh.scan.ampereinnotech.com|8
94.230.208.147|tor3e1.digitale-gesellschaft.ch|8
45.67.14.0|-|8
167.88.7.134|the-windy-onion.tor-exits.alec.ninja|8
185.220.103.9|katherinegun.tor-exit.calyxinstitute.org|8
185.220.102.7|-|8
171.25.193.20|tor-exit0-readme.dfri.se|8
176.10.99.200|accessnow.org|8
45.148.10.92|-|8
185.220.100.247|tor-exit-8.zbau.f3netze.de|8
185.220.100.244|tor-exit-5.zbau.f3netze.de|8
185.220.100.242|tor-exit-15.zbau.f3netze.de|8
185.220.100.243|tor-exit-16.zbau.f3netze.de|8
41.234.66.22|host-41.234.66.22.tedata.net|8
158.174.122.199|h-122-199.A357.priv.bahnhof.se|8
107.189.10.212|tor-node.com|8
