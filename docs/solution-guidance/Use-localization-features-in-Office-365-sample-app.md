---
title: Lokalisierung-Features in Office 365 Beispiel-add-in verwenden
ms.date: 11/03/2017
ms.openlocfilehash: e3f6644f841f53b8e62e95ed626477aef0b0ac6b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="use-localization-features-in-office-365-sample-add-in"></a><span data-ttu-id="a7106-102">Lokalisierung-Features in Office 365 Beispiel-add-in verwenden</span><span class="sxs-lookup"><span data-stu-id="a7106-102">Use localization features in Office 365 sample add-in</span></span>

<span data-ttu-id="a7106-103">Die Lokalisierungsfeatures können in Office 365 Sie lokalisierte Werte für SharePoint-Websites, Listen, Inhaltstypen und Websitespalten bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="a7106-103">You can use the localization features in Office 365 to provide localized values for SharePoint sites, lists, content types, and site columns.</span></span> 
    
<span data-ttu-id="a7106-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="a7106-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="a7106-105">Das [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) -Beispiel zeigt, wie Sie mit der Lokalisierungsfeatures von Office 365 für Websites, Listen, Inhaltstypen und Websitespalten.</span><span class="sxs-lookup"><span data-stu-id="a7106-105">The [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) sample shows you how to use the localization features of Office 365 on sites, lists, content types, and site columns.</span></span> <span data-ttu-id="a7106-106">In diesem Codebeispiel verwendet eine Konsolenanwendung, folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="a7106-106">This code sample uses a console application to do the following:</span></span>

- <span data-ttu-id="a7106-107">Erstellen von Inhaltstypen, Websitespalten und Listen und Inhaltstypen Websitespalten zuordnen.</span><span class="sxs-lookup"><span data-stu-id="a7106-107">Create content types, site columns, and lists, and associate site columns with content types.</span></span>
    
- <span data-ttu-id="a7106-108">Lokalisieren Sie den Inhaltstyp, Websitespalte, Listen- und eine benutzerdefinierte Website.</span><span class="sxs-lookup"><span data-stu-id="a7106-108">Localize the content type, site column, list, and a user-supplied site.</span></span>

> [!NOTE] 
> <span data-ttu-id="a7106-109">In diesem Artikel beschriebenen Lokalisierungsfeatures sind sind nur verfügbar in Office 365.</span><span class="sxs-lookup"><span data-stu-id="a7106-109">The localization features described in this article are only available in Office 365.</span></span> <span data-ttu-id="a7106-110">Informationen über die Lokalisierungsfeatures, die in Office 365 dedizierter oder SharePoint Server 2013: lokal verfügbar sind, finden Sie unter [How to: Localize-add-ins for SharePoint](http://msdn.microsoft.com/library/907a9189-7ce3-469a-8c87-4cef26f03c73.aspx) und [Lokalisieren von SharePoint-Lösungen](https://msdn.microsoft.com/en-us/library/ee696750.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7106-110">For information about the localization features that are available in Office 365 Dedicated or SharePoint Server 2013 on-premises, see  [How to: Localize add-ins for SharePoint](http://msdn.microsoft.com/library/907a9189-7ce3-469a-8c87-4cef26f03c73.aspx) and [Localizing SharePoint solutions](https://msdn.microsoft.com/en-us/library/ee696750.aspx).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a7106-111">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="a7106-111">Before you begin</span></span>
<span data-ttu-id="a7106-112"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="a7106-112"></span></span>

<span data-ttu-id="a7106-113">Laden Sie Sie zuerst [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="a7106-113">To get started, download the  [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="a7106-114">Bevor Sie dieses Codebeispiel ausführen:</span><span class="sxs-lookup"><span data-stu-id="a7106-114">Before you run this code sample:</span></span>

1. <span data-ttu-id="a7106-115">Konfigurieren Sie die Language-Einstellungen auf Ihrer Website ein.</span><span class="sxs-lookup"><span data-stu-id="a7106-115">Configure the language settings on your site.</span></span> <span data-ttu-id="a7106-116">Dazu:</span><span class="sxs-lookup"><span data-stu-id="a7106-116">To do this:</span></span>
    
      <span data-ttu-id="a7106-117">ein.</span><span class="sxs-lookup"><span data-stu-id="a7106-117">a.</span></span> <span data-ttu-id="a7106-118">Wählen Sie auf der Teamwebsite **Einstellungen** > **websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="a7106-118">On your team site, choose  **Settings** > **Site settings**.</span></span>
    
      <span data-ttu-id="a7106-119">b.</span><span class="sxs-lookup"><span data-stu-id="a7106-119">b.</span></span> <span data-ttu-id="a7106-120">Wählen Sie in der **Die Verwaltung von** **spracheinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="a7106-120">In  **Site Administration**, choose  **Language settings**.</span></span>
    
      <span data-ttu-id="a7106-121">c.</span><span class="sxs-lookup"><span data-stu-id="a7106-121">c.</span></span> <span data-ttu-id="a7106-122">Wählen Sie auf der Seite **Spracheinstellungen** im **alternative Sprache(n)**, die alternativen Sprachen, die Ihre Website unterstützt werden soll.</span><span class="sxs-lookup"><span data-stu-id="a7106-122">On the  **Language Settings** page, in **Alternate language(s)**, choose the alternate languages your site should support.</span></span> <span data-ttu-id="a7106-123">Sie können beispielsweise Französisch und Finnisch, auswählen, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="a7106-123">For example, you can choose French and Finnish, as shown in Figure 1.</span></span>
    
      <span data-ttu-id="a7106-124">d.</span><span class="sxs-lookup"><span data-stu-id="a7106-124">d.</span></span> <span data-ttu-id="a7106-125">Wählen Sie  **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="a7106-125">Choose  **OK**.</span></span>
     
2. <span data-ttu-id="a7106-126">Legen Sie die Anzeigesprache auf der Profilseite des Benutzers an.</span><span class="sxs-lookup"><span data-stu-id="a7106-126">Set the display language on your user's profile page.</span></span> <span data-ttu-id="a7106-127">Dazu:</span><span class="sxs-lookup"><span data-stu-id="a7106-127">To do this:</span></span>
    
      <span data-ttu-id="a7106-128">ein.</span><span class="sxs-lookup"><span data-stu-id="a7106-128">a.</span></span> <span data-ttu-id="a7106-129">Am oberen Rand der Office 365-Website wählen Sie Ihr Profilbild aus, und wählen Sie **über mich**, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="a7106-129">At the top of your Office 365 site, choose your profile picture, and then choose  **About me**, as shown in Figure 2.</span></span>
    
      <span data-ttu-id="a7106-130">b.</span><span class="sxs-lookup"><span data-stu-id="a7106-130">b.</span></span> <span data-ttu-id="a7106-131">Wählen Sie auf der Seite **über mich** **Mein Profil bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="a7106-131">On the  **About me** page, choose **Edit your profile**.</span></span>
    
      <span data-ttu-id="a7106-132">c.</span><span class="sxs-lookup"><span data-stu-id="a7106-132">c.</span></span> <span data-ttu-id="a7106-133">Wählen Sie **...** (Weitere Optionen), und klicken Sie dann auf **Sprache und Region**.</span><span class="sxs-lookup"><span data-stu-id="a7106-133">Choose  **...** (additional options), and then choose **Language and Region**.</span></span>
    
      <span data-ttu-id="a7106-134">d.</span><span class="sxs-lookup"><span data-stu-id="a7106-134">d.</span></span> <span data-ttu-id="a7106-135">Wählen Sie in **Meine Anzeigesprachen**, eine neue Sprache, die Sie auf der Website mit der Dropdownliste **Wählen Sie eine neue Sprache** festlegen ähnelt wählen Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="a7106-135">In  **My Display Languages**, choose a new language similar to the one you set on the site using the  **Pick a new language** dropdown, then choose **Add**.</span></span> <span data-ttu-id="a7106-136">Wählen Sie beispielsweise Französisch und Finnisch, wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="a7106-136">For example, choose French and Finnish, as shown in Figure 3.</span></span> <span data-ttu-id="a7106-137">Sie können die gewünschte Sprache nach oben oder unten verschieben, indem Sie auf den Pfeil nach oben und nach unten weisenden Pfeil.</span><span class="sxs-lookup"><span data-stu-id="a7106-137">You can move your preferred language up or down by choosing the up and down arrows.</span></span>
    
      <span data-ttu-id="a7106-138">e.</span><span class="sxs-lookup"><span data-stu-id="a7106-138">e.</span></span> <span data-ttu-id="a7106-139">Wählen Sie **Speichern und schließen**.</span><span class="sxs-lookup"><span data-stu-id="a7106-139">Choose  **Save all and close**.</span></span>

> [!NOTE] 
> <span data-ttu-id="a7106-140">Es kann für Ihre Website, um die ausgewählten Sprache(n) Rendern ein paar Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="a7106-140">It might take a few minutes for your site to render in the selected language(s).</span></span> 

<span data-ttu-id="a7106-141">**Abbildung 1. Spracheinstellungen für eine Website**</span><span class="sxs-lookup"><span data-stu-id="a7106-141">**Figure 1. Language settings for a site**</span></span>

![Screenshot, der die spracheinstellungen für eine Website anzeigt.](media/ffe149ae-17ab-4c55-a611-d47f4eb88c4e.png)

<span data-ttu-id="a7106-143">**Abbildung 2. Navigieren zu Profilseite des Benutzers über mich auswählen**</span><span class="sxs-lookup"><span data-stu-id="a7106-143">**Figure 2. Navigating to a user's profile page by choosing About me**</span></span>

![Screenshot der Benutzerprofilseite mit über mich hervorgehoben](media/764b2ac2-155b-4ce9-b8eb-3ae04ad26593.png)

<span data-ttu-id="a7106-145">**Abbildung 3. Ändern eines Benutzers anzeigen Sprachoptionen auf der Profilseite des Benutzers**</span><span class="sxs-lookup"><span data-stu-id="a7106-145">**Figure 3. Changing a user's display language settings on the user's profile page**</span></span>

![Screenshot des Abschnitts Sprache und Region der Profilseite des Benutzers](media/ae5f565d-c932-43dd-9dc3-87630cee3692.png)

## <a name="using-the-corecreatecontenttypes-sample-app"></a><span data-ttu-id="a7106-147">Verwenden die Core.CreateContentTypes Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="a7106-147">Using the Core.CreateContentTypes sample app</span></span>
<span data-ttu-id="a7106-148"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="a7106-148"></span></span>

<span data-ttu-id="a7106-149">Beim Ausführen dieses Codebeispiel zeigt eine Konsolenanwendung, wie in Abbildung 4 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="a7106-149">When you run this code sample, a console application displays, as shown in Figure 4.</span></span> <span data-ttu-id="a7106-150">Sie müssen die Website für die Lokalisierung von und der Office 365-Administrator-Anmeldeinformationen angeben.</span><span class="sxs-lookup"><span data-stu-id="a7106-150">You need to supply the site to localize, and your Office 365 administrator's credentials.</span></span> <span data-ttu-id="a7106-151">Wenn die Konsolenanwendung ausgeführt wird, führt die **Main** -Methode in Program.cs die folgenden Aufgaben aus:</span><span class="sxs-lookup"><span data-stu-id="a7106-151">When the console application runs, the  **Main** method in Program.cs performs the following tasks:</span></span>

- <span data-ttu-id="a7106-152">Ruft die **CreateContentTypeIfDoesNotExist** -Methode, um einen Inhaltstyp namens **"Contoso" Dokument**erstellen.</span><span class="sxs-lookup"><span data-stu-id="a7106-152">Calls the  **CreateContentTypeIfDoesNotExist** method to create a content type called **Contoso Document**.</span></span>
    
- <span data-ttu-id="a7106-153">Ruft die **CreateSiteColumn** -Methode, um eine Websitespalte namens **"Contoso" Zeichenfolge**zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="a7106-153">Calls the  **CreateSiteColumn** method to create a site column called **Contoso String**.</span></span>
    
- <span data-ttu-id="a7106-154">Ruft die **AddSiteColumnToContentType** -Methode, um die **Zeichenfolge Contoso** Websitespalte **Contoso Document** -Inhaltstyp zu verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="a7106-154">Calls the  **AddSiteColumnToContentType** method to link the **Contoso String** site column to the **Contoso Document** content type.</span></span>
    
- <span data-ttu-id="a7106-155">Ruft die **CreateCustomList** -Methode zum Erstellen einer neuen Liste **MyList**aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="a7106-155">Calls the  **CreateCustomList** method to create a new list called **MyList**.</span></span>

<span data-ttu-id="a7106-156">**Abbildung 4. Core.CreateContentTypes Konsolenanwendung**</span><span class="sxs-lookup"><span data-stu-id="a7106-156">**Figure 4. Core.CreateContentTypes console application**</span></span>

![Screenshot der Konsole Core.CreateContentTypes Anwendung](media/ee806481-0089-4c65-8f8b-027bfff6ddb9.png)

<span data-ttu-id="a7106-158">Die **Main** -Methode ruft dann die Methoden **LocalizeSiteAndList** und **LocalizeContentTypeAndField** .</span><span class="sxs-lookup"><span data-stu-id="a7106-158">The  **Main** method then calls the **LocalizeSiteAndList** and **LocalizeContentTypeAndField** methods.</span></span> <span data-ttu-id="a7106-159">Die **LocalizeSiteAndList** -Methode zeigt, wie die folgenden Aufgaben ausführen:</span><span class="sxs-lookup"><span data-stu-id="a7106-159">The **LocalizeSiteAndList** method shows you how to do the following:</span></span>

- <span data-ttu-id="a7106-160">Legen Sie unterschiedliche lokalisierte Werte für den Titel und die Beschreibung einer Website mithilfe der **SetValueForUICulture** -Methode auf die Eigenschaften **TitleResource** und **DescriptionResource** für das **Web** -Objekt.</span><span class="sxs-lookup"><span data-stu-id="a7106-160">Set different localized values for the title and description of a site, by using the  **SetValueForUICulture** method on the **TitleResource** and **DescriptionResource** properties on the **Web** object.</span></span>
    
- <span data-ttu-id="a7106-161">Legen Sie unterschiedliche lokalisierte Werte für den Titel und die Beschreibung einer Website mithilfe der **SetValueForUICulture** -Methode auf die Eigenschaften **TitleResource** und **DescriptionResource** für das **Web** -Objekt.</span><span class="sxs-lookup"><span data-stu-id="a7106-161">Set different localized values for the title and description of a site, by using the  **SetValueForUICulture** method on the **TitleResource** and **DescriptionResource** properties on the **Web** object.</span></span>
    
<span data-ttu-id="a7106-162">Die **LocalizeContentTypeAndField** -Methode zeigt, wie die folgenden Aufgaben ausführen:</span><span class="sxs-lookup"><span data-stu-id="a7106-162">The  **LocalizeContentTypeAndField** method shows you how to do the following:</span></span>

- <span data-ttu-id="a7106-163">Legen Sie unterschiedliche lokalisierte Werte für den Namen und die Beschreibung eines Inhaltstyps mithilfe der **SetValueForUICulture** -Methode auf die Eigenschaften **NameResource** und **DescriptionResource** im **ContentType** -Objekt.</span><span class="sxs-lookup"><span data-stu-id="a7106-163">Set different localized values for the name and description of a content type, by using the  **SetValueForUICulture** method on the **NameResource** and **DescriptionResource** properties on the **ContentType** object.</span></span>
    
- <span data-ttu-id="a7106-164">Legen Sie andere lokalisierte Werte für den Titel und die Beschreibung einer Website mithilfe der **SetValueForUICulture** -Methode auf die **TitleResource** und **DescriptionResource** -Eigenschaften auf das **Field** -Objekt.</span><span class="sxs-lookup"><span data-stu-id="a7106-164">Set different localized values for the title and description of a site, by using the  **SetValueForUICulture** method on the **TitleResource** and **DescriptionResource** properties on the **Field** object.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="a7106-165">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="a7106-165">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="a7106-166">Wie in Abbildung 5 gezeigt, zeigt Ihre Website Ihrer benutzerdefinierten französischen Titel **"Hello World"-Französisch**, der mit der **LocalizeSiteAndList** -Methode festgelegt wurde.</span><span class="sxs-lookup"><span data-stu-id="a7106-166">As shown in Figure 5, your site displays your custom French title  **Hello World - French**, which was set using the  **LocalizeSiteAndList** method.</span></span>

<span data-ttu-id="a7106-167">**Abbildung 5. Angepasste Seitentitel aktualisiert, indem die LocalizeSiteAndList-Methode**</span><span class="sxs-lookup"><span data-stu-id="a7106-167">**Figure 5. Customized page title updated by the LocalizeSiteAndList method**</span></span>

![Screenshot des Titels aktualisierte angepasste Seite](media/14471283-f7b6-49ca-a507-a3e28e43ee22.png)

## <a name="see-also"></a><span data-ttu-id="a7106-169">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="a7106-169">See also</span></span>
<span data-ttu-id="a7106-170"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a7106-170"></span></span>

-  [<span data-ttu-id="a7106-171">Lokalisierung Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a7106-171">Localization solutions for SharePoint 2013 and SharePoint Online</span></span>](localization-solutions-for-sharepoint-2013-and-sharepoint-online.md)
    
-  [<span data-ttu-id="a7106-172">Core.CreateContentTypes</span><span class="sxs-lookup"><span data-stu-id="a7106-172">Core.CreateContentTypes</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes)
    
-  [<span data-ttu-id="a7106-173">Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a7106-173">Enterprise content management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
