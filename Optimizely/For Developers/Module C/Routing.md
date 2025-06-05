#Devs #ModuleC 
# Simple Address
A simpler route for a page, shortcut.
### Redirect to Simple Address
```c#
public void ConfigureServices(IServiceCollection services)
{
	services.Configure<RoutingOptions>(options => 
	{
		options.PreferredUrlFormat = PreferredUrlFormat.Simple;
		options.PreferredUrlFormatRedirection = HttpRedirect.Permanent;
		// HttpRedirect: None, Temporary, Permanent
	})
}
```