#ModuleB #Devs 

A Content Type is a class that inherits `IContent` or a base-class that implements `IContent`, and has the `[ContentType]` decorator.

The CMS has four main types built-in:
1. **Page**: an instance of a class that derives the `PageData` class.
2. **Folder**: instance of `ContentFolder` class.
3. **Media**: instance of any class that derives `MediaData` or the subclasses `ImageData` or `VideoData`
4. **Block**: instance of class that derives `BlockData`
	1. Forms use `FormContainerBase` which inherits `BlockData`, so forms are a special type of Block.


#### Content Reference Class
`ContentReference` is a reference to any piece of content, it has three properties to uniquely identify an item:
- ID : int
- WorkID : int
- ProviderName : string

Any new project will have at least four existing `ContentReference` instances before you add anything yourself.
The Root page, for all sites folder, and the wastebasket.

WorkID is like a version ID. It is a globally incrementing id, any changes to the content will increment the WorkID.

`IContent` has two link properties:
- `ContentLink`: A reference to itself
- `ParentLink`: A reference to its parent page/folder

`PageData` has additional link properties:
- `PageLink`: a page reference to itself (deprecated)
- `ArchiveLink`: a page reference to where to move when the page expires.

## Content Template Design
There are two extremes for content templates:
- **Many pages, no blocks**: This is a strict layout for when editors aren't completely trusted. You have the capability to set very strict access rights for content creation. Editors are probably only allowed to create a page and fill in simpler content areas based on the template. Each page template is a specific use and layout.
- **Few pages, many blocks**: Very flexible layout, few page templates with generic ContentArea to allow editors to add any combination of content.

You will most likely use a combination of both in the real world.

# Content Type Comparison
![[Pasted image 20250602102438.png]]
