#Devs #Editor
For the demo site, install `EPiServer.Personalization.MaxMindGeolocation`
Next copy the GeoLite2 folder from the exercise files in Module A, to the App_Data folder in the demo project.

Then in `Startup.cs` add the following
```
services.AddMaxMindGeolocationProvider(options =>
{
	options.DatabasePath = @"<YourProjectPath>\App_Data\GeoLite2\GeoLite2-City.mmdb";
	options.LocationsDatabasePath = @"<YourProjectPath>\App_Data\GeoLite2\GeoLite2-City-Locations-en.csv";
});
```
This will add geolocation criteria when customizing an Audience with new criterion.
For example we can add an Audience that consists of visitors from Sweden, that visits the site on the weekend.

Go into **Audiences** in the editing interface and add a new one called "Swedish Weekenders".
You can now add a new criteria for **Geographic Location** and select Europe + Sweden.
Also add a criteria for **Time of Day** and select Saturday and Sunday checkboxes.

Audiences are covered in the [[Audiences]] section of **CMS Usage**, a separate course that covers the same concepts, slightly updated.