---
title: "Erstellen eines von einem Anbieter gehosteten Add-Ins, das eine benutzerdefinierte SharePoint-Liste und einen benutzerdefinierten Inhaltstyp enthält"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: e5dacf516a3569b2dd38cdbe1936e6c874cb0556
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type"></a><span data-ttu-id="ffad3-102">Erstellen eines von einem Anbieter gehosteten Add-Ins, das eine benutzerdefinierte SharePoint-Liste und einen benutzerdefinierten Inhaltstyp enthält</span><span class="sxs-lookup"><span data-stu-id="ffad3-102">Create a provider-hosted add-in that includes a custom SharePoint list and content type</span></span>
<span data-ttu-id="ffad3-p101">Erstellen Sie ein SharePoint-Add-In, das eine in der Cloud gehostete Webanwendung mit benutzerdefinierten, in SharePoint gehosteten Listenvorlagen, Listeninstanzen und benutzerdefinierten Inhaltstypen unter Verwendung der Office Developer Tools für Visual Studio 2012 kombiniert. In diesem Artikel erfahren Sie, wie Sie mit SharePoint-Add-In-Webs interagieren, indem Sie den REST/OData-Webdienst verwenden, und wie Sie OAuth in einem SharePoint-Add-In implementieren.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p101">Create a SharePoint Add-in that combines a cloud-hosted web application with custom SharePoint-hosted list templates, list instances, and custom content types by using the Office Developer Tools for Visual Studio 2012. Learn how to interact with SharePoint add-in webs by using the REST/OData web service, and how to implement OAuth in a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="ffad3-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="ffad3-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="ffad3-p103">Die meisten klassischen SharePoint-Komponenten, wie benutzerdefinierte Inhaltstypen, benutzerdefinierte Listendefinitionen und Workflows, können einem in der Cloud gehosteten SharePoint-Add-In hinzugefügt werden. Das einfache Beispiel in diesem Artikel enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="ffad3-p103">Most classic SharePoint components, such as custom content types, custom list definitions, and workflows, can be included in a cloud-hosted SharePoint Add-in. The simple example in this article contains the following:</span></span>
 

- <span data-ttu-id="ffad3-110">Add-In-Webs mit</span><span class="sxs-lookup"><span data-stu-id="ffad3-110">An add-in web with</span></span>
    
      - <span data-ttu-id="ffad3-111">einigen benutzerdefinierten Websitespalten</span><span class="sxs-lookup"><span data-stu-id="ffad3-111">some custom site columns</span></span>
    
 
  - <span data-ttu-id="ffad3-112">einem benutzerdefinierten Inhaltstyp, der die benutzerdefinierten Spalten verwendet</span><span class="sxs-lookup"><span data-stu-id="ffad3-112">a custom content type that uses the custom columns</span></span>
    
 
  - <span data-ttu-id="ffad3-113">einer benutzerdefinierten Listenvorlage, die den benutzerdefinierten Inhaltstyp verwendet</span><span class="sxs-lookup"><span data-stu-id="ffad3-113">a custom list template that uses the custom content type</span></span>
    
 
  - <span data-ttu-id="ffad3-114">einer Listeninstanz auf Grundlage der benutzerdefinierten Listendefinition</span><span class="sxs-lookup"><span data-stu-id="ffad3-114">a list instance based on the custom list definition</span></span>
    
 
- <span data-ttu-id="ffad3-115">Eine ASP.NET-Webanwendung, die Daten aus der Listeninstanz liest</span><span class="sxs-lookup"><span data-stu-id="ffad3-115">An ASP.NET web application that reads data from the list instance</span></span>
    
 

## <a name="prerequisites-for-creating-this-sharepoint-add-in"></a><span data-ttu-id="ffad3-116">Voraussetzungen zum Erstellen dieses SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="ffad3-116">Prerequisites for creating this SharePoint Add-in</span></span>
<span data-ttu-id="ffad3-117"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="ffad3-117"></span></span>


-  <span data-ttu-id="ffad3-118">[Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682) oder höher.</span><span class="sxs-lookup"><span data-stu-id="ffad3-118">[Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682) or later.</span></span>
    
 
-  [<span data-ttu-id="ffad3-119">Office Developer Tools</span><span class="sxs-lookup"><span data-stu-id="ffad3-119">Office Developer Tools</span></span>](https://msdn.microsoft.com/de-DE/office/aa905340.aspx)
    
 
- <span data-ttu-id="ffad3-120">Eine SharePoint- Installation zum Testen und Debuggen</span><span class="sxs-lookup"><span data-stu-id="ffad3-120">A SharePoint installation for testing and debugging</span></span>
    
      - <span data-ttu-id="ffad3-p104">Diese Komponenten können sich auf dem selben Computer befinden, den Sie als Entwicklungscomputer verwenden. Sie können die Entwicklung jedoch auch mit einer Remoteinstallation von SharePoint durchführen. Wenn Sie mit einer Remoteinstallation arbeiten, müssen Sie das Clientobjektmodell so installieren, dass es für das Clientobjektmodell auf der Zielinstallation verteilbar ist. Es ist als verteilbares Paket im Microsoft Download Center verfügbar. Suchen Sie nach "SDKs für SharePoint Server 2013-Clientkomponenen" oder "SKDs für SharePoint Online-Clientkomponenten".</span><span class="sxs-lookup"><span data-stu-id="ffad3-p104">This can be on the same computer as your development computer, or you can develop with a remote SharePoint installation. If you work with a remote installation, you need to install the client object model redistributable on the target installation. It is available as a redistributable package on the Microsoft Download Center. Search for "SharePoint Server 2013 Client Components SDK" or "SharePoint Online Client Components SDK".</span></span> 
    
 
  - <span data-ttu-id="ffad3-125">Die SharePoint-Testwebsite muss aus der Websitedefinition der **Entwicklerwebsite** (die Sie in der Zentraladministration erstellen können) erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="ffad3-125">The test SharePoint website must be created from the  **Developer Site** site definition (which you can create in Central Administration).</span></span>
    
 
  - <span data-ttu-id="ffad3-p105">Ihre Remote-Webanwendung kommuniziert mit der Add-In-Website entweder über JavaScript und die domänenübergreifende  [-Bibliothek](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md) oder über [OAuth](authorization-and-authentication-of-sharepoint-add-ins.md). Wenn OAuth verwendet wird, wie im fortlaufenden Beispiel in diesem Artikel, muss die SharePoint-Installation für die Verwendung von OAuth konfiguriert sein.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p105">Your remote web application communicates with the add-in web by using either JavaScript and the  [cross-domain library](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md) or [OAuth](authorization-and-authentication-of-sharepoint-add-ins.md). If OAuth is used, as it is in the continuing example of this article, the SharePoint installation must be configured to use OAuth.</span></span>
    
 

 <span data-ttu-id="ffad3-128">**Hinweis** Anweisungen zum Einrichten einer Entwicklungsumgebung, die Ihren Anforderungen entspricht, finden Sie unter [Erste Schritte beim Erstellen von Add-Ins für Office und SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span><span class="sxs-lookup"><span data-stu-id="ffad3-128">**Note**  For guidance on how to setup a development environment that fits your needs, see  [Start building Office and SharePoint Add-ins](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span></span>
 


### <a name="core-concepts-to-know-for-creating-an-add-in"></a><span data-ttu-id="ffad3-129">Wichtige Kernkonzepte für die Erstellung eines Add-Ins</span><span class="sxs-lookup"><span data-stu-id="ffad3-129">Core concepts to know for creating an add-in</span></span>

<span data-ttu-id="ffad3-130">Bevor Sie Ihr erstes Add-In erstellen, sollten Sie grundsätzlich wissen, was SharePoint-Add-Ins sind, und die Unterschiede zwischen in SharePoint gehosteten und in der Cloud gehosteten SharePoint-Add-Ins kennen. Die Artikel in Tabelle 1 vermitteln Ihnen dieses Wissen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-130">Before you create your first add-in, you should have a basic understanding of what SharePoint Add-ins are and the differences between SharePoint-hosted and cloud-hosted SharePoint Add-ins. The articles in Table 1 should give you that understanding.</span></span>
 

 

<span data-ttu-id="ffad3-131">**Tabelle 1. Kernkonzepte für die Erstellung eines Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="ffad3-131">**Table 1. Core concepts for creating an add-in**</span></span>


|<span data-ttu-id="ffad3-132">**Titel des Artikels**</span><span class="sxs-lookup"><span data-stu-id="ffad3-132">**Article title**</span></span>|<span data-ttu-id="ffad3-133">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ffad3-133">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="ffad3-134">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="ffad3-134">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)|<span data-ttu-id="ffad3-135">Hier finden Sie Informationen über das neue Add-In-Modell in SharePoint, das es Ihnen ermöglicht, Add-Ins als kompakte, einfach zu verwendende Lösungen für Endbenutzer zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-135">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>|
| [<span data-ttu-id="ffad3-136">Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="ffad3-136">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md)|<span data-ttu-id="ffad3-137">Hier finden Sie Informationen über Aspekte der Architektur von SharePoint-Add-Ins und das Modell für SharePoint-Add-Ins, einschließlich Add-In-Hostingoptionen, Benutzeroberflächenoptionen, Bereitstellungssystem, Sicherheitssystem und Lebenszyklus.</span><span class="sxs-lookup"><span data-stu-id="ffad3-137">Learn about aspects of the architecture of SharePoint Add-ins and the model for SharePoint Add-ins, including the add-in hosting options, user interface (UI) options, deployment system, security system, and life cycle.</span></span>|
| [<span data-ttu-id="ffad3-138">Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="ffad3-138">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md)|<span data-ttu-id="ffad3-139">Hier finden Sie Informationen über die verschiedenen Möglichkeiten zum Hosten von SharePoint-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="ffad3-139">Learn about the various ways that you can host SharePoint Add-ins.</span></span>|

## <a name="develop-the-sharepoint-add-in"></a><span data-ttu-id="ffad3-140">Entwickeln des SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="ffad3-140">Develop the SharePoint Add-in</span></span>
<span data-ttu-id="ffad3-141"><a name="Develop"> </a></span><span class="sxs-lookup"><span data-stu-id="ffad3-141"></span></span>

 <span data-ttu-id="ffad3-142">Mit den Schritten in diesem Abschnitt erstellen Sie auf Ihrem Entwicklungscomputer ein SharePoint-Add-In, das eine Add-In-Website mit SharePoint-Komponenten und eine Remote-Webanwendung umfasst.</span><span class="sxs-lookup"><span data-stu-id="ffad3-142">In the procedures of this section, you create a SharePoint Add-in that includes an add-in web with SharePoint components and a remote web application on your development machine.</span></span>
 

 

### <a name="to-set-up-the-visual-studio-2012-solution-and-its-elements"></a><span data-ttu-id="ffad3-143">So richten Sie die Visual Studio 2012-Projektmappe und ihre Elemente ein</span><span class="sxs-lookup"><span data-stu-id="ffad3-143">To set up the Visual Studio 2012 solution and its elements</span></span>


1. <span data-ttu-id="ffad3-p106">Erstellen Sie in Visual Studio 2012 ein **SharePoint-Add-In**-Projekt im Knoten **Office SharePoint | Add-Ins** (entweder unter **C#** oder **Visual Basic**) in der Vorlagenstruktur des Assistenten **Neues Projekt**. Wählen Sie die Hostingoption **Von Anbieter gehostet** aus. Im fortlaufenden Beispiel dieses Artikels wird C# als Sprache verwendet, und „LocalTheater“ ist der Projektname.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p106">In Visual Studio 2012, create an  **Add-in for SharePoint** project from the **Office SharePoint | Add-ins** node (under either **C#** or **Visual Basic**) in the templates tree of the  **New Project** wizard. Choose the **Provider-hosted** hosting option. In the continuing example of this article, C# is used as the language andLocalTheater is the project name.</span></span>
    
 
2. <span data-ttu-id="ffad3-147">Wählen Sie **Fertig stellen** im Assistenten aus.</span><span class="sxs-lookup"><span data-stu-id="ffad3-147">Choose  **Finish** in the wizard.</span></span>
    
 
3. <span data-ttu-id="ffad3-p107">Öffnen Sie im Manifest-Designer die Datei „AppManifest.xml“. Für das **Title**-Element wird der Projektname als Standardwert angezeigt. Ersetzen Sie ihn durch einen griffigeren Namen, denn dies ist der Name des Add-Ins, den der Benutzer in der Benutzeroberfläche sieht.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p107">Open the AppManifest.xml file in the manifest designer. The  **Title** element has the project name as its default value. Replace it with something more friendly because this is the name of the add-in that users see in the UI.</span></span>
    
 
4. <span data-ttu-id="ffad3-p108">Geben Sie für **Name** einen Namen für das Add-In ein. Es handelt sich um einen internen Namen, der nur ASCII-Zeichen und keine Leerzeichen enthalten darf, wie z. B. „LocalTheater“.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p108">Specify a  **Name** for the add-in. This is an internal name that must contain only ASCII characters and must contain no spaces; for example,LocalTheater.</span></span>
    
 
5. <span data-ttu-id="ffad3-153">Öffnen Sie die Datei „Web.config“ im Webanwendungsprojekt, und fügen Sie das Element `<customErrors mode="Off"/>` dem Element **system.web** hinzu.</span><span class="sxs-lookup"><span data-stu-id="ffad3-153">Open the Web.config file in the web application project and add the element  `<customErrors mode="Off"/>` to the **system.web** element.</span></span>
    
 
6. <span data-ttu-id="ffad3-p109">Stellen Sie sicher, dass im Webanwendungsprojekt Verweise auf die folgenden Assemblys vorhanden sind. (Falls in Ihrer Edition von Visual Studio 2012 die Verweise nicht automatisch hinzugefügt wurden, fügen Sie sie jetzt hinzu.)</span><span class="sxs-lookup"><span data-stu-id="ffad3-p109">Check to see that references to the following assemblies are in the web application project. (If your edition of Visual Studio 2012 did not add the references automatically, then add them now.)</span></span>
    
      -  <span data-ttu-id="ffad3-p110">**Microsoft.IdentityModel.dll** Diese Assembly wird im globalen Assemblycache mit Windows Identity Foundation (WIF) installiert. Da es sich um eine .NET Framework 3.5-Assembly handelt, wird sie standardmäßig aus dem **Framework** des Dialogfelds **Verweis hinzufügen** herausgefiltert. Sie können einen Verweis auf sie hinzufügen, indem Sie direkt zum Verzeichnis `C:\Program Files\Reference Assemblies\Microsoft\Windows Identity Foundation\v3.5` Ihres Entwicklungscomputers navigieren.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p110">**Microsoft.IdentityModel.dll** This assembly is installed into the global assembly cache with Windows Identity Foundation (WIF). Because this is a .NET Framework 3.5 assembly, it is filtered out of the **Framework** node of the **Add Reference** dialog box by default. You can add a reference to it by browsing directly to the `C:\Program Files\Reference Assemblies\Microsoft\Windows Identity Foundation\v3.5` directory of your development computer.</span></span>
    
 
  -  <span data-ttu-id="ffad3-159">**Microsoft.IdentityModel.Extensions.dll** Sie können einen Verweis darauf hinzufügen, indem Sie direkt zum Ordner `C:\Program Files\Reference Assemblies\Microsoft\Microsoft Identity Extensions\1.0` Ihres Entwicklungscomputers navigieren.</span><span class="sxs-lookup"><span data-stu-id="ffad3-159">**Microsoft.IdentityModel.Extensions.dll** You can add a reference to it by browsing directly to the `C:\Program Files\Reference Assemblies\Microsoft\Microsoft Identity Extensions\1.0` folder of your development computer.</span></span>
    
 
  -  <span data-ttu-id="ffad3-160">**System.IdentityModel.dll** Diese Assembly ist Teil von .NET Framework 4 und wird auf dem Knoten **Assemblies | Framework** des Dialogfelds **Verweis hinzufügen** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ffad3-160">**System.IdentityModel.dll** This assembly is part of the .NET Framework 4, and it appears on the **Assemblies | Framework** node of the **Add Reference** dialog box.</span></span>
    
 
7. <span data-ttu-id="ffad3-p111">Wenn Ihre Remotewebanwendung auf Informationen im Hostweb und im Add-In-Web zugreift, müssen Sie der Datei „AppManifest.xml“ ein **AppPermissionRequests**-Element mit einem oder mehreren untergeordneten **AppPermissionRequest**-Elementen hinzufügen. (Die Webanwendung im fortlaufenden Beispiel dieses Artikels greift nur auf das Add-In-Web zu. Add-In-Prinzipale verfügen automatisch über alle erforderlichen Berechtigungen für das Add-In-Web, sodass die Datei „AppManifest.xml“ in dem Beispiel kein **AppPermissionRequests**-Element umfasst). Weitere Informationen über Add-In-Berechtigungsanforderungen und wie sie hinzugefügt werden, finden Sie unter [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="ffad3-p111">If your remote web application accesses information in the host web as well as the add-in web, you must add an  **AppPermissionRequests** element, with one or more child **AppPermissionRequest** elements, to the AppManifest.xml file. (The web application in the continuing example of this article accesses only the add-in web. Add-in principals automatically have all permissions needed to the add-in web, so the AppManifest.xml in the example does not have an **AppPermissionRequests** element.) For more information about add-in permission requests and how to add them, see [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint.md).</span></span>
    
 

### <a name="to-add-the-sharepoint-components"></a><span data-ttu-id="ffad3-164">So fügen Sie SharePoint-Komponenten hinzu</span><span class="sxs-lookup"><span data-stu-id="ffad3-164">To add the SharePoint components</span></span>


1. <span data-ttu-id="ffad3-p112">Zum Hinzufügen von SharePoint-Komponenten zu einem Add-In gehen Sie gleich vor wie beim Hinzufügen von Komponenten zu einem klassischen Farmlösung. Es kann jedoch nicht jede Art von SharePoint-Komponente einem SharePoint-Add-In hinzugefügt werden. Die Zwecke, denen diese Komponenten dienen, werden in SharePoint-Add-Ins auf andere Weise erreicht. Ausführlichere Informationen darüber, welche Arten von SharePoint-Komponenten einem SharePoint-Add-In hinzugefügt werden können und wie sie einem Projekt hinzugefügt werden, finden Sie unter  [Typen von SharePoint-Komponenten, die in einem SharePoint-Add-In enthalten sein können](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#TypesOfSPComponentsInApps).</span><span class="sxs-lookup"><span data-stu-id="ffad3-p112">You add SharePoint components to an add-in exactly as you would add them to a classic farm solution. However, not every kind of SharePoint component can be included in a SharePoint Add-in. The purposes these components serve are accomplished in other ways in SharePoint Add-ins. For detailed information about what kinds of SharePoint components can be included in a SharePoint Add-in and how to include them in a project, see  [Types of SharePoint components that can be in a SharePoint Add-in](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#TypesOfSPComponentsInApps).</span></span>
    
    <span data-ttu-id="ffad3-p113">Verwenden Sie für das fortlaufende Beispiel die folgenden Verfahren. Diese geben Beispiele für die Verwendung von Visual Studio 2012 zum Hinzufügen von benutzerdefinierten Spalten, Inhaltstypen, Listenvorlagen und Listeninstanzen zu einem SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p113">For purposes of the continuing example, use the following procedures. These will provide examples of using Visual Studio 2012 to add custom columns, content types, list templates, and list instances to a SharePoint Add-in.</span></span>
    
### <a name="to-create-the-custom-column-types"></a><span data-ttu-id="ffad3-170">So erstellen Sie benutzerdefinierte Spaltentypen</span><span class="sxs-lookup"><span data-stu-id="ffad3-170">To create the custom column types</span></span>


1. <span data-ttu-id="ffad3-171">Fügen Sie im **Projektmappen-Explorer** ein SharePoint-Element **Websitespalte** zum SharePoint-Add-In-Projekt mit dem Namen „Actor“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="ffad3-171">In  **Solution Explorer**, add a SharePoint  **Site Column** item to the SharePoint Add-in project with the nameActor.</span></span>
    
 
2. <span data-ttu-id="ffad3-p114">Bearbeiten Sie in der Datei „elements.xml“ für die neue Websitespalte das **Field**-Element so, dass es die im folgenden Beispiel dargestellten Attribute und Werte aufweist, mit der Ausnahme, dass der Wert der GUID für das **ID**-Attribut, den Visual Studio 2012 dafür generiert hat, nicht geändert wird. Vergessen Sie nicht die umschließenden Klammern „{}“.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p114">In the elements.xml file for the new site column, edit the  **Field** element so that it has the attributes and values shown in the following example, except that you should not change the GUID for the **ID** attribute from the value Visual Studio 2012 generated for it. Don't forget the framing braces "{}".</span></span>
    
```
  <Field ID="{generated GUID}" 
       Name="Actor" 
       Title="Actor" 
       DisplayName="Actor/Actress" 
       Group="Theater and Movies" 
       Description="The person cast, perhaps tentatively, in the role" 
       Type="Text" 
/>
```

3. <span data-ttu-id="ffad3-174">Fügen Sie dem Projekt eine weitere **Websitespalte** mit dem Namen „CastingStatus“ hinzu.</span><span class="sxs-lookup"><span data-stu-id="ffad3-174">Add another  **Site Column** to the project namedCastingStatus.</span></span>
    
 
4. <span data-ttu-id="ffad3-175">Bearbeiten Sie in der Datei „elements.xml“ für die neue Websitespalte das **Field**-Element so, dass es die im folgenden Beispiel dargestellten Attribute und Werte aufweist, mit der Ausnahme, dass der Wert der GUID für das **ID**-Attribut, den Visual Studio 2012 dafür generiert hat, nicht geändert wird.</span><span class="sxs-lookup"><span data-stu-id="ffad3-175">In the elements.xml file for the new site column, edit the  **Field** element so that it has the attributes and values shown in the following example, except that you should not change the GUID for the **ID** attribute from the value Visual Studio 2012 generated for it.</span></span>
    
```
  <Field ID="{generated GUID}" 
       Name="CastingStatus" 
       Title="CastingStatus"
       DisplayName="Casting Status" 
       Group="Theater and Movies" 
       Description="The current casting status of the role" 
       Type="Choice">
</Field>
```

5. <span data-ttu-id="ffad3-p115">Weil es sich um ein Auswahlfeld handelt, müssen Sie die Auswahlmöglichkeiten, die Reihenfolge ihrer Anzeige in der Dropdownliste, wenn ein Benutzer eine Auswahl trifft, sowie die Standardauswahl angeben. Fügen Sie dem **Field**-Element das folgende untergeordnete Markup hinzu.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p115">Because this is a Choice field, you must specify the possible choices, the order in which they should appear in the drop-down list when a user is making a choice, and the default choice. Add the following child markup to the  **Field** element.</span></span>
    
```
  <CHOICES>
      <CHOICE>Not Started</CHOICE>
      <CHOICE>Audition Scheduled</CHOICE>
      <CHOICE>Auditioned</CHOICE>
      <CHOICE>Role Offered</CHOICE>
      <CHOICE>Committed to Role</CHOICE>
</CHOICES>
<MAPPINGS>
      <MAPPING Value="1">Not Started</MAPPING>
      <MAPPING Value="2">Audition Scheduled</MAPPING>
      <MAPPING Value="3">Auditioned</MAPPING>
      <MAPPING Value="4">Role Offered</MAPPING>
      <MAPPING Value="5">Committed to Role</MAPPING>
</MAPPINGS>
<Default>Not Started</Default>
```


### <a name="to-create-the-custom-content-type"></a><span data-ttu-id="ffad3-178">So erstellen Sie den benutzerdefinierten Inhaltstyp</span><span class="sxs-lookup"><span data-stu-id="ffad3-178">To create the custom content type</span></span>


1. <span data-ttu-id="ffad3-p116">Fügen Sie im **Projektmappen-Explorer** ein SharePoint-Element **Inhaltstyp** zum SharePoint-Add-In-Projekt mit dem Namen „ActingRole“ hinzu. Wenn Sie vom Assistenten dazu aufgefordert werden, den Basisinhaltstyp auszuwählen, klicken Sie auf **Element** und dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p116">In  **Solution Explorer**, add a SharePoint  **Content Type** item to the SharePoint Add-in project with the nameActingRole. When prompted by the wizard to select the base content type, choose  **Item**, and then choose  **Finish**.</span></span>
    
 
2. <span data-ttu-id="ffad3-181">Wenn der Inhaltstyp-Designer nicht automatisch geöffnet wird, wählen Sie den Inhaltstyp **ActingRole** im **Projektmappen-Explorer** aus, um ihn zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-181">If the content type designer does not automatically open, choose the  **ActingRole** content type in **Solution Explorer** to open it.</span></span>
    
 
3. <span data-ttu-id="ffad3-182">Öffnen Sie die Registerkarte **Inhaltstyp** im Designer, und füllen Sie die Textfelder wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="ffad3-182">Open the  **Content Type** tab in the designer and fill the text boxes as follows:</span></span>
    
      -  <span data-ttu-id="ffad3-183">**Inhaltstypname**: ActingRole</span><span class="sxs-lookup"><span data-stu-id="ffad3-183">**Content Type Name**: ActingRole</span></span>
    
 
  -  <span data-ttu-id="ffad3-184">**Beschreibung**: Stellt eine Rolle in einem Stück oder Film dar.</span><span class="sxs-lookup"><span data-stu-id="ffad3-184">**Description**: Represents a role in a play or movie.</span></span>
    
 
  -  <span data-ttu-id="ffad3-185">**Gruppenname**: Theater and Movies</span><span class="sxs-lookup"><span data-stu-id="ffad3-185">**Group Name**: Theater and Movies</span></span>
    
 
4. <span data-ttu-id="ffad3-p117">Stellen Sie sicher, dass  *keines*  der Kontrollkästchen auf der Registerkarte aktiviert ist. Das Kontrollkästchen für **Erbt die Spalten vom übergeordneten Inhaltstyp** ist möglicherweise standardmäßig aktiviert. *Deaktivieren Sie es unbedingt.*</span><span class="sxs-lookup"><span data-stu-id="ffad3-p117">Verify that  *none*  of the check boxes on the tab are selected. The check box for **Inherits the columns from the parent Content Type** may be selected by default. *Be sure to clear it.*</span></span> 
    
 
5. <span data-ttu-id="ffad3-189">Öffnen Sie die Registerkarte **Spalten** im Designer.</span><span class="sxs-lookup"><span data-stu-id="ffad3-189">Open the  **Columns** tab in the designer.</span></span>
    
 
6. <span data-ttu-id="ffad3-p118">Verwenden Sie das Raster, um dem Inhaltstyp die zwei Websitespalten hinzuzufügen. Sie sind in der Dropdownliste nach ihren Anzeigenamen aufgeführt: **Actor/Actress** und **CastingStatus**. (Wenn sie nicht aufgeführt sind, haben Sie möglicherweise das Projekt nicht mehr gespeichert, nachdem Sie die benutzerdefinierten Websitespalten hinzufügt haben. Wählen Sie **Speichern** aus.)</span><span class="sxs-lookup"><span data-stu-id="ffad3-p118">Use the grid to add the two site columns to the content type. They are listed in the drop-down list by their display names:  **Actor/Actress** and **CastingStatus**. (If they are not listed, you may not have saved the project since adding the custom site columns. Choose  **Save all**.)</span></span>
    
 
7. <span data-ttu-id="ffad3-194">Speichern Sie die Datei, und schließen Sie den Designer.</span><span class="sxs-lookup"><span data-stu-id="ffad3-194">Save the file and close the designer.</span></span>
    
 
8. <span data-ttu-id="ffad3-195">Der nächste Schritt erfordert, dass Sie direkt im unformatierten XML des Inhaltstyps arbeiten. Wählen Sie daher im **Projektmappen-Explorer** die dem Inhaltstyp **ActingRole** untergeordnete Datei „elements.xml“ aus.</span><span class="sxs-lookup"><span data-stu-id="ffad3-195">The next step requires that you work directly in the raw XML for the content type, so in  **Solution Explorer**, choose the elements.xml file child of the  **ActingRole** content type.</span></span>
    
 
9. <span data-ttu-id="ffad3-p119">Die Datei enthält bereits **FieldRef**-Elemente für die beiden Spalten, die Sie hinzugefügt haben. Fügen Sie **FieldRef**-Elemente für zwei integrierte SharePoint-Spalten als übergeordnete Elemente der beiden bereits vorhandenen hinzu. Nachfolgend dargestellt ist das Markup für die Elemente. *Sie müssen diese GUIDs für die ID-Attribute verwenden, da diese integrierte Feldtypen mit festen IDs sind.* Fügen Sie sie *über* den beiden **FieldRef**-Elementen für die benutzerdefinierten Websitespalten hinzu.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p119">There are already  **FieldRef** elements in the file for the two columns that you added. Add **FieldRef** elements for two built-in SharePoint columns as peers of the two that are already there. The following is the markup for the elements. *You must use these same GUIDs for the ID attribute because these are built-in field types with fixed IDs.*  Add these *above*  the two **FieldRef** elements for the custom site columns.</span></span>
    
```
  <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Character" />
<FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Character" />
```


    Note that we have given these fields a custom display name:  **Character**, in the sense of a character in a play or movie.
    
 

### <a name="to-create-the-custom-list-template-and-a-list-instance"></a><span data-ttu-id="ffad3-201">So erstellen Sie die benutzerdefinierte Listenvorlage und eine Listeninstanz</span><span class="sxs-lookup"><span data-stu-id="ffad3-201">To create the custom list template and a list instance</span></span>


1. <span data-ttu-id="ffad3-p120">Fügen Sie ein SharePoint-Element **Liste** zum SharePoint-Add-In-Projekt mit dem Namen „CharactersInShow“ hinzu. Lassen Sie auf der Seite **Listeneinstellungen auswählen** im **Assistenten zum Anpassen von SharePoint** den Listenanzeigenamen auf dem Standardwert **CharactersInShow**, aktivieren Sie das Optionsfeld **Anpassbare Liste erstellen basierend auf**, und wählen Sie in der Dropdownliste **Standard (leer)** aus. Klicken Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p120">Add a SharePoint  **List** item to the SharePoint Add-in project with the nameCharactersInShow. On the  **Choose List Settings** page of the **SharePoint Customization Wizard**, leave the list display name at the default  **CharactersInShow**, choose the  **Create a customizable list based on** option button, and choose **Default (Blank)** on the drop-down list. Then choose **Finish**.</span></span>
    
 
2. <span data-ttu-id="ffad3-p121">Wenn Sie den Assistenten abschließen, wird eine Listenvorlage **CharactersInShow** mit einer untergeordneten Listeninstanz namens **CharactersInShowInstance** erstellt. Möglicherweise wurde standardmäßig ein Listen-Designer geöffnet. Er wird in einem späteren Schritt verwendet.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p121">When you complete the wizard, a  **CharactersInShow** list template is created with a child list instance named **CharactersInShowInstance**. A list designer may have opened by default. It is used in a later step.</span></span>
    
 
3. <span data-ttu-id="ffad3-208">Öffnen Sie die untergeordnete Datei „elements.xml“ der Listenvorlage **CharactersInShow** ( *nicht* die untergeordnete Datei „elements.xml“ von **CharactersInShowInstance**).</span><span class="sxs-lookup"><span data-stu-id="ffad3-208">Open the elements.xml child of the  **CharactersInShow** list template ( *not*  the elements.xml child of the **CharactersInShowInstance**).</span></span>
    
 
4. <span data-ttu-id="ffad3-209">Fügen Sie dem Attribut **DisplayName** Leerzeichen hinzu, damit es besser aussieht: „Characters In Show“.</span><span class="sxs-lookup"><span data-stu-id="ffad3-209">Add spaces to the  **DisplayName** attribute to make it friendlier:"Characters In Show".</span></span>
    
 
5. <span data-ttu-id="ffad3-210">Legen Sie das Attribut **Description** auf „Characters in a play or movie“ fest.</span><span class="sxs-lookup"><span data-stu-id="ffad3-210">Set the  **Description** attribute to"The characters in a play or movie."</span></span>
    
 
6. <span data-ttu-id="ffad3-211">Lassen Sie alle anderen Attribute auf dem Standardwert, speichern Sie die Datei, und schließen Sie sie.</span><span class="sxs-lookup"><span data-stu-id="ffad3-211">Leave all other attributes at their default, save the file and close it.</span></span>
    
 
7. <span data-ttu-id="ffad3-212">Wenn der Listen-Designer nicht geöffnet wurde, wählen Sie den Knoten **CharactersInShow** im **Projektmappen-Explorer** aus.</span><span class="sxs-lookup"><span data-stu-id="ffad3-212">If the list designer is not open, choose the  **CharactersInShow** node in **Solution Explorer**.</span></span>
    
 
8. <span data-ttu-id="ffad3-213">Öffnen Sie die Registerkarte **Spalten** im Designer, und klicken Sie dann auf die Schaltfläche **Inhaltstypen**.</span><span class="sxs-lookup"><span data-stu-id="ffad3-213">Open the  **Columns** tab in the designer, and then choose the **Content Types** button.</span></span>
    
 
9. <span data-ttu-id="ffad3-214">Fügen Sie im Dialogfeld **Einstellungen für Inhaltstypen** den Inhaltstyp **ActingRole** hinzu.</span><span class="sxs-lookup"><span data-stu-id="ffad3-214">In the  **Content Type Settings** dialog, add the **ActingRole** content type.</span></span>
    
 
10. <span data-ttu-id="ffad3-215">Wählen Sie in der Liste der Typen den Inhaltstyp **ActingRole** aus, und klicken Sie auf die Schaltfläche **Als Standard festlegen**.</span><span class="sxs-lookup"><span data-stu-id="ffad3-215">Choose the  **ActingRole** content type in the list of types, and choose the **Set as Default** button.</span></span>
    
    <span data-ttu-id="ffad3-216">Wählen Sie den Inhaltstyp **Element** aus, klicken Sie mit der rechten Maustaste auf die kleine Pfeilspitze, die links vom Inhaltstypnamen angezeigt wird, und klicken Sie dann auf **Löschen**.</span><span class="sxs-lookup"><span data-stu-id="ffad3-216">Choose the  **Item** content type, right-click the small arrowhead that appears to the left of the content type name, and then choose **Delete**.</span></span>
    
 
11. <span data-ttu-id="ffad3-p122">Wiederholen Sie den vorherigen Schritt für den Inhaltstyp **Ordner**, sodass **ActingRole** als einziger Inhaltstyp angezeigt wird. Klicken Sie auf **OK**, um das Dialogfeld zu schließen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p122">Repeat the preceding step for the  **Folder** content type, so **ActingRole** is the only content type listed. Choose **OK** to close the dialog.</span></span>
    
 
12. <span data-ttu-id="ffad3-p123">In der Liste der Spalten sind jetzt drei Spalten vorhanden. Wählen Sie **Titel** aus, klicken Sie mit der rechten Maustaste auf die kleine Pfeilspitze, die links vom Inhaltstypnamen angezeigt wird, und klicken Sie dann auf **Löschen**. Jetzt sollten nur zwei Spalten angezeigt werden, **Actor/Actress** und **Casting Status**.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p123">Three columns are now on the list of columns. Choose  **Title**, right-click the small arrowhead that appears to the left of the content type name, and then choose  **Delete**. Only two columns should now be listed,  **Actor/Actress** and **Casting Status**.</span></span>
    
 
13. <span data-ttu-id="ffad3-p124">Öffnen Sie die Registerkarte **Liste** des Designers. Diese Registerkarte wird verwendet, um bestimmte Werte für die Liste *Instanz*, nicht für die Liste *Vorlage* festzulegen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p124">Open the  **List** tab of the designer. This tab is used to set certain values for the list *instance*  , not the list *template*  .</span></span>
    
 
14. <span data-ttu-id="ffad3-224">Ändern Sie die Werte auf dieser Registerkarte wie folgt:</span><span class="sxs-lookup"><span data-stu-id="ffad3-224">Change the values on this tab to the following:</span></span>
    
      -  <span data-ttu-id="ffad3-225">**Titel**: Characters in Hamlet</span><span class="sxs-lookup"><span data-stu-id="ffad3-225">**Title**: Characters in Hamlet</span></span>
    
 
  -  <span data-ttu-id="ffad3-226">**Listen-URL**: Lists/CharactersInHamlet</span><span class="sxs-lookup"><span data-stu-id="ffad3-226">**List URL**: Lists/CharactersInHamlet</span></span>
    
 
  -  <span data-ttu-id="ffad3-227">**Beschreibung**: Die Charaktere in Hamlet und Casting-Informationen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-227">**Description**: The characters in Hamlet and casting information.</span></span>
    
 

     <span data-ttu-id="ffad3-228">Lassen Sie die Kontrollkästchen auf ihrer Standardeinstellung, speichern Sie die Datei, und schließen Sie den Designer.</span><span class="sxs-lookup"><span data-stu-id="ffad3-228">Leave the check boxes at their default status, save the file, and close the designer.</span></span>
    
 
15. <span data-ttu-id="ffad3-p125">Die Listeninstanz hat möglicherweise ihren alten Namen im **Projektmappen-Explorer** beibehalten. Wenn dies der Fall ist, öffnen Sie das Kontextmenü für **CharactersInShowInstance**, wählen **Umbenennen** aus, und ändern den Namen in „CharactersInHamlet“.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p125">The list instance may have its old name in  **Solution Explorer**. If so, open the shortcut menu for  **CharactersInShowInstance**, choose  **Rename**, and change the name to CharactersInHamlet.</span></span>
    
 
16. <span data-ttu-id="ffad3-231">Öffnen Sie die Datei „schema.xml“.</span><span class="sxs-lookup"><span data-stu-id="ffad3-231">Open the schema.xml file.</span></span>
    
 
17. <span data-ttu-id="ffad3-p126">In der Datei können zwei **ContentType**-Elemente vorhanden sein, eines mit dem **Name**-Attributwert „ActingRole“ und eines mit dem Namen **ListFieldsContentType**. Nur das mit dem Namen „ActingRole“ ist relevant, löschen Sie daher alle anderen **ContentType**-Elemente.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p126">There may be two  **ContentType** elements in the file, one with the **Name** attribute value ofActingRole and another called **ListFieldsContentType**. Only the one called ActingRole belongs, so delete any other **ContentType** elements.</span></span>
    
     <span data-ttu-id="ffad3-p127">**Hinweis** Möglicherweise befindet sich kein Zeilenumbruch zwischen den **ContentType**-Elementen, sodass es zunächst aussieht, als sei nur ein Element vorhanden. Scrollen Sie nach rechts, und suchen Sie sorgfältig nach weiteren Elementen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p127">**Note**  There may not be line breaks between the  **ContentType** elements, in which case it may appear at first that there is only one. Scroll to the right and check carefully for others.</span></span>
18. <span data-ttu-id="ffad3-p128">Für das Element **Fields** müssten zwei **Field**-Elemente vorhanden sein (die in einer Zeile stehen, wenn sich zwischen ihnen kein Zeilenumbruch befindet). Eines sollte das Element **Field** in der Datei elements.xml der Websitespalte **Actor** genau duplizieren, das andere sollte das Element **Field** in der Datei elements.xml der Websitespalte **CastingStatus** genau duplizieren. Wenn einschließlich aller untergeordneten Elemente (wie z. B. die Elemente **CHOICES** und **MAPPINGS**) keine genaue Übereinstimmung vorhanden ist, kopieren Sie das Element **Field** in der Datei elements.xml der Websitespalte und fügen es anstelle des nicht übereinstimmenden Elements **Field** in die Datei „schema.xml“ ein.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p128">The  **Fields** element should have two **Field** elements (which are on a single line if there is no line break between them). One should exactly duplicate the **Field** element in the **Actor** site column elements.xml and the other should exactly duplicate the **Field** element from the **CastingStatus** site column elements.xml. If there is not an exact match, including all child elements (such as the **CHOICES** and **MAPPINGS** elements), copy the **Field** element from the site column elements.xml file and paste it in place of the mismatched **Field** element in the schema.xml file.</span></span>
    
 
19. <span data-ttu-id="ffad3-p129">Ersetzen Sie dann in der Datei „schema.xml“ im Element **View**, dessen BaseViewID-Wert „0“ ist, das vorhandene **ViewFields**-Element durch das folgende Markup. (Verwenden Sie genau diese GUID für das **FieldRef**-Element mit dem Namen `LinkTitle`.)</span><span class="sxs-lookup"><span data-stu-id="ffad3-p129">Still in the schema.xml file, in the  **View** element whose BaseViewID value is "0", replace the existing **ViewFields** element with the following markup. (Use exactly this GUID for the **FieldRef** named `LinkTitle`.)</span></span>
    
```
  <ViewFields>
  <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Character" />
  <FieldRef Name="Actor" ID="{GUID from the site column elements.xml}" />
  <FieldRef Name="CastingStatus" ID="{GUID from the site column elements.xml}" />
</ViewFields>
```

20. <span data-ttu-id="ffad3-p130">Ersetzen Sie die beiden fehlenden ID-Attributwerte durch die GUIDs in den „elements.xml“-Dateien der entsprechenden Websitespalten. Vergessen Sie nicht die umschließenden Klammern „{}“.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p130">Replace the two missing ID attribute values with the GUIDs in the respective site column elements.xml files. Don't forget the framing braces "{}".</span></span> 
    
 
21. <span data-ttu-id="ffad3-p131">Ersetzen Sie dann in der Datei „schema.xml“ im Element **View**, dessen BaseViewID-Wert „1“ ist, das vorhandene **ViewFields**-Element durch das folgende Markup. (Verwenden Sie genau diese GUID für das **FieldRef**-Element mit dem Namen `LinkTitle`.)</span><span class="sxs-lookup"><span data-stu-id="ffad3-p131">Still in the schema.xml file, in the  **View** element whose BaseViewID value is "1", replace the existing **ViewFields** element with the following markup. (Use exactly this GUID for the **FieldRef** named `LinkTitle`.)</span></span>
    
```
  <ViewFields>
  <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Character" />
</ViewFields>
```

22. <span data-ttu-id="ffad3-245">Kopieren Sie die beiden **FieldRef**-Elemente für `Actor` und `CastingStatus`, die Sie in der vorherigen Ansicht diesem **ViewFields**-Element als gleichgeordnete Elemente von `LinkTitle`**FieldRef** hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="ffad3-245">Copy the two  **FieldRef** elements for `Actor` and `CastingStatus` that you added to the previous view to this **ViewFields** element as siblings of the `LinkTitle` **FieldRef**.</span></span>
    
 
23. <span data-ttu-id="ffad3-246">Speichern und schließen Sie die Datei „schema.xml“.</span><span class="sxs-lookup"><span data-stu-id="ffad3-246">Save and close the schema.xml file.</span></span>
    
 
24. <span data-ttu-id="ffad3-247">Öffnen Sie die Datei „elements.xml“, die ein untergeordnetes Element der Listeninstanz **CharactersInHamlet** ist.</span><span class="sxs-lookup"><span data-stu-id="ffad3-247">Open the elements.xml file that is a child of the list instance  **CharactersInHamlet**.</span></span>
    
 
25. <span data-ttu-id="ffad3-248">Geben Sie in die Liste einige Anfangsdaten ein, indem Sie das folgende Markup als untergeordnetes Element des **ListInstance**-Elements hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-248">Populate the list with some initial data by adding the following markup as a child of the  **ListInstance** element.</span></span>
    
```
  <Data>
  <Rows>
    <Row>
      <Field Name="Title">Hamlet</Field>
      <Field Name="Actor">Tom Higginbotham</Field>
      <Field Name="CastingStatus">Committed to Role</Field>
    </Row>
    <Row>
      <Field Name="Title">Claudius</Field>
      <Field Name="Actor"></Field>
      <Field Name="CastingStatus">Not Started</Field>
    </Row>
    <Row>
      <Field Name="Title">Gertrude</Field>
      <Field Name="Actor">Satomi Hayakawa</Field>
      <Field Name="CastingStatus">Auditioned</Field>
    </Row>
    <Row>
      <Field Name="Title">Ophelia</Field>
      <Field Name="Actor">Cassi Hicks</Field>
      <Field Name="CastingStatus">Committed to Role</Field>
    </Row>
    <Row>
      <Field Name="Title">The ghost</Field>
      <Field Name="Actor">Lertchai Treetawatchaiwong</Field>
      <Field Name="CastingStatus">Role Offered</Field>
    </Row>
  </Rows>
</Data>
```

2. <span data-ttu-id="ffad3-p132">Wählen Sie im **Projektmappen-Explorer** die Option **Feature1** aus, um den Feature-Designer zu öffnen. Im Designer legen Sie für den **Titel** „Theater and Movie Data Components“ und für die **Beschreibung** Websitespalten, Inhaltstypen und Listeninstanzen für Daten zu Theater und Film fest. Speichern Sie die Datei, und schließen Sie den Designer.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p132">In  **Solution Explorer**, choose  **Feature1** to open the Feature designer. In the designer, set the **Title** toTheater and Movie Data Components and set the **Description** toSite columns, content types, and list instances for data about theater and movies.. Save the file, and close the designer.</span></span>
    
 
3. <span data-ttu-id="ffad3-252">Wenn **Feature1** im **Projektmappen-Explorer** nicht umbenannt wurde, öffnen Sie das zugehörige Kontextmenü, wählen **Umbenennen** aus, und benennen die Option in „TheaterAndMovieDataComponents“ um.</span><span class="sxs-lookup"><span data-stu-id="ffad3-252">If the  **Feature1** in **Solution Explorer** has not been renamed, open its shortcut menu, choose **Rename**, and rename it TheaterAndMovieDataComponents.</span></span>
    
 

### <a name="to-code-the-remote-web-application-project"></a><span data-ttu-id="ffad3-253">So codieren Sie das Remotewebanwendungs-Projekt</span><span class="sxs-lookup"><span data-stu-id="ffad3-253">To code the remote web application project</span></span>


- <span data-ttu-id="ffad3-p133">Entwickeln Sie die Webanwendung wie jede andere Webanwendung für Ihren bevorzugten Plattformstapel. Bei einem Microsoft-Stapel können Sie entweder den REST/OData-Webdienst oder eines der Clientobjektmodelle in SharePoint verwenden. Bei einem Nicht-Microsoft-Stapel können Sie die REST/OData-Endpunkte in SharePoint verwenden, um Erstellungs-, Lese-, Aktualisierungs- und Löschoperationen (CRUD: Create, Read, Update and Delete) in der Add-In-Website durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p133">Develop the web application as you would any other web application for your preferred platform stack. For a Microsoft stack, you can use either the REST/OData web service or one of the client object models in SharePoint. For a non-Microsoft stack, you can use the REST/OData endpoints in SharePoint to perform create/read/update/delete (CRUD) operations on data in the add-in web.</span></span>
    
     <span data-ttu-id="ffad3-p134">**Hinweis** Wenn Sie dem Webanwendungsprojekt in Visual Studio einen Verweis auf eine Assembly hinzufügen, legen Sie die Eigenschaft **Lokale Kopie** der Assembly auf **True** fest, es sei denn, Sie wissen, dass die Assembly bereits auf dem Webserver installiert ist, oder Sie können sicherstellen, dass sie installiert wird, bevor Sie Ihr Add-In bereitstellen. .NET Framework wird auf Microsoft Azure-Webrollen und Azure-Websites installiert. Die SharePoint-Clientassemblys und die verschiedenen verwalteten Codeerweiterungen und Foundations von Microsoft werden jedoch nicht installiert. Office Developer Tools für Visual Studio 2012 fügt automatisch Verweise auf einige häufig in SharePoint-Add-Ins verwendete Assemblys hinzu und legt die Eigenschaft **Lokale Kopie** fest.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p134">**Note**  When you add a reference to an assembly to your web application project in Visual Studio, set the  **Copy Local** property of the assembly to **True**, unless you know that the assembly is already installed on the web server, or you can ensure that it is installed before you deploy your add-in. The .NET Framework is installed on Microsoft Azure Web Roles and Azure Web Sites. But the SharePoint client assemblies and the various Microsoft managed code extensions and foundations are not installed. Office Developer Tools for Visual Studio 2012 automatically adds references to some assemblies commonly used in SharePoint Add-ins and sets the  **Copy Local** property.</span></span>

    <span data-ttu-id="ffad3-p135">In dem fortlaufenden Beispiel entwickeln Sie eine ASP.NET-Webanwendung. Führen Sie die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p135">For the continuing example, you develop an ASP.NET web application. Take the following steps.</span></span>
    
      1. <span data-ttu-id="ffad3-p136">Öffnen Sie die Datei „Default.aspx“, und ersetzen Sie das Textelement der Datei durch das folgende Markup. Das Markup fügt eine Schaltfläche **Get the Cast** hinzu, welche, wenn sie ausgewählt wird, die Liste **Characters in Hamlet** im Add-In-Web liest und deren Daten in einem [GridView](http://msdn2.microsoft.com/de-DE/library/4w7ya1ts)-Steuerelement darstellt, das erst nach dem Klicken auf die Schaltfläche angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p136">Open the Default.aspx file and replace the body element of the file with the following markup. The markup adds a  **Get the Cast** button that, when chosen, reads the **Characters in Hamlet** list that is in the add-in web and presents its data in a [GridView](http://msdn2.microsoft.com/de-DE/library/4w7ya1ts) control that appears only after the button is pressed.</span></span>
    
```HTML
  <body >
    <form id="form1" runat="server">
    <div>
    <h2>Local Theater</h2>
    </div>
    <asp:Literal ID="Literal1" runat="server"><br /><br /></asp:Literal>

    <asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="Get the Cast"/>

    <asp:Literal ID="Literal2" runat="server"><br /><br /></asp:Literal>

    <asp:GridView ID="GridView1" runat="server" Caption="The Cast" ></asp:GridView>
    </form>
</body>
```

  2. <span data-ttu-id="ffad3-265">Öffnen Sie die Datei „Default.aspx.cs“, und fügen Sie die folgenden **using**-Anweisungen hinzu.</span><span class="sxs-lookup"><span data-stu-id="ffad3-265">Open the Default.aspx.cs file and add the following  **using** statements to it.</span></span>
    
```C#
  using Microsoft.SharePoint.Client;
using Microsoft.IdentityModel.S2S.Tokens;
using System.Net;
using System.IO;
using System.Xml;
using System.Data;
using System.Xml.Linq;
using System.Xml.XPath;
using Microsoft.SharePoint.Samples;
```


    The last of these statements refers to the namespace that is declared in the TokenHelper.cs file.
    
 
  3. <span data-ttu-id="ffad3-266">Fügen Sie der **Default**-Klasse die folgenden Felder hinzu.</span><span class="sxs-lookup"><span data-stu-id="ffad3-266">Add the following fields to the  **Default** class.</span></span>
    
```C#
  SharePointContextToken contextToken;
string accessToken;
Uri sharepointUrl;
```

  4. <span data-ttu-id="ffad3-p137">Ersetzen Sie die **Page_Load**-Methode durch den folgenden Code, der die **TokenHelper**-Klasse verwendet, um Token von dem OAuth-kompatiblen sicheren Token-Server abzurufen. Der Zugriffstoken wird dann in der Eigenschaft [CommandArgument](http://msdn2.microsoft.com/de-DE/library/hykdabtx) der Schaltfläche zum späteren Abrufen durch den Click-Ereignishandler der Schaltfläche gespeichert.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p137">Replace the  **Page_Load** method with the following code that uses the **TokenHelper** class to obtain tokens from the OAuth-compliant secure token server. The access token is then stored in the [CommandArgument](http://msdn2.microsoft.com/de-DE/library/hykdabtx) property of the button for later retrieval by the button's click event handler.</span></span>
    
```C#
  protected void Page_Load(object sender, EventArgs e)
{
    TokenHelper.TrustAllCertificates();
    string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);

    if (contextTokenString != null)
    {
        // Get context token
        contextToken = TokenHelper.ReadAndValidateContextToken(contextTokenString, Request.Url.Authority);

        // Get access token
        sharepointUrl = new Uri(Request.QueryString["SPAppWebUrl"]);
        accessToken = TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority).AccessToken;
        
        // Pass the access token to the button event handler.
        Button1.CommandArgument = accessToken;
    }
}
```

  5. <span data-ttu-id="ffad3-p138">Fügen Sie der **Default**-Klasse den folgenden Ereignishandler hinzu. Der Handler beginnt, den in der Eigenschaft [CommandArgument](http://msdn2.microsoft.com/de-DE/library/hykdabtx) der Schaltfläche gespeicherten Zugriffstoken abzurufen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p138">Add the following event handler to the  **Default** class. The handler begins by retrieving the access token that was stored in the button's [CommandArgument](http://msdn2.microsoft.com/de-DE/library/hykdabtx) property.</span></span>
    
```C#
  protected void Button1_Click(object sender, EventArgs e)
{
    // Retrieve the access token that the Page_Load method stored
    // in the button's command argument.
    string accessToken = ((Button)sender).CommandArgument;
}
```

  6. <span data-ttu-id="ffad3-271">Der Handler muss die geänderte Add-In-Web-URL auf Postbacks neu beziehen. Fügen Sie daher den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="ffad3-271">The handler needs to reacquire the modified add-in web URL on postbacks, so add the following code.</span></span>
    
```C#
  if (IsPostBack)
{
    sharepointUrl = new Uri(Request.QueryString["SPAppWebUrl"]);
}
```

  7. <span data-ttu-id="ffad3-p139">Fügen Sie die folgende Zeile hinzu, die einen der SharePoint-REST/OData-Endpunkte verwendet, um Listendaten abzurufen. In diesem Beispiel liest der Code die Liste **Characters in Hamlet**, die für das Add-In-Web bereitgestellt wird. Die APIs für diesen Dienst machen es einfach, in einer einzelnen Codezeile eine Liste auszuwählen und drei Felder in der Liste zum Zurückgeben festzulegen. Beachten Sie, dass Sie in der OData-URL den internen Namen der Felder (Spalten) und nicht den Anzeigenamen angeben müssen, damit der Code `Title`, `Actor` sowie `CastingStatus` verwendet und nicht `Character`, `Actor/Actress` und `Casting Status.` Weitere Informationen über den REST/OData-Webdienst finden Sie unter [Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen](use-odata-query-operations-in-sharepoint-rest-requests.md).</span><span class="sxs-lookup"><span data-stu-id="ffad3-p139">Add the following line that uses one of the SharePoint REST/OData endpoints to obtain list data. In this example, the code reads the  **Characters in Hamlet** list that is deployed to the add-in web. The APIs for this service make it easy, in a single line of code, to select a list and specify three fields from the list to return. Note that in the OData URL you must use the internal names of the fields (columns) rather than the display names, so the code uses `Title`,  `Actor`, and  `CastingStatus` rather than `Character`,  `Actor/Actress`, and  `Casting Status.` For more information about the REST/OData web service, see [Use OData query operations in SharePoint REST requests](use-odata-query-operations-in-sharepoint-rest-requests.md).</span></span>
    
```C#
  // REST/OData URL section
 string oDataUrl = "/_api/Web/lists/getbytitle('Characters In Hamlet')/items?$select=Title,Actor,CastingStatus";
```

  8. <span data-ttu-id="ffad3-276">Fügen Sie den folgenden Code hinzu, der die Klassen[HttpWebRequest](http://msdn2.microsoft.com/de-DE/library/8y7x3zz2) und [HttpWebResponse](http://msdn2.microsoft.com/de-DE/library/ww5755y6) des [System.Net](http://msdn2.microsoft.com/de-DE/library/btdf6a7e)-Namespace verwendet, um die HTTP-Anforderungs- und -Antwortobjekte zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="ffad3-276">Add the following code that uses the  [HttpWebRequest](http://msdn2.microsoft.com/de-DE/library/8y7x3zz2) and [HttpWebResponse](http://msdn2.microsoft.com/de-DE/library/ww5755y6) classes of the [System.Net](http://msdn2.microsoft.com/de-DE/library/btdf6a7e) namespace to construct the HTTP request and response objects.</span></span>
    
```C#
  // HTTP Request and Response construction section
HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(sharepointUrl.ToString() + oDataUrl);
request.Method = "GET";
request.Accept = "application/atom+xml";
request.ContentType = "application/atom+xml;type=entry";
request.Headers.Add("Authorization", "Bearer " + accessToken);
HttpWebResponse response = (HttpWebResponse)request.GetResponse();
```

  9. <span data-ttu-id="ffad3-p140">Fügen Sie den folgenden Code hinzu, um das ATOM-formatierte Antwort-XML zu analysieren. Er verwendet die Klassen des Namespace  [System.Xml.Linq](http://msdn2.microsoft.com/de-DE/library/bb299195) , um die zurückgegebenen Daten zu analysieren und eine [List<T>](http://msdn2.microsoft.com/de-DE/library/6sh2ey19) der Elemente aus der SharePoint-Liste zu erstellen. (Sie könnten auch die Klassen des Namespace [System.Xml](http://msdn2.microsoft.com/de-DE/library/y3y47afh) verwenden.) Beachten Sie, dass in dem von SharePoint zurückgegebenen XML die untergeordneten Elemente des **entry**-Elements die Metadaten zu dem Listenelement enthalten. Die tatsächlichen Zeilendaten eines SharePoint-Listenelements sind zwei Schichten weiter unten im **properties**-Element geschachtelt. Aus diesem Grund wird die Erweiterungsmethode  [Elements<T>](http://msdn2.microsoft.com/de-DE/library/bb348465) zweimal verwendet, um die höheren Ebenen herauszufiltern.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p140">Add the following code to parse the ATOM-formatted response XML. It uses the classes of the  [System.Xml.Linq](http://msdn2.microsoft.com/de-DE/library/bb299195) namespace to parse the data that is returned and construct a [List<T>](http://msdn2.microsoft.com/de-DE/library/6sh2ey19) of the items from the SharePoint list. (You could also use the classes of the [System.Xml](http://msdn2.microsoft.com/de-DE/library/y3y47afh) namespace.) Note that, in the XML that SharePoint returns, the child elements of the **entry** element hold metadata about the list item. The actual row data of a SharePoint list item is nested two layers down in the **properties** element. For that reason the [Elements<T>](http://msdn2.microsoft.com/de-DE/library/bb348465) extension method is used twice to filter out the higher levels.</span></span>
    
```C#
  // Response markup parsing section
XDocument oDataXML = XDocument.Load(response.GetResponseStream(), LoadOptions.None);
XNamespace atom = "http://www.w3.org/2005/Atom";
XNamespace d = "http://schemas.microsoft.com/ado/2007/08/dataservices";
XNamespace m = "http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"; 

List<XElement> entries = oDataXML.Descendants(atom + "entry")
                         .Elements(atom + "content")
                         .Elements(m + "properties")
                         .ToList();
```

  10. <span data-ttu-id="ffad3-p141">Fügen Sie die folgende LINQ-Abfrage hinzu, um eine [IEnumerable<T>](http://msdn2.microsoft.com/de-DE/library/9eekhta0)-Sammlung eines anonymen Typs zu erstellen, die nur die Eigenschaften besitzt, die Sie benötigen. Beachten Sie, dass obwohl der Code durch seinen internen `Title`-Namen auf das Elementfeld Titel verweisen muss, der Eigenschaftenname in dem anonymen Typ, dem der Wert zugewiesen wird, als `Character` benannt werden kann. Ein Effekt davon ist, dass der besser geeignete Name **Character** auf der Seite angezeigt wird, wenn die Sammlung an ein Rastersteuerelement gebunden wird.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p141">Add the following LINQ query to construct an  [IEnumerable<T>](http://msdn2.microsoft.com/de-DE/library/9eekhta0) collection of an anonymous type that has just the properties you need and no others. Note that although the code must refer to the item title field by its internal name `Title`, the property name in the anonymous type, to which the value is assigned, can be named  `Character`. One effect of this is that when the collection is bound to a grid control, the more appropriate name  **Character** appears on the page.</span></span>
    
```C#
  var entryFieldValues = from entry in entries
                       select new { Character=entry.Element(d + "Title").Value, 
                                    Actor=entry.Element(d + "Actor").Value, 
                                    CastingStatus=entry.Element(d + "CastingStatus").Value };

```

  11. <span data-ttu-id="ffad3-p142">Schließen Sie den Handler mit dem folgenden Code ab, um die Daten an ein  [GridView](http://msdn2.microsoft.com/de-DE/library/4w7ya1ts) -Steuerelement auf der Seite zu binden. Die Spaltenüberschriften in dem Steuerelement werden standardmäßig als die Eigenschaftsnamen des anonymen Typs angezeigt: `Character`,  `Actor` und `CastingStatus`. Das  [GridView](http://msdn2.microsoft.com/de-DE/library/4w7ya1ts) -Steuerelement besitzt Eigenschaften, die es Ihnen ermöglichen, die Überschriften der Namens- und Formatierungsspalten zu steuern, sodass sie **Actor/Actress** und **Casting Status** lauten können, um mit den Spaltenüberschriften in SharePoint übereinzustimmen. Diese Methoden werden der Einfachheit halber hier nicht beschrieben. (Sie könnten auch ein [DataGrid](http://msdn2.microsoft.com/de-DE/library/e1zk1ey1) -Steuerelement verwenden.)</span><span class="sxs-lookup"><span data-stu-id="ffad3-p142">Finish the handler with the following code to bind the data to a  [GridView](http://msdn2.microsoft.com/de-DE/library/4w7ya1ts) control on the page. The column headers in the grid default to the property names of the anonymous type: `Character`,  `Actor`, and  `CastingStatus`. The  [GridView](http://msdn2.microsoft.com/de-DE/library/4w7ya1ts) control has properties that enable you to control the name and formatting column headers, so you could have **Actor/Actress** and **Casting Status** to match the column headers in SharePoint. For simplicity, these techniques are not described here. (You could also use a [DataGrid](http://msdn2.microsoft.com/de-DE/library/e1zk1ey1) control.)</span></span>
    
```C#
  GridView1.DataSource = entryFieldValues;
GridView1.DataBind();

```

  12. <span data-ttu-id="ffad3-290">Speichern Sie alle Dateien.</span><span class="sxs-lookup"><span data-stu-id="ffad3-290">Save all files.</span></span>
    
 

### <a name="to-test-and-debug-the-sharepoint-add-in"></a><span data-ttu-id="ffad3-291">So testen und debuggen Sie das SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="ffad3-291">To test and debug the SharePoint Add-in</span></span>


1. <span data-ttu-id="ffad3-p143">Um das SharePoint-Add-In und seine Remote-Webanwendung zu testen, drücken Sie in Visual Studio 2012 die Taste F5. Die Webanwendung wird für IIS Express unter localhost bereitgestellt. Das SharePoint-Add-In wird auf der SharePoint-Zielwebsite installiert. (Im fortlaufenden Beispiel versucht die Remote-Anwendung  *nicht*  , mit der *Host*  -Website zu interagieren, und der Add-In-Prinzipal verfügt automatisch über Berechtigungen für die *Add-In*  -Website, daher werden Sie *nicht*  zum Erteilen von Berechtigungen aufgefordert.) Die Seite **Websiteinhalt** Ihrer SharePoint-Zielwebsite wird geöffnet und das dort aufgeführte neue Add-In wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p143">To test the SharePoint Add-in and its remote web application, choose the F5 key in Visual Studio 2012. The web application is deployed to IIS Express at localhost. The SharePoint Add-in will is installed to the target SharePoint website. (In the continuing example, the remote add-in does  *not*  try to interact with the *host*  web and the add-in principal automatically has permissions to the *add-in*  web, so you are *not*  prompted to grant permissions.) The **Site Contents** page of your target SharePoint website opens, and you see the new add-in listed there.</span></span>
    
 
2. <span data-ttu-id="ffad3-p144">Wenn Sie das SharePoint-Add-In auswählen, wird die Remotewebanwendung auf der Seite geöffnet, die Sie im **StartPage**-Element in der Datei „AppManifest.xml“ festgelegt haben. Verwenden Sie die Webanwendung nach Bedarf, um zu überprüfen, ob sie funktioniert. Im fortlaufenden Beispiel in diesem Thema klicken Sie einfach auf die Schaltfläche. Dadurch wird eine Tabelle erstellt und mit der Liste **Characters in Hamlet** des Add-In-Webs ausgefüllt.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p144">Choose the SharePoint Add-in, and the remote web application opens to the page you specified in the  **StartPage** element in the AppManifest.xml file. Use the web application as needed to verify that it is working. In the continuing example of this topic, just choose the button. Doing so creates a grid and populates it with the **Characters in Hamlet** list of the add-in web.</span></span>
    
 

## <a name="publishing-the-sharepoint-add-in"></a><span data-ttu-id="ffad3-300">Veröffentlichen des SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="ffad3-300">Publishing the SharePoint Add-in</span></span>
<span data-ttu-id="ffad3-301"><a name="Publish"> </a></span><span class="sxs-lookup"><span data-stu-id="ffad3-301"></span></span>

<span data-ttu-id="ffad3-p145">Um Ihr SharePoint-Add-In zu veröffentlichen, laden Sie das Add-In-Paket in einen Unternehmens-Add-In-Katalog oder den Office Add-In-Store. Weitere Informationen finden Sie unter  [Veröffentlichen im Office Store oder im Add-In-Katalog eines Unternehmens](deploying-and-installing-sharepoint-add-ins-methods-and-options.md#MarketOrCatalog) und [Veröffentlichen von SharePoint-Add-Ins](publish-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="ffad3-p145">To publish your SharePoint Add-in, upload the add-in package to a corporate add-in catalog or to the Office add-in store. For more information, see  [Publishing to the Office Store or an organization's add-in catalog](deploying-and-installing-sharepoint-add-ins-methods-and-options.md#MarketOrCatalog) and [Publish SharePoint Add-ins](publish-sharepoint-add-ins.md).</span></span>
 

 

## <a name="troubleshooting"></a><span data-ttu-id="ffad3-304">Problembehandlung</span><span class="sxs-lookup"><span data-stu-id="ffad3-304">Troubleshooting</span></span>
<span data-ttu-id="ffad3-305"><a name="Troubleshooting"> </a></span><span class="sxs-lookup"><span data-stu-id="ffad3-305"></span></span>

<span data-ttu-id="ffad3-p146">Wenn das Add-In nicht funktioniert, sollten Sie überlegen, ob nicht ein Fehler im CAML-Markup die Bereitstellung der SharePoint-Komponenten blockiert. Verwenden Sie zum Überprüfen der Bereitstellung ein ähnliches Verfahren wie das folgende, das auf dem fortlaufenden Beispiel basiert.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p146">If the add-in is not working, you should consider whether a mistake in the CAML markup is blocking deployment of the SharePoint components. Use a procedure similar to the following, which is based on the continuing example, to verify the deployment.</span></span>
 

 

### <a name="to-test-the-provisioning-of-the-add-in-web"></a><span data-ttu-id="ffad3-308">So testen Sie die Bereitstellung des Add-In-Webs</span><span class="sxs-lookup"><span data-stu-id="ffad3-308">To test the provisioning of the add-in web</span></span>


1. <span data-ttu-id="ffad3-p147">Öffnen Sie die Seite **Websiteeinstellungen** des Hostwebs. Klicken Sie im Abschnitt **Websitesammlungsverwaltung** auf den Link **Websitehierarchie**.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p147">Open the  **Site Settings** page of the host web. In the **Site Collection Administration** section, choose the **Site hierarchy** link.</span></span>
    
 
2. <span data-ttu-id="ffad3-p148">Auf der Seite **Websitehierarchie** wird das Add-In nach seiner URL aufgeführt. Starten Sie es nicht. Kopieren Sie stattdessen die URL, und verwenden Sie die URL in den verbleibenden Schritten.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p148">On the  **Site Hierarchy** page, you see your add-in listed by its URL. Do not launch it. Instead, copy the URL and use the URL in the remaining steps.</span></span>
    
 
3. <span data-ttu-id="ffad3-314">Navigieren Sie zu „_URL_des_Add-In-Webs_/_layouts/15/ManageFeatures.aspx“ und überprüfen Sie auf der sich öffnenden Seite **Websitefeatures**, ob **Theater and Movie Data Components** in der alphabetischen Liste der Features in Ihrem SharePoint-Add-In aufgeführt wird und der Status **Aktiv** ist.</span><span class="sxs-lookup"><span data-stu-id="ffad3-314">Navigate to  _URL_of_app_web_/_layouts/15/ManageFeatures.aspx and, on the  **Site Features** page that opens, verify that **Theater and Movie Data Components** is on the alphabetical list of Features in your SharePoint Add-in and that its status is **Active**.</span></span>
    
 
4. <span data-ttu-id="ffad3-315">Navigieren Sie zu „_URL_des_Add-In-Webs_/_layouts/15/mngfield.aspx“, und überprüfen Sie auf der sich öffnenden Seite **Websitespalten**, ob eine Gruppe **Theater and Movies** in der Liste der Websitespalten vorhanden ist und ob sie Ihre neuen benutzerdefinierten Websitespalten, **Actor/Actress** und **Casting Status**, enthält.</span><span class="sxs-lookup"><span data-stu-id="ffad3-315">Navigate to  _URL_of_app_web_/_layouts/15/mngfield.aspx and, on the  **Site Columns** page that opens, verify that a **Theater and Movies** group is in the list of site columns and that it contains your new custom site columns, **Actor/Actress** and **Casting Status**.</span></span>
    
 
5. <span data-ttu-id="ffad3-316">Navigieren Sie zu „_URL_des_Add-In-Webs_/_layouts/15/mngctype.aspx“, und überprüfen Sie auf der sich öffnenden Seite **Websiteinhaltstypen**, ob eine Gruppe **Theater and Movies** in der Liste der Inhaltstypen vorhanden ist und ob sie Ihren neuen Inhaltstyp **ActingRole** enthält.</span><span class="sxs-lookup"><span data-stu-id="ffad3-316">Navigate to  _URL_of_app_web_/_layouts/15/mngctype.aspx and, on the  **Site Content Types** page that opens, verify that a **Theater and Movies** group is in the list of content types and that it contains your new **ActingRole** content type.</span></span>
    
 
6. <span data-ttu-id="ffad3-p149">Klicken Sie auf den Link zum Inhaltstyp **ActingRole**. Überprüfen Sie auf der sich öffnenden Seite **Websiteinhaltstyp**, ob der Inhaltstyp die zwei neuen Websitespaltentypen, **Actor/Actress** und **Casting Status** umfasst, und ob das Elementtitelfeld mit ihrem benutzerdefinierten Anzeigenamen benannt wurde: **Character**.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p149">Choose the link to the  **ActingRole** content type. On the **Site Content Type** page that opens, verify that the content type has the two new site column types, **Actor/Actress** and **Casting Status**, and that the item title field has been given your custom display name:  **Character**.</span></span>
    
 
7. <span data-ttu-id="ffad3-319">Navigieren Sie zu „ _URL_des_Add-In-Webs_/_layouts/15/mcontent.aspx“, und überprüfen Sie auf der sich öffnenden Seite **Websitebibliotheken und -listen**, ob ein Link **„Characters in Hamlet“ anpassen** vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="ffad3-319">Navigate to  _URL_of_app_web_/_layouts/15/mcontent.aspx and, on the  **Site Libraries and Lists** page that opens, verify that there is a **Customize "Characters in Hamlet"** link.</span></span>
    
 
8. <span data-ttu-id="ffad3-p150">Klicken Sie auf den Link **„Characters in Hamlet“ anpassen**, und überprüfen Sie auf der Seite der Listeneinstellungen, ob der einzige Inhaltstyp für diese Liste Ihr benutzerdefinierter Inhaltstyp **ActingRole** ist und ob Ihre zwei neuen Websitespalten, **Actor/Actress** und **Casting Status**, im Abschnitt **Spalten** aufgeführt werden. (Die Titelspalte wird möglicherweise mit ihrem internen Namen **Titel** anstatt mit dem von Ihnen angegebenen Anzeigenamen **Character** angezeigt.)</span><span class="sxs-lookup"><span data-stu-id="ffad3-p150">Choose the  **Customize "Characters in Hamlet"** link and verify on the list settings page that the only content type for the list is your custom **ActingRole** content type and that your two new site columns, **Actor/Actress** and **Casting Status** are listed in the **Columns** section. (The Title column may appear with its internal name **Title**, instead of the display name  **Character** that you gave it.)</span></span>
    
     <span data-ttu-id="ffad3-p151">**Hinweis** Falls auf der Seite kein Abschnitt **Inhaltstypen** dieser Art vorhanden ist, müssen Sie die Verwaltung der Inhaltstypen aktivieren. Klicken Sie auf den Link **Erweiterte Einstellungen**, und aktivieren Sie auf der Seite **Erweiterte Einstellungen** die Verwaltung der Inhaltstypen. Klicken Sie anschließend auf **OK**. Die vorherige Seite wird wieder angezeigt, und es ist ein Abschnitt **Inhaltstypen** vorhanden.</span><span class="sxs-lookup"><span data-stu-id="ffad3-p151">**Note**  If there is no  **Content Types** section on the page, you must enable management of content types. Click the **Advanced Settings** link and on the **Advanced Settings** page, enable management of content types and click **OK**. You are returned to the previous page and there is now a list of  **Content Types** section.</span></span>
9. <span data-ttu-id="ffad3-p152">Am oberen Seitenrand befindet sich die **Webadresse** der Liste. Kopieren Sie die Adresse, fügen Sie sie in die Adressleiste Ihres Browsers ein, und navigieren Sie dann zu der Liste. Überprüfen Sie, ob in der Liste die von Ihnen erstellten Beispielelemente vorhanden sind. (Die Titelspalte kann mit ihrem internen Namen **Title** anstatt mit dem von Ihnen angegebenen Anzeigenamen **Character** angezeigt werden.)</span><span class="sxs-lookup"><span data-stu-id="ffad3-p152">Near the top of the page is the  **Web Address** of the list. Copy this and paste it into the address bar of your browser, and then navigate to the list. Verify that the list has the sample items that you created. (The Title column may appear with its internal name **Title**, instead of the display name  **Character** that you gave it.)</span></span>
    
 

## <a name="next-steps"></a><span data-ttu-id="ffad3-329">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="ffad3-329">Next steps</span></span>
<span data-ttu-id="ffad3-330"><a name="NextSteps"> </a></span><span class="sxs-lookup"><span data-stu-id="ffad3-330"></span></span>

<span data-ttu-id="ffad3-p153">In diesem Artikel wurde beschrieben, wie ein einfaches hybrides SharePoint-Add-In mit einer Remotewebanwendung erstellt wird. Die nächsten Schritte könnten sein:</span><span class="sxs-lookup"><span data-stu-id="ffad3-p153">This article demonstrated how to create a simple hybrid SharePoint Add-in with a remote web application. As next steps, consider the following:</span></span>
 

 

- <span data-ttu-id="ffad3-p154">Hinzufügen von vollständiger CRUD-Funktionalität zum Add-In mit den REST/OData-Endpunkten oder einem der Clientobjektmodelle. Weitere Informationen finden Sie unter  [Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen](use-odata-query-operations-in-sharepoint-rest-requests.md) und [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode](complete-basic-operations-using-sharepoint-client-library-code.md).</span><span class="sxs-lookup"><span data-stu-id="ffad3-p154">Adding full CRUD functionality to the add-in with either the REST/OData endpoints or one of the client object models. For more information, see  [Use OData query operations in SharePoint REST requests](use-odata-query-operations-in-sharepoint-rest-requests.md) and [Complete basic operations using SharePoint client library code](complete-basic-operations-using-sharepoint-client-library-code.md).</span></span>
    
 
- <span data-ttu-id="ffad3-p155">Lokalisieren Ihres SharePoint-Add-Ins für andere Kulturen. Weitere Informationen finden Sie unter [Lokalisieren von SharePoint-Add-Ins](localize-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="ffad3-p155">Localizing your SharePoint Add-in for other cultures. For more information, see  [Localize SharePoint Add-ins](localize-sharepoint-add-ins.md).</span></span>
    
 
- <span data-ttu-id="ffad3-p156">Erstellen eines Windows Phone Companion-Add-Ins, das die Funktionalität der Remote-Webanwendung dupliziert. Weitere Informationen finden Sie unter  [Erstellen von mobilen Add-Ins für SharePoint](http://msdn.microsoft.com/de-DE/library/office/jj163228.aspx).</span><span class="sxs-lookup"><span data-stu-id="ffad3-p156">Creating a Windows Phone companion add-in that duplicates the functionality of the remote web application. For more information, see  [Build mobile SharePoint Add-ins 2013](http://msdn.microsoft.com/de-DE/library/office/jj163228.aspx).</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="ffad3-339">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ffad3-339">Additional resources</span></span>
<span data-ttu-id="ffad3-340"><a name="SP15createcloud_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ffad3-340"></span></span>


-  [<span data-ttu-id="ffad3-341">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="ffad3-341">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="ffad3-342">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="ffad3-342">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
    
 

