# di-utility-network-export-subnetwork-by-rest
 
This repo provides a no-code solution using ArcGIS Data Interoperability for ArcGIS Pro to automate Exporting Subnetwork for a Utility Network dataset published on an ArcGIS Enterprise platform on the most current UN version.

The original source of this no-code solution was first published in ArcGis Blog in the two-part blog series written by Jon De Rose and Renato Salvaleon. 

Leveraging Data for External Systems - Automating Export Subnetwork using Data Interoperability<br/>
[Part One ](https://www.esri.com/arcgis-blog/products/utility-network/data-management/exporting-subnetworks-using-data-interoperability/)<br/>
[Part Two ](https://www.esri.com/arcgis-blog/products/utility-network/data-management/exporting-subnetworks-using-data-interoperability-part2/)<br/>

You can still find the blog's workspace solution [from part two of the blog](https://community.esri.com/t5/arcgis-utility-network-documents/sample-workbench-file-leveraging-data-for-external/ta-p/1053123) or in this repo's [UNv3 release page.](https://github.com/salvaleonrp/di-utility-network-export-subnetwork-by-rest/releases/tag/v2.6.0)

## Features
Converts JSON result of an export subnetwork REST API call to the following outputs: Mobile GDB, File GDB, CAD and shapefile.

## Limitations
1. Utility Networks that are stored in file geodatabase or mobile geodatabases are out of scope.
2. No filters or validation were made for Subnetworks where ```ISDIRTY = 1```. If an attempt was made to export a dirty subnetwork, the JSON return on the Export Subnetwork HTTPCaller will return the following error code and message:
 ```
  "extendedCode": -2147208457, "message": "Dirty subnetwork cannot be exported.",
 ```

## Solutions
1. [Export Subnetwork only](https://github.com/ArcGIS/di-utility-network-export-subnetwork-by-rest/blob/main/Export%20Subnetwork%20only/ExportSubnetworkV6.fmwt) 
2. [Export Subnetwork plus customer fields](https://github.com/ArcGIS/di-utility-network-export-subnetwork-by-rest/blob/main/Export%20Subnetwork%20plus%20customer%20fields/ExportSubnetworkV6Advanced.fmwt)
3. [Helper workspace template](ListSubnetworksServer.fmwt) to use for populating your user parameters for Domain network, Tier name, Subnetwork name. The helper list will also generate a list of subnetwork to use for automating Export Subnetwork for your entire utility network dataset. 

> [!NOTE] 
>The helper solution uses the ArcGIS Server feature service reader format which is new to Pro 3.1. The advantage of using this format is there is no JSON to parse and no max record counts and paging to consider. For earlier versions of Pro use the HTTPCaller configuring the query rest endpoint of the ```Layer: Subnetworks (ID: 500002)```. 

## Instructions
Solutions 1 and 2 will have instructions in their respective readme.md file. For the helper file, there is an annotation on the worksapce canvass to follow.


## Requirements
* Data Interoperability for ArcGIS Pro 3.1 or higher
* ArcGIS Pro 3.1 or  higher
* Enterprise Utility Network with a schema of UNv6 or higher

## Suggestions for modifying the solutions
1. Enable both the Feature Cache and Feature Counts tools while authoring. 
2. Test small, test often at the beginning. Start with the reader first.
3. Use the Play buttons on the canvass object as you tweak the existing solution,  until you get to your destination datasets.
4. When configuring your own utlity network for this solution, leave the existing format reader on the canvas and use the Add reader tool. After the schema hydrates connect to the existing transformer from which the original reader is connected to. Once the new feature types is connected to the transformer, you can delete the original reader from the navigation pane.
5. When you are satisfied with the state of your solution, you can disable both Feature Cache and Feature Counts. 
6. If you are reauthoring your solution to have multiple outputs, test the solution one output format at a time. 


## Resources
Below are links to essential references used in the blogs.

Utility Network docs:<br/>
* [Export Subnetworks (Doc)](https://pro.arcgis.com/en/pro-app/latest/help/data/utility-network/export-subnetworks.htm)<br/>
* [Trace (Doc)](https://pro.arcgis.com/en/pro-app/latest/help/data/utility-network/about-tracing-utility-networks.htm)<br/>
* [Utility Network Upgrade History (Doc)](https://pro.arcgis.com/en/pro-app/latest/help/data/utility-network/utility-network-upgrade-history.htm)<br/>
* [Export Subnetwork GP Tool (Doc)](https://pro.arcgis.com/en/pro-app/latest/tool-reference/utility-networks/export-subnetwork.htm)<br/>
* [Export Subnetwork Rest API (Doc)](https://developers.arcgis.com/rest/services-reference/enterprise/exportsubnetwork-utility-network-server-.htm)<br/>
* [Network Topology index (Pro SDK Doc)](https://github.com/esri/arcgis-pro-sdk/wiki/ProConcepts-Utility-Network#network-topology)<br/>
* [Tracing subset of the Utility Network (Pro SDK Doc)](https://github.com/esri/arcgis-pro-sdk/wiki/ProConcepts-Utility-Network#tracing)<br/>

Utility Network blogs (latest on top):<br/>

Name and Link | Pro/Enterprise Version | Date
--- | --- | ---
[Network Integrations](https://www.esri.com/arcgis-blog/products/utility-network/electric-gas/utility-network-journey-network-integrations/)| 3.1/11.1 |6/13/2023
[Parsing Utility Network JSON Files (Python)](https://community.esri.com/t5/arcgis-utility-network-documents/parsing-utility-network-json-files/ta-p/1314718/jump-to/first-unread-message)| 3.1/11.1 |8/31/2023
[Adding Description to Export Subnetwork JSON blog](https://community.esri.com/t5/arcgis-utility-network-questions/adding-descriptions-to-export-subnetwork-json/m-p/367933)| 2.4 |	3/10/2020
[Command line automation for Utility Network blog](https://www.esri.com/arcgis-blog/products/utility-network/administration/automating-utility-network-functions-using-command-line/)| 2.1/10.6	| 6/5/2018
[Web Trace tool Blog](https://www.esri.com/arcgis-blog/products/utility-network/data-management/a-technical-walk-through-for-a-simple-utility-network-web-trace-tool-with-javascript/) | 2.1/10.6 | 2/28/2018

Data Interoperability doc and related Automation blogs<br/>
* [Spatial ETL Tool (Doc)](https://pro.arcgis.com/en/pro-app/latest/help/data/data-interoperability/spatial-etl-tools.htm)
* [Automate yor ETL Processes blog](https://community.esri.com/t5/arcgis-data-interoperability-blog/automate-your-etl-processes-on-a-schedule-two-ways/ba-p/883616)<br/>
* [Ontario511](https://pm.maps.arcgis.com/home/item.html?id=4ec1d2420089451bb173e90ce01e2e0a)<br/>
* [Import Building GeoJSON](https://pm.maps.arcgis.com/home/item.html?id=9da0f8ae5fee45aca11bf77f712884c8)<br/>

JSON tutorial references:<br/>
* [Learn JSON](https://www.youtube.com/watch?v=iiADhChRriM)<br/>

## Issues

Find a bug or want to request a new feature?  Please let us know by submitting an issue.

## Contributing

Esri welcomes contributions from anyone and everyone. Please see our [guidelines for contributing](https://github.com/esri/contributing).

## Licensing
Copyright 2023 Esri

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

A copy of the license is available in the repository's [license.txt](https://github.com/salvaleonrp/di-data-driven-electric-utility-export-subnetwork/blob/main/license.txt) file.

[](Esri Tags: Data Interoperability for ArcGIS Pro)
[](Esri Tags: Utility Network)
