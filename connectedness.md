# connectedness

This script is used to perform a general health-check of the connectedness of a node.  
It performs a series of 6 tests, which can be customised to suit the specific node they are being executed on. 

Tests include:

* Comparing the number of established BGP peers against a configured threshold
* Testing for the presence of a specified marker prefix in OSPF
* Testing for the presence of a specified marker prefix in ISIS
* Comparing the number of FULL OSPF neighbours against a configured threshold (This test is currently disabled due to the use of SLAX mvars requiring Junos 12.2 or later)
* Testing for the presence of a specified (BGP) prefix from a specified AS
* Comparing the number of active prefixes in a specified route-table against a configured threshold

###Example configuration:

Most variable names should be fairly self-explanatory

    match / {
    	<op-script-results> {
        	call established-bgp-peers( $min-peer-count = "0" );
        	call ospf-marker-route( $marker-route = "11.0.0.1/32" );
        	call isis-marker-route( $marker-route = "11.0.0.1/32" );
        	call full-ospf-neighbours( $area = "0", $min-ospf-neighbours = "4" );
        	call bgp-as-marker-route( $marker-route = "103.252.114.0/23", $as-number = "13414" );
        	call active-prefixes( $route-table = "inet.0", $min-active-routes = "5");
        	call active-next-hops( $prefix = "10.0.0.0/24", $route-table = "inet.0", $min-next-hops = "3" );

        }
    }

###Example output:
	bdale@vsrx1-fried> op connectedness    
	PASS: Available BGP Peers: 0 of 2
	FAIL: OSPF marker route 11.0.0.1/32 is inactive
	FAIL: ISIS marker route 11.0.0.1/32 is inactive
	FAIL: Full OSPF neighbours: 0
	FAIL: BGP marker route 103.252.114.0/23 inactive from AS13414
	PASS: 13 active prefixes in inet.0 - 5 required
	PASS: Prefix 11.0.0.0/24 has 5 out of 3 active next-hops
