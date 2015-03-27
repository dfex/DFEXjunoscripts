### show-lldp-neat

This script provides a similar output to "show lldp neighbor" except it includes the LLDP Port ID field.

Used in conjuction with **set protocols lldp port-id-subtype interface-name** on the remote switch, it will provide the far-end switch physical port name and description.

```
comlinx@GD-rck-22c> op show-lldp-neat    
Local Interface     Local Parent        Neighbour Hostname  Neighbour Interface Neighbour Interface Description
ge-0/1/0.0          -                   GD-eng-22c          523                 ge-0/1/1.0                    
```
You can test this directly from Junos providing your box can resolve DNS and reach the Internet:

```
op url https://raw.githubusercontent.com/dfex/DFEXjunoscripts/master/show-lldp-neat.slax
```