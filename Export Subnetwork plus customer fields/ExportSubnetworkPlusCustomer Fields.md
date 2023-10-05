# export-subnetwork-plus-customer-fields
 
This is a more complex solution that merges the JSON return of the Export Subnetwork REST api with the feature layers of your utility network. Most integrations with the utility network with 3rd party applications rely on other customer fields that are stored in the attribute table of each feature layer participating in the dataset.

While Export Subnetwork Rest API has a configurable ```resultTypeFields``` array in the ```resultTypes``` parameter that would export the fields, it is very tedious to configure and would still require domain descriptions to be pulled from the feature service properties. 

There are two options to add this in the solution. 

The ideal option is to query the features of your network dataset using the globalid of the features returned by the Export Subnetwork REST API so you can merge their attributes into the your data stream. 

If your network dataset is small enough,  the second option is to read the whole network dataset and let the solution filter out the merged features into the solution. Since my sample is fairly small and simple with eight circuits, I'll use the second option for this advanced solution.

## Instructions
1. Fork and then clone the repo. 
> [!NOTE]
> If you do not intend to contribute to this repo, you can just download the workspace template (fmwt) file.
2. Unzip to your desired destination and open the ExportSubnetworkV6Advanced.fmwt FME workspace template (fmwt) file using Data Interoperability workbench app. You can also double-click to open.

> [!NOTE]
> The solution is meant as a guide. The provided workspace will not run without configuring your own enterprise utility network dataset correctly. The token getter is configured to work with Basic authentication using the UN owner account username and password. If you use OAUTH2 or other authentication types for your dataset, a web service and a web connection must be created in the Workbench app. The [ESRIOnlineTokenGetter](https://hub.safe.com/publishers/bruceharold/transformers/esrionlinetokengetter) will need to be replaced by an HTTPCaller using that new web connection. 
3. Re-configure the workspace to your own utility network. 
> [!IMPORTANT]
> If the query string parameters of the Export Subnetwork is configured sufficiently for the destination data, there is no further configuration needed.<br/>

Optional:
4. Reconfigure the following Query String parameters of the Export Subnetwork HTTPCaller below <br/>
![Query String Parameters of Export Subnetwork][HTTPCaller query string] <br/>

using the GP tool pane as reference, below.<br/>
![Export Subnetwork GP pane populated][ExportSub GP pane]<br/>



## Export Subnetwork HTTPCaller Configuration

The current solution configuration are below:

## Suggestions for configuring ExportSubnetwork
5. Configure the Export Subnetwork rest API http caller to your desired tool parameters. Start with Pro, configure the GP tool, then run. Capture the paramteres using atool like Fiddler or Postman.


[HTTPCaller query string]: /image.png
[ExportSub GP pane]: /image-1.png
