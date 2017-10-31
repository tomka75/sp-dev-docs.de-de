---
title: Problembehandlung bei Dokumentbibliotheken
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 1629b514a8fa4a84d7d916214d89501f24d6a25b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="troubleshooting-document-libraries"></a><span data-ttu-id="6c5af-102">Problembehandlung bei Dokumentbibliotheken</span><span class="sxs-lookup"><span data-stu-id="6c5af-102">Troubleshooting document libraries</span></span>
<span data-ttu-id="6c5af-103">In diesem Thema erfahren Sie von Problemen, die auftreten können, wenn Sie von einem Cloud-Geschäfts-Add-In auf eine SharePoint-Dokumentbibliothek zugreifen, und mit welchen Techniken Sie diese Probleme beheben können.</span><span class="sxs-lookup"><span data-stu-id="6c5af-103">In this topic, you can learn about problems that may occur when you access a SharePoint document library from a cloud business add-in and the techniques that you can use to resolve those problems.</span></span>
 

 <span data-ttu-id="6c5af-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="6c5af-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 

## <a name="error-this-add-in-does-not-support-uploading-documents-from-your-current-browser"></a><span data-ttu-id="6c5af-107">Fehler: Dieses Add-Un unterstützt das Hochladen von Dokumenten in diesem Browser nicht.</span><span class="sxs-lookup"><span data-stu-id="6c5af-107">Error: This add-in does not support uploading documents from your current browser</span></span>

<span data-ttu-id="6c5af-p102">Wenn Sie ein Dokument in eine verbundene Dokumentbibliothek in einem Cloud-Geschäfts-Add-In hochladen wollen, scheitert der Versuch mit folgender Fehlermeldung: "Dieses Add-In unterstützt nicht das Hochladen von Dokumenten aus dem aktuellen Browser. Verwenden Sie die neueste Version." Dieses Problem tritt nur bei einigen älteren Browsern auf, die die HTML5 FileReader-API nicht unterstützen. Fügen Sie das NuGet-Paket zu Ihrem Projekt hinzu, und stellen Sie das Add-In erneut bereit, um das Problem zu beheben.</span><span class="sxs-lookup"><span data-stu-id="6c5af-p102">When attempting to upload a document to an associated document library in a cloud business add-in, the upload fails with the error message "This add-in does not support uploading documents from your current browser. Please use the latest version". This issue only occurs on certain older browsers that don't support the HTML5 FileReader API. It can be fixed by adding a NuGet package to your project and redeploying the add-in.</span></span>
 

 

### <a name="to-prevent-the-error"></a><span data-ttu-id="6c5af-112">So verhindern Sie den Fehler</span><span class="sxs-lookup"><span data-stu-id="6c5af-112">To prevent the error</span></span>


1. <span data-ttu-id="6c5af-113">Öffnen Sie im **Projektmappen-Explorer** das Kontextmenü für das Projekt **Server**, und wählen Sie **NuGet-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="6c5af-113">In  **Solution Explorer**, open the shortcut menu for the  **Server** project and choose **Manage NuGet Packages**.</span></span>
    
 
2. <span data-ttu-id="6c5af-114">Erweitern Sie im Dialogfeld **NuGet-Pakete verwalten** den Knoten **Online**, und geben Sie dann im Feld **Online suchen** Webseiten ein, wie in Abbildung 1 gezeigt.</span><span class="sxs-lookup"><span data-stu-id="6c5af-114">In the  **Manage NuGet Packages** dialog box, expand the **Online** node, and then in the **Search Online** box enter web pages, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="6c5af-115">**Abbildung 1. Auswahloptionen im Dialogfeld „NuGet-Pakete verwalten“**</span><span class="sxs-lookup"><span data-stu-id="6c5af-115">**Figure 1. Selections in the Manage NuGet Packages dialog box**</span></span>

 

  ![Auswahloptionen im Dialogfeld „NuGet-Pakete verwalten“](../images/NuGet.PNG)
 

 

 
3. <span data-ttu-id="6c5af-117">Wählen Sie in der Ergebnisliste den Eintrag **Microsoft ASP.NET-Webseiten**, und klicken Sie dann auf **Installieren**.</span><span class="sxs-lookup"><span data-stu-id="6c5af-117">In the list of results, choose  **Microsoft ASP.NET Web Pages**, and then choose the  **Install** button.</span></span>
    
    <span data-ttu-id="6c5af-118">Das Dialogfeld **Zustimmung zur Lizenz** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="6c5af-118">The  **License Acceptance** dialog box opens.</span></span>
    
 
4. <span data-ttu-id="6c5af-119">Lesen Sie im Dialogfeld **Zustimmung zur Lizenz** die Lizenzbedingungen. Klicken Sie auf **Annehmen**, wenn Sie den Bedingungen zustimmen.</span><span class="sxs-lookup"><span data-stu-id="6c5af-119">In the  **License Acceptance** dialog box, review the license terms, and if you agree to the terms choose the **I Accept** button.</span></span>
    
 
5. <span data-ttu-id="6c5af-120">Wenn das Paket fertig installiert ist, klicken Sie auf **Schließen**.</span><span class="sxs-lookup"><span data-stu-id="6c5af-120">When the package finishes installing, choose the  **Close** button.</span></span>
    
 
6. <span data-ttu-id="6c5af-121">Veröffentlichen Sie das aktualisierte Add-In auf Ihrer SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="6c5af-121">Publish the updated add-in to your SharePoint site.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="6c5af-122">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6c5af-122">Additional resources</span></span>
<span data-ttu-id="6c5af-123"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6c5af-123"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="6c5af-124">Zuordnen einer Dokumentbibliothek zu einer Entität</span><span class="sxs-lookup"><span data-stu-id="6c5af-124">Associate a document library with an entity</span></span>](associate-a-document-library-with-an-entity.md)
    
 

