#Devs #ModuleB 

Creating a new Page content type with the CLI
*The project name is AlloyTraining, we created a new empty project without any pages, name the first page StartPage.
The demonstration video says to use the -na tag for namespace, however it seems newer versions of the cli tool has altered this to -p:na or --namespace*

`dotnet new epi-cms-contenttype --namespace AlloyTraining.Models.Pages --name StartPage`
or
`dotnet new epi-cms-contenttype -p:na AlloyTraining.Models.Pages --name StartPage`

In the `ContentType` decorator, we can add more options like
- `GroupName` will place the page template within a group in the editing interface.
- `Order` determines where in the group the page template is located, its ordering rank.

In the `Display` decorator on a property of the content type, you can also add a `Prompt` option.
This will render a prompt in the editing interface.

You can add custom properties to a Content Type, however all custom properties must be `public virtual`.


When you then go to the editing interface to add this new StartPage content to your website, you will notice that you don't get the option to select the content type, this is because there is only one content type to choose from and it will default to the only available type.

## Create page template
We create a new controller using the CLI
Following the demonstration, create a new folder in the project called `Controllers` and open in terminal.
Just as with the Content Type cli command, this is also using the updated namespace tags.
`dotnet new epi-cms-pagecontroller -p:na AlloyTraining.Controllers -ct StartPage --name StartPageController`

`-ct StartPage` selects the Content Type used for the controller.


## Create View
Add a new folder called Views under the project, and a folder for the StartPage view.
Create a new file using the Razor View - Empty template in Visual Studio.
Also add a new file directly under Views, using the Razor View Imports template in VS.

In the  \_ViewImports.cshtml file we can add @using declarations that will be imported into all views.
We will add these for now
```
@using EPiServer.Core
@using EPiServer.Web.Mvc.Html
```
Next we can also fill in the view for StartPage
```
@model AlloyTraining.Models.Pages.StartPage

@{
}

<h1>
    @Html.PropertyFor(m => m.Heading)
</h1>
```



![[Pasted image 20250602113943.png]]