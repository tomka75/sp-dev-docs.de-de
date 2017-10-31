---
title: Verwaltete Navigation in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6dbb9da2d644b6f6f93ea4508616daee7fac321e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="managed-navigation-in-sharepoint"></a><span data-ttu-id="7d70f-102">Verwaltete Navigation in SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d70f-102">Managed navigation in SharePoint</span></span>

  
    
    
![Konzeptuelles Übersichtsthema](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="7d70f-104">Erfahren Sie mehr über das Feature der taxonomiegesteuerten verwalteten Navigation in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d70f-104">Learn about the taxonomy-driven managed navigation feature in SharePoint.</span></span>
## <a name="introducing-managed-navigation"></a><span data-ttu-id="7d70f-105">Einführung in die verwaltete Navigation</span><span class="sxs-lookup"><span data-stu-id="7d70f-105">Introducing managed navigation</span></span>
<span data-ttu-id="7d70f-106"><a name="SP15_ManagedNav_Introducing"> </a></span><span class="sxs-lookup"><span data-stu-id="7d70f-106"><a name="SP15_ManagedNav_Introducing"> </a></span></span>

<span data-ttu-id="7d70f-p101">Eine gut durchdachte Navigation sagt den Benutzern einer Website eine Menge über die Geschäfte, Produkte und Dienste, die auf der Website angeboten werden. Indem sie die Taxonomie hinter der Navigation aktualisieren, können Unternehmen Änderungen vorantreiben und damit Schritt halten, ohne die Websitenavigation während des Vorgangs neu erstellen zu müssen. In SharePoint können Sie mit dem Feature der verwalteten Navigation eine Websitenavigation entwerfen, die durch verwaltete Metadaten gesteuert wird, und SEO-freundliche URLs erstellen, die von der Struktur der verwalteten Navigation abgeleitet werden. Die verwaltete Navigation bietet eine Alternative zum herkömmlichen SharePoint-Navigationsfeature - der strukturierten Navigation -, das auf der Struktur von SharePoint basiert. Da die verwaltete Navigation von der Taxonomie gesteuert wird, können Sie sie verwenden, um eine Websitenavigation um wichtige Geschäftskonzepte herum zu entwerfen, ohne die Struktur Ihrer Websites oder Websitekomponenten ändern zu müssen.</span><span class="sxs-lookup"><span data-stu-id="7d70f-p101">A well-designed navigation tells your site's users a lot about the business, products, and services that the website offers. By updating the taxonomy behind the navigation, businesses can drive and keep up with change without having to recreate their site navigation in the process. In SharePoint, the managed navigation feature enables you to design site navigation that is driven by managed metadata and create SEO-friendly URLs that are derived from the managed navigation structure. Managed navigation provides an alternative to the traditional SharePoint navigation feature—structured navigation—that is based on the structure of SharePoint. Because managed navigation is driven by taxonomy, you can use it to design site navigation around important business concepts without changing the structure of your sites or site components.</span></span>
  
    
    

## <a name="how-managed-navigation-works"></a><span data-ttu-id="7d70f-112">Funktionsweise der verwalteten Navigation</span><span class="sxs-lookup"><span data-stu-id="7d70f-112">How managed navigation works</span></span>
<span data-ttu-id="7d70f-113"><a name="SP15_ManagedNav_HowManagedNavWorks"> </a></span><span class="sxs-lookup"><span data-stu-id="7d70f-113"><a name="SP15_ManagedNav_HowManagedNavWorks"> </a></span></span>

<span data-ttu-id="7d70f-p102">Die verwaltete Navigation bietet ein Framework für dynamisch generierte Seiten und stellt eine dazugehörige SEO-freundliche URL zur Verfügung. Jede generierte Seite wird in der Navigationshierarchie dargestellt. Statt separate Seiten für jede Kategorie in der Taxonomie erstellen zu müssen, bietet das Framework einen Vorlagen- und Vererbungsmechanismus, der die Zielseiten für die einzelnen Navigationslinks erstellt. Sie können das Feature der Themenseiten verwenden, um die Benutzeroberfläche der Zielseiten anzupassen.</span><span class="sxs-lookup"><span data-stu-id="7d70f-p102">Managed navigation provides a framework for dynamically generated pages and provides an associated SEO-friendly URL. Each generated page is represented in the navigation hierarchy. Instead of requiring separate pages to be authored for each category in the taxonomy, the framework provides a templating and inheritance mechanism that creates the landing pages for each navigation link. You can use the topic pages feature to customize the landing page experience.</span></span>
  
    
    
<span data-ttu-id="7d70f-p103">APIs für verwaltete Navigation sind in die Taxonomie- und Veröffentlichungsbibliotheken in SharePoint integriert. Verwaltete Metadatenkomponenten wie Ausdruckssätze und der Terminologiespeicher werden verwendet, um die taxonomiegesteuerte Navigation für Ihre Website zu aktivieren. In der .NET-Serverklassenbibliothek enthält der  [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) -Namespace Ausdrucks-, Ausdruckssatz- und andere Klassenobjekte, die die **Term**-Klasse und die **TermSet**-Klasse im  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) -Navigationsnamespace spiegeln, sodass Methoden und Eigenschaften bereitgestellt werden, die speziell dafür vorgesehen sind, diese Metadatenelemente Navigationselementen zuzuordnen. Mit anderen Klassen wie z. B. [TaxonomySiteMapNode](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.TaxonomySiteMapNode.aspx) können Sie Metadaten mit verschiedenen Navigationselementen für Websites bereitstellen, wie z. B. mit Siteübersichtsknoten und anderen Teile der Websitenavigation. Über andere Klassen kann Zwischenspeicheung und Kontext für die verwalteten Navigation bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="7d70f-p103">Managed navigation APIs are built into the taxonomy and publishing libraries in SharePoint. Managed metadata components like term sets and the term store are used to enable taxonomy-driven navigation for your site. In the .NET server class library, the  [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) namespace contains term, term set, and other class objects that mirror the **Term** class and **TermSet** class in the [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) navigation namespace, providing methods and properties specifically designed to associate those metadata items with navigation elements. Other classes, like [TaxonomySiteMapNode](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.TaxonomySiteMapNode.aspx) , enable you to provide metadata with various site navigation elements, such as site map nodes and other parts of your site's navigation. Other classes enable caching and context for managed navigation.</span></span>
  
    
    
<span data-ttu-id="7d70f-p104">Sie können Links der taxonomiegesteuerten Navigation in der globalen Navigation anzeigen. Die globale Navigation ist eine Navigationsebene mit einer oder mehreren Ebenen, die immer vorhanden ist, häufig am oberen Rand einer Website angezeigt wird und die Inhaltskategorien die obersten Ebene enthält. Sie können diese Links auch im aktuellen Navigationssteuerelement anzeigen, das häufig auf der linken Seite einer Seite zu finden ist. Das aktuelle Navigationssteuerelement stellt die nächste Hierarchieebene für die in der globalen Navigation gewählte Kategorie oder eine Gruppe von Links dar, die zu dieser Kategorie gehören.</span><span class="sxs-lookup"><span data-stu-id="7d70f-p104">You can display taxonomy-driven navigation links in the Global Navigation. The Global Navigation is a navigation layer with one or more layers that's always present, which often appears at the top of a site and displays the top-level content categories. You can also display these links in the current navigation control that often appears on the left side of a page. The current navigation control represents the next level of hierarchy for the category chosen in Global Navigation, or a set of links that belong to that category.</span></span>
  
    
    

## <a name="friendly-urls-and-the-managed-navigation-provider"></a><span data-ttu-id="7d70f-127">Benutzerfreundliche URLs und Anbieter der verwalteten Navigation</span><span class="sxs-lookup"><span data-stu-id="7d70f-127">Friendly URLs and the managed navigation provider</span></span>
<span data-ttu-id="7d70f-128"><a name="SP15_ManagedNav_FriendlyURLs"> </a></span><span class="sxs-lookup"><span data-stu-id="7d70f-128"><a name="SP15_ManagedNav_FriendlyURLs"> </a></span></span>

<span data-ttu-id="7d70f-p105">Wenn Sie zum ersten Mal zu einer SharePoint-Website navigieren, stellen Sie möglicherweise fest, dass sich das URL-Format geändert hat. Statt einer Adresse mit einer  `/Pages/default.aspx`-Erweiterung endet die Seiten-URL nur mit  `/`. Die verwaltete Navigation bietet ein Schema für benutzerfreundliche URLs, das auf allen Website-, Kategorie-, und Elementseiten konsistent ist.</span><span class="sxs-lookup"><span data-stu-id="7d70f-p105">When you browse to a SharePoint site for the first time, you may notice that the URL format has changed. Instead of an address with a  `/Pages/default.aspx` extension, the page URL ends with only `/`. Managed navigation provides a scheme for friendly URLs that is consistent across site, category, and item pages.</span></span>
  
    
    
<span data-ttu-id="7d70f-p106">Dies wird vom Anbieter der verwalteten Navigation möglich gemacht. Wenn Sie zum Stamm einer beliebigen Website navigieren, die den Anbieter der verwalteten Navigation verwendet, steuert die Willkommensseiten-Einstellung der Website die Seite, die im Browser geladen und angezeigt wird; die angezeigte URL (die auch in Suchergebnissen angezeigt wird) wird jedoch in diesem benutzerfreundlicheren Format neu geschrieben.</span><span class="sxs-lookup"><span data-stu-id="7d70f-p106">The managed navigation provider enables this experience. When you navigate to the root of any site that uses the managed navigation provider, the Site Welcome Page setting controls the page that's loaded and displayed in the browser, but the URL you see (and that appears in search results) is rewritten to this friendlier format.</span></span>
  
    
    
<span data-ttu-id="7d70f-p107">Jede Seite, auch die Willkommensseite Ihrer Website, kann eine benutzerfreundliche URL aufweisen. Je nachdem, wie Sie Ihre Website konfigurieren, wird den meisten Seiten automatisch eine benutzerfreundliche URL zugewiesen. Benutzerfreundliche URLs können lokalisiert werden.</span><span class="sxs-lookup"><span data-stu-id="7d70f-p107">Any page, including your site's Welcome Page, can have a friendly URL. Depending on how you configure your site, most pages automatically get a friendly URL. Friendly URLs can be localized.</span></span>
  
    
    

## <a name="managed-navigation-apis"></a><span data-ttu-id="7d70f-137">APIs für verwaltete Navigation</span><span class="sxs-lookup"><span data-stu-id="7d70f-137">Managed Navigation APIs</span></span>
<span data-ttu-id="7d70f-138"><a name="SP15_ManagedNav_ManagedNavAPIs"> </a></span><span class="sxs-lookup"><span data-stu-id="7d70f-138"><a name="SP15_ManagedNav_ManagedNavAPIs"> </a></span></span>

<span data-ttu-id="7d70f-p108">Die Taxonomie-API bietet verschiedene neue Methoden und Eigenschaften in SharePoint, mit denen Sie Ausdrücke, Ausdruckssätze und andere Metadatenelemente im Terminologiespeicher für die Nutzung in Websitenavigationsszenarios verwenden können. Dieses APIs sind im .NET-Client, im .NET-Server, in Silverlight und in JavaScript-Programmiermodellen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="7d70f-p108">The taxonomy API provides several new methods and properties in SharePoint that you can use to customize terms, term sets, and other metadata elements in the term store for use in site navigation scenarios. These APIs are available in the .NET client, .NET server, Silverlight, and JavaScript programming models.</span></span>
  
    
    

## <a name="code-example-customizing-managed-navigation-with-the-net-client-object-model-csom-api"></a><span data-ttu-id="7d70f-141">Codebeispiel: Anpassen der verwalteten Navigation mit der .NET-Clientobjektmodell (CSOM)-API</span><span class="sxs-lookup"><span data-stu-id="7d70f-141">Code Example: Customizing managed navigation with the .NET client object model (CSOM) API</span></span>
<span data-ttu-id="7d70f-142"><a name="SP15_ManagedNav_CustomizingManagedNavWithNETCSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="7d70f-142"><a name="SP15_ManagedNav_CustomizingManagedNavWithNETCSOM"> </a></span></span>

<span data-ttu-id="7d70f-143">Wenn Sie das .NET-Clientobjektmodell für Taxonomie verwenden, können Sie einen neuen Navigationsausdruckssatz erstellen, sofern ein Terminologiespeicher für die aktuelle Websitesammlung vorhanden ist, oder einen vorhandenen Ausdruckssatz so konvertieren, dass er die verwaltete Navigation unterstützt.</span><span class="sxs-lookup"><span data-stu-id="7d70f-143">When you use the .NET client object model for taxonomy, you can create a new navigation term set if a term store exists for the current site collection, or convert an existing term set into one that supports managed navigation.</span></span>
  
    
    

  
    
    



```cs

///Create a navigation term set.
public class NavigationTermSetTests
    {
      public void CreateNavigationTermSet()
              {
               ClientContext clientContext = new ClientContext(TestConfig.ServerUrl);
            
                 TaxonomySession taxonomySession = TaxonomySession.GetTaxonomySession(clientContext);
                 taxonomySession.UpdateCache();

                 clientContext.Load(taxonomySession, ts => ts.TermStores);
                 clientContext.ExecuteQuery();

                 if (taxonomySession.TermStores.Count == 0)
                 throw new InvalidOperationException("The Taxonomy Service is offline or missing");

                 TermStore termStore = taxonomySession.TermStores[0];
                 clientContext.Load(termStore, 
                 ts => ts.Name, 
                 ts => ts.WorkingLanguage);

                 // Does the TermSet object already exist?
                 TermSet existingTermSet;

                 // Handles an error that occurs if the return value is null.
                 ExceptionHandlingScope exceptionScope = new ExceptionHandlingScope(clientContext);
             using (exceptionScope.StartScope())
                 {
                 using (exceptionScope.StartTry())
                 {
                 existingTermSet = termStore.GetTermSet(TestConfig.NavTermSetId);
                 }
                 using (exceptionScope.StartCatch())
                {
                }
                }
                clientContext.ExecuteQuery();

                if (!existingTermSet.ServerObjectIsNull.Value)
                {
                Log("CreateNavigationTermSet(): Deleting old TermSet");
                existingTermSet.DeleteObject();
                termStore.CommitAll();
                clientContext.ExecuteQuery();
                }

                Log("CreateNavigationTermSet(): Creating new TermSet");

               // Creates a new TermSet object.
            TermGroup siteCollectionGroup = termStore.GetSiteCollectionGroup(clientContext.Site, 
                createIfMissing: true);
            TermSet termSet = siteCollectionGroup.CreateTermSet("Navigation Demo", TestConfig.NavTermSetId, 
                termStore.WorkingLanguage);

            termStore.CommitAll();
            clientContext.ExecuteQuery();

            NavigationTermSet navTermSet = NavigationTermSet.GetAsResolvedByWeb(clientContext,
                termSet, clientContext.Web, "GlobalNavigationTaxonomyProvider");

            navTermSet.IsNavigationTermSet = true;
            navTermSet.TargetUrlForChildTerms.Value = "~site/Pages/Topics/Topic.aspx";

            termStore.CommitAll();
            clientContext.ExecuteQuery();

            NavigationTerm term1 = navTermSet.CreateTerm("Term 1", NavigationLinkType.SimpleLink, Guid.NewGuid());
            term1.SimpleLinkUrl = "http://www.bing.com/";

            Guid term2Guid = new Guid("87FAA433-4E3E-4500-AA5B-E04330B12ACD");
            NavigationTerm term2 = navTermSet.CreateTerm("Term 2", NavigationLinkType.FriendlyUrl,
                term2Guid);

            NavigationTerm childTerm = term2.CreateTerm("Term 2 child", NavigationLinkType.FriendlyUrl, Guid.NewGuid());

            childTerm.GetTaxonomyTerm().TermStore.CommitAll();
            clientContext.ExecuteQuery();
}


```


## <a name="code-example-customizing-managed-navigation-with-the-net-server-object-model-api"></a><span data-ttu-id="7d70f-144">Codebeispiel: Anpassen der verwalteten Navigation mit der .NET-Serverobjektmodell-API</span><span class="sxs-lookup"><span data-stu-id="7d70f-144">Code Example: Customizing managed navigation with the .NET server object model API</span></span>
<span data-ttu-id="7d70f-145"><a name="SP15_ManagedNav_CustomizingManagedNavNETServerObjectModel"> </a></span><span class="sxs-lookup"><span data-stu-id="7d70f-145"><a name="SP15_ManagedNav_CustomizingManagedNavNETServerObjectModel"> </a></span></span>

<span data-ttu-id="7d70f-146">Sie können die .NET-Servertaxonomieklassen und -methoden im  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) - und [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) -Namespace verwenden, um einen neuen Navigationsausdruckssatz zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="7d70f-146">You can use the .NET server taxonomy classes and methods in the  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) and [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) namespaces to create a new navigation term set.</span></span>
  
    
    

  
    
    



```cs

///Create a navigation term set.
using (SPSite site = new SPSite(TestConfig.ServerUrl))
            {
                using (SPWeb web = site.OpenWeb())
                {
                    TaxonomySession taxonomySession = new TaxonomySession(site, updateCache: true);

                    /// Use the first TermStore object in the list.
                    if (taxonomySession.TermStores.Count == 0)
                        throw new InvalidOperationException("The Taxonomy Service is offline or missing");

                    TermStore termStore = taxonomySession.TermStores[0];

                    /// Does the TermSet object already exist?
                    TermSet existingTermSet = termStore.GetTermSet(TestConfig.NavTermSetId);
                    if (existingTermSet != null)
                    {
                        Log("CreateNavigationTermSet(): Deleting old TermSet");
                        existingTermSet.Delete();
                        termStore.CommitAll();
                    }

                    Log("CreateNavigationTermSet(): Creating new TermSet");

                    /// Create a new TermSet object.
                    Group siteCollectionGroup = termStore.GetSiteCollectionGroup(site);
                    TermSet termSet = siteCollectionGroup.CreateTermSet("Navigation Demo", TestConfig.NavTermSetId);

                    NavigationTermSet navTermSet = NavigationTermSet.GetAsResolvedByWeb(termSet, web,
                        StandardNavigationProviderNames.GlobalNavigationTaxonomyProvider);

                    navTermSet.IsNavigationTermSet = true;
                    navTermSet.TargetUrlForChildTerms.Value = "~site/Pages/Topics/Topic.aspx";

                    NavigationTerm term1 = navTermSet.CreateTerm("Term 1", NavigationLinkType.SimpleLink);
                    term1.SimpleLinkUrl = "http://www.bing.com/";

                    Guid term2Guid = new Guid("87FAA433-4E3E-4500-AA5B-E04330B12ACD");
                    NavigationTerm term2 = navTermSet.CreateTerm("Term 2", NavigationLinkType.FriendlyUrl,
                        term2Guid);

                    /// Verify that the NavigationTermSetView is being applied correctly.
                    Assert.AreEqual(web.ServerRelativeUrl + "/term-2", term2.GetResolvedDisplayUrl(null).ToString());

                    string expectedTargetUrl = web.ServerRelativeUrl 
                        + "/Pages/Topics/Topic.aspx?TermStoreId=" + termStore.Id.ToString() 
                        + "&amp;TermSetId=" + TestConfig.NavTermSetId.ToString()
                        + "&amp;TermId=" + term2Guid.ToString();
                    Assert.AreEqual(expectedTargetUrl, term2.GetResolvedTargetUrl(null, null).ToString());

                    NavigationTerm childTerm = term2.CreateTerm("Term 2 child", NavigationLinkType.FriendlyUrl);
                    Assert.AreEqual(web.ServerRelativeUrl + "/term-2/term-2-child", childTerm.GetResolvedDisplayUrl(null).ToString());

                    /// Commit changes.
                    childTerm.GetTaxonomyTerm().TermStore.CommitAll();
                }
            }
```


## <a name="additional-resources"></a><span data-ttu-id="7d70f-147">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="7d70f-147">Additional resources</span></span>
<span data-ttu-id="7d70f-148"><a name="SP15_ManagedNav_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="7d70f-148"><a name="SP15_ManagedNav_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="7d70f-149">Inhaltssuche-Webpart in SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d70f-149">Content Search Web Part in SharePoint</span></span>](content-search-web-part-in-sharepoint.md)
    
  

