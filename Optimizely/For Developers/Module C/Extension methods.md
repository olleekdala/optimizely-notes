#Devs #ModuleC 
# Html
Methods we've already seen include **PropertyFor** and **EditAttributes**.

### Translate
Used to translate strings. 
Uses `LocalizationService` behind the scenes.
```c#
<p>
	@Html.Translate("/articlepagetemplate/published")
</p>
```
This looks up the XPath expression in the languages xml
`Resources\LanguageFiles\Views.xml`
```xml
<?xml version="1.0" encoding="utf-8" ?>
<languages>
	<language name="English" id="en">
		<articlepagetemplate>
			<published>Last updated</published>
```
And for the swedish translation you would have a swedish language tag. 
```xml
<language name="Svenska" id="sv">
	<articlepagetemplate>
		<published>Senast uppdaterad</published>
```

### Rendering hyperlinks and URLs for a content reference
For when you have a `ContentReference` property you can use:
```c#
@Html.ContentLink(referenceToVideo)
```
and this would render a hyperlink
```html
<a href="/siteassets/videos/contentapprovals.mpeg">contentapprovals.mpeg</a>
```
Only ContentReferences that can have a url works for this method such as Pages and Media assets. Folders or Blocks would not work. They would only output the name without a clickable link.

Since `ContentLink` always outputs the anchor tag, you might want to have a bit more control of the specific tag used for the content.
You can do this with `@Url.ContentUrl(referenceToVideo)` method
This outputs the relative site path to the content instead of an anchor tag, which means you can use it more flexibly:
```html
<video src="@Url.ContentUrl(referenceToVideo)" />
```
Translates to 
```html
<video src="/siteassets/videos/contentapprovals.mpeg" />
```

### Render content data
**`@Html.RenderContentData`**
Any content that implements `IContentData` can be used with this extension method.
It is used when you have a ContentReference you want to load the partial template of.

To do this you can't pass the ContentReference directly to the method, first you have to load the content from a loader.
```c#
@inject EPiServer.IContentLoader loader
@{
	IContentData content = loader.Get<IContentData>(referenceToVideo)
	Html.RenderContentData(content, isContentInContentArea: false);
}

```

# Writing your own extension methods for views
You can write your own methods, since writing multiple statements of code in views (.cshtml) can get messy, and extensions simplify the view code.

*Note that if your extension method needs to use the `ServiceLocator` you should avoid creating this extension method. Using the `ServiceLocator` is considered bad practice. Any work requiring a dependency service should be done in the Controller and pass the simple values to the view model.*

```c#
namespace AlloyTraining.Business.ExtensionMethods;
public static class ContentExtensions
{
	public static TContent Get<TContent>(this ContentReference contentLink) where TContent : IContent
	{
		var loader = ServiceLocator.Current.GetInstance<IContentLoader>();
		return loader.Get<TContent>(contentLink);
	}
}
```

