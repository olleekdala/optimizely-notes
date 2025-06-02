#Devs #ModuleB 
Content Properties are used to store and present data
Properties can be defined **Code First**

There are two types of properties:
- Built-in or Inherited properties
	- Name, ContentLink, StartPublish etc
- Custom properties
	- If added from Admin view, these can be removed.
	- If added code first, the admin view can't remove them.

### Convention
![[Pasted image 20250602145115.png]]

### Debugging
Something useful for debugging the properties of a content type is the Property property on the type.
Property is a collection of PropertyData, so it can be iterated over to display information, for example listing all properties in a table with a foreach loop
```c#
@foreach(PropertyData property in Model.Property) 
{
	@property.Name
	@property.Value
```
