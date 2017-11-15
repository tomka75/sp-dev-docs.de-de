---
title: Vorgehensweise Exportieren Sie das Namensfeld in einer Dokumentbibliothek-Liste in einer mobilen Anwendung
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 901c2012-18c6-4dbd-a787-f8650a0cc7a8
ms.openlocfilehash: e7d2d65e3e1a229d0cbf6853be86264caa850ba2
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-export-the-name-field-in-a-document-library-list-to-a-mobile-app"></a><span data-ttu-id="6a57c-102">Vorgehensweise: Exportieren Sie das Namensfeld in einer Dokumentbibliothek-Liste in einer mobilen Anwendung</span><span class="sxs-lookup"><span data-stu-id="6a57c-102">How to: Export the Name field in a Document Library list to a mobile app</span></span>
<span data-ttu-id="6a57c-p101">Exportieren Sie das Feld "Name" einer Dokumentbibliotheksliste mit dem Visual Studio SharePoint-Listen-Assistenten in eine mobile App. Das Feld "Name" wird nicht automatisch angezeigt, wenn Benutzer eine mobile App für eine Dokumentbibliothek in SharePoint erstellen. In einer Liste Dokumentbibliothek kann Benutzer verschiedene Dokumente hochladen. Ein Listenelement für ein Dokument besteht typischerweise als Eigenschaften **Title**, **Name**und eine Verknüpfung mit dem Dokument. Wenn ein Entwickler eine Windows Phone 7-app für die Dokumentbibliothek erstellt, wird das Feld **Name** nicht in der IDE-Assistent exportiert. Daher hat der Entwickler nur schwer feststellen, den Namen des Dokuments. (Dies ist, da SharePoint Felder vom Typ "Datei" standardmäßig nicht unterstützt.)</span><span class="sxs-lookup"><span data-stu-id="6a57c-p101">Export the Name field of a Document Library list to a mobile app by using the Visual Studio SharePoint List wizard. The Name field does not appear automatically when a user creates a mobile app for a document library in SharePoint. In a Document Library list, a user can upload various documents. A list item for a document typically has **Title**, **Name**, and a link to the document as properties. If a developer creates a Windows Phone 7 app against the document library, the **Name** field is not exported in the IDE wizard. Thus the developer has no easy way of knowing the document name. (This is because SharePoint does not support fields of type "FILE" by default.)</span></span>
  
    
    


> <span data-ttu-id="6a57c-110">**Hinweis:** Die **Title**-Eigenschaft umfasst nicht die Dateinamenerweiterung.</span><span class="sxs-lookup"><span data-stu-id="6a57c-110">**Note** The **Title** property does not include the file name extension.</span></span>
  
    
    


<span data-ttu-id="6a57c-111">Wenn Sie einem Dokument abrufen, die vollständige URL des Dokuments erstellen und öffnen Sie das Dokument in der standardanwendung (beispielsweise Word) möchten, müssen Sie Code zum Abrufen des Namens des tatsächlichen Datei so schreiben.</span><span class="sxs-lookup"><span data-stu-id="6a57c-111">So if you want to fetch a document, build the full URL of the document, and open the document in the default application (such as Word), you must write code to get the actual file name.</span></span>
  
    
    


> <span data-ttu-id="6a57c-112">**Wichtig:** Wenn Sie eine App für Windows Phone 8 entwickeln, müssen Sie Visual Studio Express 2012 anstelle von Visual Studio 2010 Express verwenden.</span><span class="sxs-lookup"><span data-stu-id="6a57c-112">**Important** If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express. Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="6a57c-113">Mit Ausnahme der Entwicklungsumgebung gelten alle Informationen in diesem Artikel für das Erstellen von Apps sowohl unter Windows Phone 8 als auch unter Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="6a57c-113">Important If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express. Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="6a57c-114">Weitere Informationen finden Sie unter [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung mobiler Apps für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="6a57c-114">For more information, see  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span></span> 
  
    
    


## <a name="prerequisites-for-exporting-the-name-field-of-a-document-library"></a><span data-ttu-id="6a57c-115">Voraussetzungen für das Exportieren des Felds „Name“ der Dokumentbibliothek</span><span class="sxs-lookup"><span data-stu-id="6a57c-115">Prerequisites for exporting the Name field of a document library</span></span>


- <span data-ttu-id="6a57c-116">SharePoint</span><span class="sxs-lookup"><span data-stu-id="6a57c-116">SharePoint</span></span>
    
  
- <span data-ttu-id="6a57c-117">Visual Studio Express 2010 mit den neuen SharePoint-Vorlagen</span><span class="sxs-lookup"><span data-stu-id="6a57c-117">Visual Studio Express 2010 with the new SharePoint templates</span></span>
    
  

## <a name="customize-the-generated-classes"></a><span data-ttu-id="6a57c-118">Anpassen der generierten Klassen</span><span class="sxs-lookup"><span data-stu-id="6a57c-118">Customize the generated classes</span></span>
<span data-ttu-id="6a57c-119"><a name="HowToExportTheNameFieldInADocumentLibraryListToAMobileApp_CustomizeTheGeneratedClases"> </a></span><span class="sxs-lookup"><span data-stu-id="6a57c-119"></span></span>

<span data-ttu-id="6a57c-p103">Um die **Name** dar und Access-Anlagen aus einer Dokumentbibliothek zu exportieren, müssen Sie einige Änderungen vornehmen, in der **ListDataProvider** -Klasse, DisplayItemViewModel.cs und in der **DisplayForm** -Klasse. Wenn ein Entwickler den Assistenten für neuen SPList aus Visual Studio verwendet, erstellt der Assistent mehrere Klassen, die das Model-View-ViewModel-Entwurfsmuster folgen. (Weitere Informationen finden Sie [unter Verwendung des Model-View-ViewModel-Musters](http://msdn.microsoft.com/en-us/library/hh821028.aspx).) Es werden zwei Ordner erstellt: eine heißt Ansichten und enthält alle Dateien, die zum Ändern der verschiedenen Listenansichten (beispielsweise DisplayForm, EditForm, Listen- und NewForm) erforderlich. Der andere heißt ViewModels und DisplayItemViewModel, EditItemViewModel, ListViewModel und NewItemViewModel enthält. Sie können einige dieser Klassen, die vom Assistenten generierte ändern.</span><span class="sxs-lookup"><span data-stu-id="6a57c-p103">To export the **Name** field and access attachments from a document library, you must make a few changes in the **ListDataProvider** class, in DisplayItemViewModel.cs, and in the **DisplayForm** class. When a developer uses the new SPList wizard from Visual Studio, the wizard creates several classes that follow the Model-View-ViewModel design pattern. (For more information, see [Using the Model-View-ViewModel Pattern](http://msdn.microsoft.com/en-us/library/hh821028.aspx).) Two folders are created: One is named Views and contains all files needed to modify various list views (such as DisplayForm, EditForm, List, and NewForm). The other is named ViewModels and contains DisplayItemViewModel, EditItemViewModel, ListViewModel, and NewItemViewModel. You will be modifying some of these classes generated by the wizard.</span></span>
  
    
    

### <a name="step-1-modify-listdataprovider-to-fetch-splistitemfile-property"></a><span data-ttu-id="6a57c-125">Schritt 1: Ändern von ListDataProvider zum Abrufen von SPListItem.File-Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="6a57c-125">Step 1: Modify ListDataProvider to fetch SPListItem.File property</span></span>


1. <span data-ttu-id="6a57c-126">Fügen Sie in der **ListDataProvider** -Klasse die folgende Codezeile in der **LoadItem** -Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="6a57c-126">In the **ListDataProvider** class, add the following line of code in the **LoadItem** method.</span></span>
    
     `Context.Load(spListItem, Item => Item.File);`
    
  
2. <span data-ttu-id="6a57c-127">Fügen Sie auch in der **ListDataProvider** -Klasse den folgenden Code in der **LoadData** -Methode.</span><span class="sxs-lookup"><span data-stu-id="6a57c-127">Also in the **ListDataProvider** class, add the following code in the **LoadData** method.</span></span>
    
     `Context.Load(items, listItems => listItems.Include(item => item.File));`
    
  

### <a name="step-2-add-the-fileurl-and-filename-properties"></a><span data-ttu-id="6a57c-128">Schritt 2: Hinzufügen der Eigenschaften FileUrl und Dateiname</span><span class="sxs-lookup"><span data-stu-id="6a57c-128">Step 2: Add the FileUrl and FileName properties</span></span>


- <span data-ttu-id="6a57c-129">Fügen Sie den folgenden Code in DisplayItemViewModel.cs um **DisplayVM**.</span><span class="sxs-lookup"><span data-stu-id="6a57c-129">In DisplayItemViewModel.cs, add the following code to **DisplayVM**.</span></span>
    
```cs
  
public string m_fileUrl;
        public string FileUrl
        {
            get
            {
                if (string.IsNullOrEmpty(m_fileUrl))
                {
                    IListDataProvider p = this.DataProvider;
                    p.LoadItem(this.ID, (LoadItemCompletedEventArgs args) =>
                         {
                             FileUrl = this.DataProvider.SiteUrl + 
                                       args.Item.File.ServerRelativeUrl;
                         });
                }
                return m_fileUrl;
            }
            set
            {
                m_fileUrl = value;
                RaisePropertyChanged("FileUrl");
            }
        }
        public string m_fileName;
        public string FileName
        {
            get
            {
                if (string.IsNullOrEmpty(m_fileName))
                {
                    IListDataProvider p = this.DataProvider;
                    p.LoadItem(this.ID, (LoadItemCompletedEventArgs args) =>
                    {
                        FileName = args.Item.File.Name;
                    });
                }

                return m_fileName;
            }
            set
            {
                m_fileName = value;
                RaisePropertyChanged("FileName");
            }
        }
```


### <a name="step-3-add-a-hyperlink-to-the-displayform-that-binds-to-fileurl-and-filename"></a><span data-ttu-id="6a57c-130">Schritt 3: Hinzufügen eines Hyperlinks zu den DisplayForm, die FileUrl und der Dateiname bindet</span><span class="sxs-lookup"><span data-stu-id="6a57c-130">Step 3: Add a hyperlink to the DisplayForm that binds to FileUrl and FileName</span></span>


- <span data-ttu-id="6a57c-131">Fügen Sie dem Formular anzeigen.</span><span class="sxs-lookup"><span data-stu-id="6a57c-131">Add the following changes to the Display form.</span></span>
    
```XML
  
<StackPanel HorizontalAlignment="Left" Orientation="Horizontal" Margin="0,5,0,5">
  <TextBlock TextWrapping="Wrap" Width="150" HorizontalAlignment="Left" 
   Style="{StaticResource PhoneTextNormalStyle}">
    FileUrl :
  </TextBlock>
  <HyperlinkButton Content="{Binding FileName}" NavigateUri="{Binding FileUrl}" 
   x:Name="hypFile" TargetName="_blank" />
</StackPanel>

```


## <a name="additional-resources"></a><span data-ttu-id="6a57c-132">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6a57c-132">Additional resources</span></span>
<span data-ttu-id="6a57c-133"><a name="SP15StoreSPlist_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6a57c-133"></span></span>


-  [<span data-ttu-id="6a57c-134">Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="6a57c-134">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="6a57c-135">Vorgehensweise: Erstellen eine Windows Phone SharePoint Liste app</span><span class="sxs-lookup"><span data-stu-id="6a57c-135">How to: Create a Windows Phone SharePoint list app</span></span>](how-to-create-a-windows-phone-sharepoint-list-app.md)
    
  
-  [<span data-ttu-id="6a57c-136">Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint</span><span class="sxs-lookup"><span data-stu-id="6a57c-136">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="6a57c-137">Windows Phone SDK 7.1</span><span class="sxs-lookup"><span data-stu-id="6a57c-137">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="6a57c-138">Microsoft SharePoint SDK für Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="6a57c-138">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

