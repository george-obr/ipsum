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

Wall of shame (2020-01-14)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
185.220.102.8|-|10
128.31.0.13|tor-exit.csail.mit.edu|9
89.234.157.254|marylou.nos-oignons.net|9
171.25.193.77|tor-exit1-readme.dfri.se|9
171.25.193.78|tor-exit4-readme.dfri.se|9
185.220.101.3|-|8
185.165.168.229|-|8
104.244.79.250|gulltoppr.prpl.space|8
45.95.168.105|maxko-hosting.com|8
85.248.227.164|tollana.enn.lu|8
171.25.193.25|tor-exit5-readme.dfri.se|8
176.10.99.200|accessnow.org|8
144.217.255.89|ns542132.ip-144-217-255.net|8
35.0.127.52|tor-exit.eecs.umich.edu|8
5.199.130.188|tor.piratenpartei-nrw.de|8
46.165.230.5|tor-exit.dhalgren.org|8
195.206.105.217|zrh-exit.privateinternetaccess.com|8
