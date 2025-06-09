#Devs #ModuleA

There are six permissions a role can have
- Read
- Create
	- Does not give the right to create the content type it is set for. More accurately it gives the right to **create children** for that content type.
- Change
- Delete
- Publish
- Administer

Access rights can be set for
- Content Items
- Content Types (create only)
- Permissions for Functions
- Languages (Create and change)
And can be assigned to
- Users (but don't)
- Groups (including virtual roles)
- Visitor Groups (but only read access)

Permissions for **Content Types** are not set under the setting page **Set Access Rights** but instead under the specific type in **Content Types**. This permission will grant the group the right to create this content type.

The same for Permissions for Functions and Languages.
Course material mentions that Languages are Change only, however the admin view in the recent version appears to allow both Create and Change, although because the access right is set per Language, and that Language must already be created to set access rights on it, it effectively means Change only.

# Code first

You can set roles code first by using the decorator
```
[Access(Roles = "NewsEditors")]
public class NewsPage : StandardPage 
{
```
Roles can be a comma separated string with multiple roles.
Then under `appsettings.json` you map this role to a **Virtual Role**.

This sets the access level on the News Page **Content Type** to NewsEditors. 
***This is covered in Exercise A2, starting from page 29 the exercise book***