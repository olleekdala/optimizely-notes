Most of the settings you can configure in code for a property are for changing how it behaves and appears in the editing interface.

There are a few decorators that are useful to know
- Required
- Searchable includes the property value in the indexes
- CultureSpecific enables multiple languages
- ScaffoldColumn(false) hides the property from the editing interface
- Editable(false) makes the property readonly in the editing interface
- Display
	- Name
	- Description
	- GroupName
	- Order
	- And more

**GroupName and Order** are related settings. GroupName is a sort of category for where that content type appears in the editing interface when creating a new piece of content.
Order in this context is where in that group the item appears.
You can create custom groups by creating a static class with string constants as group names.

Adding the `[GroupDefinitions]` lets you enhance the tab structure by ordering the groups just as you would the Content Type itself, and also set specific access rights for a group name.
```c#
[GroupDefinitions]
public static class SiteTabNames
{
	[Display(Order = 10)]
	[RequiredAccess(AccessLevel.Publish)]
	public const string Contact = "Contact Info";
}
```
This example shows the static class with string constants, where a order has been set on the property, and a specific access level is required to see this group.
You would then use this class to set the GroupName for content types
```c#
[Display(GroupName = SiteTabNames.Contact)]
public virtual string Phone { get; set; }
```


