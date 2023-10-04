# export-subnetwork-only
 
This solution uses the JSON return of the Export Subnetwork REST api and relies on its supported parameters only. These api parameters are configured in the solution, parameterized as Query String parameters of the HTTPCaller transformer.

## Instructions
1. Fork and then clone the repo. 
> [!NOTE]
> If you do not intend to contribute to this repo, you can just download the workspace tempalte (fmwt file).
2. Unzip to your desired destination and open the FME workspace template (fmwt) file using Data Interoperability workbench app. 
> [!NOTE]
> The solution is meant as a guide. The provided workspace will not run without configuring your own enterprise utility network dataset correctly. The token getter is configured to work with Basic authentication using the UN owner account username and password. If you use OAUTH2 or other authentication types for your dataset, a web connection must be created and the [ESRIOnlineTokenGetter](https://hub.safe.com/publishers/bruceharold/transformers/esrionlinetokengetter) will need to be replaced by an HTTPCaller using that new web connection. 
3. Re-configure the workspace to your own utility network. 
> [!IMPORTANT]
> If the query string parameters of the Export Subnetwork is configured sufficiently for the destination data, there is no further configuration needed.<br/>

Optional:
4. Reconfigure the following Query String parameters of the Export Subnetwork HTTPCaller below <br/>
![Query String Parameters of Export Subnetwork][HTTPCaller query string] <br/>

using the GP pane tool as reference, below.<br/>
![Export Subnetwork GP pane populated][ExportSub GP pane]<br/>



## Export Subnetwork HTTPCaller Configuration

The current solution configuration are below:

Request URL: $(HostUrl)/server/rest/services/NapervilleElectric31_SQLServer/UtilityNetworkServer/exportSubnetwork
HTTP Method: Get
JSON Result output: _serverResponse

### Query String Parameters
[Rest API parameters](https://developers.arcgis.com/rest/services-reference/enterprise/exportsubnetwork-utility-network-server-.htm) | [GP Pane parameters](https://pro.arcgis.com/en/pro-app/latest/tool-reference/utility-networks/export-subnetwork.htm) | [Workbench app User parameters](http://docs.safe.com/fme/2017.1/html/FME_Desktop_Documentation/FME_Workbench/Workbench/published_private_parameters.htm)
--- | --- | ---
token|  |	@Value(token)
subnetworkName| Subnetwork Name| ${SunetworkName}
f | |pjson
gdbVersion | | (default)
sessionId | | (default)
moment | | (default)
domanNetworkName| Domain Netowrk | Electric
tierName | Tier |Electric Distribution
exportAcknowledgement| Set export acknowledged | (default)

### traceConfiguration

```
{
	"includeContainers": true,
	"includeContent": true,
	"includeStructures": true,
	"includeBarriers": true,
	"validateConsistency": true,
	"includeIsolated": false,
	"ignoreBarriersAtStartingPoints": false,
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
    "includeDomainDescriptions" : true,
    "includePropagatedValues": false,
    "networkAttributeNames": [],
    "diagramTemplateName": "",
    "resultTypeFields": []
  },
  {
    "type": "connectivity",
    "includeGeometry": true,
    "includeDomainDescriptions" : true,
    "includePropagatedValues": false,
    "networkAttributeNames": [],
    "diagramTemplateName": "",
    "resultTypeFields": []
  },
  {
    "type": "associations",
    "includeGeometry": true,
    "includeDomainDescriptions" : true,
    "includePropagatedValues": false,
    "networkAttributeNames": [],
    "diagramTemplateName": "",
    "resultTypeFields": []
  }
]

```


## Suggestions for reconfiguring the solution
1. Enable both the Feature Cache and Feature Counts tools while authoring. When you are satisfied with the state of your solution, 
2. Test small, test often at the beginning. Start with the reader first.
3. Use the Play buttons on the canvass object as you tweak the existing solution.
4. Avoid Importing feature types on an existing format reader. Use Add reader format to add the first feature type/s. After the schema hydrates connect to the existing transformer from which the original reader is connected to. Once the new feature types is connected to the transformer, you can delete the original reader.
5. Configure the Export Subnetwork rest API http caller to your desired tool parameters. Start with Pro, configure the GP tool, then run. Capture the paramteres using atool like Fiddler or Postman.

[](Esri Tags: Data Interoperability for ArcGIS Pro)
[](Esri Tags: Utility Network)


[HTTPCaller query string]: image.png
[ExportSub GP pane]: image-1.png