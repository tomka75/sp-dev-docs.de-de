---
title: "Einfügen eines Add-In-Webparts in das vom Anbieter gehostete Add-In"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 24b4138796d5a0a9c899f232e1cc4643cc04d772
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="include-an-add-in-part-in-the-provider-hosted-add-in"></a><span data-ttu-id="272ac-102">Einfügen eines Add-In-Webparts in das vom Anbieter gehostete Add-In</span><span class="sxs-lookup"><span data-stu-id="272ac-102">Include an add-in part in the provider-hosted add-in</span></span>
<span data-ttu-id="272ac-103">Erfahren Sie, wie Sie ein Remotewebformular in einer SharePoint-Seite in einem vom Anbieter gehosteten SharePoint-Add-In anzeigen.</span><span class="sxs-lookup"><span data-stu-id="272ac-103">Learn how to surface a remote web form in a SharePoint page in a provider-hosted SharePoint Add-in.</span></span>
 

 <span data-ttu-id="272ac-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="272ac-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="272ac-107">Dies ist der sechste in einer Reihe von Artikeln über die Grundlagen der Entwicklung von vom Anbieter gehosteten SharePoint-Add-Ins. Sie sollten sich zuerst mit [SharePoint Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut machen:</span><span class="sxs-lookup"><span data-stu-id="272ac-107">This is the sixth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="272ac-108">Erste Schritte beim Erstellen von von einem Anbieter gehosteten SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="272ac-108">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="272ac-109">Übertragen des SharePoint-Aussehens und -Verhaltens auf Ihr vom Anbieter gehostetes Add-In</span><span class="sxs-lookup"><span data-stu-id="272ac-109">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
    
 
-  [<span data-ttu-id="272ac-110">Einfügen einer benutzerdefinierten Schaltfläche in das vom Anbieter gehostete Add-In</span><span class="sxs-lookup"><span data-stu-id="272ac-110">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in.md)
    
 
-  [<span data-ttu-id="272ac-111">Schnelle Übersicht über das SharePoint-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="272ac-111">Get a quick overview of the SharePoint object model</span></span>](get-a-quick-overview-of-the-sharepoint-object-model.md)
    
 
-  [<span data-ttu-id="272ac-112">Hinzufügen von SharePoint-Schreibvorgängen zum vom Anbieter gehosteten Add-In</span><span class="sxs-lookup"><span data-stu-id="272ac-112">Add SharePoint write operations to the provider-hosted add-in</span></span>](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)
    
 

 <span data-ttu-id="272ac-p102">**Hinweis** Wenn Sie diese Reihe zu vom Anbieter gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) herunterladen und die Datei „BeforeAdd-inPart.sln“ öffnen.</span><span class="sxs-lookup"><span data-stu-id="272ac-p102">**Note**  If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeAdd-inPart.sln file.</span></span>
 

<span data-ttu-id="272ac-p103">In diesem Artikel fügen Sie eine besondere Art von Webpart namens Add-In-Webpart zum SharePoint-Add-In hinzu. Das Add-In-Webpart stellt das Bestellformular des Add-Ins Bestellformular auf einer SharePoint-Seite zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="272ac-p103">In this article, you add a special kind of Web Part, called an add-in part to the SharePoint Add-in. The add-in part exposes the add-in's order form on a SharePoint page.</span></span>
 

## <a name="create-the-add-in-part"></a><span data-ttu-id="272ac-117">Erstellen des Add-In-Webparts</span><span class="sxs-lookup"><span data-stu-id="272ac-117">Create the add-in part</span></span>


 

 

 <span data-ttu-id="272ac-p104">**Hinweis** Die Einstellungen für Startprojekte in Visual Studio werden normalerweise auf die Standardwerte zurückgesetzt, wann immer die Projektmappe erneut geöffnet wird. Führen Sie die folgenden Schritte immer unmittelbar nach dem erneuten Öffnen der Beispielprojektmappe in dieser Artikelreihe durch: Klicken Sie mit der rechten Maustaste oben im **Projektmappen-Explorer** auf den Projektmappenknoten, und wählen Sie **Startprojekte festlegen** aus. Stellen Sie sicher, dass alle drei Projekte in der Spalte **Aktion** auf **Starten** festgelegt sind.</span><span class="sxs-lookup"><span data-stu-id="272ac-p104">**Note**   The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles: Right-click the solution node at the top of **Solution Explorer** and select **Set startup projects**.  Make sure all three projects are set to **Start** in the **Action** column.</span></span>
 


1. <span data-ttu-id="272ac-121">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das **ChainStore**-Projekt, und wählen Sie **Hinzufügen | Neues Element** aus.</span><span class="sxs-lookup"><span data-stu-id="272ac-121">In  **Solution Explorer**, right-click the  **ChainStore** project and select **Add | New Item**.</span></span>
    
 
2. <span data-ttu-id="272ac-p105">Wählen Sie **Clientwebpart (Hostweb)** aus, nennen Sie es „Bestellung absenden“, und klicken Sie dann auf **Hinzufügen**. (Clientwebpart ist eine andere Bezeichnung für Add-In-Webpart.)</span><span class="sxs-lookup"><span data-stu-id="272ac-p105">Select  **Client Web Part (Host Web)**, give it the name Place Order, and then press  **Add**. ("Client Web Part" is another name for "add-in part".)</span></span>
    
 
3. <span data-ttu-id="272ac-124">Wählen Sie auf der nächsten Seite des Assistenten das zweite Optionsfeld aus: **URL einer vorhandenen Webseite für den Clientwebpart-Inhalt auswählen oder eingeben**.</span><span class="sxs-lookup"><span data-stu-id="272ac-124">On the next page of the wizard, select the second radio button:  **Select or enter the URL of an existing web page for the client web part content**.</span></span>
    
 
4. <span data-ttu-id="272ac-125">Wählen Sie in der Dropdownliste die URL für die Seite **OrderForm.aspx** aus, und klicken Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="272ac-125">In the drop down list, select the URL for the  **OrderForm.aspx** page, and then press **Finish**.</span></span>
    
    <span data-ttu-id="272ac-126">Eine Datei „elements.xml“, die das Add-In-Webpart definiert, wird dem Projekt hinzugefügt und geöffnet.</span><span class="sxs-lookup"><span data-stu-id="272ac-126">An elements.xml file that defines the add-in part is added to the project and opened.</span></span>
    
 
5. <span data-ttu-id="272ac-127">Ändern Sie im Element **ClientWebPart** die folgenden Attribute auf die angegebenen Werte:</span><span class="sxs-lookup"><span data-stu-id="272ac-127">In the  **ClientWebPart** element, change the following attributes to these values:</span></span>
    

|<span data-ttu-id="272ac-128">**Attribut**</span><span class="sxs-lookup"><span data-stu-id="272ac-128">**Attribute**</span></span>|<span data-ttu-id="272ac-129">**Wert**</span><span class="sxs-lookup"><span data-stu-id="272ac-129">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="272ac-130">Title</span><span class="sxs-lookup"><span data-stu-id="272ac-130">Title</span></span>|<span data-ttu-id="272ac-131">Bestellung absenden</span><span class="sxs-lookup"><span data-stu-id="272ac-131">Place Order</span></span>|
|<span data-ttu-id="272ac-132">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="272ac-132">Description</span></span>|<span data-ttu-id="272ac-133">Formular zum Aufgeben einer Bestellung</span><span class="sxs-lookup"><span data-stu-id="272ac-133">Form to place an order</span></span>|
|<span data-ttu-id="272ac-134">DefaultHeight</span><span class="sxs-lookup"><span data-stu-id="272ac-134">DefaultHeight</span></span>|<span data-ttu-id="272ac-135">320</span><span class="sxs-lookup"><span data-stu-id="272ac-135">320</span></span>|

    Leave all the other attributes with their defaults and save the file.
    
 

## <a name="run-the-add-in-and-test-the-add-in-part"></a><span data-ttu-id="272ac-136">Ausführen des Add-Ins und Testen de Add-In-Websparts</span><span class="sxs-lookup"><span data-stu-id="272ac-136">Run the add-in and test the add-in part</span></span>


 

 

1. <span data-ttu-id="272ac-p106">Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio hostet die Remotewebanwendung in IIS Express und die SQL-Datenbank in SQL Express. Außerdem wird eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durchgeführt, und das Add-In wird sofort ausgeführt. Sie werden aufgefordert, Berechtigungen für das Add-In zu erteilen, bevor die Startseite geöffnet wird.</span><span class="sxs-lookup"><span data-stu-id="272ac-p106">Use the F5 key to deploy and run your add-in. Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in a SQL Express. It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. You are prompted to grant permissions to the add-in before it's start page opens.</span></span>
    
 
2. <span data-ttu-id="272ac-p107">Wenn die Add-In-Startseite geöffnet wird, wurde das Add-In bereitgestellt, und das Add-In-Webpart **Bestellung absenden** steht Benutzern zum Hinzufügen zu einem beliebigen Webpart-Bereich auf einer beliebigen SharePoint-Seite der Hongkong Store-Website zur Verfügung. Führen Sie die folgenden Schritte aus, um es der Startseite hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="272ac-p107">When the add-in's start page opens, the add-in has been deployed and the  **Place Order** add-in part is available to for users to add to any Web Part area on any SharePoint page in the Hong Kong store's website. Follow these steps to add it to the home page.</span></span>
    
      1. <span data-ttu-id="272ac-143">Klicken Sie auf **Zurück zur Website** im Chromsteuerelement am oberen Rand der Seite, um die Startseite des Store in Hongkong zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="272ac-143">Press  **Back to Site** on the chrome control at the top of the start page to open the home page of the Hong Kong store.</span></span>
    
 
  2. <span data-ttu-id="272ac-144">Öffnen Sie auf dem Menüband die Registerkarte **Seite**, und klicken Sie auf die Schaltfläche **Bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="272ac-144">On the ribbon, open the  **Page** tab and press the **Edit** button.</span></span>
    
 
  3. <span data-ttu-id="272ac-p108">Nachdem sich die Seite im Bearbeitungsmodus befindet, öffnen Sie die Registerkarte **Einfügen** auf dem Menüband, und klicken Sie auf die Schaltfläche **Add-In-Webpart**. (Die Schaltfläche heißt möglicherweise immer noch **App-Webpart**.)</span><span class="sxs-lookup"><span data-stu-id="272ac-p108">After the page is in edit mode, open the  **Insert** tab on the ribbon, and the press the **Add-in Part** button. (The button may still be called **App Part**.)</span></span>
    
 
  4. <span data-ttu-id="272ac-p109">Wählen Sie im geöffneten Webpart-Einfügesteuerelement das Add-In-Webpart **Bestellung absenden** aus. Das Steuerelement sieht ähnlich aus wie folgt.</span><span class="sxs-lookup"><span data-stu-id="272ac-p109">On the Web Part insertion control that opens, select the  **Place Order** add-in part. The control will look similar to the following.</span></span>
    
  ![Das Webpart-Einfügesteuerelement in SharePoint. Das Webpart „Bestellung absenden“ ist hervorgehoben. Sein Name und seine Beschreibung werden in einem Feld auf der rechten Seite angezeigt.](../images/aae61f89-2e9e-4808-8b0c-2439dad7c701.PNG)
 

 

 
  5. <span data-ttu-id="272ac-p111">Klicken Sie in eine beliebige Webpartzone im Formular. Damit wird der Standort festgelegt, an dem das Add-In-Webpart eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="272ac-p111">Click somewhere in one of the Web Part zones of the form. This is to set the location where the add-in part will go.</span></span> 
    
 
  6. <span data-ttu-id="272ac-p112">Klicken Sie im Webpart-Einfügesteuerelement auf **Hinzufügen**. Das Add-In-Webpart **Bestellung absenden** wird der Webpartzone hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="272ac-p112">Click  **Add** on the Web Part insertion control. The **Place Order** add-in part will be added to the Web Part zone.</span></span>
    
 
  7. <span data-ttu-id="272ac-156">Klicken Sie auf deim Menüband auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="272ac-156">On the ribbon press  **Save**.</span></span>
    
 
3. <span data-ttu-id="272ac-p113">Das Bestellformular wird nun auf der Seite angezeigt und hat das Aussehen und Verhalten des Rests der Seite übernommen. Es sollte wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="272ac-p113">The order form now appears on the page and it has the look-and-feel of the rest of the page. It should look like the following:</span></span> 
    
  ![Das Add-In-Webpart „Bestellung absenden“ auf der Seite mit Textfeldern von Produkt, Lieferant und Menge. Auch eine Schaltfläche „Bestellung absenden“ ist verfügbar.](../images/beae2e3c-c1f4-4334-8ab8-0c42252cb2a2.PNG)
 

 

 
4. <span data-ttu-id="272ac-p115">Geben Sie Werte für **Lieferant**, **Produkt** und **Menge** ein, und klicken Sie auf **Bestellung absenden**. Es scheint nichts zu passieren, aber es wird eine Bestellung in die Datenbank des Unternehmens eingegeben. Optional können Sie die Felder des Add-In-Webparts leeren, indem Sie die Seite aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="272ac-p115">Enter values for  **Supplier**,  **Product**, and  **Quantity** and press **Place Order**. Nothing will appear to happen, but an order is entered in the corporate database. Optionally, you can empty the fields of the add-in part by refreshing the page.</span></span>
    
 
5. <span data-ttu-id="272ac-p116">Verwenden Sie im Browser die Schaltfläche „Zurück“, bis Sie wieder auf die Startseite für das ChainStore-Add-In zurückgekehrt sind, und klicken Sie dann auf die Schaltfläche **Bestellungen anzeigen**. Ihre neue Bestellung wird jetzt aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="272ac-p116">Use the browser's back button until you are back at the Chain Store add-in's start page; and then press  **Show Orders**. Your new order is listed.</span></span>
    
 
6. <span data-ttu-id="272ac-p117">Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.</span><span class="sxs-lookup"><span data-stu-id="272ac-p117">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
7. <span data-ttu-id="272ac-p118">Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewähr, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.</span><span class="sxs-lookup"><span data-stu-id="272ac-p118">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="272ac-170"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="272ac-170"></span></span>

 <span data-ttu-id="272ac-p119">Das Add-In hängt von zwei Listen ab, die Sie manuell erstellt haben. Sie möchten nicht, dass Ihre Benutzer dies ausführen müssen. Im nächsten Artikel beginnen Sie mit dem Prozess, diese Listen automatisch zu erstellen. Der erste wichtige Schritt ist die Erstellung von benutzerdefinierten Handlern für das Ereignis der Installation eines Add-ins: [Behandeln von Add-In-Ereignissen im vom Anbieter gehosteten Add-In](handle-add-in-events-in-the-provider-hosted-add-in.md)</span><span class="sxs-lookup"><span data-stu-id="272ac-p119">The add-in depends on two lists that you created manually. You don't want your users to have to do that. In the next article you begin the process of automatically creating these lists. The first major step is to create custom handlers for the event of installing an add-in: [Handle add-in events in the provider-hosted add-in](handle-add-in-events-in-the-provider-hosted-add-in.md)</span></span>
 

 

