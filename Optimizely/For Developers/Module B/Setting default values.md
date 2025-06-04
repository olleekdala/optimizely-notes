#Devs #ModuleB 

Admins can set default values for pages through the admin view.
Developers can set the same default values code first.

To do this you would override the `SetDefaultValues` method on the Content Type.
```c#
[ContentType]
public class NewsPage : PageData
{
	public virtual string Heading { get; set; }
	public override void SetDefaultValue(ContentType contentType)
	{
		VisibleInMenu = false; // setting built-in properties
		StopPublish = DateTime.Now.AddDays(45);
		this[MetaDataProperties.PageChildOrderRule] = Filters.FilterSortOrder.Index;
		Heading = "Welcome!" // setting custom properties
	
		// applies defaults from Admin view
		base.SetDefaultValues(contentType);
	}
```