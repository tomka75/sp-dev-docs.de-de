---
title: Exportieren des Namensfelds einer Dokumentbibliotheksliste in eine mobile App
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 901c2012-18c6-4dbd-a787-f8650a0cc7a8
ms.openlocfilehash: c17eae0cbc62a597ba17e61a47c4bfcb660fd42e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="export-the-name-field-in-a-document-library-list-to-a-mobile-app"></a>Exportieren des Namensfelds einer Dokumentbibliotheksliste in eine mobile App

Exportieren Sie das Feld "Name" einer Dokumentbibliotheksliste mit dem Visual Studio SharePoint-Listen-Assistenten in eine mobile App. Das Feld "Name" wird nicht automatisch angezeigt, wenn Benutzer eine mobile App für eine Dokumentbibliothek in SharePoint erstellen. In einer Liste Dokumentbibliothek kann Benutzer verschiedene Dokumente hochladen. Ein Listenelement für ein Dokument besteht typischerweise als Eigenschaften **Title**, **Name**und eine Verknüpfung mit dem Dokument. Wenn ein Entwickler eine Windows Phone 7-app für die Dokumentbibliothek erstellt, wird das Feld **Name** nicht in der IDE-Assistent exportiert. Daher hat der Entwickler nur schwer feststellen, den Namen des Dokuments. (Dies ist, da SharePoint Felder vom Typ "Datei" standardmäßig nicht unterstützt.)
  
> [!NOTE]
> Die **Title**-Eigenschaft umfasst nicht die Dateinamenerweiterung.
  
    
    


Wenn Sie einem Dokument abrufen, die vollständige URL des Dokuments erstellen und öffnen Sie das Dokument in der standardanwendung (beispielsweise Word) möchten, müssen Sie Code zum Abrufen des Namens des tatsächlichen Datei so schreiben.
  
    
    


> **Wichtig:** Wenn Sie eine App für Windows Phone 8 entwickeln, müssen Sie Visual Studio Express 2012 anstelle von Visual Studio 2010 Express verwenden. Mit Ausnahme der Entwicklungsumgebung gelten alle Informationen in diesem Artikel für das Erstellen von Apps sowohl auf Windows Phone 8 als auch auf Windows Phone 7. Weitere Informationen finden Sie unter [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung mobiler Apps für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md). 
  
    
    


## <a name="prerequisites-for-exporting-the-name-field-of-a-document-library"></a>Voraussetzungen für das Exportieren des Felds „Name“ der Dokumentbibliothek


- SharePoint
    
  
- Visual Studio Express 2010 mit den neuen SharePoint-Vorlagen
    
  

## <a name="customize-the-generated-classes"></a>Anpassen der generierten Klassen
<a name="HowToExportTheNameFieldInADocumentLibraryListToAMobileApp_CustomizeTheGeneratedClases"> </a>

Um die **Name** dar und Access-Anlagen aus einer Dokumentbibliothek zu exportieren, müssen Sie einige Änderungen vornehmen, in der **ListDataProvider** -Klasse, DisplayItemViewModel.cs und in der **DisplayForm** -Klasse. Wenn ein Entwickler den Assistenten für neuen SPList aus Visual Studio verwendet, erstellt der Assistent mehrere Klassen, die das Model-View-ViewModel-Entwurfsmuster folgen. (Weitere Informationen finden Sie [unter Verwendung des Model-View-ViewModel-Musters]((http://msdn.microsoft.com/de-DE/library/hh821028.aspx)).) Es werden zwei Ordner erstellt: eine heißt Ansichten und enthält alle Dateien, die zum Ändern der verschiedenen Listenansichten (beispielsweise DisplayForm, EditForm, Listen- und NewForm) erforderlich. Der andere heißt ViewModels und DisplayItemViewModel, EditItemViewModel, ListViewModel und NewItemViewModel enthält. Sie können einige dieser Klassen, die vom Assistenten generierte ändern.
  
    
    

### <a name="step-1-modify-listdataprovider-to-fetch-splistitemfile-property"></a>Schritt 1: Ändern von ListDataProvider zum Abrufen von SPListItem.File-Eigenschaft


1. Fügen Sie in der **ListDataProvider** -Klasse die folgende Codezeile in der **LoadItem** -Methode hinzu.
    
     `Context.Load(spListItem, Item => Item.File);`
    
  
2. Fügen Sie auch in der **ListDataProvider** -Klasse den folgenden Code in der **LoadData** -Methode.
    
     `Context.Load(items, listItems => listItems.Include(item => item.File));`
    
  

### <a name="step-2-add-the-fileurl-and-filename-properties"></a>Schritt 2: Hinzufügen der Eigenschaften FileUrl und Dateiname


- Fügen Sie den folgenden Code in DisplayItemViewModel.cs um **DisplayVM**.
    
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


### <a name="step-3-add-a-hyperlink-to-the-displayform-that-binds-to-fileurl-and-filename"></a>Schritt 3: Hinzufügen eines Hyperlinks zu den DisplayForm, die FileUrl und der Dateiname bindet


- Fügen Sie dem Formular anzeigen.
    
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


## <a name="see-also"></a>Siehe auch
<a name="SP15StoreSPlist_addlresources"> </a>


-  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Vorgehensweise: Erstellen eine Windows Phone SharePoint Liste app](how-to-create-a-windows-phone-sharepoint-list-app.md)
    
  
-  [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Windows Phone SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Microsoft SharePoint SDK für Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

