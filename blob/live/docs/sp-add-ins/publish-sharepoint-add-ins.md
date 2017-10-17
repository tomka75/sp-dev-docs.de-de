---
title: "Veröffentlichen von SharePoint-Add-Ins"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 760c56cd4fcca1e998fd908a7c0dda44baddd228
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="publish-sharepoint-add-ins"></a><span data-ttu-id="dba86-102">Veröffentlichen von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="dba86-102">Publish SharePoint Add-ins</span></span>
<span data-ttu-id="dba86-103">In diesem Thema geht es um Artikel und Ressourcen, die Ihnen bei der Veröffentlichung Ihrer SharePoint-Add-Ins helfen.</span><span class="sxs-lookup"><span data-stu-id="dba86-103">Find articles and resources to help you publish your SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="dba86-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="dba86-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="get-started-with-publishing-your-add-ins"></a><span data-ttu-id="dba86-107">Erste Schritte beim Veröffentlichen Ihrer Add-Ins</span><span class="sxs-lookup"><span data-stu-id="dba86-107">Get started with publishing your add-ins</span></span>
<span data-ttu-id="dba86-108"><a name="bk_gettingstarted"> </a></span><span class="sxs-lookup"><span data-stu-id="dba86-108"></span></span>

<span data-ttu-id="dba86-p102">Nachdem Sie Ihr SharePoint-Add-In fertig gestellt haben, besteht der letzte Schritt darin, das Add-In Ihren Benutzern verfügbar zu machen. Zu diesem Zweck können Sie das Add-In an zwei verschiedenen Orten veröffentlichen:</span><span class="sxs-lookup"><span data-stu-id="dba86-p102">You've finished developing your SharePoint Add-in—the final step is making that add-in available to your users. You can do this by publishing the add-in to one of two places:</span></span>
 

 

-  <span data-ttu-id="dba86-p103">**Im öffentlichen Office Store.** Wenn Sie Ihr Add-In im Office Store öffentlich anbieten, steht es allen Benutzern von SharePoint-Bereitstellungen zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="dba86-p103">**The public Office Store.** Publish your add-in to the Office Store to make the add-in publically available, so that it can be acquired by users of any SharePoint deployment.</span></span>
    
 
-  <span data-ttu-id="dba86-p104">**Im internen Add-In-Katalog einer Organisation.** Wenn Sie Ihre Add-Ins im internen Add-In-Katalog einer Organisation veröffentlichen, der in Ihrer SharePoint-Bereitstellung gehostet wird, machen Sie sie für Benutzer verfügbar, die auf diese SharePoint-Bereitstellung zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="dba86-p104">**An internal organization add-in catalog.** Publish your add-ins to an internal organization add-in catalog, hosted on your SharePoint deployment, to make them available to users with access to that SharePoint deployment.</span></span>
    
 
<span data-ttu-id="dba86-115">Informationen darüber, wie Sie Ihr Add-In zur Veröffentlichung mit Visual Studio 2012 verpacken, finden Sie unter [Veröffentlichen von SharePoint-Add-Ins mithilfe von Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="dba86-115">For information about how to package your add-in for publication by using Visual Studio 2012, see  [Publish SharePoint Add-ins by using Visual Studio](publish-sharepoint-add-ins-by-using-visual-studio.md).</span></span>
 

 

### <a name="publishing-to-the-office-store"></a><span data-ttu-id="dba86-116">Veröffentlichen im Office Store</span><span class="sxs-lookup"><span data-stu-id="dba86-116">Publishing to the Office Store</span></span>

<span data-ttu-id="dba86-117">Zu Veröffentlichen eines Add-Ins im Office Store müssen Sie sich zunächst [als Microsoft-Entwickler registrieren](https://sellerdashboard.microsoft.com/Registration).</span><span class="sxs-lookup"><span data-stu-id="dba86-117">To publish an add-in to the Office Store, you must first  [register as a Microsoft developer](https://sellerdashboard.microsoft.com/Registration).</span></span> 
 

 
<span data-ttu-id="dba86-p105">Wenn Sie ein Add-In zur Veröffentlichung in den Office Store hochladen, führt Microsoft eine Reihe von Überprüfungen durch, um sicherzustellen, dass Ihr Add-In den Add-In-Inhalts- und -verhaltensrichtlinien entspricht. Beispielsweise wird geprüft, ob das Add-In-Manifestmarkup gültig und vollständig ist, und sichergestellt, dass im Add-In enthaltene SharePoint-Lösungspakete (WSP-Dateien) keine unzulässigen Elemente oder SharePoint-Features mit einem Geltungsbereich enthalten, der über "Web" hinausgeht. Das Paket wird zudem auf unzulässigen Inhalt geprüft. Wenn das Add-In alle Tests besteht, wird es in eine Datei verpackt und von Microsoft signiert.</span><span class="sxs-lookup"><span data-stu-id="dba86-p105">When you upload an add-in to the Office Store for publication, Microsoft performs a series of verification checks to ensure your add-in adheres to the add-in content and behavior guidelines. For example, it checks whether the add-in manifest markup is valid and complete and verifies that any SharePoint solution packages (.wsp files) that are included in the add-in do not contain elements that aren't allowed, or SharePoint Features with a scope that is broader than Web. The package is also inspected for objectionable content. If the add-in package passes all tests, it's wrapped into a file and signed by Microsoft.</span></span>
 

 
<span data-ttu-id="dba86-p106">Wenn Sie Ihr Add-In zur Veröffentlichung in den Office Store hochladen, können Sie Lizenzbedingungen für Benutzer anbieten, die das Add-In herunterladen. Die Add-In-Lizenz definiert:</span><span class="sxs-lookup"><span data-stu-id="dba86-p106">When you upload your add-in for publication on the Office Store, you can choose the terms of the license you want to offer users when they download it. Use this add-in license to decide:</span></span> 
 

 

- <span data-ttu-id="dba86-124">ob Sie Ihr Add-In kostenlos, als Testversion oder zum Kauf anbieten;</span><span class="sxs-lookup"><span data-stu-id="dba86-124">Whether you are offering your add-in for free, trial, or for purchase.</span></span>
    
 
- <span data-ttu-id="dba86-125">ob Ihr Add-In auf Pro-Benutzer- oder Websitebasis erworben werden kann.</span><span class="sxs-lookup"><span data-stu-id="dba86-125">Whether your add-in can be acquired on a per-user or site basis.</span></span>
    
 
<span data-ttu-id="dba86-p107">SharePoint erzwingt keine Lizenzbedingungen für die Add-In-Verwendung, sondern bietet ein Lizenzierungsframework, das es Ihnen ermöglicht, Codelogik in Ihr Add-In einzubinden und die von Ihnen gewünschten Lizenzierungsbeschränkungen durchzusetzen. Beispielsweise können Sie Codelogik in Ihr Add-In aufnehmen, die Benutzern Zugriff auf bestimmte Add-In-Features gewährt, sofern sie über eine kostenpflichtige Lizenz und nicht nur eine Testlizenz verfügen. Weitere Informationen finden Sie unter  [Lizenzieren von Office- und SharePoint-Add-Ins](http://msdn.microsoft.com/library/license-your-office-and-sharepoint-add-ins%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="dba86-p107">SharePoint does not enforce license terms for add-in usage—it provides a licensing framework that lets you include code logic in your add-in to enforce whatever licensing restrictions you choose. For example, you can include code logic in your add-in that enables users to access certain add-in features if they have a paid license, but not if they have a trial license. For more information, see  [License your Office and SharePoint Add-ins](http://msdn.microsoft.com/library/license-your-office-and-sharepoint-add-ins%28Office.15%29.aspx).</span></span>
 

 

### <a name="publishing-to-an-add-in-catalog"></a><span data-ttu-id="dba86-129">Veröffentlichen in einem Add-In-Katalog</span><span class="sxs-lookup"><span data-stu-id="dba86-129">Publishing to an add-in catalog</span></span>

<span data-ttu-id="dba86-p108">Wenn Sie SharePoint-Add-Ins für die Verwendung durch Ihr eigenes Unternehmen oder einen spezifischen Unternehmensclient und nicht die Allgemeinheit erstellen, möchten Sie Ihr Add-In wahrscheinlich in einem von SharePoint gehosteten internen Add-In-Katalog veröffentlichen. Ein privater Add-In-Katalog ist eine dedizierte Websitesammlung in einer SharePoint-Webanwendung (oder einer SharePoint Online-Instanz), die als Host für Dokumentbibliotheken für SharePoint-Add-Ins und Office-Add-Ins dient. Wenn der Katalog in eine eigene Websitesammlung eingefügt wird, ist es für den Webanwendungsadministrator oder Mandantenadministrator einfacher, Zugriffsberechtigungen für den Katalog zu begrenzen.</span><span class="sxs-lookup"><span data-stu-id="dba86-p108">If you're creating SharePoint Add-ins for your own company's use or a specific corporate client, instead of the general public, you'll likely want to publish your add-in to an internal add-in catalog hosted on SharePoint. A private add-in catalog is a dedicated site collection in a SharePoint web application (or a SharePoint Online tenancy) that hosts document libraries for SharePoint Add-ins and Office Add-ins. Putting the catalog into its own site collection makes it easier for the web application administrator or tenant administrator to limit permissions to the catalog.</span></span>
 

 
<span data-ttu-id="dba86-p109">Das Hochladen eines SharePoint-Add-In in einen unternehmenseigenen Add-In-Katalog ist genauso einfach wie das Hochladen irgendeiner Datei in eine SharePoint-Dokumentbibliothek. Sie brauchen nur die lokale URL des Add-In-Pakets und ein paar andere Informationen, wie den Namen des Add-Ins, in ein Popupformular einzugeben. Wenn Sie das Add-In in einen Add-In-Katalog hochladen, werden ähnliche Kontrollen durchgeführt, und Add-Ins, die die Prüfung nicht bestanden haben, werden im Katalog als ungültig markiert oder deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="dba86-p109">Uploading a SharePoint Add-in to a corporate add-in catalog is as easy as uploading any file to a SharePoint document library. You fill out a pop-up form in which you supply the local URL of the add-in package and other information, such as the name of the add-in. When you upload the add-in to an add-in catalog, there are similar checks and add-ins that do not pass are marked as invalid or disabled in the catalog.</span></span>
 

 

## <a name="deciding-where-to-publish-your-sharepoint-add-in"></a><span data-ttu-id="dba86-135">Entscheiden, wo Ihr SharePoint-Add-In veröffentlicht werden soll</span><span class="sxs-lookup"><span data-stu-id="dba86-135">Deciding where to publish your SharePoint Add-in</span></span>
<span data-ttu-id="dba86-136"><a name="bk_decide"> </a></span><span class="sxs-lookup"><span data-stu-id="dba86-136"></span></span>

<span data-ttu-id="dba86-p110">In der folgenden Tabelle wird die Veröffentlichung im Office Store mit der Veröffentlichung in einem Add-In-Katalog verglichen. Zudem wird auf kritische Punkte hingewiesen, die bei der Entscheidung, wo ein Add-In veröffentlicht werden soll, zu berücksichtigen sind. Wir empfehlen, die Veröffentlichung des Add-Ins bereits vor dem Entwurf und der Entwicklung zu planen, da sich der Ort der Veröffentlichung in manchen Fällen auf den Entwurf und die Entwicklung des Add-Ins auswirkt.</span><span class="sxs-lookup"><span data-stu-id="dba86-p110">The following table offers a comparison of publishing to the Office Store or to an add-in catalog, and lists issues to consider when deciding where to publish your add-in. We recommend you decide where you plan to publish your add-in before you design and develop it; in some cases, such as licensing, where you publish your add-in will affect the design and development of your add-in.</span></span>
 

 

<span data-ttu-id="dba86-139">**Tabelle 1: Überlegungen zum Ort der Veröffentlichung eines Add-Ins**</span><span class="sxs-lookup"><span data-stu-id="dba86-139">**Table 1. Considerations for where to publish your add-in**</span></span>


|<span data-ttu-id="dba86-140">**Office Store**</span><span class="sxs-lookup"><span data-stu-id="dba86-140">**Office Store**</span></span>|<span data-ttu-id="dba86-141">**Add-In-Katalog**</span><span class="sxs-lookup"><span data-stu-id="dba86-141">**Add-in Catalog**</span></span>|
|:-----|:-----|
|<span data-ttu-id="dba86-142">Das Add-In ist öffentlich zugänglich.</span><span class="sxs-lookup"><span data-stu-id="dba86-142">Add-in is publically available.</span></span>|<span data-ttu-id="dba86-143">Das Add-In steht Benutzern zur Verfügung, die auf diese SharePoint-Bereitstellung zugreifen können.</span><span class="sxs-lookup"><span data-stu-id="dba86-143">Add-in is available to users with access to this SharePoint deployment</span></span>|
|<span data-ttu-id="dba86-144">Ein Lizenzierungsframework ist verfügbar.</span><span class="sxs-lookup"><span data-stu-id="dba86-144">Licensing framework available.</span></span>|<span data-ttu-id="dba86-145">Es steht kein Lizenzierungsframework zur Nutzung zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="dba86-145">Licensing framework is not available for use.</span></span>|
|<span data-ttu-id="dba86-146">Das Add-In-Paket wird von Microsoft auf die Einhaltung technischer und Inhaltsrichtlinien geprüft.</span><span class="sxs-lookup"><span data-stu-id="dba86-146">Add-in package verified by Microsoft for technical and content adherence to policies.</span></span>|<span data-ttu-id="dba86-147">Die Überprüfung des Add-In-Pakets wird beim Hochladen von SharePoint durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="dba86-147">Add-in package verification performed by SharePoint when add-in is uploaded.</span></span>|
|<span data-ttu-id="dba86-148">Sie müssen beim Microsoft Seller Dashboard angemeldet sein, um Add-Ins hochladen zu können.</span><span class="sxs-lookup"><span data-stu-id="dba86-148">You must be signed up with Microsoft Seller Dashboard to upload add-ins.</span></span>|<span data-ttu-id="dba86-149">Es ist keine Registrierung bei Microsoft erforderlich.</span><span class="sxs-lookup"><span data-stu-id="dba86-149">No registration with Microsoft required.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="dba86-150">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="dba86-150">Additional resources</span></span>
<span data-ttu-id="dba86-151"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="dba86-151"></span></span>


-  [<span data-ttu-id="dba86-152">Erstellen oder Aktualisieren von Client-IDs und geheimen Clientschlüsseln im Verkäuferdashboard</span><span class="sxs-lookup"><span data-stu-id="dba86-152">Create or update client IDs and secrets in the Seller Dashboard</span></span>](http://msdn.microsoft.com/library/create-or-update-client-ids-and-secrets-in-the-seller-dashboard%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="dba86-153">Verwenden des Verkäuferdashboards zum Übermitteln von Office- und SharePoint-Add-Ins und Office 365-Apps an den Office Store</span><span class="sxs-lookup"><span data-stu-id="dba86-153">Use the Seller Dashboard to submit Office and SharePoint Add-ins and Office 365 apps to the Office Store</span></span>](http://msdn.microsoft.com/library/use-the-seller-dashboard-to-submit-office-and-sharepoint-add-ins-and-office-365-apps-to-the-office-store%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="dba86-154">Validierungsrichtlinien für an den Office Store übermittelte Apps und Add-Ins (Version 2.1)</span><span class="sxs-lookup"><span data-stu-id="dba86-154">Validation policies for apps and add-ins submitted to the Office Store (version 2.1)</span></span>](http://msdn.microsoft.com/library/validation-policies-for-apps-and-add-ins-submitted-to-the-office-store-version-2-1%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="dba86-155">Office-Entwicklung</span><span class="sxs-lookup"><span data-stu-id="dba86-155">Start building Office and SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx)
    
 
-  [<span data-ttu-id="dba86-156">Lizenzieren von Office- und SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="dba86-156">License your Office and SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/license-your-office-and-sharepoint-add-ins%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="dba86-157">Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen</span><span class="sxs-lookup"><span data-stu-id="dba86-157">Deploying and installing SharePoint Add-ins: methods and options</span></span>](deploying-and-installing-sharepoint-add-ins-methods-and-options.md)
    
 
-  [<span data-ttu-id="dba86-158">Mandantschaften und Bereitstellungsbereiche von SharePoint- Add-Ins</span><span class="sxs-lookup"><span data-stu-id="dba86-158">Tenancies and deployment scopes for SharePoint Add-ins</span></span>](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="dba86-159">Veröffentlichen von SharePoint-Add-Ins mithilfe von Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dba86-159">Publish SharePoint Add-ins by using Visual Studio</span></span>](publish-sharepoint-add-ins-by-using-visual-studio.md)
    
 
-  [<span data-ttu-id="dba86-160">Veröffentlichen von Add-Ins für den Office Store</span><span class="sxs-lookup"><span data-stu-id="dba86-160">Publishing Office Add-ins Store</span></span>](http://social.msdn.microsoft.com/Forums/en-US/officestore)
    
 

