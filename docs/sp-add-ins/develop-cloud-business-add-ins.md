---
title: "Entwickeln von Cloud-Geschäfts-Add-Ins"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 9fea6e5b8133cceabfbb280af38d26078bc8dab3
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="develop-cloud-business-add-ins"></a><span data-ttu-id="f2cf4-102">Entwickeln von Cloud-Geschäfts-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f2cf4-102">Develop cloud business add-ins</span></span>
 <span data-ttu-id="f2cf4-p101">Cloud-Geschäfts-Add-Ins basieren auf Visual Studio LightSwitch-Technologien. Einige der Aufgaben zum Entwickeln von Cloud-Geschäfts-Add-Ins betreffen nur die Cloud-Geschäfts-Add-In-Vorlage, die meisten sind jedoch die gleichen wie für LightSwitch-HTML-Client-Add-Ins.</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p101">Cloud business add-ins are based on Visual Studio LightSwitch technologies. Some of the tasks for developing cloud business add-ins are unique to the Cloud Business Add-in template, but most are the same as for LightSwitch HTML Client add-ins.</span></span>
 

 <span data-ttu-id="f2cf4-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="cloud-business-add-in-developer-tasks"></a><span data-ttu-id="f2cf4-108">Entwickleraufgaben für Cloud-Business-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f2cf4-108">Cloud Business Add-in developer tasks</span></span>


- <span data-ttu-id="f2cf4-p103">Cloud-Business-Add-Ins werden mithilfe der Vorlage für Cloud-Business-Add-Ins in Visual Studio erstellt. Weitere Informationen finden Sie unter [Erstellen eines Cloud-Business-Add-Ins](create-a-cloud-business-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p103">Cloud business add-ins are created by using the Cloud Business Add-in template in Visual Studio. See  [Create a cloud business add-in](create-a-cloud-business-add-in.md).</span></span>
    
 
- <span data-ttu-id="f2cf4-p104">Mit der Dokumentbibliothek-Funktion in SharePoint können Sie Dokumente erstellen oder hochladen, die mit einzelnen Elementen in einer List oder Entität verknüpft sind. Weitere Informationen dazu finden Sie unter  [Zuordnen einer Dokumentbibliothek zu einer Entität](associate-a-document-library-with-an-entity.md).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p104">By using the document library feature in SharePoint, you can create or upload documents associated with individual items in a list or entity. See  [Associate a document library with an entity](associate-a-document-library-with-an-entity.md).</span></span>
    
 
- <span data-ttu-id="f2cf4-p105">Zusätzlich zu den Office-Vorlagen, die beim Hinzufügen eines Dokuments zu einer SharePoint-Dokumentbibliothek verfügbar sind, können Sie Ihre eigenen Vorlagen verwenden. Weitere Informationen finden Sie unter  [Bereitstellen einer Vorlage für eine Dokumentbibliothek in einem Cloud-Geschäfts-Add-In](provide-a-template-for-a-document-library-in-a-cloud-business-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p105">In addition to the Office templates that are available when you add a document to a SharePoint document library, you can provide your own templates. See  [Provide a template for a document library in a cloud business add-in](provide-a-template-for-a-document-library-in-a-cloud-business-add-in.md).</span></span>
    
 
- <span data-ttu-id="f2cf4-p106">Mit den Features für soziale Netzwerk und die Zusammenarbeit in SharePoint for Office 365 können Benutzer Aktivitäten in einer Liste verfolgen und Kommentare hinzufügen. Sie können mühelos einen Newsfeed für Ihre Cloud-Geschäfts-Add-Ins erstellen, indem Sie einige Eigenschaften aktivieren. Weitere Informationen dazu finden Sie unter  [Aktivieren eines Newsfeeds für ein Cloud-Geschäfts-Add-In](enable-a-newsfeed-for-a-cloud-business-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p106">Social and collaboration features in SharePoint for Office 365 allow users to track activity on a list and add comments. You can easily create a newsfeed for your Cloud Business Add-in by enabling a couple of properties. See  [Enable a newsfeed for a cloud business add-in](enable-a-newsfeed-for-a-cloud-business-add-in.md).</span></span>
    
 

## <a name="html-client-developer-tasks"></a><span data-ttu-id="f2cf4-118">Entwickleraufgaben für HTML-Client</span><span class="sxs-lookup"><span data-stu-id="f2cf4-118">HTML Client developer tasks</span></span>


- <span data-ttu-id="f2cf4-p107">Beim Entwerfen von HTML-Bildschirmen verwenden Sie hauptsächlich die Designer- und Tool-Fenster, Sie können die Bildschirme jedoch auch mithilfe von Code auf bestimmte Weise ändern. Mit den LightSwitch JavaScript-APIs können viele Aufgaben ausgeführt werden. Weitere Informationen dazu finden Sie unter  [Vorgehensweise: Ändern eines HTML-Bildschirms mithilfe von Code](http://msdn.microsoft.com/de-de/library/jj733572.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p107">When you design HTML screens, you primarily use designers and tool windows, but you can also use code to modify those screens in specific ways. By using LightSwitch JavaScript APIs, you can perform many tasks. See  [How to: Modify an HTML Screen by Using Code](http://msdn.microsoft.com/de-de/library/jj733572.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p108">Wenn Sie ein HTML-Client-Add-In entwickeln, können Sie mehrere Typen von Bildschirmen erstellen. Weitere Informationen finden Sie unter [Auswählen eines Bildschirmtyps für einen HTML-Client](http://msdn.microsoft.com/de-de/library/jj713590.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p108">When you develop an HTML client add-in, you can create several types of screens. See  [Choosing a Screen Type for an HTML Client](http://msdn.microsoft.com/de-de/library/jj713590.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p109">Erstellen Sie einen Bildschirm, um Informationen auf einem Mobilgerät anzuzeigen oder zu sammeln. Weitere Informationen finden Sie unter [Gewusst wie: Erstellen eines HTML-Clientbildschirms](http://msdn.microsoft.com/de-de/library/jj713589.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p109">Create a screen to display or collect information on a mobile device. See  [How to: Create an HTML Client Screen](http://msdn.microsoft.com/de-de/library/jj713589.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p110">Wenn Sie ein Dialogfeld oder ein Popup für Ihr Add-In erstellen, können Benutzer Informationen auf einem Telefon, Tablet oder einem anderen mobilen Gerät anzeigen oder angeben, auf dem ein Client des Add-Ins läuft. Weitere Informationen dazu finden Sie unter  [Vorgehensweise: Erstellen eines Dialogfelds oder Popups](http://msdn.microsoft.com/de-de/library/jj713587.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p110">If you create a dialog or a popup for your add-in, users can display or specify information on a phone, tablet, or other mobile device that's running a client for that add-in. See  [How to: Create a Dialog or Popup](http://msdn.microsoft.com/de-de/library/jj713587.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p111">Mit dem Bildschirm-Designer können Sie die Darstellung der Bildschirme in einem HTML-Client ändern. Weitere Informationen dazu finden Sie unter  [Vorgehensweise: Entwerfen eines HTML-Bildschirms mit dem Bildschirm-Designer](http://msdn.microsoft.com/de-de/library/jj733575.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p111">By using the screen designer, you can modify the appearance of screens in an HTML client. See  [How to: Design an HTML Screen by Using the Screen Designer](http://msdn.microsoft.com/de-de/library/jj733575.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p112">Wenn Sie ein HTML Mobile Client-Add-In entwickeln, können Sie Code hinzufügen, der ausgeführt wird, wenn der Benutzer auf einem Bildschirm im Client auf eine Schaltfläche tippt. Weitere Informationen dazu finden Sie unter  [Vorgehensweise: Hinzufügen einer Schaltfläche](http://msdn.microsoft.com/de-de/library/jj733573.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p112">When you develop an HTML mobile client add-in, you can add code that runs when the user taps a button on a screen in that client. See  [How to: Add a Button](http://msdn.microsoft.com/de-de/library/jj733573.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p113">Sie können einen Eingabewert sammeln oder einen berechneten Wert anzeigen, indem Sie ein lokales Eigenschaftsfeld zu einem Bildschirm hinzufügen. Weitere Informationen dazu finden Sie unter  [Vorgehensweise: Hinzufügen einer lokalen Eigenschaft zu einem Bildschirm](http://msdn.microsoft.com/de-de/library/jj733571.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p113">You can collect an input value or display a calculated value by adding a local property field to a screen. See  [How to: Add a Local Property to a Screen](http://msdn.microsoft.com/de-de/library/jj733571.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p114">Sie können benutzerdefinierte HTML-Steuerelemente zum Bildschirm hinzufügen. Durch die Verwendung der benutzerdefinierten Steuerelemente können Sie Informationen anzeigen und sammeln, die über die Funktionen der integrierten HTML-Steuerelemente hinausgehen. Weitere Informationen dazu finden Sie unter  [Vorgehensweise: Hinzufügen eines benutzerdefinierten Steuerelements zu einem HTML-Bildschirm](http://msdn.microsoft.com/de-de/library/jj733569.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p114">You can add custom HTML controls to a screen. By using custom controls, you can display or collect information in ways that exceed the capabilities of the built-in HTML controls. See  [How to: Add a Custom Control to an HTML Screen](http://msdn.microsoft.com/de-de/library/jj733569.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p115">Durch Filtern der Daten, die im HTML-Client angezeigt werden, können Sie den Benutzern helfen, die relevantesten Daten für ihre Aufgaben zu ermitteln. Weitere Informationen dazu finden Sie unter  [Vorgehensweise: Filtern von Daten in einem HTML-Client](http://msdn.microsoft.com/de-de/library/jj733574.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p115">By filtering the data that appears in your HTML client, you can help users identify the most relevant data for their tasks. See  [How to: Filter Data in an HTML Client](http://msdn.microsoft.com/de-de/library/jj733574.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p116">Beim Entwerfen eines HTML-Client-Add-Ins geben Sie an, wie Benutzer einen Bildschirm öffnen. Sie können einen Bildschirm öffnen, indem Sie auf ein Listenelement auf einem anderen Bildschirm oder eine Schaltfläche in der Befehlsleiste tippen. Weitere Informationen dazu finden Sie unter  [Vorgehensweise: Steuernavigation zwischen HTML-Bildschirmen](http://msdn.microsoft.com/de-de/library/jj733570.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p116">As you design an HTML client add-in, you specify how users open one screen from another. They can open a screen by tapping either a list item on another screen or a button on the command bar. See  [How to: Control Navigation between HTML Screens](http://msdn.microsoft.com/de-de/library/jj733570.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p117">Zusätzlich zur Standardnavigation können Sie ein Navigationsmenü bereitstellen, mit dem Benutzer direkt auf einen anderen Bildschirm springen können. Weitere Informationen dazu finden Sie unter  [Vorgehensweise: Erstellen eines Navigationsmenüs](http://msdn.microsoft.com/de-de/library/dn546744.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p117">In addition to the standard navigation, you can provide a navigation menu that allows users to jump directly to another screen. See  [How to: Create a Navigation Menu](http://msdn.microsoft.com/de-de/library/dn546744.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p118">Beim Entwickeln eines HTML Mobile Client-Add-Ins können Sie JavaScript-Code schreiben, der ausgeführt wird, wenn der Benutzer ein bestimmtes Ereignis auslöst. Weitere Informationen dazu finden Sie unter  [Vorgehensweise: Verarbeiten von Bildschirm-Ereignissen in einem Mobile Client](http://msdn.microsoft.com/de-de/library/jj863131.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p118">As you develop an HTML mobile client add-in, you can write JavaScript code that runs when a user initiates a certain event. See  [How to: Handle Screen Events in a Mobile Client](http://msdn.microsoft.com/de-de/library/jj863131.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p119">Sie können mobile Add-Ins erstellen, die auf SharePoint-Workflows zugreifen und sie aktualisieren. Dadurch wird sichergestellt, dass Geschäftsprozesse in einer bestimmten Abfolge durchgeführt werden. Sie können beispielsweise einen Workflow zum Weiterleiten eines Dokuments zur Genehmigung oder zum Verarbeiten einer Gehaltsliste. Weitere Informationen finden Sie unter  [Exemplarische Vorgehensweise: Zugreifen auf einen SharePoint-Workflow](http://msdn.microsoft.com/de-de/library/dn282437.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p119">You can create mobile add-ins that access and update SharePoint workflows, which help ensure that business processes are performed in a particular sequence. For example, you might use a workflow to route a document for approval or to process a payroll. See  [Walkthrough: Accessing a SharePoint Workflow](http://msdn.microsoft.com/de-de/library/dn282437.aspx).</span></span>
    
 
- <span data-ttu-id="f2cf4-p120">Mit LightSwitch können Sie einen HTML-Client erstellen, in dem mobile Benutzer Daten mit modernen berührungsgesteuerten Geräten wie Smartphones und Tablets von Remotespeicherorten anzeigen, hinzufügen und aktualisieren können. In dieser exemplarischen Vorgehensweise erstellen Sie einen Client für eine fiktive Spedition, Contoso Spedition, mit dem die Mitarbeiter des Kundendiensts leichter einschätzen können, wie viele Mitarbeiter, LKWs und Kisten für einen Auftrag erforderlich sind. Weitere Informationen finden Sie unter  [Exemplarische Vorgehensweise: Erstellen eines Clients für mobile Benutzer](http://msdn.microsoft.com/de-de/library/jj674624.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2cf4-p120">By using LightSwitch, you can create an HTML client in which mobile users can view, add, and update data from remote locations by using modern, touch-oriented devices such as phones and tablets. In this walkthrough, you'll create a client for a fictional moving company, Contoso Moving, so that its customer-service staff can more easily estimate how many people, trucks, and boxes each job will require. See  [Walkthrough: Creating a Client for Mobile Users](http://msdn.microsoft.com/de-de/library/jj674624.aspx).</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="f2cf4-152">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="f2cf4-152">Additional resources</span></span>
<span data-ttu-id="f2cf4-153"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f2cf4-153"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="f2cf4-154">Erstellen von Cloud-Business-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="f2cf4-154">Create cloud business add-ins</span></span>](create-cloud-business-add-ins.md)
    
 
-  [<span data-ttu-id="f2cf4-155">HTML-Clientbildschirme für LightSwitch-Anwendungen</span><span class="sxs-lookup"><span data-stu-id="f2cf4-155">HTML Client Screens for LightSwitch Add-ins</span></span>](http://msdn.microsoft.com/de-de/library/jj674623.aspx)
    
 

