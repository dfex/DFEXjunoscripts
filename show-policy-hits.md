### show-policy-hits

This script provides list of all security policies configured on an SRX, with source zone, destination zone, policy name and policy action alongside a counter for each time the policy has been triggered.

Juniper has since provided this functionality built-in to Junos 12.1, with```show security policies hit-count```but for versions prior to that it was difficult to compile a readable list. 

In order to capture policy hits, all policies will require```then count```as a policy action.

To apply this to an existing SRX deployment, use an apply-group as follows:

```
set group POLICY-COUNT set security policies from-zone <*> to-zone <*> policy <*> then count
set security policies apply-group POLICY-COUNT
```
You can test this directly from Junos providing your box can resolve DNS and reach the Internet:

```
op url https://raw.githubusercontent.com/dfex/DFEXjunoscripts/master/show-policy-hits.slax
```