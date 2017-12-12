---
title: "Synchronisieren Sie-add-in für SharePoint-Gruppen Beispiel Begriff"
ms.date: 11/03/2017
ms.openlocfilehash: 4d78f316ad42639db4e8932515c574d867d421fc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="synchronize-term-groups-sample-add-in-for-sharepoint"></a>Synchronisieren Sie-add-in für SharePoint-Gruppen Beispiel Begriff

Als Teil Ihrer Strategie für die Enterprise Content Management (ECM) können Sie über mehrere SharePoint-Terminologiespeicher ausdrucksgruppen synchronisieren.
    
_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Das [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) -Beispiel veranschaulicht das ein vom Anbieter gehosteten add-in mit eine Taxonomie Quell- und synchronisiert werden. Dieses Add-in synchronisiert zwei Terminologiespeicher in den verwalteten Metadatendienst - Quelle und ein Ziel Terminologiespeicher. Die folgenden Objekte dienen zum Synchronisieren von ausdrucksgruppen:

- **TermStore** 

- **ChangeInformation** 

Verwenden Sie diese Lösung, wenn Folgendes auf Sie zutrifft:

- Synchronisieren von zwei Taxonomien. Beispielsweise können Sie SharePoint Online und SharePoint Server 2013 lokal für verschiedene Datenmengen, aber sie verwenden die gleiche Taxonomie.
    
- Synchronisieren von Änderungen an einer bestimmten Begriffsgruppe nur.

## <a name="before-you-begin"></a>Bevor Sie beginnen:
<a name="sectionSection0"> </a>

Laden Sie Sie zuerst [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Bevor Sie dieses Add-in ausführen, benötigen Sie über die Berechtigung zum Zugriff auf den Terminologiespeicher in den verwalteten Metadatendienst. Abbildung 1 zeigt das Office 365 Administrationscenter, wo diese Berechtigungen zugewiesen werden.

**Abbildung 1. Zuweisen von Berechtigungen auf den Ausdruck speichern, in der SharePoint-Verwaltungskonsole**

![Screenshot zeigt, dass dem SharePoint-Administrator zentrieren, mit dem Terminologiespeicher Taxonomie Begriff Store Suchfeld und die Begriff Store Administratoren Feldern hervorgehoben.](media/93a19898-6ae2-4176-b030-2546f4c86c5c.png)

Zuweisen von Berechtigungen auf den Terminologiespeicher

1. Wählen Sie das Office 365 Administrationscenter **Ausdruck zu speichern**.
    
2. Wählen Sie im **TAXONOMIETERMINOLOGIESPEICHER**den Ausdruckssatz, dass Sie ein Administrator zuweisen möchten.
    
3. Geben Sie im **Ausdruck speichern Administratoren**die organisationskonto, die Berechtigungen für Administrator den Begriff erforderlich sind.

## <a name="using-the-coremmssync-sample-app"></a>Verwenden die Core.MMSSync Beispiel-app
<a name="sectionSection1"> </a>

Wenn Sie das Add-in starten, sehen Sie eine Konsolenanwendung, wie in Abbildung 2 dargestellt. Sie werden aufgefordert, die folgenden Informationen eingeben:

- Die URL des im Office 365 Administrationscenter, das die Quelle Terminologiespeicher enthält (Dies ist die URL für den Metadatendienst managed Quell). Geben Sie zum Beispiel https://contososource-admin.sharepoint.com ein.
    
- Den Benutzernamen und das Kennwort eines laufzeitspeicheradministrators auf Ihre Datenquelle verwalteter Metadatendienst.
    
- Die URL der Menüschaltfläche 365 Administrationscenter, die den Begriff Zielspeicher enthält (Dies ist die URL des Ziels MMS). Geben Sie zum Beispiel https://contosotarget-admin.sharepoint.com ein.
    
- Den Benutzernamen und das Kennwort eines laufzeitspeicheradministrators auf Ihrer Ziel verwalteter Metadatendienst.
    
- Den Typ des Vorgangs, die Sie ausführen möchten. Sie können:
    
    - Verschieben einer Begriffsgruppe (Szenario 1) mithilfe des **TermStore** -Objekts.
    
    - Process Changes (Szenario 2) mithilfe des **ChangeInformation** -Objekts.

**Wichtige**  In diesem Beispiel-add-in funktioniert mit beiden SharePoint Online und SharePoint Server 2013 lokal.

**Abbildung 2. Core.MMSSync Konsolenanwendung**

![Screenshot der Konsole Anwendung anfordern von Informationen eingegeben werden.](media/1ef0e4f4-6f79-46b0-83d3-bdf9d87ccad9.png)

Nachdem Sie Ihr Szenario ausgewählt haben, geben Sie den Namen der Begriffsgruppe, den, die Sie aus der Quelle zu Ihrer Ziel verwalteten Metadatendienst synchronisieren, wie in Abbildung 3 dargestellt möchten. Geben Sie zum Beispiel Enterprise ein.

**Abbildung 3. Begriff Gruppen in den verwalteten Metadatendienst**

![Screenshot der Taxonomie Begriff Store Dropdown-Liste.](media/5202fd88-4f2f-4b68-8083-165e6702bc86.png)
### <a name="scenario-1---move-term-group"></a>Szenario 1 – Begriffsgruppe verschieben

Bei der Auswahl **Begriffsgruppe verschieben**des Add-Ins werden Sie aufgefordert, geben Sie eine Term-Gruppe zum Synchronisieren und ruft dann die **CopyNewTermGroups** -Methode in MMSSyncManager.cs. **CopyNewTermGroups** führt dann Folgendes ein, um eine Begriffsgruppe aus dem Terminologiespeicher Quelle auf den Terminologiespeicher Ziel kopieren:

1. Ruft die Quell- und Ziel-Begriff Objekte gespeichert.
    
2. Stellt sicher, dass die Sprachen des Ausdrucks Quell- und speichert die Übereinstimmung. 
    
3. Überprüft, ob die Quelle Begriffsgruppe nicht im Terminologiespeicher Ziel vorhanden ist, und klicken Sie dann die Quelle Begriffsgruppe auf den Terminologiespeicher Ziel mithilfe von **CreateNewTargetTermGroup**kopiert. 
    
Sie können die Parameter _TermGroupExclusions_, _TermGroupToCopy_und _TermSetInclusions_ gefiltert, welche Begriffe verarbeitet festlegen.

Im folgenden Codebeispiel wird die Verwendung der Methods **CopyNewTermGroups** und **CreateNewTargetTermGroup** MMSSyncManager.cs.

> [!NOTE] 
> Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

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

### <a name="scenario-2---process-changes"></a>Szenario 2: Änderungen an

Bei der Auswahl von **Änderungen an**das Add-in werden Sie aufgefordert, geben Sie einen Begriff Gruppe zum Synchronisieren, und klicken Sie dann die **ProcessChanges** -Methode in MMSSyncManager.cs. **ProcessChanges** verwendet die **GetChanges** -Methode der **ChangedInformation** -Klasse, um alle Änderungen an Gruppen, Ausdruckssätze und Ausdrücke in der Quelle verwalteten Metadatendienst abzurufen. Änderungen werden klicken Sie dann auf das Ziel verwalteten Metadatendienst angewendet.

> [!NOTE] 
> Dieses Dokument enthält nur einige Teile der **ProcessChanges** -Methode. Um die gesamte Methode zu überprüfen, öffnen Sie die Core.MMSSync-Lösung in Visual Studio.

Die **ProcessChanges** -Methode startet, indem Sie ein **TaxonomySession** -Objekt zu erstellen.

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

Im nächsten Schritt werden Änderungen durch Verwenden des **ChangeInformation** -Objekts und Festlegen von das Startdatum für das **ChangeInformation** -Objekt abgerufen. In diesem Beispiel werden alle Änderungen, die innerhalb des letzten Jahres vorgenommen wurden.

```C#
Log.Internal.TraceInformation((int)EventId.TermStore_GetChangeLog, "Reading the changes");
            ChangeInformation changeInformation = new ChangeInformation(sourceClientContext);
            changeInformation.StartTime = startFrom;
            ChangedItemCollection termStoreChanges = sourceTermStore.GetChanges(changeInformation);
            sourceClientContext.Load(termStoreChanges);
            sourceClientContext.ExecuteQuery();

```

Die **GetChanges** -Methode gibt eine **ChangedItemCollection**, die alle Änderungen, die in der Terminologiespeicher auftreten auflistet, wie im folgenden Codebeispiel dargestellt. Die letzte Zeile des Beispiels überprüft, um festzustellen, ob die **etwa ChangedItem** einer Begriffsgruppe wurde. **ProcessChanges** enthält Code zum Ausführen von ähnlicher Prüfungen auf die **etwa ChangedItem** für Ausdruckssätze und Ausdrücke.

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

Der Elementtyp des geänderten möglicherweise einer Begriffsgruppe, Ausdruckssatz oder Begriff. Jeder geänderte Element hat sich verschiedene Vorgänge, die darauf ausgeführt werden können. Die folgende Tabelle enthält die Vorgänge, die Sie für jede geänderte Elementtyp ausführen können. 

|Was geändert? (ChangedItemType) | Vorgänge können Sie mit der geänderten Elementtyp (ChangedOperationType) ausführen.|
|---|---|
|Gruppe|<p>Gruppe löschen</p><p>Gruppe hinzufügen</p><p>Gruppe bearbeiten|
|TermSet|</p>Ausdruckssatz löschen</p><p>Ausdruckssatz verschieben</p><p>Ausdruckssatz kopieren</p><p>Hinzufügen von Ausdruckssatz</p><p>Bearbeiten von Ausdruckssatz<p>|
|Begriff|</p>Begriff löschen</p><p>Ausdruck verschieben</p><p>Ausdruck kopieren</p><p>Pfad ändern Begriff</p><p>Zusammenführen von Begriff</p><p>Begriff hinzufügen</p><p>Begriff bearbeiten<p>|

Der folgende Code zeigt, wie Sie einen Löschvorgang auszuführen, wenn einer Begriffsgruppe in der Quelle verwalteten Metadatendienst gelöscht wurde.

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

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Enterprise Content Management-Lösungen für SharePoint 2013 und SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [OfficeDevPnP.Core-Beispiel](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core)
    
-  [Core.MMS-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS)
