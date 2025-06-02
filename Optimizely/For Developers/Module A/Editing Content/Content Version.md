#Editor #Devs #ModuleA 

Pages are automatically versioned when Editors make changes and publish content.
The maximum number of stored versions can be configured in the `appsettings.json` file
```
"EPiServer": {
	"Cms": {
		"Content": {
			"MaximumVersions": "20",
```
0 would mean unlimited page versions will be kept. 
20 is default.


