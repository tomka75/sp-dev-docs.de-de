---
title: Verwaltete Metadaten und Navigation in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b66d4ec1-a2ef-49cc-8ca5-a6b516bff02e
ms.openlocfilehash: 3da23b3b9d628188322c876094c616a4c0a8a0cb
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="managed-metadata-and-navigation-in-sharepoint"></a><span data-ttu-id="ab2b2-102">Verwaltete Metadaten und Navigation in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ab2b2-102">Managed metadata and navigation in SharePoint</span></span>

  
    
    
![Konzeptuelles Übersichtsthema](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="ab2b2-104">Informationen über verwaltete Metadaten von Unternehmen (EMM) und Navigationsfunktionen in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-104">Learn about enterprise managed metadata (EMM) and navigation features in SharePoint.</span></span>
## <a name="managed-metadata-feature-enhancements-in-sharepoint-for-developers"></a><span data-ttu-id="ab2b2-105">Funktionsverbesserungen für verwaltete Metadaten in SharePoint für Entwickler</span><span class="sxs-lookup"><span data-stu-id="ab2b2-105">Managed metadata feature enhancements in SharePoint for developers</span></span>
<span data-ttu-id="ab2b2-106"><a name="SP15_ManagedMetadataAndNav_ManagedMetadataFeatureEnhancements"> </a></span><span class="sxs-lookup"><span data-stu-id="ab2b2-106"><a name="SP15_ManagedMetadataAndNav_ManagedMetadataFeatureEnhancements"> </a></span></span>

<span data-ttu-id="ab2b2-p101">Mit verwalteten Metadaten können Sie Taxonomien erstellen und Strategien markieren, die bestimmten Geschäftsanforderungen entsprechen. In SharePoint wurde der grundlegende verwaltete Metadaten-API-Satz erweitert und verbessert, um mehr Funktionen bereitzustellen und mehr Szenarien zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-p101">You can use managed metadata to build taxonomies and tagging strategies that meet specific, detailed business needs. In SharePoint, the basic managed metadata API set is expanded and enhanced to provide more capabilities and scenario support.</span></span>
  
    
    

## <a name="net-client-object-model-csom-support-for-managed-metadata-apis"></a><span data-ttu-id="ab2b2-109">Unterstützung vom .NET-Clientobjektmodell für verwaltete Metadaten-APIs</span><span class="sxs-lookup"><span data-stu-id="ab2b2-109">.NET client object model (CSOM) support for managed metadata APIs</span></span>
<span data-ttu-id="ab2b2-110"><a name="SP15_ManagedMetadataAndNav_CSOMSupport"> </a></span><span class="sxs-lookup"><span data-stu-id="ab2b2-110"><a name="SP15_ManagedMetadataAndNav_CSOMSupport"> </a></span></span>

<span data-ttu-id="ab2b2-p102">Das SharePoint-Clientobjektmodell unterstützt das Anpassen und Erstellen von Taxonomien. Taxonomie steht im .NET-Clientobjektmodell, in Silverlight und in JavaScript-Programmiermodellen zur Verfügung. Die Entwicklung mit diesem ähnelt der Entwicklung mit dem .NET-Serverprogrammiermodell. Möglicherweise möchten Sie Clientobjektmodell-Lösungen zur Unterstützung von Szenarien entwickeln, in denen das Lesen von Inhalten häufiger auftritt, als das Erstellen oder Verwalten von diesen. Sie müssen das Clientobjektmodell verwenden, um die Verwendung von Taxonomie in einem cloudbasierten Szenario wie SharePoint Online oder für eine Teilmenge von Szenarien zu aktivieren, die lokal verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-p102">The SharePoint CSOM supports taxonomy customization and development. Taxonomy is available in .NET client (CSOM), Silverlight, and JavaScript programming models. Developing with it is logically similar to developing with the .NET server programming model. You may find it useful to develop CSOM solutions to support scenarios where reading content is more common than authoring or administering it. You need to use CSOM to enable taxonomy use in a cloud scenario like SharePoint Online or for a subset of scenarios that are available on premises.</span></span>
  
    
    
<span data-ttu-id="ab2b2-116">Wenn Sie ein neues Clientobjektmodell-Projekt in Visual Studio erstellen möchten, in dem die Taxonomiefunktion verwendet wird, legen Sie die folgenden Verweise fest:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-116">When you want to create a new CSOM project in Visual Studio that uses taxonomy functionality, set the following references:</span></span>
  
    
    

- <span data-ttu-id="ab2b2-117">Microsoft.SharePoint.Client.dll</span><span class="sxs-lookup"><span data-stu-id="ab2b2-117">Microsoft.SharePoint.Client.dll</span></span>
    
  
- <span data-ttu-id="ab2b2-118">Microsoft.SharePoint.Client.Runtime.dll</span><span class="sxs-lookup"><span data-stu-id="ab2b2-118">Microsoft.SharePoint.Client.Runtime.dll</span></span>
    
  
- <span data-ttu-id="ab2b2-119">Microsoft.SharePoint.Client.Taxonomy.dll</span><span class="sxs-lookup"><span data-stu-id="ab2b2-119">Microsoft.SharePoint.Client.Taxonomy.dll</span></span>
    
  
<span data-ttu-id="ab2b2-120">Die Entwicklung von Anpassungen mit dem Clientobjektmodell ähnelt weitestgehend der Entwicklung von .NET-Servertaxonomielösungen: Informationen zum **TaxonomySession**- und **TermStore**-Objekt, zu **Group**-, **TermSet**- und **Term**-Objekten, die für die Sitzung erforderlich sind.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-120">Developing customizations with CSOM is very similar to developing .NET server taxonomy solutions: get a reference to the **TaxonomySession** object and the **TermStore** object, **Group** objects, **TermSet** objects, and **Term** objects required for the session.</span></span>
  
    
    

### <a name="code-examples-basic-operations-with-the-taxonomy-csom"></a><span data-ttu-id="ab2b2-121">Codebeispiele: Grundlegende Vorgänge mit dem Taxonomie-Clientobjektmodell</span><span class="sxs-lookup"><span data-stu-id="ab2b2-121">Code Examples: Basic operations with the Taxonomy CSOM</span></span>
<span data-ttu-id="ab2b2-122"><a name="SP15_ManagedMetadataAndNav_ExampleBasicOperations"> </a></span><span class="sxs-lookup"><span data-stu-id="ab2b2-122"><a name="SP15_ManagedMetadataAndNav_ExampleBasicOperations"> </a></span></span>

<span data-ttu-id="ab2b2-p103">Mit den folgenden Codebeispielen können Sie grundlegende Vorgänge mit dem Taxonomie-Clientobjektmodell abschließen. Im ersten Beispiel werden ein **Group**- Objekt, ein **TermSet**-Objekt und **Term**-Objekte erstellt. Im zweiten Beispiel wird ein **Group**-Objekt durchlaufen und seine Inhalte werden geschrieben.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-p103">You can use the following code examples to complete basic operations with the taxonomy CSOM. The first example creates a **Group** object, a **TermSet** object, and **Term** objects. The second example iterates on a **Group** object and writes its contents.</span></span>
  
    
    

```cs

       private void CreateColorsTermSet(string siteUrl)
        {
           ClientContext clientContext = new ClientContext(siteUrl);
 
           TaxonomySession taxonomySession = TaxonomySession.GetTaxonomySession(clientContext);
            clientContext.Load(taxonomySession,
                ts => ts.TermStores.Include(
                    store => store.Name,
                    store => store.Groups.Include(
                        group => group.Name
                        )
                    )
                );
            clientContext.ExecuteQuery();
 
           if( taxonomySession != null )
            {
               TermStore termStore = taxonomySession.GetDefaultSiteCollectionTermStore();
               if (termStore != null)
                {
                   //
                   //  Create group, termset, and terms.
                   //
                   TermGroup myGroup = termStore.CreateGroup("MyGroup",Guid.NewGuid());
                   TermSet myTermSet = myGroup.CreateTermSet("Color",Guid.NewGuid(), 1033);
                    myTermSet.CreateTerm("Red", 1033,Guid.NewGuid());
                    myTermSet.CreateTerm("Orange", 1033,Guid.NewGuid());
                    myTermSet.CreateTerm("Yellow", 1033,Guid.NewGuid());
                    myTermSet.CreateTerm("Green", 1033,Guid.NewGuid());
                    myTermSet.CreateTerm("Blue", 1033,Guid.NewGuid());
                    myTermSet.CreateTerm("Purple", 1033,Guid.NewGuid());
 
                    clientContext.ExecuteQuery();
                }
            }
        }
 
       private void DumpTaxonomyItems(string siteUrl)
        {
           ClientContext clientContext = new ClientContext(siteUrl);
 
           //
           // Load up the taxonomy item names.
           //
            TaxonomySession taxonomySession =TaxonomySession.GetTaxonomySession(clientContext);
           TermStore termStore = taxonomySession.GetDefaultSiteCollectionTermStore();
            clientContext.Load(termStore,
                    store => store.Name,
                    store => store.Groups.Include(
                        group => group.Name,
                        group => group.TermSets.Include(
                            termSet => termSet.Name,
                            termSet => termSet.Terms.Include(
                                term => term.Name)
                        )
                    )
            );
            clientContext.ExecuteQuery();
 
 
           //
           //Writes the taxonomy item names.
           //
           if( taxonomySession != null )
            {
               if (termStore != null)
                {
                   foreach( TermGroup groupin termStore.Groups)
                    {
                       Console.WriteLine("Group " + group.Name);
 
                       foreach( TermSet termSetin group.TermSets )
                        {
                           Console.WriteLine("TermSet " + termSet.Name);
 
                            foreach(Term term in termSet.Terms)
                            {
                               //Writes root-level terms only.
                               Console.WriteLine("Term " + term.Name);
                            }
                        }
                    }
                }
            }
 
        }

```


  
    
    

## <a name="pinning"></a><span data-ttu-id="ab2b2-126">Anheften</span><span class="sxs-lookup"><span data-stu-id="ab2b2-126">Pinning</span></span>
<span data-ttu-id="ab2b2-127"><a name="SP15_ManagedMetadataAndNav_Pinning"> </a></span><span class="sxs-lookup"><span data-stu-id="ab2b2-127"><a name="SP15_ManagedMetadataAndNav_Pinning"> </a></span></span>

<span data-ttu-id="ab2b2-p104">In Microsoft SharePoint Server 2010konnten Benutzer Ausdrücke (und alle innerhalb des wiederverwendeten Ausdrucks verschachtelten Ausdrücke) an anderen Stellen in der Ausdruckshierarchie wiederverwendet werden. Wenn diese Ausdrücke nach Wiederverwendung geändert wurden, wurden die Änderungen an allen Stellen übernommen, wo diese wiederverwendet wurden. In SharePoint wurde das Anheften von Ausdrücken eingeführt. Ein angehefteter Ausdruck entspricht einem wiederverwendeten Ausdruck mit der Ausnahme, dass er schreibgeschützt ist und nicht an den Stellen geändert werden kann, an denen er wiederverwendet wird. Ein Beispiel hierzu finden Sie unter  [Vorgehensweise: Verwendung Code Pin Bedingungen Navigation Begriff wird im SharePoint](how-to-use-code-to-pin-terms-to-navigation-term-sets-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="ab2b2-p104">In Microsoft SharePoint Server 2010, users could reuse terms (and all terms nested under the reused terms) in other locations in the term hierarchy. After these terms were reused, they could be modified and changes would be seen everywhere the terms were reused. SharePoint introduces term pinning. A pinned term is just like a term that is reused, except it is read only and cannot be changed in the locations where the term is reused. For an example, see  [How to: Use code to pin terms to navigation term sets in SharePoint](how-to-use-code-to-pin-terms-to-navigation-term-sets-in-sharepoint.md).</span></span>
  
    
    

  
    
    

## <a name="datasheet-view-support-for-managed-metadata-column-types"></a><span data-ttu-id="ab2b2-133">Unterstützung für die Datenblattansicht für verwaltete Metadaten-Spaltentypen</span><span class="sxs-lookup"><span data-stu-id="ab2b2-133">Datasheet view support for managed metadata column types</span></span>
<span data-ttu-id="ab2b2-134"><a name="SP15_ManagedMetadataAndNav_DatasheetViewSupport"> </a></span><span class="sxs-lookup"><span data-stu-id="ab2b2-134"><a name="SP15_ManagedMetadataAndNav_DatasheetViewSupport"> </a></span></span>

<span data-ttu-id="ab2b2-p105">In SharePoint wurde die Datenblatt-Ansichtsfunktion geändert. Die Standardansicht für die Rasterbearbeitung wird nun mit einem Doppelklick auf die Aktion geöffnet werden. Metadatenspalten können mit den gleichen Funktionen wie beim Bearbeiten von einzelnen Elementen bearbeitet werden. Dies umfasst den Zugriff auf den Ausdruckssatz hinter der Spalte. Bei dieser Funktion geht es um Funktionen zur Metadatenänderung, die beim Bearbeiten eines einzelnen Elements für die Datenblattbearbeitung zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-p105">In SharePoint, the datasheet view functionality has changed. Now, the datasheet uses a double-click action to open standard view for grid editing. You can now edit metadata columns using the same features that are available when you edit individual items. This includes access to the term set that is behind the column. This feature is all about bringing the metadata modification functionality available when editing an individual item to datasheet editing.</span></span>
  
    
    

## <a name="managed-navigation"></a><span data-ttu-id="ab2b2-140">Verwaltete Navigation</span><span class="sxs-lookup"><span data-stu-id="ab2b2-140">Managed navigation</span></span>
<span data-ttu-id="ab2b2-141"><a name="SP15_ManagedMetadataAndNav_ManagedNav"> </a></span><span class="sxs-lookup"><span data-stu-id="ab2b2-141"><a name="SP15_ManagedMetadataAndNav_ManagedNav"> </a></span></span>

<span data-ttu-id="ab2b2-p106">Die verwaltete Navigation umfasst verwaltete Metadatenfunktionen wie das Anheften von Elementen an Ausdrücke und das Verwalten von Ausdrücken in einem Ausdrucksspeicher zur Bereitstellung einer in hohem Maße angepassten Websitenavigation. Die strukturierte Navigation, die von der SharePoint-Infrastruktur abhängt, ist in SharePoint weiterhin verfügbar.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-p106">Managed navigation uses managed metadata features, such as the ability to tag items with terms and manage terms in a term store, to provide highly customized site navigation. The structured navigation that depends on the SharePoint infrastructure is also still available in SharePoint.</span></span>
  
    
    

## <a name="friendly-urls"></a><span data-ttu-id="ab2b2-144">Benutzerfreundliche URLs</span><span class="sxs-lookup"><span data-stu-id="ab2b2-144">Friendly URLs</span></span>
<span data-ttu-id="ab2b2-145"><a name="SP15_ManagedMetadataAndNav_FriendlyURLs"> </a></span><span class="sxs-lookup"><span data-stu-id="ab2b2-145"><a name="SP15_ManagedMetadataAndNav_FriendlyURLs"> </a></span></span>

<span data-ttu-id="ab2b2-p107">Benutzerfreundliche URLs stellen ein kürzeres URL-Format dar, das in der Adressleiste der meisten SharePoint-Veröffentlichungsseiten angezeigt wird, einschließlich der Willkommensseite Ihrer Website. Sie sind SEO-freundlich und werden in Suchergebnissen angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-p107">Friendly URLs are a shorter URL format displayed in the address bar of most SharePoint publishing pages, including the Welcome Page of your site. They are SEO-friendly and appear in search results.</span></span> 
  
    
    

## <a name="support-for-new-scenarios"></a><span data-ttu-id="ab2b2-148">Unterstützung für neue Szenarien</span><span class="sxs-lookup"><span data-stu-id="ab2b2-148">Support for new scenarios</span></span>
<span data-ttu-id="ab2b2-149"><a name="SP15_ManagedMetadataAndNav_SupportForNewScenarios"> </a></span><span class="sxs-lookup"><span data-stu-id="ab2b2-149"><a name="SP15_ManagedMetadataAndNav_SupportForNewScenarios"> </a></span></span>

<span data-ttu-id="ab2b2-150">Mit dem Ausdrucksspeicher-Manager können Ausdrucksverwendungsmodelle, die auf flexibleren und leistungsstärkeren verwalteten Metadatenfunktionen in basieren, verbessert und erweitert werden:</span><span class="sxs-lookup"><span data-stu-id="ab2b2-150">A term store manager can enhance and expand term usage models based on more flexible and powerful managed metadata functionality in :</span></span>
  
    
    

- <span data-ttu-id="ab2b2-p108">Verweisen auf eine andere Websitesammlung und Anzeigen von Ausdrücken von anderen Benutzern.Wenn Sie Ihren Ausdruckssatz für andere mit dem verwalteten Metadatendienst verknüpften Websitesammlungen zur Verfügung stellen möchten, erstellen Sie ein **global term set**. Wenn Sie einen privaten Ausdruckssatz erstellen möchten, der nur für eine bestimmte Websitesammlung zur Verfügung steht, wenn er im verwalteten Metadatendienst gespeichert ist, erstellen Sie ein **local term set**.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-p108">Link to another site collection and view others' terms. If you want to make your term set available to other site collections connected to the managed metadata service, create a **global term set**. If you want to create a private term set that is available only to a specific site collection when it is stored in the managed metadata service, create a **local term set**.</span></span> 
    
  
- <span data-ttu-id="ab2b2-154">Das Verwenden von Schlüsselwörtern außerhalb eines bestimmten Ausdruckssatzes für Benutzer blockieren.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-154">Block users from using keywords outside of a specific term set.</span></span>
    
  
- <span data-ttu-id="ab2b2-155">Zusätzliche, mehrsprachige Unterstützung, darunter Unterstützung für automatisierte Übersetzung und flexible LCIDs.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-155">Gain additional multilingual support, including support for automated translation and flexible LCIDs.</span></span> 
    
  

## <a name="unsupported-scenarios-for-working-with-custom-site-definitions"></a><span data-ttu-id="ab2b2-156">Nicht unterstützte Szenarien für das Arbeiten mit benutzerdefinierten Websitedefinitionen</span><span class="sxs-lookup"><span data-stu-id="ab2b2-156">Unsupported scenarios for working with custom site definitions</span></span>
<span data-ttu-id="ab2b2-157"><a name="SP15_ManagedMetadataAndNav_UnsupportedScenarios"> </a></span><span class="sxs-lookup"><span data-stu-id="ab2b2-157"><a name="SP15_ManagedMetadataAndNav_UnsupportedScenarios"> </a></span></span>


- <span data-ttu-id="ab2b2-158">In SharePoint wird das Erstellen von Taxonomiefeldern (verwalteten Metadaten-Websitespalten) mithilfe einer XML-Definition nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-158">SharePoint does not support creating taxonomy fields (managed metadata site columns) declaratively by way of XML definition.</span></span>
    
  
- <span data-ttu-id="ab2b2-159">In SharePoint wird das Verwenden von Taxonomiefeldern (verwalteten Metadaten-Websitespalten) in Websitevorlagen nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="ab2b2-159">SharePoint does not support the use of taxonomy fields (managed metadata site columns) in site templates.</span></span>
    
  
- <span data-ttu-id="ab2b2-160">Weitere Informationen finden Sie im Microsoft Support-Artikel #898631:  [Unterstützte und nicht unterstütze Szenarien](http://support2.microsoft.com/default.aspx?scid=kb;EN-US;898631
)</span><span class="sxs-lookup"><span data-stu-id="ab2b2-160">For more information, see Microsoft Support Article #898631:  [Supported and unsupported scenarios](http://support2.microsoft.com/default.aspx?scid=kb;EN-US;898631
)</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="ab2b2-161">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ab2b2-161">See also</span></span>
<span data-ttu-id="ab2b2-162"><a name="SP15_ManagedMetadataAndNav_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="ab2b2-162"><a name="SP15_ManagedMetadataAndNav_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="ab2b2-163">Verwaltete Navigation in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ab2b2-163">Managed navigation in SharePoint</span></span>](managed-navigation-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ab2b2-164">Inhaltssuche-Webpart in SharePoint</span><span class="sxs-lookup"><span data-stu-id="ab2b2-164">Content Search Web Part in SharePoint</span></span>](content-search-web-part-in-sharepoint.md)
    
  

