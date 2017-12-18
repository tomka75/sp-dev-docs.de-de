---
title: "Verwenden von Code zum Anheften von Ausdrücken zu Ausdruckssätzen in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4a2811dc-25fd-4eb2-b0ab-1edded64c556
ms.openlocfilehash: c04261b5106e2c66a308b0f96afd09b2065e41d4
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="use-code-to-pin-terms-to-navigation-term-sets-in-sharepoint"></a>Verwenden von Code zum Anheften von Ausdrücken zu Ausdruckssätzen in SharePoint

In diesem Artikel erfahren Sie, wie Sie Code verwenden, um Ausdrücke an Navigationsausdruckssätze anzuheften.

Bei der Taxonomieerstellung ist das Anheften die Möglichkeit, einen Ausdruck an ein Ziel anzufügen. In SharePoint wurde das Anheften von Ausdrücken eingeführt. Ein angehefteter Ausdruck ist einfach ein Ausdruck, der wiederverwendet wird, mit der Ausnahme, dass er schreibgeschützt ist und nicht an dem Ort geändert werden kann, an dem der Ausdruck verwendet wird.

In der SharePoint verwaltete Navigation können Sie die API zur Pin neue oder vorhandene Ausdrücke auf ein  [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.NavigationTermSet.aspx) -Objekt. In Microsoft SharePoint Server 2010 konnten Benutzer Begriffe (und alle geschachtelten den wiederverwendete Bestimmungen Begriffe) an anderen Stellen in der Hierarchie Begriff wiederverwenden. Nach dieser Begriffe wiederverwendet wurden, sie an einem Standort geändert werden konnte und Änderungen überall angezeigt werden würde, wurden die Begriffe wiederverwendet.

## <a name="term-pinning-essentials"></a>Feste Essentials Begriff
<a name="SP15_H2UseCodeToPinTerms_TermPinningEssentials"> </a>

Um zu verstehen, in SharePoint verankern, sollten Sie erfahren Sie, dass Navigation, Terminologiespeicher und Konzepte und APIs ähnliche verwaltete Metadaten, Ausdrücke, Ausdruckssätze, verwaltet. Tabelle 1 beschreibt Artikeln, in denen Weitere Informationen zum Anheften übergeben. 
  
    
    

**In Tabelle 1. Kernkonzepte für Verankern**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [Eine kurze Einführung in Enterprise Metadata Management für Microsoft SharePoint Server 2010-Entwickler](http://msdn.microsoft.com/library/113a5d75-ac4d-498b-8436-725e04fb685d%28Office.15%29.aspx) <br/> |In diesem Artikel ist für SharePoint Server 2010 geschrieben, bietet eine grundlegende Übersicht über die verwaltete Metadaten von Unternehmen programming Modell und die wichtigsten Konzepte, wie Ausdrücke und Ausdruckssätze.  <br/> |
| [Verwaltete Navigation in SharePoint](managed-navigation-in-sharepoint.md) <br/> |Eine Einführung in das Feature taxonomiegesteuerte verwaltete Navigation in SharePoint.  <br/> |
   

## <a name="use-code-to-complete-pinning-tasks"></a>Verwenden von Code festen Aufgaben
<a name="SP15_H2UseCodeToPinTerms_UseCodeToCompletePinning"> </a>

Benutzerdefinierten Code .NET Server, .NET Client (CSOM), Silverlight, oder JavaScript Programmiermodellen zum Anheften Vorgängen für Ausdrücke und Ausdruckssätze ausführen können. Die folgenden Codebeispiele für .NET Server enthalten einen Test für festen Begriffe im Zusammenhang mit navigationsausdruckssätzen und eine Methode, die Sie verwenden können, zu prüfen, ob ein **Term** -Objekt auf ein Objekt des angegebenen **TermSet** fixiert ist. Klicken Sie dann der Test **Term** Objekte erstellt und fixiert eine von ihnen angegebene **NavigationTermSet** -Objekt.
  
    
    

### <a name="to-pin-terms-to-navigation-term-sets"></a>So heften Sie Begriffe im Zusammenhang mit navigationsausdruckssätzen an


- Im folgende Beispiel testet festen Begriffe im Zusammenhang mit navigationsausdruckssätzen. Anschließend wird das  [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.SharePoint.NavigationTermSet.aspx) -Objekt, das enthält Methoden und Eigenschaften, die in verwalteten Navigation Szenarien, wie das Erstellen von Website taxonomiegesteuerte Navigationsmenüs sind.
    
    Im Beispiel prüft zunächst, ob ein **NavigationTermSet** -Objekt vorhanden ist. Wenn eine nicht vorhanden ist, erstellt der Code eine **NavigationTermSet**. (Sofern bereits vorhanden, löscht der Code der alte Datenbankserver bevor sie einen neuen Anwendungspool erstellt). Klicken Sie dann nach der Code einige **Term** -Objekte aus auswählt erstellt, erstellt eine Veröffentlichung (ASPX) Auslagerungsdatei zu Demonstrationszwecken, wird als benutzerdefinierte Zielseite für angeheftete Begriffe festgelegt und dann fixiert einige Navigationseigenschaften auf der Seite.
    


```cs
  
public void TermPinningTest()
        {
using (SPSite site = new SPSite(TestConfig.ServerUrl))
            {
                using (SPWeb web = site.OpenWeb())
                {
                    TaxonomySession taxonomySession = new TaxonomySession(site, updateCache: true);

                    // Create the navigation term set.
                    NavigationTermSet menuNavTermSet = DemoUtilities.SetUpSampleNavTermSet(
                        this.TestContext, taxonomySession, web);
                    TermSet menuTaxTermSet = menuNavTermSet.GetTaxonomyTermSet();

                    TermStore termStore = menuTaxTermSet.TermStore;
                    Group group = menuTaxTermSet.Group;

                    // Does the tagging Taxonomy term set already exist?
                    TermSet taggingTaxTermSet = group.TermSets.FirstOrDefault(
                        ts => ts.Id == TestConfig.TaggingTermSetId);

                    if (taggingTaxTermSet != null)
                    {
                        Log("Deleting old tagging term set");

                        // If the tagging Taxonomy term set already exists, delete the old one.
                        taggingTaxTermSet.Delete();
                        termStore.CommitAll();
                    }

                    Log("Creating the tagging term set");

                    taggingTaxTermSet = group.CreateTermSet("Demo Tagging TermSet", TestConfig.TaggingTermSetId);

                    int lcid = termStore.WorkingLanguage;

                    // Create some terms.
                    Term taggingProductsTaxTerm = taggingTaxTermSet.CreateTerm("Products", lcid);
                    taggingProductsTaxTerm.CreateTerm("Electronics", lcid);
                    taggingProductsTaxTerm.CreateTerm("Footwear", lcid);
                    taggingProductsTaxTerm.CreateTerm("Sports", lcid);

                    termStore.CommitAll();

                    /// Pinning the products subtree. Pins the "Products" Term object to the NavigationTermSet object.
                    Term menuProductsTaxTerm = menuTaxTermSet.ReuseTermWithPinning(taggingProductsTaxTerm);
                    termStore.CommitAll();

                    /// Creating the publishing page template DemoTargetPage.aspx");
                    PublishingWeb publishingWeb = PublishingWeb.GetPublishingWeb(web);

                    SPListItem pageListItem = null;
                    PublishingPage publishingPage;
                    try
                    {
                        pageListItem = web.GetListItem(web.Url + "/Pages/DemoTargetPage.aspx");
                        publishingPage = PublishingPage.GetPublishingPage(pageListItem);
   
                    }
                    catch (FileNotFoundException)
                    {
                        Log("Creating new target page");
                        publishingPage = publishingWeb.AddPublishingPage("DemoTargetPage.aspx", publishingWeb.DefaultPageLayout);
                        Log("Checking in target page draft");
                        publishingPage.CheckIn("TermPinningTest");
                    }

                    // Set a custom target page for the pinned terms and then set some navigation properties.

                    // Normally the navigation objects are obtained by way of an optimized function such as
                    // TaxonomyNavigation.GetTermSetForWeb() or TaxonomyNavigationContext.Current.NavigationTerm.
                    // The function guarantees that URLs will be resolved using a valid NavigationTerm.View.
                    // But because we are populating totally new data, the cache will probably not be updated
                    // yet, so instead we manually construct a view using GetAsResolvedByWeb().
                    NavigationTerm menuProductsNavTerm = NavigationTerm.GetAsResolvedByWeb(menuProductsTaxTerm,
                        web, StandardNavigationProviderNames.GlobalNavigationTaxonomyProvider);

                    menuProductsNavTerm.TargetUrl.Value = publishingPage.Uri.AbsolutePath;
                    menuProductsNavTerm.TargetUrlForChildTerms.Value = publishingPage.Uri.AbsolutePath;

                    termStore.CommitAll();

                    Log("TermPinningTest completed successfully");
                }
            }

}
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_H2UseCodeToPinTerms_AdditionalResources"> </a>


-  [Verwaltete Metadaten und Navigation in SharePoint](managed-metadata-and-navigation-in-sharepoint.md)
    
  
-  [Microsoft.SharePoint.Publishing.Navigation](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx)
    
  

