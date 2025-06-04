#Devs #ModuleB 
Simplest validation method is by decorating any properties using Microsofts validation attributes.
You can also create a custom attribute by inheriting the **ValidationAttribute**, and overriding the `IsValid` method, and decorating the class with your new custom attribute.

```c#
public class OperaYear : ValidationAttribute
{
	public override bool IsValid(object value)
	{
		if (!(value is int)) return false;
		return ((int)value) > 1597;
	}
}

// Using the attribute on a property
[OperaYear]
public virtual int OperaWritten { get; set; }
```
### Optimizely Validator
Optimizely comes with its own validator that you can customize for any content type.

```c#
using EPiServer.Validation;

public class EmployeePageValidator : IValidate<EmployeePage>
{
	public IEnumerable<ValidationError> Validate(EmployeePage instance)
	{
		if (instance.HireDate < instance.BirthDate)
		{
			yield return new ValidationError
			{
				PropertyName = "HireDate",
				ErrorMessage = "An employee cannot be hierd before they are born!",
				Severity = ValidationErrorSeverity.Warning,
				RelatedProperties = new[] { "BirthDate" }
			};
```
Following the demonstration, I have added a validator for ProductPage, when I create a new ProductPage and break the rules for validation I get this result:
![[Pasted image 20250604090249.png]]

These have the **Warning** and **Info** severity levels respectively, which does not prevent you from publishing the page. If you wish to prevent publishing if validation is broken, use **Error** as the severity level. It appears as a red message:
![[Pasted image 20250604090415.png]]

*Demo note: If you're following the video demonstrations, he swaps back to the AlloyDemo site instead of the AlloyTraining project. If you wish to complete this demonstration in the AlloyTraining project, you have to add these pages to your models:*
`StandardPage.cs`
```c#
using System.ComponentModel.DataAnnotations;
namespace AlloyTraining.Models.Pages
{
    [ContentType(DisplayName = "Standard",
        GroupName = SiteGroupNames.Common,
        Description = "Use this page type unless you need a more specialized one.")]
    [AvailableContentTypes(Include = new[] { typeof(StandardPage) },
        Exclude = new[] { typeof(ProductPage) })]
    public class StandardPage : PageData
    {
        [CultureSpecific]
        [Display(Name = "Main body",
            Description = "The main body will be shown in the main content area of the page, using the XHTML-editor you can insert for example text, images and tables.",
            GroupName = SystemTabNames.Content,
            Order = 150)]
        public virtual XhtmlString MainBody { get; set; }
    }
}
```
`ProductPage.cs`
```c#
using System.ComponentModel.DataAnnotations;
namespace AlloyTraining.Models.Pages
{
    [ContentType(DisplayName = "Product",
        GroupName = SiteGroupNames.Specialized, Order = 20,
        Description = "Use this for software products that Alloy sells.")]
    public class ProductPage : StandardPage
    {
        [CultureSpecific]
        [Display(Name = "Unique selling points",
            GroupName = SystemTabNames.Content, Order = 320)]
        [Required]
        public virtual IList<string> UniqueSellingPoints { get; set; }
    }
}
```
# Events (covered again later)
![[Pasted image 20250604091028.png]]