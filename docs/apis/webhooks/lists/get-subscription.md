# <a name="get-subscriptions"></a>Abrufen von Abonnements

Ruft ein oder mehrere Webhook-Abonnements in einer SharePoint-Liste ab.

## <a name="permissions"></a>Berechtigungen

### <a name="get-a-single-subscription"></a>Abrufen eines einzelnen Abonnements

Die Anwendung muss mindestens Bearbeitenberechtigungen für die SharePoint-Liste haben, aus der das Abonnement abgerufen wird.

**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**

Sie müssen der Azure AD-Anwendung die in der folgenden Tabelle angegebenen Berechtigungen erteilen. Ein Abonnement kann nur von der Azure AD-Anwendung, die es erstellt hat, abgerufen werden. 

Anwendung | Berechtigung 
------------|------------
Office 365 SharePoint Online|Lese-/Schreibzugriff auf Elemente und Listen in allen Websitesammlungen.

**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**

Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. Ein Abonnement kann nur von dem SharePoint-Add-In, das es erstellt hat, abgerufen werden. 

Umfang | Berechtigungen 
------|------------
Liste|Verwalten

### <a name="get-all-subscriptions"></a>Abrufen aller Abonnements

Die Anwendung muss mindestens Berechtigungen zum Verwalten von Listen für die SharePoint-Liste haben, aus der das Abonnement abgerufen wird.

**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**

Sie müssen der Azure AD-App die in der folgenden Tabelle angegebenen Berechtigungen erteilen. 

Anwendung | Berechtigung 
------------|------------
Office 365 SharePoint Online|Sie benötigen Vollzugriff auf alle Websitesammlungen.

**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**

Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. 

Bereich | Berechtigungen 
------|------------
Liste|Vollzugriff

## <a name="http-request"></a>HTTP-Anforderung

### <a name="get-a-single-subscription"></a>Abrufen eines einzelnen Abonnements

#### <a name="list-webhook"></a>Listen-Webhook
```
GET _api/web/lists('list-id')/subscriptions('id')
```

##### <a name="example"></a>Beispiel

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

#### <a name="request-body"></a>Anforderungstext

Geben Sie für diese Methode keinen Anforderungstext an.

##### <a name="response"></a>Antwort

Dies gibt das Abonnement für die Anzeige durch die aufrufende Anwendung zurück.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "odata.metadata": "https://contoso.sharepoint.com/_api/$metadata#SP.ApiData.Subscriptions/@Element",
  "odata.type": "Microsoft.SharePoint.Webhooks.Subscription",
  "odata.id": "https://contoso.sharepoint.com/_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7')",
  "odata.editLink": "web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7')",
  "expirationDateTime": "2016-04-30T16:17:57Z",
  "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
  "notificationUrl": "https://contoso.azurewebistes.net/api/webhook/handlerequest",
  "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
}
```

### <a name="get-all-subscriptions"></a>Abrufen aller Abonnements

#### <a name="list-webhook"></a>Listen-Webhook
```
GET _api/web/lists('list-id')/subscriptions
```

##### <a name="example"></a>Beispiel

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
```

#### <a name="request-body"></a>Anforderungstext

Geben Sie für diese Methode keinen Anforderungstext an.

##### <a name="response"></a>Antwort

Dies gibt eine Auflistung aller Abonnements in einer SharePoint-Ressource zurück. 

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "odata.metadata": "https://a830edad9050849295j16032914.sharepoint.com/_api/$metadata#SP.ApiData.Subscriptions",
  "value": [
    {
      "odata.type": "Microsoft.SharePoint.Webhooks.Subscription",
      "odata.id": "https://contoso.sharepoint.com/_api/Microsoft.SharePoint.Webhooks.Subscriptionc3175b9c-1491-454f-b5da-980431e36146",
      "odata.editLink": "Microsoft.SharePoint.Webhooks.Subscriptionc3175b9c-1491-454f-b5da-980431e36146",
      "clientState": "{A0A354EC-97D4-4D83-9DDB-144077ADB449}",
      "expirationDateTime": "2016-04-30T16:17:57Z",
      "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
      "notificationUrl": "https://contoso.azurewebsites.net/api/webhook/handlerequest",
      "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
    }
  ]
}
```
