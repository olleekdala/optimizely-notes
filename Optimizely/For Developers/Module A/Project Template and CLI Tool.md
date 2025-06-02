#Devs #ModuleA 
## Templates and Demo project

To find installed templates for Optimizely:
`dotnet new list opti`

If you haven't installed any templates you wouldn't see anything in the result. If so you can add the Optimizely templates by running this command
`dotnet new install EPiServer.Templates`

Generate a new project from template using
`dotnet new <template-name>`

In the course we will set up using the template  `epi-alloy-mvc`
It will generate a project and by default the name of the project will be the same as the directory it was created in.

Now you can run `dotnet run` to  build and start the server.
It will start listening on `localhost:5000`
When you first visit the page it will prompt you to create an admin user.

After the admin user is created and logged in, you have access to the [[Editing Interface]] by clicking the blue edit button in the top right.

Any CMS template includes the path to the editor interface by `/episerver/cms` 
If the empty template is used and there is no front page, you would still be able to access the admin/editing interface using this endpoint.
### Optimizely CLI tool
`dotnet tool install EPiServer.Net.Cli --global --add-source https://nuget.optimizely.com/feed/packages.svc/`
`dotnet tool list -g`


# Project Structure
When building the template project locally, you will have this structure.
Note that **you are expected to change the database and blob locations for any production environment**.

- **App_Data**: Contains the database `<ProjectName>.mdf` storing content. **blobs** subdirectory stores media assets.
- **bin**: .NET, CMS and dependency assemblies
- **Business, Extensions and Helpers**: Business logic, framework components, extension methods.
- **Models**: C# classes that represent content in the CMS database
- **Components, Controllers and Views**: provide content templates.
- **wwwroot**: images, styles (CSS) and scripts
- **modules**: shell modules and any add-ons you install
- **Resources/Translations**: XML files to localize the CMS and the visitor site UI
- **ClientResources**: files required in the browser for extended features

### Feature Folders
The default structure of a ModelViewController project is not always prefereable because it only separates by technical concerns.

Instead we could separate them by feature, to make the developer experience better and maintenance easier.

For example there is a feature concerning search in the Alloy template project.
By default it is separated into the MVC directories as such:

Controllers
	SearchPageController.cs
Views
	SearchPage
		Index.cshtml
Models
	Pages
		SearchPage.cs
		ISearchPage.cs

Instead we could group them by their feature in a **Features** folder

Features
	Search
		SearchPageController.cs
		Index.cshtml
		SearchPage.cs
		ISearchPage.cs

Making this refactoring could require additional changes, for example for the Controller to return the correct view you would modify the code slightly:

`SearchPageController.cs`
In the `Index`method you would alter the return statement from
`return View(model);`
to
`return View("Features/Search/Index.cshtml", model);`


# Frontend Frameworks
The Alloy template uses Bootstrap to handle responsive design.
The course will use Bootstrap for the training site as well, however you can use **any modern frontend framework** such as React, Angular or Vue.
CMS also supports SPA frameworks during On-Page Editing

