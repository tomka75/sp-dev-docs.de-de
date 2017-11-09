---
title: Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 36681335-f772-4499-8445-f94481bc18e7
ms.openlocfilehash: 7e9f0794b49f41ac405378c73fd38bf5f9323881
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="build-windows-phone-apps-that-access-sharepoint"></a><span data-ttu-id="b89fb-102">Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="b89fb-102">Build Windows Phone apps that access SharePoint</span></span>
<span data-ttu-id="b89fb-103">Erfahren Sie, wie Sie SharePoint-Add-Ins erstellen können, die SharePoint und mobilen Geräte integrieren, z. B. Windows Phone 8 und Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="b89fb-103">Learn how to create SharePoint Add-ins that integrate SharePoint and mobile devices such as Windows Phone 8 and Windows Phone 7.</span></span>
## <a name="introduction-to-building-mobile-apps-with-sharepoint"></a><span data-ttu-id="b89fb-104">Einführung in das Erstellen von mobilen Apps mit SharePoint</span><span class="sxs-lookup"><span data-stu-id="b89fb-104">Introduction to building mobile apps with SharePoint</span></span>
<span data-ttu-id="b89fb-105"><a name="SP15mobileapp_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="b89fb-105"></span></span>

<span data-ttu-id="b89fb-p101">SharePoint gibt Entwicklern die Möglichkeit, mobile Apps zu erstellen, die die Benutzer begleiten, attraktiv und interaktiv sowie immer und überall verfügbar sind, wenn die Benutzer mit ihnen arbeiten wollen. Sie können Windows Phone 8- und Windows Phone 7Anwendungen mit lokalen SharePoint-Diensten und -Anwendungen kombinieren oder mit SharePoint-Remotediensten und -anwendungen, die in der Cloud ausgeführt werden (z. B. solche, die SharePoint Online verwenden), um leistungsfähige Anwendungen zu erstellen, die die Funktionalität über den klassischen Desktop- oder Laptopcomputer hinaus in eine wirklich mobile und besser zugängliche Umgebung erweitern.</span><span class="sxs-lookup"><span data-stu-id="b89fb-p101">SharePoint provides an exciting opportunity for developers to build mobile apps that travel with users, are interactive and attractive, and are available whenever and wherever users want to work with them. You can combine Windows Phone 8 and Windows Phone 7 applications with on-premises SharePoint services and applications, or with remote SharePoint services and applications that run in the cloud (such as those that use SharePoint Online) to create powerful applications that extend the functionality beyond the traditional desktop or laptop, and into a truly portable and much more accessible environment.</span></span>
  
    
    
<span data-ttu-id="b89fb-p102">Die neuen von SharePoint bereitgestellten Mobilitätsfeatures basieren auf vorhandenen Microsoft-Tools und -Technologien wie SharePoint, Windows Phone, Visual Studio und Silverlight. Entwickler, die bereits mit diesen Technologien und deren zugehörigen Tools vertraut sind, können damit mobile Apps mit SharePoint für Windows Phone ohne Einarbeitungsphase erstellen. In diesem Abschnitt betrachten wir einige Arten von mobilen Apps mit SharePoint näher, die Sie für Windows Phone 8 und erstellen können, und sehen uns die häufigsten Möglichkeiten zum Anpassen dieser Anwendungen an. bietet ein Framework und Tools für Entwickler, einschließlich -Projektvorlagen, um mithilfe vonSharePoint Online mobile Lösungen zu erstellen, die mit SharePoint-Daten sowohl in lokalen SharePoint-Installationen als auch in der Cloud interagieren. Abbildung 1 zeigt, wie eine einfache Listenanwendung auf einem Windows Phone aussehen könnte.</span><span class="sxs-lookup"><span data-stu-id="b89fb-p102">The new mobility features offered by SharePoint are built on existing Microsoft tools and technologies, such as SharePoint, Windows Phone, Visual Studio, and Silverlight. Developers who are already familiar with those technologies and their related tools will be able to create SharePoint-powered mobile apps for Windows Phone without a steep learning curve. In this section, we explore some of the types of SharePoint-powered mobile apps you can build for Windows Phone 8 and Windows Phone 7 and the most common ways to customize those applications. SharePoint provides a framework and tools for developers, including Visual Studio 2010 project templates, to create mobile solutions that interact with SharePoint data both in on-premises SharePoint installations and in the cloud, using SharePoint Online. Figure 1 shows how a simple list application could look on Windows Phone.</span></span>
  
    
    

<span data-ttu-id="b89fb-113">**Abbildung 1. SharePoint-Listenelemente in einer Windows Phone-App**</span><span class="sxs-lookup"><span data-stu-id="b89fb-113">**Figure 1. SharePoint list items in a Windows Phone app**</span></span>

  
    
    

  
    
    
![SharePoint-Listenelemente in einer Windows Phone-App](../images/9159345c-ce12-41a6-8994-fc2e9aa26fd6.gif)
  
    
    

  
    
    

  
    
    

## <a name="what-skills-do-you-need-to-create-mobile-apps"></a><span data-ttu-id="b89fb-115">Welche Qualifikationen benötigen Sie zum Erstellen von mobilen Apps?</span><span class="sxs-lookup"><span data-stu-id="b89fb-115">What skills do you need to create mobile apps?</span></span>
<span data-ttu-id="b89fb-116"><a name="SP15buildmobile_needtoknow"> </a></span><span class="sxs-lookup"><span data-stu-id="b89fb-116"></span></span>

<span data-ttu-id="b89fb-p103">In diesem Abschnitt wird davon ausgegangen, dass Sie mit SharePoint, .NET Framework, dem Visual Studio-Entwicklungssystem und Visual C# vertraut sind. Es ist auch von Vorteil, wenn Sie über etwas Erfahrung mit der Windows Phone 8- oder Windows Phone 7-Anwendungsentwicklung mithilfe von Silverlight verfügen, und es ist hilfreich, wenn Sie mit XAML, dem StackPanel und Pivot-Steuerelementen für Windows Phone sowie mit Konzepten, wie z. B. Tombstoning, Silverlight-Datenbindung usw., vertraut sind. Wenn Sie noch nicht der Windows Phone-Anwendungsentwicklung mithilfe von Silverlight vertraut sind, empfehlen wir, dass Sie sich die folgenden Ressourcen ansehen.</span><span class="sxs-lookup"><span data-stu-id="b89fb-p103">In this section, we assume that you're familiar with SharePoint, the .NET Framework, the Visual Studio development system, and Visual C#. It's also good to have some experience with Windows Phone 8 or Windows Phone 7 application development using Silverlight, and it helps to be familiar with XAML, the StackPanel and Pivot controls for Windows Phone, and concepts such as tombstoning, Silverlight data binding, and so on. If you are new to Windows Phone application development using Silverlight, we recommend that you check out the following resources.</span></span>
  
    
    

-  [<span data-ttu-id="b89fb-120">Entwickeln einer Windows Phone-Anwendung von Anfang bis Ende</span><span class="sxs-lookup"><span data-stu-id="b89fb-120">Developing a Windows Phone Application from Start to Finish</span></span>](http://msdn.microsoft.com/en-us/library/gg680270%28v=pandp.11%29.aspx)
    
  
-  [<span data-ttu-id="b89fb-121">Benutzeroberfläche für Windows Phone</span><span class="sxs-lookup"><span data-stu-id="b89fb-121">User interface for Windows Phone</span></span>](http://msdn.microsoft.com/en-us/library/windowsphone/develop/ff967556%28v=vs.105%29.aspx)
    
  
-  [<span data-ttu-id="b89fb-122">Schnellstart: Erstellen einer Benutzeroberfläche mit XAML für Windows Phone</span><span class="sxs-lookup"><span data-stu-id="b89fb-122">Quickstart: Creating a user interface with XAML for Windows Phone</span></span>](http://msdn.microsoft.com/en-us/library/windowsphone/develop/jj207025%28v=vs.105%29.aspx)
    
  
-  [<span data-ttu-id="b89fb-123">Pivot-Steuerelementarchitektur für Windows Phone</span><span class="sxs-lookup"><span data-stu-id="b89fb-123">Pivot control architecture for Windows Phone</span></span>](http://msdn.microsoft.com/en-us/library/windowsphone/develop/ff941097%28v=vs.105%29.aspx)
    
  

## <a name="development-overview-for-mobile-apps-using-sharepoint"></a><span data-ttu-id="b89fb-124">Entwicklungsübersicht für mobile Apps mithilfe von SharePoint</span><span class="sxs-lookup"><span data-stu-id="b89fb-124">Development overview for mobile apps using SharePoint</span></span>
<span data-ttu-id="b89fb-125"><a name="SP15buildmobile_devoverview"> </a></span><span class="sxs-lookup"><span data-stu-id="b89fb-125"></span></span>

<span data-ttu-id="b89fb-p104">Sie können eine Vielzahl von mobilen Apps mithilfe von SharePoint erstellen. In diesem Abschnitt wird beschrieben, was in der Version SharePoint, die die Entwicklung mobiler Apps für Entwickler erleichtert, neu ist oder sich geändert hat.</span><span class="sxs-lookup"><span data-stu-id="b89fb-p104">You can build a wide variety of mobile apps using SharePoint. This section describes what's new or changed in the SharePoint release that makes mobile app development simple for developers.</span></span>
  
    
    

### <a name="windows-phone-sharepoint-application-template"></a><span data-ttu-id="b89fb-128">Vorlage für Windows Phone SharePoint-Anwendung</span><span class="sxs-lookup"><span data-stu-id="b89fb-128">Windows Phone SharePoint Application template</span></span>

<span data-ttu-id="b89fb-p105">Dies ist die einfachste Art von mobilen App, die Sie erstellen können, um eine normale Liste auf das Telefon zu bringen. SharePoint bietet eine Visual Studio-Vorlage, damit Sie schnell und einfach SharePoint-Listenanwendungen für Windows Phone erstellen können. Sie können z. B. eine Windows Phone-Anwendung in der Art einer "Aufgabenliste" erstellen, die Ihre Aufgabenliste aus SharePoint auf das Windows Phone bringt und Ihnen so ermöglicht, den Status einer Aufgabe mit Ihrem Telefon unterwegs zu aktualisieren. Ein weiteres Beispiel ist ein Produktkatalog für eine Bestandsliste in SharePoint, der für Vertriebsmitarbeiter auf dem Telefon verfügbar ist. Durch Installieren des Windows Phone SharePoint-SDKs erhalten Sie zwei Vorlagen für eine Windows Phone SharePoint-Anwendung in Visual Studio 2010 oder Visual Studio 2010 Express für Windows Phone. (Siehe  [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).) Mithilfe der Vorlage für die Windows Phone SharePoint-Anwendung können Sie den Schritten eines Assistenten zum Erstellen einer funktionalen Windows Phone-App folgen, die auf Daten in einer SharePoint-Liste zugreifen und diese bearbeiten dann.</span><span class="sxs-lookup"><span data-stu-id="b89fb-p105">This is the simplest type of mobile app you can build to bring a regular list to the phone. SharePoint offers a Visual Studio template to enable you to quickly and easily create SharePoint list applications for the Windows Phone. For example, you can build a "To Do List"-type Windows Phone application that brings your task list from SharePoint into the Windows Phone and enables the you to use your phone to update the status of a task on the go. Another example is having the product catalog for an inventory list in SharePoint available on the phone for the sales people. Installing the Windows Phone SharePoint SDK makes two Windows Phone SharePoint Application templates available to you in Visual Studio 2010 or Visual Studio 2010 Express for Windows Phone. (See  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).) Using the Windows Phone SharePoint List Application template, you can follow the steps of a wizard to create a functional Windows Phone app that can access and manipulate data in a SharePoint list.</span></span>
  
    
    

### <a name="new-and-enhanced-mobility-object-model-in-sharepoint"></a><span data-ttu-id="b89fb-135">Neues und verbessertes Mobilitätsobjektmodell in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b89fb-135">New and enhanced mobility object model in SharePoint</span></span>

<span data-ttu-id="b89fb-136">SharePoint Fügt mehrere neue Klassen sowohl zu den Server- als auch zu den Clientobjektmodellen hinzu, um die weiter oben in diesem Artikel beschriebenen SharePoint-Mobilitätsszenarien zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="b89fb-136">SharePoint adds several new classes to both the server and client object models to enable the SharePoint mobility scenarios that we described earlier in this article.</span></span>
  
    
    
<span data-ttu-id="b89fb-137">Um standortabhängige Apps zu aktivieren, gibt es neben mehreren zugeordneten Klassen zum Strukturieren des Werts von Ortsfeldern und deren Rendering eine neue systemeigene Feldtypklasse, **SPFieldGeoLocation**.</span><span class="sxs-lookup"><span data-stu-id="b89fb-137">To enable location-aware apps, there is a new native field type class, **SPFieldGeoLocation**, along with several associated classes for structuring the value of location fields and rendering them.</span></span> <span data-ttu-id="b89fb-138">Diese Klassen können auch im SharePoint-Clientobjektmodell für Silverlight aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="b89fb-138">These classes are also callable in the SharePoint client object model for Silverlight.</span></span> <span data-ttu-id="b89fb-139">Der neue Feldtyp enthält auch eine Definition, die der standardmäßigen SharePoint-Datei „fldtypes.xml“ hinzugefügt wurde, und neue Benutzersteuerelemente zum Rendern des Felds auf den Anzeige-, Bearbeitungs- und neuen Formularen.</span><span class="sxs-lookup"><span data-stu-id="b89fb-139">The new field type also has a definition added to the standard SharePoint fldtypes.xml file and new user controls for rendering the field on the Display, Edit, and New forms.</span></span> <span data-ttu-id="b89fb-140">Eine Übersicht finden Sie unter[Integrieren von Standort- und Kartenfunktionen in SharePoint](integrating-location-and-map-functionality-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="b89fb-140">For an overview, see  [Integrating location and map functionality in SharePoint](integrating-location-and-map-functionality-in-sharepoint.md).</span></span> 
  
    
    
<span data-ttu-id="b89fb-p107">Um die SharePoint-Authentifizierung für Windows Phone-Benutzer zu ermöglichen, umfasst das Clientobjektmodell eine neue **Authenticator**-Klasse und mehrere verknüpfte Klassen. Eine Übersicht finden Sie unter  [Übersicht über das SharePoint-Objektmodell für die mobile Clientauthentifizierung](overview-of-the-sharepoint-mobile-client-authentication-object-model.md).</span><span class="sxs-lookup"><span data-stu-id="b89fb-p107">To enable SharePoint authentication for Windows Phone users, the client object model includes a new **Authenticator** class and several associated classes. For an overview, see [Overview of the SharePoint mobile client authentication object model](overview-of-the-sharepoint-mobile-client-authentication-object-model.md).</span></span>
  
    
    
<span data-ttu-id="b89fb-p108">Um automatische Benachrichtigungen für Windows Phone-Benutzer für Ereignisse auf einer SharePoint-Farm zu ermöglichen, enthält das Serverobjektmodell mehrere neue Klassen, von denen jede auch über das Clientobjektmodell aufgerufen werden kann. Zu diesen Klassen gehören Methoden, über die sich Telefon-Apps bei SharePoint-Server-Apps für Benachrichtigungen zu bestimmten Typen von Ereignissen registrieren können. Es gibt auch Methoden, die die Server-Apps verwenden, um Benachrichtigungen an registrierte Abonnenten zu senden. Eine Übersicht finden Sie unter  [Erstellen einer SharePoint-Listen-App für Windows Phone zum Empfangen von Pushbenachrichtigungen](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md#BKMK_NotificationPhoneApp).</span><span class="sxs-lookup"><span data-stu-id="b89fb-p108">To enable automatic notifications to Windows Phone users of events on a SharePoint farm, the server object model includes several new classes, each of which is also callable from the client object model. These classes include methods that enable phone apps to register with SharePoint server apps for notifications about specified types of events. There are also methods that the server apps use to send notifications to registered subscribers. For an overview, see  [Create a Windows Phone SharePoint list app to receive push notifications](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md#BKMK_NotificationPhoneApp).</span></span>
  
    
    
<span data-ttu-id="b89fb-p109">Mit SharePoint sind Sie nicht auf die Entwicklung mobiler Apps nur für Windows Phone 8 und Windows Phone 7 beschränkt. Mit der JavaScript-Programmierschnittstelle und der neuen REST-Programmierschnitstelle (Representational State Transfer), die von SharePoint bereitgestellt wird, können Sie Anwendungen für andere Geräte als Windows Phone-Geräte erstellen. Sie können mit SharePoint-Websites mithilfe von JavaScript interagieren, das wie Skripts im Browser ausgeführt wird, oder remote mithilfe einer beliebigen Technologie, die standardmäßige REST-Funktionen unterstützt. Der folgende Abschnitt enthält einen Überblick über die REST- und JavaScript-Programmierschnittstellen.</span><span class="sxs-lookup"><span data-stu-id="b89fb-p109">With SharePoint, you're not limited to mobile app development just for Windows Phone 8 and Windows Phone 7. With the JavaScript programming interface and the new Representational State Transfer (REST) programming interface provided by SharePoint, you can create applications for non-Windows Phone mobile devices; you can interact with SharePoint sites by using JavaScript that executes as scripts in the browser, or remotely by using any technology that supports standard REST capabilities. The following section provides an overview of the REST and JavaScript programming interfaces.</span></span>
  
    
    

#### <a name="ecmascript-javascript-jscript-object-model-architecture"></a><span data-ttu-id="b89fb-150">Objektmodellarchitektur ECMAScript (JavaScript, JScript)</span><span class="sxs-lookup"><span data-stu-id="b89fb-150">ECMAScript (JavaScript, JScript) object model architecture</span></span>

<span data-ttu-id="b89fb-151">In SharePoint Foundation 2010 wurden die Clientobjektmodelle eingeführt, über die Entwickler eine Remotekommunikation mit SharePoint mithilfe einer Webprogrammiertechnologie ihrer Wahl ausführen konnten: .NET Framework, Silverlight oder JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b89fb-151">SharePoint Foundation 2010 introduced the client object models, which enabled developers to perform remote communication with SharePoint by using the web programming technology of their choice: the .NET Framework, Silverlight, or JavaScript.</span></span>
  
    
    
<span data-ttu-id="b89fb-p110">In SharePoint Foundation 2010 stellen die Clientobjektmodelle APIs bereit, mit denen Entwickler über ein Skript, das im Browser ausgeführt wird, über Code (basierend auf .NET Framework 3.5 oder höher), der in einer von .NET Framework verwalteten Anwendung ausgeführt wird, oder über Code, der in einer Silverlight 2.0-Anwendung ausgeführt wird, mit SharePoint-Websites interagieren können. Die Datei „proxy.js" und verwaltete DLL-Dateien, aus denen die Clientobjektmodelle bestehen, basieren auf dem client.svc-Webdienst und verarbeiten die effektive Batchverarbeitung, die Serialisierung von Anforderungen sowie die Analyse von Antworten. Abbildung 2 zeigt eine allgemeine Übersicht über die Architektur des SharePoint-Clientobjektmodells.</span><span class="sxs-lookup"><span data-stu-id="b89fb-p110">In SharePoint Foundation 2010, the client object models provide APIs that enable developers to interact with SharePoint sites from script that executes in the browser, from code (based on the .NET Framework 3.5 or later) that executes in a .NET Framework-managed application, or from code that executes in a Silverlight 2.0 application. The proxy .js and managed .dll files that compose the client object models are built on the client.svc web service, and handle the effective batching, serialization of requests, and parsing of replies. Figure 2 shows a high-level view of the SharePoint client object model architecture.</span></span>
  
    
    

<span data-ttu-id="b89fb-155">**Abbildung 2. Architektur des SharePoint-Clientobjektmodells**</span><span class="sxs-lookup"><span data-stu-id="b89fb-155">**Figure 2. SharePoint client object model architecture**</span></span>

  
    
    

  
    
    
![Architektur des SharePoint-Clientobjektmodells](../images/SP15Con_BuildSharePointAppsForMobileDevices_Fig3.png)
  
    
    
<span data-ttu-id="b89fb-157">Informationen zum Verwenden des JavaScript-Clientobjektmodells mit SharePoint-Daten finden Sie unter  [ECMAScript-Clientobjektmodell](http://channel9.msdn.com/learn/courses/SharePoint2010Developer/ClientObjectModel/ECMAScriptClientObjectModel).</span><span class="sxs-lookup"><span data-stu-id="b89fb-157">To learn how to use the JavaScript client object model against SharePoint data, see  [ECMAScript Client Object Model](http://channel9.msdn.com/learn/courses/SharePoint2010Developer/ClientObjectModel/ECMAScriptClientObjectModel)</span></span>
  
    
    

#### <a name="rest-endpoints-in-sharepoint"></a><span data-ttu-id="b89fb-158">REST-Endpunkte in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b89fb-158">REST endpoints in SharePoint</span></span>

<span data-ttu-id="b89fb-p111">Um die REST-Funktionen zu nutzen, die in SharePoint integriert sind, erstellen Sie mithilfe des OData-Standards (Open Data Protocol), welcher der Clientobjektmodell-API entspricht, die Sie verwenden möchten, eine RESTful-HTTP-Anforderung. Der client.svc-Webdienst verarbeitet die HTTP-Anforderung und liefert die entsprechende Antwort im Atom- oder JavaScript Object Notation (JSON)-Format. Die Clientanwendung muss diese Antwort dann analysieren. In Abbildung 3 ist eine allgemeine Ansicht der SharePoint-REST-Architektur dargestellt.</span><span class="sxs-lookup"><span data-stu-id="b89fb-p111">To use the REST capabilities that are built into SharePoint, you can construct a RESTful HTTP request using the Open Data Protocol (OData) standard that corresponds to the desired client object model API. The client.svc web service handles the HTTP request and serves the appropriate response, in either Atom or JavaScript Object Notation (JSON) format. The client application must then parse that response. Figure 3 shows a high-level view of the SharePoint REST architecture.</span></span>
  
    
    

<span data-ttu-id="b89fb-163">**Abbildung 3. SharePoint-REST-Architektur**</span><span class="sxs-lookup"><span data-stu-id="b89fb-163">**Figure 3. SharePoint REST architecture**</span></span>

  
    
    

  
    
    
![SharePoint REST-Architektur](../images/SP15Con_BuildSharePointAppsForMobileDevices_Fig2.png)
  
    
    
<span data-ttu-id="b89fb-p112">Derzeit ist der REST-Dienst in SharePoint schreibgeschützt. Dies bedeutet, dass nur REST-Endpunkte, die eine HTTP-GET-Operation darstellen, verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="b89fb-p112">Currently, the REST service in SharePoint is read-only. That is, only REST endpoints that represent an HTTP GET operation are available</span></span>
  
    
    
<span data-ttu-id="b89fb-p113">Standardmäßig werden die Antworten des SharePoint REST-Diensts mithilfe des Atom-Protokolls gemäß der OData-Spezifikation formatiert. Darüber hinaus unterstützt der REST-Dienst HTTP-Accept-Header, mit denen Entwickler angeben können, dass die Antwort im JSON-Format zurückgegeben wird. Weitere Informationen zur REST-Diensten in SharePoint finden Sie unter  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b89fb-p113">By default, the SharePoint REST service responses are formatted using the Atom protocol, according to the OData specification. In addition, the REST service supports HTTP Accept headers that enable developers to specify that the response is returned in JSON format. To learn more about REST services in SharePoint, see  [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="b89fb-170">Der SharePoint REST-Dienst unterstützt die folgenden OData-Abfrageoperatoren:</span><span class="sxs-lookup"><span data-stu-id="b89fb-170">The SharePoint REST service supports the following OData query operators:</span></span>
  
    
    

- <span data-ttu-id="b89fb-171">Filter</span><span class="sxs-lookup"><span data-stu-id="b89fb-171">Filter</span></span>
    
  
- <span data-ttu-id="b89fb-172">Take</span><span class="sxs-lookup"><span data-stu-id="b89fb-172">Take</span></span>
    
  
- <span data-ttu-id="b89fb-173">Erweitern</span><span class="sxs-lookup"><span data-stu-id="b89fb-173">Expand</span></span>
    
  

## <a name="start-developing-mobile-apps-for-sharepoint"></a><span data-ttu-id="b89fb-174">Beginnen mit der Entwicklung von mobilen Apps für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b89fb-174">Start developing mobile apps for SharePoint</span></span>
<span data-ttu-id="b89fb-175"><a name="SP15buildmobile_start"> </a></span><span class="sxs-lookup"><span data-stu-id="b89fb-175"></span></span>

<span data-ttu-id="b89fb-176">Die folgenden Vorgehensweisen und Übersichten befassen sich mit den spezifischen Informationen, die Sie benötigen, um mit der Entwicklung Ihrer mobilen Apps zu beginnen:</span><span class="sxs-lookup"><span data-stu-id="b89fb-176">The following how-tos and overviews delve into the specific information you need to start your mobile app development:</span></span>
  
    
    

-  [<span data-ttu-id="b89fb-177">Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b89fb-177">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="b89fb-178">Überblick über Anwendungsvorlagen für Windows Phone SharePoint in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b89fb-178">Overview of Windows Phone SharePoint application templates in Visual Studio</span></span>](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md)
    
  
-  [<span data-ttu-id="b89fb-179">Architektur der Vorlage Windows Phone SharePoint-Liste-Anwendung</span><span class="sxs-lookup"><span data-stu-id="b89fb-179">Architecture of the Windows Phone SharePoint List Application template</span></span>](architecture-of-the-windows-phone-sharepoint-list-application-template.md)
    
  
-  [<span data-ttu-id="b89fb-180">Vorgehensweise: Erstellen eine Windows Phone SharePoint Liste app</span><span class="sxs-lookup"><span data-stu-id="b89fb-180">How to: Create a Windows Phone SharePoint list app</span></span>](how-to-create-a-windows-phone-sharepoint-list-app.md)
    
  
-  [<span data-ttu-id="b89fb-181">Vorgehensweise: anmelden und Fortsetzen von Anrufen SharePoint Listenelementen auf einem Telefon mit Windows</span><span class="sxs-lookup"><span data-stu-id="b89fb-181">How to: Store and retrieve SharePoint list items on a Windows Phone</span></span>](how-to-store-and-retrieve-sharepoint-list-items-on-a-windows-phone.md)
    
  
-  [<span data-ttu-id="b89fb-182">Vorgehensweise: Implementieren von Validierung von Business Logik und die Daten in einem Windows Phone-app für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b89fb-182">How to: Implement business logic and data validation in a Windows Phone app for SharePoint</span></span>](how-to-implement-business-logic-and-data-validation-in-a-windows-phone-app-for-s.md)
    
  
-  [<span data-ttu-id="b89fb-183">Vorgehensweise: Support- und konvertieren SharePoint FieldTypes für Windows Phone-apps</span><span class="sxs-lookup"><span data-stu-id="b89fb-183">How to: Support and convert SharePoint field types for Windows Phone apps</span></span>](how-to-support-and-convert-sharepoint-field-types-for-windows-phone-apps.md)
    
  
-  [<span data-ttu-id="b89fb-184">Vorgehensweise: Anpassen der Liste Element Abfragen und Filtern von Daten für Windows Phone-apps</span><span class="sxs-lookup"><span data-stu-id="b89fb-184">How to: Customize list item queries and filter data for Windows Phone apps</span></span>](how-to-customize-list-item-queries-and-filter-data-for-windows-phone-apps.md)
    
  
-  [<span data-ttu-id="b89fb-185">Gewusst wie: Anpassen der Benutzeroberfläche einer SharePoint-Listen-App für Windows Phone</span><span class="sxs-lookup"><span data-stu-id="b89fb-185">How to: Customize the user interface of a SharePoint list app for Windows Phone</span></span>](how-to-customize-the-user-interface-of-a-sharepoint-list-app-for-windows-ph.md)
    
  
-  [<span data-ttu-id="b89fb-186">Vorgehensweise: Verwenden mehrerer 2013 für SharePoint-in ein Windows Phone-app Listen</span><span class="sxs-lookup"><span data-stu-id="b89fb-186">How to: Use multiple SharePoint lists in a Windows Phone app</span></span>](how-to-use-multiple-sharepoint-lists-in-a-windows-phone-app.md)
    
  
-  [<span data-ttu-id="b89fb-187">Vorgehensweise: Konfigurieren und Verwenden von Pushbenachrichtigungen in SharePoint-apps für Windows Phone</span><span class="sxs-lookup"><span data-stu-id="b89fb-187">How to: Configure and use push notifications in SharePoint apps for Windows Phone</span></span>](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md)
    
  
-  [<span data-ttu-id="b89fb-188">Integrieren von Standort- und Kartenfunktionen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b89fb-188">Integrating location and map functionality in SharePoint</span></span>](integrating-location-and-map-functionality-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b89fb-189">Vorgehensweise: Erstellen eine mobile app in SharePoint, die Daten aus einer externen Datenquelle enthält.</span><span class="sxs-lookup"><span data-stu-id="b89fb-189">How to: Create a mobile app in SharePoint that contains data from an external data source</span></span>](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md)
    
  
-  [<span data-ttu-id="b89fb-190">Vorgehensweise: Integrieren von Zuordnungen in Windows Phone-Anwendungen und SharePoint aufgelistet</span><span class="sxs-lookup"><span data-stu-id="b89fb-190">How to: Integrate maps with Windows Phone apps and SharePoint lists</span></span>](how-to-integrate-maps-with-windows-phone-apps-and-sharepoint-lists.md)
    
  
-  [<span data-ttu-id="b89fb-191">Vorgehensweise: Erstellen Suchvorgänge gesteuerte mobile Anwendungen mit der Navigation und Ereignis protokollieren von REST-Schnittstellen</span><span class="sxs-lookup"><span data-stu-id="b89fb-191">How to: Build search-driven mobile apps with the Navigation and Event Logging REST interfaces</span></span>](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="b89fb-192">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="b89fb-192">Additional resources</span></span>
<span data-ttu-id="b89fb-193"><a name="SP15buildmobile_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b89fb-193"></span></span>


  
    
    

-  [<span data-ttu-id="b89fb-194">Programmiermodelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="b89fb-194">Programming models in SharePoint</span></span>](programming-models-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b89fb-195">Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint</span><span class="sxs-lookup"><span data-stu-id="b89fb-195">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="b89fb-196">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="b89fb-196">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="b89fb-197">Microsoft SharePoint SDK für Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="b89fb-197">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [<span data-ttu-id="b89fb-198">Windows Phone SDK 7.1</span><span class="sxs-lookup"><span data-stu-id="b89fb-198">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="b89fb-199">Microsoft SharePoint SDK für Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="b89fb-199">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  
-  [<span data-ttu-id="b89fb-200">Informationen zu Expression Blend</span><span class="sxs-lookup"><span data-stu-id="b89fb-200">About Expression Blend</span></span>](http://msdn.microsoft.com/en-us/library/cc296376%28Expression.40%29.aspx)
    
  

