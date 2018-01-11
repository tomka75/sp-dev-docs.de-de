# <a name="sharepoint-online-tenant-properties"></a>Eigenschaften des SharePoint Online-Mandanten

> [!NOTE]
> Mandanteneigenschaften sind derzeit in der Vorschau in der ersten Version verfügbar und können geändert werden. Sie werden in Produktionsumgebungen derzeit nicht unterstützt.

Mit Mandanteneigenschaften können Administratoren Eigenschaften im App-Katalog hinzufügen, die von verschiedenen SharePoint-Framework-Komponenten gelesen werden können. Mandanteneigenschaften werden von Mandantenadministratoren mithilfe der [Microsoft SharePoint Online-Verwaltungsshell]((https://technet.microsoft.com/de-DE/library/fp161372.aspx)) verwaltet, die ein PowerShell-Modul zum Verwalten des SharePoint Online-Abonnements in Office 365 darstellt.

## <a name="manage-tenant-properties"></a>Verwalten von Mandanteneigenschaften

Mit der Microsoft SharePoint Online-Verwaltungsshell können Mandantenadministratoren mithilfe von PowerShell Mandanteneigenschaften hinzufügen und entfernen. 

> Laden Sie die Microsoft SharePoint Online-Verwaltungsshell [hier](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunter.

Die folgenden PowerShell-Cmdlets stehen zum Verwalten von Mandanteneigenschaften zur Verfügung:

Da Mandanteneigenschaften im Mandanten-App-Katalog gespeichert werden, müssen Sie die URL der Mandanten-App-Katalog-Websitesammlung in den folgenden Cmdlets angeben.

### <a name="get-spostorageentity"></a>Get-SPOStorageEntity
Gilt für: Office 365, SharePoint Online

Syntax Get-SPOStorageEntity [-Website] <AppCatalogSiteURL> [-Key] <String>

### <a name="set-spostorageentity"></a>Set-SPOStorageEntity
Gilt für: Office 365, SharePoint Online

Syntax Set-SPOStorageEntity [-Website] <AppCatalogSiteURL> [-Key] <String> [-Wert] <String> [-Beschreibung] <String> [-Kommentare] <String>

### <a name="remove-spostorageentity"></a>Remove-SPOStorageEntity
Gilt für: Office 365, SharePoint Online

Syntax Remove-SPOStorageEntity [-Website] <AppCatalogSiteURL> [-Key] <String>

## <a name="reading-tenant-properties"></a>Lesen von Mandanteneigenschaften

Entwickler können Mandanteneigenschaften mit SharePoint-REST-APIs lesen und sie in SharePoint-Framework-Komponenten wie Webparts und Erweiterungen verwenden.

## <a name="http-request"></a>HTTP-Anforderung

### <a name="get-a-tenant-property"></a>Abrufen einer Mandanteneigenschaft

```text
GET _api/web/GetStorageEntity('key')
```

#### <a name="example"></a>Beispiel

```text
GET _api/web/GetStorageEntity('AnalyticsKey')
```

#### <a name="request-body"></a>Anforderungstext

Geben Sie für diese Methode keinen Anforderungstext an.

#### <a name="response"></a>Antwort

Diese Anforderung gibt die Speicherentitätsinformationen für den angegebenen Schlüssel zurück.

```text
HTTP/1.1 200 OK
Content-Type: application/json
{
    "Comment":"Tenant property comment.",
    "Description":"Tenant property description",
    "Value":"Tenant property key value"
}
```
