---
title: "Erstellen von mobilen Apps für andere Plattformen mit SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 017df869-44fb-4ffe-82fb-4654e01329ad
ms.openlocfilehash: 9332b25b93ea89d0bafc4a7074d1b0895f82f0f8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="build-mobile-apps-for-other-platforms-using-sharepoint"></a>Erstellen von mobilen Apps für andere Plattformen mit SharePoint
Erfahren Sie, wie Sie REST (Representational State Transfer) zum Erstellen einer mobilen SharePoint-App für eine beliebige Plattform verwenden. Mobile Geräte sind heutzutage leistungsfähiger und benutzerfreundlicher geworden. Laptops, Netbooks und Tablet-PCs und Mobiltelefone bieten Mitarbeitern Zugriff auf die Informationen und Anwendungen, die sie für ihre Arbeit benötigen. Und die Entwicklung von Anwendungen für mobile Geräte war noch nie einfacher. Dementsprechend erfordern immer mehr Geschäftsszenarien die Integration von Clientanwendungen in ihre Geschäftsprozessen. In diesem Artikel wird beschrieben, wie mobile Client-Apps in SharePoint integriert werden. Sie können eine mobile App erstellen, um SharePoint-Inhalte von beliebigen Speicherorten zu durchsuchen und eine Verbindung mit SharePoint-Listen und -Bibliotheken zum Zugriff auf Daten herzustellen.
  
    
    

Um eine mobile App zu entwickeln, die mit SharePoint interagiert, können Sie allgemeine Dienste verwenden, auf die über offene Protokolle zugegriffen werden kann. In SharePoint Foundation 2010 wurden die Clientobjektmodelle eingeführt, sodass Entwickler eine Remotekommunikation mit SharePoint über eine Webprogrammiertechnologie ihrer Wahl ausführen konnten: .NET Framework, Microsoft Silverlight oder JavaScript. In SharePoint wird ein REST-Dienst (Representational State Transfer) eingeführt, der mit den Clientobjektmodellen vollständig vergleichbar ist. In SharePoint wird praktisch jede API in den Clientobjektmodellen über einen entsprechenden REST-Endpunkt verfügen. Entwickler können nun über eine beliebige Technologie, die REST-Webanforderungen unterstützt, remote mit dem SharePoint-Objektmodell interagieren. REST kann von jeder beliebigen Programmiersprache genutzt werden, die Sie für Ihre mobile Anwendungsentwicklung verwenden möchten. Sie können grundlegende Erstellungs-, Lese-, Aktualisierungs- und Löschoperationen (Create, Read, Update, Delete: CRUD) durchführen, indem Sie die von SharePoint bereitgestellte REST (Representational State Transfer)-Schnittstelle verwenden. Die REST-Schnittstelle macht alle SharePoint-Entitäten und -Operationen verfügbar, die in den anderen SharePoint-Client-APIs verfügbar sind. Ein Vorteil bei der Verwendung von REST besteht darin, dass Sie keine Verweise auf SharePoint-Bibliotheken oder Clientassemblys hinzufügen müssen. Stattdessen führen Sie HTTP-Anforderungen an die entsprechenden Endpunkte durch, um SharePoint-Entitäten wie Websites, Listen und Listenelemente abzurufen oder zu aktualisieren. Unter  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx) finden Sie eine ausführliche Einführung zur SharePoint-REST-Schnittstelle und ihrer Architektur.
  
    
    


## <a name="rest-endpoints-in-sharepoint"></a>REST-Endpunkte in SharePoint
<a name="BuildMobileAppsInSharePoint2013ForNonWindowsPhone_REST_EndpointsInSharePoint2013"> </a>

Um die REST-Funktionen zu nutzen, die in SharePoint integriert sind, erstellen Sie mithilfe des OData-Standards (Open Data Protocol), welcher der Clientobjektmodell-API entspricht, die Sie verwenden möchten, eine RESTful-HTTP-Anforderung. Der client.svc-Webdienst verarbeitet die HTTP-Anforderung und liefert die entsprechende Antwort im Atom- oder JavaScript Object Notation (JSON)-Format . Die Clientanwendung muss diese Antwort dann analysieren. in Abbildung 1 ist eine allgemeine Ansicht der SharePoint-REST-Architektur dargestellt.
  
    
    

**Abbildung 1. SharePoint-REST-Architektur**

  
    
    

  
    
    
![SharePoint REST-Architektur](../images/SP15Con_BuildSharePointAppsForMobileDevices_Fig2.png)
  
    
    
Die Endpunkte im SharePoint-REST-Dienst entsprechen den Typen und Mitgliedern in den SharePoint-Clientobjektmodellen. Mithilfe von HTTP-Anforderungen können Sie diese REST-Endpunkte verwenden, um typische CRUD-Vorgänge für SharePoint-Artefakte wie Listen und Websites durchzuführen.
  
    
    
Allgemein gilt:
  
    
    

- Endpunkte, die Leseoperationen darstellen, werden HTTP- **GET**-Befehlen zugeordnet.
    
  
- Endpunkte, die Aktualisierungsoperationen darstellen, werden HTTP- **POST**-Befehlen zugeordnet.
    
  
- Endpunkte, die Aktualisierungs- oder Einfügeoperationen darstellen, werden HTTP- **PUT**-Befehlen zugeordnet.
    
  
Bei der Auswahl einer zu verwendenden HTTP-Anforderung sollten Sie Folgendes bedenken:
  
    
    

- Verwenden Sie **POST**, um Artefakte wie Listen und Websites zu erstellen. Der SharePoint-REST-Dienst unterstützt das Senden von **POST**-Befehlen, die Objektdefinitionen enthalten, an Endpunkte, die Sammlungen darstellen.
    
  
- Alle nicht erforderlichen Eigenschaften in **POST**-Operationen werden auf ihre Standardwerte festgelegt. Wenn Sie eine schreibgeschützte Eigenschaft im Rahmen einer **POST**-Operation festzulegen versuchen, gibt der Dienst eine Ausnahme zurück.
    
  
- Verwenden Sie die Operationen **PUT**, **PATCH** und **MERGE**, um vorhandene SharePoint-Objekte zu aktualisieren. Jeder Dienstendpunkt, der eine **set**-Operation für eine Objekteigenschaft darstellt, unterstützt **PUT**-Anforderungen und **MERGE**-Anforderungen. Bei **MERGE**-Anforderungen ist das Festlegen von Eigenschaften optional. Alle Eigenschaften, die Sie nicht explizit festlegen, behalten ihre aktuelle Eigenschaft. Bei **PUT**-Befehlen werden jedoch alle Eigenschaften, die Sie nicht explizit festlegen, auf ihre Standardeigenschaften festgelegt. Darüber hinaus gibt der REST-Dienst eine Ausnahme zurück, wenn Sie bei Verwendung von HTTP- **PUT**-Befehlen nicht alle erforderlichen Eigenschaften in Objektaktualisierungen angeben.
    
  
- Verwenden Sie den HTTP- **DELETE**-Befehl für die spezifische Endpunkt-URL, um das durch den Endpunkt dargestellte SharePoint-Objekt zu löschen. Bei wiederverwendbaren Objekten, wie Listen, Dateien und Listenelementen, führt dies zu einer **Recycle**-Operation. Weitere Informationen finden Sie unter  [Erste Schritte mit den SharePoint REST-Dienst](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx).
    
  

## <a name="authenticate-users-to-sharepoint"></a>Authentifizieren von Benutzern in SharePoint
<a name="BuildMobileAppsInSharePoint2013ForNonWindowsPhone_AuthenticatingNonWindowsAppForSharePoint"> </a>

Um Ihre mobile App mit SharePoint zu authentifizieren, können Sie das Protokoll MS-OFBA verwenden. Weitere Informationen finden Sie unter  [[MS-OFBA]: Formularbasierte Authentifizierungprotokollspezifikation für Office](http://msdn.microsoft.com/library/30c7bbe9-b284-421f-b866-4e7ed4866027%28Office.15%29.aspx). Der Protokollclient ist zum Speichern und Übertragen von Cookies konfiguriert. Der Protokollclient ist von dem Remoteprotokollserver abhängig, um die Identität des Benutzers als ein oder mehrere HTTP-Cookies festzulegen. Nachdem die Identität des Benutzers eingerichtet wurde, sendet der Client dann jedes Cookie bei jeder nachfolgenden HTTP-Anforderung.
  
    
    
Wenn sich ein Benutzer bei SharePoint anmeldet, wird das Token des Benutzers überprüft und dann zum Anmelden bei SharePoint verwendet. Das Token des Benutzers ist ein Sicherheitstoken, das von einem Identitätsanbieter ausgegeben wird. SharePoint unterstützt verschiedene Arten von Authentifizierung. Weitere Informationen finden Sie unter [Authentifizierung, Autorisierung und Sicherheit in SharePoint](authentication-authorization-and-security-in-sharepoint.md). Zum Authentifizieren eines Benutzer können Sie die REST-Schnittstelle verwenden. Beim Autorisierungsprozess wird überprüft, ob ein authentifiziertes Subjekt (eine App oder ein Benutzer, in dessen Namen die App fungiert) über die Berechtigung zum Ausführen bestimmter Vorgänge oder für den Zugriff auf bestimmte Ressourcen (z. B. eine Liste oder einen SharePoint-Dokumentordner) verfügt.
  
    
    
Mit OData können Sie auf eine Datenquelle zugreifen, z. B. eine Datenbank, indem Sie zu einer speziell gestalteten URL navigieren. Dadurch wird ein vereinfachter Ansatz zum Herstellen einer Verbindung und zum Arbeiten mit Datenquellen ermöglicht, die innerhalb einer Organisation gehostet werden. OData ist ein Protokoll, das HTTP, Atom und JavaScript Object Notation (JSON) verwendet, damit Entwickler Anwendungen schreiben können, die mit einer ständig wachsenden Anzahl von Datenquellen kommunizieren können. Microsoft unterstützt die Erstellung dieses Standards als eine Möglichkeit, um den Datenaustausch zwischen Anwendungen und Datenspeichern zu ermöglichen, auf die aus dem Internet zugegriffen werden können. Der neue OData-Connector ermöglicht SharePoint die Kommunikation mit OData-Anbietern. Weitere Informationen finden Sie unter  [OData (Open Data Protocol)](http://www.odata.org).
  
    
    
Der folgende Code veranschaulicht, wie Sie Ihre App für SharePoint mithilfe von REST-Endpunkten für grundlegende oder formularbasierte Authentifizierung authentifizieren. Das folgende Codebeispiel wurde in C# geschrieben, es kann jedoch entsprechend der Anforderung der Plattform eine beliebige andere Programmiersprache zum Erstellen der HTTP-Anforderung verwendet werden.
  
    
    



```cs

string SharePointUrl = "https://Target SharePoint site";

private void AuthenticateToSharePoint(object sender, RoutedEventArgs e)
{
    ODataAuthenticator odataAt = new ODataAuthenticator("<Username>", "<password>");
    odataAt.CookieCachingEnabled = true;
    odataAt.AuthenticationCompleted += new EventHandler<AuthenticationCompletedEventArgs>(odataAt_AuthenticationCompleted);
    odataAt.Authenticate(new Uri(SharePointUrl, UriKind.Absolute));
}

void odataAt_AuthenticationCompleted(object sender, AuthenticationCompletedEventArgs e)
{
    HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(SharePointUrl.ToString() + "/_api/web/lists");
    endpointRequest.Method = "GET";
    endpointRequest.Accept = "application/json;odata=verbose";
          endpointRequest.CookieContainer = (sender as ODataAuthenticator).CookieContainer;
    
    endpointRequest.BeginGetResponse(new AsyncCallback((IAsyncResult res) =>
    {
        HttpWebRequest webReq = res.AsyncState as HttpWebRequest;
        WebResponse response = webReq.EndGetResponse(res);

        HttpWebResponse httpResponse = response as HttpWebResponse;
        HttpStatusCode code = httpResponse.StatusCode;
        this.Dispatcher.BeginInvoke(() =>
        {
            MessageBox.Show(code.ToString());
        });
    }), endpointRequest);
}

```

Zum Authentifizieren eines **HttpWebrequest** für den Endpunkt sollten Sie zuerst eine Authentifizierung für SharePoint mit der **ODataAuthenticator**-Klasse durchführen. Vor dem Aufrufen von **Authenticate**-Methode registrieren Sie das **ODataAuthenticator**-Objekt für das **AuthenticationCompleted**-Ereignis.
  
    
    
Nachdem die Authentifizierung innerhalb des **OnAuthenticationCompleted**-Ereignisses erfolgt ist, können Sie die **CookieContainer**-Eigenschaft im **ODataAuthenticator**-Objekt verwenden, das an das **HttpWebRequest**-Objekt angefügt werden kann, um die REST-Aufrufe für SharePoint zu authentifizieren.
  
    
    

## <a name="work-with-sharepoint-list-items-using-rest"></a>Arbeiten mit SharePoint-Listenelementen mithilfe von REST
<a name="BuildMobileAppsInSharePoint2013ForNonWindowsPhone_WorkingWithTheSharePointListItemUsingREST"> </a>

Das folgende Beispiel zeigt, wie Sie alle Elemente einer Liste **abrufen**.
  
    
    

```

url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: GET
headers:
// MS-OFBA protocol returns a cookie.
  Cookie: cookie


    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Das folgende Beispiel zeigt, wie sie ein bestimmtes Listenelement **abrufen**.
  
    
    



```

url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: GET
headers:
    
// MS-OFBA protocol return a cookie.
  Cookie: cookie
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Der folgende XML-Code zeigt ein Beispiel für die Listenelementeigenschaften, die beim Anfordern des XML-Inhaltstyps zurückgegeben werden.
  
    
    



```XML

<content type="application/xml">
        <m:properties>
        <d:FileSystemObjectType m:type="Edm.Int32">0</d:FileSystemObjectType>
        <d:Id m:type="Edm.Int32">1</d:Id>
        <d:ID m:type="Edm.Int32">1</d:ID>
        <d:ContentTypeId>0x010049564F321A0F0543BA8C6303316C8C0F</d:ContentTypeId>
        <d:Title>an item</d:Title>
        <d:Modified m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Modified>
        <d:Created m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Created>
        <d:AuthorId m:type="Edm.Int32">11</d:AuthorId>
        <d:EditorId m:type="Edm.Int32">11</d:EditorId>
        <d:OData__UIVersionString>1.0</d:OData__UIVersionString>
        <d:Attachments m:type="Edm.Boolean">false</d:Attachments>
        <d:GUID m:type="Edm.Guid">eb6850c5-9a30-4636-b282-234eda8b1057</d:GUID>
    </m:properties>
</content>
```

Das folgende Beispiel zeigt, wie Sie ein Listenelement **erstellen**.
  
> [!NOTE]
> 
> Um diese Operation durchzuführen, müssen Sie die Eigenschaft **ListItemEntityTypeFullName** der Liste kennen und sie als Wert von **type** im Textkörper der HTTP-Anforderung übergeben.
  
    
    




```

url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'Test'}
headers:
    
// MS-OFBA protocol returns a cookie.
  Cookie: cookie
     X-RequestDigest = form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

Das folgende Beispiel zeigt, wie Sie ein Listenelement **aktualisieren**.
  
> [!NOTE]
> Um diese Operation durchzuführen, müssen Sie die Eigenschaft **ListItemEntityTypeFullName** der Liste kennen und sie als Wert von **type** im Textkörper der HTTP-Anforderung übergeben.
  
    
    




```

url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'TestUpdated'}
headers:
// MS-OFBA protocol returns a cookie.
  Cookie: cookie
     X-RequestDigest = form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"MERGE",
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

Das folgende Beispiel zeigt, wie Sie ein Listenelement **löschen**.
  
    
    



```

url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
headers:
// MS-OFBA protocol returns a cookie.
  Cookie: cookie
     X-RequestDigest = form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```

Weitere Informationen finden Sie unter  [Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-REST-Endpunkten](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx).
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Verwenden des SharePoint REST-Diensts](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx)
    
  
-  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [Programmieren mit dem SharePoint REST-Dienst](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [Erste Schritte mit den SharePoint REST-Dienst](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx)
    
  
-  [Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
    
  
-  [Durchführen von REST-Aufrufen mit C# und JavaScript für SharePoint - Demo](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
    
  
-  [Open Data Protocol](http://www.odata.org/)
    
  
-  [Autorisierung und Authentifizierung für Add-Ins in SharePoint](http://msdn.microsoft.com/library/bde5647a-fff1-4b51-b67b-2139de79ce4a%28Office.15%29.aspx)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Microsoft SharePoint SDK für Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  

