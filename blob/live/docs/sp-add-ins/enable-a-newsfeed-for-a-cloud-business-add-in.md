---
title: "Aktivieren eines Newsfeesd für ein Cloud-Business-Add-In"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 7c056146fc17cb08a6d01d2ac1baedd6af01eeb2
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="enable-a-newsfeed-for-a-cloud-business-add-in"></a><span data-ttu-id="a19e7-102">Aktivieren eines Newsfeesd für ein Cloud-Business-Add-In</span><span class="sxs-lookup"><span data-stu-id="a19e7-102">Enable a newsfeed for a cloud business add-in</span></span>
<span data-ttu-id="a19e7-p101">Mit den Features für soziale Netzwerke und die Zusammenarbeit in SharePoint für Office 365 können Benutzer Aktivitäten in einer Liste verfolgen und Kommentare hinzufügen. Sie können mühelos einen Newsfeed für Ihr Cloud-Geschäfts-Add-In erstellen, indem Sie einige Eigenschaften aktivieren.</span><span class="sxs-lookup"><span data-stu-id="a19e7-p101">Social and collaboration features in SharePoint for Office 365 allow users to track activity on a list and add comments. You can easily create a newsfeed for your Cloud Business Add-in by enabling a couple of properties.</span></span>
 

 <span data-ttu-id="a19e7-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="a19e7-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="a19e7-108">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="a19e7-108">Prerequisites</span></span>

<span data-ttu-id="a19e7-109">Zum Hosten des Newsfeeds benötigen Sie in Office 365 eine SharePoint-Entwicklerwebsite, die Sie unter  [Registrieren für eine Office 365-Entwicklerwebsite](http://go.microsoft.com/fwlink/?LinkId=263490) erhalten.</span><span class="sxs-lookup"><span data-stu-id="a19e7-109">To host the newsfeed, you'll need a SharePoint Developer site on Office 365, which you can get from  [Sign up for an Office 365 Developer Site](http://go.microsoft.com/fwlink/?LinkId=263490).</span></span>
 

 

## <a name="procedures"></a><span data-ttu-id="a19e7-110">Verfahren</span><span class="sxs-lookup"><span data-stu-id="a19e7-110">Procedures</span></span>


### <a name="to-enable-a-newsfeed"></a><span data-ttu-id="a19e7-111">So aktivieren Sie einen Newsfeed</span><span class="sxs-lookup"><span data-stu-id="a19e7-111">To enable a newsfeed</span></span>


1. <span data-ttu-id="a19e7-112">Öffnen Sie im Projektmappen-Explorer die Entität, die die Liste repräsentiert, der Sie einen Newsfeed hinzufügen möchten, und klicken Sie dann in der Leiste **Perspektive** auf die Registerkarte **Server**.</span><span class="sxs-lookup"><span data-stu-id="a19e7-112">In Solution Explorer, open the entity representing the list where you want to add a newsfeed, and then on the  **Perspective** bar choose the **Server** tab.</span></span>
    
 
2. <span data-ttu-id="a19e7-113">Aktivieren Sie im Fenster **Eigenschaften** die Kontrollkästchen **Nach dem Erstellen posten** und/oder **Nach dem Aktualisieren posten**.</span><span class="sxs-lookup"><span data-stu-id="a19e7-113">In the  **Properties** window, select the **Post when Created** and/or **Post when Updated** check boxes.</span></span>
    
  ![Eigenschaften für soziales Netzwerk](../images/CBAsocial.PNG)
 

     <span data-ttu-id="a19e7-p103">Durch Aktivieren von **Nach dem Erstellen posten** wird für jedes neue Listenelement ein Thread zum Newsfeed hinzugefügt. Durch Aktivieren von **Nach dem Aktualisieren posten** wird ein Thread hinzugefügt, wenn ein Wert eines Listenelements geändert wird. Postauslöser ermitteln, welche Felder in dem Element einen Posts auslösen.</span><span class="sxs-lookup"><span data-stu-id="a19e7-p103">**Post when Created** adds a thread to the newsfeed for each new list item. **Post when Updated** adds a thread when the value for an item in the list is changed. Post triggers determine which fields in the item will trigger a post.</span></span>
    
 
3. <span data-ttu-id="a19e7-118">Klicken Sie auf den Link **Auswählen von Postauslösern**.</span><span class="sxs-lookup"><span data-stu-id="a19e7-118">Choose the  **Choose post triggers** link.</span></span>
    
    <span data-ttu-id="a19e7-119">Das Dialogfeld **Auswählen von Postauslösern** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="a19e7-119">The  **Choose post triggers** dialog box appears.</span></span>
    
 
4. <span data-ttu-id="a19e7-120">Aktivieren Sie im Dialogfeld **Auswählen von Postauslösern** die Kontrollkästchen aller Felder, die einen Post auslösen sollen, und klicken Sie anschließend auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="a19e7-120">In the  **Choose post triggers** dialog box, select the check boxes for all fields that you want to trigger a post, and then choose the **OK** button.</span></span>
    
    <span data-ttu-id="a19e7-121">Ein einzelner Thread wird für alle Änderungen in einem Element erstellt, unabhängig davon, wie viele Felder Sie auswählen.</span><span class="sxs-lookup"><span data-stu-id="a19e7-121">A single thread will be created for all changes in an item no matter how many fields you choose.</span></span>
    
 

### <a name="to-access-a-newsfeed"></a><span data-ttu-id="a19e7-122">So greifen Sie auf einen Newsfeed zu</span><span class="sxs-lookup"><span data-stu-id="a19e7-122">To access a newsfeed</span></span>


1. <span data-ttu-id="a19e7-123">Klicken Sie auf der Menüleiste auf **Debuggen**, **Debuggen starten**, um die Anwendung auszuführen.</span><span class="sxs-lookup"><span data-stu-id="a19e7-123">On the menu bar, choose  **Debug**,  **Start Debugging** to run the application.</span></span>
    
 
2. <span data-ttu-id="a19e7-p104">Öffnen Sie in der laufenden Anwendung den Suchbildschirm der Entität, die die Liste repräsentiert, der Sie einen Newsfeed hinzugefügt haben. Wenn Sie die Option **Nach dem Erstellen posten** aktiviert haben, müssen Sie ein neues Element hinzufügen. Wenn Sie die Option **Nach dem Aktualisieren posten** aktiviert haben, müssen Sie die Felder bearbeiten, die Sie im Dialogfeld **Auswählen von Postauslösern** ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="a19e7-p104">In the running application, open the browse screen for the entity representing the list where you added a newsfeed. If you enabled  **Post when Created**, add a new item. If you enabled  **Post when Updated**, edit the fields that you selected in the  **Choose post triggers** dialog box.</span></span>
    
 
3. <span data-ttu-id="a19e7-127">Klicken Sie auf der SharePoint-Chromleiste auf den Link **Newsfeed**.</span><span class="sxs-lookup"><span data-stu-id="a19e7-127">On the SharePoint chrome bar, choose the  **Newsfeed** link.</span></span>
    
  ![Die SharePoint-Chromleiste](../images/CBAnewsfeed.PNG)
 

    <span data-ttu-id="a19e7-p105">Die Seite **Newsfeed** wird in einem neuen Browserfenster geöffnet und zeigt die Einträge der hinzugefügten und/oder aktualisierten Elemente an. Sie können für einen Beitrag auf den Link **Gefällt mir** klicken oder auf den Link **Antworten** klicken, um einen Kommentar hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="a19e7-p105">The  **Newsfeed** page opens in a new browser window with entries for the added and/or updated items. You can choose the **Like** link for a post, or you can choose the **Reply** link to add a comment.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="a19e7-131">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a19e7-131">Additional resources</span></span>
<span data-ttu-id="a19e7-132"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a19e7-132"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="a19e7-133">Entwickeln von Cloud-Business-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="a19e7-133">Develop cloud business add-ins</span></span>](develop-cloud-business-add-ins.md)
    
 
-  [<span data-ttu-id="a19e7-134">Soziale Funktionen und Zusammenarbeit in SharePoint</span><span class="sxs-lookup"><span data-stu-id="a19e7-134">Social and collaboration features in SharePoint</span></span>](http://msdn.microsoft.com/en-us/library/office/jj163280.aspx)
    
 
-  [<span data-ttu-id="a19e7-135">Erstellen eines Cloud-Business-Add-Ins mit einem sozialen Newsfeed</span><span class="sxs-lookup"><span data-stu-id="a19e7-135">Create a cloud business add-in with a social newsfeed</span></span>](create-a-cloud-business-add-in-with-a-social-newsfeed.md)
    
 
