---
title: "Synchronisieren Sie-add-in für SharePoint-Gruppen Beispiel Begriff"
ms.date: 11/03/2017
ms.openlocfilehash: 4d78f316ad42639db4e8932515c574d867d421fc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="synchronize-term-groups-sample-add-in-for-sharepoint"></a><span data-ttu-id="451d9-102">Synchronisieren Sie-add-in für SharePoint-Gruppen Beispiel Begriff</span><span class="sxs-lookup"><span data-stu-id="451d9-102">Synchronize term groups sample add-in for SharePoint</span></span>

<span data-ttu-id="451d9-103">Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie über mehrere SharePoint-Terminologiespeicher ausdrucksgruppen synchronisieren.</span><span class="sxs-lookup"><span data-stu-id="451d9-103">As part of your Enterprise Content Management (ECM) strategy, you can synchronize term groups across multiple SharePoint term stores.</span></span>
    
<span data-ttu-id="451d9-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="451d9-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="451d9-105">Das [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) -Beispiel veranschaulicht das ein vom Anbieter gehosteten add-in mit eine Taxonomie Quell- und synchronisiert werden.</span><span class="sxs-lookup"><span data-stu-id="451d9-105">The [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) sample shows you how to use a provider-hosted add-in to synchronize a source and target taxonomy.</span></span> <span data-ttu-id="451d9-106">Dieses Add-in synchronisiert zwei Terminologiespeicher in den verwalteten Metadatendienst - Quelle und ein Ziel Terminologiespeicher.</span><span class="sxs-lookup"><span data-stu-id="451d9-106">This add-in synchronizes two term stores in the managed metadata service - a source and a target term store.</span></span> <span data-ttu-id="451d9-107">Die folgenden Objekte dienen zum Synchronisieren von ausdrucksgruppen:</span><span class="sxs-lookup"><span data-stu-id="451d9-107">The following objects are used to synchronize term groups:</span></span>

- <span data-ttu-id="451d9-108">**TermStore**</span><span class="sxs-lookup"><span data-stu-id="451d9-108">**TermStore**</span></span> 

- <span data-ttu-id="451d9-109">**ChangeInformation**</span><span class="sxs-lookup"><span data-stu-id="451d9-109">**ChangeInformation**</span></span> 

<span data-ttu-id="451d9-110">Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:</span><span class="sxs-lookup"><span data-stu-id="451d9-110">Use this solution if you want to:</span></span>

- <span data-ttu-id="451d9-111">Synchronisieren von zwei Taxonomien.</span><span class="sxs-lookup"><span data-stu-id="451d9-111">Synchronize two taxonomies.</span></span> <span data-ttu-id="451d9-112">Beispielsweise können Sie SharePoint Online und SharePoint Server 2013 lokal für verschiedene Datenmengen, aber sie verwenden die gleiche Taxonomie.</span><span class="sxs-lookup"><span data-stu-id="451d9-112">For example, you might use both SharePoint Online and SharePoint Server 2013 on-premises for different sets of data, but they use the same taxonomy.</span></span>
    
- <span data-ttu-id="451d9-113">Synchronisieren von Änderungen an einer bestimmten Begriffsgruppe nur.</span><span class="sxs-lookup"><span data-stu-id="451d9-113">Synchronize changes made to a specific term group only.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="451d9-114">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="451d9-114">Before you begin</span></span>
<span data-ttu-id="451d9-115"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="451d9-115"></span></span>

<span data-ttu-id="451d9-116">Laden Sie Sie zuerst [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="451d9-116">To get started, download the  [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="451d9-117">Bevor Sie dieses Add-in ausführen, benötigen Sie über die Berechtigung zum Zugriff auf den Terminologiespeicher in den verwalteten Metadatendienst.</span><span class="sxs-lookup"><span data-stu-id="451d9-117">Before you run this add-in, you'll need permission to access the term store in the managed metadata service.</span></span> <span data-ttu-id="451d9-118">Abbildung 1 zeigt das Office 365 Administrationscenter, wo diese Berechtigungen zugewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="451d9-118">Figure 1 shows the Office 365 admin center where these permissions are assigned.</span></span>

<span data-ttu-id="451d9-119">**Abbildung 1. Zuweisen von Berechtigungen auf den Ausdruck speichern, in der SharePoint-Verwaltungskonsole**</span><span class="sxs-lookup"><span data-stu-id="451d9-119">**Figure 1. Assigning permissions to the term store in the SharePoint admin center**</span></span>

![Screenshot zeigt, dass dem SharePoint-Administrator zentrieren, mit dem Terminologiespeicher Taxonomie Begriff Store Suchfeld und die Begriff Store Administratoren Feldern hervorgehoben.](media/93a19898-6ae2-4176-b030-2546f4c86c5c.png)

<span data-ttu-id="451d9-121">Zuweisen von Berechtigungen auf den Terminologiespeicher</span><span class="sxs-lookup"><span data-stu-id="451d9-121">To assign permissions to the term store:</span></span>

1. <span data-ttu-id="451d9-122">Wählen Sie das Office 365 Administrationscenter **Ausdruck zu speichern**.</span><span class="sxs-lookup"><span data-stu-id="451d9-122">From the Office 365 admin center, choose  **term store**.</span></span>
    
2. <span data-ttu-id="451d9-123">Wählen Sie im **TAXONOMIETERMINOLOGIESPEICHER**den Ausdruckssatz, dass Sie ein Administrator zuweisen möchten.</span><span class="sxs-lookup"><span data-stu-id="451d9-123">In  **TAXONOMY TERM STORE**, choose the term set that you want to assign an administrator to.</span></span>
    
3. <span data-ttu-id="451d9-124">Geben Sie im **Ausdruck speichern Administratoren**die organisationskonto, die Berechtigungen für Administrator den Begriff erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="451d9-124">In  **Term Store Administrators**, enter the organizational account that requires term store administrator permissions.</span></span>

## <a name="using-the-coremmssync-sample-app"></a><span data-ttu-id="451d9-125">Verwenden die Core.MMSSync Beispiel-app</span><span class="sxs-lookup"><span data-stu-id="451d9-125">Using the Core.MMSSync sample app</span></span>
<span data-ttu-id="451d9-126"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="451d9-126"></span></span>

<span data-ttu-id="451d9-127">Wenn Sie das Add-in starten, sehen Sie eine Konsolenanwendung, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="451d9-127">When you start the add-in, you see a console application, as shown in Figure 2.</span></span> <span data-ttu-id="451d9-128">Sie werden aufgefordert, die folgenden Informationen eingeben:</span><span class="sxs-lookup"><span data-stu-id="451d9-128">You are prompted to enter the following information:</span></span>

- <span data-ttu-id="451d9-129">Die URL des im Office 365 Administrationscenter, das die Quelle Terminologiespeicher enthält (Dies ist die URL für den Metadatendienst managed Quell).</span><span class="sxs-lookup"><span data-stu-id="451d9-129">The URL of the Office 365 admin center that contains the source term store (this is the URL of the source managed metadata service).</span></span> <span data-ttu-id="451d9-130">Geben Sie zum Beispiel https://contososource-admin.sharepoint.com ein.</span><span class="sxs-lookup"><span data-stu-id="451d9-130">For example, you might enter https://contososource-admin.sharepoint.com.</span></span>
    
- <span data-ttu-id="451d9-131">Den Benutzernamen und das Kennwort eines laufzeitspeicheradministrators auf Ihre Datenquelle verwalteter Metadatendienst.</span><span class="sxs-lookup"><span data-stu-id="451d9-131">The user name and password of a term store administrator on your source managed metadata service.</span></span>
    
- <span data-ttu-id="451d9-132">Die URL der Menüschaltfläche 365 Administrationscenter, die den Begriff Zielspeicher enthält (Dies ist die URL des Ziels MMS).</span><span class="sxs-lookup"><span data-stu-id="451d9-132">The URL of theOffice 365 admin center that contains the target term store (this is the URL of the target MMS).</span></span> <span data-ttu-id="451d9-133">Geben Sie zum Beispiel https://contosotarget-admin.sharepoint.com ein.</span><span class="sxs-lookup"><span data-stu-id="451d9-133">For example, you might enter https://contosotarget-admin.sharepoint.com.</span></span>
    
- <span data-ttu-id="451d9-134">Den Benutzernamen und das Kennwort eines laufzeitspeicheradministrators auf Ihrer Ziel verwalteter Metadatendienst.</span><span class="sxs-lookup"><span data-stu-id="451d9-134">The user name and password of a term store administrator on your target managed metadata service.</span></span>
    
- <span data-ttu-id="451d9-135">Den Typ des Vorgangs, die Sie ausführen möchten.</span><span class="sxs-lookup"><span data-stu-id="451d9-135">The type of operation you want to perform.</span></span> <span data-ttu-id="451d9-136">Sie können:</span><span class="sxs-lookup"><span data-stu-id="451d9-136">You can either:</span></span>
    
    - <span data-ttu-id="451d9-137">Verschieben einer Begriffsgruppe (Szenario 1) mithilfe des **TermStore** -Objekts.</span><span class="sxs-lookup"><span data-stu-id="451d9-137">Move a term group (scenario 1) by using the  **TermStore** object.</span></span>
    
    - <span data-ttu-id="451d9-138">Process Changes (Szenario 2) mithilfe des **ChangeInformation** -Objekts.</span><span class="sxs-lookup"><span data-stu-id="451d9-138">Process changes (scenario 2) by using the  **ChangeInformation** object.</span></span>

<span data-ttu-id="451d9-139">**Wichtige**  In diesem Beispiel-add-in funktioniert mit beiden SharePoint Online und SharePoint Server 2013 lokal.</span><span class="sxs-lookup"><span data-stu-id="451d9-139">**Important**  This sample add-in works with both SharePoint Online and SharePoint Server 2013 on-premises.</span></span>

<span data-ttu-id="451d9-140">**Abbildung 2. Core.MMSSync Konsolenanwendung**</span><span class="sxs-lookup"><span data-stu-id="451d9-140">**Figure 2. Core.MMSSync console application**</span></span>

![Screenshot der Konsole Anwendung anfordern von Informationen eingegeben werden.](media/1ef0e4f4-6f79-46b0-83d3-bdf9d87ccad9.png)

<span data-ttu-id="451d9-142">Nachdem Sie Ihr Szenario ausgewählt haben, geben Sie den Namen der Begriffsgruppe, den, die Sie aus der Quelle zu Ihrer Ziel verwalteten Metadatendienst synchronisieren, wie in Abbildung 3 dargestellt möchten.</span><span class="sxs-lookup"><span data-stu-id="451d9-142">After you select your scenario, enter the name of the term group you want to synchronize from your source to your target managed metadata service, as shown in Figure 3.</span></span> <span data-ttu-id="451d9-143">Geben Sie zum Beispiel Enterprise ein.</span><span class="sxs-lookup"><span data-stu-id="451d9-143">For example, you might enter Enterprise.</span></span>

<span data-ttu-id="451d9-144">**Abbildung 3. Begriff Gruppen in den verwalteten Metadatendienst**</span><span class="sxs-lookup"><span data-stu-id="451d9-144">**Figure 3. Term groups in the managed metadata service**</span></span>

![Screenshot der Taxonomie Begriff Store Dropdown-Liste.](media/5202fd88-4f2f-4b68-8083-165e6702bc86.png)
### <a name="scenario-1---move-term-group"></a><span data-ttu-id="451d9-146">Szenario 1 – Begriffsgruppe verschieben</span><span class="sxs-lookup"><span data-stu-id="451d9-146">Scenario 1 - Move term group</span></span>

<span data-ttu-id="451d9-147">Bei der Auswahl **Begriffsgruppe verschieben**des Add-Ins werden Sie aufgefordert, geben Sie eine Term-Gruppe zum Synchronisieren und ruft dann die **CopyNewTermGroups** -Methode in MMSSyncManager.cs.</span><span class="sxs-lookup"><span data-stu-id="451d9-147">When you select  **Move Term Group**, the add-in prompts you to enter a term group to synchronize and then calls the  **CopyNewTermGroups** method in MMSSyncManager.cs.</span></span> <span data-ttu-id="451d9-148">**CopyNewTermGroups** führt dann Folgendes ein, um eine Begriffsgruppe aus dem Terminologiespeicher Quelle auf den Terminologiespeicher Ziel kopieren:</span><span class="sxs-lookup"><span data-stu-id="451d9-148">**CopyNewTermGroups** then does the following to copy a term group from the source term store to the target term store:</span></span>

1. <span data-ttu-id="451d9-149">Ruft die Quell- und Ziel-Begriff Objekte gespeichert.</span><span class="sxs-lookup"><span data-stu-id="451d9-149">Retrieves the source and target term store objects.</span></span>
    
2. <span data-ttu-id="451d9-150">Stellt sicher, dass die Sprachen des Ausdrucks Quell- und speichert die Übereinstimmung.</span><span class="sxs-lookup"><span data-stu-id="451d9-150">Verifies that the languages of the source and target term stores match.</span></span> 
    
3. <span data-ttu-id="451d9-151">Überprüft, ob die Quelle Begriffsgruppe nicht im Terminologiespeicher Ziel vorhanden ist, und klicken Sie dann die Quelle Begriffsgruppe auf den Terminologiespeicher Ziel mithilfe von **CreateNewTargetTermGroup**kopiert.</span><span class="sxs-lookup"><span data-stu-id="451d9-151">Verifies that the source term group doesn't exist in the target term store, and then copies the source term group to the target term store by using  **CreateNewTargetTermGroup**.</span></span> 
    
<span data-ttu-id="451d9-152">Sie können die Parameter _TermGroupExclusions_, _TermGroupToCopy_und _TermSetInclusions_ gefiltert, welche Begriffe verarbeitet festlegen.</span><span class="sxs-lookup"><span data-stu-id="451d9-152">You can set the  _TermGroupExclusions_,  _TermGroupToCopy_, and  _TermSetInclusions_ parameters to filter which terms get processed.</span></span>

<span data-ttu-id="451d9-153">Im folgenden Codebeispiel wird die Verwendung der Methods **CopyNewTermGroups** und **CreateNewTargetTermGroup** MMSSyncManager.cs.</span><span class="sxs-lookup"><span data-stu-id="451d9-153">The following code shows the  **CopyNewTermGroups** and **CreateNewTargetTermGroup** methods in MMSSyncManager.cs.</span></span>

> [!NOTE] 
> <span data-ttu-id="451d9-154">Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="451d9-154">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
public bool CopyNewTermGroups(ClientContext sourceContext, ClientContext targetContext, List<string> termGroupExclusions = null, string termGroupToCopy = null)
        {
            TermStore sourceTermStore = GetTermStoreObject(sourceContext);
            TermStore targetTermStore = GetTermStoreObject(targetContext);

            
            List<int> languagesToProcess = null;
            if (!ValidTermStoreLanguages(sourceTermStore, targetTermStore, out languagesToProcess))
            {
                Log.Internal.TraceError((int)EventId.LanguageMismatch, "The target termstore default language is not available as language in the source term store, syncing cannot proceed.");
                return false;
            }

            // Get a list of term groups to process. Exclude site collection-scoped groups and system groups.
            IEnumerable<TermGroup> termGroups = sourceContext.LoadQuery(sourceTermStore.Groups.Include(g => g.Name,
                                                                                                       g => g.Id,
                                                                                                       g => g.IsSiteCollectionGroup,
                                                                                                       g => g.IsSystemGroup))
                                                                                              .Where(g => g.IsSystemGroup == false &amp;&amp; g.IsSiteCollectionGroup == false);
            sourceContext.ExecuteQuery();

            foreach (TermGroup termGroup in termGroups)
            {
                // Skip term group if you only want to copy one particular term group.
                if (!String.IsNullOrEmpty(termGroupToCopy))
                {
                    if (!termGroup.Name.Equals(termGroupToCopy, StringComparison.InvariantCultureIgnoreCase))
                    {
                        continue;
                    }
                }

                // Skip term groups that you do not want to copy.
                if (termGroupExclusions != null &amp;&amp; termGroupExclusions.Contains(termGroup.Name, StringComparer.InvariantCultureIgnoreCase))
                {
                    Log.Internal.TraceInformation((int)EventId.CopyTermGroup_Skip, "Skipping {0} as this is a system termgroup", termGroup.Name);
                    continue;
                }

                // About to start copying a term group.
                TermGroup sourceTermGroup = GetTermGroup(sourceContext, sourceTermStore, termGroup.Name);
                TermGroup targetTermGroup = GetTermGroup(targetContext, targetTermStore, termGroup.Name);

                if (sourceTermGroup == null)
                {
                    continue;
                }
                if (targetTermGroup != null)
                {
                    if (sourceTermGroup.Id != targetTermGroup.Id)
                    {
                        // Term group exists with a different ID, unable to sync.
                        Log.Internal.TraceWarning((int)EventId.CopyTermGroup_IDMismatch, "The term groups have different ID's. I don't know how to work it.");
                    }
                    else
                    {
                        // Do nothing as this term group was previously copied. Term group changes need to be 
                        // picked up by the change log processing.
                        Log.Internal.TraceInformation((int)EventId.CopyTermGroup_AlreadyCopied, "Termgroup {0} was already copied...changes to it will need to come from changelog processing.", termGroup.Name);
                    }
                }
                else
                {
                    Log.Internal.TraceInformation((int)EventId.CopyTermGroup_Copying, "Copying termgroup {0}...", termGroup.Name);
                    this.CreateNewTargetTermGroup(sourceContext, targetContext, sourceTermGroup, targetTermStore, languagesToProcess);
                }
            }

            return true;
        }



private void CreateNewTargetTermGroup(ClientContext sourceClientContext, ClientContext targetClientContext, TermGroup sourceTermGroup, TermStore targetTermStore, List<int> languagesToProcess)
        {
            TermGroup destinationTermGroup = targetTermStore.CreateGroup(sourceTermGroup.Name, sourceTermGroup.Id);
            if (!string.IsNullOrEmpty(sourceTermGroup.Description))
            {
                destinationTermGroup.Description = sourceTermGroup.Description;
            }

            TermSetCollection sourceTermSetCollection = sourceTermGroup.TermSets;
            if (sourceTermSetCollection.Count > 0)
            {
                foreach (TermSet sourceTermSet in sourceTermSetCollection)
                {
                    sourceClientContext.Load(sourceTermSet,
                                              set => set.Name,
                                              set => set.Description,
                                              set => set.Id,
                                              set => set.Contact,
                                              set => set.CustomProperties,
                                              set => set.IsAvailableForTagging,
                                              set => set.IsOpenForTermCreation,
                                              set => set.CustomProperties,
                                              set => set.Terms.Include(
                                                        term => term.Name,
                                                        term => term.Description,
                                                        term => term.Id,
                                                        term => term.IsAvailableForTagging,
                                                        term => term.LocalCustomProperties,
                                                        term => term.CustomProperties,
                                                        term => term.IsDeprecated,
                                                        term => term.Labels.Include(label => label.Value, label => label.Language, label => label.IsDefaultForLanguage)));

                    sourceClientContext.ExecuteQuery();

                    TermSet targetTermSet = destinationTermGroup.CreateTermSet(sourceTermSet.Name, sourceTermSet.Id, targetTermStore.DefaultLanguage);
                    targetClientContext.Load(targetTermSet, set => set.CustomProperties);
                    targetClientContext.ExecuteQuery();
                    UpdateTermSet(sourceClientContext, targetClientContext, sourceTermSet, targetTermSet);

                    foreach (Term sourceTerm in sourceTermSet.Terms)
                    {
                        Term reusedTerm = targetTermStore.GetTerm(sourceTerm.Id);
                        targetClientContext.Load(reusedTerm);
                        targetClientContext.ExecuteQuery();

                        Term targetTerm;
                        if (reusedTerm.ServerObjectIsNull.Value)
                        {
                            try
                            {
                                targetTerm = targetTermSet.CreateTerm(sourceTerm.Name, targetTermStore.DefaultLanguage, sourceTerm.Id);
                                targetClientContext.Load(targetTerm, term => term.IsDeprecated,
                                                                     term => term.CustomProperties,
                                                                     term => term.LocalCustomProperties);
                                targetClientContext.ExecuteQuery();
                                UpdateTerm(sourceClientContext, targetClientContext, sourceTerm, targetTerm, languagesToProcess);
                            }
                            catch (ServerException ex)
                            {
                                if (ex.Message.IndexOf("Failed to read from or write to database. Refresh and try again.") > -1)
                                {
                                    // This exception was due to caching issues and generally is thrown when terms are reused across groups.
                                    targetTerm = targetTermSet.ReuseTerm(reusedTerm, false);
                                }
                                else
                                {
                                    throw ex;
                                }
                            }
                        }
                        else
                        {
                            targetTerm = targetTermSet.ReuseTerm(reusedTerm, false);
                        }

                        targetClientContext.Load(targetTerm);
                        targetClientContext.ExecuteQuery();

                        targetTermStore.UpdateCache();

                        // Refresh session and term store references to force reload of the term just added. You need 
                        // to do this because there can be an update change event following next, and if you don't,
                        // the newly created term set cannot be obtained from the server.
                        targetTermStore = GetTermStoreObject(targetClientContext);

                        // Recursively add the other terms.
                        ProcessSubTerms(sourceClientContext, targetClientContext, targetTermSet, targetTerm, sourceTerm, languagesToProcess, targetTermStore.DefaultLanguage);
                    }
                }
            }
            targetClientContext.ExecuteQuery();
        }

```

### <a name="scenario-2---process-changes"></a><span data-ttu-id="451d9-155">Szenario 2: Änderungen an</span><span class="sxs-lookup"><span data-stu-id="451d9-155">Scenario 2 - Process changes</span></span>

<span data-ttu-id="451d9-156">Bei der Auswahl von **Änderungen an**das Add-in werden Sie aufgefordert, geben Sie einen Begriff Gruppe zum Synchronisieren, und klicken Sie dann die **ProcessChanges** -Methode in MMSSyncManager.cs.</span><span class="sxs-lookup"><span data-stu-id="451d9-156">When you select  **Process Changes**, the add-in prompts you to enter a Term Group to synchronize, and then calls the  **ProcessChanges** method in MMSSyncManager.cs.</span></span> <span data-ttu-id="451d9-157">**ProcessChanges** verwendet die **GetChanges** -Methode der **ChangedInformation** -Klasse, um alle Änderungen an Gruppen, Ausdruckssätze und Ausdrücke in der Quelle verwalteten Metadatendienst abzurufen.</span><span class="sxs-lookup"><span data-stu-id="451d9-157">**ProcessChanges** uses the **GetChanges** method of the **ChangedInformation** class to retrieve all changes made to groups, term sets, and terms in the source managed metadata service.</span></span> <span data-ttu-id="451d9-158">Änderungen werden klicken Sie dann auf das Ziel verwalteten Metadatendienst angewendet.</span><span class="sxs-lookup"><span data-stu-id="451d9-158">Changes are then applied to the target managed metadata service.</span></span>

> [!NOTE] 
> <span data-ttu-id="451d9-159">Dieses Dokument enthält nur einige Teile der **ProcessChanges** -Methode.</span><span class="sxs-lookup"><span data-stu-id="451d9-159">This document includes only some parts of the  **ProcessChanges** method.</span></span> <span data-ttu-id="451d9-160">Um die gesamte Methode zu überprüfen, öffnen Sie die Core.MMSSync-Lösung in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="451d9-160">To review the entire method, open the Core.MMSSync solution in Visual Studio.</span></span>

<span data-ttu-id="451d9-161">Die **ProcessChanges** -Methode startet, indem Sie ein **TaxonomySession** -Objekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="451d9-161">The  **ProcessChanges** method starts by creating a **TaxonomySession** object.</span></span>

```C#
Log.Internal.TraceInformation((int)EventId.TaxonomySession_Open, "Opening the taxonomy session");
            TaxonomySession sourceTaxonomySession = TaxonomySession.GetTaxonomySession(sourceClientContext);
            TermStore sourceTermStore = sourceTaxonomySession.GetDefaultKeywordsTermStore();
            sourceClientContext.Load(sourceTermStore,
                                            store => store.Name,
                                            store => store.DefaultLanguage,
                                            store => store.Languages,
                                            store => store.Groups.Include(group => group.Name, group => group.Id));
            sourceClientContext.ExecuteQuery();

```

<span data-ttu-id="451d9-162">Im nächsten Schritt werden Änderungen durch Verwenden des **ChangeInformation** -Objekts und Festlegen von das Startdatum für das **ChangeInformation** -Objekt abgerufen.</span><span class="sxs-lookup"><span data-stu-id="451d9-162">Next, it retrieves changes by using the  **ChangeInformation** object, and setting the start date on the **ChangeInformation** object.</span></span> <span data-ttu-id="451d9-163">In diesem Beispiel werden alle Änderungen, die innerhalb des letzten Jahres vorgenommen wurden.</span><span class="sxs-lookup"><span data-stu-id="451d9-163">This example retrieves all changes that were made within the last year.</span></span>

```C#
Log.Internal.TraceInformation((int)EventId.TermStore_GetChangeLog, "Reading the changes");
            ChangeInformation changeInformation = new ChangeInformation(sourceClientContext);
            changeInformation.StartTime = startFrom;
            ChangedItemCollection termStoreChanges = sourceTermStore.GetChanges(changeInformation);
            sourceClientContext.Load(termStoreChanges);
            sourceClientContext.ExecuteQuery();

```

<span data-ttu-id="451d9-164">Die **GetChanges** -Methode gibt eine **ChangedItemCollection**, die alle Änderungen, die in der Terminologiespeicher auftreten auflistet, wie im folgenden Codebeispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="451d9-164">The  **GetChanges** method returns a **ChangedItemCollection**, which enumerates all changes occurring in the term store, as shown in the following code example.</span></span> <span data-ttu-id="451d9-165">Die letzte Zeile des Beispiels überprüft, um festzustellen, ob die **etwa ChangedItem** einer Begriffsgruppe wurde.</span><span class="sxs-lookup"><span data-stu-id="451d9-165">The last line of the example checks to determine whether the  **ChangedItem** was a term group.</span></span> <span data-ttu-id="451d9-166">**ProcessChanges** enthält Code zum Ausführen von ähnlicher Prüfungen auf die **etwa ChangedItem** für Ausdruckssätze und Ausdrücke.</span><span class="sxs-lookup"><span data-stu-id="451d9-166">**ProcessChanges** includes code to perform similar checks on the **ChangedItem** for term sets and terms.</span></span>

```C#
foreach (ChangedItem _changeItem in termStoreChanges)
                {
                    
                    if (_changeItem.ChangedTime < startFrom)
                    {
                        Log.Internal.TraceVerbose((int)EventId.TermStore_SkipChangeLogEntry, "Skipping item {1} changed at {0}", _changeItem.ChangedTime, _changeItem.Id);
                        continue;
                    }

                    Log.Internal.TraceVerbose((int)EventId.TermStore_ProcessChangeLogEntry, "Processing item {1} changed at {0}. Operation = {2}, ItemType = {3}", _changeItem.ChangedTime, _changeItem.Id, _changeItem.Operation, _changeItem.ItemType);

                    #region Group changes
                    if (_changeItem.ItemType == ChangedItemType.Group)

```

<span data-ttu-id="451d9-167">Der Elementtyp des geänderten möglicherweise einer Begriffsgruppe, Ausdruckssatz oder Begriff.</span><span class="sxs-lookup"><span data-stu-id="451d9-167">The changed item type might be a term group, term set, or term.</span></span> <span data-ttu-id="451d9-168">Jeder geänderte Element hat sich verschiedene Vorgänge, die darauf ausgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="451d9-168">Each changed item type has different operations you can perform on it.</span></span> <span data-ttu-id="451d9-169">Die folgende Tabelle enthält die Vorgänge, die Sie für jede geänderte Elementtyp ausführen können.</span><span class="sxs-lookup"><span data-stu-id="451d9-169">The following table lists the operations that you can perform on each changed item type.</span></span> 

|<span data-ttu-id="451d9-170">Was geändert?</span><span class="sxs-lookup"><span data-stu-id="451d9-170">What changed?</span></span> <span data-ttu-id="451d9-171">(ChangedItemType)</span><span class="sxs-lookup"><span data-stu-id="451d9-171">(ChangedItemType)</span></span> | <span data-ttu-id="451d9-172">Vorgänge können Sie mit der geänderten Elementtyp (ChangedOperationType) ausführen.</span><span class="sxs-lookup"><span data-stu-id="451d9-172">Operations you can perform on changed item type (ChangedOperationType)</span></span>|
|---|---|
|<span data-ttu-id="451d9-173">Gruppe</span><span class="sxs-lookup"><span data-stu-id="451d9-173">Group</span></span>|<p><span data-ttu-id="451d9-174">Gruppe löschen</span><span class="sxs-lookup"><span data-stu-id="451d9-174">Delete group</span></span></p><p><span data-ttu-id="451d9-175">Gruppe hinzufügen</span><span class="sxs-lookup"><span data-stu-id="451d9-175">Add group</span></span></p><p><span data-ttu-id="451d9-176">Gruppe bearbeiten</span><span class="sxs-lookup"><span data-stu-id="451d9-176">Edit group</span></span>|
|<span data-ttu-id="451d9-177">TermSet</span><span class="sxs-lookup"><span data-stu-id="451d9-177">TermSet</span></span>|</p><span data-ttu-id="451d9-178">Ausdruckssatz löschen</span><span class="sxs-lookup"><span data-stu-id="451d9-178">Delete term set</span></span></p><p><span data-ttu-id="451d9-179">Ausdruckssatz verschieben</span><span class="sxs-lookup"><span data-stu-id="451d9-179">Move term set</span></span></p><p><span data-ttu-id="451d9-180">Ausdruckssatz kopieren</span><span class="sxs-lookup"><span data-stu-id="451d9-180">Copy term set</span></span></p><p><span data-ttu-id="451d9-181">Hinzufügen von Ausdruckssatz</span><span class="sxs-lookup"><span data-stu-id="451d9-181">Add term set</span></span></p><p><span data-ttu-id="451d9-182">Bearbeiten von Ausdruckssatz</span><span class="sxs-lookup"><span data-stu-id="451d9-182">Edit term set</span></span><p>|
|<span data-ttu-id="451d9-183">Begriff</span><span class="sxs-lookup"><span data-stu-id="451d9-183">Term</span></span>|</p><span data-ttu-id="451d9-184">Begriff löschen</span><span class="sxs-lookup"><span data-stu-id="451d9-184">Delete term</span></span></p><p><span data-ttu-id="451d9-185">Ausdruck verschieben</span><span class="sxs-lookup"><span data-stu-id="451d9-185">Move term</span></span></p><p><span data-ttu-id="451d9-186">Ausdruck kopieren</span><span class="sxs-lookup"><span data-stu-id="451d9-186">Copy term</span></span></p><p><span data-ttu-id="451d9-187">Pfad ändern Begriff</span><span class="sxs-lookup"><span data-stu-id="451d9-187">Path change term</span></span></p><p><span data-ttu-id="451d9-188">Zusammenführen von Begriff</span><span class="sxs-lookup"><span data-stu-id="451d9-188">Merge term</span></span></p><p><span data-ttu-id="451d9-189">Begriff hinzufügen</span><span class="sxs-lookup"><span data-stu-id="451d9-189">Add term</span></span></p><p><span data-ttu-id="451d9-190">Begriff bearbeiten</span><span class="sxs-lookup"><span data-stu-id="451d9-190">Edit term</span></span><p>|

<span data-ttu-id="451d9-191">Der folgende Code zeigt, wie Sie einen Löschvorgang auszuführen, wenn einer Begriffsgruppe in der Quelle verwalteten Metadatendienst gelöscht wurde.</span><span class="sxs-lookup"><span data-stu-id="451d9-191">The following code shows how to perform a delete operation when a term group was deleted in the source managed metadata service.</span></span>

```C#
#region Delete group
                        if (_changeItem.Operation == ChangedOperationType.DeleteObject)
                        {
                            TermGroup targetTermGroup = targetTermStore.GetGroup(_changeItem.Id);
                            targetClientContext.Load(targetTermGroup, group => group.Name);
                            targetClientContext.ExecuteQuery();

                            if (!targetTermGroup.ServerObjectIsNull.Value)
                            {
                                if (termGroupExclusions == null || !termGroupExclusions.Contains(targetTermGroup.Name, StringComparer.InvariantCultureIgnoreCase))
                                {
                                    Log.Internal.TraceInformation((int)EventId.TermGroup_Delete, "Deleting group: {0}", targetTermGroup.Name);
                                    targetTermGroup.DeleteObject();
                                    targetClientContext.ExecuteQuery();
                                }
                            }
                        }
                        #endregion

```

## <a name="see-also"></a><span data-ttu-id="451d9-192">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="451d9-192">See also</span></span>
<span data-ttu-id="451d9-193"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="451d9-193"></span></span>

-  [<span data-ttu-id="451d9-194">Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="451d9-194">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="451d9-195">OfficeDevPnP.Core-Beispiel</span><span class="sxs-lookup"><span data-stu-id="451d9-195">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core)
    
-  [<span data-ttu-id="451d9-196">Core.MMS-Beispiel</span><span class="sxs-lookup"><span data-stu-id="451d9-196">Core.MMS sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS)
