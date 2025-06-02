#Devs #ModuleB 

From an empty project like AlloyTraining, there is no support for media assets yet, we need to add new models for media assets like images and video.

To do this we have to create new classes that inherit from the MediaData, ImageData, or VideoData class to add the support.

```
using EPiServer.Framework.DataAnnotations;

namespace AlloyTraining.Models.Media;

[ContentType(
    DisplayName = "Image",
    GUID = "91372021-DB5A-4E61-A3D2-B0FF553826DC",
    Description = "Use this to upload images.")]
[MediaDescriptor(ExtensionString = "png,jpg,jpeg")]
public class ImageFile : ImageData
{
}
```
Here I have implemented the **ImageFile** class, it inherits the **ImageData** and accepts png, jpg, jpeg as file formats.

You would do the same for VideoFile and other formats you want, maybe a DocumentFile for PDF etc.

#### Rendering media
For now, we're just dragging and dropping media types into a rich text property, as the MainBody on StartPage.

When we drag media types into a rich text property, they are rendered based on the inherited class.
- **MediaData**: Renders an anchor tag with the link to the asset.
  `<a href="siteassets/documents/note.txt>notes.txt</a>`
- **ImageData**: Renders an img tag.
  `<img src="siteassets/products/alloy-meet.jpeg" />`
- **VideoData**: Renders a video tag.
  `<video src="siteassets/products/alloy-meet.mpeg" />`

