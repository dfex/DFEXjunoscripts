# connectedness

This script is used to perform a number of general health-check tests in order to determine the "connectedness" of a node.

It also allows for a number of actions to then be taken on the configuration of the router to propagate this connectivity state throughout a network.

By default, the script will execute in "info" mode, which will simply summarise the current "connectedness" of the platform.

When passed the execute parameter, the script will use the test results and make changes to the configuration.

Tests include:

* Comparing the number of established BGP peers against a configured threshold
* Testing for the presence of a specified marker prefix in OSPF
* Testing for the presence of a specified marker prefix in ISIS
* Comparing the number of FULL OSPF neighbours against a configured threshold (This test is currently disabled due to the use of SLAX mvars requiring Junos 12.2 or later)
* Testing for the presence of a specified (BGP) prefix from a specified AS
* Comparing the number of active prefixes in a specified route-table against a configured threshold
* Comparing the number of active next-hops installed for a specified prefix against a configured threshold

Current actions include:

* Overload an OSPF Area; in the master instance by default, or in a specified routing-instance
* Overload an ISIS Area; in the master instance by default, or in a specified routing-instance
* Add an apply-group to a specified bgp group; in the master instance by default, or in a specified routing-instance

To do:

* ~~Add functionality to remove actions (when connectedness is restored)~~
* Test that removal of apply-group only affects specified apply-group and not all
* Run pre-flight checks to ensure we're not performing commits on existing configuration
* Add in thresholds/scoring system


###Example configuration:

Most variable names should be fairly self-explanatory

    match / {
        <op-script-results> {
            if ($mode = "info") {
                <output> jcs:printf("%s", "Informational mode" );
                call established-bgp-peers( $min-peer-count = "0" );
                call ospf-marker-route( $marker-route = "11.0.0.1/32" );
                call isis-marker-route( $marker-route = "11.0.0.1/32" );
                call full-ospf-neighbours( $area = "0", $min-ospf-neighbours = "4" );
                call bgp-as-marker-route( $marker-route = "103.252.114.0/23", $as-number = "13414" );
                call active-prefixes-installed( $route-table = "inet.0", $min-active-routes = "5" );
                call active-next-hops( $prefix = "11.0.0.0/24", $route-table = "inet.0", $min-next-hops = "3" );
            }
            else if ($mode = "execute") {
                <output> jcs:printf("%s", "Execute mode" );
                call overload-isis();
                call overload-isis( $instance = "BEN" );
                call overload-ospf();
                call overload-ospf( $instance = "BEN" );
                call bgp-apply-group( $instance = "master", $bgp-group = "MYPEERS", $apply-group-name = "BGP-REJECT-ALL")
            }
        }
        var $close-results = jcs:close($router);
    }

###Example output:
	bdale@mx80-lab01> op connectedness
	Informational mode
	PASS: Available BGP Peers: 0 of 2
	FAIL: OSPF marker route 11.0.0.1/32 is inactive
	FAIL: ISIS marker route 11.0.0.1/32 is inactive
	FAIL: Full OSPF neighbours: 0
	FAIL: BGP marker route 103.252.114.0/23 inactive from AS13414
	PASS: 13 active prefixes in inet.0 - 5 required
	PASS: Prefix 11.0.0.0/24 has 5 out of 3 active next-hops
    
    bdale@mx80-lab01> op connectedness mode execute                           
    Execute mode
    Overloading ISIS in instance master
    Overloading ISIS in instance TEST-INSTANCE
    Overloading OSPF in instance master
    Overloading OSPF in instance TEST-INSTANCE