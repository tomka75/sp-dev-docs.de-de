---
title: Durchsuchen der App Manifestdatei-Struktur und des Pakets eines SharePoint-Add-Ins
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: d178c11ac3cfaa0d53f8517bfa3fa7da21a354c2
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in"></a><span data-ttu-id="51657-102">Durchsuchen der App Manifestdatei-Struktur und des Pakets eines SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="51657-102">Explore the app manifest structure and the package of a SharePoint Add-in</span></span>
<span data-ttu-id="51657-103">Erfahren Sie mehr über die Add-In-Paketstruktur und die Manifestdatei für ein SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="51657-103">Learn about the add-in package structure and the manifest file for a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="51657-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="51657-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="add-in-for-sharepoint-package-structure"></a><span data-ttu-id="51657-107">Paketstruktur von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="51657-107">Add-in for SharePoint package structure</span></span>
<span data-ttu-id="51657-108"><a name="Package"> </a></span><span class="sxs-lookup"><span data-stu-id="51657-108"></span></span>

<span data-ttu-id="51657-p102">Ein SharePoint-Add-In-Paket ist eine Datei mit der Erweiterung "APP", die dem Standard  [Open Packaging Conventions (OPC)](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx) entspricht. Das Paket enthält die folgenden Elemente:</span><span class="sxs-lookup"><span data-stu-id="51657-p102">A SharePoint Add-in package is a file that has an ".app" extension and that complies with the  [Open Packaging Conventions (OPC)](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx). The package contains the following items:</span></span>
 

 

-  <span data-ttu-id="51657-p103">**Add-In-Manifest:** Dies ist eine erforderliche Datei mit dem Namen "appmanifest.xml". SharePoint entnimmt daraus Informationen zu einigen wichtigen Eigenschaften des Add-Ins, z. B. den Titel und die zur Ausführung erforderlichen Berechtigungen. Weitere Informationen zum Inhalt dieser Datei finden Sie unter [Manifestdatei für Add-Ins für SharePoint](#AppManifest).</span><span class="sxs-lookup"><span data-stu-id="51657-p103">**Add-in manifest:** This is a required file that is named appmanifest.xml. It tells SharePoint about some important properties of the add-in, such as its title and the permissions it needs to run. For more information about the contents of this file, see [Add-in for SharePoint manifest file](#AppManifest).</span></span>
    
 
-  <span data-ttu-id="51657-p104">**SharePoint-Lösungspakete:** Optional kann das Add-In ein SharePoint-Lösungspaket (WSP-Datei) mit den Komponenten des Add-In-Webs enthalten. Diese Komponenten können Seiten, Listeninstanzen, Ansichten, Dokumente, Features mit **Web**-Bereich und andere SharePoint-Komponenten umfassen. (Weitere Informationen dazu, welche SharePoint-Komponenten in ein SharePoint-Add-In aufgenommen werden können, finden Sie unter  [Typen von SharePoint-Komponenten, die in einem SharePoint-Add-In enthalten sein können](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#TypesOfSPComponentsInApps).) Die WSP-Datei kann auch Office-Add-Ins enthalten. Die in der WSP-Datei enthaltenen Komponenten werden im Add-In-Web bereitgestellt. Ein Beispiel für ein Add-In-Paket, das ein SharePoint-Lösungspaket enthält, finden Sie unter  [Gewusst wie: Erstellen eines von einem Anbieter gehosteten Add-Ins, das eine benutzerdefinierte SharePoint-Liste und einen benutzerdefinierten Inhaltstyp enthält](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-conte.md).</span><span class="sxs-lookup"><span data-stu-id="51657-p104">**SharePoint Solution Packages:** Optionally, the add-in may include a SharePoint solution package (.wsp file) that contains the components of the add-in web. These components may include pages, list instances, views, documents, **Web**-scoped Features, and other SharePoint components. (For more information about what SharePoint components can be included in a SharePoint Add-in, see  [Types of SharePoint components that can be in a SharePoint Add-in](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#TypesOfSPComponentsInApps).) The .wsp file may also contain Office Add-ins. The components in the .wsp file are deployed to the add-in web. For an example of an add-in package that includes a SharePoint solution package, see  [Create a provider-hosted add-in that includes a custom SharePoint list and content type](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-conte.md).</span></span>
    
 
-  <span data-ttu-id="51657-p105">**Hostweb-Features mit benutzerdefinierten Aktionen oder Add-In-Parts:** Neben den SharePoint-Komponenten, die im Add-In-Web bereitgestellt werden, kann ein SharePoint-Add-In auch eine oder mehrere benutzerdefinierte Aktionen (Kontextmenübefehle oder Menübanderweiterungen) im Hostweb bereitstellen. Hierzu wird ein Feature in das Add-In-Paket eingefügt, das nicht in der .WSP-Datei des Pakets enthalten ist und das die Komponenten bereitstellt, die für das Hostweb vorgesehen sind. Dieses "freie" Feature wird als Hostweb-Feature bezeichnet. Add-In-Parts werden auf die gleiche Weise im Hostweb bereitgestellt. Das Hostweb-Feature besteht aus der SharePoint-Standarddatei "feature.xml" und mindestens einer zugehörigen "elements.xml"-Datei. Die "elements.xml"-Datei für eine benutzerdefinierte Aktion enthält beispielsweise das **CustomAction**-Markup für die benutzerdefinierte Aktion. Es kann auch Markup für Add-In-Parts enthalten. Nur diese beiden Komponenten können im Hostweb-Feature enthalten sein. Diese Hostweb-Features werden im Add-In-Manifest nicht einzeln aufgeführt. Es handelt sich jedoch im Sinn von OPC um "parts", und es besteht eine explizite OPC-Beziehung zwischen dem Add-In-Manifest und jeder dieser Dateien. Ein Beispiel für ein Add-In-Paket, das ein Hostweb-Feature enthält, finden Sie unter  [Gewusst wie: Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit Add-Ins für SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="51657-p105">**Host web Features with Custom Actions or add-in parts:** In addition to the SharePoint components that are deployed to the add-in web, a SharePoint Add-in can also deploy one or more custom actions (shortcut menu items or ribbon extensions) to the host web. This is accomplished by including in the add-in package a Feature that is not inside the package's .wsp file and that deploys the components that will go to the host web. This "loose" Feature is called a host web Feature. Add-in parts are deployed to the host web in the same way. The host web Feature consists of a standard SharePoint feature.xml file and one or more associated elements.xml files. An elements.xml file for a custom action, for example, contains the **CustomAction** markup for the custom action. It can also include markup for add-in parts. Only these two kinds of components can be in the host web Feature. These host web Features are not itemized in the add-in manifest. However, they are "parts" in the OPC sense, and there is an explicit OPC relationship between the add-in manifest and each of these files. For an example of an add-in package that includes a host web Feature, see [Create custom actions to deploy with SharePoint Add-ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span></span>
    
     <span data-ttu-id="51657-p106">**Hinweis** Mandantenadministratoren haben die Möglichkeit, ein SharePoint-Add-In per Batch auf mehreren Websites zu installieren. Ein Add-In, das auf diese Weise installiert worden ist, hat den Gültigkeitsbereich **Mandant**. Wenn das Add-In nicht per Batch, sondern stattdessen auf jeder Website getrennt installiert wurde, hat es den Gültigkeitsbereich **Web**Wenn das Hostweb-Feature Menübanderweiterungen oder Add-In-Webparts enthält, werden diese nicht für die Hostwebs bereitgestellt, wenn das Add-In per Batch installiert wird. Daher werden nur Kontextmenüelemente mit Add-Ins im Mandantenbereich bereitgestellt. Der Add-In-Bereich darf nicht mit dem Featurebereich verwechselt werden. Der Featurebereich bestimmt, wo die in einem Feature enthaltenen Elemente bereitgestellt werden. Mögliche Bereiche sind **Farm**, **WebApplication**, **Website** (d. h. die Websitesammlung) und **Web**. Nur die Option **Web** ist für Features in SharePoint-Add-Ins zulässig (sowohl Hostweb-Features als auch Features in einer WSP-Datei in einem Add-In-Paket). Der Add-In-Bereich bezeichnet den Bereich, in dem ein Add-In installiert wurde. Mögliche Bereiche sind **Web**, wenn das Add-In parallel auf einem oder mehreren Websites installiert wurde, und **Mandant**, wenn das Add-In auf allen oder einer Teilmenge der Websites der Mandantschaft eines Kunden installiert wurde. Weitere Informationen zu den Bereichen **Mandant** und **Web** finden Sie unter [Mandantschaften und Bereitstellungsbereiche von SharePoint-Add-Ins](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="51657-p106">**Note**  Tenant administrators have the option to batch-install a SharePoint Add-in to multiple websites. An add-in that has been installed in this way is said to have  **Tenant** scope. If the add-in has not been batch-installed, and is instead installed to each website separately, it has **Web** scope. If the host web Feature includes ribbon extensions or add-in parts, they are not deployed to the host webs if the add-in is batch-installed, so only shortcut menu items are deployed with Tenant-scoped add-ins. Add-in scope should not be confused with Feature scope. Feature scope determines where the elements in a Feature are deployed. The possibilities are **Farm**,  **WebApplication**,  **Site** (that is, site collection), and **Web**. Only the  **Web** option is permitted for Features in SharePoint Add-ins (both host web Features and Features inside a .wsp in an add-in package). Add-in scope refers to the scope at which an add-in is installed. The possibilities are **Web**, in which case the add-in has been installed to one or more websites site-by-site, and  **Tenant**, in which case the add-in has been batch installed to all or some subset of the websites in a customer's tenancy. For more information about  **Tenant** and **Web** scope, see [Tenancies and deployment scopes for SharePoint Add-ins](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md).</span></span>
-  <span data-ttu-id="51657-p107">**Lokalisierungsressourcendateien (.RESX):** Diese Dateien sind für die Lokalisierung verschiedener Aspekte des Add-In-Manifests vorgesehen, zu denen der Titel und Aspekte der Hostweb-Features im Add-In-Paket gehören. (Einzelne Teile des Add-In-Pakets, die sich in einem eigenen Paket befinden, wie WSP-Dateien, Azure-Websites-Pakete und Add-In-Manifeste, verfügen jeweils über eigene Lokalisierungsprozesse, die genauso ausgeführt werden wie bei Elementen, die nicht Teil eines SharePoint-Add-In sind.) Ein Beispiel zu einem Add-In-Paket, das die RESX-Dateien für ein Hostweb-Feature enthält, finden Sie unter [Lokalisieren von Add-Ins für SharePoint](localize-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="51657-p107">**Localization resource files (.resx):** These are for localizing aspects of the add-in manifest that include the add-in title and aspects of host web Features in the add-in package. (Individual parts of the add-in package that are inside their own package, such as .wsp files, Azure Web Sites packages, and add-in manifests, each have their own localization processes that are applied exactly as they would be if the items in question were not part of a SharePoint Add-in.) For an example of an add-in package that includes .resx files for a host web Feature, see [Localize SharePoint Add-ins](localize-sharepoint-add-ins.md).</span></span>
    
 
-  <span data-ttu-id="51657-p108">**Office-Add-Ins Manifeste:** Optional können ein oder mehrere Office-Add-Ins-Manifeste vorhanden sein, die jeweils eine Paketdefinition für ein Office-Add-In enthalten. Dieser Teil kann nur dann in das Add-In-Paket aufgenommen werden, wenn das Add-In in einen unternehmenseigenen Add-In-Katalog für SharePoint und nicht in einen öffentlichen Add-In-Store hochgeladen wird. Weitere Informationen finden Sie unter [Veröffentlichen von SharePoint-Add-Ins](publish-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="51657-p108">**Office Add-ins Manifests:** Optionally, there may be one or more Office Add-ins manifests that each package an Office Add-in. This part can be included in the add-in package only if the add-in is going to be uploaded to a SharePoint corporate add-in catalog, not the public marketplace. See [Publish SharePoint Add-ins](publish-sharepoint-add-ins.md) for more information.</span></span>
    
 

## <a name="add-in-for-sharepoint-manifest-file"></a><span data-ttu-id="51657-144">Manifestdatei von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="51657-144">Add-in for SharePoint manifest file</span></span>
<span data-ttu-id="51657-145"><a name="AppManifest"> </a></span><span class="sxs-lookup"><span data-stu-id="51657-145"></span></span>

<span data-ttu-id="51657-p109">Jedes SharePoint-Add-In enthält die Datei "appmanifest.xml". Mit der Datei "appmanifest.xml" werden SharePoint die erforderlichen Informationen zum Add-In mitgeteilt und die wichtigsten Eigenschaften des Add-Ins definiert. Nachfolgend werden einige Elemente aufgeführt, die im Manifest angegeben werden:</span><span class="sxs-lookup"><span data-stu-id="51657-p109">Every SharePoint Add-in includes an appmanifest.xml file. The appmanifest.xml tells SharePoint what it must know about the add-in and defines the add-in's most important properties. The following are some of the items that are specified in the manifest:</span></span>
 

 

- <span data-ttu-id="51657-149">Der interne Name, die Produkt-ID und die Version des Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="51657-149">The internal name, product ID, and version of the add-in.</span></span>
    
 
- <span data-ttu-id="51657-p110">Die URL der Startseite. Die Startseite ist die Seite, die beim Start des Add-Ins geöffnet wird. Es kann sich dabei um eine Seite im Add-In-Web, eine cloudbasierte Seite oder eine Seite auf einem Webserver des unabhängigen Softwareherstellers handeln.</span><span class="sxs-lookup"><span data-stu-id="51657-p110">The URL of the start page, which is the page that opens when the add-in is started. This can be a page in the add-in web, a cloud-based page, or a page on a web server of the ISV.</span></span>
    
     <span data-ttu-id="51657-p111">**Hinweis** Unter Umständen gelten Einschränkungen dafür, welche Art von Datei im **StartPage**-Element angegeben werden kann. Ausführliche Informationen finden Sie unter [StartPage Element (PropertiesDefinition ComplexType) (SharePoint-Add-In Manifest)](http://msdn.microsoft.com/library/3092674c-a6c3-9021-3d7e-e716562a4a4f%28Office.15%29.aspx). Wenn Sie mehrere Abfrageparameter im **StartPage**-Wert kombinieren, müssen Sie diese Parameter durch Angabe des Codes für das kaufmännische Und-Zeichen „`&amp;amp;`“ statt „`&amp;`“ oder eines Semikolons aneinanderreihen.</span><span class="sxs-lookup"><span data-stu-id="51657-p111">**Note**  In certain circumstances, there may be restrictions on what type of file can be specified in the  **StartPage** element. For details, see [StartPage element (PropertiesDefinition complexType) (SharePoint Add-in Manifest)](http://msdn.microsoft.com/library/3092674c-a6c3-9021-3d7e-e716562a4a4f%28Office.15%29.aspx). When you are combining more than one query parameter in the  **StartPage** value, you must use the encoded ampersand " `&amp;amp;`" rather than " `&amp;`" or a semi-colon to append them together.</span></span>
- <span data-ttu-id="51657-p112">Andere Eigenschaften des Add-Ins. Hierzu gehören der Titel und die Gebietsschemas, die von dem Add-In unterstützt werden (beides erforderlich), die URLs der Dienste, welche die Ereignisse "post-install", "post-upgrade" und "pre-uninstall" behandeln, sowie die Webvorlage, die zum Erstellen des Add-In-Webs verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="51657-p112">Other properties of the add-in. These include title and the locales supported by the add-in (both are required), the URLs of services that handle the post-install, post-upgrade, and pre-uninstall events, and the web template to use when the add-in web is created.</span></span>
    
 
- <span data-ttu-id="51657-157">Anforderungen von Berechtigungen zum Zugriff auf SharePoint-Ressourcen außerhalb des Add-In-Webs.</span><span class="sxs-lookup"><span data-stu-id="51657-157">Requests for permissions the add-in needs to SharePoint resources outside the add-in web.</span></span>
    
 
- <span data-ttu-id="51657-p113">Eine zu Authentifizierungs- und Autorisierungszwecken zu verwendende Identifikation des Add-In-Prinzipals. Diesem Prinzipal werden die Berechtigungen gewährt. Bei einem in SharePoint gehosteten Add-In ist dies nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="51657-p113">An identification, for authentication and authorization purposes, of the add-in principal. It is this principal that is granted permissions. This is not required for a SharePoint-hosted add-in.</span></span>
    
 
- <span data-ttu-id="51657-p114">Eine Liste der Voraussetzungen, falls vorhanden, die für das Add-In verfügbar sein müssen, damit das Add-In installiert werden kann. Beispielsweise kann es notwendig sein, bestimmte Features zu installieren und zu aktivieren und bestimmte Dienste zu lizenzieren und zu installieren.</span><span class="sxs-lookup"><span data-stu-id="51657-p114">A list of the prerequisites, if any, that must be available to the add-in in order for the add-in to be installed. For example, certain Features may need to be installed and activated, and certain services may need to be licensed and installed.</span></span>
    
 

 <span data-ttu-id="51657-163">**Hinweis** Lediglich die Add-In-Manifestdatei ist im Add-In-Paket erforderlich. Nicht alle oben genannten Elemente müssen in dieser Datei vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="51657-163">**Note**  The add-in manifest file is the only required item in the add-in package, but not all of the items in the previous list are required parts of the file.</span></span> 
 

<span data-ttu-id="51657-p115">Ausführliche Informationen zum Markup für das Add-In-Manifest finden Sie unter dem Knoten  [Schemareferenz für Manifeste von apps für SharePoint](http://msdn.microsoft.com/library/1f8c5d44-3b60-0bfe-9069-1df821220691%28Office.15%29.aspx). Dieses Thema ist kein Ersatz für die Informationen unter diesem Knoten, einschließlich der Informationen zu den erforderlichen Elementen und Attributen. Beachten Sie auch, dass SharePoint-Add-In-Manifeste gegenüber Office-Add-In-Manifesten ein anderes Schema aufweisen. Informationen zu Letzteren finden Sie unter  [Schemareferenz für Apps für Office-Manifeste (v1.1)](http://msdn.microsoft.com/library/7e0cadc3-f613-8eb9-57ef-9032cbb97f92%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="51657-p115">For detailed information about the add-in manifest markup, see the node  [Schema reference for manifests of SharePoint Add-ins](http://msdn.microsoft.com/library/1f8c5d44-3b60-0bfe-9069-1df821220691%28Office.15%29.aspx). This topic is not a substitute for the information in that node, including information about required elements and attributes. Also, note that SharePoint add-in manifests have a different schema from Office Add-in manifests. You can find information about the latter at  [Schema reference for Office Add-ins manifests (v1.1)](http://msdn.microsoft.com/library/7e0cadc3-f613-8eb9-57ef-9032cbb97f92%28Office.15%29.aspx).</span></span>
 

 
<span data-ttu-id="51657-p116">Es folgt ein Beispiel für die Datei "appmanifest.xml". Beachten Sie, dass in diesem Beispiel die Startseite des Add-Ins eine ASP.NET-Seite auf einem Remoteserver und keine Seite der SharePoint-Website ist. Die URL dieser Seite enthält eine Abfragezeichenfolge, mit der die URL des Hostwebs an die Remotewebanwendung übergeben wird. Der Teil "{HostUrl}" dieser Zeichenfolge ist ein Token, das beim Starten des Add-Ins aufgelöst wird. Das Add-In fordert eine Schreibberechtigung (write) für alle Listen im Hostweb an. Die Remotewebanwendung ist der Add-In-Prinzipal, dem diese Berechtigung gewährt werden muss.</span><span class="sxs-lookup"><span data-stu-id="51657-p116">The following is an example of an appmanifest.xml file. Note that in this example, the start page for the add-in is an ASP.NET page that is on a remote server, not a page on the SharePoint site. The URL for the page includes a query string that passes to the remote web application the URL of the host web. The "{HostUrl}" part of the string is a token that is resolved when the add-in is launched. The add-in is requesting Write permission to all the lists in the host web. The add-in principal that must be granted this permission is the remote web application.</span></span>
 

 
<span data-ttu-id="51657-p117">Sie müssen in Ihrem Add-In-Manifest entweder das **SupportedLocales**- oder das **SupportedLanguages**-Element verwenden. **SupportedLanguages** gilt als veraltet und wird durch **SupportedLocales** ersetzt. Das **SupportedLanguages**-Element funktioniert auch nach der Veröffentlichung, Sie sollten es jedoch nicht mehr verwenden. Weitere Informationen zu diesen Elementen finden Sie unter [SupportedLocales-Element (PropertiesDefinition ComplexType) (SharePoint-Add-In Manifest)](http://msdn.microsoft.com/library/49bde91a-8d7a-be17-4c91-82c9c19f0f61%28Office.15%29.aspx) und [SupportedLanguages-Element (PropertiesDefinition ComplexType) (SharePoint-Add-In Manifest)](http://msdn.microsoft.com/library/7a8da886-5731-9abd-2911-5cd268bba4cf%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="51657-p117">You must use either the  **SupportedLocales** or the **SupportedLanguages** element in your add-in manifest. **SupportedLanguages** is being deprecated in favor of **SupportedLocales**. The  **SupportedLanguages** element will continue to work even after release, but you should refrain from using it. For more information about these elements see [SupportedLocales element (PropertiesDefinition complexType) (SharePoint Add-in Manifest)](http://msdn.microsoft.com/library/49bde91a-8d7a-be17-4c91-82c9c19f0f61%28Office.15%29.aspx) and [SupportedLanguages element (PropertiesDefinition complexType) (SharePoint Add-in Manifest)](http://msdn.microsoft.com/library/7a8da886-5731-9abd-2911-5cd268bba4cf%28Office.15%29.aspx).</span></span>
 

 

 <span data-ttu-id="51657-p118">**Hinweis** Die Werte des **Scope**-Attributs des **AppPermissionRequest**-Elements sind wie URIs strukturiert, es handelt sich jedoch um Zeichenfolgenliterale. Im folgenden Beispiel ist kein Teil des Beispielwerts für **Scope** ein Platzhalter. Weitere Informationen zu Berechtigungen finden Sie unter [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="51657-p118">**Note**  The values of the  **Scope** attribute of the **AppPermissionRequest** element are structured like URIs, but they are actually literal strings. No part of the example **Scope** value in the following example is a placeholder. For more information about permissions, see [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint.md).</span></span>
 




```XML
<?xml version="1.0" encoding="utf-8" ?>
<App xmlns="http://schemas.microsoft.com/sharepoint/2012/app/manifest"
     ProductID="{4a07f3bd-803d-45f2-a710-b9e944c3396e}"
     Version="1.0.0.0"
     SharePointMinVersion="15.0.0.0"
     Name="MySampleApp"
>
  <Properties>
    <Title>My Sample App</Title>
    <StartPage>http://MyRemoteWebApplicationServer/default.aspx/?SPHostUrl={HostUrl}</StartPage>
    <SupportedLocales>
      <SupportedLocale CultureName="en-US" />
    </SupportedLocales>        
  </Properties>

  <AppPermissionRequests>
    <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web/list" Right="Write"/>
  </AppPermissionRequests>

  <AppPrincipal>
    <RemoteWebApplication ClientId="1ee82b34-7c1b-471b-b27e-ff272accd564" />
  </AppPrincipal>
</App>

```


### <a name="url-tokens-in-the-add-in-manifest"></a><span data-ttu-id="51657-180">URL-Token im Add-In-Manifest</span><span class="sxs-lookup"><span data-stu-id="51657-180">URL tokens in the add-in manifest</span></span>

<span data-ttu-id="51657-p119">SharePoint stellt verschiedene Token bereit, die im **StartPage**-Element und an anderen Stellen in Add-Ins und Komponenten zur Darstellung von Informationen verwendet werden können, die erst bekannt sind, wenn das Add-In ausgeführt wird. Die SharePoint-Infrastruktur löst diese Token auf. Einige Token werden am Anfang der URL angegeben, und andere Token können innerhalb einer URL verwendet werden, z. B. der Wert eines Abfrageparameters. Diese und einige andere Token können auch in verschiedenen SharePoint-Entwicklungskontexten verwendet werden. Ausführliche Informationen zu diesen Token und ihrer Verwendung finden Sie unter [URL-Zeichenfolgen und Tokens in SharePoint-Add-Ins](url-strings-and-tokens-in-sharepoint-add-ins.md). Allgemeine Informationen zu anderen Token und URLs in SharePoint finden Sie unter [URLs und Tokens in SharePoint](http://msdn.microsoft.com/library/161418d7-8123-4c4e-91a1-97e43c17f0e6%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="51657-p119">SharePoint provides several tokens that can be used in the  **StartPage** element and other places in add-ins and components of add-ins to represent information that is not known until the add-in is run. The SharePoint infrastructure resolves these tokens. Some are used at the beginning of the URL and others can be used within a URL such as the value of a query parameter. These tokens and several others can also be used in a variety of SharePoint development contexts. For detailed information about all the tokens and where they can be used, see [URL strings and tokens in SharePoint Add-ins](url-strings-and-tokens-in-sharepoint-add-ins.md). For general information about other tokens and URLs in SharePoint, see  [URLs and tokens in SharePoint](http://msdn.microsoft.com/library/161418d7-8123-4c4e-91a1-97e43c17f0e6%28Office.15%29.aspx).</span></span>
 

 

 <span data-ttu-id="51657-186">**Hinweis** Diese Token werden nicht im **Scope**-Attribut des **AppPermissionRequest**-Elements verwendet.</span><span class="sxs-lookup"><span data-stu-id="51657-186">**Note**  These tokens are not used in the  **Scope** attribute of an **AppPermissionRequest** element.</span></span>
 


## <a name="additional-resources"></a><span data-ttu-id="51657-187">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="51657-187">Additional resources</span></span>
<span data-ttu-id="51657-188"><a name="SP15Exploreappmanifest_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="51657-188"></span></span>


-  [<span data-ttu-id="51657-189">Entwickeln von SharePoint-Add-ins</span><span class="sxs-lookup"><span data-stu-id="51657-189">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="51657-190">Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="51657-190">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md)
    
 
-  [<span data-ttu-id="51657-191">Schemareferenz für Manifeste von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="51657-191">Schema reference for manifests of SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/1f8c5d44-3b60-0bfe-9069-1df821220691%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="51657-192">Open Packaging Conventions (OPC)</span><span class="sxs-lookup"><span data-stu-id="51657-192">Open Packaging Conventions (OPC)</span></span>](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx)
    
 
-  [<span data-ttu-id="51657-193">Datenebenenanwendungen (DAC)</span><span class="sxs-lookup"><span data-stu-id="51657-193">Data-Tier Application Connection (DAC)</span></span>](http://msdn.microsoft.com/en-us/library/ee210546)
    
 
-  [<span data-ttu-id="51657-194">Web Deploy 2.0</span><span class="sxs-lookup"><span data-stu-id="51657-194">Web Deploy 2.0</span></span>](http://www.iis.net/download/WebDeploy)
    
 

