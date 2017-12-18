---
title: "Erstellen von suchgesteuerten mobilen Apps mit den REST-Schnittstellen für Navigation und Ereignisprotokollierung"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5b313130-500c-4ccf-80ea-b102f30e5afb
ms.openlocfilehash: 98ba8acf95b52ddc183574684901923b4544e37c
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="build-search-driven-mobile-apps-with-the-navigation-and-event-logging-rest-interfaces"></a>Erstellen von suchgesteuerten mobilen Apps mit den REST-Schnittstellen für Navigation und Ereignisprotokollierung

In SharePoint werden die REST-Schnittstellen für Navigation und Ereignisprotokollierung eingeführt, die es Ihnen ermöglichen, eine suchgesteuerte mobile App für mobile Geräte wie Smartphones und Tablets zu erstellen, auf denen andere Betriebssysteme (keine Windows-Betriebssysteme) wie beispielsweise Android und iOS ausgeführt werden.
## <a name="how-apps-work-with-the-product-catalog"></a>Zusammenarbeit von Apps mit dem Produktkatalog
<a name="mobile_app_and_product_catalog"> </a>

Ein Produktkatalog kann auf unterschiedliche Weise auf einem mobilen Gerät angezeigt werden. In der Vergangenheit können Sie einen mobilen Channel für den Produktkatalog in SharePoint konfigurieren. Erstellen eines mobilen Kanals können Sie ein Erscheinungsbild anpassen, die alle Bildschirmgröße auf einem mobilen Gerät entspricht. Die resultierende Seite wird im angezeigt. ASPX-Format mit einem Webbrowser auf dem mobilen Gerät. Die Struktur der Seiten und die entsprechende Logik wird von dem Server mit SharePoint behandelt. Im Gegensatz dazu eine app, die mit der Navigation und Ereignis Protokollierung REST-Schnittstellen erstellt ist suchbasierte und fungiert als Front-End, die Produkt-Katalogstrukturen zu navigieren.
  
    
    
Eine app ist keine eigenständige Anwendung, aber es funktioniert in einer vorhandenen SharePoint-Installation mit einem Produktkatalog einrichten. Die app kann die Navigationsstruktur dynamisch aktualisieren, wenn Produktkatalog in dieser bestimmten SharePoint-Installation geändert wurde. Darüber hinaus, klicken Sie auf Ereignisse, die durch den Benutzer wieder auf dem Server mit SharePoint gesendet werden, um die Qualität der Empfehlungen für den Produktkatalog vorgenommene insgesamt zu verbessern.
  
    
    
Die app erstellt Produktkatalog anzeigen, ohne mit einem Webbrowser vom Benutzer benötigten Seiten. Gestaltungsvorlagen, Seitenlayouts und Logik zum Erstellen von Seiten zum Anzeigen des Produktkatalogs werden als einer app auf Geräte heruntergeladen; Diese Seiten werden wiederverwendet, wenn der Benutzer die app ausgeführt wird. Während der Benutzer des Produktkatalogs navigiert, wird die app gleichzeitig eine Navigationsstruktur erstellt und richtet Seiten. Suchabfragen werden zum Ausfüllen relevanter Seiten mit Elementinhalts an der Produktkatalog in SharePoint gesendet. Die entsprechenden Suchergebnisse werden dann verwendet, um die Seiten zu füllen.
  
    
    

## <a name="example-create-a-search-driven-mobile-app-with-home-category-and-item-detail-pages"></a>Beispiel: Erstellen einer mobilen suchbasierte-app mit Home, Kategorie und Element Projektdetailseiten verwalten
<a name="example_search_driven_mobile_app"> </a>

Angenommen, Sie haben eine mobile app mit drei Arten von Seiten: eine Homepage, Kategorieseiten und objektdetailseiten. In den folgenden Abschnitten wird beschrieben, wie die Navigation, Ereignisprotokollierung und Search-REST-Schnittstellen zum Erstellen von Seiten verwendet werden.
  
    
    

### <a name="home-page-for-a-search-driven-mobile-app"></a>Homepage für eine suchbasierte mobilen app

In der Regel wird **die Homepage** angezeigt, wenn die app gestartet wird. **Die Homepage** enthält im Menü der Produkt-Katalog, Text und ein statisches Bild, wie in Abbildung 1 dargestellt.
  
    
    

**Abbildung 1. Homepage für eine suchbasierte mobilen app**

  
    
    

  
    
    
![Erstellen suchgesteuerter mobiler Apps](../images/SP15_Buildsearch-drivenmobileappspages_home.gif)
  
    
    
Um diese Seite zu konstruieren, sendet die app einen Navigation REST-Aufruf an den Server mit SharePoint Anfordern der Navigationsstruktur des Produktkatalogs. Im nächsten Schritt wird die app verwendet die Antwortdaten, um die richtige Taxonomie oder Menüstruktur einzurichten und zeigt die richtige Begriffsnamen für den Produktkatalog. Zusätzliche Inhalte wie Seitenlayout, Titeltext und statische Bilder werden in der app selbst gespeichert. Wenn die Taxonomie zu einem späteren Zeitpunkt geändert wird, kann die app aktualisiert werden, mit dem REST der Navigation angerufen, wenn es ausgeführt wird.
  
    
    
Es folgt ein Beispiel für eine typische Navigation REST-Aufrufs.
  
    
    



```

GET http://server/_api/navigation/menustate?mapprovidername='GlobalNavigationSwitchableProvider'

```

Eine entsprechende Antwort wird angezeigt,  [Beispielantwort für eine REST Navigation für eine mobile app aufgerufen werden](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md#response_navigation_rest).
  
    
    

### <a name="category-page-for-a-search-driven-mobile-app"></a>Kategorieseite für eine suchbasierte mobilen app

**Kategorieseite** viele Elemente in einer ausgewählten Kategorie angezeigt. Jedes Element in einer Kategorie aufgeführt kann in der Regel durch einige relevante Elementdaten wie Titel, ein Bild und Preis dargestellt werden. Diese Daten werden aus dem Produktkatalog erfasst, mithilfe einer Suchabfrage SharePoint Search-REST-Dienst wie in Abbildung 2 dargestellt.
  
    
    

**Abbildung 2. Kategorieseite für eine suchbasierte mobilen app**

  
    
    

  
    
    
![Erstellen suchgesteuerter mobiler Apps](../images/Buildsearch-drivenmobileappspages.gif)
  
    
    
Wenn Sie eine der Kategorien im vorherigen Diagramm auswählen, wird angenommen, **TV**, **eine Kategorieseite** angezeigt.
  
    
    
Es folgt ein Beispiel für eine typische Search-REST-Abfrage zum Abrufen von Inhalten für eine bestimmte Kategorie.
  
    
    



```

GET http://server/_api/search/query?querytext='owstaxidProductCatalogItemCategory:#0<TermGuid>'

```

Eine übereinstimmende Antwort wird in [Beispielantwort für eine Search-REST-Abfrage für eine mobile App](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md#response_search_rest) gezeigt.
  
    
    
Die Abfrageverarbeitungskomponente in SharePoint gibt Suchergebnisse zurück, die Daten für eine bestimmte Kategorie enthalten. Die App präsentiert die Daten auf der Seite **Kategorie**. Liegt ein bestes Suchergebnis vor, das der ausgewählten Kategorie zugeordnet ist, erkennt die Abfrageverarbeitungskomponente diese Zuordnung und extrahiert die Daten des besten Suchergebnisses aus der entsprechenden Datenbank. Diese ist im Diagramm als **BB** bezeichnet. Die Suchergebnisse werden dann mit Ergebnissen aus der Datenbank der besten Suchergebnisse gemischt und in einer Ergebnistabelle zurück an die App gesendet. Die App ist verantwortlich für die Extraktion der verschiedenen Teile der Ergebnisse aus der Tabelle und für die Anzeige des besten Suchergebnisses an einem dedizierten Ort.
  
    
    

### <a name="item-detail-pages-for-a-search-driven-mobile-app"></a>Elementdetailseiten für eine suchbasierte mobile App

Wenn Sie ein Element in einer Kategorie auswählen, wird die Seite **Elementdetails** angezeigt. Auf dieser Seite wird ein Element mit Daten wie Titel, Produktbilder, technische Beschreibung, Preis und Übermittlungsinformationen ausführlich beschrieben. Weitere Empfehlungen oder Bewertungen, wenn verfügbar, auch angezeigt. Um die Seite **Details für** zu konstruieren, sendet die app zwei Abfragen: eine Abfrage zum Abrufen von Elementdaten und eine andere Abfrage empfangen Empfehlungen im Zusammenhang mit, dass das Element, wie in Abbildung 3 dargestellt.
  
    
    

**Abbildung 3. Element-Detailseite für eine suchbasierte mobilen app**

  
    
    

  
    
    
![Suchgesteuertes Erstellen](../images/Buildsearch-drivenmobileappspages_item_details.gif)
  
    
    
Es folgt ein Beispiel für eine typische Search-REST-Abfrage zum Abrufen von Inhalten für ein bestimmtes Element.
  
    
    



```

GET http://server/_api/search/query?querytext='ProductCatalogItemNumberOWSTEXT:1234567'
```

Empfehlungen werden nicht in der app selbst in SharePoint, berechnet. Empfehlungen basierend auf der Benutzerereignisse erstellen - nicht nur in diese spezielle app aber alle Benutzerereignisse, die mithilfe des Produktkatalogs erfasst werden - die app sendet ständig Veranstaltungen, sobald sie, an den Produktkatalog in SharePoint über einen Anruf Ereignis auftreten. Diese Benutzerereignisse werden im Ereignisprotokoll gespeichert und verarbeitet nur wie andere Benutzer Ereignissen im Zusammenhang mit diesem bestimmten Element. Kein Rückruf wird an die app aus dem Produktkatalog gesendet. Die Empfehlungen berechnet stehen für die app über den SharePoint Search-REST-Dienst.
  
    
    
Das folgende Beispiel zeigt einen Anruf typische **POST** für die ereignisprotokollierung.
  
    
    



```
POST http://server/_api/events/logevent
{
      "usageEntry": {
            "__metadata": {
                  "type": "Microsoft.SharePoint.Administration.UsageEntry"
            },
            "EventTypeId": 1,
            "ItemId": "an item fb7c-4196-8123-e54eee5f4787",
            "ScopeId": "61141c0e-fb7c ",
            "Site": "61141c0e- 
-4196-8123-e54eee5f4787",
            "User": "johndoe"
      }
}
```

Der Dienst folgt standard-HTTP-Rückgabecodes: eine 200 HTTP-Antwort gibt eine erfolgreiche Anforderung. Es sind keine Antworten aus dem Produktkatalog für das Ereignis Protokollierung REST-Schnittstelle.
  
    
    

## <a name="example-response-for-a-navigation-rest-call-for-a-mobile-app"></a>Beispielantwort für eine REST Navigation für eine mobile app aufgerufen werden
<a name="response_navigation_rest"> </a>


```

<?xml version="1.0" encoding="utf-8"?>
<d:MenuState xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml" m:type="SP.MenuState">

  <d:FriendlyUrlPrefix>/sites/contoso/</d:FriendlyUrlPrefix>
  <d:Nodes>
    <d:element m:type="SP.MenuNode">
      <d:CustomProperties m:null="true" />
      <d:FriendlyUrlSegment>electronics</d:FriendlyUrlSegment>
      <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
      <d:Key>16c4c3c8-0309-47f7-9d9b-17e699febce8</d:Key>
      <d:Nodes>
        <d:element m:type="SP.MenuNode">
          <d:CustomProperties m:null="true" />
          <d:FriendlyUrlSegment>audio</d:FriendlyUrlSegment>
          <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
          <d:Key>3e2d5c67-3fad-4cfa-8e1c-8c74fdf3a34b</d:Key>
          <d:Nodes>
            <d:element m:type="SP.MenuNode">
              <d:CustomProperties m:null="true" />
              <d:FriendlyUrlSegment>car-audio</d:FriendlyUrlSegment>
              <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
              <d:Key>e3d271a4-dcbf-464d-a557-23848ccaa54f</d:Key>
              <d:Nodes />
              <d:NodeType m:type="Edm.Int32">1</d:NodeType>
              <d:SimpleUrl></d:SimpleUrl>
              <d:Title>Car audio</d:Title>
            </d:element>
            <d:element m:type="SP.MenuNode">
              <d:CustomProperties m:null="true" />
              <d:FriendlyUrlSegment>headphones</d:FriendlyUrlSegment>
              <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
              <d:Key>7ad146d0-61b5-4b55-9da0-db7eaaa20f4a</d:Key>
              <d:Nodes />
              <d:NodeType m:type="Edm.Int32">1</d:NodeType>
              <d:SimpleUrl></d:SimpleUrl>
              <d:Title>Headphones</d:Title>
            </d:element>
            <d:element m:type="SP.MenuNode">
              <d:CustomProperties m:null="true" />
              <d:FriendlyUrlSegment>mp3</d:FriendlyUrlSegment>
              <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
              <d:Key>7387fe97-52fa-464b-878a-b05d04e7032e</d:Key>
              <d:Nodes />
              <d:NodeType m:type="Edm.Int32">1</d:NodeType>
              <d:SimpleUrl></d:SimpleUrl>
              <d:Title>MP3</d:Title>
            </d:element>
            <d:element m:type="SP.MenuNode">
              <d:CustomProperties m:null="true" />
              <d:FriendlyUrlSegment>speakers</d:FriendlyUrlSegment>
              <d:Hidden m:type="Edm.Boolean">false</d:Hidden>
              <d:Key>65da907c-9565-45f6-a278-cbce7f74ab3d</d:Key>
              <d:Nodes />
              <d:NodeType m:type="Edm.Int32">1</d:NodeType>
              <d:SimpleUrl></d:SimpleUrl>
              <d:Title>Speakers</d:Title>
            </d:element>
          </d:Nodes>
          <d:NodeType m:type="Edm.Int32">1</d:NodeType>
          <d:SimpleUrl></d:SimpleUrl>
          <d:Title>Audio</d:Title>
        </d:element>
      </d:Nodes>
      <d:NodeType m:type="Edm.Int32">1</d:NodeType>
      <d:SimpleUrl></d:SimpleUrl>
      <d:Title>Electronics</d:Title>
    </d:element>
  </d:Nodes>
  <d:SimpleUrl m:null="true" />
  <d:SPSitePrefix>/sites/contoso/</d:SPSitePrefix>
  <d:SPWebPrefix>/sites/contoso/</d:SPWebPrefix>
  <d:StartingNodeKey>2168423f-3fea-4324-a5cb-90be8f079750</d:StartingNodeKey>
  <d:StartingNodeTitle>contoso</d:StartingNodeTitle>
  <d:Version>2012-05-29T12:00:04.4747484Z</d:Version>
</d:MenuState>

```


## <a name="example-response-for-a-search-rest-query-for-a-mobile-app"></a>Beispielantwort für eine Search-REST-Abfrage für eine mobile app
<a name="response_search_rest"> </a>


```

<d:query xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml" m:type="Microsoft.Office.Server.Search.REST.SearchResult">
  <d:ElapsedTime m:type="Edm.Int32">4640</d:ElapsedTime>
  <d:PrimaryQueryResult m:type="Microsoft.Office.Server.Search.REST.QueryResult">
    <d:CustomResults m:null="true"/>
    <d:QueryId>7fea4ced-5789-4067-beab-8f807410b29e</d:QueryId>
    <d:QueryRuleId m:type="Edm.Guid">00000000-0000-0000-0000-000000000000</d:QueryRuleId>
    <d:RefinementResults m:null="true"/>
    <d:RelevantResults m:type="Microsoft.Office.Server.Search.REST.RelevantResults">
      <d:GroupTemplateId m:null="true"/>
      <d:ItemTemplateId m:null="true"/>
      <d:Properties>
        ...
      </d:Properties>
      <d:ResultTitle m:null="true"/>
      <d:ResultTitleUrl m:null="true"/>
      <d:RowCount m:type="Edm.Int32">10</d:RowCount>
      <d:Table m:type="SP.SimpleDataTable">
        <d:Rows>
          ...
        </d:Rows>
      </d:Table>
      <d:TotalRows m:type="Edm.Int32">2048964</d:TotalRows>
      <d:TotalRowsIncludingDuplicates m:type="Edm.Int32">2048964</d:TotalRowsIncludingDuplicates>
    </d:RelevantResults>
    <d:SpecialTermResults m:null="true"/>
  </d:PrimaryQueryResult>
  <d:Properties>
    ...
  </d:Properties>
  <d:SecondaryQueryResults m:null="true"/>
  <d:SpellingSuggestion/>
  <d:TriggeredRules>
  </d:TriggeredRules>
</d:query>
```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  

