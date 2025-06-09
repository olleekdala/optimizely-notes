#Devs #ModuleF 
### Programmatically creating a new page
You need access to the `IContentRepository` object to do this
```c#
private readonly IContentRepository repo;

// Create a new page and set its parent.
// Note that GetDefault creates a new instance.
ProductPage page = repo.GetDefault<ProductPage>(parentLink: PageReference.StartPage)

// Set page properties
page.Name = "Alloy go"; // IContent.Name
page.MainBody = new XhtmlString("<p>This is produced programmatically</p>");

// Save the page and access levels.
ContentReference newPageLink = repo.Save(
	page,
	EPiServer.DataAccess.SaveAction.Publish,
	EPiServer.Security.AccessLevel.NoAccess
);
```
### Updating an existing page
Again we need the `IContentRepository`
```c#
ContentReference pageLink = ...;
// Objects from Get are readonly, so we call CreateWriteableClone to be able to make changes to the object.
ProductPage page = repo.Get<PageData>(pageLink).CreateWriteableClone() as ProductPage;

if (page != null) 
{
	page.MainBody = new XhtmlString("<p>Updated programmatically!</p>");
	ContentReference updatedPageLink = repo.Save(
		page,
		EPiServer.DataAccess.SaveAction.CheckIn, // Ready to publish
		EPiServer.Security.AccessLevel.Edit // Whoever executes this needs minimum edit access rights.
	);
}
```
### Creating a new shared block
This is similar to creating a page, except that BlockData does not implement IContent, so we must cast it to IContent before setting properties like Name and calling the Save method.

```c#
// Most code before this is just like when creating a page
// Before setting Name and Saving, cast to IContent.
var content = newBlock as IContent;
content.Name = "Alloy Go Launch";
ContentReference newBlockLink = repo.Save(content, SaveAction.Publish, AccessLevel.NoAccess);
```
### Updating existing block
Similar again to updating a page.
```c#
// Unless we need to update the name, we don't have to cast to IContent until in the Save method.
// Updating a block in this case is exactly the same as updating a page with the small change in the Save method:
ContentReference updatedBlockLink = repo.Save(
	(IContent)updateBlock,
	SaveAction.CheckOut,
	AccessLevel.Edit
);
```
### Deleting content
This is a way to 'hard' delete content. `forceDelete` ignores references to content.
```c#
repo.Delete(contentReference, forceDelete: true, access: AccessLevel.NoAccess)
```

For a soft delete, i.e. moving it to the Trash.
```c#
repo.MoveToWastebasket(contentReference);
// Or
repo.Move(
	contentReference,
	destination: ContentReference.WasteBasket,
	requiredSourceAccess: AccessLevel.NoAccess,
	requiredDestinationAccess: AccessLevel.NoAccess
);
```