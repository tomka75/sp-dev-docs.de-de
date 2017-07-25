<span data-ttu-id="2b478-p102">Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. Ein Abonnement kann nur von dem SharePoint-Add-In, das es erstellt hat, abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="2b478-p102">You must grant the SharePoint add-in the following permission(s) or higher. A subscription can only be retrieved by the SharePoint add-in that created it.</span></span>

Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen. Ein Abonnement kann nur von dem SharePoint-Add-In, das es erstellt hat, abgerufen werden. 

<span data-ttu-id="2b478-116">Umfang</span><span class="sxs-lookup"><span data-stu-id="2b478-116">Scope</span></span> | <span data-ttu-id="2b478-117">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="2b478-117">Permission Rights</span></span> 
------|------------
<span data-ttu-id="2b478-118">Liste</span><span class="sxs-lookup"><span data-stu-id="2b478-118">List</span></span>|<span data-ttu-id="2b478-119">Verwalten</span><span class="sxs-lookup"><span data-stu-id="2b478-119">Manage</span></span>

### <a name="get-all-subscriptions"></a><span data-ttu-id="2b478-120">Abrufen aller Abonnements</span><span class="sxs-lookup"><span data-stu-id="2b478-120">Get all subscriptions</span></span>

<span data-ttu-id="2b478-121">Die Anwendung muss mindestens Berechtigungen zum Verwalten von Listen für die SharePoint-Liste haben, aus der das Abonnement abgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="2b478-121">The application must have manage list permissions to the SharePoint list where the subscription will be retrieved.</span></span>

<span data-ttu-id="2b478-122">**Wenn es sich bei Ihrer Anwendung um eine Microsoft Azure Active Directory (AD)-Anwendung handelt:**</span><span class="sxs-lookup"><span data-stu-id="2b478-122">**If your application is a Microsoft Azure Active Directory (AD) application:**</span></span>

<span data-ttu-id="2b478-123">Sie müssen der Azure AD-App die in der folgenden Tabelle angegebenen Berechtigungen erteilen.</span><span class="sxs-lookup"><span data-stu-id="2b478-123">You must grant the Azure AD app the permissions specified in the following table.</span></span> 

<span data-ttu-id="2b478-124">Anwendung</span><span class="sxs-lookup"><span data-stu-id="2b478-124">Application</span></span> | <span data-ttu-id="2b478-125">Berechtigung</span><span class="sxs-lookup"><span data-stu-id="2b478-125">Permission</span></span> 
------------|------------
<span data-ttu-id="2b478-126">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="2b478-126">Office 365 SharePoint Online</span></span>|<span data-ttu-id="2b478-127">Sie benötigen Vollzugriff auf alle Websitesammlungen.</span><span class="sxs-lookup"><span data-stu-id="2b478-127">Have full control of all site collections.</span></span>

<span data-ttu-id="2b478-128">**Wenn es sich bei Ihrer Anwendung um ein SharePoint-Add-In handelt:**</span><span class="sxs-lookup"><span data-stu-id="2b478-128">**If your application is a SharePoint add-in:**</span></span>

<span data-ttu-id="2b478-129">Sie müssen dem SharePoint-Add-In mindestens die folgenden Berechtigungen erteilen.</span><span class="sxs-lookup"><span data-stu-id="2b478-129">You must grant the SharePoint add-in the following permission(s) or higher.</span></span> 

<span data-ttu-id="2b478-130">Bereich</span><span class="sxs-lookup"><span data-stu-id="2b478-130">Scope</span></span> | <span data-ttu-id="2b478-131">Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="2b478-131">Permission Rights</span></span> 
------|------------
<span data-ttu-id="2b478-132">Liste</span><span class="sxs-lookup"><span data-stu-id="2b478-132">List</span></span>|<span data-ttu-id="2b478-133">Vollzugriff</span><span class="sxs-lookup"><span data-stu-id="2b478-133">Full control</span></span>

## <a name="http-request"></a><span data-ttu-id="2b478-134">HTTP-Anforderung</span><span class="sxs-lookup"><span data-stu-id="2b478-134">HTTP request</span></span>

### <a name="get-a-single-subscription"></a><span data-ttu-id="2b478-135">Abrufen eines einzelnen Abonnements</span><span class="sxs-lookup"><span data-stu-id="2b478-135">Get a single subscription</span></span>

#### <a name="list-webhook"></a><span data-ttu-id="2b478-136">Listen-Webhook</span><span class="sxs-lookup"><span data-stu-id="2b478-136">List webhook</span></span>
```
GET _api/web/lists('list-id')/subscriptions('id')
```

##### <a name="example"></a><span data-ttu-id="2b478-137">Beispiel</span><span class="sxs-lookup"><span data-stu-id="2b478-137">Example</span></span>

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

#### <a name="request-body"></a><span data-ttu-id="2b478-138">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="2b478-138">Request body</span></span>

<span data-ttu-id="2b478-139">Geben Sie für diese Methode keinen Anforderungstext an.</span><span class="sxs-lookup"><span data-stu-id="2b478-139">Do not supply a request body for this method.</span></span>

##### <a name="response"></a><span data-ttu-id="2b478-140">Antwort</span><span class="sxs-lookup"><span data-stu-id="2b478-140">Response</span></span>

<span data-ttu-id="2b478-141">Dies gibt das Abonnement für die Anzeige durch die aufrufende Anwendung zurück.</span><span class="sxs-lookup"><span data-stu-id="2b478-141">This returns the subscription viewable by the calling application.</span></span>

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

### <a name="get-all-subscriptions"></a><span data-ttu-id="2b478-142">Abrufen aller Abonnements</span><span class="sxs-lookup"><span data-stu-id="2b478-142">Get all subscriptions</span></span>

#### <a name="list-webhook"></a><span data-ttu-id="2b478-143">Listen-Webhook</span><span class="sxs-lookup"><span data-stu-id="2b478-143">List webhook</span></span>
```
GET _api/web/lists('list-id')/subscriptions
```

##### <a name="example"></a><span data-ttu-id="2b478-144">Beispiel</span><span class="sxs-lookup"><span data-stu-id="2b478-144">Example</span></span>

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
```

#### <a name="request-body"></a><span data-ttu-id="2b478-145">Anforderungstext</span><span class="sxs-lookup"><span data-stu-id="2b478-145">Request body</span></span>

<span data-ttu-id="2b478-146">Geben Sie für diese Methode keinen Anforderungstext an.</span><span class="sxs-lookup"><span data-stu-id="2b478-146">Do not supply a request body for this method.</span></span>

##### <a name="response"></a><span data-ttu-id="2b478-147">Antwort</span><span class="sxs-lookup"><span data-stu-id="2b478-147">Response</span></span>

<span data-ttu-id="2b478-148">Dies gibt eine Auflistung aller Abonnements in einer SharePoint-Ressource zurück.</span><span class="sxs-lookup"><span data-stu-id="2b478-148">This returns a collection of all subscriptions on a SharePoint resource.</span></span> 

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
