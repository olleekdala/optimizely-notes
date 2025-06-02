#Devs #Editor  #ModuleA 
![[Pasted image 20250530114407.png]]![[Pasted image 20250530114441.png]]
![[Pasted image 20250530114544.png]]

In the demo we add the following code to `Startup.cs`
```
services.Configure<TinyMceConfiguration>(config =>
{
	TinyMceSettings defaultSettings = config.Default();

	TinyMceSettings mainBodyStandardPageSettings = config.For<StandardPage>(page
	=> page.MainBody);
	
	mainBodyStandardPageSettings.AddPlugin("code");
	mainBodyStandardPageSettings.AppendToolbar("code");
});
```
`mainBodyStandardPageSettings` is using the For<> method to specify which content type it is configuring for. We add the code plugin and append it to the toolbar. 

If we wanted to replace the entire toolbar with only the code plugin, we would set it using `Toolbar` method.
Replace `AppendToolbar` with `Toolbar`
`mainBodyStandardPageSettings.Toolbar("code");`

You can also customize the toolbar
`mainBodyStandardPageSettings.Toolbar("bold epi-link | code");`
This for example adds the bold formatting option, inserting a link, and a divider followed by source code viewer.

In AlloyDemo, the About Us page is an instance of StandardPage if you want to verify these changes works in the demo.

`defaultSettings` applies to any other rich text editor toolbar.