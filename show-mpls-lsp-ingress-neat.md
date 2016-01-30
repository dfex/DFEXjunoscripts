### show-mpls-lsp-ingress-neat

This script provides a much neater output to "show mpls lsp ingress" with re-sizable fields in case your Path names are particularly long.  

Written in about 20 minutes so that @hoffnz can sleep better and help keep the Junos ER queue free from "niche pedantry", thereby allowing the rest of us that don't work at large tech companies to get **real** features added.

There is currently an output issue whereby the Total counts are somehow inserted before the LSP descriptions, but there is a cold beer waiting for me in the kitchen, and I can't be bothered wrestling with SLAX any more today.

Special thanks to @ssl_boy for his unfailing ability to keep it real : )

References:

* https://twitter.com/hoffnz/status/693152072062144512
* https://twitter.com/ssl_boy/status/693155428549709824

Output:

```
bdale@vsrx2# run op show-mpls-lsp-ingress-neat    
Ingress LSP: 2 sessions
Total 2 displayed, Up 2, Down 0

To              From            State Rt P  Active Path                    LSP Name                      
11.0.0.1        11.0.0.2        Up     0    FOLLOW-THE-YELLOW-BRICK-ROAD-2 THIS-IS-THE-BIGGEST-LSP-NAME-EVER
11.0.0.1        111.111.111.111 Up     0 *  WELL-PAVED-WITH-NICHE-PEDANTRY NO-WAY-THIS-LSP-NAME-IS-EVEN-BIGGER
```
You can test this directly from Junos providing your box can resolve DNS and reach the Internet:

```
op url https://raw.githubusercontent.com/dfex/DFEXjunoscripts/master/show-mpls-lsp-ingress-neat.slax
```