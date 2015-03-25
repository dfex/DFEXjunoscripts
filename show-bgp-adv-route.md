### show-bgp-adv-route

This script takes an IP/prefix as input, and lists all BGP ASs and Peers to which it is currently being advertised along with any aggregate prefix:

```
bdale@0ffnet-srx210-gw> op show-bgp-adv-route prefix 172.16.10.4   
Peer AS    Peer IP                            Aggregate Prefix                   
65534      172.16.22.1                        172.16.10.0/24                     
4294967295 172.16.23.1                        172.16.10.0/24                     
1234567890 2402:c001:fcd1:ba20:ae43:1001:2311 172.16.0.0/16
```

You can test this directly from Junos providing your box can resolve DNS and reach the Internet:

```
op url https://raw.githubusercontent.com/dfex/DFEXjunoscripts/master/show-bgp-adv-route.slax prefix 172.16.10.1
```