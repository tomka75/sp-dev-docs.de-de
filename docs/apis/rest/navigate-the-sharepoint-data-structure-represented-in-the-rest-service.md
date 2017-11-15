---
title: Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 21d0326e9729a0cdb16f03211fae76a76859e5ab
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="navigate-the-sharepoint-data-structure-represented-in-the-rest-service"></a>Navigieren in der im REST-Dienst dargestellten SharePoint-Datenstruktur
Informationen zum Starten von einem REST-Endpunkt für einen gegebenen SharePoint-Element und Navigieren zu und Zugreifen auf dazugehörige Elemente, z. B. übergeordnete Standorte oder die Bibliotheksstruktur, in der sich das jeweilige Element befindet. 
 
## <a name="navigate-from-a-given-url-to-reach-other-sharepoint-resources"></a>Navigieren von einer bestimmten URL zu anderen SharePoint-Ressourcen
Wenn Sie mit dem SharePoint REST-Dienst arbeiten, kennen Sie häufig die URL eines bestimmten SharePoint-Elements, möchten aber auf dazugehörige Elemente zugreifen, z. B. den Ordner oder die Bibliotheksstruktur, in dem/der sich das jeweilige Element befindet. Angenommen, Sie erstellen ein Add-In, bei dem die Benutzer die URL eines Dokuments in eine SharePoint-Bibliothek eingeben. Ihr Add-In muss dann die URL aufgliedern, um die tatsächliche URL der SharePoint-Website zu bestimmen. Anschließend kann das Add-In im Auftrag des Benutzers weitere Anforderungen an die Website stellen, z. B. zum Erstellen, Aktualisieren oder Löschen verwandter Elemente oder Ressourcen. 
 
Zu diesem Zweck muss das Add-in folgende Informationen von SharePoint abfragen:
 
- Die serverrelativen URLs der Website und die Websitesammlung, die die Ressource enthält   
 
- Ein Formulardigest, mit dem Sie Abfragen ausführen können, die den Status der Ressource ändern. Beispiel:  **POST**,  **PUT**,  **MERGE** und  **DELETE**.
    
Das grundlegende Verfahren:

1. Verwenden Sie den Operator `/contextinfo` mit der angegebenen URL, um auf die Adressen der Website und der Websitesammlung und den Formulardigest zuzugreifen. Verwenden Sie den Operator `/contextinfo` in folgendem Format:
    
     `http://server/web/doclib/forms/_api/contextinfo`
    
    Zur Verbesserung der Sicherheit gegenüber websiteübergreifenden Scriptingversuchen akzeptiert der `/contextinfo`-Operator nur **POST**-Anforderungen.
    
 
2. Verwenden Sie für den Zugriff auf zusätzliche Ressourcen bei Bedarf die Objekteigenschaften [SPContextWebInformation](#bk_props), die der `/contextinfo`-Operator zurückgibt.
    
 
 **Verwenden**
 

1. Beginnen Sie mit einer URL zu einem SharePoint-Element. Beispiel:
    
     `http://site/web/doclib/myDocument.docx`
     
2. Entfernen Sie den Namen der spezifischen Ressource vom Ende der URL, damit die URL auf eine Dokumentbibliothek, einen Ordner oder eine Liste verweist. In diesem Fall:
    
     `http://site/web/doclib/`
    
3. Fügen Sie den Zeiger des REST-Dienstes und den `/contextinfo`-Operator an die URL an:
    
     `http://site/web/doclib/_api/contextinfo`
    
4. Lesen Sie den Formulardigest und die Eigenschaften **WebFullUrl** aus der Antwort aus.
    
5. Fügen Sie den Zeiger des REST-Dienstes `_api` an die Web-URL an:
    
6. Verwenden Sie die resultierende URL und den Formulardigest für Anforderungen nach anderen Ressourcen, die Sie benötigen.
    
Sie müssen den Formulardigest nicht übergeben, wenn Sie **GET**-Anforderungen oder Anforderungen mit einem überprüften OAuth-Token ausführen möchten.
 
## <a name="navigate-parent-and-child-sites"></a>Navigieren durch über- und untergeordnete Websites
<a name="bk_sites"> </a> Wenn Sie mithilfe des SharePoint Serverobjektmodells durch die Websitestruktur navigieren, verwenden Sie für den Zugriff auf Objekte, die übergeordnete und untergeordnete Websites darstellen, die Eigenschaften **SPWeb.ParentWeb** und **SPWeb.Webs**.

Die entsprechenden REST Ressourcen – `web/parentweb` und `web/webs`– geben keine Objekte zurück, die Websites darstellen. Der Grund ist, dass der REST-Dienst OData-Standards entspricht und solche Anforderungen durch das Zurückgeben vollständiger Websitedarstellungen ineffizient würden. Stattdessen geben sie ein [WebInfo-Objekt](#bk_webinfo) mit den skalaren Eigenschaften der Website, aber ohne zugehörige Entitätenmengen wie Sammlungen oder Feldsammlungen zurück.
  
Um zu einer bestimmten übergeordneten oder untergeordneten Website zu navigieren, erstellen Sie die entsprechende REST-URL zu dieser Website und verwenden Sie dabei **Id** oder **Title**. Hier können Sie auf die mit der Website verknüpften Entitätenmengen zugreifen.
 
## <a name="navigating-folder-structure"></a>Navigieren durch die Datei- und Ordnerstruktur
<a name="bk_folders"> </a> Der SharePoint REST-Dienst bietet keine Unterstützung für das Durchsuchen der Ordnerhierarchie einer Website über die URL-Konstruktion. Verwenden Sie stattdessen das REST-Äquivalent der Methode **Web.GetFolderByServerRelativeUrl**. Beispiel:
 
 *Durch den REST-Dienst nicht unterstützte Navigation:* 
  
 `/_vti_bin/client.svc/web/lists/SharedDocuments/folder1/stuff/things/Recycle`
 
Durch den REST-Dienst unterstützte Navigation: 
 
 `/_vti_bin/client.svc/web/GetFolderByServerRelativeUrl('SharedDocuments/folder1/stuff/things')/Recycle`.
 

## <a name="spcontextwebinformation-object-properties"></a>SPContextWebInformation-Objekteigenschaften
<a name="bk_props"> </a>

|**Eigenschaft SPContextWebInformation**|**Beschreibung**|
|:-----|:-----|
|**webFullUrl**|Ruft die serverrelative URL der nächstgelegenen Website ab.|
|**siteFullUrl**|Ruft die serverrelative URL des Stamms der Websitesammlung ab, in der die Website enthalten ist. Wenn der Stamm einer Websitesammlung am nächsten gelegen ist, dann entspricht der Wert der Eigenschaft **webFullUrl** der Eigenschaft **siteFullUrl**.|
|**formDigestValue**|Ruft den Formulardigest der Serveranforderung ab.|
|**LibraryVersion**|Ruft die aktuelle Version der REST-Bibliothek ab.|
|**SupportedSchemaVersions**|Ruft die Versionen des Schemas der REST-/CSOM-Bibliothek ab, die unterstützt werden.|

## <a name="webinfo-object"></a>WebInfo-Objekt
<a name="bk_webinfo"> </a>

|**WebInfo-Eigenschaft**|**Beschreibung**|
|:-----|:-----|
|**Created**|Ruft einen Wert ab, der angibt, wann die Website erstellt wurde.|
|**Beschreibung**|Dient zum Abrufen oder Festlegen der Beschreibung der Website.|
|**Id**|Ruft einen Wert ab, der den Websitebezeichner angibt.|
|**Language**|Ruft einen Wert ab, der die Gebietsschema-ID (LCID) für die Sprache angibt, die auf der Website verwendet wird.|
|**LastItemModifiedDate**|Ruft einen Wert ab, der angibt, wann ein Element in der Website zuletzt geändert wurde.|
|**Title**|Dient zum Abrufen oder Festlegen des Titels der Website.|
|**WebTemplateId**|Ruft den Bezeichner der Websitevorlage ab.|

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Grundlegendes zum SharePoint REST-Dienst](get-to-know-the-sharepoint-rest-service.md)
-  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint REST-Endpunkten](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [Arbeiten mit Listen und Listenelementen unter Verwendung von REST](working-with-lists-and-list-items-with-rest.md)
-  [Arbeiten mit Ordnern und Dateien unter Verwendung von REST](working-with-folders-and-files-with-rest.md)
-  [Ermitteln von URIs von SharePoint REST-Dienstendpunkten](determine-sharepoint-rest-service-endpoint-uris.md)
-  [Verwenden von OData-Abfragevorgängen in SharePoint REST-Anforderungen](use-odata-query-operations-in-sharepoint-rest-requests.md)
-  [REST-API-Referenz und Beispiele](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [Synchronisieren von SharePoint-Elementen mit dem REST-Dienst](synchronize-sharepoint-items-using-the-rest-service.md)
-  [Verwenden von ETag-Werten zum Bestimmen der Version von Dokument- und Listenelementen über den REST-Dienst](http://msdn.microsoft.com/library/use-etag-values-through-the-rest-service-to-get-document-list-item-versioning%28Office.15%29.aspx)
    
 

 

 

