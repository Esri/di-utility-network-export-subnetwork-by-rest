# export-subnetwork-plus-customer-fields
 
This is a more complex solution that merges the JSON return of the Export Subnetwork REST api with the feature layers of your utility network. Most integrations with the utility network with 3rd party applications rely on other customer fields that are stored in the attribute table of each feature layer participating in the dataset.

While Export Subnetwork Rest API has a configurable ```resultTypeFields``` array in the ```resultTypes``` parameter that would export the fields, it is very tedious to configure and would need more JSON parsing in the solution. The [first solution illustrates the sample configuration and how these json is configured and parsed in the workspace](.\Export%20Subnetwork%20only\readme.md).

There are two options to add this to the solution. 

The ideal option is to query the features of your network dataset using the globalid of the features returned by the Export Subnetwork REST API so you can merge their attributes into your data stream. 

If your network dataset is small enough,  the second option is to read the whole network dataset and let the solution filter out the merged features into the solution. Since my sample is fairly small and simple with eight circuits, I'll use the second option for this advanced solution. This option will be not ideal for medium to large datasets.

## Instructions
1. Fork and then clone the repo. 
> [!NOTE]
> If you do not intend to contribute to this repo, you can just download the workspace template (fmwt) file.
2. Unzip to your desired destination and open the ExportSubnetworkV6Advanced.fmwt FME workspace template (fmwt) file using Data Interoperability workbench app. You can also double-click to open.

> [!NOTE]
> The solution is meant as a guide. The provided workspace will not run without configuring your own enterprise utility network dataset correctly. The token getter is configured to work with Basic authentication using the UN owner account username and password. If you use OAUTH2 or other authentication types for your dataset, a web service and a web connection must be created in the Workbench app. The [ESRIPortalTokenGetter](https://hub.safe.com/publishers/bruceharold/transformers/esriportaltokengetter) will need to be replaced by an HTTPCaller using that new web connection. 

3. Re-configure the workspace to your own utility network. 
> [!IMPORTANT]
> If the query string parameters of the Export Subnetwork is configured sufficiently for the destination data, there is no further configuration needed.<br/>

4. To visualize the solution easier in full extent, dynamic schemas were used for the outputs. You can opt to replace dynamic workflow with transformers that you can manage the schema and destination formats in a more deliberate way.
> [!IMPORTANT]
> No attempts Were made to clean up attributes for the destination formats, except for the following:<br/>
>   - removed attributes that have more than 31 characters (limitation of mobile gdb)<br/>
>   - removed duplicate attributes that caused errors when writing.<br/>
>   - attribute values of shapefiles were left unpopulated when field names are truncated to the limit of nine characters.<br/>




