### chassis-beacon

This script triggers the chassis beacon (LED) to be enabled on a specified FPC for a specified period of time.

```
op chassis-beacon fpc 2 timeout 60
```

You can test this directly from Junos providing your box can resolve DNS and reach the Internet:

```
op url https://raw.githubusercontent.com/dfex/DFEXjunoscripts/master/chassis-beacon.slax fpc 2 timeout 60
```