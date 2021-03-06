
# <a name="managed-navigation-in-sharepoint"></a>Verwaltete Navigation in SharePoint

  
    
    
![Konzeptuelles Übersichtsthema](../../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
Erfahren Sie mehr über das Feature der taxonomiegesteuerten verwalteten Navigation in SharePoint.
## <a name="introducing-managed-navigation"></a>Einführung in die verwaltete Navigation
<a name="SP15_ManagedNav_Introducing"> </a>

Eine gut durchdachte Navigation sagt den Benutzern einer Website eine Menge über die Geschäfte, Produkte und Dienste, die auf der Website angeboten werden. Indem sie die Taxonomie hinter der Navigation aktualisieren, können Unternehmen Änderungen vorantreiben und damit Schritt halten, ohne die Websitenavigation während des Vorgangs neu erstellen zu müssen. In SharePoint können Sie mit dem Feature der verwalteten Navigation eine Websitenavigation entwerfen, die durch verwaltete Metadaten gesteuert wird, und SEO-freundliche URLs erstellen, die von der Struktur der verwalteten Navigation abgeleitet werden. Die verwaltete Navigation bietet eine Alternative zum herkömmlichen SharePoint-Navigationsfeature - der strukturierten Navigation -, das auf der Struktur von SharePoint basiert. Da die verwaltete Navigation von der Taxonomie gesteuert wird, können Sie sie verwenden, um eine Websitenavigation um wichtige Geschäftskonzepte herum zu entwerfen, ohne die Struktur Ihrer Websites oder Websitekomponenten ändern zu müssen.
  
    
    

## <a name="how-managed-navigation-works"></a>Funktionsweise der verwalteten Navigation
<a name="SP15_ManagedNav_HowManagedNavWorks"> </a>

Die verwaltete Navigation bietet ein Framework für dynamisch generierte Seiten und stellt eine dazugehörige SEO-freundliche URL zur Verfügung. Jede generierte Seite wird in der Navigationshierarchie dargestellt. Statt separate Seiten für jede Kategorie in der Taxonomie erstellen zu müssen, bietet das Framework einen Vorlagen- und Vererbungsmechanismus, der die Zielseiten für die einzelnen Navigationslinks erstellt. Sie können das Feature der Themenseiten verwenden, um die Benutzeroberfläche der Zielseiten anzupassen.
  
    
    
APIs für verwaltete Navigation sind in die Taxonomie- und Veröffentlichungsbibliotheken in SharePoint integriert. Verwaltete Metadatenkomponenten wie Ausdruckssätze und der Terminologiespeicher werden verwendet, um die taxonomiegesteuerte Navigation für Ihre Website zu aktivieren. In der .NET-Serverklassenbibliothek enthält der  [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) -Namespace Ausdrucks-, Ausdruckssatz- und andere Klassenobjekte, die die **Term**-Klasse und die **TermSet**-Klasse im  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) -Navigationsnamespace spiegeln, sodass Methoden und Eigenschaften bereitgestellt werden, die speziell dafür vorgesehen sind, diese Metadatenelemente Navigationselementen zuzuordnen. Mit anderen Klassen wie z. B. [TaxonomySiteMapNode](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.TaxonomySiteMapNode.aspx) können Sie Metadaten mit verschiedenen Navigationselementen für Websites bereitstellen, wie z. B. mit Siteübersichtsknoten und anderen Teile der Websitenavigation. Über andere Klassen kann Zwischenspeicheung und Kontext für die verwalteten Navigation bereitgestellt werden.
  
    
    
Sie können Links der taxonomiegesteuerten Navigation in der globalen Navigation anzeigen. Die globale Navigation ist eine Navigationsebene mit einer oder mehreren Ebenen, die immer vorhanden ist, häufig am oberen Rand einer Website angezeigt wird und die Inhaltskategorien die obersten Ebene enthält. Sie können diese Links auch im aktuellen Navigationssteuerelement anzeigen, das häufig auf der linken Seite einer Seite zu finden ist. Das aktuelle Navigationssteuerelement stellt die nächste Hierarchieebene für die in der globalen Navigation gewählte Kategorie oder eine Gruppe von Links dar, die zu dieser Kategorie gehören.
  
    
    

## <a name="friendly-urls-and-the-managed-navigation-provider"></a>Benutzerfreundliche URLs und Anbieter der verwalteten Navigation
<a name="SP15_ManagedNav_FriendlyURLs"> </a>

Wenn Sie zum ersten Mal zu einer SharePoint-Website navigieren, stellen Sie möglicherweise fest, dass sich das URL-Format geändert hat. Statt einer Adresse mit einer  `/Pages/default.aspx`-Erweiterung endet die Seiten-URL nur mit  `/`. Die verwaltete Navigation bietet ein Schema für benutzerfreundliche URLs, das auf allen Website-, Kategorie-, und Elementseiten konsistent ist.
  
    
    
Dies wird vom Anbieter der verwalteten Navigation möglich gemacht. Wenn Sie zum Stamm einer beliebigen Website navigieren, die den Anbieter der verwalteten Navigation verwendet, steuert die Willkommensseiten-Einstellung der Website die Seite, die im Browser geladen und angezeigt wird; die angezeigte URL (die auch in Suchergebnissen angezeigt wird) wird jedoch in diesem benutzerfreundlicheren Format neu geschrieben.
  
    
    
Jede Seite, auch die Willkommensseite Ihrer Website, kann eine benutzerfreundliche URL aufweisen. Je nachdem, wie Sie Ihre Website konfigurieren, wird den meisten Seiten automatisch eine benutzerfreundliche URL zugewiesen. Benutzerfreundliche URLs können lokalisiert werden.
  
    
    

## <a name="managed-navigation-apis"></a>APIs für verwaltete Navigation
<a name="SP15_ManagedNav_ManagedNavAPIs"> </a>

Die Taxonomie-API bietet verschiedene neue Methoden und Eigenschaften in SharePoint, mit denen Sie Ausdrücke, Ausdruckssätze und andere Metadatenelemente im Terminologiespeicher für die Nutzung in Websitenavigationsszenarios verwenden können. Dieses APIs sind im .NET-Client, im .NET-Server, in Silverlight und in JavaScript-Programmiermodellen verfügbar.
  
    
    

## <a name="code-example-customizing-managed-navigation-with-the-net-client-object-model-csom-api"></a>Codebeispiel: Anpassen der verwalteten Navigation mit der .NET-Clientobjektmodell (CSOM)-API
<a name="SP15_ManagedNav_CustomizingManagedNavWithNETCSOM"> </a>

Wenn Sie das .NET-Clientobjektmodell für Taxonomie verwenden, können Sie einen neuen Navigationsausdruckssatz erstellen, sofern ein Terminologiespeicher für die aktuelle Websitesammlung vorhanden ist, oder einen vorhandenen Ausdruckssatz so konvertieren, dass er die verwaltete Navigation unterstützt.
  
    
    

  
    
    



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


## <a name="code-example-customizing-managed-navigation-with-the-net-server-object-model-api"></a>Codebeispiel: Anpassen der verwalteten Navigation mit der .NET-Serverobjektmodell-API
<a name="SP15_ManagedNav_CustomizingManagedNavNETServerObjectModel"> </a>

Sie können die .NET-Servertaxonomieklassen und -methoden im  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) - und [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx) -Namespace verwenden, um einen neuen Navigationsausdruckssatz zu erstellen.
  
    
    

  
    
    



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


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_ManagedNav_AdditionalResources"> </a>


-  [Inhaltssuche-Webpart in SharePoint](content-search-web-part-in-sharepoint)
    
  

