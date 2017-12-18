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
# <a name="use-code-to-pin-terms-to-navigation-term-sets-in-sharepoint"></a><span data-ttu-id="47a73-102">Verwenden von Code zum Anheften von Ausdrücken zu Ausdruckssätzen in SharePoint</span><span class="sxs-lookup"><span data-stu-id="47a73-102">How to: Use code to pin terms to navigation term sets in SharePoint</span></span>

<span data-ttu-id="47a73-103">In diesem Artikel erfahren Sie, wie Sie Code verwenden, um Ausdrücke an Navigationsausdruckssätze anzuheften.</span><span class="sxs-lookup"><span data-stu-id="47a73-103">Learn how to use code to pin terms to navigation term sets.</span></span>

<span data-ttu-id="47a73-104">Bei der Taxonomieerstellung ist das Anheften die Möglichkeit, einen Ausdruck an ein Ziel anzufügen.</span><span class="sxs-lookup"><span data-stu-id="47a73-104">In taxonomy creation, pinning is the ability to attach a term to a target.</span></span> <span data-ttu-id="47a73-105">In SharePoint wurde das Anheften von Ausdrücken eingeführt.</span><span class="sxs-lookup"><span data-stu-id="47a73-105">SharePoint introduces term pinning.</span></span> <span data-ttu-id="47a73-106">Ein angehefteter Ausdruck ist einfach ein Ausdruck, der wiederverwendet wird, mit der Ausnahme, dass er schreibgeschützt ist und nicht an dem Ort geändert werden kann, an dem der Ausdruck verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="47a73-106">Learn how to use code to pin terms to navigation term sets. In taxonomy creation, pinning is the ability to attach a term to a target. SharePoint introduces term pinning. A pinned term is just like a term that is reused, except it is read-only and cannot be changed in the location where the term is used.</span></span>

<span data-ttu-id="47a73-p102">In der SharePoint verwaltete Navigation können Sie die API zur Pin neue oder vorhandene Ausdrücke auf ein  [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.NavigationTermSet.aspx) -Objekt. In Microsoft SharePoint Server 2010 konnten Benutzer Begriffe (und alle geschachtelten den wiederverwendete Bestimmungen Begriffe) an anderen Stellen in der Hierarchie Begriff wiederverwenden. Nach dieser Begriffe wiederverwendet wurden, sie an einem Standort geändert werden konnte und Änderungen überall angezeigt werden würde, wurden die Begriffe wiederverwendet.</span><span class="sxs-lookup"><span data-stu-id="47a73-p102">In SharePoint managed navigation, the API enables you to pin new or existing terms to a  [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.NavigationTermSet.aspx) object. In Microsoft SharePoint Server 2010, users could reuse terms (and all terms nested under the reused terms) in other locations in the term hierarchy. After these terms were reused, they could be modified in any location and changes would be seen everywhere the terms were reused.</span></span>

## <a name="term-pinning-essentials"></a><span data-ttu-id="47a73-110">Feste Essentials Begriff</span><span class="sxs-lookup"><span data-stu-id="47a73-110">Term pinning essentials</span></span>
<span data-ttu-id="47a73-111"><a name="SP15_H2UseCodeToPinTerms_TermPinningEssentials"> </a></span><span class="sxs-lookup"><span data-stu-id="47a73-111"><a name="SP15_H2UseCodeToPinTerms_TermPinningEssentials"> </a></span></span>

<span data-ttu-id="47a73-p103">Um zu verstehen, in SharePoint verankern, sollten Sie erfahren Sie, dass Navigation, Terminologiespeicher und Konzepte und APIs ähnliche verwaltete Metadaten, Ausdrücke, Ausdruckssätze, verwaltet. Tabelle 1 beschreibt Artikeln, in denen Weitere Informationen zum Anheften übergeben.</span><span class="sxs-lookup"><span data-stu-id="47a73-p103">To understand pinning in SharePoint, you may want to learn about managed metadata, terms, term sets, managed navigation, the term store, and other related concepts and APIs. Table 1 describes articles that give more information about pinning.</span></span> 
  
    
    

<span data-ttu-id="47a73-114">**In Tabelle 1. Kernkonzepte für Verankern**</span><span class="sxs-lookup"><span data-stu-id="47a73-114">**Table 1. Core concepts for pinning**</span></span>


|<span data-ttu-id="47a73-115">**Titel des Artikels**</span><span class="sxs-lookup"><span data-stu-id="47a73-115">**Article title**</span></span>|<span data-ttu-id="47a73-116">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="47a73-116">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="47a73-117">Eine kurze Einführung in Enterprise Metadata Management für Microsoft SharePoint Server 2010-Entwickler</span><span class="sxs-lookup"><span data-stu-id="47a73-117">A Brief Introduction to Enterprise Metadata Management for Microsoft SharePoint Server 2010 Developers</span></span>](http://msdn.microsoft.com/library/113a5d75-ac4d-498b-8436-725e04fb685d%28Office.15%29.aspx) <br/> |<span data-ttu-id="47a73-118">In diesem Artikel ist für SharePoint Server 2010 geschrieben, bietet eine grundlegende Übersicht über die verwaltete Metadaten von Unternehmen programming Modell und die wichtigsten Konzepte, wie Ausdrücke und Ausdruckssätze.</span><span class="sxs-lookup"><span data-stu-id="47a73-118">Written for SharePoint Server 2010, this article provides a basic overview of the enterprise managed metadata programming model and core concepts, such as terms and term sets.</span></span>  <br/> |
| [<span data-ttu-id="47a73-119">Verwaltete Navigation in SharePoint</span><span class="sxs-lookup"><span data-stu-id="47a73-119">Managed navigation in SharePoint</span></span>](managed-navigation-in-sharepoint.md) <br/> |<span data-ttu-id="47a73-120">Eine Einführung in das Feature taxonomiegesteuerte verwaltete Navigation in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="47a73-120">An introduction to the taxonomy-driven managed navigation feature in SharePoint.</span></span>  <br/> |
   

## <a name="use-code-to-complete-pinning-tasks"></a><span data-ttu-id="47a73-121">Verwenden von Code festen Aufgaben</span><span class="sxs-lookup"><span data-stu-id="47a73-121">Use code to complete pinning tasks</span></span>
<span data-ttu-id="47a73-122"><a name="SP15_H2UseCodeToPinTerms_UseCodeToCompletePinning"> </a></span><span class="sxs-lookup"><span data-stu-id="47a73-122"><a name="SP15_H2UseCodeToPinTerms_UseCodeToCompletePinning"> </a></span></span>

<span data-ttu-id="47a73-p104">Benutzerdefinierten Code .NET Server, .NET Client (CSOM), Silverlight, oder JavaScript Programmiermodellen zum Anheften Vorgängen für Ausdrücke und Ausdruckssätze ausführen können. Die folgenden Codebeispiele für .NET Server enthalten einen Test für festen Begriffe im Zusammenhang mit navigationsausdruckssätzen und eine Methode, die Sie verwenden können, zu prüfen, ob ein **Term** -Objekt auf ein Objekt des angegebenen **TermSet** fixiert ist. Klicken Sie dann der Test **Term** Objekte erstellt und fixiert eine von ihnen angegebene **NavigationTermSet** -Objekt.</span><span class="sxs-lookup"><span data-stu-id="47a73-p104">You can use custom code from the .NET server, .NET client (CSOM), Silverlight, or JavaScript programming models to complete pinning operations on terms and term sets. The following .NET server code examples include a test for pinning terms to navigation term sets, and a method that you can use to test whether a **Term** object is pinned to a specified **TermSet** object. Then, the test creates **Term** objects, and pins one of them to the specified **NavigationTermSet** object.</span></span>
  
    
    

### <a name="to-pin-terms-to-navigation-term-sets"></a><span data-ttu-id="47a73-126">So heften Sie Begriffe im Zusammenhang mit navigationsausdruckssätzen an</span><span class="sxs-lookup"><span data-stu-id="47a73-126">To pin terms to navigation term sets</span></span>


- <span data-ttu-id="47a73-p105">Im folgende Beispiel testet festen Begriffe im Zusammenhang mit navigationsausdruckssätzen. Anschließend wird das  [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.SharePoint.NavigationTermSet.aspx) -Objekt, das enthält Methoden und Eigenschaften, die in verwalteten Navigation Szenarien, wie das Erstellen von Website taxonomiegesteuerte Navigationsmenüs sind.</span><span class="sxs-lookup"><span data-stu-id="47a73-p105">The following sample tests pinning terms to navigation term sets. It uses the  [NavigationTermSet](https://msdn.microsoft.com/library/Microsoft.SharePoint.SharePoint.NavigationTermSet.aspx) object, which contains methods and properties that are handy in managed navigation scenarios, such as creating taxonomy-driven site navigation menus.</span></span>
    
    <span data-ttu-id="47a73-p106">Im Beispiel prüft zunächst, ob ein **NavigationTermSet** -Objekt vorhanden ist. Wenn eine nicht vorhanden ist, erstellt der Code eine **NavigationTermSet**. (Sofern bereits vorhanden, löscht der Code der alte Datenbankserver bevor sie einen neuen Anwendungspool erstellt). Klicken Sie dann nach der Code einige **Term** -Objekte aus auswählt erstellt, erstellt eine Veröffentlichung (ASPX) Auslagerungsdatei zu Demonstrationszwecken, wird als benutzerdefinierte Zielseite für angeheftete Begriffe festgelegt und dann fixiert einige Navigationseigenschaften auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="47a73-p106">The sample first checks whether a **NavigationTermSet** object exists. If one doesn't exist, then the code creates a **NavigationTermSet**. (If one already exists, the code deletes the old one before it creates a new one). Then, after the code creates some **Term** objects to pick from, it creates a publishing page (.aspx) file for demonstration purposes, sets it as the custom target page for pinned terms, and then pins some navigation properties to the page.</span></span>
    


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


## <a name="additional-resources"></a><span data-ttu-id="47a73-133">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="47a73-133">Additional resources</span></span>
<span data-ttu-id="47a73-134"><a name="SP15_H2UseCodeToPinTerms_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="47a73-134"><a name="SP15_H2UseCodeToPinTerms_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="47a73-135">Verwaltete Metadaten und Navigation in SharePoint</span><span class="sxs-lookup"><span data-stu-id="47a73-135">Managed metadata and navigation in SharePoint</span></span>](managed-metadata-and-navigation-in-sharepoint.md)
    
  
-  [<span data-ttu-id="47a73-136">Microsoft.SharePoint.Publishing.Navigation</span><span class="sxs-lookup"><span data-stu-id="47a73-136">Microsoft.SharePoint.Publishing.Navigation</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.Navigation.aspx)
    
  

