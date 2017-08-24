# <a name="choose-patterns-for-developing-and-hosting-your-sharepoint-add-in"></a><span data-ttu-id="addf2-101">Auswählen von Mustern für die Entwicklung und das Hosten Ihres SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="addf2-101">Choose patterns for developing and hosting your SharePoint Add-in</span></span>
<span data-ttu-id="addf2-102">Lernen Sie die verschiedenen Möglichkeiten zum Hosten der Komponenten von SharePoint-Add-Ins kennen.</span><span class="sxs-lookup"><span data-stu-id="addf2-102">Learn about the different ways that you can host the components of SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="addf2-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="addf2-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="addf2-p102">Das SharePoint-Add-In-Modell führt eine breite Palette von Hosting- und Entwicklungsansätzen ein. Einige dieser Ansätze können kombiniert werden. So können Ihre Add-Ins z. B. SharePoint-gehostete und remote gehostete Komponenten verwenden. Um herauszufinden, welches Muster Sie verwenden möchten, ist es hilfreich, mit den eigenen Anforderungen, Technologien und Zielen zu beginnen und diese mit den Optionen und Möglichkeiten abzugleichen, die SharePoint-Add-Ins bieten.</span><span class="sxs-lookup"><span data-stu-id="addf2-p102">Learn about the different ways that you can host the components of SharePoint Add-ins. The SharePoint add-in model introduces a wide range of hosting and development patterns. Some of these patterns can be used in combination with each other. For example, your add-ins can mix SharePoint-hosted and remotely hosted components. The most useful way to determine which patterns you'll want to use is to start with your own requirements, technologies, and goals and match them with the options and possibilities that are enabled by SharePoint Add-ins.</span></span>
 

## <a name="what-to-think-about-when-choosing-your-development-pattern"></a><span data-ttu-id="addf2-110">Faktoren, die Sie bei der Auswahl eines Entwicklungsmusters bedenken sollten</span><span class="sxs-lookup"><span data-stu-id="addf2-110">What to think about when choosing your development pattern</span></span>
<span data-ttu-id="addf2-111"><a name="ChoosePattern"> </a></span><span class="sxs-lookup"><span data-stu-id="addf2-111"></span></span>

<span data-ttu-id="addf2-p103">SharePoint-Add-Ins erweitern die Palette möglicher Programmiersprachen und Technologiestapel, die Sie zum Arbeiten mit SharePoint-Ressourcen und -Diensten verwenden können. Welche Optionen genau zur Verfügung stehen, hängt sowohl vom Typ des Add-In als auch vom Hostingmuster ab, den Sie wählen. Sie können Ansätze auch kombinieren.</span><span class="sxs-lookup"><span data-stu-id="addf2-p103">SharePoint Add-ins widen the range of possible programming languages and technology stacks that you can use when you work with SharePoint resources and services. The precise range of options depends on both the type of add-in and the hosting pattern that you choose. It's also possible to mix patterns.</span></span>
 

 

### <a name="sharepoint-hosted-add-ins"></a><span data-ttu-id="addf2-115">Von SharePoint gehostete Add-Ins</span><span class="sxs-lookup"><span data-stu-id="addf2-115">SharePoint-hosted add-ins</span></span>
<span data-ttu-id="addf2-116"><a name="SPHosted"> </a></span><span class="sxs-lookup"><span data-stu-id="addf2-116"></span></span>

<span data-ttu-id="addf2-p104">Beginnen wir mit der einfachsten Option: in SharePoint gehostete Add-Ins oder Add-Ins, bei denen alle Komponenten entweder in einer lokalen oder einer Office 365-SharePoint-Farm gehostet werden. In SharePoint gehostete Add-Ins werden auf einer SharePoint-Website installiert, die als das Hostweb bezeichnet wird. Ihre Ressourcen werden auf einer isolierten untergeordneten Website eines Hostweb gehostet, die als dasAdd-In-Web bezeichnet wird. Es ist wichtig, [den Unterscheid zwischen Hostwebs und Add-In-Webs](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013) zu kennen. Abbildung 1 illustriert die grundlegende Architektur eines in SharePoint gehosteten Add-In.</span><span class="sxs-lookup"><span data-stu-id="addf2-p104">Start with the simplest option: SharePoint-hosted add-ins, or add-ins where all components are hosted on either an on-premises or Office 365 SharePoint farm. SharePoint-hosted add-ins are installed on a SharePoint website, called the host web. They have their resources hosted on an isolated subsite of a host web, called the add-in web. It's important to know  [the difference between host webs and add-in webs](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013). Figure 1 illustrates the basic architecture of a SharePoint-hosted add-in.</span></span>
 

 

<span data-ttu-id="addf2-122">**Abbildung 1: Architektur eines von SharePoint gehosteten Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="addf2-122">**Figure 1. SharePoint-hosted add-in architecture**</span></span>

 

 
![Die Komponenten eines von SharePoint gehosteten Add-Ins werden im Add-In-Web einer SharePoint-Farm gehostet.](../../images/SP15_hosting_SPhosted.gif)
 
<span data-ttu-id="addf2-124">Sie können ein in SharePoint gehostete Add-In mit Add-Ins kombinieren, die über remote gehostete Komponenten verfügen. Jedes Add-In oder jeder Teil eines Add-In, die auf einem Add-In-Web ausgeführt wird, hat die folgenden Anforderungen für drei Kernkomponenten: wo das Add-In gehostet wird, wie das Add-In autorisiert wird, und welche Sprache das Add-In verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="addf2-124">You can combine a SharePoint-hosted add-in with add-ins that have remotely hosted components, but any add-in or portion of an add-in that runs on an add-in web has the following set of requirements for three key components: where the add-in is hosted, how the add-in gets authorization, and what language it can use.</span></span>
 

 


|<span data-ttu-id="addf2-125">**Komponente**</span><span class="sxs-lookup"><span data-stu-id="addf2-125">**Component**</span></span>|<span data-ttu-id="addf2-126">**Anforderung für von SharePoint gehostete Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="addf2-126">**SharePoint-hosted add-in requirement**</span></span>|
|:-----|:-----|
|<span data-ttu-id="addf2-127">Wo die Komponenten des Add-Ins gehostet werden</span><span class="sxs-lookup"><span data-stu-id="addf2-127">Where the add-in components are hosted</span></span>|<span data-ttu-id="addf2-128">In der isolierten Add-In-Domäne Ihrer SharePoint-Farm</span><span class="sxs-lookup"><span data-stu-id="addf2-128">In the isolated add-in domain of your SharePoint farm</span></span>|
|<span data-ttu-id="addf2-129">Wie das Add-In autorisiert wird</span><span class="sxs-lookup"><span data-stu-id="addf2-129">How the add-in gets authorized</span></span>|<span data-ttu-id="addf2-130">Die Rechte des angemeldeten Benutzers</span><span class="sxs-lookup"><span data-stu-id="addf2-130">The privileges of the signed-in user</span></span>|
|<span data-ttu-id="addf2-131">Welche Sprache das Add-In verwenden kann</span><span class="sxs-lookup"><span data-stu-id="addf2-131">What language the add-in can use</span></span>|<span data-ttu-id="addf2-132">JavaScript (mit der SharePoint-JSOM-Bibliothek) + HTML</span><span class="sxs-lookup"><span data-stu-id="addf2-132">JavaScript (with the SharePoint JSOM library) + HTML</span></span>|
<span data-ttu-id="addf2-p105">Dieses Muster ist am einfachsten bereitzustellen, und Sie können die  [Erstellen eines einfachen von SharePoint gehosteten Add-Ins mithilfe von Napa Office 365-Entwicklungstools](create-a-basic-sharepoint-hosted-add-in-by-using-napa-office-365-development-tools) verwenden. Sie sollten Folgendes bedenken, bevor Sie sich zur Erstellung eines in SharePoint gehosteten Add-Ins entschließen.</span><span class="sxs-lookup"><span data-stu-id="addf2-p105">This pattern is the easiest to deploy, and you can use the  [Create a basic SharePoint-hosted add-in by using Napa Office 365 Development Tools](create-a-basic-sharepoint-hosted-add-in-by-using-napa-office-365-development-tools). You'll want to consider the following before deciding to create a SharePoint-hosted add-in.</span></span>
 

 


|<span data-ttu-id="addf2-135">**Erhalten Sie diese Vorteile**</span><span class="sxs-lookup"><span data-stu-id="addf2-135">**Get these benefits**</span></span>|<span data-ttu-id="addf2-136">**Berücksichtigen Sie aber Folgendes**</span><span class="sxs-lookup"><span data-stu-id="addf2-136">**But consider this**</span></span>|
|:-----|:-----|
|<span data-ttu-id="addf2-137">Allgemeine SharePoint-Artefakte, wie Listen und Webparts, können wieder verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="addf2-137">Reuse common SharePoint items, like lists and Web Parts.</span></span>|<span data-ttu-id="addf2-138">Sie können in dem Add-In nur JavaScript und keinen serverseitigen Code verwenden.</span><span class="sxs-lookup"><span data-stu-id="addf2-138">You can use only JavaScript in the add-in—you can't use any server-side code.</span></span>|
|<span data-ttu-id="addf2-139">Aufgrund der leichten Erstellung und Bereitstellung eignen sie sich gut für Produktivitätsapps für kleine Teams und Geschäftsprozessautomatisierung, mit weniger komplexen Geschäftsregeln.</span><span class="sxs-lookup"><span data-stu-id="addf2-139">Relatively easy to create and deploy, so they are good for small team productivity add-ins and business process automation, with lower complexity business rules.</span></span>|<span data-ttu-id="addf2-140">Ihr Add-In besitzt nur die Autorisierungsrechte des angemeldeten Benutzers.</span><span class="sxs-lookup"><span data-stu-id="addf2-140">Your add-in has only the authorization privileges of the signed-in user.</span></span>|
 [<span data-ttu-id="addf2-141">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="addf2-141">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
 

 

### <a name="provider-hosted-add-ins"></a><span data-ttu-id="addf2-142">Vom Anbieter gehostete Add-Ins</span><span class="sxs-lookup"><span data-stu-id="addf2-142">Provider-hosted add-ins</span></span>
<span data-ttu-id="addf2-143"><a name="SelfHosted"> </a></span><span class="sxs-lookup"><span data-stu-id="addf2-143"></span></span>

<span data-ttu-id="addf2-p106">Vom Anbieter gehostete SharePoint-Add-Ins umfassen Komponenten, die außerhalb der SharePoint-Farm bereitgestellt und gehostet werden. Sie werden im Hostweb installiert, die Remotekomponenten werden allerdings auf einem anderen Server gehostet,  *der kein Server in der SharePoint-Farm sein sollte*  . In Abbildung 2 ist die grundlegende Architektur eines vom Anbieter gehosteten Add-Ins illustriert.</span><span class="sxs-lookup"><span data-stu-id="addf2-p106">Provider-hosted SharePoint Add-ins include components that are deployed and hosted outside the SharePoint farm. They are installed to the host web, but their remote components are hosted on another server  *that should not be a server in the SharePoint farm*  . Figure 2 illustrates the basic architecture of a provider-hosted add-in.</span></span>
 

 

<span data-ttu-id="addf2-147">**Abbildung 2: Architektur eines vom Anbieter gehosteten Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="addf2-147">**Figure 2. Provider-hosted add-in architecture**</span></span>

 

 
![Die Komponenten eines vom Anbieter gehosteten Add-Ins werden über einen beliebigen Webserver oder Hostingdienst gehostet.](../../images/SP15_hosting_Provider.gif)
 
<span data-ttu-id="addf2-149">Die folgende Tabelle zeigt, dass die Anforderungen für Hosting-Orte, Add-In-Autorisierung und Sprachen bei vom Anbieter gehosteten Add-Ins um einiges geringer sind als bei in SharePoint gehosteten Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="addf2-149">The following table shows how the requirements for hosting location, add-in authorization, and languages are much less fixed for provider-hosted add-ins than they are for SharePoint-hosted add-ins.</span></span>
 

 


|<span data-ttu-id="addf2-150">**Komponente**</span><span class="sxs-lookup"><span data-stu-id="addf2-150">**Component**</span></span>|<span data-ttu-id="addf2-151">**Anforderung für vom Anbieter gehostete Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="addf2-151">**Provider-hosted add-in requirement**</span></span>|
|:-----|:-----|
|<span data-ttu-id="addf2-152">Wo die Komponenten des Add-Ins gehostet werden</span><span class="sxs-lookup"><span data-stu-id="addf2-152">Where the add-in components are hosted</span></span>|<span data-ttu-id="addf2-153">Beliebiger Webserver oder Hostingdienst</span><span class="sxs-lookup"><span data-stu-id="addf2-153">Any web server or hosting service</span></span>|
|<span data-ttu-id="addf2-154">Wie das Add-In autorisiert wird</span><span class="sxs-lookup"><span data-stu-id="addf2-154">How the add-in gets authorized</span></span>|<span data-ttu-id="addf2-155">OAuth oder die domänenübergreifende JavaScript-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="addf2-155">OAuth or the JavaScript cross-domain library</span></span>|
|<span data-ttu-id="addf2-156">Welche Sprache das Add-Inverwenden kann</span><span class="sxs-lookup"><span data-stu-id="addf2-156">What language the add-in can use</span></span>|<span data-ttu-id="addf2-157">Jede Sprache, die von Ihrem Webserver oder Hostingdienst unterstützt wird</span><span class="sxs-lookup"><span data-stu-id="addf2-157">Any language supported by your web server or hosting service</span></span>|
<span data-ttu-id="addf2-p107">Ein vom Anbieter gehostetes Add-In interagiert mit einer SharePoint-Website, verwendet aber auch Ressourcen und Dienste, die sich auf der Remotewebsite befinden. Sie sollten Folgendes bedenken, bevor Sie sich zur Erstellung eines vom Anbieter gehosteten Add-Ins entschließen.</span><span class="sxs-lookup"><span data-stu-id="addf2-p107">A provider-hosted add-in interacts with a SharePoint site but also uses resources and services that are located on the remote site. You'll want to consider the following before deciding to create a provider-hosted add-in.</span></span>
 

 


|<span data-ttu-id="addf2-160">**Erhalten Sie diese Vorteile**</span><span class="sxs-lookup"><span data-stu-id="addf2-160">**Get these benefits**</span></span>|<span data-ttu-id="addf2-161">**Berücksichtigen Sie aber Folgendes**</span><span class="sxs-lookup"><span data-stu-id="addf2-161">**But consider this**</span></span>|
|:-----|:-----|
|<span data-ttu-id="addf2-162">Sie können das Add-In auf Microsoft Azure oder einer beliebigen Remote-Webplattform hosten, einschließlich Plattformen von anderen Anbietern als Microsoft.</span><span class="sxs-lookup"><span data-stu-id="addf2-162">Host the add-in on Microsoft Azure or any remote web platform, including non-Microsoft platforms.</span></span> |<span data-ttu-id="addf2-163">Sie sind für das Erstellen der Installations-, Upgrade- und Deinstallationslogik der Remotekomponenten verantwortlich.</span><span class="sxs-lookup"><span data-stu-id="addf2-163">You are responsible for creating the installation, upgrade, and uninstallation logic of the remote components.</span></span>|
|<span data-ttu-id="addf2-164">Verwenden Sie eins der SharePoint-Clientobjektmodelle, die domänenübergreifende JavaScript-Bibliothek oder den SharePoint [REST/OData-basierten Webdienst](http://msdn.microsoft.com/magazine/dn198245.aspx) für die Interaktion mit SharePoint.</span><span class="sxs-lookup"><span data-stu-id="addf2-164">Use one of the SharePoint client object models, the JavaScript cross-domain library, or the SharePoint  [REST/OData-based web service](http://msdn.microsoft.com/magazine/dn198245.aspx) to interact with SharePoint.</span></span>|<span data-ttu-id="addf2-165">Jede Art der Interaktion mit SharePoint hat [entsprechende Optionen für den Datenzugriff](secure-data-access-and-client-object-models-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="addf2-165">Each way of interacting with SharePoint has  [corresponding options for approaches to data access](secure-data-access-and-client-object-models-for-sharepoint-add-ins).</span></span>|
|<span data-ttu-id="addf2-166">Sichern Sie sich die Autorisierung für SharePoint-Daten mithilfe von einem [der drei Autorisierungssysteme](three-authorization-systems-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="addf2-166">Gain authorization to SharePoint data using one of  [the three authorization systems](three-authorization-systems-for-sharepoint-add-ins).</span></span>|<span data-ttu-id="addf2-167">Sie müssen sich zwischen OAuth und der domänenübergreifenden Bibliothek entscheiden, um den Zugang des Add-Ins zu SharePoint zu autorisieren.</span><span class="sxs-lookup"><span data-stu-id="addf2-167">You need to decide between OAuth and the cross-domain library to authorize your add-in's access to SharePoint.</span></span>|

## <a name="match-your-hosting-pattern-with-your-development-goals"></a><span data-ttu-id="addf2-168">Abstimmen des Hostingmusters mit Ihren Entwicklungszielen</span><span class="sxs-lookup"><span data-stu-id="addf2-168">Match your hosting pattern with your development goals</span></span>
<span data-ttu-id="addf2-169"><a name="MatchPattern"> </a></span><span class="sxs-lookup"><span data-stu-id="addf2-169"></span></span>

<span data-ttu-id="addf2-p108">Bei der Auswahl eines Hostingmusters müssen Sie nicht nur die technischen Vorteile und Einschränkungen jeder Option abwägen, sondern auch Ihre Entwicklungsziele berücksichtigen. Die folgende Tabelle erleichtert Ihnen, das für Ihre Anforderungen am besten geeignete Hostingmuster zu finden.</span><span class="sxs-lookup"><span data-stu-id="addf2-p108">In addition to considering the technical advantages and constraints of each option, you'll also need to think about your development goals when deciding on a hosting pattern. You can use the following table to help sort out which hosting pattern best fits your needs.</span></span>
 

 


|<span data-ttu-id="addf2-172">**Ihre Anforderungen**</span><span class="sxs-lookup"><span data-stu-id="addf2-172">**Your requirements**</span></span>|<span data-ttu-id="addf2-173">**Empfohlenes Hostingmuster**</span><span class="sxs-lookup"><span data-stu-id="addf2-173">**Recommended Hosting pattern**</span></span>|<span data-ttu-id="addf2-174">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="addf2-174">**Example**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="addf2-175">Nur mit neuen SharePoint-Entitäten arbeiten und diese bereitstellen</span><span class="sxs-lookup"><span data-stu-id="addf2-175">Work with and provision new SharePoint entities exclusively</span></span>|<span data-ttu-id="addf2-176">Von SharePoint gehostet</span><span class="sxs-lookup"><span data-stu-id="addf2-176">SharePoint-hosted add-in</span></span>|<span data-ttu-id="addf2-177">Ein Add-In, das eine Personenauswahlsteuerung enthält und Informationen zu SharePoint-Benutzern in einer SharePoint-Liste speichert</span><span class="sxs-lookup"><span data-stu-id="addf2-177">An add-in that includes a people picker control and that stores information about SharePoint users in a SharePoint list</span></span>|
|<span data-ttu-id="addf2-178">Vorhandene SharePoint-Entitäten verwenden und mit externen Webdiensten (keine SharePoint-Webdienste) interagieren</span><span class="sxs-lookup"><span data-stu-id="addf2-178">Use existing SharePoint entities and interact with external (non-SharePoint) web services</span></span>|<span data-ttu-id="addf2-179">Vom Internetanbieter gehostet</span><span class="sxs-lookup"><span data-stu-id="addf2-179">Provider-hosted</span></span>|<span data-ttu-id="addf2-180">Ein Add-In, die Kundenadressen aus einer bestehenden SharePoint-Liste im Hostweb abruft und einen Zuordnungsdienst in einer Webanwendung verwendet, um deren Standorte anzuzeigen</span><span class="sxs-lookup"><span data-stu-id="addf2-180">An add-in that gets customer addresses from an existing SharePoint list in the host web and uses a mapping service in a web application to display their locations</span></span>|
|<span data-ttu-id="addf2-181">Neue SharePoint-Entitäten bereitstellen und mit externen Webdiensten interagieren</span><span class="sxs-lookup"><span data-stu-id="addf2-181">Provision new SharePoint entities and interact with external web services</span></span>|<span data-ttu-id="addf2-182">Kombination aus in SharePoint gehostet und vom Anbieter gehostet</span><span class="sxs-lookup"><span data-stu-id="addf2-182">Combined SharePoint-hosted and provider-hosted</span></span>|<span data-ttu-id="addf2-183">Ein Zuordnungs-Add-In, das eine SharePoint-Liste im Add-In-Web bereitstellt, sodass sie die Koordinaten (Breiten- und Längengrade) für Adressen speichern kann, die vom Benutzer angegeben werden oder aus einer vorhandenen SharePoint-Liste bezogen werden</span><span class="sxs-lookup"><span data-stu-id="addf2-183">A mapping add-in that provisions a SharePoint list on the appweb so that it can store latitude and longitude coordinates for addresses that are supplied by the user or pulled from an existing SharePoint list</span></span>|

## <a name="what-to-think-about-when-choosing-your-hosting-pattern-for-provider-hosted-add-ins"></a><span data-ttu-id="addf2-184">Was Sie bei der Auswahl des Hostingmusters für vom Anbieter gehostete Add-Ins bedenken sollten</span><span class="sxs-lookup"><span data-stu-id="addf2-184">What to think about when choosing your hosting pattern for provider-hosted add-ins</span></span>
<span data-ttu-id="addf2-185"><a name="ThinkAbout"> </a></span><span class="sxs-lookup"><span data-stu-id="addf2-185"></span></span>

<span data-ttu-id="addf2-p109">In SharePoint gehostete Add-Ins weisen ein festes Hostingmuster auf, da sie im Add-In-Web gehostet werden. Vom Anbieter gehostete Add-Ins bieten die größte Flexibilität für das Hosting der verschiedenen Komponenten Ihres Add-Ins. Wenn Sie ein Add-In erstellen möchten, müssen Sie daher Ihre Ziele und Anforderungen mit dem entsprechenden Hostingmuster abgleichen.</span><span class="sxs-lookup"><span data-stu-id="addf2-p109">SharePoint-hosted add-ins have a fixed hosting pattern, since they are hosted on the add-in web. Provider-hosted add-ins provide more flexibility for hosting the various components of your add-in, so if you choose to create one, you'll need to match your goals and requirements to the appropriate hosting pattern.</span></span> 
 

 

### <a name="oauth-or-the-cross-domain-library"></a><span data-ttu-id="addf2-188">OAuth oder die domänenübergreifende Bibliothek</span><span class="sxs-lookup"><span data-stu-id="addf2-188">OAuth or the cross-domain library</span></span>

<span data-ttu-id="addf2-p110">Eine der wichtigsten Fragen, die Sie sich stellen sollten, wenn Sie vom Anbieter gehostete Add-Ins in Betracht ziehen und sich über deren Erstellung Gedanken machen, ist, wie das Add-In die Autorisierung zur Interaktion mit SharePoint erhält. Vom Anbieter gehostete Add-Ins bieten Ihnen zwei Optionen: die domänenübergreifende JavaScript-Bibliothek und OAuth.</span><span class="sxs-lookup"><span data-stu-id="addf2-p110">One of the most important questions you need to ask when considering provider-hosted add-ins and how you'll build them is how the add-in will get authorization to interact with SharePoint. Provider-hosted add-ins give you two choices: the JavaScript cross-domain library and OAuth.</span></span> 
 

 
<span data-ttu-id="addf2-p111">Über die  [domänenübergreifende Bibliothek](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library)können Sie von den Remotekomponenten Ihres Add-Ins über einen Proxy mit mehr als einer Domäne interagieren. Wenn clientseitiger Code und die Berechtigungen eines Benutzers ausreichen, der bei SharePoint angemeldet ist, ist die domänenübergreifende Bibliothek eine gute Option. Die domänenübergreifende Bibliothek ist auch praktisch, wenn Sie Remoteaufrufe durch eine Firewall durchführen.</span><span class="sxs-lookup"><span data-stu-id="addf2-p111">The  [cross-domain library](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library) lets you interact with more than one domain from the remote components of your add-in through a proxy. If client-side code and the permissions of a user who is signed in to SharePoint are sufficient, the cross-domain library is a good option. The cross-domain library is also convenient whenever you are making remote calls through a firewall.</span></span>
 

 
<span data-ttu-id="addf2-p112">OAuth ist ein offenes Protokoll für die Autorisierung, das auf leicht verwaltbare Weise eine sichere Autorisierung von Clientanwendungen (Desktop-, Web- und mobile Anwendungen) ermöglicht. Wenn Sie planen, ein Add-In für SharePoint zu erstellen, das in einer Remotewebanwendung ausgeführt wird und an SharePoint zurückkommuniziert, müssen Sie oft OAuth verwenden. OAuth ist immer erforderlich, wenn Sie SharePoint von einer remote gehosteten Webanwendung aufrufen, die nicht ausschließlich clientseitigen Code (HTML + JavaScript) verwenden kann.  [Erfahren Sie mehr über die Funktionsweise von OAuth in Add-Ins für SharePoint.](creating-sharepoint-add-ins-that-use-low-trust-authorization)</span><span class="sxs-lookup"><span data-stu-id="addf2-p112">OAuth is an open protocol for authorization that enables secure authorization from client applications (desktop, web, and mobile applications) in an easily manageable way. If you plan to build a SharePoint Add-in that runs in a remote web application and communicates back to SharePoint, you will often need to use OAuth. OAuth is required whenever you are calling into SharePoint from a remotely hosted web application that can't use client-side code (HTML + JavaScript) exclusively.  [Learn more about how OAuth works in SharePoint Add-ins.](creating-sharepoint-add-ins-that-use-low-trust-authorization)</span></span>
 

 
 <span data-ttu-id="addf2-198">Unter  [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins) und [Drei Autorisierungssysteme für SharePoint-Add-Ins](three-authorization-systems-for-sharepoint-add-ins) wird die Auswahl zwischen OAuth und der domänenübergreifenden Bibliothek ausführlicher erläutert.</span><span class="sxs-lookup"><span data-stu-id="addf2-198">[Secure data access and client object models for SharePoint Add-ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins) and [Three authorization systems for SharePoint Add-ins](three-authorization-systems-for-sharepoint-add-ins) explain the choice between OAuth and the cross-domain library more thoroughly.</span></span>
 

 

### <a name="oauth-with-on-premises-sharepoint-farms"></a><span data-ttu-id="addf2-199">OAuth mit lokalen SharePoint-Farmen</span><span class="sxs-lookup"><span data-stu-id="addf2-199">OAuth with on-premises SharePoint farms</span></span>

<span data-ttu-id="addf2-p113">Wenn Sie eine lokale Bereitstellung von SharePoint verwenden, können Sie OAuth benutzen, müssen sich aber zwischen der Erstellung eines besonders vertrauenswürdigen Add-Ins und der Verwendung eines Office 365-Mandanten entscheiden. Office 365 verwendet Microsoft Azure Access Control Service (ACS) als Vertrauensbroker, und wenn Sie keinen Zugriff auf einen Office 365-Mandanten haben, müssen Sie  [Erstellen besonders vertrauenswürdiger Add-Ins für SharePoint](create-high-trust-sharepoint-add-ins) verwenden, das Zertifikate für die Einrichtung einer Vertrauensstellung zwischen Ihrem Add-In und SharePoint benutzt. Sie können besonders vertrauenswürdige Add-Ins zum Add-In-Katalog Ihrer SharePoint-Farm hinzufügen, können sie aber nicht im Office Store verkaufen. Wenn Sie Zugriff auf einen Office 365-Mandanten haben, können Sie diesen mit Ihrer lokalen Installation von SharePoint verknüpfen und [ACS als Vertrauensbroker für Add-Ins verwenden, die in Ihrer lokalen SharePoint-Bereitstellung installiert werden](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site).</span><span class="sxs-lookup"><span data-stu-id="addf2-p113">If you are using an on-premises deployment of SharePoint, you can use OAuth, but you will have to choose between creating high-trust add-ins and using an Office 365 tenancy. Office 365 uses Microsoft Azure Access Control Service (ACS) as the trust broker, and if you do not have access to an Office 365 tenancy, you'll need to use  [Create high-trust SharePoint Add-ins](create-high-trust-sharepoint-add-ins), which uses certificates to establish trust between your add-in and SharePoint. You can add high trust add-ins to the add-in catalog of your SharePoint farm, but you can't sell them in the Office Store. If you do have access to an Office 365 tenancy, you can link it to your on-premises installation of SharePoint and  [use ACS as the trust broker for add-ins that are installed to your on-premises SharePoint](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site).</span></span>
 

 
<span data-ttu-id="addf2-p114">In der folgenden Tabelle sind alle möglichen Ansätze für das Hosting der SharePoint-Komponenten und der Remotekomponenten Ihres Add-Ins sowie die Vertrauensbroker aufgeführt, die Ihnen bei Verwendung von OAuth zur Verfügung stehen. Beachten Sie, dass Sie Zugriff auf einen Office 365-Mandanten benötigen, um ACS zur Einrichtung einer Vertrauensstellung zwischen SharePoint und einer SharePoint-Add-In zu verwenden, die in einer lokalen Installation von SharePoint installiert ist.</span><span class="sxs-lookup"><span data-stu-id="addf2-p114">The following table lists all of the possible patterns for hosting both the SharePoint components and the remote components of your add-in, along with the trust brokers that are available to you if you're using OAuth. Note that you'll need access to an Office 365 tenant in order to use ACS to establish trust between SharePoint and a SharePoint Add-in that is installed to an on-premises installation of SharePoint.</span></span>
 

 


|<span data-ttu-id="addf2-206">**Speicherort der SharePoint-Komponenten**</span><span class="sxs-lookup"><span data-stu-id="addf2-206">**SharePoint component location**</span></span>|<span data-ttu-id="addf2-207">**Speicherort der Remotekomponenten**</span><span class="sxs-lookup"><span data-stu-id="addf2-207">**Remote component location**</span></span>|<span data-ttu-id="addf2-208">**Vertrauensbroker**</span><span class="sxs-lookup"><span data-stu-id="addf2-208">**Trust broker**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="addf2-209">Lokal</span><span class="sxs-lookup"><span data-stu-id="addf2-209">On premises</span></span>|<span data-ttu-id="addf2-210">In Cloud</span><span class="sxs-lookup"><span data-stu-id="addf2-210">In cloud</span></span>|<span data-ttu-id="addf2-211">ACS, Zertifikat</span><span class="sxs-lookup"><span data-stu-id="addf2-211">ACS, certificate</span></span>|
|<span data-ttu-id="addf2-212">Lokal</span><span class="sxs-lookup"><span data-stu-id="addf2-212">On premises</span></span>|<span data-ttu-id="addf2-213">Lokal</span><span class="sxs-lookup"><span data-stu-id="addf2-213">On premises</span></span>|<span data-ttu-id="addf2-214">ACS, Zertifikat</span><span class="sxs-lookup"><span data-stu-id="addf2-214">ACS, certificate</span></span>|
|<span data-ttu-id="addf2-215">Office 365 SharePoint-Website</span><span class="sxs-lookup"><span data-stu-id="addf2-215">Office 365 SharePoint site</span></span>|<span data-ttu-id="addf2-216">In Cloud</span><span class="sxs-lookup"><span data-stu-id="addf2-216">In cloud</span></span>|<span data-ttu-id="addf2-217">ACS</span><span class="sxs-lookup"><span data-stu-id="addf2-217">ACS</span></span>|
|<span data-ttu-id="addf2-218">Office 365 SharePoint-Website</span><span class="sxs-lookup"><span data-stu-id="addf2-218">Office 365 SharePoint site</span></span>|<span data-ttu-id="addf2-219">Lokal</span><span class="sxs-lookup"><span data-stu-id="addf2-219">On premises</span></span>|<span data-ttu-id="addf2-220">ACS</span><span class="sxs-lookup"><span data-stu-id="addf2-220">ACS</span></span>|

## <a name="combine-provider-hosting-and-sharepoint-hosting"></a><span data-ttu-id="addf2-221">Kombinieren von Anbieterhosting und SharePoint-Hosting</span><span class="sxs-lookup"><span data-stu-id="addf2-221">Combine provider hosting and SharePoint hosting</span></span>
<span data-ttu-id="addf2-222"><a name="Combined"> </a></span><span class="sxs-lookup"><span data-stu-id="addf2-222"></span></span>

<span data-ttu-id="addf2-p115">Sie können auch Add-Ins erstellen, die sowohl in SharePoint gehostete als auch in der Cloud gehostete Komponenten enthalten. Sie können z. B. ein  [in der Cloud gehostete Add-In erstellen, das eine benutzerdefinierte SharePoint-Liste und einen benutzerdefinierten Inhaltstyp enthält](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type). Wenn Sie diese Architektur wählen, müssen in Ihrem Entwurf und Muster die im Modell enthaltenen Sicherheitseinschränkungen berücksichtigt werden. Sie können in den von SharePoint gehosteten Codekomponenten nur JavaScript verwenden, und die remote gehosteten Komponenten müssen OAuth oder die domänenübergreifende Bibliothek für die Interaktion mit der SharePoint-Website benutzen. Wenn Sie dieses Muster in Erwägung ziehen, sollten Sie die  [Funktionsweise der Add-In-Autorisierung in SharePoint](authorization-and-authentication-of-sharepoint-add-ins) verstehen. Abbildung 4 zeigt die Funktionsweise dieser Architektur, wenn Sie Microsoft Azure zum Hosten der Remotekomponenten Ihres Add-Ins sowie OAuth verwenden.</span><span class="sxs-lookup"><span data-stu-id="addf2-p115">You can also build add-ins that include both SharePoint-hosted and cloud-hosted components. For example, you can create a  [cloud-hosted add-in that includes a custom SharePoint list and content type](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type). If you choose to use this architecture, your design and approach must account for security limitations that are built into the model. You can use only JavaScript in the code components that are hosted by SharePoint, and the remotely hosted components must use either OAuth or the cross-domain library to interact with the SharePoint website. When considering this approach, make sure that you understand how  [add-in authorization works in SharePoint](authorization-and-authentication-of-sharepoint-add-ins). Figure 4 shows you how this architecture works if you use Microsoft Azure to host the remote components of your add-in, and you use OAuth.</span></span>
 

 

<span data-ttu-id="addf2-229">**Abbildung 4: Kommunikation zwischen Servern für SharePoint-Add-Ins bei Verwendung von OAuth und Windows Azure**</span><span class="sxs-lookup"><span data-stu-id="addf2-229">**Figure 4. SharePoint add-in server-to-server communication when you use OAuth and Windows Azure**</span></span>

 

 
![Einschränkungen für die Kommunikation zwischen Servern](../../images/SP15HelloWorldSPApp_Fig01.png)
 
 [<span data-ttu-id="addf2-231">Erfahren Sie, wie Sie ein Add-In erstellen, das Cloud-Hosting und SharePoint-Hosting kombiniert.</span><span class="sxs-lookup"><span data-stu-id="addf2-231">Learn how to create an add-in that combines cloud hosting and SharePoint hosting.</span></span>](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type)
 

 
<span data-ttu-id="addf2-232">Hier sind einige Punkte, über die Sie nachdenken sollten, wenn Sie eine Kombination aus Anbieterhosting und SharePoint-Hosting in Erwägung ziehen.</span><span class="sxs-lookup"><span data-stu-id="addf2-232">Here are some things to think about when you're considering a combination of provider hosting and SharePoint hosting.</span></span>
 

 


|<span data-ttu-id="addf2-233">**Erhalten Sie diese Vorteile**</span><span class="sxs-lookup"><span data-stu-id="addf2-233">**Get these benefits**</span></span>|<span data-ttu-id="addf2-234">**Berücksichtigen Sie aber Folgendes**</span><span class="sxs-lookup"><span data-stu-id="addf2-234">**But consider this**</span></span>|
|:-----|:-----|
|<span data-ttu-id="addf2-235">Alle Vorteile von beiden Ansätzen werden kombiniert.</span><span class="sxs-lookup"><span data-stu-id="addf2-235">All the benefits of the two approaches.</span></span>|<span data-ttu-id="addf2-236">Die komplexere Architektur erfordert sorgfältige Planung bezüglich der Kommunikation zwischen Servern und der Einschränkungen für siteübergreifendes Skripting.</span><span class="sxs-lookup"><span data-stu-id="addf2-236">More complex architecture requires careful planning around server-to-server communication and cross-site scripting restrictions.</span></span>|

## <a name="provider-hosted-add-ins-in-azure-web-roles"></a><span data-ttu-id="addf2-237">Vom Anbieter gehostete Add-Ins in Azure-Webrollen</span><span class="sxs-lookup"><span data-stu-id="addf2-237">Provider-hosted add-ins in Azure Web Roles</span></span>
<span data-ttu-id="addf2-238"><a name="AzureWebRole"> </a></span><span class="sxs-lookup"><span data-stu-id="addf2-238"></span></span>

<span data-ttu-id="addf2-p116">Sie können eine vom Anbieter gehostete SharePoint-Add-In in einer Microsoft Azure-Webrolle statt in einer Webanwendung (unabhängig davon, ob die Webanwendung lokal oder eine Azure-Website ist) hosten. Eine Azure-Webrolle ist äußerst wichtig, und eine Website auf Grundlage der Internetinformationsdienste und ein Hosting auf Azure. Sie können den Vorteil der Hostingdienste und die Skalierbarkeit der Azure-Webrollen nutzen. Sie können außerdem die Leistung und Benutzerfreundlichkeit Ihrer SharePoint-Add-In verbessern, insbesondere, wenn das Add-In häufig genutzt wird oder sich die Anfrage danach im Laufe der Zeit ändert. Wenn die SharePoint-Add-In weitere Serverressourcen benötigt, kann Azure sie dynamisch dem Add-In zuordnen.</span><span class="sxs-lookup"><span data-stu-id="addf2-p116">You can host a provider-hosted SharePoint Add-in on a Microsoft Azure web role instead of a web application (whether the web application is on-premises or a Azure Web Site). An Azure web role is, essentially, a website that's based on Internet Information Services (IIS) and hosted on Azure. You can take advantage of the hosting services and scalability of Azure web roles. You can also enhance the performance and usability of your SharePoint Add-in, especially if the add-in is heavily used or demand for it changes over time. If the SharePoint Add-in ever requires more server resources, Azure can dynamically allocate them to the add-in.</span></span>
 

 
<span data-ttu-id="addf2-244">Unter den folgenden Links finden Sie weitere Informationen zu Azure-Webrollen:</span><span class="sxs-lookup"><span data-stu-id="addf2-244">See the following links for more information about Azure web roles.</span></span>
 

 

-  [<span data-ttu-id="addf2-245">Was ist ein Clouddienst?</span><span class="sxs-lookup"><span data-stu-id="addf2-245">What is a cloud service?</span></span>](http://www.windowsazure.com/en-us/manage/services/cloud-services/what-is-a-cloud-service/)
    
 
-  [<span data-ttu-id="addf2-246">Einführung in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="addf2-246">Introducing Microsoft Azure</span></span>](http://www.windowsazure.com/en-us/develop/net/fundamentals/intro-to-windows-azure/)
    
 
-  [<span data-ttu-id="addf2-247">Automatische Skalierung und Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="addf2-247">Autoscaling and Microsoft Azure</span></span>](http://msdn.microsoft.com/en-us/library/hh680945%28v=pandp.50%29.aspx)
    
 
<span data-ttu-id="addf2-248">Als Voraussetzung benötigen Sie das Microsoft Azure SDK für .NET (VS 2012) 1.8.1, das Sie mithilfe des  [Webplattform-Installer](http://www.microsoft.com/web/downloads/platform.aspx). installieren können</span><span class="sxs-lookup"><span data-stu-id="addf2-248">As a prerequisite, you will need the Microsoft Azure SDK for .NET (VS 2012) 1.8.1, which you can install by using the  [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
 

 
<span data-ttu-id="addf2-249">Die Art, wie Sie das Projekt in vsnv erstellen, hängt davon ab, ob Sie ein SharePoint Add-In-Projekt starten und anschließend das Azure-Webrollenprojekt hinzufügen, oder das Azure-Projekt starten und anschließend das SharePoint-Projekt hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="addf2-249">The way that you use create the project in vsnv depends on whether you start with a SharePoint Add-in project and then add the Azure web role project, or you start with the Azure project and then add the SharePoint project.</span></span>
 

 

### <a name="add-a-cloud-service-to-an-existing-add-in"></a><span data-ttu-id="addf2-250">Hinzufügen eines Clouddiensts zu einem vorhandenen Add-In</span><span class="sxs-lookup"><span data-stu-id="addf2-250">Add a cloud service to an existing add-in</span></span>

<span data-ttu-id="addf2-p117">Wenn Sie bereits ein vom Anbieter gehostetes SharePoint-Add-In haben, das Sie auf Azure hosten möchten, wählen Sie in der Projektmappe für das SharePoint-Add-In das Webanwendungsprojekt aus. Klicken Sie in der Menüleiste auf **Projekt**, **Microsoft Azure-Clouddienstprojekt hinzufügen**. Es wird ein Azure-Projekt mit der Bezeichnung _NameOfTheWebAppProject_.Azure zur Projektmappe Ihres SharePoint-Add-Ins hinzugefügt. Eine Webrolle für das Webprojekt wird ebenfalls zum Projekt für den Azure-Clouddienst hinzugefügt. Office Developer Tools für Visual Studio 2012 legt die erforderlichen Projekteigenschaften fest, sodass die Webrolle mit dem SharePoint-Add-In arbeiten kann.</span><span class="sxs-lookup"><span data-stu-id="addf2-p117">If you already have a provider-hosted SharePoint Add-in that you want to host on Azure, choose the web application project in the solution for the SharePoint Add-in. On the menu bar, choose **Project**, **Add Microsoft Azure Cloud Service Project**. A Azure project, called  _NameOfTheWebAppProject_.Azure, is added to the solution for your SharePoint Add-in. A web role for the web project is also added to the project for the Azure cloud service. The Office Developer Tools for Visual Studio 2012 sets the necessary project properties so that the web role can work with the SharePoint Add-in.</span></span>
 

 

### <a name="add-an-add-in-to-an-existing-web-role"></a><span data-ttu-id="addf2-256">Hinzufügen eines Add-Ins zu einer vorhandenen Webrolle</span><span class="sxs-lookup"><span data-stu-id="addf2-256">Add an add-in to an existing web role</span></span>

<span data-ttu-id="addf2-p118">Wenn Sie bereits eine Webrolle in einem Azure-Clouddienst haben, den Sie als Host für ein vom Anbieter gehostetes SharePoint-Add-In verwenden möchten, öffnen Sie das Azure-Cloudprojekt in Visual Studio, und wählen Sie dann im **Projektmappen-Explorer** das Webrollenprojekt aus. Klicken Sie in der Menüleiste auf **Projekt**, **SharePoint-Add-In-Projekt hinzufügen**. Ein Projekt für ein vom Anbieter gehostetes SharePoint-Add-In mit der Bezeichnung _NameOfTheWebAppProject_.Azure wird erstellt und zur Projektmappe hinzugefügt. Visual Studio verweist auf die Azure-Webrolle als Web-Projekthost für das SharePoint-Add-In.</span><span class="sxs-lookup"><span data-stu-id="addf2-p118">If you already have a web role in an Azure cloud service that you want to use as a host for a provider-hosted SharePoint Add-in, open the Azure cloud project in Visual Studio, and then, in **Solution Explorer**, choose the web role project. On the menu bar, choose **Project**, **Add Add-in for SharePoint Project**. A project for a provider-hosted SharePoint Add-in is created, called  _NameOfTheWebAppProject_.Azure, and added to the solution. Visual Studio references the Azure web role as the web project host for the SharePoint Add-in.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="addf2-261">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="addf2-261">Additional resources</span></span>
<span data-ttu-id="addf2-262"><a name="SPAppModelArch_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="addf2-262"></span></span>

<span data-ttu-id="addf2-263">Weitere Informationen finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="addf2-263">For more information, see the following resources:</span></span>
 

 

-  [<span data-ttu-id="addf2-264">Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="addf2-264">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 
-  [<span data-ttu-id="addf2-265">SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="addf2-265">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="addf2-266">Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="addf2-266">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="addf2-267">Autorisierung und Authentifizierung von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="addf2-267">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="addf2-268">OAuth-Ablauf mit Kontexttoken für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="addf2-268">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="addf2-269">Verwenden einer Office 365 SharePoint-Website, um vom Anbieter gehostete Add-Ins auf einer lokalen SharePoint-Website zu autorisieren</span><span class="sxs-lookup"><span data-stu-id="addf2-269">Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site</span></span>](use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site)
    
 
-  [<span data-ttu-id="addf2-270">SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen</span><span class="sxs-lookup"><span data-stu-id="addf2-270">SharePoint Add-ins compared with SharePoint solutions</span></span>](http://msdn.microsoft.com/library/0e9efadb-aaf2-4c0d-afd5-d6cf25c4e7a8%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="addf2-271">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="addf2-271">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="addf2-272">Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="addf2-272">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="addf2-273">Erstellen eines von einem Anbieter gehosteten Add-Ins, das eine benutzerdefinierte SharePoint-Liste und einen benutzerdefinierten Inhaltstyp enthält</span><span class="sxs-lookup"><span data-stu-id="addf2-273">Create a provider-hosted add-in that includes a custom SharePoint list and content type</span></span>](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type)
    
 

