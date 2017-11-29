---
title: Erstellen von SharePoint-Inhaltstypen mithilfe von CSOM
ms.date: 11/03/2017
ms.openlocfilehash: 6a0e7eff44bffbc6b2de3cc181fe9b2d09df1117
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="create-sharepoint-content-types-by-using-csom"></a><span data-ttu-id="2904d-102">Erstellen von SharePoint-Inhaltstypen mithilfe von CSOM</span><span class="sxs-lookup"><span data-stu-id="2904d-102">Create SharePoint content types by using CSOM</span></span>

<span data-ttu-id="2904d-103">Erstellen von SharePoint-Inhaltstypen mithilfe von CSOM, und Ändern der Lokalisierung mithilfe von Features in SharePoint 2013 SP1 eingeführt.</span><span class="sxs-lookup"><span data-stu-id="2904d-103">Create SharePoint content types by using CSOM, and make localization changes by using features introduced in SharePoint 2013 SP1.</span></span>

<span data-ttu-id="2904d-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="2904d-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="2904d-105">Im Beispiel [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) können zum programmgesteuerten Erstellen von Websitespalten und Inhaltstypen und miteinander zu verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="2904d-105">You can use the [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) sample to programmatically create site columns and content types and link them together.</span></span> <span data-ttu-id="2904d-106">Sie können auch verwenden, der SharePoint 2013 SP1 CSOM APIs, verfügbar in [SharePoint Server 2013 Client Components SDK](http://www.microsoft.com/en-us/download/details.aspx?id=35585), um einen bestimmten Inhaltstyp-ID hinzuzufügen und Lokalisieren von Inhaltstypen, Listen und Titel der Website.</span><span class="sxs-lookup"><span data-stu-id="2904d-106">You can also use the SharePoint 2013 SP1 CSOM APIs, available in the [SharePoint Server 2013 Client Components SDK](http://www.microsoft.com/en-us/download/details.aspx?id=35585), to add a specific content type identifier, and localize content types, lists, and site titles.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="2904d-107">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="2904d-107">Before you begin</span></span>

<span data-ttu-id="2904d-108">Herunterladen Sie das [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) -Beispiel um zu Beginn des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="2904d-108">To get started, download the [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) sample from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="create-content-types-and-site-columns"></a><span data-ttu-id="2904d-109">Erstellen von Inhaltstypen und Websitespalten</span><span class="sxs-lookup"><span data-stu-id="2904d-109">Create content types and site columns</span></span>

<span data-ttu-id="2904d-110">Im folgenden Codebeispiel wird veranschaulicht, wie zum Erstellen eines Inhaltstyps mithilfe der **komplexer ContentTypeCreationInformation** -Klasse, einschließlich Festlegen der ID ab.</span><span class="sxs-lookup"><span data-stu-id="2904d-110">The following code example shows how to create a content type by using the  **ContentTypeCreationInformation** class, including setting the ID.</span></span>

<span data-ttu-id="2904d-111">**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="2904d-111">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
ContentTypeCollection contentTypes = web.ContentTypes;
cc.Load(contentTypes);
cc.ExecuteQuery();

foreach (var item in contentTypes)
{
  if (item.StringId == "0x0101009189AB5D3D2647B580F011DA2F356FB2")
    return;
}

// Create a Content Type Information object.
ContentTypeCreationInformation newCt = new ContentTypeCreationInformation();
// Set the name for the content type.
newCt.Name = "Contoso Document";
// Inherit from oob document - 0x0101 and assign. 
newCt.Id = "0x0101009189AB5D3D2647B580F011DA2F356FB2";
// Set content type to be available from specific group.
newCt.Group = "Contoso Content Types";
// Create the content type.
ContentType myContentType = contentTypes.Add(newCt);
cc.ExecuteQuery();

Using AddFieldAsXml you can add fields to the FieldCollection of a site collection:
FieldCollection fields = web.Fields;
cc.Load(fields);
cc.ExecuteQuery();

string FieldAsXML = @"<Field ID='{4F34B2ED-9CFF-4900-B091-4C0033F89944}' Name='ContosoString' DisplayName='Contoso String' Type='Text' Hidden='False' Group='Contoso Site Columns' Description='Contoso Text Field' />";
Field fld = fields.AddFieldAsXml(FieldAsXML, true, AddFieldOptions.DefaultValue);
cc.Load(fields);
cc.Load(fld);
cc.ExecuteQuery();

```

<span data-ttu-id="2904d-112">Verknüpfen Sie Felder für den Inhaltstyp mithilfe der Klassen **FieldLinkCollection** und **FieldLinkCreationInformation** .</span><span class="sxs-lookup"><span data-stu-id="2904d-112">Link the fields to the content type by using the  **FieldLinkCollection** and **FieldLinkCreationInformation** classes.</span></span>

```C#
FieldCollection fields = web.Fields;
Field fld = fields.GetByInternalNameOrTitle("ContosoString");
cc.Load(fields);
cc.Load(fld);
cc.ExecuteQuery();

FieldLinkCollection refFields = myContentType.FieldLinks;
cc.Load(refFields);
cc.ExecuteQuery();

foreach (var item in refFields)
{
  if (item.Name == "ContosoString")
    return;
  }

FieldLinkCreationInformation link = new FieldLinkCreationInformation();
link.Field = fld;
myContentType.FieldLinks.Add(link);
myContentType.Update(true);
cc.ExecuteQuery();

```

## <a name="localize-content-types-list-and-site-titles"></a><span data-ttu-id="2904d-113">Lokalisieren von Inhaltstypen, Listen- und Titel der Website</span><span class="sxs-lookup"><span data-stu-id="2904d-113">Localize content types, list, and site titles</span></span>

<span data-ttu-id="2904d-114">Mithilfe des folgenden Codes So lokalisieren Sie den Titel der Website und die websitebeschreibung.</span><span class="sxs-lookup"><span data-stu-id="2904d-114">Use the following code to localize the site title and site description.</span></span>

```C#
web.TitleResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnÃ¤ minut");
web.DescriptionResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnetty saitti");

```

<span data-ttu-id="2904d-115">Eine Liste verwenden Sie die gleiche Weise wie bei einer Website.</span><span class="sxs-lookup"><span data-stu-id="2904d-115">For a list, you use the same approach as for a site.</span></span>

```C#
list.TitleResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnÃ¤ minut");
list.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤mÃ¤ esimerkki nÃ¤yttÃ¤Ã¤ miten voit kielikÃ¤Ã¤ntÃ¤Ã¤ listoja.");

```

<span data-ttu-id="2904d-116">Für Inhaltstypen müssen Sie die Option für die Lokalisierung von Name und Beschreibung.</span><span class="sxs-lookup"><span data-stu-id="2904d-116">For content types, you have the option to localize the name and description.</span></span> <span data-ttu-id="2904d-117">für Felder können Sie die Werte für Titel und Beschreibung lokalisieren.</span><span class="sxs-lookup"><span data-stu-id="2904d-117">for fields, you can localize the title and description values.</span></span>

```C#
myContentType.NameResource.SetValueForUICulture("fi-FI", "Contoso Dokumentti");
myContentType.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤mÃ¤ on geneerinen Contoso dokumentti.");

fld.TitleResource.SetValueForUICulture("fi-FI", "Contoso Teksti");
fld.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤Ã¤ on niiku Contoso metadatalle.");

```

## <a name="create-document-content-types-and-site-columns"></a><span data-ttu-id="2904d-118">Erstellen von Inhaltstypen und Websitespalten</span><span class="sxs-lookup"><span data-stu-id="2904d-118">Create document content types and site columns</span></span>

<span data-ttu-id="2904d-119">Im folgenden Beispiel wird gezeigt, wie Dokument Inhaltstypen erstellen und dann mit dem Inhaltstyp Zuordnen einer Dokumentvorlage.</span><span class="sxs-lookup"><span data-stu-id="2904d-119">The following example shows how to create document content types and then associate a document template with the content type.</span></span> 

<span data-ttu-id="2904d-120">Dieses Beispiel fügt einen neuen Inhaltstyp 'Contoso Dokument' aufgerufen, um die Websitesammlung an.</span><span class="sxs-lookup"><span data-stu-id="2904d-120">This example adds a new content type called 'Contoso Document' to the site collection.</span></span> <span data-ttu-id="2904d-121">In diesem Inhaltstyp weist eine benutzerdefinierte Vorlage, die damit verknüpft ist, wenn ein neues Dokument erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="2904d-121">This content type has a custom template associated with it when a new document is created.</span></span>

```C#
ContentType ct = web.ContentTypes.GetById("0x0101009189AB5D3D2647B580F011DA2F356FB2");
            cc.Load(ct); cc.ExecuteQuery();
            string ctFolderServerRelativeURL = "_cts/" + ct.Name;
            Folder ctFolder = web.GetFolderByServerRelativeUrl(ctFolderServerRelativeURL);
            cc.Load(ctFolder);
            cc.ExecuteQuery();

            string path = @"C:\Data\Test Documents\Doc CT File.docx";
            string fileName = System.IO.Path.GetFileName(path);
            byte[] filecontent = System.IO.File.ReadAllBytes(path);

            using (System.IO.FileStream fs = new System.IO.FileStream(path, System.IO.FileMode.Open))
            {
                FileCreationInformation newFile = new FileCreationInformation();
                newFile.Content = filecontent;
                newFile.Url = ctFolderServerRelativeURL + "/" + fileName;

                Microsoft.SharePoint.Client.File uploadedFile = ctFolder.Files.Add(newFile);
                cc.Load(uploadedFile);
                cc.ExecuteQuery();
                //Microsoft.SharePoint.Client.File.SaveBinaryDirect(clientContext, ctFolderServerRelativeURL + "/" + fileName, fs, true);

                
                cc.Load(ct); cc.ExecuteQuery();
                ct.DocumentTemplate = fileName;
                ct.Update(false);
                cc.Load(ct); cc.ExecuteQuery();
                Console.WriteLine("Content type updates");
            }

```

## <a name="additional-resources"></a><span data-ttu-id="2904d-122">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="2904d-122">Additional resources</span></span>
<span data-ttu-id="2904d-123"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2904d-123"></span></span>

- [<span data-ttu-id="2904d-124">SharePoint-Website Bereitstellen von Lösungen</span><span class="sxs-lookup"><span data-stu-id="2904d-124">SharePoint site provisioning solutions</span></span>](sharepoint-site-provisioning-solutions.md)
    
- [<span data-ttu-id="2904d-125">FTC zu CAM - Erstellen von Inhaltstypen mit bestimmten CSO mit IDs</span><span class="sxs-lookup"><span data-stu-id="2904d-125">FTC to CAM - Create Content Types with specific IDs using CSO</span></span>](http://blogs.msdn.com/b/vesku/archive/2014/02/28/ftc-to-cam-create-content-types-with-specific-ids-using-csom.aspx)
    
- [<span data-ttu-id="2904d-126">SharePoint Server 2013-Clientkomponenten – SDK</span><span class="sxs-lookup"><span data-stu-id="2904d-126">SharePoint Server 2013 Client Components SDK</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35585)
