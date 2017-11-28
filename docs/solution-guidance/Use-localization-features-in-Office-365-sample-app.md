---
title: Lokalisierung-Features in Office 365 Beispiel-add-in verwenden
ms.date: 11/03/2017
ms.openlocfilehash: 83ced206837c555fc644715c77a1fa070ad23e9e
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="use-localization-features-in-office-365-sample-add-in"></a>Lokalisierung-Features in Office 365 Beispiel-add-in verwenden

Die Lokalisierungsfeatures können in Office 365 Sie lokalisierte Werte für SharePoint-Websites, Listen, Inhaltstypen und Websitespalten bereitzustellen. 
    
_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_
    
Das [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) -Beispiel zeigt, wie Sie mit der Lokalisierungsfeatures von Office 365 für Websites, Listen, Inhaltstypen und Websitespalten. In diesem Codebeispiel verwendet eine Konsolenanwendung, folgende Aktionen ausführen:

- Erstellen von Inhaltstypen, Websitespalten und Listen und Inhaltstypen Websitespalten zuordnen.
    
- Lokalisieren Sie den Inhaltstyp, Websitespalte, Listen- und eine benutzerdefinierte Website.

**Hinweis**  In diesem Artikel beschriebenen Lokalisierungsfeatures sind sind nur verfügbar in Office 365. Informationen über die Lokalisierungsfeatures, die in Office 365 dedizierter oder SharePoint Server 2013: lokal verfügbar sind, finden Sie unter [How to: Localize-add-ins for SharePoint](http://msdn.microsoft.com/library/907a9189-7ce3-469a-8c87-4cef26f03c73.aspx) und [Lokalisieren von SharePoint-Lösungen](https://msdn.microsoft.com/en-us/library/ee696750.aspx).

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Bevor Sie dieses Codebeispiel ausführen:

1. Konfigurieren Sie die Language-Einstellungen auf Ihrer Website ein. Dazu:
    
      ein. Wählen Sie auf der Teamwebsite **Einstellungen** > **websiteeinstellungen**.
    
      b. Wählen Sie in der **Die Verwaltung von** **spracheinstellungen**.
    
      c. Wählen Sie auf der Seite **Spracheinstellungen** im **alternative Sprache(n)**, die alternativen Sprachen, die Ihre Website unterstützt werden soll. Sie können beispielsweise Französisch und Finnisch, auswählen, wie in Abbildung 1 dargestellt.
    
      d. Wählen Sie  **OK** aus.
     
2. Legen Sie die Anzeigesprache auf der Profilseite des Benutzers an. Dazu:
    
      ein. Am oberen Rand der Office 365-Website wählen Sie Ihr Profilbild aus, und wählen Sie **über mich**, wie in Abbildung 2 dargestellt.
    
      b. Wählen Sie auf der Seite **über mich** **Mein Profil bearbeiten**.
    
      c. Wählen Sie **...** (Weitere Optionen), und klicken Sie dann auf **Sprache und Region**.
    
      d. Wählen Sie in **Meine Anzeigesprachen**, eine neue Sprache, die Sie auf der Website mit der Dropdownliste **Wählen Sie eine neue Sprache** festlegen ähnelt wählen Sie dann auf **Hinzufügen**. Wählen Sie beispielsweise Französisch und Finnisch, wie in Abbildung 3 dargestellt. Sie können die gewünschte Sprache nach oben oder unten verschieben, indem Sie auf den Pfeil nach oben und nach unten weisenden Pfeil.
    
      e. Wählen Sie **Speichern und schließen**.

**Hinweis**  Es kann für Ihre Website, um die ausgewählten Sprache(n) Rendern ein paar Minuten dauern. 

**Abbildung 1. Spracheinstellungen für eine Website**

![Screenshot, der die spracheinstellungen für eine Website anzeigt.](media/ffe149ae-17ab-4c55-a611-d47f4eb88c4e.png)

**Abbildung 2. Navigieren zu Profilseite des Benutzers über mich auswählen**

![Screenshot der Benutzerprofilseite mit über mich hervorgehoben](media/764b2ac2-155b-4ce9-b8eb-3ae04ad26593.png)

**Abbildung 3. Ändern eines Benutzers anzeigen Sprachoptionen auf der Profilseite des Benutzers**

![Screenshot des Abschnitts Sprache und Region der Profilseite des Benutzers](media/ae5f565d-c932-43dd-9dc3-87630cee3692.png)

## <a name="using-the-corecreatecontenttypes-sample-app"></a>Verwenden die Core.CreateContentTypes Beispiel-app
<a name="sectionSection1"> </a>

Beim Ausführen dieses Codebeispiel zeigt eine Konsolenanwendung, wie in Abbildung 4 dargestellt. Sie müssen die Website für die Lokalisierung von und der Office 365-Administrator-Anmeldeinformationen angeben. Wenn die Konsolenanwendung ausgeführt wird, führt die **Main** -Methode in Program.cs die folgenden Aufgaben aus:

- Ruft die **CreateContentTypeIfDoesNotExist** -Methode, um einen Inhaltstyp namens **"Contoso" Dokument**erstellen.
    
- Ruft die **CreateSiteColumn** -Methode, um eine Websitespalte namens **"Contoso" Zeichenfolge**zu erstellen.
    
- Ruft die **AddSiteColumnToContentType** -Methode, um die **Zeichenfolge Contoso** Websitespalte **Contoso Document** -Inhaltstyp zu verknüpfen.
    
- Ruft die **CreateCustomList** -Methode zum Erstellen einer neuen Liste **MyList**aufgerufen.

**Abbildung 4. Core.CreateContentTypes Konsolenanwendung**

![Screenshot der Konsole Core.CreateContentTypes Anwendung](media/ee806481-0089-4c65-8f8b-027bfff6ddb9.png)

Die **Main** -Methode ruft dann die Methoden **LocalizeSiteAndList** und **LocalizeContentTypeAndField** . Die **LocalizeSiteAndList** -Methode zeigt, wie die folgenden Aufgaben ausführen:

- Legen Sie unterschiedliche lokalisierte Werte für den Titel und die Beschreibung einer Website mithilfe der **SetValueForUICulture** -Methode auf die Eigenschaften **TitleResource** und **DescriptionResource** für das **Web** -Objekt.
    
- Legen Sie unterschiedliche lokalisierte Werte für den Titel und die Beschreibung einer Website mithilfe der **SetValueForUICulture** -Methode auf die Eigenschaften **TitleResource** und **DescriptionResource** für das **Web** -Objekt.
    
Die **LocalizeContentTypeAndField** -Methode zeigt, wie die folgenden Aufgaben ausführen:

- Legen Sie unterschiedliche lokalisierte Werte für den Namen und die Beschreibung eines Inhaltstyps mithilfe der **SetValueForUICulture** -Methode auf die Eigenschaften **NameResource** und **DescriptionResource** im **ContentType** -Objekt.
    
- Legen Sie andere lokalisierte Werte für den Titel und die Beschreibung einer Website mithilfe der **SetValueForUICulture** -Methode auf die **TitleResource** und **DescriptionResource** -Eigenschaften auf das **Field** -Objekt.
    
**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.

```C#
private static void LocalizeSiteAndList(ClientContext cc, Web web)
        {
            // Localize the site title.
            web.TitleResource.SetValueForUICulture("en-US", "Hello World");
            web.TitleResource.SetValueForUICulture("fi-FI", "Hello World - Finnish");
            web.TitleResource.SetValueForUICulture("fr-FR", "Hello World - French");
            // Localize the site description.
            web.DescriptionResource.SetValueForUICulture("en-US", "Hello World site sample");
            web.DescriptionResource.SetValueForUICulture("fi-FI", " Hello World site sample - Finnish");
            web.DescriptionResource.SetValueForUICulture("fr-FR", " Hello World site sample - French");
            web.Update();
            cc.ExecuteQuery();

            // Localize the custom list that was created previously.
            List list = cc.Web.Lists.GetByTitle("MyList");
            cc.Load(list);
            cc.ExecuteQuery();
            // Localize the list title.
            list.TitleResource.SetValueForUICulture("en-US", "Hello World");
            list.TitleResource.SetValueForUICulture("fi-FI", "Hello World - Finnish");
            list.TitleResource.SetValueForUICulture("fr-FR", " Hello World - French");
            // Localize the list description.
            list.DescriptionResource.SetValueForUICulture("en-US", "This example localizes a list using CSOM.");
            list.DescriptionResource.SetValueForUICulture("fi-FI", "This example localizes a list using CSOM - Finnish.");
            list.DescriptionResource.SetValueForUICulture("fr-FR", "This example localizes a list using CSOM - French.");
            list.Update();
            cc.ExecuteQuery();
        }

private static void LocalizeContentTypeAndField(ClientContext cc, Web web)
        {
            ContentTypeCollection contentTypes = web.ContentTypes;
            ContentType myContentType = contentTypes.GetById("0x0101009189AB5D3D2647B580F011DA2F356FB2");
            cc.Load(contentTypes);
            cc.Load(myContentType);
            cc.ExecuteQuery();
            // Localize content type name.
            myContentType.NameResource.SetValueForUICulture("en-US", "Contoso Document");
            myContentType.NameResource.SetValueForUICulture("fi-FI", "Contoso Document - Finnish");
            myContentType.NameResource.SetValueForUICulture("fr-FR", "Contoso Document - French");
            // Localize content type description.
            myContentType.DescriptionResource.SetValueForUICulture("en-US", "This is the Contoso Document.");
            myContentType.DescriptionResource.SetValueForUICulture("fi-FI", " This is the Contoso Document - Finnish.");
            myContentType.DescriptionResource.SetValueForUICulture("fr-FR", " This is the Contoso Document - French.");
            myContentType.Update(true);
            cc.ExecuteQuery();

            // Localize the site column.
            FieldCollection fields = web.Fields;
            Field fld = fields.GetByInternalNameOrTitle("ContosoString");
            // Localize site column title.
            fld.TitleResource.SetValueForUICulture("en-US", "Contoso String");
            fld.TitleResource.SetValueForUICulture("fi-FI", "Contoso String - Finnish");
            fld.TitleResource.SetValueForUICulture("fr-FR", "Contoso String - French");
            // Localize site column description.
            fld.DescriptionResource.SetValueForUICulture("en-US", "Used to store Contoso specific metadata.");
            fld.DescriptionResource.SetValueForUICulture("fi-FI", "Used to store Contoso specific metadata - Finnish.");
            fld.DescriptionResource.SetValueForUICulture("fr-FR", "Used to store Contoso specific metadata - French.");
            fld.UpdateAndPushChanges(true);
            cc.ExecuteQuery();
        }
```

Wie in Abbildung 5 gezeigt, zeigt Ihre Website Ihrer benutzerdefinierten französischen Titel **"Hello World"-Französisch**, der mit der **LocalizeSiteAndList** -Methode festgelegt wurde.

**Abbildung 5. Angepasste Seitentitel aktualisiert, indem die LocalizeSiteAndList-Methode**

![Screenshot des Titels aktualisierte angepasste Seite](media/14471283-f7b6-49ca-a507-a3e28e43ee22.png)

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Lokalisierung Lösungen für SharePoint 2013 und SharePoint Online](localization-solutions-for-sharepoint-2013-and-sharepoint-online.md)
    
-  [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes)
    
-  [Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
