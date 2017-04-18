# <a name="create-a-new-subscription"></a>Erstellen eines neuen Abonnements 

Erstellt ein neues Webhook-Abonnement in einer SharePoint-Liste. 

## <a name="permissions"></a>Berechtigungen

Die Anwendung muss mindestens Bearbeitenberechtigungen für die SharePoint-Liste haben, in der das Abonnement erstellt wird.

**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**

Sie müssen der Azure AD-App die in der folgenden Tabelle angegebenen Berechtigungen erteilen:

Anwendung | Berechtigung 
------------|------------
Office 365 SharePoint Online|Lese-/Schreibzugriff auf Elemente und Listen in allen Websitesammlungen.

**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**

Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen:

Bereich | Berechtigungen 
------|------------
Liste|Verwalten

## <a name="http-request"></a>HTTP-Anforderung

```
POST /_api/web/lists('list-id')/subscriptions
```

## <a name="request-body"></a>Anforderungstext

Schließen Sie die folgenden Eigenschaften in die Anforderung ein.

Name | Typ | Beschreibung 
-----|------|------------
resource|string|Die URL der Liste, aus der Benachrichtigungen empfangen werden.
notificationUrl|string|Die Dienst-URL, an den Benachrichtigungen gesendet werden.
expirationDateTime|date|Das Datum, an dem die Benachrichtigung abläuft und gelöscht wird.
client-clientState|string|Optional. Verschlüsselte Zeichenfolge, die bei allen Benachrichtigungen zurück an den Client übergeben wird. Dies können Sie zum Überprüfen von Benachrichtigungen oder zum Kategorisieren unterschiedlicher Abonnements verwenden.


### <a name="example"></a>Beispiel

```http
POST /_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
Accept: application/json
Content-Type: application/json

{
  "resource": "https://contoso.sharepoint.com/_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')",
  "notificationUrl": "https://91e383a5.ngrok.io/api/webhook/handlerequest",
  "expirationDateTime": "2016-04-27T16:17:57+00:00"
}
```

## <a name="response"></a>Antwort

Wenn das Abonnement hinzugefügt wird, wird eine `201 Created`-Antwort zurückgegeben, die das neu erstellte Abonnementobjekt enthält.

### <a name="example"></a>Beispiel

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
    "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
    "expirationDateTime": "2016-04-27T16:17:57Z",    
    "notificationUrl": "https://91e383a5.ngrok.io/api/webhook/handlerequest",
    "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
}
```

## <a name="url-validation"></a>URL-Überprüfung

Bevor ein neues Abonnement erstellt wird, sendet SharePoint eine Anforderung mit einem Überprüfungstoken im Textkörper der Anfrage an die bereitgestellt Dienst-URL. Ihr Dienst muss auf diese Anforderung durch Zurückgeben des Überprüfungstokens antworten.

Wenn der Dienst die Anforderung auf diese Weise nicht überprüfen kann, wird das Abonnement nicht erstellt. Weitere Informationen finden Sie unter [Übersicht über SharePoint-Webhooks](../overview-sharepoint-webhooks).
