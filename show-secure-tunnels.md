### show-secure-tunnels

This script provides formatted, summarised list of the essential pieces of information from the Junos command: ```show security ipsec security-associations detail ``` 

```
bdale@0ffnet-srx210-gw> op show-secure-tunnels    
VPN Name                 Interface   State   Port    Remote Gateway                          
MY-VPN                   st0.103     up      4500    181.212.91.157                          
OTHER-VPN                st0.110     up      500     64.242.153.255                          
SOMEONE-IPSEC-VPN        st0.101     up      500     203.133.113.253                         
OTHER-PERSON-VPN         st0.104     up      16664   216.213.96.242                          
SOME-TEST-VPN            st0.111     up      500     143.209.115.54                          
MGMT-VPNS-EASTWEST       st0.113     up      500     125.155.155.52                          
MGMT-VPNS-NORTHSOUTH     st0.112     up      500     121.153.62.210                          
DUMPS-IPSEC-VPN          st0.100     up      4500    176.166.251.174                          
bdale-IPSEC-VPN          st0.0       up      500     159.167.250.207           
```

You can test this directly from Junos providing your box can resolve DNS and reach the Internet:

```
op url https://raw.githubusercontent.com/dfex/DFEXjunoscripts/master/show-secure-tunnels.slax
```


