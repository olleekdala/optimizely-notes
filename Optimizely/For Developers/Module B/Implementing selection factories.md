#Devs #ModuleB 

To describe a selection factory, the simplest example is to use a custom string property on a content type.
```c#
[Display(Name = "Work status")]
public virtual string WorkStatus { get; set; }
```
This will by default produce a single line text box in the editing interface.
To customize this, we use Selection Factories to change it into for example a dropdown list, or multiple checkboxes.

To implement your own selection factory:
```c#
public class WorkStatusSelectionFactory : ISelectionFactory
{
	public IEnumerable<ISelectItem> GetSelection(ExtendedMetadata metadata)
	{
		yield return new SelectItem { Value = "FT", Text = "Full-time" };
		yield return new SelectItem { Value = "PT", Text = "Part-time" };
		yield return new SelectItem { Value = "ST", Text = "Student" };
		yield return new SelectItem { Value = "UN", Text = "Unemployed" };
	}
}
```
With this selection factory, we can now decorate the string property

```c#
[SelectOne(SelectionFactoryType = typeof(WorkStatusSelectionFactory))]
public virtual string WorkStatus { get; set; }
```
**SelectOne** is for a dropdown list, **SelectMany** is for multiple checkboxes.
The string property would store either the single value, or a comma-separated string if SelectMany is used.

The **GetSelection** method can include more complicated logic, for example if it has a dependency on some other property being set.
In this case you need the page to refresh when a property is selected.

Say we have a `bool` property:
```c#
[ReloadOnChange]
public virtual bool IncludeExtendedItems { get; set; }
```
I have decorated this property with the **ReloadOnChange** attribute, which refreshes the editing context when the property is changed.

```c#
public class WorkStatusSelectionFactory : ISelectionFactory
{
	public IEnumerable<ISelectItem> GetSelection(ExtendedMetadata metadata)
	{
		IContent content = metadata.FindOwnerContent();
		PropertyData property = content?.Property[nameof(PersonPage.IncludeExtendedItems)];
		if (property?.Value != null && (bool)property.Value)
		{
			// yield selections...
		}
```