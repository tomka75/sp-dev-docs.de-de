# <a name="sharepoint-online-tenant-properties"></a><span data-ttu-id="e97e9-101">Eigenschaften des SharePoint Online-Mandanten</span><span class="sxs-lookup"><span data-stu-id="e97e9-101">SharePoint Online Tenant Properties</span></span>

<span data-ttu-id="e97e9-102">Mit Mandanteneigenschaften können Mandantenadministratoren Eigenschaften im App-Katalog hinzufügen, die von verschiedenen SharePoint-Framework-Komponenten gelesen werden können.</span><span class="sxs-lookup"><span data-stu-id="e97e9-102">Tenant Properties allow tenant administrators to add properties in the app catalog that can be read by various SharePoint Framework components.</span></span> <span data-ttu-id="e97e9-103">Mandanteneigenschaften werden von Mandantenadministratoren mithilfe der [Microsoft SharePoint Online-Verwaltungsshell](https://technet.microsoft.com/de-DE/library/fp161372.aspx) verwaltet, die ein PowerShell-Modul zum Verwalten des SharePoint Online-Abonnements in Office 365 darstellt.</span><span class="sxs-lookup"><span data-stu-id="e97e9-103">The Tenant Properties are managed by tenant administrators using the [Microsoft SharePoint Online Management Shell](https://technet.microsoft.com/de-DE/library/fp161372.aspx) which is a PowerShell module to manage your SharePoint Online subscription in the Office 365.</span></span>

## <a name="manage-tenant-properties"></a><span data-ttu-id="e97e9-104">Verwalten von Mandanteneigenschaften</span><span class="sxs-lookup"><span data-stu-id="e97e9-104">Manage tenant properties</span></span>

<span data-ttu-id="e97e9-105">Mit der Microsoft SharePoint Online-Verwaltungsshell können Mandantenadministratoren mithilfe von PowerShell Mandanteneigenschaften hinzufügen und entfernen.</span><span class="sxs-lookup"><span data-stu-id="e97e9-105">Using the Microsoft SharePoint Online Management Shell, tenant administrators can add and remove tenant properties using PowerShell.</span></span> 

> <span data-ttu-id="e97e9-106">Laden Sie die Microsoft SharePoint Online-Verwaltungsshell [hier](https://www.microsoft.com/en-us/download/details.aspx?id=35588) herunter.</span><span class="sxs-lookup"><span data-stu-id="e97e9-106">Download the Microsoft SharePoint Online Management Shell [here](https://www.microsoft.com/en-us/download/details.aspx?id=35588)</span></span>

<span data-ttu-id="e97e9-107">Die folgenden PowerShell-Cmdlets stehen zum Verwalten von Mandanteneigenschaften zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="e97e9-107">The following PowerShell cmdlets are available to manage the tenant properties:</span></span>

<span data-ttu-id="e97e9-108">Da Mandanteneigenschaften im Mandanten-App-Katalog gespeichert werden, müssen Sie die URL der Mandanten-App-Katalog-Websitesammlung in den folgenden Cmdlets angeben.</span><span class="sxs-lookup"><span data-stu-id="e97e9-108">Since tenant properties are stored in the tenant app catalog, you will need to provide the tenant app catalog site collection URL in the cmdlets below.</span></span>

### <a name="get-spostorageentity"></a><span data-ttu-id="e97e9-109">Get-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="e97e9-109">Get-SPOStorageEntity</span></span>
<span data-ttu-id="e97e9-110">Gilt für: Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e97e9-110">Applies to: Office 365, SharePoint Online</span></span>

<span data-ttu-id="e97e9-111">Syntax Get-SPOStorageEntity [-Website] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="e97e9-111">Syntax Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span></span>

### <a name="set-spostorageentity"></a><span data-ttu-id="e97e9-112">Set-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="e97e9-112">Set-SPOStorageEntity</span></span>
<span data-ttu-id="e97e9-113">Gilt für: Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e97e9-113">Applies to: Office 365, SharePoint Online</span></span>

<span data-ttu-id="e97e9-114">Syntax Set-SPOStorageEntity [-Website] <AppCatalogSiteURL> [-Key] <String> [-Wert] <String> [-Beschreibung] <String> [-Kommentare] <String></span><span class="sxs-lookup"><span data-stu-id="e97e9-114">Syntax Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String></span></span>

### <a name="remove-spostorageentity"></a><span data-ttu-id="e97e9-115">Remove-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="e97e9-115">Remove-SPOStorageEntity</span></span>
<span data-ttu-id="e97e9-116">Gilt für: Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e97e9-116">Applies to: Office 365, SharePoint Online</span></span>

<span data-ttu-id="e97e9-117">Syntax Remove-SPOStorageEntity [-Website] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="e97e9-117">Syntax Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span></span>

## <a name="reading-tenant-properties"></a><span data-ttu-id="e97e9-118">Lesen von Mandanteneigenschaften</span><span class="sxs-lookup"><span data-stu-id="e97e9-118">Reading tenant properties</span></span>

<span data-ttu-id="e97e9-119">Entwickler können Mandanteneigenschaften mit SharePoint-REST-APIs lesen und sie in SharePoint-Framework-Komponenten wie Webparts und Erweiterungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="e97e9-119">Developers can read tenant properties using the SharePoint REST APIs and use them in SharePoint Framework components such as web parts and extensions.</span></span>

## <a name="http-request"></a><span data-ttu-id="e97e9-120">HTTP-Anforderung</span><span class="sxs-lookup"><span data-stu-id="e97e9-120">HTTP request</span></span>

### <a name="get-a-tenant-property"></a><span data-ttu-id="e97e9-121">Abrufen einer Mandanteneigenschaft</span><span class="sxs-lookup"><span data-stu-id="e97e9-121">Get a tenant property</span></span>

```text
GET _api/web/GetStorageEntity('key')
```

#### <a name="example"></a><span data-ttu-id="e97e9-122">Beispiel</span><span class="sxs-lookup"><span data-stu-id="e97e9-122">Example</span></span>

```text
GET _api/web/GetStorageEntity('AnalyticsKey')
```

#### <a name="request-body"></a><span data-ttu-id="e97e9-123">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="e97e9-123">Request body</span></span>

<span data-ttu-id="e97e9-124">Geben Sie für diese Methode keinen Anforderungstext an.</span><span class="sxs-lookup"><span data-stu-id="e97e9-124">Do not supply a request body for this method.</span></span>

#### <a name="response"></a><span data-ttu-id="e97e9-125">Antwort</span><span class="sxs-lookup"><span data-stu-id="e97e9-125">Response</span></span>

<span data-ttu-id="e97e9-126">Diese Anforderung gibt die Speicherentitätsinformationen für den angegebenen Schlüssel zurück.</span><span class="sxs-lookup"><span data-stu-id="e97e9-126">This returns the storage entity information for the given key.</span></span>

```text
HTTP/1.1 200 OK
Content-Type: application/json
{
    "Comment":"Tenant property comment.",
    "Description":"Tenant property description",
    "Value":"Tenant property key value"
}
```
