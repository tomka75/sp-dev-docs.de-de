---
title: Aktualisieren eines Abonnements
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6638ad3f3919f9e14497adb7dacc1c1a09c139f6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="update-a-subscription"></a>Aktualisieren eines Abonnements

Aktualisiert ein Webhook-Abonnement in einer SharePoint-Liste.

## <a name="permissions"></a>Berechtigungen

Die Anwendung muss mindestens Bearbeitenberechtigungen für die SharePoint-Liste haben, in der das Abonnement aktualisiert wird.  

**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**

Sie müssen der Azure AD-Anwendung die in der folgenden Tabelle angegebenen Berechtigungen erteilen. Ein Abonnement kann nur von der Azure AD-Anwendung, die es erstellt hat, aktualisiert werden.

Anwendung | Berechtigung 
------------|------------
Office 365 SharePoint Online|Lese-/Schreibzugriff auf Elemente und Listen in allen Websitesammlungen. 

**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**

Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. Ein Abonnement kann nur von dem SharePoint-Add-In, das es erstellt hat, aktualisiert werden.

Umfang | Berechtigungen 
------|------------
Liste|Verwalten

## <a name="http-request"></a>HTTP-Anforderung

```
PATCH _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a>Beispiel

```http
PATCH _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
Content-Type: application/json

{
  "notificationUrl": "https://contoso.azurewebsites.net/api/v2/webhook-receiver",
  "expirationDateTime": "2016-01-03T11:23:00.000Z"
}
```

## <a name="request-body"></a>Anforderungstext

Schließen Sie die folgenden Eigenschaften in die Anforderung ein.

Name | Typ | Beschreibung 
-----|------|------------
notificationUrl|string|Die Dienst-URL, an den Benachrichtigungen gesendet werden.
expirationDateTime|date|Das Datum, an dem die Benachrichtigung abläuft und gelöscht wird.
client-clientState|Zeichenfolge|Optional. Verschlüsselte Zeichenfolge, die bei allen Benachrichtigungen zurück an den Client übergeben wird. Dies können Sie zum Überprüfen von Benachrichtigungen oder zum Kategorisieren unterschiedlicher Abonnements verwenden.


## <a name="response"></a>Antwort

Wenn das Abonnement gefunden und erfolgreich aktualisiert wird, wird eine `204 No Content`-Antwort zurückgegeben.

### <a name="example"></a>Beispiel

```http
HTTP/1.1 204 No Content
```
