---
title: Verwaltete Metadaten und Navigation in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b66d4ec1-a2ef-49cc-8ca5-a6b516bff02e
ms.openlocfilehash: e4b5453894cf03a93758157b5caa2e2f92208646
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="managed-metadata-and-navigation-in-sharepoint"></a>Verwaltete Metadaten und Navigation in SharePoint

  
    
    
![Konzeptuelles Übersichtsthema](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
Informationen über verwaltete Metadaten von Unternehmen (EMM) und Navigationsfunktionen in SharePoint.
## <a name="managed-metadata-feature-enhancements-in-sharepoint-for-developers"></a>Funktionsverbesserungen für verwaltete Metadaten in SharePoint für Entwickler
<a name="SP15_ManagedMetadataAndNav_ManagedMetadataFeatureEnhancements"> </a>

Mit verwalteten Metadaten können Sie Taxonomien erstellen und Strategien markieren, die bestimmten Geschäftsanforderungen entsprechen. In SharePoint wurde der grundlegende verwaltete Metadaten-API-Satz erweitert und verbessert, um mehr Funktionen bereitzustellen und mehr Szenarien zu unterstützen.
  
    
    

## <a name="net-client-object-model-csom-support-for-managed-metadata-apis"></a>Unterstützung vom .NET-Clientobjektmodell für verwaltete Metadaten-APIs
<a name="SP15_ManagedMetadataAndNav_CSOMSupport"> </a>

Das SharePoint-Clientobjektmodell unterstützt das Anpassen und Erstellen von Taxonomien. Taxonomie steht im .NET-Clientobjektmodell, in Silverlight und in JavaScript-Programmiermodellen zur Verfügung. Die Entwicklung mit diesem ähnelt der Entwicklung mit dem .NET-Serverprogrammiermodell. Möglicherweise möchten Sie Clientobjektmodell-Lösungen zur Unterstützung von Szenarien entwickeln, in denen das Lesen von Inhalten häufiger auftritt, als das Erstellen oder Verwalten von diesen. Sie müssen das Clientobjektmodell verwenden, um die Verwendung von Taxonomie in einem cloudbasierten Szenario wie SharePoint Online oder für eine Teilmenge von Szenarien zu aktivieren, die lokal verfügbar sind.
  
    
    
Wenn Sie ein neues Clientobjektmodell-Projekt in Visual Studio erstellen möchten, in dem die Taxonomiefunktion verwendet wird, legen Sie die folgenden Verweise fest:
  
    
    

- Microsoft.SharePoint.Client.dll
    
  
- Microsoft.SharePoint.Client.Runtime.dll
    
  
- Microsoft.SharePoint.Client.Taxonomy.dll
    
  
Die Entwicklung von Anpassungen mit dem Clientobjektmodell ähnelt weitestgehend der Entwicklung von .NET-Servertaxonomielösungen: Informationen zum **TaxonomySession**- und **TermStore**-Objekt, zu **Group**-, **TermSet**- und **Term**-Objekten, die für die Sitzung erforderlich sind.
  
    
    

### <a name="code-examples-basic-operations-with-the-taxonomy-csom"></a>Codebeispiele: Grundlegende Vorgänge mit dem Taxonomie-Clientobjektmodell
<a name="SP15_ManagedMetadataAndNav_ExampleBasicOperations"> </a>

Mit den folgenden Codebeispielen können Sie grundlegende Vorgänge mit dem Taxonomie-Clientobjektmodell abschließen. Im ersten Beispiel werden ein **Group**- Objekt, ein **TermSet**-Objekt und **Term**-Objekte erstellt. Im zweiten Beispiel wird ein **Group**-Objekt durchlaufen und seine Inhalte werden geschrieben.
  
    
    

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


  
    
    

## <a name="pinning"></a>Anheften
<a name="SP15_ManagedMetadataAndNav_Pinning"> </a>

In Microsoft SharePoint Server 2010konnten Benutzer Ausdrücke (und alle innerhalb des wiederverwendeten Ausdrucks verschachtelten Ausdrücke) an anderen Stellen in der Ausdruckshierarchie wiederverwendet werden. Wenn diese Ausdrücke nach Wiederverwendung geändert wurden, wurden die Änderungen an allen Stellen übernommen, wo diese wiederverwendet wurden. In SharePoint wurde das Anheften von Ausdrücken eingeführt. Ein angehefteter Ausdruck entspricht einem wiederverwendeten Ausdruck mit der Ausnahme, dass er schreibgeschützt ist und nicht an den Stellen geändert werden kann, an denen er wiederverwendet wird. Ein Beispiel hierzu finden Sie unter  [Vorgehensweise: Verwendung Code Pin Bedingungen Navigation Begriff wird im SharePoint](how-to-use-code-to-pin-terms-to-navigation-term-sets-in-sharepoint.md).
  
    
    

  
    
    

## <a name="datasheet-view-support-for-managed-metadata-column-types"></a>Unterstützung für die Datenblattansicht für verwaltete Metadaten-Spaltentypen
<a name="SP15_ManagedMetadataAndNav_DatasheetViewSupport"> </a>

In SharePoint wurde die Datenblatt-Ansichtsfunktion geändert. Die Standardansicht für die Rasterbearbeitung wird nun mit einem Doppelklick auf die Aktion geöffnet werden. Metadatenspalten können mit den gleichen Funktionen wie beim Bearbeiten von einzelnen Elementen bearbeitet werden. Dies umfasst den Zugriff auf den Ausdruckssatz hinter der Spalte. Bei dieser Funktion geht es um Funktionen zur Metadatenänderung, die beim Bearbeiten eines einzelnen Elements für die Datenblattbearbeitung zur Verfügung stehen.
  
    
    

## <a name="managed-navigation"></a>Verwaltete Navigation
<a name="SP15_ManagedMetadataAndNav_ManagedNav"> </a>

Die verwaltete Navigation umfasst verwaltete Metadatenfunktionen wie das Anheften von Elementen an Ausdrücke und das Verwalten von Ausdrücken in einem Ausdrucksspeicher zur Bereitstellung einer in hohem Maße angepassten Websitenavigation. Die strukturierte Navigation, die von der SharePoint-Infrastruktur abhängt, ist in SharePoint weiterhin verfügbar.
  
    
    

## <a name="friendly-urls"></a>Benutzerfreundliche URLs
<a name="SP15_ManagedMetadataAndNav_FriendlyURLs"> </a>

Benutzerfreundliche URLs stellen ein kürzeres URL-Format dar, das in der Adressleiste der meisten SharePoint-Veröffentlichungsseiten angezeigt wird, einschließlich der Willkommensseite Ihrer Website. Sie sind SEO-freundlich und werden in Suchergebnissen angezeigt. 
  
    
    

## <a name="support-for-new-scenarios"></a>Unterstützung für neue Szenarien
<a name="SP15_ManagedMetadataAndNav_SupportForNewScenarios"> </a>

Mit dem Ausdrucksspeicher-Manager können Ausdrucksverwendungsmodelle, die auf flexibleren und leistungsstärkeren verwalteten Metadatenfunktionen in basieren, verbessert und erweitert werden:
  
    
    

- Verweisen auf eine andere Websitesammlung und Anzeigen von Ausdrücken von anderen Benutzern.Wenn Sie Ihren Ausdruckssatz für andere mit dem verwalteten Metadatendienst verknüpften Websitesammlungen zur Verfügung stellen möchten, erstellen Sie ein **global term set**. Wenn Sie einen privaten Ausdruckssatz erstellen möchten, der nur für eine bestimmte Websitesammlung zur Verfügung steht, wenn er im verwalteten Metadatendienst gespeichert ist, erstellen Sie ein **local term set**. 
    
  
- Das Verwenden von Schlüsselwörtern außerhalb eines bestimmten Ausdruckssatzes für Benutzer blockieren.
    
  
- Zusätzliche, mehrsprachige Unterstützung, darunter Unterstützung für automatisierte Übersetzung und flexible LCIDs. 
    
  

## <a name="unsupported-scenarios-for-working-with-custom-site-definitions"></a>Nicht unterstützte Szenarien für das Arbeiten mit benutzerdefinierten Websitedefinitionen
<a name="SP15_ManagedMetadataAndNav_UnsupportedScenarios"> </a>


- In SharePoint wird das Erstellen von Taxonomiefeldern (verwalteten Metadaten-Websitespalten) mithilfe einer XML-Definition nicht unterstützt.
    
  
- In SharePoint wird das Verwenden von Taxonomiefeldern (verwalteten Metadaten-Websitespalten) in Websitevorlagen nicht unterstützt.
    
  
- Weitere Informationen finden Sie im Microsoft Support-Artikel #898631:  [Unterstützte und nicht unterstütze Szenarien](http://support2.microsoft.com/default.aspx?scid=kb;EN-US;898631
)
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_ManagedMetadataAndNav_AdditionalResources"> </a>


-  [Verwaltete Navigation in SharePoint](managed-navigation-in-sharepoint.md)
    
  
-  [Inhaltssuche-Webpart in SharePoint](content-search-web-part-in-sharepoint.md)
    
  

