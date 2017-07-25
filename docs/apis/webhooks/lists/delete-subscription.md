<span data-ttu-id="28c65-p103">Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. Ein Abonnement kann nur von dem SharePoint-Add-In, das es erstellt hat, gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="28c65-p103">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be deleted by the SharePoint add-in that created it.</span></span>

Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. Ein Abonnement kann nur von dem SharePoint-Add-In, das es erstellt hat, gelöscht werden.

<span data-ttu-id="28c65-116">Umfang</span><span class="sxs-lookup"><span data-stu-id="28c65-116">Scope</span></span> | <span data-ttu-id="28c65-117">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="28c65-117">Permission Rights</span></span> 
------|------------
<span data-ttu-id="28c65-118">Liste</span><span class="sxs-lookup"><span data-stu-id="28c65-118">List</span></span>|<span data-ttu-id="28c65-119">Verwalten</span><span class="sxs-lookup"><span data-stu-id="28c65-119">Manage</span></span>

## <a name="http-request"></a><span data-ttu-id="28c65-120">HTTP-Anforderung</span><span class="sxs-lookup"><span data-stu-id="28c65-120">HTTP request</span></span>

```
DELETE _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a><span data-ttu-id="28c65-121">Beispiel</span><span class="sxs-lookup"><span data-stu-id="28c65-121">Example</span></span>

```http
DELETE _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

## <a name="request-body"></a><span data-ttu-id="28c65-122">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="28c65-122">Request body</span></span>

<span data-ttu-id="28c65-123">Geben Sie für diese Methode keinen Anforderungstext an.</span><span class="sxs-lookup"><span data-stu-id="28c65-123">Do not supply a request body for this method.</span></span>

## <a name="response"></a><span data-ttu-id="28c65-124">Antwort</span><span class="sxs-lookup"><span data-stu-id="28c65-124">Response</span></span>

<span data-ttu-id="28c65-125">Wenn das Abonnement gefunden und erfolgreich gelöscht wird, wird eine `204 No Content`-Antwort zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="28c65-125">If the subscription is found and successfully deleted, then a `204 No Content` response is returned.</span></span>

### <a name="example"></a><span data-ttu-id="28c65-126">Beispiel</span><span class="sxs-lookup"><span data-stu-id="28c65-126">Example</span></span>

```http
HTTP/1.1 204 No Content
```
