#Devs #ModuleB 

To restrict which pages could be created as children of other pages, you can either change settings in the Admin view, or by adding the **AvailableContentTypes** attribute and setting **Include** or **IncludeOn** on a page type.

In the AlloyTraining demo, we've set the attribute on the **StartPage**:
```c#
[AvailableContentTypes(Include = new[] { typeof(StandardPage)})]
```
This means that only children of the StandardPage page type can be created under StartPage.

If you do not have access to the definition of a page type, you could use the **IncludeOn** parameter for AvailableContentTypes.
For example you have PageA that you can't alter the available content types on, but you need PageB to be included as possible children for PageA, and you have access to the PageB definition.
Then you can set available content types on PageB like so:
```c#
[AvailableContentTypes(IncludeOn = new[] { typeof(PageA) })]
public class PageB : PageData
```
This means the parents of PageB are allowed to be of type PageA.

**Exclude** and **ExcludeOn** are the reverse operation of the above. It also overrides any **Include**.