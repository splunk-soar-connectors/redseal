[comment]: # "Auto-generated SOAR connector documentation"
# RedSeal

Publisher: Splunk  
Connector Version: 1.0.9  
Product Vendor: RedSeal  
Product Name: RedSeal  
Product Version Supported (regex): ".\*"  
Minimum Product Version: 4.0.1068  

This app integrates with RedSeal to implement investigative and polling actions

[comment]: # " File: README.md"
[comment]: # "  Copyright (c) 2019 Splunk Inc."
[comment]: # ""
[comment]: # "  Licensed under Apache 2.0 (https://www.apache.org/licenses/LICENSE-2.0.txt)"
[comment]: # "  "
[comment]: # ""
If server is configured for **HTTPS** and **HTTP** URL is configured in asset, "run query" and "on
poll" actions will not work.


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a RedSeal asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**server_url** |  required  | string | Server URL (eg: https://10.10.10.10)
**verify_server_cert** |  optional  | boolean | Verify Server Certificate
**username** |  required  | string | Username
**password** |  required  | password | Password

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[run query](#action-run-query) - Submit a query to fetch security impact, access details and threat details between two endpoints  
[on poll](#action-on-poll) - Ingest data to phantom  
[list subnets](#action-list-subnets) - List all subnets of a given type  
[list devices](#action-list-devices) - List all devices of a given type  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'run query'
Submit a query to fetch security impact, access details and threat details between two endpoints

Type: **investigate**  
Read only: **True**

For run query, &quotsource&quot and &quotdestination&quot parameter takes input as described:<br><ul><li>For types <b>All Subnets</b>, <b>All Trusted Subnets</b> and <b>All Untrusted Subnets</b>, no input parameter needs to be provided for &quotsource&quot and &quotdestination&quot</li><br><li>For types <b>Host</b> and <b>Device</b>, <i>Tree ID</i> needs to be provided for &quotsource&quot and &quotdestination&quot</li><br><li>For type <b>Subnet</b>, <i>ID</i> needs to be provided for &quotsource&quot and &quotdestination&quot</li><br><li>For type <b>Group</b>, <i>redseal data path</i> needs to be provided for &quotsource&quot and &quotdestination&quot eg. &quotSubnet/Trusted&quot, &quotPrimary Capability/Host&quot</li><br><li>For type <b>Address range</b>, parameter can be provided as IP, Netmask and Address Range for &quotsource&quot and &quotdestination&quot<br><ul>eg. <li>&quot10.10.10.1&quot</li><li>&quot10.10.1.15/24&quot</li><li>&quot10.10.1.1-10.10.2.255&quot</li></li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**source_type** |  required  | Source type (Default: Address Range) | string | 
**source** |  optional  | Source target | string |  `redseal tree id`  `ip`  `redseal address range`  `redseal group path` 
**destination_type** |  required  | Destination type (Default: Address Range) | string | 
**destination** |  optional  | Destination target | string |  `redseal tree id`  `ip`  `redseal address range`  `redseal group path` 

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string |  |   success  failed 
action_result.parameter.destination | string |  `redseal tree id`  `ip`  `redseal address range`  `redseal group path`  |   2c9090a556eaeeac0156eb04fe5d5468  10.100.111.20 
action_result.parameter.destination_type | string |  |   Address Range  All Subnets  All Trusted Subnets  All Untrusted Subnets  Device  Group  Host  Subnet 
action_result.parameter.source | string |  `redseal tree id`  `ip`  `redseal address range`  `redseal group path`  |   2c9090a556eaeeac0156eb04fe5d5468 
action_result.parameter.source_type | string |  |   Address Range  All Subnets  All Trusted Subnets  All Untrusted Subnets  Device  Group  Host  Subnet 
action_result.data.\*.access.\*.Destination.@class | string |  |   Host 
action_result.data.\*.access.\*.Destination.CIDR | string |  `redseal address range`  |   10.100.111.0/24 
action_result.data.\*.access.\*.Destination.Description | string |  |   connected to finance1 
action_result.data.\*.access.\*.Destination.GivenName | string |  |   Local - Finance 2 
action_result.data.\*.access.\*.Destination.ID | string |  `redseal tree id`  |   2c9080ff3955cfbc013955eebf9d034f 
action_result.data.\*.access.\*.Destination.Name | string |  |   Local - Finance 2 
action_result.data.\*.access.\*.Destination.TrustLevel | string |  |   Trusted 
action_result.data.\*.access.\*.Destination.Type | string |  |   Numbered 
action_result.data.\*.access.\*.Source.@class | string |  |   Host 
action_result.data.\*.access.\*.Source.CIDR | string |  `redseal address range`  |   10.100.111.0/24 
action_result.data.\*.access.\*.Source.Description | string |  |   Checkpoint 
action_result.data.\*.access.\*.Source.GivenName | string |  |   Local - Finance 2 
action_result.data.\*.access.\*.Source.ID | string |  `redseal tree id`  |   2c9080ff3955cfbc013955eebf9d034f 
action_result.data.\*.access.\*.Source.Name | string |  |   Local - Finance 2 
action_result.data.\*.access.\*.Source.TrustLevel | string |  |   Trusted 
action_result.data.\*.access.\*.Source.Type | string |  |   Numbered 
action_result.data.\*.access.\*.Traffic.\*.DestinationIP | string |  `ip`  |   10.100.111.9 
action_result.data.\*.access.\*.Traffic.\*.DestinationPort | string |  `port`  |   any 
action_result.data.\*.access.\*.Traffic.\*.Protocol | string |  |   any 
action_result.data.\*.access.\*.Traffic.\*.SourceIP | string |  `ip`  |   10.100.111.2 
action_result.data.\*.access.\*.Traffic.\*.SourcePort | string |  `port`  |   any 
action_result.data.\*.impact.Destination.CollectiveImpact | string |  |   ACIS 
action_result.data.\*.impact.Destination.ExposedVulnerabilities | string |  |   76 
action_result.data.\*.impact.Destination.LeapFrog | string |  |   true 
action_result.data.\*.impact.Destination.MaxCVSS | string |  |   10 
action_result.data.\*.impact.Destination.NumberOfHosts | string |  |   1 
action_result.data.\*.impact.Destination.OldestScan | string |  |   Jul 16, 2016 11:00:51 AM UTC 
action_result.data.\*.impact.Destination.UniqueVulnerabilities | string |  |   64 
action_result.data.\*.impact.DestinationExposureType | string |  |   Indirect 
action_result.data.\*.impact.DownStream.DownstreamQuery.Destinations.IPs | string |  |   any 
action_result.data.\*.impact.DownStream.DownstreamQuery.Destinations.Ports | string |  |   any 
action_result.data.\*.impact.DownStream.DownstreamQuery.Destinations.Restrict | string |  |   ONLY_COMPUTER_SYSTEMS 
action_result.data.\*.impact.DownStream.DownstreamQuery.Destinations.Targets.Target.\*.ID | string |  `redseal tree id`  |   2c9090a556eaeeac0156eb05007067e5 
action_result.data.\*.impact.DownStream.DownstreamQuery.Destinations.Targets.Target.\*.Name | string |  |   All Trusted Subnets 
action_result.data.\*.impact.DownStream.DownstreamQuery.Destinations.Targets.Target.\*.Type | string |  |   AllTrustedSubnets 
action_result.data.\*.impact.DownStream.DownstreamQuery.DirectMode | string |  |   false 
action_result.data.\*.impact.DownStream.DownstreamQuery.NoDetails | string |  |   false 
action_result.data.\*.impact.DownStream.DownstreamQuery.Protocol | string |  |   any 
action_result.data.\*.impact.DownStream.DownstreamQuery.Sources.IPs | string |  |   any 
action_result.data.\*.impact.DownStream.DownstreamQuery.Sources.Ports | string |  |   any 
action_result.data.\*.impact.DownStream.DownstreamQuery.Sources.Restrict | string |  |   NONE 
action_result.data.\*.impact.DownStream.DownstreamQuery.Sources.Targets.Target.\*.ID | string |  `redseal tree id`  |   2c9090a556eaeeac0156eb05007067e5 
action_result.data.\*.impact.DownStream.DownstreamQuery.Sources.Targets.Target.\*.Name | string |  |   lynette.lab.redseal.net 
action_result.data.\*.impact.DownStream.DownstreamQuery.Sources.Targets.Target.\*.Type | string |  |   Host 
action_result.data.\*.impact.DownStream.DownstreamQuery.Track | string |  |   false 
action_result.data.\*.impact.DownStream.DownstreamQuery.Type | string |  |   NETMAP 
action_result.data.\*.impact.DownStream.ReachableHosts | string |  |   109 
action_result.data.\*.impact.PathStatus | string |  |   OPEN 
action_result.data.\*.impact.SourceExposureType | string |  |   Untrusted 
action_result.data.\*.threats.\*.Destination.@class | string |  |   Host 
action_result.data.\*.threats.\*.Destination.CIDR | string |  `redseal address range`  |   10.102.4.0/24 
action_result.data.\*.threats.\*.Destination.Description | string |  |   connected to finance1 
action_result.data.\*.threats.\*.Destination.GivenName | string |  |   FTP-2 
action_result.data.\*.threats.\*.Destination.ID | string |  `redseal tree id`  |   2c9080ff3955cfbc013955eead0f0229 
action_result.data.\*.threats.\*.Destination.Name | string |  |   Local - Finance 2 
action_result.data.\*.threats.\*.Destination.TrustLevel | string |  |   Trusted 
action_result.data.\*.threats.\*.Destination.Type | string |  |   Numbered 
action_result.data.\*.threats.\*.LinkStatus | string |  |    
action_result.data.\*.threats.\*.Source.@class | string |  |   Host 
action_result.data.\*.threats.\*.Source.CIDR | string |  `redseal address range`  |   10.100.111.0/24 
action_result.data.\*.threats.\*.Source.Description | string |  |   connected to finance1 
action_result.data.\*.threats.\*.Source.GivenName | string |  |   Local - Finance 2 
action_result.data.\*.threats.\*.Source.ID | string |  `redseal tree id`  |   2c9080ff3955cfbc013955eebf9d034f 
action_result.data.\*.threats.\*.Source.Name | string |  |   Local - Finance 2 
action_result.data.\*.threats.\*.Source.TrustLevel | string |  |   Trusted 
action_result.data.\*.threats.\*.Source.Type | string |  |   Numbered 
action_result.data.\*.threats.\*.Threat.\*.Applications.Threats.\*.Application | string |  |   Web server 
action_result.data.\*.threats.\*.Threat.\*.Applications.Threats.\*.DestinationIPs.string | string |  `ip`  |   10.102.4.9 
action_result.data.\*.threats.\*.Threat.\*.Applications.Threats.\*.DestinationPorts.string | string |  `port`  |   80 
action_result.data.\*.threats.\*.Threat.\*.Applications.Threats.\*.FromMultiHome | string |  |   false 
action_result.data.\*.threats.\*.Threat.\*.Applications.Threats.\*.Name | string |  |   CVE-2004-2320 
action_result.data.\*.threats.\*.Threat.\*.Applications.Threats.\*.Protocols.string | string |  |   TCP 
action_result.data.\*.threats.\*.Threat.\*.Applications.Threats.\*.SourceIPs.string | string |  `ip`  |   10.100.111.9 
action_result.data.\*.threats.\*.Threat.\*.Destination.@class | string |  |   Host 
action_result.data.\*.threats.\*.Threat.\*.Destination.Groups | string |  |    
action_result.data.\*.threats.\*.Threat.\*.Destination.IPAddress | string |  `ip`  |   10.102.4.9 
action_result.data.\*.threats.\*.Threat.\*.Destination.L2Connections | string |  |    
action_result.data.\*.threats.\*.Threat.\*.Destination.Metrics.Name | string |  |   lynette.lab.redseal.net 
action_result.data.\*.threats.\*.Threat.\*.Destination.Metrics.TreeId | string |  `redseal tree id`  |   2c9090a556eaeeac0156eb0503c801f1 
action_result.data.\*.threats.\*.Threat.\*.Destination.Metrics.URL | string |  `url`  |   https://10.17.1.84/data/metrics/host/2c9090a556eaeeac0156eb0503c801f1 
action_result.data.\*.threats.\*.Threat.\*.Destination.Name | string |  |   lynette.lab.redseal.net 
action_result.data.\*.threats.\*.Threat.\*.Destination.RepositoryTimestamp | string |  |   Aug 15, 2016 1:09:00 PM UTC 
action_result.data.\*.threats.\*.Threat.\*.Destination.TreeId | string |  `redseal tree id`  |   2c9090a556eaeeac0156eb0503c801f1 
action_result.data.\*.threats.\*.Threat.\*.Destination.Type | string |  |   Active 
action_result.data.\*.threats.\*.Threat.\*.Destination.URL | string |  `url`  |   https://10.17.1.84/data/host/id/2c9090a556eaeeac0156eb0503c801f1 
action_result.data.\*.threats.\*.Threat.\*.Destination.UniqueApplicationNames.@class | string |  |   list 
action_result.data.\*.threats.\*.Threat.\*.Source.@class | string |  |   Host 
action_result.data.\*.threats.\*.Threat.\*.Source.Groups | string |  |    
action_result.data.\*.threats.\*.Threat.\*.Source.IPAddress | string |  `ip`  |   10.100.111.9 
action_result.data.\*.threats.\*.Threat.\*.Source.L2Connections | string |  |    
action_result.data.\*.threats.\*.Threat.\*.Source.Name | string |  |   lynette.lab.redseal.net 
action_result.data.\*.threats.\*.Threat.\*.Source.RepositoryTimestamp | string |  |   Aug 23, 2016 4:31:28 PM UTC 
action_result.data.\*.threats.\*.Threat.\*.Source.TreeId | string |  `redseal tree id`  |   2c9090a556eaeeac0156eb04fe6e54e1 
action_result.data.\*.threats.\*.Threat.\*.Source.Type | string |  |   Active 
action_result.data.\*.threats.\*.Threat.\*.Source.URL | string |  `url`  |   https://10.17.1.84/data/host/id/2c9090a556eaeeac0156eb04fe6e54e1 
action_result.data.\*.threats.\*.Threat.\*.Source.UniqueApplicationNames.@class | string |  |   list 
action_result.data.\*.threats.\*.highVulnCount | string |  |   0 
action_result.data.\*.threats.\*.lowVulnCount | string |  |   0 
action_result.data.\*.threats.\*.medVulnCount | string |  |   0 
action_result.data.\*.threats.\*.totalRowCount | string |  |   0 
action_result.summary | string |  |  
action_result.message | string |  |   Impact details found. Access details found. Threat details found. 
summary.total_objects | numeric |  |   1 
summary.total_objects_successful | numeric |  |   1   

## action: 'on poll'
Ingest data to phantom

Type: **ingest**  
Read only: **True**

Action will add all the &quotZone Pair Access Details&quot for which &quotZone Pair Status&quot is <b>Warning</b> or <b>Fail</b> and &quotZone Pair Access Details&quot status is not <b>APPROVED</b>.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**container_count** |  optional  | Maximum number of containers to ingest | numeric | 
**container_id** |  optional  | Parameter ignored in this app | string | 
**start_time** |  optional  | Parameter ignored in this app | numeric | 
**end_time** |  optional  | Parameter ignored in this app | numeric | 
**artifact_count** |  optional  | Parameter ignored in this app | numeric | 

#### Action Output
No Output  

## action: 'list subnets'
List all subnets of a given type

Type: **investigate**  
Read only: **True**

For type <b>Unmapped Hosts</b>, the &quotTree ID&quot obtained has to be used as input parameter for query actions with type <b>Host</b>.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**type** |  required  | Type of subnets (Default: Infrastructure) | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string |  |   success  failed 
action_result.parameter.type | string |  |   Infrastructure  Known Compromises  Trusted  Unmapped Hosts 
action_result.data.\*.CIDR | string |  `redseal address range`  |   10.100.0.0/30 
action_result.data.\*.Description | string |  |   connected to Core-2-ios 
action_result.data.\*.GivenName | string |  |   Local - Finance 3 
action_result.data.\*.Groups | string |  |    
action_result.data.\*.ID | string |  `redseal tree id`  |   2c9080ff3955cfbc013955eecbc2047c 
action_result.data.\*.IPAddress | string |  `ip`  |   10.100.111.2 
action_result.data.\*.L2Connections | string |  |    
action_result.data.\*.LastImportedDate | string |  |   Aug 10, 2015 1:33:45 PM UTC 
action_result.data.\*.LastModifiedDate.#text | string |  |   Aug 10, 2015 1:33:45 PM UTC 
action_result.data.\*.LastModifiedDate.@defined-in | string |  |   Computer 
action_result.data.\*.Name | string |  |   10.100.0.0/30 
action_result.data.\*.PrimaryCapability | string |  |   FIREWALL 
action_result.data.\*.RepositoryTimestamp | string |  |   Jul 6, 2011 1:40:26 PM UTC 
action_result.data.\*.TreeId | string |  `redseal tree id`  |   2c9080ff3955cfbc013955ee92630157 
action_result.data.\*.TrustLevel | string |  |   Trusted 
action_result.data.\*.Type | string |  |   Numbered 
action_result.data.\*.URL | string |  `url`  |   https://10.17.1.84/data/subnet/id/2c9080ff3955cfbc013955eecbc2047c 
action_result.data.\*.UniqueApplicationNames.@class | string |  |   list 
action_result.summary.total_subnets | numeric |  |   115 
action_result.message | string |  |   Total subnets: 115 
summary.total_objects | numeric |  |   1 
summary.total_objects_successful | numeric |  |   1   

## action: 'list devices'
List all devices of a given type

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**type** |  required  | Type of device (Default: Firewall) | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string |  |   success  failed 
action_result.parameter.type | string |  |   Firewall  Host  Load Balancer  Router  Switch  Wireless Controller 
action_result.data.\*.DeviceType | string |  |   NetScreen 
action_result.data.\*.Groups | string |  |    
action_result.data.\*.IPAddress | string |  `ip`  |   10.100.111.2 
action_result.data.\*.L2Connections | string |  |    
action_result.data.\*.LastImportedDate | string |  |   Aug 10, 2015 1:33:45 PM UTC 
action_result.data.\*.LastModifiedDate.#text | string |  |   Aug 10, 2015 1:33:45 PM UTC 
action_result.data.\*.LastModifiedDate.@defined-in | string |  |   Computer 
action_result.data.\*.Name | string |  |   Campus-lab-FW-MFE 
action_result.data.\*.PrimaryCapability | string |  |   FIREWALL 
action_result.data.\*.RepositoryTimestamp | string |  |   Jul 6, 2011 1:40:26 PM UTC 
action_result.data.\*.TreeId | string |  `redseal tree id`  |   2c9080ff3955cfbc013955ee92630157 
action_result.data.\*.Type | string |  |   Active 
action_result.data.\*.URL | string |  `url`  |   https://10.17.1.84/data/device/id/2c9080ff3955cfbc013955ee92630157 
action_result.data.\*.UniqueApplicationNames.@class | string |  |   list 
action_result.summary.total_devices | numeric |  |   518 
action_result.message | string |  |   Total devices: 518 
summary.total_objects | numeric |  |   1 
summary.total_objects_successful | numeric |  |   1 