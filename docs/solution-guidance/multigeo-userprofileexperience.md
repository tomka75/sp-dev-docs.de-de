---
title: Verwenden von Benutzerprofilen in einem SharePoint Multi-Geo-Mandanten
ms.date: 11/03/2017
ms.openlocfilehash: 85362f0bd67c1e148d8c75d691a67033e880c722
ms.sourcegitcommit: 4ea7e9cb1efb53f89da236282002956739d77418
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="work-with-user-profiles-in-a-sharepoint-multi-geo-tenant"></a>Verwenden von Benutzerprofilen in einem SharePoint Multi-Geo-Mandanten

> **Wichtig:** OneDrive und SharePoint Online Multi-Geo ist derzeit in der Vorschau und kann geändert.

In einem Mandanten Multi-Geo können Sie eine bevorzugte Datenspeicherort für einen Benutzer definieren. Dieser Artikel beschreibt auch zum Suchen der Website eines Benutzers OneDrive und zum Lesen und Aktualisieren von Standard und benutzerdefinierten Benutzerprofileigenschaften.

## <a name="where-are-user-profiles-located-in-a-multi-geo-tenant"></a>Wo befinden sich die Benutzerprofile in einem Mandanten Multi-Geo?
In einem Multi-Geo-Mandanten SharePoint Benutzer Zeitspanne, die die Speicherorte der verschiedenen Geo - beispielsweise einige Benutzer in Nordamerika, sind einige in Europa und So weiter. Dieses Modell gilt auch für Benutzerkonten und persönliche Websites von (OneDrive für Unternehmen). Idealerweise werden die Benutzer und ihre Benutzerkonten und Websites am selben Speicherort Geo an. Um dies, stellen Sie sicher, bevor Sie persönliche Websites erstellen, legen Sie bevorzugte Datenspeicherort des Benutzers auf ihrem Standort Geo. 

Im Beispiel in der folgenden Abbildung dargestellt Benutzer vesa@contoso.onmicrosoft.com in Europa Leben ist und eine bevorzugte Datenspeicherort auf **EUR**festgelegt wurde. Als solche:
 
- Die Standard-Kopie der Profil des Benutzers befindet sich in den Europa Geo-Speicherort.
- Persönliche Website des Benutzers wird in den Europa Geo Speicherort erstellt.

Benutzer bert@contoso.onmicrosoft.com hat seine bevorzugte Datenspeicherort auf **Name**festgelegt. Da er eine persönliche Website in Europa gehostet werden hatte, bevor seine bevorzugte Datenspeicherort festgelegt wurde, bleibt seinem Profil in Europa. 

![World Karte zur Erläuterung von Geo Standardspeicherort in Nordamerika und Satelliten Speicherorte in Europa und Asien, mit Benutzern, geografisch Speicherorte und bevorzugte Datenspeicherorte festlegen](media/multigeo/multigeouserprofiles_intro.png)

Profile und der persönlichen Websites der Benutzer befinden sich in den gleichen Speicherort Geo. Für Benutzer, die nicht mit eine persönliche Website verfügen:

- Wenn sie eine bevorzugte Datenspeicherort festgelegt, befindet sich ihr Profil in diesen Speicherort Geo.
- Wenn sie eine bevorzugte Datenspeicherort nicht eingerichtet haben, ist ihr Profil den Standardspeicherort Geo gespeichert.

Zum Speicherort des Profils eines Benutzers programmgesteuert zu ermitteln, können Sie eine der folgenden Aktionen ausführen:

- Verwenden Sie das SharePoint-Benutzerprofil API. Diese Vorgehensweise wird empfohlen, da sie in allen Szenarien funktioniert. 
- Verwenden Sie Microsoft Graph. Dies gilt für Benutzer, die auch persönliche Websites haben, aber nicht für Benutzer, die nicht über persönliche Websites verfügen.

### <a name="use-the-sharepoint-user-profile-api-to-detect-the-profile-location"></a>Verwenden Sie die SharePoint-Benutzer-Profil-API, um den Speicherort des Profils erkennen
Rufen Sie die SharePoint-Benutzer-Profil-API über REST oder CSOM, um die persönliche Website-Host-URL für ein bestimmtes Konto abzurufen. Diese URL enthält Hosts der persönlichen Websites für persönliche Websites des Benutzers, unabhängig davon, ob die persönliche Website erstellt wurde. Das folgende Beispiel zeigt die REST-Aufrufs.

```
GET https://contoso.sharepoint.com/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)/personalsitehosturl?%40v=%27i%3A0%23.f%7Cmembership%7Cbert%40contoso.onmicrosoft.com%27
```

Wenn Sie c# verwenden, ist CSOM, wie im folgenden Beispiel dargestellt einfacher zu nutzen.

```C#
public string GetUserPersonalSiteHostUrlCSOM(string userPrincipalName)
{
    string result = null;

    PeopleManager peopleManager = new PeopleManager(this.clientContext);
    var userProperties = peopleManager.GetPropertiesFor($"i:0#.f|membership|{userPrincipalName}");
    this.clientContext.Load(userProperties);
    this.clientContext.ExecuteQuery();
    result = userProperties.PersonalSiteHostUrl;

    return result;
}
```

Wenn Sie die Host-URL für persönliche Websites haben, können Sie, die zusammen mit der [Serverfarm mit mehreren geografisch](multigeo-discovery.md) Ermittlungsinformationen den Mandanten Admin-Website-URL für den Speicherort der Geo abgerufen, die dem Profil des Benutzers hostet.

Finden Sie weitere Informationen finden Sie [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .

### <a name="use-microsoft-graph-to-detect-the-users-personal-site-url"></a>Verwenden von Microsoft Graph zum Erkennen von persönlichen Website-URL des Benutzers
Zum Ermitteln des Benutzers persönliche Website-URL in einem Multi-Geo-Mandanten können Sie den folgenden Aufruf von Microsoft Graph verwenden:

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=mySite
```

Wenn Sie die Host-URL für persönliche Websites haben, können Sie, die zusammen mit der [Serverfarm mit mehreren geografisch](multigeo-discovery.md) Ermittlungsinformationen den Mandanten Admin-Website-URL für den Speicherort der Geo abgerufen, die dem Profil des Benutzers hostet.

>**Hinweis:** Wenn der Benutzer eine persönliche Website vorhanden ist, funktionieren diese Vorgehensweise nicht. Verwenden Sie stattdessen die SharePoint-Benutzer-Profil-API.

Finden Sie weitere Informationen finden Sie [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .

## <a name="updating-user-profile-properties"></a>Aktualisieren von Benutzerprofileigenschaften
Verfügbarmachen von Massenupdates für Benutzerprofileigenschaften ist ein häufiges Szenario für Unternehmenskunden. Der Prozess zum Verwenden variiert basierend auf dem Typ der Benutzerprofileigenschaft, den Sie aktualisieren möchten.

### <a name="updating-default-user-profile-properties"></a>Aktualisieren die standardmäßigen Benutzerprofileigenschaften
Einige Benutzerprofileigenschaften sind standardmäßig verfügbar. beispielsweise **Abteilung**, **Mich-Seite**und **PreferredDataLocation**. Es wird empfohlen, die Microsoft Graph-API verwenden, um diese Eigenschaften zu aktualisieren, da Microsoft Graph Geo-geeignet ist. Im folgenden Beispiel wird veranschaulicht, wie die **Mich-Seite** -Eigenschaft für den Benutzer bert@contoso.onmicrosoft.com zu aktualisieren.

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=aboutme
```

Finden Sie weitere Informationen finden Sie [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .

#### <a name="updating-the-preferred-data-location-property"></a>Aktualisieren die bevorzugten Daten Location-Eigenschaft
Bevorzugte Datenspeicherort (**PreferredDataLocation** -Eigenschaft) des Benutzers gibt die bevorzugte Geo-Position für den Benutzer. Dies wirkt sich auf Folgendes:

- Die Geo-Speicherort an, in dem Benutzer persönliche Websites bereitgestellt wird
- Die Geo-Speicherort, in dem der Benutzer Gruppe Websites erstellt werden 

Da die bevorzugte Datenspeicherort eine Standardeigenschaft ist, wird empfohlen, die Microsoft Graph-API verwenden, um diese Konfiguration wie im folgenden Beispiel dargestellt. 

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=preferredDataLocation

PATCH https://graph.microsoft.com/beta/users/bert@contoso.onmicrosoft.com

JSON payload:
{
    "preferredDataLocation" : "eur"
}

```

Finden Sie weitere Informationen finden Sie [MultiGeo.UserPreferredDataLocation](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserPreferredDataLocation) .

### <a name="custom-sharepoint-user-profile-properties"></a>Benutzerdefinierte SharePoint-Benutzerprofileigenschaften
Sie können unternehmensspezifische Benutzerprofileigenschaften von Benutzerprofilen in SharePoint hinzufügen. Für SharePoint Multi-Geo-Mandanten gelten die folgenden Aspekte:

- Benutzerdefinierte Benutzerprofileigenschaften werden auf Standortebene Geo erstellt. Wenn Sie eine Eigenschaft in den Europa Geo Speicherort erstellen, ist diese Eigenschaft in den anderen Geo Speicherorten nicht verfügbar. Es empfiehlt sich erstellen Sie benutzerdefinierte Profileigenschaften an allen Speicherorten von geografisch. Dadurch wird das Risiko, dass Daten bei einer Verschiebung Benutzer über Geo Standorte verloren.
- Sie müssen Lesen und Aktualisieren von benutzerdefinierten Benutzerprofileigenschaften auf Standortebene Geo. Wenn Sie eine benutzerdefinierte Eigenschaft an allen Speicherorten von Geo erstellt haben, müssen Sie die Speicherorte der Geo durchlaufen und aktualisieren Sie die Eigenschaft für alle Benutzer.

```C#
// For SharePoint Online custom properties, use the following approach.
string userPrincipalName = "bert@contoso.onmicrosoft.com";
string userAccountName = $"i:0#.f|membership|{userPrincipalName}";
PeopleManager peopleManager = new PeopleManager(tenantAdminContext);
var propsToRetrieve = new string[] { "CostCenter", "CustomProperty" };
var props = peopleManager.GetUserProfilePropertiesFor(new UserProfilePropertiesForUser(tenantAdminContext, userAccountName, propsToRetrieve));
tenantAdminContext.ExecuteQuery();

int i = 0;
foreach (var prop in props)
{
    Console.WriteLine($"Prop: {propsToRetrieve[i]} Value: {prop}");
    i++;
}

// Update user profile properties
peopleManager.SetSingleValueProfileProperty(userAccountName, "CostCenter", "89786879");
tenantAdminContext.ExecuteQuery();
```

Finden Sie weitere Informationen finden Sie [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .

### <a name="using-the-bulk-user-profile-update-api"></a>Verwenden des Bulk Benutzer Profile Updates API
Die [Massen Benutzerprofil aktualisieren API](https://msdn.microsoft.com/en-us/pnp_articles/bulk-user-profile-update-api-for-sharepoint-online) können Massenupdates an benutzerdefinierten Benutzerprofileigenschaften in einer Serverfarm mit mehreren geografisch Mandanten vornehmen. Beachten Sie Folgendes:

- Diese API auf Standortebene Geo funktioniert und ist nicht Multi-Geo berücksichtigen. Wenn Sie in den Europa Geo Speicherort die API verwenden, werden beispielsweise nur Konten in Europa aktualisiert.
- Wenn Sie eine Importdatei mit Konten in verschiedenen Geo Speicherorte angeben, wird die API nur die Eigenschaften für die Benutzer in diesen Speicherort Geo aktualisiert.


## <a name="see-also"></a>Siehe auch

- [Einführung in die API für Massen Aktualisieren von benutzerdefinierten Benutzerprofileigenschaften für SharePoint Online](bulk-user-profile-update-api-for-sharepoint-online.md)
- [User Profile Batch Update-API-Beispiel](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.BatchUpdate.API)


