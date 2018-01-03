---
title: "Übersicht über das mobile SharePoint-Objektmodell"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 72319846-d02d-49e7-b830-48eb8f5715cb
ms.openlocfilehash: 171c14d60a6f3063e8a903387a0faad34cd34308
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="overview-of-the-sharepoint-mobile-object-model"></a>Übersicht über das mobile SharePoint-Objektmodell
Informationen Sie zu neuen öffentlichen Klassen im Serverobjektmodell SharePoint und Silverlight-Clientobjektmodell, die zum Entwickeln von integrierter Lösungen für SharePoint und Windows Phone 7.5 verwendet werden.
## <a name="client-object-model-for-mobile-silverlight"></a>Clientobjektmodell für mobile Silverlight
<a name="SP15OM_ClientOM"> </a>

Alle Klassen in diesem Abschnitt werden im **Microsoft.SharePoint.Client** -Namespace. Zusätzlich zu den APIs in diesem Abschnitt können die meisten Klassen und Member im Abschnitt Serverobjektmodell für die SharePoint-Mobilität auch in das Clientobjektmodell aufgerufen werden. Für Klassen, die mit "SP" beginnen, wird der Client-Objekt Modellname der "SP" entfernt. In anderen Fällen wird der Client Modell Objektname angegeben. Elementnamen sind die gleichen in des Clientobjektmodells, es sei denn, in denen anders angegeben.
  
    
    

### <a name="alternateurl-class"></a>AlternateUrl-Klasse

Stellt eine alternative URL für eine Webanwendung und die Zone, für die sie gilt.
  
    
    

```cs

public class AlternateUrl
```


#### <a name="properties"></a>Eigenschaften

 **Uri** (schreibgeschützt)
  
    
    
Ruft den URI der alternativen URL ab.
  
    
    



```cs
public String Uri
```

 **UrlZone** (schreibgeschützt)
  
    
    
Ruft die Zone der alternativen URL an.
  
    
    



```
public UrlZone UrlZone
```

Die UrlZone-Klasse ist die Client-Objektmodellversion der SPUrlZone-Klasse im Serverobjektmodell. Weitere Informationen hierzu finden Sie unter der  [SharePoint 2010 Software Development Kit (SDK)]((http://msdn.microsoft.com/de-DE/library/ee557253.aspx)).
  
    
    

### <a name="authenticationcompletedeventargs-class"></a>AuthenticationCompletedEventArgs-Klasse

Stellt Daten über ein **AuthenticationCompleted** -Ereignis bereit.
  
    
    

```cs
public sealed class AuthenticationCompletedEventArgs : AsyncCompletedEventArgs

```


#### <a name="constructors"></a>Konstruktoren

Initialisiert eine neue Instanz der AuthenticationCompletedEventArgs-Klasse.
  
    
    

```cs

public AuthenticationCompletedEventArgs(Exception error, bool canceled, HttpStatusCode userState)
```

 **Parameter**
  
    
    

-  _error_ ist das Exception-Objekt, wenn es eine Ausnahme ausgelöst wird, in der Authentifizierungsversuch wurde.
    
  
-  _canceled_ ist True, wenn der Authentifizierungsversuch abgebrochen wurde, bevor es erfolgreich oder fehlgeschlagen konnte.
    
  
-  _userState_ ist die HttpStatusCode vom Server zurückgegeben.
    
  

#### <a name="properties"></a>Eigenschaften

 **HttpStatusCode** (schreibgeschützt)
  
    
    
Ruft den Status, die vom Server nach einen Authentifizierungsversuch zurückgegeben.
  
    
    



```cs
public HttpStatusCode HttpStatusCode
```


### <a name="authenticationstatus-enum"></a>AuthenticationStatus-Enumeration

Gibt den aktuellen Status des einen Authentifizierungsversuch.
  
    
    

- **NotStarted**
    
  
- **InProgress**
    
  
- **CompletedSuccess**
    
  
- **CompletedException**
    
  

### <a name="authenticator-class"></a>Authentifizierungsserver-Klasse

Stellt Methoden zum Authentifizieren eines Benutzers auf einer SharePoint-Website bereit.
  
    
    

```
public class Authenticator : ICredentials
```


#### <a name="constructors"></a>Konstruktoren

Initialisiert eine neue Instanz der Klasse an.
  
    
    

```cs
public Authenticator()

public Authenticator(Uri uagServerUrl)
```

 **Parameter**
  
    
    
 _uagServerUrl_ ist die absolute URL eines Servers United Access Gateway (UAG).
  
    
    



```cs

public Authenticator(string userName, string password)
```

 **Parameter**
  
    
    
 _userName_ ist der Name für die Anmeldeinformationen.
  
    
    
 _password_ ist das Kennwort für die Anmeldeinformationen.
  
    
    



```cs
public Authenticator(string userName, string password, string domain)
```

 **Parameter**
  
    
    
 _userName_ ist der Name für die Anmeldeinformationen.
  
    
    
 _password_ ist das Kennwort für die Anmeldeinformationen.
  
    
    
 _domain_ ist der Name der Domäne oder des Computers, auf dem die Anmeldeinformationen überprüft werden, in der Regel die Domäne des aktuellen Benutzers.
  
    
    



```cs
public Authenticator(string userName, string password, Uri uagServerUrl)
```

 **Parameter**
  
    
    
 _userName_ ist der Name für die Anmeldeinformationen.
  
    
    
 _password_ ist das Kennwort für die Anmeldeinformationen.
  
    
    
 _uagServerUrl_ ist die absolute URL eines Servers United Access Gateway (UAG).
  
    
    



```cs
public Authenticator(string userName, string password, string domain, Uri uagServerUrl)
```

 **Parameter**
  
    
    
 _userName_ ist der Name für die Anmeldeinformationen.
  
    
    
 _password_ ist das Kennwort für die Anmeldeinformationen.
  
    
    
 _domain_ ist der Name der Domäne oder des Computers, auf dem die Anmeldeinformationen überprüft werden, in der Regel die Domäne des aktuellen Benutzers.
  
    
    
 _uagServerUrl_ ist die absolute URL eines Servers United Access Gateway (UAG).
  
    
    

#### <a name="methods"></a>Methoden

 **ClearAllApplicationSettings**
  
    
    
Löscht alle Cookies, Anmeldeinformationen und UAG-Einstellungen aus dem Cache.
  
    
    



```cs
public static void ClearAllApplicationSettings
```

 **ClearAllCookies**
  
    
    
Löscht alle gespeicherten Cookies, und die **Status** -Eigenschaft aller **Authenticator** -Objekte auf **NotStarted**festgelegt.
  
    
    



```cs
public static void ClearAllCookies()
```

 **ClearAllCredentials**
  
    
    
Löscht alle Anmeldeinformationen aus dem Cache und die **Status** -Eigenschaft aller **Authenticator** -Objekte auf **NotStarted**festgelegt.
  
    
    



```cs
public static void ClearAllCredentials()
```

 **GetCredential**
  
    
    
Ruft ein Objekt mit Anmeldeinformationen für den angegebenen Uri und Authentifizierungstyp.
  
    
    



```
public NetworkCredential GetCredential(Uri uri, string authType)
```

 **Parameter**
  
    
    

-  _uri_ ist der URI, einschließlich der Port, für die der Client die Authentifizierung bereitstellt.
    
  
-  _authType_ ist die Art der Authentifizierung angefordert.
    
  
Diese Methode ist nur für die anonyme Authentifizierung verwendet. Wenn  _authType_ nicht "Basic" ist, wird ein leeres Objekt zurückgegeben. Weitere Informationen über die **NetworkCredential** -Klasse finden Sie unter [NetworkCredential-Klasse]((http://msdn.microsoft.com/de-DE/library/system.net.networkcredential.aspx)).
  
    
    
 **IsRequestUnauthorized**
  
    
    
Gibt true zurück, wenn die Autorisierung Anforderung aufgrund einer ungültigen Cookie oder Anmeldeinformationen ist fehlgeschlagen.
  
    
    



```cs
public static bool IsRequestUnauthorized(ClientRequestFailedEventArgs failedEventArgs)
```


#### <a name="properties"></a>Eigenschaften

 **AllowSmartRouting**
  
    
    
Ruft ab oder legt diesen fest einen Indikator, ob der smart-routing aktiviert ist.
  
    
    



```
public bool AllowSmartRouting
```

Beim smart routing aktiviert ist, versucht das **Authenticator** -Objekt mit dem Server herstellen, die SharePoint- und dem UAG-Server ausgeführt wird und verwendet, je nachdem, was zuerst als Kommunikationskanal antwortet. Wenn kein UAG-Server vorhanden ist, wird diese Eigenschaft ignoriert. Der Standardwert ist **true**. Wenn **false**, dem UAG-Server immer verwendet wird.
  
    
    
 **AuthenticatorMode**
  
    
    
Ruft ab oder legt den Authentifizierungsmodus fest.
  
    
    



```cs
public ClientAuthenticationMode AuthenticationMode
```

Weitere Informationen zu den **ClientAuthenticationMode** -Enumeration finden Sie weiter unten in diesem Dokument.
  
    
    
 **CookieCachingEnabled**
  
    
    
Ruft ab oder legt diesen fest einen Indikator gibt an, ob Cookies zwischengespeichert werden.
  
    
    



```
public bool CookieCachingEnabled
```

Wenn Sie das Zwischenspeichern von Cookies aktivieren, sollten Sie Sie, dass die Cookies zu einem bestimmten Zeitpunkt ablaufen. Wenn diese abgelaufen sind, wenn **ExecuteQueryAsync** aufgerufen wird, klicken Sie dann der Aufruf fehlschlägt, und der Rückruf für Fehler ausgeführt wird. Entsprechend, wenn Sie diese Eigenschaft auf True festlegen, müssen Sie Code für den Rückruf für Fehler hinzufügen, die den Cache gelöscht, in diesem Fall. Hier ist ein Beispiel, wobei `execQueryArgs` der den Typ **ClientRequestFailedEventArgs** in der Failure-Rückruf **ExecuteQueryAsync**übergeben.
  
    
    



```cs
if (Authenticator.IsRequestUnauthorized(execQueryArgs))
{
    (sender as Authenticator).ClearCookies();
}
```

 **CredentialCachingEnabled**
  
    
    
Ruft ab oder legt diesen fest einen Indikator gibt an, ob die Anmeldeinformationen zwischengespeichert werden.
  
    
    



```cs

public bool CredentialCachingEnabled
```

 **Domain**
  
    
    
Ruft ab oder legt diesen fest, Domäne oder des Computers für die Anmeldeinformationen in der Regel ist dies die Domäne des aktuellen Benutzers.
  
    
    



```cs
public string Domain
```

Wenn diese Eigenschaft auf einen neuen Wert festgelegt ist, wird die **Status** -Eigenschaft auf nicht gestartet festgelegt.
  
    
    
 **NavigateBackAfterAuthentication**
  
    
    
Dient zum Abrufen oder festlegen einen Indikator gibt an, ob der Benutzer wieder auf die vorherige Seite auf der Anmeldeseite von dem navigiert werden soll.
  
    
    



```cs
public bool NavigateBackAfterAuthentication
```

 **Password**
  
    
    
Ruft ab oder legt das Kennwort für die Anmeldeinformationen.
  
    
    



```cs
public string Password
```

Wenn diese Eigenschaft auf einen neuen Wert festgelegt ist, wird die **Status** -Eigenschaft auf **NotStarted**festgelegt.
  
    
    
 **PromptOnFailure**
  
    
    
Ruft ab oder legt diesen fest einen Indikator gibt an, ob der Benutzer aufgefordert werden soll, einen Namen und ein Kennwort eingeben, wenn die erste Authentifizierung ein Fehler auftritt.
  
    
    



```cs
public bool PromptOnFailure
```

 **Status** (schreibgeschützt)
  
    
    
Ruft den Status des Programms zur Authentifizierung ab.
  
    
    



```cs
public AuthenticationStatus Status
```

Finden Sie weiter oben in diesem Dokument, um Informationen über die **AuthenticationStatus** -Klasse.
  
    
    
 **UagServerUrl**
  
    
    
Dient zum Abrufen oder Festlegen der URL des UAG-Server.
  
    
    



```cs
public Uri UagServerUrl
```

 **UserName**
  
    
    
Ruft ab oder legt den Benutzernamen für die Anmeldeinformationen.
  
    
    



```cs
public string UserName
```

Wenn diese Eigenschaft auf einen neuen Wert festgelegt ist, wird die **Status** -Eigenschaft auf **NotStarted**festgelegt.
  
    
    

#### <a name="events"></a>Veranstaltungen

 **AuthenticationCompleted**
  
    
    
Wird ausgelöst, wenn der Authentifizierungsversuch unabhängig davon, ob es erfolgreich abgeschlossen wurde.
  
    
    



```cs
public event EventHandler<AuthenticationCompletedEventArgs> AuthenticationCompleted;
```


### <a name="clientauthenticationmode-enum"></a>ClientAuthenticationMode-Enumeration

Gibt einen Authentifizierungsmodus für ein **Authenticator** -Objekt an. Hierbei handelt es sich um eine vorhandene Enumeration an die, einen neuen Wert **BrowserBasedAuthentication** hinzugefügt wurde.
  
    
    


|**Standard**||
|:-----|:-----|
|**FormsAuthentication** <br/> |Stellt die formularbasierte Authentifizierung-Modus  <br/> |
|**Anonymous** <br/> |Anonymen Zugriffsmodus darstellt  <br/> |
|**BrowserBasedAuthentication** <br/> |Microsoft Office Forms basierte Authentifizierung (MSOFBA) Modus darstellt  <br/> |
   

### <a name="odataauthenticator-class"></a>ODataAuthenticator-Klasse

Stellt Methoden zum Authentifizieren eines Benutzers auf einer SharePoint-Website bereit.
  
    
    

```cs
public class ODataAuthenticator : Authenticator
```


#### <a name="constructors"></a>Konstruktoren

Die Konstruktoren sind identisch mit der übergeordneten Klassenkonstruktoren. Weitere Informationen finden Sie weiter oben in diesem Dokument Authentifizierungsserver-Klasse.
  
    
    

#### <a name="methods"></a>Methoden

 **Authenticate**
  
    
    
Authentifiziert einen Benutzer mit der angegebenen Website.
  
    
    



```cs
public new void Authenticate(Uri serverUrl)
```

Das Schlüsselwort  `new` wird verwendet, da die übergeordnete Klasse eine interne Methode mit demselben Namen verfügt.
  
    
    

#### <a name="properties"></a>Eigenschaften

 **CookieContainer** (schreibgeschützt)
  
    
    
Ruft einen Container mit Cookies für Anfragen auf der Website ab.
  
    
    



```cs
public new CookieContainer CookieContainer
```

Das Schlüsselwort  `new` wird verwendet, da die übergeordnete Klasse eine interne Methode mit demselben Namen verfügt.
  
    
    
 **ResolvedUrl** (schreibgeschützt)
  
    
    
Ruft die URL, die für die Kommunikation mit dem Server verwendet wird, auf dem SharePoint ausgeführt wird, wenn ein **ODataAuthenticator** verwendet wird. Dies ist möglicherweise die URL auf dem UAG-Server veröffentlicht oder, wenn die **AllowSmartRouting** -Eigenschaft auf true festgelegt ist, kann dies die URL der SharePoint-Intranet sein, wenn zuerst erreicht wird die **Authenticate** -Methode aufgerufen wird.
  
    
    



```cs
public Uri ResolvedUrl
```


### <a name="serversettings-class"></a>ServerSettings-Klasse

Stellt eine Methode zum Abrufen von alternativen URLs der Webanwendung, die eine Website enthält.
  
    
    

```cs
public static class ServerSettings
```


#### <a name="methods"></a>Methoden

 **GetAlternateUrls**
  
    
    
Ruft die alternativen URLs der angegebenen Website ab.
  
    
    



```cs
public static ClientObjectList<AlternateUrl> GetAlternateUrls(ClientRuntimeContext context)
```

 **Parameter**
  
    
    
 _context_ ist die ein Objekt, das den aktuellen Clientkontext darstellt.
  
    
    
Finden Sie weiter oben in diesem Dokument, um Informationen über die **AlternateUrl** -Klasse.
  
    
    

## <a name="server-object-model-for-sharepoint-mobility"></a>Objektmodell für Mobilität mit SharePoint Server
<a name="SP15OM_ServerOM"> </a>

Alle Klassen in diesem Abschnitt werden im **Microsoft.SharePoint** -Namespace. Es sei denn, in denen angegeben werden sind diese ebenfalls in das Clientobjektmodell verfügbar. Für Klassen, die mit "SP" beginnen, wird der Client-Objekt Modellname der "SP" entfernt. In anderen Fällen wird der Client Modell Objektname angegeben. Elementnamen sind die gleichen in des Clientobjektmodells, es sei denn, in denen anders angegeben.
  
    
    

### <a name="geolocationfieldcontrol-class"></a>GeolocationFieldControl-Klasse

(Nicht verfügbar im Client Object Model). 
  
    
    
Steuert das Rendern von Feldern **SPFieldGeolocation**. Ein Objekt dieses Typs wird als der Wert der **FieldRenderingControl** -Eigenschaft eines **SPFieldGeolocation** -Objekts verwendet.
  
    
    



```cs
public class GeolocationFieldControl : BaseFieldControl
```

Im Zusammenhang mit dieser Klasse Beachten Sie außerdem, dass es zwei renderingvorlagen, eines für den Anzeigemodus und einen für New- und Edit-Modus gibt. Sie sind in der Datei % SHAREPOINTROOT%\\TEMPLATE\\ControlTemplates\\DefaultTemplates.ascx definiert.
  
    
    

#### <a name="fields"></a>Felder

Die folgenden dienen zum Rendern des Felds in der neuen und bearbeiteten Modi verwendet.
  
    
    

```cs
protected TextBox m_latitudeBox;
protected TextBox m_longitudeBox;
protected Label m_longitudeLabel;
protected Label m_latitudeLabel;
```


#### <a name="methods"></a>Methoden

Mit dieser Klasse sind keine nicht abgeleitete öffentlichen Eigenschaften eingeführt. Standard Außerkraftsetzungen von einigen abgeleiteten Methoden sind vorhanden, wie in der folgenden Tabelle angegeben.
  
    
    


|**Method**|**This override???**|
|:-----|:-----|
|CreateChildControls  <br/> |Erstellt die untergeordneten Steuerelemente einschließlich ein JavaScript Map-Steuerelement für den Anzeigemodus.  <br/> |
|Konferenzzustandsobjekt  <br/> |Verschiebt den Fokus auf das Längengrad Textbox untergeordnete Steuerelement.  <br/> |
|OnPreRender  <br/> |Die base-Methode aufgerufen.  <br/> |
|Validieren  <br/> |Überprüft die Breiten- und Längengrad Werte, die in der Benutzeroberfläche (UI) angezeigt werden. Dies wird nicht die Eigenschaften **Longitude** und **Latitude** des zugrunde liegenden **SPFieldGeolocatonValue** -Objekts validiert die abweichen wird, wenn der Benutzer eine oder mehrere der folgenden Werte in der Benutzeroberfläche geändert und die Änderungen noch nicht gespeichert wurde. <br/> |
   

#### <a name="properties"></a>Eigenschaften

Mit dieser Klasse sind keine nicht abgeleitete öffentlichen Eigenschaften eingeführt. Standard Außerkraftsetzungen von einige abgeleiteten Eigenschaften sind vorhanden, wie in der folgenden Tabelle angegeben.
  
    
    


|**Eigenschaft**|**Diese Außerkraftsetzung...**|
|:-----|:-----|
|CssClass  <br/> |Verhält sich wie die übergeordnete Implementierung.  <br/> |
|DefaultTemplateName  <br/> |Gibt "GeolocationField"  <br/> |
|DisplayTemplateName  <br/> |Gibt "GeolocationDisplayField"  <br/> |
|Wert  <br/> |Dient zum Abrufen oder Festlegen des Werts, der mithilfe eines Objekts **SPFieldGeolocationValue** gerendert wird. <br/> |
   

### <a name="spfieldgeolocation-class"></a>SPFieldGeolocation-Klasse

Stellt ein Feld (Spalte), das ein Verzeichnis auf der ganzen Welt von Längengrad, Breiten- und möglicherweise Höhe definierten enthält.
  
    
    

```cs

public class SPFieldGeolocation : SPField
```

Im Zusammenhang mit dieser Klasse wird der Feldtyp **Geolocation** in % _SHAREPOINTROOT%_\\TEMPLATE\\XML\\fldtypes.xml definiert.
  
    
    

#### <a name="constructors-overloaded"></a>Konstruktoren (überladen)

Initialisiert eine neue Instanz der **SPFieldGeolocation** -Klasse.
  
    
    

```cs
public SPFieldGeolocation(SPFieldCollection fields, string fieldName)
public SPFieldGeolocation(SPFieldCollection fields, string fieldName, string displayName)
```

 **Parameter**
  
    
    

-  _fields_ ist die Auflistung der Feldtypen dar, die das neue Feld Typ-Objekt hinzugefügt wird.
    
  
-  _fieldName_ ist ein interner Name des neuen Feldtyps.
    
  
-  _displayName_ ist ein Anzeigename des neuen Feldtyps.
    
  

#### <a name="methods"></a>Methoden

 **GetFieldValueForClientRender**
  
    
    
Ruft den Wert des Felds, sodass es auf dem Client gerendert werden kann.
  
    
    



```cs

public override object GetFieldValueForClientRender(SPItem item, SPControlMode mode)
```

Parameter
  
    
    

-  _item_ ist das aktuelle Listenelement.
    
  
-  _mode_ ist die aktuelle Rendermodus wie neu, bearbeiten oder anzeigen.
    
  
 **GetJsonClientFormFieldSchema**
  
    
    
Ruft das Feldschema als JavaScript Object Notation (JSON) ab.
  
    
    



```cs
public override Dictionary<string, object> GetJsonClientFormFieldSchema(SPControlMode mode)
```

 **Parameter**
  
    
    
 _mode_ ist die aktuelle Rendermodus wie neu, bearbeiten oder anzeigen.
  
    
    
 **ValidateAndParseValue**
  
    
    
Überprüft, ob das angegebene Listenelement nicht null ist, und klicken Sie dann überprüft, ob die Zeichenfolge ist Übereinstimmung Open geografische Consortium (OGC) Standards strukturiert und gibt ihn als ein Objekt, das in der **SPFieldGeolocationValue** -Typ ist.
  
    
    



```cs
public override object ValidateAndParseValue(SPListItem item, string value)
```

 **Parameter**
  
    
    

-  _item_ ist ein Listenelement, das mit dem Wert aktualisiert werden soll.
    
  
-  _value_ ist eine Zeichenfolgendarstellung eines Geolocation-Werts.
    
  
Die folgenden Methoden sind standard Außerkraftsetzungen von geerbten Methoden, die in SharePoint 2010 waren. Die spezifische Informationen für diese Klasse ist in der folgenden Tabelle.
  
    
    


|**Methode**|**Diese Außerkraftsetzung...**|
|:-----|:-----|
|GetFieldValue (String s)  <br/> |Gibt den angegebenen Wert als ein Objekt, das in SPFieldGeolocationValue ist.  <br/> |
|GetFieldValueAsText (Object o)  <br/> |GetValidatedString bindet.  <br/> |
|GetValidatedString (Object o)  <br/> |Überprüft, ob der angegebene Wert ist mit Open geografische Consortium (OGC) Standards strukturiert und wird als Zeichenfolge zurückgegeben.  <br/> |
   

#### <a name="properties"></a>Eigenschaften

 **JSLink**
  
    
    
Ruft den Namen der JavaScript-Datei ab, die die Felder des **SPFieldGeolocation**-Typs rendert, oder legt den Namen fest.
  
> [!NOTE]
> Die JSLink-Eigenschaft wird nicht für Umfrage- oder Ereignislisten unterstützt. Ein SharePoint-Kalender ist eine Ereignisliste. 
  
    
    




```cs
public override string JSLink
```

Der Standardwert ist "clienttemplates.js| Geolocationfieldtemplate.js|SP.Map.js".
  
    
    
 **FieldRenderingMobileWebControl**
  
    
    
Ruft das **SPMobileGeolocationField** -Objekt, das das Feld gerendert wird.
  
    
    



```cs
public override SPMobileBaseFieldControl FieldRenderingMobileControl
```

Diese Eigenschaft ersetzt die veraltete **FieldRenderingMobileControl**.
  
    
    
Die anderen Eigenschaften sind standard Außerkraftsetzungen von geerbten Eigenschaften, die in SharePoint 2010 waren. Die spezifische Informationen für diese Klasse ist in der folgenden Tabelle.
  
    
    


|**Eigenschaft**|**Die Überschreibung...**|
|:-----|:-----|
|FieldValueType  <br/> |Gibt **typeof(SPFieldGeolocationValue)**zurück.  <br/> |
|FieldRenderingControl  <br/> |Gibt ein **GeolocationFieldControl** -Objekt zurück. <br/> |
|Filterbar  <br/> |Gibt **false**zurück.  <br/> |
|Sortierbar  <br/> |Gibt **false**zurück.  <br/> |
|Veraltet.  <br/> FieldRenderingMobileControl  <br/> |Gibt ein **SPMobileGeolocationField** -Objekt zurück. <br/> |
   

### <a name="spfieldgeolocationvalue-class"></a>SPFieldGeolocationValue-Klasse

Stellt ein Verzeichnis auf der ganzen Welt zu durch Längengrad, Breiten- und möglicherweise Höhe definiert.
  
    
    

```cs
public class SPFieldGeolocationValue : SPFieldGeographyValue
```


#### <a name="constructors-overloaded"></a>Konstruktoren (überladen)

Initialisiert eine neue Instanz der **SPFieldGeolocationValue** -Klasse.
  
    
    

```cs
public SPFieldGeolocationValue()
public SPFieldGeolocationValue(string fieldValue)
public SPFieldGeolocationValue(double latitude, double longitude)
public SPFieldGeolocationValue(double latitude, double longitude, double altitude, double measure)

```

 **Parameter**
  
    
    

-  _fieldValue_ ist eine Zeichenfolge in einem der folgenden Formate Well-Known Text (WKT):
    
  - "Point ( _longitude_ _latitude_)", wobei  _longitude_ und _latitude_ Zeichenfolgen aus einer oder mehreren Ziffern, optional einschließlich pro Periode sind (der als Dezimaltrennzeichen interpretiert wird) und optional beginnend mit einem Bindestrich (der als ein negatives interpretiert wird).
    
  
  - "Punkt (_longitude_ _latitude_ _altitude_ _measure_), wobei _longitude_, _latitude_, _altitude_ und _measure_ Zeichenfolgen aus einer oder mehreren Ziffern sind, die optional einen Punkt enthalten (der als Dezimaltrennzeichen interpretiert wird) und optional mit einem Bindestrich beginnen (der als negatives Zeichen interpretiert wird).
    
  
-  _latitude_ ist die Breite und muss zwischen 90,0 und 90,0.
    
  
-  _longitude_ ist die Längengrad und muss zwischen 180,0 und 180,0.
    
  
-  _altitude_ ist die Höhe an.
    
  
-  _measure_ ist eine alternative Bezeichnung des Punkts. Siehe **Measure** -Eigenschaft weiter unten in diesem Abschnitt Weitere Informationen.
    
  

#### <a name="methods"></a>Methoden

 **ToString**
  
    
    
Diese Außerkraftsetzung gibt eine der folgenden, je nachdem, ob der **Altitude** oder **Measure** -Eigenschaft einen Wert ungleich Null zugewiesen wurden.
  
    
    

- Wenn weder Höhe noch Measure einen Null-Wert zugewiesen wurde:
    
    "Point ( _longitude_ _latitude_)", wobei  _longitude_ und _latitude_ Zeichenfolgen aus einer oder mehreren Ziffern, optional einschließlich pro Periode sind (der als Dezimaltrennzeichen interpretiert wird) und optional beginnend mit einem Bindestrich (der als ein negatives interpretiert wird).
    
  
- Andernfalls (mindestens einer der beiden Eigenschaften **Altitude** oder **Measure** wurde ein anderer Wert als Null zugewiesen):
    
    "Punkt (longitude latitude altitude measure), wobei _longitude_,  _latitude_, _altitude_ und _measure_ Zeichenfolgen aus einer oder mehreren Ziffern sind, die optional einen Punkt enthalten (der als Dezimaltrennzeichen interpretiert wird) und optional mit einem Bindestrich beginnen (der als negatives Zeichen interpretiert wird). Wenn **Altitude** oder **Measure** kein anderer Wert als Null zugewiesen wurde, wird der Wert der Eigenschaft **WellKnownText** als 0 gemeldet. Wenn **Altitude** oder **Measure** als 0 gemeldet werden, kann dies daran liegen, dass den Eigenschaften nie ein anderer Wert als Null zugewiesen wurde, aber es kann auch daran liegen, dass eine 0 zugewiesen wurde.
    
  



```cs

public override string ToString()
```

 **ToWellKnownText**
  
    
    
**ToString**bindet.
  
    
    



```cs
public string ToWellKnownText()
```


#### <a name="properties"></a>Eigenschaften

 **Altitude**
  
    
    
Dient zum Abrufen oder festlegen die Höhe des Speicherorts. Die Verwendung dieser Eigenschaft ist optional und die angenommenen--Einheit (beispielsweise Meter) und Nullpunkt (beispielsweise gefährliche Ebene oder Center der Erde) ist benutzerdefiniert.
  
    
    



```cs
public double Altitude
```

 **Latitude**
  
    
    
Dient zum Abrufen oder Festlegen der Breite des Speicherorts.
  
    
    



```cs
public double Latitude
```

Der Wert muss zwischen 90,0 und 90,0.
  
    
    
 **Longitude**
  
    
    
Dient zum Abrufen oder festlegen die Länge des Speicherorts.
  
    
    



```cs
public double Longitude
```

Der Wert muss zwischen 180,0 und 180,0.
  
    
    
 **Measure**
  
    
    
Ruft ab oder legt eine alternative Bezeichnung des Punkts Speicherort. Wenn der Punkt entlang einer fahren mit Datenpunkten Meilenstein ist, konnte beispielsweise diese Eigenschaft verwendet werden, die die Nummer des Meilensteins enthalten soll, die am nächsten liegt der Punkt ist. Wenn der Punkt in einem öffentlichen camping Bereich mit nummerierten Zeltplätze ist, konnte diese Eigenschaft verwendet werden, die die Anzahl der der nächste Campsite enthalten soll. Die Semantik der-Eigenschaft ist vollständig benutzergesteuerten und deren Verwendung ist optional.
  
    
    



```cs
public double Measure
```


### <a name="spfieldtype-enum"></a>SPFieldType-Enumeration

Diese Enumeration verfügt über ein neuer Wert hinzugefügt wurde:
  
    
    

```cs
Geolocation
```


### <a name="spphonenotificationcontent-class"></a>SPPhoneNotificationContent-Klasse

Eine Basisklasse für Klassen, die den Inhalt einer Benachrichtigung Telefon darstellen. Abgeleitete Klassen müssen deklarieren Sie eine oder mehrere Felder oder Eigenschaften, die den Inhalt enthalten und müssen die **PreparePayload** -Methode, um den Inhalt in ein Bytearray transformieren implementieren.
  
    
    

```cs
public abstract class SPPhoneNotificationContent
```


#### <a name="methods"></a>Methoden

 **PreparePayload**
  
    
    
Wenn in einer abgeleiteten Klasse implementiert wird, überträgt den Inhalt in ein Bytearray, die über das Netzwerk mit dem Benachrichtigungsdienst gesendet wird. Es ist keine Standard-Implementierung, damit diese Methode eine abgeleitete Klasse implementiert werden muss.
  
    
    



```cs
protected internal abstract byte[] PreparePayload();
```


#### <a name="properties"></a>Eigenschaften

 **NotificationType** (schreibgeschützt)
  
    
    
Ruft den Typ der Benachrichtigung (beispielsweise Kacheln oder Toast) für die Inhalte konzipiert ist.
  
    
    



```cs
public SPPhoneNotificationType NotificationType

```

Informationen zu den **SPPhoneNotificationType**finden Sie weiter unten in diesem Dokument.
  
    
    
 **SubscriberType** (schreibgeschützt)
  
    
    
Ruft den Typ des Abonnenten beispielsweise eine Windows Phone-Gerät ab.
  
    
    



```cs

public SPPhoneNotificationSubscriberType SubscriberType
```

Informationen zu den **SPPhoneNotificationSubscriberType**finden Sie weiter unten in diesem Dokument.
  
    
    

### <a name="spphonenotificationresponse-class"></a>SPPhoneNotificationResponse-Klasse

Stellt das Ergebnis der Versuch, eine Benachrichtigung zu senden.
  
    
    

```cs
public class SPPhoneNotificationResponse
```


#### <a name="methods"></a>Methoden

 **Create**
  
    
    
Erstellt ein **SPPhoneNotificationResponse** -Objekt.
  
    
    



```cs
public static SPPhoneNotificationResponse
Create(SPPhoneNotificationSubscriberType subscriberType, 
SPPhoneNotificationType notificationType, HttpWebResponse response)
```

 **Parameter**
  
    
    

-  _subscriberType_ ist das Gerät, wie beispielsweise Windows Phone 7.5.
    
  
-  _notificationType_ ist der Typ der Benachrichtigung, wie Toast oder Kachel.
    
  
-  _response_ ist die HTTP-Antwortobjekt, das vom Server generiert wurde.
    
  
Weitere Informationen zu **SPPhoneNotificationSubscriberType** und **SPPhoneNotificationType**finden Sie weiter unten in diesem Dokument.
  
    
    

#### <a name="properties"></a>Eigenschaften

 **NotificationType** (schreibgeschützt)
  
    
    
Ruft den Typ der Benachrichtigung (beispielsweise Toast oder nebeneinander).
  
    
    



```cs

public SPPhoneNotificationType NotificationType
```

Informationen zu den SPPhoneNotificationType finden Sie weiter unten in diesem Dokument.
  
    
    
 **ServiceToken** (schreibgeschützt)
  
    
    
Ruft das Token des Notification Service, der in der Benachrichtigung verwendet wurde.
  
    
    



```cs
public string ServiceToken
```

 **StatusCode** (schreibgeschützt)
  
    
    
Ruft den HTTP-Statuscode ab. Eine Zeichenfolgenversion einen **HttpStatusCode** -Wert.
  
    
    



```cs
public string StatusCode
```

 **SubscriberType**
  
    
    
Ruft ab oder legt den Typ des Geräts an die die Benachrichtigung gesendet wurde.
  
    
    



```cs
public SPPhoneNotificationSubscriberType SubscriberType
```

Informationen zu den **SPPhoneNotificationSubscriberType**finden Sie weiter unten in diesem Dokument.
  
    
    
 **TimeStamp** (schreibgeschützt)
  
    
    
Die UTC-Zeit der Benachrichtigung.
  
    
    



```cs
public DateTime Timestamp
```


### <a name="spphonenotificationsubscriber-class"></a>SPPhoneNotificationSubscriber-Klasse

Eine Basisklasse für Klassen, die ein-Abonnent auf einer SharePoint-Anwendung serverseitige einstufen Benachrichtigungen darstellen.
  
    
    

```cs
public abstract class SPPhoneNotificationSubscriber
```


#### <a name="methods"></a>Methoden

Benachrichtigen
  
    
    
Sendet den Inhalt der angegebenen Benachrichtigung an den Abonnenten mit Fehler überprüfen.
  
    
    



```cs
public SPPhoneNotificationResponse Notify(SPPhoneNotificationContent notificationContent)
```

 **Parameter**
  
    
    
 _notificationContent_ werden Informationen über das Ereignis, das die Benachrichtigung auslöste.
  
    
    
Diese Methode kann nicht überschrieben werden. Umschließt die abstrakte **NotifyInternal** -Methode, und stellt sicher, dass bestimmte fehlerüberprüfung durchgeführt wird, wenn **NotifyInternal** aufgerufen wird.
  
    
    
Weitere Informationen zu den Klassen **SPPhoneNotificationContent** und **SPPhoneNotificationResponse** finden Sie weiter oben in diesem Dokument.
  
    
    
 **NotifyInternal**
  
    
    
Wenn Sie in einer abgeleiteten Klasse überschrieben wird, sendet den Inhalt der angegebenen Benachrichtigung an den Abonnenten.
  
    
    



```cs
protected abstract SPPhoneNotificationResponse NotifyInternal(SPPhoneNotificationContent notificationContent);
```

 **Parameter**
  
    
    
 _notificationContent_ werden Informationen über das Ereignis, das die Benachrichtigung auslöste.
  
    
    
Weitere Informationen zu den Klassen **SPPhoneNotificationContent** und **SPPhoneNotificationResponse** finden Sie weiter oben in diesem Dokument.
  
    
    
 **ToString**
  
    
    
Gibt die ausgewählten Eigenschaften des Objekts als Zeichenfolge.
  
    
    



```cs
public override string ToString()
```

Die standardmäßige Implementierung enthält die Eigenschaften **ParentWeb**, **ApplicationTag**und **DeviceAppInstanceId**.
  
    
    
Aktualisieren
  
    
    
Speichert ein (möglicherweise geänderten) **SPPhoneNotificationSubscriber** -Objekt an der Website Abonnenten Store.
  
    
    



```cs
public void Update()
```

 **ValidateSubscriberProperties**
  
    
    
Wenn in einer abgeleiteten Klasse implementiert wird, überprüft die ausgewählte Eigenschaften des Objekts.
  
    
    



```cs
protected abstract void ValidateSubscriberProperties();
```


#### <a name="properties"></a>Eigenschaften

 **CustomArgs**
  
    
    
Dient zum Abrufen oder Festlegen einer benutzerdefinierten Argumente-Zeichenfolge, die den Status des Abonnements Benachrichtigungen darstellt. Diese Zeichenfolge konnte von der Anwendungslogik zur Unterscheidung zwischen seine Benachrichtigung Abonnenten für verschiedene Arten von Benachrichtigungen verwendet werden.
  
    
    



```cs
public string CustomArgs
```

 **DeviceAppInstanceId** (schreibgeschützt)
  
    
    
Ruft eine ID für die spezifische Instanz der Anwendung auf das Telefon oder anderen mobilen Gerät.
  
    
    



```cs
public Guid DeviceAppInstanceId
```

 **LastModifiedTimeStamp** (schreibgeschützt)
  
    
    
Ruft Datum und Uhrzeit der letzten des Abonnenten Änderung.
  
    
    



```cs
public DateTime LastModifiedTimeStamp
```

 **RegistrationTimeStamp** (schreibgeschützt)
  
    
    
Ruft Datum und Uhrzeit des Abonnenten Wenn registriert für Benachrichtigungen.
  
    
    



```cs
public DateTime RegistrationTimeStamp
```

 **ServiceToken**
  
    
    
Ruft ab oder legt diesen fest Channel Übermittlungsinformationen, die von einem Benachrichtigungsdienst, wie etwa Channel-URI benötigt wird.
  
    
    



```cs
public string ServiceToken
```

 **SubscriberType** (schreibgeschützt)
  
    
    
Ruft den Typ des Geräts, wie Windows Phone 7.
  
    
    



```cs
public SPPhoneNotificationSubscriberType SubscriberType
```

Informationen über die **SPPhoneNotificationSubscriberType** -Klasse finden Sie weiter unten in diesem Dokument.
  
    
    
 **User** (schreibgeschützt)
  
    
    
Dient zum Abrufen des registrierten Benutzers für Benachrichtigungen.
  
    
    



```cs
public SPUser User
```


### <a name="spphonenotificationsubscribercollection-class"></a>SPPhoneNotificationSubscriberCollection-Klasse

Eine Auflistung von pushbenachrichtigungsabonnenten. Das Auflistungsobjekt dauert **Int32** Indexer.
  
    
    

```cs
public sealed class SPPhoneNotificationSubscriberCollection : SPBaseCollection
```


#### <a name="properties"></a>Eigenschaften

 **Count**
  
    
    
Ruft die Anzahl der Elemente in der Auflistung ab.
  
    
    



```cs
public override int Count
```


### <a name="spphonenotificationsubscribertype-enum"></a>SPPhoneNotificationSubscriberType-Enumeration

Gibt einen Typ des Geräts, die Benachrichtigungen erhalten kann.
  
    
    


|**Benachrichtigung**|**Gerät**|
|:-----|:-----|
|||
|**WP7** <br/> |Windows Phone 7.5  <br/> |
|**Custom** <br/> |Nur von Windows Phone 7.5  <br/> |
   

### <a name="spphonenotificationtype-enum"></a>SPPhoneNotificationType-Enumeration

Gibt den Typ der Benachrichtigung.
  
    
    


|||
|:-----|:-----|
|**None** <br/> ||
|**Tile** <br/> ||
|**Toast** <br/> ||
|**Raw** <br/> ||
   

### <a name="spweb-class"></a>SPWeb-Klasse

Diese Klasse wurden die folgenden Elemente hinzugefügt.
  
    
    

#### <a name="methods"></a>Methoden

 **DoesPhoneNotificationSubscriberExist**
  
    
    
Ruft einen Wert, der angibt, ob der aktuelle Benutzer ein-Abonnent für die angegebene Instanz der angegebenen app ist.
  
    
    



```cs
public bool DoesPhoneNotificationSubscriberExist(Guid deviceAppInstanceId)
```

 **GetPhoneNotificationSubscriber**
  
    
    
Ruft ein-Abonnent Benachrichtigung mit der angegebenen Anwendung und Telefon IDs aus der Website Abonnementspeicher Benachrichtigungsliste ab.
  
    
    



```cs
public SPPhoneNotificationSubscriber GetPhoneNotificationSubscriber(Guid deviceAppInstanceId)
```

 **Parameter**
  
    
    
 _deviceAppInstanceId_ ist die ID für die Instanz der Anwendung auf einem bestimmten Telefon oder Gerät.
  
    
    
Weitere Informationen über die **SPPhoneNotificationSubscriber** -Klasse finden Sie unter weiter oben in diesem Dokument.
  
    
    
 **GetPhoneNotificationSubscribers** (überladen)
  
    
    
Ruft eine Auflistung von pushbenachrichtigungsabonnenten aus der Website Abonnementspeicher Benachrichtigungsliste, optional Filterung anhand der IDs der Phone-Anwendungen und möglicherweise auch auf eine der folgenden: der Benutzer oder einige benutzerdefinierte Argumente.
  
    
    



```cs
public SPPhoneNotificationSubscriberCollection GetPhoneNotificationSubscribers(string customArgs)
```

> [!NOTE]
> Der Client-Objekt-Modellname lautet **GetPhoneNotificationSubscribersByArgs**. 
  
    
    




```cs
public SPPhoneNotificationSubscriberCollection GetPhoneNotificationSubscribers(string user)

```

> [!NOTE]
> Der Client-Objekt-Modellname lautet **GetPhoneNotificationSubscribersByUser**. 
  
    
    

 **Parameter**
  
    
    

-  _customArgs_ sind zusätzliche benutzerdefinierte Informationen, die möglicherweise einige Benachrichtigung-aktivierte Anwendungen verwenden.
    
  
-  _user_ ist der Benutzer, die für die Benachrichtigungen registriert.
    
  
Weitere Informationen über die **SPPhoneNotificationSubscriberCollection** -Klasse finden Sie unter weiter oben in diesem Dokument.
  
    
    
 **RegisterPhoneNotificationSubscriber**
  
    
    
Phone-app auf einem Telefon zum Empfangen von Benachrichtigungen registriert.
  
    
    



```cs

public SPPhoneNotificationSubscriber RegisterPhoneNotificationSubscriber(SPPhoneNotificationSubscriberType subscriberType, Guid deviceAppInstanceId, string serviceToken)
```

 **Parameter**
  
    
    

-  _subscriberType_ ist der Typ des Geräts, wie Windows Phone 7.
    
  
-  _deviceAppInstanceId_ ist die ID für die Instanz der app auf einem bestimmten Telefon oder Gerät.
    
  
-  _serviceToken_ ist das Token, das vom Benachrichtigungsdienst verwendet wird, die an den Abonnenten Benachrichtigung sendet.
    
  
Informationen zu **SPPhoneNotificationSubscriberType**finden Sie weiter oben in diesem Dokument.
  
    
    
 **UnregisterPhoneNotificationSubscriber**
  
    
    
Hebt die Registrierung einer Phone-app auf einem Telefon aus den Empfang von Benachrichtigungen.
  
    
    



```cs
public void UnregisterPhoneNotificationSubscriber(Guid deviceAppInstanceId)
```

 **Parameter**
  
    
    
 _deviceAppInstanceId_ ist die ID für die Instanz der app auf einem bestimmten Telefon oder Gerät.
  
    
    

#### <a name="properties"></a>Eigenschaften

 **PhoneNotificationSubscribers** (schreibgeschützt)
  
    
    
Ruft eine Auflistung aller das Telefon pushbenachrichtigungsabonnenten anmelden Abonnenten der Website ab.
  
    
    



```cs
public SPPhoneNotificationSubscriberCollection PhoneNotificationSubscribers
```

Informationen über die **SPPhoneNotificationSubscriberCollection** -Klasse finden Sie weiter oben in diesem Dokument.
  
    
    

### <a name="wp7notificationtilecontent-class"></a>WP7NotificationTileContent-Klasse

Stellt den Inhalt der Benachrichtigung über eine Kachel dar.
  
    
    

```cs
public sealed class WP7NotificationTileContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a>Konstruktoren

Initialisiert eine neue Instanz der WP7NotificationTileContent-Klasse.
  
    
    

```cs
public WP7NotificationTileContent()
```


#### <a name="methods"></a>Methoden

 **PreparePayload**
  
    
    
Überträgt den Inhalt in ein Array von **Byte**, die über das Netzwerk mit dem Benachrichtigungsdienst gesendet wird.
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a>Eigenschaften

 **Count**
  
    
    
Dient zum Abrufen oder festlegen die Anzahl der Benachrichtigung. Muss zwischen-1 bis 99 inklusive sein.
  
    
    



```cs
public int Count
```

Das Festlegen von-1 wird die Anzahl die nicht über die Kachel geändert.
  
    
    
 **Title**
  
    
    
Dient zum Abrufen oder Festlegen des Titels der Kachel-Benachrichtigung.
  
    
    



```cs
public string Title
```

 **BackgroundImagePath**
  
    
    
Ruft ab oder legt den Pfad auf die Kachel Hintergrundbild.
  
    
    



```cs
public string BackgroundImagePath
```

 **BackBackgroundImagePath**
  
    
    
Ruft ab oder legt diesen fest das Hintergrundbild des der Rückseite des eine Invertierung Kachel.
  
    
    



```cs
public string BackBackgroundImagePath
```

 **BackContent**
  
    
    
Ruft ab oder legt den Inhalt der Rückseite des eine Invertierung Kachel.
  
    
    



```cs
public string BackContent
```

 **BackTitle**
  
    
    
Ruft ab oder legt des Titels, die auf der Rückseite des eine Invertierung Kachel angezeigt wird.
  
    
    



```cs
public string BackTitle
```

 **TileId**
  
    
    
Dient zum Abrufen oder Festlegen der ID der Kachel.
  
    
    



```cs
public string TileId
```


### <a name="wp7notificationtoastcontent-class"></a>WP7NotificationToastContent-Klasse

Stellt den Inhalt der ein Toast-Benachrichtigung an.
  
    
    

```cs
public sealed class WP7NotificationToastContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a>Konstruktoren

Initialisiert eine neue Instanz der WP7NotificationToastContent-Klasse.
  
    
    

```cs
public WP7NotificationToastContent()
```


#### <a name="methods"></a>Methoden

 **PreparePayload**
  
    
    
Überträgt den Inhalt in ein Array von **Byte**, die über das Netzwerk mit dem Benachrichtigungsdienst gesendet wird.
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a>Eigenschaften

 **Meldung**
  
    
    
Dient zum Abrufen oder Festlegen der Meldung von Toast-Benachrichtigung.
  
    
    



```cs
public string Message
```

 **Title**
  
    
    
Dient zum Abrufen oder Festlegen des Titels der Toast-Benachrichtigung.
  
    
    



```cs
public string Title
```

 **Param**
  
    
    
Ruft ab oder legt diesen fest benutzerdefinierte Einstellungsdaten, die an die empfangende Anwendung übergeben wird, wenn der Benutzer auf die Toast-Benachrichtigung antwortet.
  
    
    



```cs
public string Param
```

Diese Eigenschaft kann zum Übergeben von Informationen an die empfangende Anwendung wie eine URL oder eine Reihe von Name / Wert-Paare verwendet werden.
  
    
    

### <a name="wp7notificationrawcontent-class"></a>WP7NotificationRawContent-Klasse

Stellt den Inhalt einer unformatierte Benachrichtigung.
  
    
    

```cs
public sealed class WP7NotificationRawContent : SPPhoneNotificationContent
```


#### <a name="constructors"></a>Konstruktoren

Initialisiert eine neue Instanz der WP7NotificationRawContent-Klasse.
  
    
    

```cs
public WP7NotificationRawContent()
```


#### <a name="methods"></a>Methoden

 **PreparePayload**
  
    
    
Überträgt den Inhalt in ein Bytearray, die über das Netzwerk mit dem Benachrichtigungsdienst gesendet wird.
  
    
    



```cs
protected internal override byte[] PreparePayload();
```


#### <a name="properties"></a>Eigenschaften

 **Meldung**
  
    
    
Dient zum Abrufen oder festlegen die Meldung, die der unformatierte Benachrichtigung.
  
    
    



```cs
public string Message
```


### <a name="wp7phonenotificationresponse-class"></a>WP7PhoneNotificationResponse-Klasse

Stellt das Ergebnis der Versuch, eine Benachrichtigung an eine Windows Phone 7-Abonnenten gesendet.
  
    
    

```cs
public WP7PhoneNotificationResponse(SPPhoneNotificationType notificationType, HttpWebResponse response)
```

 **Parameter**
  
    
    

-  _notificationType_ ist der Typ der Benachrichtigung, wie Toast oder Kachel.
    
  
-  _response_ ist die HTTP-Antwortobjekt, das vom Server generiert wurde.
    
  
Weitere Informationen zu **SPPhoneNotificationType**finden Sie unter weiter oben in diesem Dokument.
  
    
    

#### <a name="properties"></a>Eigenschaften

 **NotificationStatus** (schreibgeschützt)
  
    
    
Ruft den Status der Benachrichtigung, beispielsweise Erfolg oder das fehlschlagen.
  
    
    



```cs
public string NotificationStatus
```

 **DeviceConnectionStatus** (schreibgeschützt)
  
    
    
Ruft den Status des Geräts zum Zeitpunkt der Benachrichtigung ab.
  
    
    



```cs
public string DeviceConnectionStatus
```

 **SubscriptionStatus** (schreibgeschützt)
  
    
    
Der Abonnementstatus des Geräts zum Zeitpunkt der Benachrichtigung.
  
    
    



```cs
public string SubscriptionStatus
```

 **MessageId** (schreibgeschützt)
  
    
    
Ruft die ID der Nachricht, die in der Benachrichtigung gesendet wurde.
  
    
    



```
public string MessageId
```


## <a name="see-also"></a>Siehe auch
<a name="SP15MobileOM_addlresources"> </a>


-  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Vorgehensweise: Konfigurieren und Verwenden von Pushbenachrichtigungen in SharePoint-apps für Windows Phone](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md)
    
  
-  [Integrieren von Standort- und Kartenfunktionen in SharePoint](integrating-location-and-map-functionality-in-sharepoint.md)
    
  
-  [Übersicht über das SharePoint-Objektmodell für die mobile Clientauthentifizierung](overview-of-the-sharepoint-mobile-client-authentication-object-model.md)
    
  

