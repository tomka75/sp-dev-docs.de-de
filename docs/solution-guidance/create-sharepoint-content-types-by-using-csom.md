---
title: Erstellen von SharePoint-Inhaltstypen mithilfe von CSOM
ms.date: 11/03/2017
ms.openlocfilehash: 6a0e7eff44bffbc6b2de3cc181fe9b2d09df1117
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="create-sharepoint-content-types-by-using-csom"></a>Erstellen von SharePoint-Inhaltstypen mithilfe von CSOM

Erstellen von SharePoint-Inhaltstypen mithilfe von CSOM, und Ändern der Lokalisierung mithilfe von Features in SharePoint 2013 SP1 eingeführt.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Im Beispiel [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) können zum programmgesteuerten Erstellen von Websitespalten und Inhaltstypen und miteinander zu verknüpfen. Sie können auch verwenden, der SharePoint 2013 SP1 CSOM APIs, verfügbar in [SharePoint Server 2013 Client Components SDK](http://www.microsoft.com/en-us/download/details.aspx?id=35585), um einen bestimmten Inhaltstyp-ID hinzuzufügen und Lokalisieren von Inhaltstypen, Listen und Titel der Website. 

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Herunterladen Sie das [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) -Beispiel um zu Beginn des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="create-content-types-and-site-columns"></a>Erstellen von Inhaltstypen und Websitespalten

Im folgenden Codebeispiel wird veranschaulicht, wie zum Erstellen eines Inhaltstyps mithilfe der **komplexer ContentTypeCreationInformation** -Klasse, einschließlich Festlegen der ID ab.

**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

Verknüpfen Sie Felder für den Inhaltstyp mithilfe der Klassen **FieldLinkCollection** und **FieldLinkCreationInformation** .

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

## <a name="localize-content-types-list-and-site-titles"></a>Lokalisieren von Inhaltstypen, Listen- und Titel der Website

Mithilfe des folgenden Codes So lokalisieren Sie den Titel der Website und die websitebeschreibung.

```C#
web.TitleResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnÃ¤ minut");
web.DescriptionResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnetty saitti");

```

Eine Liste verwenden Sie die gleiche Weise wie bei einer Website.

```C#
list.TitleResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnÃ¤ minut");
list.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤mÃ¤ esimerkki nÃ¤yttÃ¤Ã¤ miten voit kielikÃ¤Ã¤ntÃ¤Ã¤ listoja.");

```

Für Inhaltstypen müssen Sie die Option für die Lokalisierung von Name und Beschreibung. für Felder können Sie die Werte für Titel und Beschreibung lokalisieren.

```C#
myContentType.NameResource.SetValueForUICulture("fi-FI", "Contoso Dokumentti");
myContentType.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤mÃ¤ on geneerinen Contoso dokumentti.");

fld.TitleResource.SetValueForUICulture("fi-FI", "Contoso Teksti");
fld.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤Ã¤ on niiku Contoso metadatalle.");

```

## <a name="create-document-content-types-and-site-columns"></a>Erstellen von Inhaltstypen und Websitespalten

Im folgenden Beispiel wird gezeigt, wie Dokument Inhaltstypen erstellen und dann mit dem Inhaltstyp Zuordnen einer Dokumentvorlage. 

Dieses Beispiel fügt einen neuen Inhaltstyp 'Contoso Dokument' aufgerufen, um die Websitesammlung an. In diesem Inhaltstyp weist eine benutzerdefinierte Vorlage, die damit verknüpft ist, wenn ein neues Dokument erstellt wird.

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

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [SharePoint-Website Bereitstellen von Lösungen](sharepoint-site-provisioning-solutions.md)
    
- [FTC zu CAM - Erstellen von Inhaltstypen mit bestimmten CSO mit IDs](http://blogs.msdn.com/b/vesku/archive/2014/02/28/ftc-to-cam-create-content-types-with-specific-ids-using-csom.aspx)
    
- [SharePoint Server 2013-Clientkomponenten – SDK](http://www.microsoft.com/en-us/download/details.aspx?id=35585)
