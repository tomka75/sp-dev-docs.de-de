---
title: "Angeben einer Vorlage für eine Dokumentbibliothek in einem Cloud-Business-Add-In"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: b9505ee15250d4a69a3a79b8d3a4e4893ff5e298
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="provide-a-template-for-a-document-library-in-a-cloud-business-add-in"></a><span data-ttu-id="98483-102">Angeben einer Vorlage für eine Dokumentbibliothek in einem Cloud-Business-Add-In</span><span class="sxs-lookup"><span data-stu-id="98483-102">Provide a template for a document library in a cloud business add-in</span></span>
<span data-ttu-id="98483-p101">Zusätzlich zu den Office-Vorlagen, die beim Hinzufügen eines Dokuments zu einer SharePoint-Dokumentbibliothek verfügbar sind, können Sie auch Ihre eigenen Vorlagen verwenden. Sie haben möglicherweise Ihre eigene Verkaufsangebotsvorlage, die Sie verwenden möchten, wenn neue Aufträge hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="98483-p101">In addition to the Office templates that are available when you add a document to a SharePoint document library, you can provide your own templates. For example, you might have your own sales quote template that you want to use when new orders are added.</span></span>
 

 <span data-ttu-id="98483-p102">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="98483-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## 

<span data-ttu-id="98483-p103">Wenn Sie dies noch nicht getan haben, ordnen Sie Ihrem Cloud-Business-Add-In eine Dokumentbibliothek hinzu. Weitere Informationen finden Sie unter [Zuordnen einer Dokumentbibliothek zu einer Entität](associate-a-document-library-with-an-entity.md).</span><span class="sxs-lookup"><span data-stu-id="98483-p103">If you haven't already done so, associate a document library with your cloud business add-in. See  [Associate a document library with an entity](associate-a-document-library-with-an-entity.md).</span></span>
 

 

### <a name="to-add-a-template"></a><span data-ttu-id="98483-110">So fügen Sie eine Vorlage hinzu</span><span class="sxs-lookup"><span data-stu-id="98483-110">To add a template</span></span>


1. <span data-ttu-id="98483-111">Wechseln Sie zu Ihrer SharePoint-Entwicklerwebsite, und klicken Sie anschließend auf der Seite **Entwickler** auf **Websiteinhalte**.</span><span class="sxs-lookup"><span data-stu-id="98483-111">Go to your SharePoint developer site and on the  **Developer** page, choose **Site Contents**.</span></span>
    
 
2. <span data-ttu-id="98483-112">Klicken Sie auf der Seite **Websiteinhalte** auf **Einstellungen**, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="98483-112">On the  **Site Contents** page, choose **Settings**, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="98483-113">**Abbildung 1. Der Link „Einstellungen“**</span><span class="sxs-lookup"><span data-stu-id="98483-113">**Figure 1. The Settings link**</span></span>

 

  ![Link zu Websiteeinstellungen](../images/CBA_IM_8b.PNG)
 

 

 
3. <span data-ttu-id="98483-115">Klicken Sie auf der Seite **Websiteeinstellungen** in der Liste **Web-Designer-Kataloge** auf **Websiteinhaltstypen**, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="98483-115">On the  **Site Settings** page, in the **Web Designer Galleries** list, choose **Site content types**, as shown in Figure 2.</span></span>
    
    <span data-ttu-id="98483-116">**Abbildung 2. Der Link „Websiteinhaltstypen“**</span><span class="sxs-lookup"><span data-stu-id="98483-116">**Figure 2. The Site content types link**</span></span>

 

  ![Link „Websiteinhaltstypen“](../images/CBA_IM_26.PNG)
 

 

 
4. <span data-ttu-id="98483-118">Klicken Sie auf der Seite **Websiteinhaltstypen** auf **Erstellen**, wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="98483-118">On the  **Site Content Types** page, choose **Create**, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="98483-119">**Abbildung 3. Der Link „Erstellen“**</span><span class="sxs-lookup"><span data-stu-id="98483-119">**Figure 3. The Create link**</span></span>

 

  ![Link „Erstellen“](../images/CBA_IM_27.PNG)
 

 

 
5. <span data-ttu-id="98483-p104">Geben Sie auf der Seite **Neuer Websiteinhaltstyp** einen Namen und eine Beschreibung für Ihre Vorlage ein. Wählen Sie bei **Übergeordneter Inhaltstyp** **Dokumentinhaltstyp** und **Dokument** aus, wie in Abbildung 4 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="98483-p104">On the  **New Site Content Type** page, enter a name and description for your template. For the **Parent Content Type**, choose  **Document Content Types** and **Document**, as shown in Figure 4.</span></span>
    
    <span data-ttu-id="98483-123">**Abbilgung 4. Auswahloptionen für „Übergeordneter Inhaltstyp“**</span><span class="sxs-lookup"><span data-stu-id="98483-123">**Figure 4. Parent content type selections**</span></span>

 

  ![Auswahloptionen für „Übergeordneter Inhaltstyp“](../images/CBA_IM_28.PNG)
 

 

 
6. <span data-ttu-id="98483-125">Klicken Sie im Abschnitt **Gruppe** in der Liste **Vorhandene Gruppe** auf **Dokumentinhaltstypen**, wie in Abbildung 5 dargestellt, und anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="98483-125">In the  **Group** section, in the **Existing group** list, choose **Document Content Types** as shown in Figure 5, and then choose **OK**.</span></span>
    
    <span data-ttu-id="98483-126">**Abbildung 5. Gruppeneinstellung**</span><span class="sxs-lookup"><span data-stu-id="98483-126">**Figure 5. Group setting**</span></span>

 

  ![Gruppeneinstellung](../images/CBA_IM_28a.PNG)
 

 

 
7. <span data-ttu-id="98483-128">Klicken Sie auf der Seite **Websiteinhaltstyp** auf **Erweiterte Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="98483-128">On the  **Site Content Type** page, choose **Advanced settings**.</span></span>
    
 
8. <span data-ttu-id="98483-129">Geben Sie auf der Seite **Erweiterte Einstellungen** entweder die URL einer vorhandenen Dokumentvorlage ein oder laden Sie eine neue Dokumentvorlage hoch, wie in Abbildung 6 dargestellt, und klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="98483-129">On the  **Advanced Settings** page, either enter the URL of an existing document template or upload a new document template as shown in Figure 6, and then choose **OK**.</span></span>
    
    <span data-ttu-id="98483-130">**Abbildung 6. Angeben der Dokumentvorlage**</span><span class="sxs-lookup"><span data-stu-id="98483-130">**Figure 6. Specify the document template**</span></span>

 

  ![Angeben der Dokumentvorlage](../images/CBA_IM_29.PNG)
 

 

 
9. <span data-ttu-id="98483-132">Wechseln Sie zur Seite **Websiteinhalte**, klicken Sie auf Ihre Dokumentbibliothek, und wechseln Sie dann auf die Seite **Einstellungen**.</span><span class="sxs-lookup"><span data-stu-id="98483-132">Go to the  **Site Contents** page and choose your document library, and then go to the **Settings** page.</span></span>
    
 
10. <span data-ttu-id="98483-133">Klicken Sie auf der Seite **Einstellungen** auf **Aus vorhandenen Websiteinhaltstypen hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="98483-133">On the  **Settings** page, choose **Add from existing site content types**.</span></span>
    
 
11. <span data-ttu-id="98483-134">Fügen Sie Ihre Vorlage auf der Seite **Inhaltstypen hinzufügen** wie in Abbildung 7 dargestellt hinzu, und klicken Sie anschließend auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="98483-134">On the  **Add Content Types** page, add your template as shown in Figure 7, and then choose **OK**.</span></span>
    
    <span data-ttu-id="98483-135">**Abbildung 7. Hinzufügen der Vorlage**</span><span class="sxs-lookup"><span data-stu-id="98483-135">**Figure 7. Adding the template**</span></span>

 

  ![Hinzufügen der Vorlage](../images/CBA_IM_29a.PNG)
 

 

 
12. <span data-ttu-id="98483-p105">Führen Sie Ihr Add-In aus, und fügen Sie ein Dokument hinzu. Ihre Vorlage sollte im Dialogfeld **Neue Datei erstellen** angezeigt werden, wie in Abbildung 8 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="98483-p105">Run your add-in and add a document. You should see your template in the  **Create a new file** dialog box, as shown in Figure 8.</span></span>
    
    <span data-ttu-id="98483-139">**Abbildung 8. Das Dialogfeld „Neue Datei erstellen“ mit der neuen Vorlage**</span><span class="sxs-lookup"><span data-stu-id="98483-139">**Figure 8. The Create a new file dialog box with the new template**</span></span>

 

  ![Das Dialogfeld „Neue Datei erstellen“ mit der neuen Vorlage](../images/CBA_IM_30.PNG)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="98483-141">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="98483-141">Additional resources</span></span>
<span data-ttu-id="98483-142"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="98483-142"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="98483-143">Entwickeln von Cloud-Business-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="98483-143">Develop cloud business add-ins</span></span>](develop-cloud-business-add-ins.md)
    
 
-  [<span data-ttu-id="98483-144">Zuordnen einer Dokumentbibliothek zu einer Entität</span><span class="sxs-lookup"><span data-stu-id="98483-144">Associate a document library with an entity</span></span>](associate-a-document-library-with-an-entity.md)
    
 
