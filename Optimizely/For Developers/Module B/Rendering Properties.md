#Devs #ModuleB 

Optimizely CMS uses Razor pages to render views.
In the previous section we used `@model` to bind a specific model to the view.

You can render parts of the model in different ways, some are built into dotnet, and some are by Optimizely.

To render a property as readonly, in the view access the property simply:
`@Model.MyProperty`
Since this is readonly, you will not be able to edit this property in the on-page editing interface. To allow that, you need to use the `PropertyFor` method by Optimizely.
`@Html.PropertyFor(m => m.MainBody)`

PropertyFor will wrap the content in a div. To add styling to this div you can pass an anonymous object to the method including things like CssClass and other values.
```
@Html.PropertyFor(m => m.MainContentArea, additionalViewData: new {
	CssClass = "row", Color = "pink"
})
```
The other methods of rendering data are available to enable the editing interface. For visitors, there is basically no difference between the methods as they will render everything as readonly.
- **DisplayFor**: Basically the same as rendering from the `@Model`
- **PropertyFor**: Wraps the data in a div containing special properties for the editing interface to work.
- **EditAttributes**: Used inside an html-tag to add special properties for the editing interface.
  Used together with **DisplayFor** to render the value inside the tag.

**EditAttributes** is notably used in the cases where **PropertyFor** is not good code, for example when wrapping the value in an h1 tag, having a div inside is bad. Since PropertyFor wraps the value in a div, this will produce invalid html.
Here we need to use EditAttributes.
```
<h1 @Html.EditAttributes(m => m.Heading)>
	@Html.DisplayFor(m => m.Heading)
</h1>
```

Another notable benefit of EditAttributes is allowing complex business logic when outputting values, for example if property is null, have fallback values: 
```
<h1 @Html.EditAttributes(m => m.Heading) >
    @(Model.Heading ?? Model.Name)
</h1>
```

