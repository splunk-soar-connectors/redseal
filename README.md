[comment]: # "Auto-generated SOAR connector documentation"
# RedSeal

Publisher: Splunk  
Connector Version: 1\.0\.7  
Product Vendor: RedSeal  
Product Name: RedSeal  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 4\.0\.1068  

This app integrates with RedSeal to implement investigative and polling actions

[comment]: # " File: readme.md"
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
**server\_url** |  required  | string | Server URL \(eg\: https\://10\.10\.10\.10\)
**verify\_server\_cert** |  optional  | boolean | Verify Server Certificate
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

For run query, &quotsource&quot and &quotdestination&quot parameter takes input as described\:<br><ul><li>For types <b>All Subnets</b>, <b>All Trusted Subnets</b> and <b>All Untrusted Subnets</b>, no input parameter needs to be provided for &quotsource&quot and &quotdestination&quot</li><br><li>For types <b>Host</b> and <b>Device</b>, <i>Tree ID</i> needs to be provided for &quotsource&quot and &quotdestination&quot</li><br><li>For type <b>Subnet</b>, <i>ID</i> needs to be provided for &quotsource&quot and &quotdestination&quot</li><br><li>For type <b>Group</b>, <i>redseal data path</i> needs to be provided for &quotsource&quot and &quotdestination&quot eg\. &quotSubnet/Trusted&quot, &quotPrimary Capability/Host&quot</li><br><li>For type <b>Address range</b>, parameter can be provided as IP, Netmask and Address Range for &quotsource&quot and &quotdestination&quot<br><ul>eg\. <li>&quot10\.10\.10\.1&quot</li><li>&quot10\.10\.1\.15/24&quot</li><li>&quot10\.10\.1\.1\-10\.10\.2\.255&quot</li></li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**source\_type** |  required  | Source type \(Default\: Address Range\) | string | 
**source** |  optional  | Source target | string |  `redseal tree id`  `ip`  `redseal address range`  `redseal group path` 
**destination\_type** |  required  | Destination type \(Default\: Address Range\) | string | 
**destination** |  optional  | Destination target | string |  `redseal tree id`  `ip`  `redseal address range`  `redseal group path` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.destination | string |  `redseal tree id`  `ip`  `redseal address range`  `redseal group path` 
action\_result\.parameter\.destination\_type | string | 
action\_result\.parameter\.source | string |  `redseal tree id`  `ip`  `redseal address range`  `redseal group path` 
action\_result\.parameter\.source\_type | string | 
action\_result\.data\.\*\.access\.\*\.Destination\.\@class | string | 
action\_result\.data\.\*\.access\.\*\.Destination\.CIDR | string |  `redseal address range` 
action\_result\.data\.\*\.access\.\*\.Destination\.Description | string | 
action\_result\.data\.\*\.access\.\*\.Destination\.GivenName | string | 
action\_result\.data\.\*\.access\.\*\.Destination\.ID | string |  `redseal tree id` 
action\_result\.data\.\*\.access\.\*\.Destination\.Name | string | 
action\_result\.data\.\*\.access\.\*\.Destination\.TrustLevel | string | 
action\_result\.data\.\*\.access\.\*\.Destination\.Type | string | 
action\_result\.data\.\*\.access\.\*\.Source\.\@class | string | 
action\_result\.data\.\*\.access\.\*\.Source\.CIDR | string |  `redseal address range` 
action\_result\.data\.\*\.access\.\*\.Source\.Description | string | 
action\_result\.data\.\*\.access\.\*\.Source\.GivenName | string | 
action\_result\.data\.\*\.access\.\*\.Source\.ID | string |  `redseal tree id` 
action\_result\.data\.\*\.access\.\*\.Source\.Name | string | 
action\_result\.data\.\*\.access\.\*\.Source\.TrustLevel | string | 
action\_result\.data\.\*\.access\.\*\.Source\.Type | string | 
action\_result\.data\.\*\.access\.\*\.Traffic\.\*\.DestinationIP | string |  `ip` 
action\_result\.data\.\*\.access\.\*\.Traffic\.\*\.DestinationPort | string |  `port` 
action\_result\.data\.\*\.access\.\*\.Traffic\.\*\.Protocol | string | 
action\_result\.data\.\*\.access\.\*\.Traffic\.\*\.SourceIP | string |  `ip` 
action\_result\.data\.\*\.access\.\*\.Traffic\.\*\.SourcePort | string |  `port` 
action\_result\.data\.\*\.impact\.Destination\.CollectiveImpact | string | 
action\_result\.data\.\*\.impact\.Destination\.ExposedVulnerabilities | string | 
action\_result\.data\.\*\.impact\.Destination\.LeapFrog | string | 
action\_result\.data\.\*\.impact\.Destination\.MaxCVSS | string | 
action\_result\.data\.\*\.impact\.Destination\.NumberOfHosts | string | 
action\_result\.data\.\*\.impact\.Destination\.OldestScan | string | 
action\_result\.data\.\*\.impact\.Destination\.UniqueVulnerabilities | string | 
action\_result\.data\.\*\.impact\.DestinationExposureType | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Destinations\.IPs | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Destinations\.Ports | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Destinations\.Restrict | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Destinations\.Targets\.Target\.\*\.ID | string |  `redseal tree id` 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Destinations\.Targets\.Target\.\*\.Name | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Destinations\.Targets\.Target\.\*\.Type | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.DirectMode | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.NoDetails | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Protocol | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Sources\.IPs | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Sources\.Ports | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Sources\.Restrict | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Sources\.Targets\.Target\.\*\.ID | string |  `redseal tree id` 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Sources\.Targets\.Target\.\*\.Name | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Sources\.Targets\.Target\.\*\.Type | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Track | string | 
action\_result\.data\.\*\.impact\.DownStream\.DownstreamQuery\.Type | string | 
action\_result\.data\.\*\.impact\.DownStream\.ReachableHosts | string | 
action\_result\.data\.\*\.impact\.PathStatus | string | 
action\_result\.data\.\*\.impact\.SourceExposureType | string | 
action\_result\.data\.\*\.threats\.\*\.Destination\.\@class | string | 
action\_result\.data\.\*\.threats\.\*\.Destination\.CIDR | string |  `redseal address range` 
action\_result\.data\.\*\.threats\.\*\.Destination\.Description | string | 
action\_result\.data\.\*\.threats\.\*\.Destination\.GivenName | string | 
action\_result\.data\.\*\.threats\.\*\.Destination\.ID | string |  `redseal tree id` 
action\_result\.data\.\*\.threats\.\*\.Destination\.Name | string | 
action\_result\.data\.\*\.threats\.\*\.Destination\.TrustLevel | string | 
action\_result\.data\.\*\.threats\.\*\.Destination\.Type | string | 
action\_result\.data\.\*\.threats\.\*\.LinkStatus | string | 
action\_result\.data\.\*\.threats\.\*\.Source\.\@class | string | 
action\_result\.data\.\*\.threats\.\*\.Source\.CIDR | string |  `redseal address range` 
action\_result\.data\.\*\.threats\.\*\.Source\.Description | string | 
action\_result\.data\.\*\.threats\.\*\.Source\.GivenName | string | 
action\_result\.data\.\*\.threats\.\*\.Source\.ID | string |  `redseal tree id` 
action\_result\.data\.\*\.threats\.\*\.Source\.Name | string | 
action\_result\.data\.\*\.threats\.\*\.Source\.TrustLevel | string | 
action\_result\.data\.\*\.threats\.\*\.Source\.Type | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Applications\.Threats\.\*\.Application | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Applications\.Threats\.\*\.DestinationIPs\.string | string |  `ip` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Applications\.Threats\.\*\.DestinationPorts\.string | string |  `port` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Applications\.Threats\.\*\.FromMultiHome | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Applications\.Threats\.\*\.Name | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Applications\.Threats\.\*\.Protocols\.string | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Applications\.Threats\.\*\.SourceIPs\.string | string |  `ip` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.\@class | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.Groups | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.IPAddress | string |  `ip` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.L2Connections | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.Metrics\.Name | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.Metrics\.TreeId | string |  `redseal tree id` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.Metrics\.URL | string |  `url` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.Name | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.RepositoryTimestamp | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.TreeId | string |  `redseal tree id` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.Type | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.URL | string |  `url` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Destination\.UniqueApplicationNames\.\@class | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Source\.\@class | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Source\.Groups | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Source\.IPAddress | string |  `ip` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Source\.L2Connections | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Source\.Name | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Source\.RepositoryTimestamp | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Source\.TreeId | string |  `redseal tree id` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Source\.Type | string | 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Source\.URL | string |  `url` 
action\_result\.data\.\*\.threats\.\*\.Threat\.\*\.Source\.UniqueApplicationNames\.\@class | string | 
action\_result\.data\.\*\.threats\.\*\.highVulnCount | string | 
action\_result\.data\.\*\.threats\.\*\.lowVulnCount | string | 
action\_result\.data\.\*\.threats\.\*\.medVulnCount | string | 
action\_result\.data\.\*\.threats\.\*\.totalRowCount | string | 
action\_result\.summary | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'on poll'
Ingest data to phantom

Type: **ingest**  
Read only: **True**

Action will add all the &quotZone Pair Access Details&quot for which &quotZone Pair Status&quot is <b>Warning</b> or <b>Fail</b> and &quotZone Pair Access Details&quot status is not <b>APPROVED</b>\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**container\_count** |  optional  | Maximum number of containers to ingest | numeric | 
**container\_id** |  optional  | Parameter ignored in this app | string | 
**start\_time** |  optional  | Parameter ignored in this app | numeric | 
**end\_time** |  optional  | Parameter ignored in this app | numeric | 
**artifact\_count** |  optional  | Parameter ignored in this app | numeric | 

#### Action Output
No Output  

## action: 'list subnets'
List all subnets of a given type

Type: **investigate**  
Read only: **True**

For type <b>Unmapped Hosts</b>, the &quotTree ID&quot obtained has to be used as input parameter for query actions with type <b>Host</b>\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**type** |  required  | Type of subnets \(Default\: Infrastructure\) | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.type | string | 
action\_result\.data\.\*\.CIDR | string |  `redseal address range` 
action\_result\.data\.\*\.Description | string | 
action\_result\.data\.\*\.GivenName | string | 
action\_result\.data\.\*\.Groups | string | 
action\_result\.data\.\*\.ID | string |  `redseal tree id` 
action\_result\.data\.\*\.IPAddress | string |  `ip` 
action\_result\.data\.\*\.L2Connections | string | 
action\_result\.data\.\*\.LastImportedDate | string | 
action\_result\.data\.\*\.LastModifiedDate\.\#text | string | 
action\_result\.data\.\*\.LastModifiedDate\.\@defined\-in | string | 
action\_result\.data\.\*\.Name | string | 
action\_result\.data\.\*\.PrimaryCapability | string | 
action\_result\.data\.\*\.RepositoryTimestamp | string | 
action\_result\.data\.\*\.TreeId | string |  `redseal tree id` 
action\_result\.data\.\*\.TrustLevel | string | 
action\_result\.data\.\*\.Type | string | 
action\_result\.data\.\*\.URL | string |  `url` 
action\_result\.data\.\*\.UniqueApplicationNames\.\@class | string | 
action\_result\.summary\.total\_subnets | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list devices'
List all devices of a given type

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**type** |  required  | Type of device \(Default\: Firewall\) | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.type | string | 
action\_result\.data\.\*\.DeviceType | string | 
action\_result\.data\.\*\.Groups | string | 
action\_result\.data\.\*\.IPAddress | string |  `ip` 
action\_result\.data\.\*\.L2Connections | string | 
action\_result\.data\.\*\.LastImportedDate | string | 
action\_result\.data\.\*\.LastModifiedDate\.\#text | string | 
action\_result\.data\.\*\.LastModifiedDate\.\@defined\-in | string | 
action\_result\.data\.\*\.Name | string | 
action\_result\.data\.\*\.PrimaryCapability | string | 
action\_result\.data\.\*\.RepositoryTimestamp | string | 
action\_result\.data\.\*\.TreeId | string |  `redseal tree id` 
action\_result\.data\.\*\.Type | string | 
action\_result\.data\.\*\.URL | string |  `url` 
action\_result\.data\.\*\.UniqueApplicationNames\.\@class | string | 
action\_result\.summary\.total\_devices | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 