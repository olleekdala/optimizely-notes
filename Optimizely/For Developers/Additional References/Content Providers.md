#Devs #Additional
[Content Providers](https://docs.developers.optimizely.com/content-management-system/docs/content-providers)

A content provider connects an Optimizely Content Management System (CMS) site to an external data source so that the data appears to be part of the CMS website, even though the data resides at the data source. You can build multiple custom content providers, consolidating the data into one CMS and giving users an integrated user experience. A content provider operates in the following ways.

- **Data resides in original store** – The data is not stored in the local CMS website database; the data source is integrated with CMS.
- **Requires coding and configuration** – Registered content providers must inherit from `ContentProvider` configuration or registration of a content provider. Add a registered provider to `ContentOptions.Providers`, or through `IContentProviderManager`.
- **IContent only** – The information or data from a content provider displays as CMS content only.
- **DefaultContentProvider technology** – CMS uses the content provider concept internally; that is, the local pages and content served by the CMS database are also delivered through a content provider: `DefaultContentProvider`.
- **Enable/Disable Content Provider Functionality** – To move content between content providers, special permissions must be switched on in **Admin view** > **Access Rights** > **Permissions for functions: Move between page providers**. A warning dialog box displays when you attempt to move pages between providers.



# Custom Content Provider
[Configure content providers](https://docs.developers.optimizely.com/content-management-system/docs/configuring-content-providers)

A content provider is a module that, when registered with Optimizely Content Management System (CMS), can serve the site with external data as `IContent` objects (for example `PageData` instances). A CMS site can have several different content provider instances registered, each with its own configuration data set, such as capabilities settings and so on.
## Note
A custom content provider cannot deliver the start page, root page, and waste basket (recycle bin, trash).

You configure content providers when register them. You can add attributes for the content provider type, which are passed into the provider instance when the instance is initialized. Following is an example of how to register a custom content provider with configuration values for the provider:

```c#
services.Configure<ContentOptions>(o => o.AddProvider<XmlContentProvider>("xml", config => {
    config[ContentProviderParameter.EntryPoint] = _configuration.GetValue<string>(ContentProviderParameter.EntryPoint);
    config[ContentProviderParameter.Capabilities] = ContentProviderParameter.FullProviderCapability;
    config["someConfigKey"] = "someConfigValue";
}));
```