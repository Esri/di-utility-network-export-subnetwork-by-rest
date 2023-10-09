# export-subnetwork-only
 
This solution transforms into several output formats the JSON return of the Export Subnetwork REST api. The api parameters are configured in the solution and parameterized as Query String parameters of the HTTPCaller transformer. The solution does not cover other customer data that are found in the feature layers, unless configured in the ```resultTypeFields``` array of the ```resultTypes``` parameter. See [export-subnetwork-plus-customer-fields ](https://github.com/salvaleonrp/di-utility-network-export-subnetwork-by-rest/blob/main/Export%20Subnetwork%20plus%20customer%20fields/ExportSubnetworkPlusCustomer%20Fields.md#export-subnetwork-plus-customer-fields) folder for an advanced solution.

## Instructions
1. Fork and then clone the repo. 
> [!NOTE]
> If you do not intend to contribute to this repo, you can download the workspace template (fmwt) file.<br/>
2. Unzip to your desired destination and open the ExportSubnetworkV6.fmwt FME workspace template (fmwt) file using Data Interoperability workbench app. You can also double-click to open.
> [!NOTE]
> Since this template includes a cache, when you open the template, you will see the data on the canvass in various stages of the translation without being connected to the configured utility network. However, once you run the template, the workspace will attempt to reconnect to the feature service and you will lose the cache.
> The solution is meant as a guide. The provided workspace will not run your own enterprise utility network dataset correctly without any re-configuration. <br/>

3. Re-configure the workspace to your own utility network. 
> [!IMPORTANT]
> a. The token getter is configured to work with Basic authentication using the UN owner account username and password. If you use OAUTH2 or other authentication types for your dataset, a web connection must be created and the [ESRIOnlineTokenGetter](https://hub.safe.com/publishers/bruceharold/transformers/esrionlinetokengetter) will need to be replaced by an HTTPCaller using that new web connection. <br/>
> b. If the query string parameters configuration - [ see below](https://github.com/salvaleonrp/di-utility-network-export-subnetwork-by-rest/blob/main/Export%20Subnetwork%20only/ExportSubnetworkOnly.md#query-string-parameters) - of this solution is sufficient for your destination data, there is no further configuration needed.<br/>

Optional:
4. Reconfigure the following Query String parameters of the Export Subnetwork HTTPCaller below <br/>
![Query String Parameters of Export Subnetwork][HTTPCaller query string] <br/>

using the GP tool pane as reference, below.<br/>
![Export Subnetwork GP pane populated][ExportSub GP pane]<br/>



## Export Subnetwork HTTPCaller Configuration

The current solution configuration are below:

Request URL: $(HostUrl)/server/rest/services/NapervilleElectric31_SQLServer/UtilityNetworkServer/exportSubnetwork
HTTP Method: Get
JSON Result output: _serverResponse

### Query String Parameters
[Rest API parameter](https://developers.arcgis.com/rest/services-reference/enterprise/exportsubnetwork-utility-network-server-.htm) | [GP Pane parameter](https://pro.arcgis.com/en/pro-app/latest/tool-reference/utility-networks/export-subnetwork.htm) | [Workbench app parameter value](http://docs.safe.com/fme/2017.1/html/FME_Desktop_Documentation/FME_Workbench/Workbench/published_private_parameters.htm) [^1]
--- | --- | ---
token|  |	@Value(token)
subnetworkName| Subnetwork Name| ${SubnetworkName}
f | |_pjson_
gdbVersion | | (default)
sessionId | | (default)
moment | | (default)
domanNetworkName| Domain Network | _Electric_
tierName | Tier |_Electric Distribution_
exportAcknowledgement| Set export acknowledged | (default)

The next two are also for the Query string parameters and there are no exact equivalent to the GP pane as they are a collection of the GP tool parameters implemented in the REST API. 

### traceConfiguration

```
{
	"includeContainers": true,
	"includeContent": true,
	"includeStructures": true,
	"includeBarriers": true,
	"validateConsistency": true,
	"validateLocatability": true,
	"includeIsolated": false,
	"ignoreBarriersAtStartingPoints": false,
	"includeUpToFirstSpatialContainer": false,
	"allowIndeterminateFlow": true,
	"domainNetworkName": "",
	"tierName": "",
	"targetTierName": "",
	"subnetworkName": "",
	"diagramTemplateName": "",
	"shortestPathNetworkAttributeName": "",
	"filterBitsetNetworkAttributeName": "",
	"traversabilityScope": "junctionsAndEdges",
	"conditionBarriers": [],
	"functionBarriers": [],
	"arcadeExpressionBarrier": "",
	"filterBarriers": [],
	"filterFunctionBarriers": [],
	"filterScope": "junctionsAndEdges",
	"functions": [],
	"nearestNeighbor": {
		"count": -1,
		"costNetworkAttributeName": "",
		"nearestCategories": [],
		"nearestAssets": []
	},
	"outputFilters": [],
	"outputConditions": [],
	"propagators": []
}
```
### resultTypes

```
[
	{
		"type": "features",
		"includeGeometry": true,
		"includeDomainDescriptions": true,
		"includePropagatedValues": false,
		"networkAttributeNames": [
			"Asset type",
			"Available Duct Capacity",
			"Assembly Asset Group",
			"Asset group",
			"Ducts Available",
		],
		"diagramTemplateName": "",
		"resultTypeFields": [
			{
				"networkSourceId": 11,
				"fieldName": "devicestatus"
			},
			{
				"networkSourceId": 9,
				"fieldName": "normaldevicestatus"
			},
			{
				"networkSourceId": 15,
				"fieldName": "phasescurrent"
			},
			{
				"networkSourceId": 12,
				"fieldName": "manufacturer"
			},
			{
				"networkSourceId": 14,
				"fieldName": "phasescurrent"
			},
			{
				"networkSourceId": 10,
				"fieldName": "sharedneutral"
			},
			{
				"networkSourceId": 6,
				"fieldName": "addcount"
			},
			{
				"networkSourceId": 8,
				"fieldName": "ductavailable"
			},
			{
				"networkSourceId": 4,
				"fieldName": "highvoltagerisercount"
			},
			{
				"networkSourceId": 7,
				"fieldName": "installdate"
			},
			{
				"networkSourceId": 5,
				"fieldName": "diameterwidth"
			},
			{
				"networkSourceId": 11,
				"fieldName": "SUPPORTEDSUBNETWORKNAME"
			},
			{
				"networkSourceId": 9,
				"fieldName": "loadtapchangepercent"
			},
			{
				"networkSourceId": 15,
				"fieldName": "phasesenergized"
			},
			{
				"networkSourceId": 12,
				"fieldName": "maxvoltage"
			},
			{
				"networkSourceId": 14,
				"fieldName": "TERMINALCONFIGURATION"
			},
			{
				"networkSourceId": 10,
				"fieldName": "measuredlength"
			},
			{
				"networkSourceId": 6,
				"fieldName": "materialcode"
			},
			{
				"networkSourceId": 8,
				"fieldName": "availablecapacity"
			},
			{
				"networkSourceId": 4,
				"fieldName": "materialcode"
			},
			{
				"networkSourceId": 7,
				"fieldName": "lifecyclestatus"
			},
			{
				"networkSourceId": 5,
				"fieldName": "materialsoil"
			},
			{
				"networkSourceId": 11,
				"fieldName": "lifecyclestatus"
			},
			{
				"networkSourceId": 9,
				"fieldName": "manufacturer"
			},
			{
				"networkSourceId": 15,
				"fieldName": "phasesnormal"
			},
			{
				"networkSourceId": 12,
				"fieldName": "numphasesconstructed"
			},
			{
				"networkSourceId": 14,
				"fieldName": "phasessubstituted"
			},
			{
				"networkSourceId": 10,
				"fieldName": "commonconductortype"
			},
			{
				"networkSourceId": 6,
				"fieldName": "inservicedate"
			},
			{
				"networkSourceId": 8,
				"fieldName": "assetid"
			},
			{
				"networkSourceId": 4,
				"fieldName": "foundationtype"
			},
			{
				"networkSourceId": 7,
				"fieldName": "wallid"
			},
			{
				"networkSourceId": 5,
				"fieldName": "distance"
			}
		]
	},
	{
		"type": "connectivity",
		"includeGeometry": true,
		"includeDomainDescriptions": true,
		"includePropagatedValues": false,
		"networkAttributeNames": [],
		"diagramTemplateName": "",
		"resultTypeFields": []
	},
	{
		"type": "associations",
		"includeGeometry": true,
		"includeDomainDescriptions": true,
		"includePropagatedValues": false,
		"networkAttributeNames": [],
		"diagramTemplateName": "",
		"resultTypeFields": []
	}
]

```

## Suggestions for configuring ExportSubnetwork HttpCaller
1. Start with Pro, and configure the GP tool to your expected output.
2. Before you run the GP tool, setup Fiddler or Postman to capture the web traffic between Pro and the ArcGIS Server hosting your utility network.
3. Run the tool and capture the Export subnetwork configuration and the output JSON from your capturing tool. 
4. Use both JSONs to configure in your own settings.


[^1]: _itals_ is alphanumeric, @value() is an attribute value from a feature in the data stream, ${} is a user parameter value configured at run time.

[HTTPCaller query string]: ./httpcallerquerystring.png
[ExportSub GP pane]: ./exportSubnetworkGpTool.png
