---
title: Ersetzen von Listendefinitionen erstellte SharePoint-Listen
ms.date: 11/03/2017
ms.openlocfilehash: 99caef124d7b5162839dff092d7760f7ec9dbdf3
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="replace-sharepoint-lists-created-from-list-definitions"></a><span data-ttu-id="2b484-102">Ersetzen von Listendefinitionen erstellte SharePoint-Listen</span><span class="sxs-lookup"><span data-stu-id="2b484-102">Replace SharePoint lists created from list definitions</span></span>
<span data-ttu-id="2b484-103">Ersetzen Sie Listen und Bibliotheken, die mithilfe von Listendefinitionen in SharePoint erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="2b484-103">Replace lists and libraries that were created by using list definitions in SharePoint.</span></span> 

<span data-ttu-id="2b484-104">_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="2b484-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="2b484-105">Wenn Sie Listendefinitionen verwendet, um Listen in Ihrer farmlösung zu erstellen, erfahren Sie, wie sie in neue Lösungen umgewandelt, die ähnliche Funktionalität mithilfe des Clientobjektmodells (CSOM) zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="2b484-105">If you used list definitions to create lists in your farm solution, learn how to transform them into new solutions that provide similar functionality using the client object model (CSOM).</span></span> <span data-ttu-id="2b484-106">In diesem Artikel wird beschrieben, wie das Clientobjektmodell (CSOM) zu verwenden:</span><span class="sxs-lookup"><span data-stu-id="2b484-106">This article describes how to use the client object model (CSOM) to:</span></span>

- <span data-ttu-id="2b484-107">Hier finden Sie Listen und Bibliotheken, die mithilfe von Listendefinitionen erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="2b484-107">Find lists and libraries that were created by using list definitions.</span></span>
    
- <span data-ttu-id="2b484-108">Erstellen und Konfigurieren von neuen Listen.</span><span class="sxs-lookup"><span data-stu-id="2b484-108">Create and configure new lists.</span></span>
    
- <span data-ttu-id="2b484-109">Hinzufügen und Entfernen von Ansichten von Listen.</span><span class="sxs-lookup"><span data-stu-id="2b484-109">Add and remove views from lists.</span></span>
    
- <span data-ttu-id="2b484-110">Migrieren von Inhalten aus der ursprünglichen Liste in die neue Liste.</span><span class="sxs-lookup"><span data-stu-id="2b484-110">Migrate content from the original list to the new list.</span></span>

<span data-ttu-id="2b484-111">**Wichtig**</span><span class="sxs-lookup"><span data-stu-id="2b484-111">**Important**</span></span> <p><span data-ttu-id="2b484-112">Farmlösungen können nicht mit SharePoint Online migriert werden.</span><span class="sxs-lookup"><span data-stu-id="2b484-112">Farm solutions cannot be migrated to SharePoint Online.</span></span> <span data-ttu-id="2b484-113">Durch die Techniken und den Code in diesem Artikel beschriebenen anwenden, können Sie einer neuen Lösung mit ähnlicher Funktionalität erstellen, dass Ihre farmlösungen zu ermöglichen, können in SharePoint Online bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="2b484-113">By applying the techniques and code described in this article, you can build a new solution with similar functionality that your farm solutions provide, which can then be deployed to SharePoint Online.</span></span> <span data-ttu-id="2b484-114">Wenn Sie einen direkte Transformation Ansatz verwenden, müssen Sie die neue Lösung in SharePoint Online bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="2b484-114">If you are using an in-place transformation approach, you may need to deploy the new solution to SharePoint Online.</span></span> <span data-ttu-id="2b484-115">Wenn Sie den Einsatz oder der Inhaltsmigration Ansatz verwenden, können die Tools von Drittanbietern die Listen für Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="2b484-115">If you are using the Swing or content migration approach, the third-party tools may create the lists for you.</span></span> <span data-ttu-id="2b484-116">Weitere Informationen finden Sie unter [Transformation Ansätze für Ihr neues SharePoint-Add-in bereitstellen](https://msdn.microsoft.com/library/dn986827.aspx#sectionSection1).</span><span class="sxs-lookup"><span data-stu-id="2b484-116">For more information, see [Transformation approaches to deploy your new SharePoint Add-in](https://msdn.microsoft.com/library/dn986827.aspx#sectionSection1).</span></span> <span data-ttu-id="2b484-117">Der Code in diesem Artikel erfordert zusätzlichen Code, um eine voll funktionsfähige Lösung bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="2b484-117">The code in this article requires additional code to provide a fully working solution.</span></span> <span data-ttu-id="2b484-118">In diesem Artikel erläutern beispielsweise nicht Anleitung zu Office 365, authentifizieren Implementierung Ausnahmebehandlung erforderlich, und so weiter.</span><span class="sxs-lookup"><span data-stu-id="2b484-118">For example, this article does not discuss how to authenticate to Office 365, how to implement required exception handling, and so on.</span></span> <span data-ttu-id="2b484-119">Zusätzliche Codebeispiele finden Sie unter [Office 365 Developer Mustern und Methoden Projekt](https://github.com/SharePoint/PnP).</span><span class="sxs-lookup"><span data-stu-id="2b484-119">For additional code samples, see the [Office 365 Developer Patterns and Practices project](https://github.com/SharePoint/PnP).</span></span></p><p><span data-ttu-id="2b484-120">Verwenden Sie die beschriebenen Verfahren in diesem Artikel nur ein paar Listen zu einem Zeitpunkt zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="2b484-120">Use the techniques described in this article to update only a few lists at a time.</span></span> <span data-ttu-id="2b484-121">Bei der Suche nach Listen zu aktualisieren, wird, sollte die Listen vom Listentyp nicht gefiltert werden.</span><span class="sxs-lookup"><span data-stu-id="2b484-121">Also, when finding lists to update, you should not filter the lists by list type.</span></span></p>

## <a name="before-you-begin"></a><span data-ttu-id="2b484-122">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="2b484-122">Before you begin</span></span>

<span data-ttu-id="2b484-123">Idealerweise sollten Sie überprüfen Ihrer vorhandenen farmlösungen, erfahren Sie mehr über die in diesem Artikel beschriebenen Verfahren und klicken Sie dann planen, wie diese Techniken beziehen sich auf die vorhandene Farm Solutions.</span><span class="sxs-lookup"><span data-stu-id="2b484-123">Ideally, you should review your existing farm solutions, learn about the techniques described in this article, and then plan how to apply these techniques to your existing farm solutions.</span></span> <span data-ttu-id="2b484-124">Wenn Sie mit farmlösungen vertraut sind, oder nicht über eine vorhandene farmlösung verfügen entwickelt, kann es für Sie hilfreich sein:</span><span class="sxs-lookup"><span data-stu-id="2b484-124">If you are unfamiliar with farm solutions or do not have an existing farm solution to work with, it might be helpful for you to:</span></span>

1. <span data-ttu-id="2b484-125">Laden Sie die [Projektmappe Contoso.Intranet](https://github.com/SharePoint/PnP/tree/master/Reference%20Material/Contoso.Intranet).</span><span class="sxs-lookup"><span data-stu-id="2b484-125">Download the [Contoso.Intranet solution](https://github.com/SharePoint/PnP/tree/master/Reference%20Material/Contoso.Intranet).</span></span> <span data-ttu-id="2b484-126">[Überprüfen der Anfangszustand der Website und Bibliothek für den Austausch](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/10-2%20Replacing%20Lists%20Created%20from%20Custom%20Templates/Lab.md#examine-the-initial-state-of-the-site-and-library-for-replacement) zum Abrufen von Listen erstellt wurden mit deklarativ Listendefinitionen einer schnellen Übersicht lesen.</span><span class="sxs-lookup"><span data-stu-id="2b484-126">Review [Examine the initial state of the site and library for replacement](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/10-2%20Replacing%20Lists%20Created%20from%20Custom%20Templates/Lab.md#examine-the-initial-state-of-the-site-and-library-for-replacement) to get a quick understanding of how lists were created declaratively using list definitions.</span></span>
    
    <span data-ttu-id="2b484-127">**Hinweis:**  In Contoso.Intranet, in der Datei elements.xml für SP\ListTemplate\LTContosoLibrary ist die ID für die benutzerdefinierte Listenvorlage 10003.</span><span class="sxs-lookup"><span data-stu-id="2b484-127">**Note:**  In Contoso.Intranet, in the elements.xml file for SP\ListTemplate\LTContosoLibrary, the ID for the custom list template is 10003.</span></span> <span data-ttu-id="2b484-128">Sie verwenden diese zum Identifizieren der Vorlage, die zum Erstellen der Liste verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="2b484-128">You will use this to identify the template that was used to create the list.</span></span> <span data-ttu-id="2b484-129">Überprüfen Sie auch die Konfigurationseinstellungen und Ansichten, die in Ihrer Liste definiert sind.</span><span class="sxs-lookup"><span data-stu-id="2b484-129">Also review the configuration settings and views that are defined on your list.</span></span>

2. <span data-ttu-id="2b484-130">Informationen Sie zu farmlösungen.</span><span class="sxs-lookup"><span data-stu-id="2b484-130">Learn about farm solutions.</span></span> <span data-ttu-id="2b484-131">Weitere Informationen finden Sie unter [Übersicht über SharePoint 2010-Architekturen](https://msdn.microsoft.com/en-us/library/office/gg552610%28v=office.14%29.aspx) und [Farmlösungen in SharePoint 2013](https://msdn.microsoft.com/library/jj163902.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b484-131">For more information, see [SharePoint 2010 Architectures Overview](https://msdn.microsoft.com/en-us/library/office/gg552610%28v=office.14%29.aspx) and [Build farm solutions in SharePoint 2013](https://msdn.microsoft.com/library/jj163902.aspx).</span></span>
    
## <a name="replace-lists-created-from-list-definitions"></a><span data-ttu-id="2b484-132">Ersetzen von Listendefinitionen erstellte Listen</span><span class="sxs-lookup"><span data-stu-id="2b484-132">Replace lists created from list definitions</span></span>

<span data-ttu-id="2b484-133">So ersetzen Sie Listen von Listendefinitionen erstellt:</span><span class="sxs-lookup"><span data-stu-id="2b484-133">To replace lists created from list definitions:</span></span>

1. <span data-ttu-id="2b484-134">Hier finden Sie Listen, die mit einer bestimmten Basis Vorlage erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="2b484-134">Find lists that were created using a specific base template.</span></span>
    
2. <span data-ttu-id="2b484-135">Erstellen Sie die neue Liste mit der Out-of-Box Listendefinition.</span><span class="sxs-lookup"><span data-stu-id="2b484-135">Create the new list using the out-of-the-box list definition.</span></span> 
    
3. <span data-ttu-id="2b484-136">Konfigurieren von Einstellungen für die Liste.</span><span class="sxs-lookup"><span data-stu-id="2b484-136">Configure list settings.</span></span>
    
4. <span data-ttu-id="2b484-137">Festlegen von Inhaltstypen für die neue Liste basierend auf den Inhaltstypen, die für die ursprüngliche Liste festgelegt wurden.</span><span class="sxs-lookup"><span data-stu-id="2b484-137">Set content types on the new list based on the content types that were set on the original list.</span></span>
    
5. <span data-ttu-id="2b484-138">(Optional) Ansichten hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="2b484-138">(Optional) Add views.</span></span> 
    
6. <span data-ttu-id="2b484-139">(Optional) Ansichten zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="2b484-139">(Optional) Remove views.</span></span>
    
7. <span data-ttu-id="2b484-140">Migrieren von Inhalten aus der ursprünglichen Liste in die neue Liste.</span><span class="sxs-lookup"><span data-stu-id="2b484-140">Migrate content from the original list to the new list.</span></span>
    
<span data-ttu-id="2b484-141">Im folgenden Code veranschaulicht die Methode Listen zu suchen, die mit einer bestimmten Basis Vorlage erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="2b484-141">In the following code, the method shows how to find lists that were created using a specific base template.</span></span> <span data-ttu-id="2b484-142">Diese Methode:</span><span class="sxs-lookup"><span data-stu-id="2b484-142">This method:</span></span>

1. <span data-ttu-id="2b484-143">Mithilfe der [ClientContext](https://msdn.microsoft.com/library/microsoft.sharepoint.client.clientcontext.aspx) alle Listen im aktuellen Web mit [Web.Lists](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.lists.aspx)abgerufen.</span><span class="sxs-lookup"><span data-stu-id="2b484-143">Uses the [ClientContext](https://msdn.microsoft.com/library/microsoft.sharepoint.client.clientcontext.aspx) to get all lists in the current web using [Web.Lists](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.lists.aspx).</span></span> <span data-ttu-id="2b484-144">Die Include-Anweisung wird in der Lambda-Ausdruck verwendet, um eine Sammlung von Listen zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="2b484-144">The Include statement is used in the lambda expression to return a collection of lists.</span></span> <span data-ttu-id="2b484-145">Die zurückgegebenen Listen müssen alle Eigenschaftswerte für [BaseTemplate](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetemplate.aspx) [BaseType](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetype.aspx)und [Titel](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.title.aspx)angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="2b484-145">The returned lists must all have property values specified for [BaseTemplate](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetemplate.aspx), [BaseType](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetype.aspx), and [Title](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.title.aspx).</span></span>
    
2. <span data-ttu-id="2b484-146">Für jede Liste in der Auflistung der zurückgegebenen Listen Wenn die **List.BaseTemplate** 10003 gleich ist, hinzugefügt die Liste eine Sammlung von Listen ersetzt werden, **ListsToReplace**aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="2b484-146">For each list in the collection of returned lists, if the  **List.BaseTemplate** is equal to 10003, adds the list to a collection of lists to be replaced, called **listsToReplace**.</span></span> <span data-ttu-id="2b484-147">Denken Sie daran, dass 10003 Bezeichner der benutzerdefinierten Listenvorlage war, als es in der Stichprobe Contoso.Intranet überprüft.</span><span class="sxs-lookup"><span data-stu-id="2b484-147">Remember that 10003 was the custom list template's identifier we reviewed in the Contoso.Intranet sample.</span></span>

<span data-ttu-id="2b484-148">**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="2b484-148">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
static void Main(string[] args)
{
    using (var clientContext = new ClientContext("http://w15-sp/sites/ftclab"))
    {
        Web web = clientContext.Web;
        ListCollection listCollection = web.Lists;
        clientContext.Load(listCollection,
                            l => l.Include(list => list.BaseTemplate,
                                            list => list.BaseType,
                                            list => list.Title));
        clientContext.ExecuteQuery();
        var listsToReplace = new List<List>();
        foreach (List list in listCollection)
        {
            // 10003 is the custom list template ID of the list template you're replacing.
            if (list.BaseTemplate == 10003)
            {
                listsToReplace.Add(list);
            }
        }
        foreach (List list in listsToReplace)
        {
            ReplaceList(clientContext, listCollection, list);
        }
    }
}
```

<span data-ttu-id="2b484-149">**Wichtig:**  Im vorherigen Code durchlaufen zuerst die ListCollection auswählen, welche Listen müssen geändert werden, und rufen Sie dann ReplaceList, der gestartet wird, ändern die Listen.</span><span class="sxs-lookup"><span data-stu-id="2b484-149">**Important:**  In the previous code, you first iterate over the ListCollection to select which lists need to be modified, and then call ReplaceList, which starts modifying the lists.</span></span> <span data-ttu-id="2b484-150">Dieses Muster ist erforderlich, da Ändern des Inhalts einer Auflistung beim Durchlaufen der Auflistung eine Ausnahme ausgelöst wird.</span><span class="sxs-lookup"><span data-stu-id="2b484-150">This pattern is required because modifying the content of a collection while iterating over the collection will throw an exception.</span></span>

<span data-ttu-id="2b484-151">Nach der Identifizierung einer Liste, die ersetzt werden soll, zeigt **ReplaceList** die Reihenfolge der Vorgänge ausführen, um die Liste zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="2b484-151">After identifying a list that should be replaced,  **ReplaceList** shows the order of operations to perform to replace the list.</span></span>

```C#
private static void ReplaceList(ClientContext clientContext, ListCollection listCollection, List listToBeReplaced)
{
    var newList = CreateReplacementList(clientContext, listCollection, listToBeReplaced);

    SetListSettings(clientContext, listToBeReplaced, newList);

    SetContentTypes(clientContext, listToBeReplaced, newList);

    AddViews(clientContext, listToBeReplaced, newList);

    RemoveViews(clientContext, listToBeReplaced, newList);

    MigrateContent(clientContext, listToBeReplaced, newList);
}
```

<span data-ttu-id="2b484-152">So erstellen Sie eine neue Liste, verwendet **CreateReplacementList** [ListCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.listcreationinformation.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b484-152">To create a new list,  **CreateReplacementList** uses [ListCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.listcreationinformation.aspx).</span></span> <span data-ttu-id="2b484-153">Der Titel der neuen Liste wird auf den Titel der vorhandenen Liste mit Add-in angehängt festgelegt.</span><span class="sxs-lookup"><span data-stu-id="2b484-153">The title of the new list is set to the title of the existing list, with Add-in appended to it.</span></span> <span data-ttu-id="2b484-154">Die [ListTemplateType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.listtemplatetype.aspx) -Enumeration wird der Listentyp Vorlage auf einer Dokumentbibliothek festgelegt.</span><span class="sxs-lookup"><span data-stu-id="2b484-154">The [ListTemplateType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.listtemplatetype.aspx) enumeration is used to set the list's template type to a document library.</span></span> <span data-ttu-id="2b484-155">Wenn Sie eine Liste basierend auf einen anderen Vorlagentyp erstellen, stellen Sie sicher, dass Sie den richtige Vorlagentyp verwenden.</span><span class="sxs-lookup"><span data-stu-id="2b484-155">If you are creating a list based on a different template type, make sure to use the correct template type.</span></span> <span data-ttu-id="2b484-156">Wenn Sie eine Kalenderliste erstellen, verwenden Sie **ListTemplateType.Events** anstelle von **ListTemplateType.DocumentLibrary**fest.</span><span class="sxs-lookup"><span data-stu-id="2b484-156">For example, if you are creating a calendar list, use **ListTemplateType.Events** instead of **ListTemplateType.DocumentLibrary**.</span></span>

```C#
private static List CreateReplacementList(ClientContext clientContext, ListCollection lists,List listToBeReplaced)
{
    var creationInformation = new ListCreationInformation
    {
        Title = listToBeReplaced.Title + "add-in",
        TemplateType = (int) ListTemplateType.DocumentLibrary,
    };
    List newList = lists.Add(creationInformation);
    clientContext.ExecuteQuery();
    return newList;
}
```

<span data-ttu-id="2b484-157">**SetListSettings** gilt die ursprüngliche listeneinstellungen für die neue Liste durch:</span><span class="sxs-lookup"><span data-stu-id="2b484-157">**SetListSettings** applies the original list settings to the new list by:</span></span>

1. <span data-ttu-id="2b484-158">Abrufen von verschiedenen Einstellungen für die Liste aus der ursprünglichen Liste.</span><span class="sxs-lookup"><span data-stu-id="2b484-158">Getting various list settings from the original list.</span></span>
    
2. <span data-ttu-id="2b484-159">Die Liste Einstellung aus der ursprünglichen Liste in die neue Liste anwenden.</span><span class="sxs-lookup"><span data-stu-id="2b484-159">Applying the list setting from the original list to the new list.</span></span>

```C#
private static void SetListSettings(ClientContext clientContext, List listToBeReplaced, List newList)
{
    clientContext.Load(listToBeReplaced, 
                        l => l.EnableVersioning, 
                        l => l.EnableModeration, 
                        l => l.EnableMinorVersions,
                        l => l.DraftVersionVisibility );
    clientContext.ExecuteQuery();
    newList.EnableVersioning = listToBeReplaced.EnableVersioning;
    newList.EnableModeration = listToBeReplaced.EnableModeration;
    newList.EnableMinorVersions= listToBeReplaced.EnableMinorVersions;
    newList.DraftVersionVisibility = listToBeReplaced.DraftVersionVisibility;
    newList.Update();
    clientContext.ExecuteQuery();
}
```

<span data-ttu-id="2b484-160">**Hinweis:**  Basierend auf Ihren Anforderungen, können die Einstellungen für die Liste Ihrer ursprünglichen Listen abweichen.</span><span class="sxs-lookup"><span data-stu-id="2b484-160">**Note:**  Based on your requirements, the list settings of your original lists might be different.</span></span> <span data-ttu-id="2b484-161">Überprüfen Sie die listeneinstellungen, und ändern Sie **SetListSettings** , um sicherzustellen, dass die ursprünglichen listeneinstellungen auf Ihre neuen Listen angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="2b484-161">Review your list settings and change  **SetListSettings** to ensure that your original list settings are applied to your new lists.</span></span>

<span data-ttu-id="2b484-162">**SetContentTypes** setzt die Inhaltstypen in der neuen Liste durch:</span><span class="sxs-lookup"><span data-stu-id="2b484-162">**SetContentTypes** sets the content types on the new list by:</span></span>

1. <span data-ttu-id="2b484-163">Abrufen von Inhaltstyp-Informationen aus der ursprünglichen Liste.</span><span class="sxs-lookup"><span data-stu-id="2b484-163">Getting content type information from the original list.</span></span>
    
2. <span data-ttu-id="2b484-164">Abrufen von Inhaltstyp-Informationen aus der neuen Liste.</span><span class="sxs-lookup"><span data-stu-id="2b484-164">Getting content type information from the new list.</span></span>
    
3. <span data-ttu-id="2b484-165">Bestimmen, ob die ursprüngliche Liste Inhaltstypen ermöglicht.</span><span class="sxs-lookup"><span data-stu-id="2b484-165">Determining whether the original list enables content types.</span></span> <span data-ttu-id="2b484-166">Wenn die ursprüngliche Liste Inhaltstypen nicht aktiviert wird, beendet **SetContentTypes** .</span><span class="sxs-lookup"><span data-stu-id="2b484-166">If the original list does not enable content types,  **SetContentTypes** exits.</span></span> <span data-ttu-id="2b484-167">Wenn die ursprüngliche Liste Inhaltstypen aktiviert, und klicken Sie dann **SetContentTypes** ermöglicht Inhaltstypen auf die neue Liste mit **newList.ContentTypesEnabled = True**.</span><span class="sxs-lookup"><span data-stu-id="2b484-167">If the original list enabled content types, then **SetContentTypes** enables content types on the new list using **newList.ContentTypesEnabled = true**.</span></span>
    
4. <span data-ttu-id="2b484-168">Für jeden Inhaltstyp in der ursprünglichen Liste, suchen den Inhalt für die neue Liste, eine entsprechende Content Type basierend auf den Namen des Inhaltstyps mithilfe von **newList.ContentTypes.Any erhalten Typen (ct = > ct. Name == contentType.Name)**.</span><span class="sxs-lookup"><span data-stu-id="2b484-168">For each content type in the original list, searching the content types on the new list to find a matching content type based on name of the content type by using  **newList.ContentTypes.Any(ct => ct.Name == contentType.Name)**.</span></span> <span data-ttu-id="2b484-169">Wenn der Inhaltstyp nicht in der neuen Liste ist, wird es der Liste hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="2b484-169">If the content type is not in the new list, it is added to the list.</span></span>
    
5. <span data-ttu-id="2b484-170">Laden ein zweites Mal **NewList** , da [AddExistingContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) möglicherweise die Inhaltstypen geändert haben.</span><span class="sxs-lookup"><span data-stu-id="2b484-170">Loading  **newList** a second time because [AddExistingContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) might have changed the content types.</span></span>
    
6. <span data-ttu-id="2b484-171">Für jeden Inhaltstyp in **NewList**, bestimmen, ob der Inhaltstyp ein Inhaltstyps in der ursprünglichen Liste basierend auf [ContentType.Name](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.name.aspx) mithilfe von **listToBeReplaced.ContentTypes.Any entspricht (ct = > ct. Name == contentType.Name)**.</span><span class="sxs-lookup"><span data-stu-id="2b484-171">For each content type in  **newList**, determining whether the content type matches a content type in the original list based on [ContentType.Name](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.name.aspx) by using **listToBeReplaced.ContentTypes.Any(ct => ct.Name == contentType.Name)**.</span></span> <span data-ttu-id="2b484-172">Wenn eine Übereinstimmung gefunden wird, wird der Inhaltstyp **ContentTypesToDelete** aus der neuen Liste gelöscht werden hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="2b484-172">If a match is not found, the content type is added to **contentTypesToDelete** to be deleted from the new list.</span></span>
    
7. <span data-ttu-id="2b484-173">Löschen des Inhaltstyps [ContentType.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.deleteobject.aspx)aufrufen.</span><span class="sxs-lookup"><span data-stu-id="2b484-173">Deleting the content type by calling [ContentType.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.deleteobject.aspx).</span></span>

<span data-ttu-id="2b484-174">**Hinweis:**  Wenn Sie einen direkte Transformation Ansatz verwenden und Ihre Inhaltstypen deklarativ mithilfe des Feature-Frameworks bereitgestellt wurden, müssen Sie:</span><span class="sxs-lookup"><span data-stu-id="2b484-174">**Note:**  If you are using an in-place transformation approach, and your content types were deployed declaratively using the Feature framework, you need to:</span></span> 

 1. <span data-ttu-id="2b484-175">Erstellen Sie neue Inhaltstypen.</span><span class="sxs-lookup"><span data-stu-id="2b484-175">Create new content types.</span></span>

 2. <span data-ttu-id="2b484-176">Legen Sie den Inhaltstyp für die Listenelemente beim Migrieren von Inhalt aus der ursprünglichen Liste auf die neue Liste im MigrateContent.</span><span class="sxs-lookup"><span data-stu-id="2b484-176">Set the content type on the list items when migrating the content from the original list to the new list in MigrateContent.</span></span>


```C#
private static void SetContentTypes(ClientContext clientContext, List listToBeReplaced, List newList)
{
    clientContext.Load(listToBeReplaced,
                        l => l.ContentTypesEnabled,
                        l => l.ContentTypes);
    clientContext.Load(newList,
                        l => l.ContentTypesEnabled,
                        l => l.ContentTypes);
    clientContext.ExecuteQuery();

    // If the original list doesn't use content types, do not proceed any further.
    if (!listToBeReplaced.ContentTypesEnabled) return;

    newList.ContentTypesEnabled = true;
    newList.Update();
    clientContext.ExecuteQuery();
    foreach (var contentType in listToBeReplaced.ContentTypes)
    {
        if (!newList.ContentTypes.Any(ct => ct.Name == contentType.Name))
        {
            // Current content type needs to be added to the new list. Note that the content type is added to the list, not the site.           
            newList.ContentTypes.AddExistingContentType(contentType.Parent);
            newList.Update();
            clientContext.ExecuteQuery();
        }
    }
    // Reload the content types on newList because they might have changed when AddExistingContentType was called. 
    clientContext.Load(newList, l => l.ContentTypes);
    clientContext.ExecuteQuery();
    // Remove any content types that are not needed.
    var contentTypesToDelete = new List<ContentType>();
    foreach (var contentType in newList.ContentTypes)
    {
        if (!listToBeReplaced.ContentTypes.Any(ct => ct.Name == contentType.Name))
        {
            // Current content type needs to be removed from new list.
            contentTypesToDelete.Add(contentType);
        }
    }
    foreach (var contentType in contentTypesToDelete)
    {
        contentType.DeleteObject();
    }
    newList.Update();
    clientContext.ExecuteQuery();
}
```

<span data-ttu-id="2b484-177">**Hinweis:**  Zu diesem Zeitpunkt kann die neue Liste Inhalt aus der ursprünglichen Liste annehmen.</span><span class="sxs-lookup"><span data-stu-id="2b484-177">**Note:**  At this point, the new list can accept content from the original list.</span></span> <span data-ttu-id="2b484-178">Sie können auch optional hinzufügen und Entfernen von Ansichten.</span><span class="sxs-lookup"><span data-stu-id="2b484-178">You can also optionally add and remove views.</span></span> 

<span data-ttu-id="2b484-179">Benutzer können hinzufügen oder Entfernen von Ansichten in einer Liste zu ihrer geschäftlichen Anforderungen definiert.</span><span class="sxs-lookup"><span data-stu-id="2b484-179">Users can add or remove views defined on a list to meet their business needs.</span></span> <span data-ttu-id="2b484-180">Aus diesem Grund müssen Sie zum Hinzufügen oder Entfernen von Ansichten für die neue Liste.</span><span class="sxs-lookup"><span data-stu-id="2b484-180">For this reason, you might need to add or remove views on the new list.</span></span>  <span data-ttu-id="2b484-181">**AddViews** hinzugefügt der neuen Liste von Ansichten aus der ursprünglichen Liste:</span><span class="sxs-lookup"><span data-stu-id="2b484-181">**AddViews** adds views from the original list to the new list by:</span></span>

1. <span data-ttu-id="2b484-182">Verwenden zum Abrufen aller Ansichten in der ursprünglichen Liste [List.Views](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.views.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2b484-182">Using [List.Views](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.views.aspx) to get all views on the original list.</span></span>
    
2. <span data-ttu-id="2b484-183">Verwenden des Lambda-Ausdrucks geladen werden verschiedene Eigenschaften anzeigen auf die **Views** -Auflistung.</span><span class="sxs-lookup"><span data-stu-id="2b484-183">Using the lambda expression to load various view properties on the  **views** collection.</span></span>
    
3. <span data-ttu-id="2b484-184">Erstellen eine Ansicht für die einzelnen Ansichten in der ursprünglichen Liste mithilfe von [komplexer ViewCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewcreationinformation.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b484-184">For each view in the original list, creating a view by using [ViewCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewcreationinformation.aspx).</span></span> <span data-ttu-id="2b484-185">Verschiedene Eigenschaften für die neue Ansicht basierend auf Eigenschaften anzeigen, aus der ursprünglichen Ansicht festgelegt.</span><span class="sxs-lookup"><span data-stu-id="2b484-185">Various properties are set on the new view based on view properties from the original view.</span></span> <span data-ttu-id="2b484-186">Die Hilfsmethode **GetViewType** wird aufgerufen, um die [ViewType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewtype.aspx) der Ansicht zu bestimmen.</span><span class="sxs-lookup"><span data-stu-id="2b484-186">The  **GetViewType** helper method is called to determine the [ViewType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewtype.aspx) of the view.</span></span> <span data-ttu-id="2b484-187">Die Liste der Ansichten **ViewsToCreate**aufgerufen wird dann die neue Ansicht hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="2b484-187">The new view is then added to the list of views called **viewsToCreate**.</span></span>
    
4. <span data-ttu-id="2b484-188">Die Ansichten hinzufügen mithilfe der **Add** -Methode in der Liste Views-Auflistung der **List.Views** -Auflistung.</span><span class="sxs-lookup"><span data-stu-id="2b484-188">Adding the views to the  **List.Views** collection by using the **Add** method on the list's Views collection.</span></span>

```C#
private static void AddViews(ClientContext clientContext, List listToBeReplaced, List newList)
{
    ViewCollection views = listToBeReplaced.Views;
    clientContext.Load(views,
                        v => v.Include(view => view.Paged,
                            view => view.PersonalView,
                            view => view.ViewQuery,
                            view => view.Title,
                            view => view.RowLimit,
                            view => view.DefaultView,
                            view => view.ViewFields,
                            view => view.ViewType));
    clientContext.ExecuteQuery();

    // Build a list of views which exist on the original list only.
    var viewsToCreate = new List<ViewCreationInformation>();
    foreach (View view in listToBeReplaced.Views)
    {
      var createInfo = new ViewCreationInformation
      {
          Paged = view.Paged,
          PersonalView = view.PersonalView,
          Query = view.ViewQuery,
          Title = view.Title,
          RowLimit = view.RowLimit,
          SetAsDefaultView = view.DefaultView,
          ViewFields = view.ViewFields.ToArray(),
          ViewTypeKind = GetViewType(view.ViewType),
      };
      viewsToCreate.Add(createInfo);
    }
    
    foreach (ViewCreationInformation newView in viewsToCreate)
    {
        newList.Views.Add(newView);
    }
    newList.Update();
}

private static ViewType GetViewType(string viewType)
{
    switch (viewType)
    {
        case "HTML":
            return ViewType.Html;
        case "GRID":
            return ViewType.Grid;
        case "CALENDAR":
            return ViewType.Calendar;
        case "RECURRENCE":
            return ViewType.Recurrence;
        case "CHART":
            return ViewType.Chart;
        case "GANTT":
            return ViewType.Gantt;
        default:
            return ViewType.None;
    }
}
```

<span data-ttu-id="2b484-189">Im folgenden Code werden **RemoveViews** Ansichten aus der neuen Liste entfernt:</span><span class="sxs-lookup"><span data-stu-id="2b484-189">In the following code,  **RemoveViews** removes views from the new list by:</span></span>

1. <span data-ttu-id="2b484-190">Abrufen von Listenansichten auf die neue Liste mithilfe der **List.Views** -Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="2b484-190">Getting the list views on the new list using the  **List.Views** property.</span></span>
    
2. <span data-ttu-id="2b484-191">Für jede Ansicht in der neuen Liste bestimmen, ob die Ansicht in der ursprünglichen Liste nicht vorhanden ist, durch Klicken auf den Titel der Ansicht mithilfe von **entsprechende! listToBeReplaced.Views.Any (V = > v.Title == anzeigen. Titel**.</span><span class="sxs-lookup"><span data-stu-id="2b484-191">For each view on the new list, determining whether that view does not exist in the original list by matching on the view's title by using  **!listToBeReplaced.Views.Any(v => v.Title == view.Title**.</span></span> <span data-ttu-id="2b484-192">Wenn eine Ansicht in der neuen Liste eine entsprechende Ansicht nicht in der ursprünglichen Liste verfügt, fügen Sie der Ansicht **ViewsToRemove**hinzu.</span><span class="sxs-lookup"><span data-stu-id="2b484-192">If a view in the new list does not have a matching view in the original list, then add the view to **viewsToRemove**.</span></span>
    
3. <span data-ttu-id="2b484-193">Löschen aller Ansichten in **ViewsToRemove** mit [View.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.view.deleteobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b484-193">Deleting all views in  **viewsToRemove** by using [View.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.view.deleteobject.aspx).</span></span>
    
```C#
private static void RemoveViews(ClientContext clientContext, List listToBeReplaced, List newList)
{
    // Get the list of views on the new list.
    clientContext.Load(newList, l => l.Views);
    clientContext.ExecuteQuery();

    var viewsToRemove = new List<View>();
    foreach (View view in newList.Views)
    {
        if (!listToBeReplaced.Views.Any(v => v.Title == view.Title))
        {
            // If there is no matching view in the source list, add the view to the list of views to be deleted.
            viewsToRemove.Add(view);
        }
    }
    foreach (View view in viewsToRemove)
    {
        view.DeleteObject();
    }
    newList.Update();
    clientContext.ExecuteQuery();
}
```

<span data-ttu-id="2b484-194">**MigrateContent** migriert die Inhalte aus der ursprünglichen Liste auf die neue Liste durch:</span><span class="sxs-lookup"><span data-stu-id="2b484-194">**MigrateContent** migrates the content from the original list to the new list by:</span></span>

1. <span data-ttu-id="2b484-195">Das Ziel, um die Dateien zu kopieren oder den Stammordner der neuen Liste mithilfe von [List.RootFolder](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.rootfolder.aspx)abgerufen.</span><span class="sxs-lookup"><span data-stu-id="2b484-195">Retrieving the destination to copy the files to, or the root folder of the new list, by using [List.RootFolder](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.rootfolder.aspx).</span></span> <span data-ttu-id="2b484-196">Mithilfe von [Folder.ServerRelativeUrl](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.folder.serverrelativeurl.aspx)ist die serverrelative URL des Listenordners Ziel abgerufen.</span><span class="sxs-lookup"><span data-stu-id="2b484-196">The server-relative URL of the destination list folder is retrieved by using [Folder.ServerRelativeUrl](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.folder.serverrelativeurl.aspx).</span></span>
    
2. <span data-ttu-id="2b484-197">Abrufen der Quelle für die Dateien oder den Stammordner der ursprünglichen Liste mit **List.RootFolder**.</span><span class="sxs-lookup"><span data-stu-id="2b484-197">Retrieving the source of the files, or the root folder of the original list, by using  **List.RootFolder**.</span></span> <span data-ttu-id="2b484-198">Die serverrelative URL des Listenordners und alle Dateien im Stammordner der Quelle werden mithilfe des **ClientContext** -Objekts geladen.</span><span class="sxs-lookup"><span data-stu-id="2b484-198">The server-relative URL of the list folder and all the files in the source's root folder are loaded by using the **clientContext** object.</span></span>
    
3. <span data-ttu-id="2b484-199">Für jede Datei in der Quelle erstellen **NewUrl**, womit die neue URL der Datei gespeichert.</span><span class="sxs-lookup"><span data-stu-id="2b484-199">For each file in the source, creating  **newUrl**, which stores the new URL of the file.</span></span> <span data-ttu-id="2b484-200">**NewUrl** wird erstellt, durch das Ziel Stammordner der Stamm des Quellordners ersetzen.</span><span class="sxs-lookup"><span data-stu-id="2b484-200">**newUrl** is created by replacing the source root folder with the destination's root folder.</span></span>
    
4. <span data-ttu-id="2b484-201">Kopieren die Datei auf die URL des Stammordners Ziel mithilfe [File.CopyTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.copyto.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2b484-201">Using [File.CopyTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.copyto.aspx) to copy the file to the URL of the destination root folder.</span></span> <span data-ttu-id="2b484-202">Alternativ können Sie die [File.MoveTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.moveto.aspx) -Methode verwenden, um die Datei an die Ziel-URL zu verschieben.</span><span class="sxs-lookup"><span data-stu-id="2b484-202">Alternatively, you might choose to use the [File.MoveTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.moveto.aspx) method to move the file to the destination URL.</span></span>
    
<span data-ttu-id="2b484-203">**Hinweis:**  Der folgende Code gibt alle Listenelemente.</span><span class="sxs-lookup"><span data-stu-id="2b484-203">**Note:**  The following code returns all list items.</span></span> <span data-ttu-id="2b484-204">Sollten Sie in Ihrer produktionsumgebung den folgenden Code durch Implementieren einer Schleife, und Migrieren von kleine Mengen von Listenelementen mithilfe mehrerer Iterationen optimieren.</span><span class="sxs-lookup"><span data-stu-id="2b484-204">In your production environment, consider optimizing the following code by implementing a loop, and using multiple iterations to migrate small amounts of list items.</span></span>

```C#
private static void MigrateContent(ClientContext clientContext, List listToBeReplaced, List newList)
{
    ListItemCollection items = listToBeReplaced.GetItems(CamlQuery.CreateAllItemsQuery());
    Folder destination = newList.RootFolder;
    Folder source = listToBeReplaced.RootFolder;
    clientContext.Load(destination,
                        d => d.ServerRelativeUrl);
    clientContext.Load(source,
                        s => s.Files,
                        s => s.ServerRelativeUrl);
    clientContext.Load(items,
                        i => i.IncludeWithDefaultProperties(item => item.File));
    clientContext.ExecuteQuery();


    foreach (File file in source.Files)
    {
        string newUrl = file.ServerRelativeUrl.Replace(source.ServerRelativeUrl, destination.ServerRelativeUrl);
          file.CopyTo(newUrl, true);
          //file.MoveTo(newUrl, MoveOperations.Overwrite);
    }
    clientContext.ExecuteQuery();
}
```

<span data-ttu-id="2b484-205">**Hinweis:**  Der vorstehende Code veranschaulicht, wie zum Migrieren von Dateien in einer Liste im Stammordner gespeichert.</span><span class="sxs-lookup"><span data-stu-id="2b484-205">**Note:**  The previous code shows how to migrate files stored in the root folder of a list.</span></span> <span data-ttu-id="2b484-206">Wenn Ihre Liste Unterordner umfasst, müssen Sie zusätzlichen Code zum Migrieren der Unterordner und deren Inhalt hinzu.</span><span class="sxs-lookup"><span data-stu-id="2b484-206">If your list has subfolders, you will need to add additional code to migrate the subfolders and their contents.</span></span> <span data-ttu-id="2b484-207">Wenn in Ihrer Liste Workflows verwendet wird, ist zusätzlicher Code erforderlich, können Sie den Workflow auf die neue Liste zuordnen.</span><span class="sxs-lookup"><span data-stu-id="2b484-207">If your list uses workflows, additional code is required to associate the workflow to the new list.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b484-208">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="2b484-208">Additional resources</span></span>
<span data-ttu-id="2b484-209"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2b484-209"></span></span>

- [<span data-ttu-id="2b484-210">Transformieren von Farmlösungen in das SharePoint-Add-In-Modell</span><span class="sxs-lookup"><span data-stu-id="2b484-210">Transform farm solutions to the SharePoint add-in model</span></span>](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [<span data-ttu-id="2b484-211">SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="2b484-211">SharePoint 2013</span></span>](https://msdn.microsoft.com/library/office/jj162979.aspx)
