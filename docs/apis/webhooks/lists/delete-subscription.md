# <a name="delete-a-subscription"></a>Löschen eines Abonnements

Löscht ein Webhook-Abonnement aus einer SharePoint-Liste. Nach dem Löschen des Abonnements werden keine Benachrichtigungen mehr übermittelt.

## <a name="permissions"></a>Berechtigungen

Die Anwendung muss mindestens Bearbeitenberechtigungen für die SharePoint-Liste haben, aus der das Abonnement gelöscht wird.

**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**

Sie müssen der Azure AD-App die in der folgenden Tabelle angegebenen Berechtigungen erteilen. Ein Abonnement kann nur von der Azure AD-Anwendung, die es erstellt hat, gelöscht werden.

Anwendung | Berechtigung 
------------|------------
Office 365 SharePoint Online|Lese-/Schreibzugriff auf Elemente und Listen in allen Websitesammlungen.

**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**

Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. Ein Abonnement kann nur von dem SharePoint-Add-In, das es erstellt hat, gelöscht werden.

Umfang | Berechtigungen 
------|------------
Liste|Verwalten

## <a name="http-request"></a>HTTP-Anforderung

```
DELETE _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a>Beispiel

```http
DELETE _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

## <a name="request-body"></a>Anforderungstext

Geben Sie für diese Methode keinen Anforderungstext an.

## <a name="response"></a>Antwort

Wenn das Abonnement gefunden und erfolgreich gelöscht wird, wird eine `204 No Content`-Antwort zurückgegeben.

### <a name="example"></a>Beispiel

```http
HTTP/1.1 204 No Content
```
