---
title: Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online
ms.date: 11/03/2017
ms.openlocfilehash: f758e3aea35bf83519cf48059f33f9846ebc5cd9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="introducing-the-api-for-bulk-updating-custom-user-profile-properties-for-sharepoint-online"></a><span data-ttu-id="96fa7-102">Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="96fa7-102">Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online</span></span>


<span data-ttu-id="96fa7-103">_**Applies to:** SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="96fa7-103">_**Applies to:** SharePoint Online_</span></span>

<span data-ttu-id="96fa7-104">As part of the new Client Side Object Model (CSOM) version (4622.1208 or newer), SharePoint has the ability to bulk import custom user profile properties.</span><span class="sxs-lookup"><span data-stu-id="96fa7-104">As part of the new Client Side Object Model (CSOM) version (4622.1208 or newer), SharePoint has the ability to bulk import custom user profile properties.</span></span> <span data-ttu-id="96fa7-105">Prior to this release, your only option was to take advantage of the user profile CSOM operations for updating specific properties for individual user profiles.</span><span class="sxs-lookup"><span data-stu-id="96fa7-105">Prior to this release, your only option was to take advantage of the user profile CSOM operations for updating specific properties for individual user profiles.</span></span> <span data-ttu-id="96fa7-106">However, this approach is inefficient and too time consuming (especially when dealing with thousands of profiles).</span><span class="sxs-lookup"><span data-stu-id="96fa7-106">However, this approach is inefficient and too time consuming (especially when dealing with thousands of profiles).</span></span>

<span data-ttu-id="96fa7-107">Many enterprises need to replicate custom attributes to the SharePoint user profile service and so a more performant user profile bulk API has been released.</span><span class="sxs-lookup"><span data-stu-id="96fa7-107">Many enterprises need to replicate custom attributes to the SharePoint user profile service and so a more performant user profile bulk API has been released.</span></span>

## <a name="an-overview-of-the-bulk-user-profile-update-process"></a><span data-ttu-id="96fa7-108">An Overview of the Bulk User Profile Update Process</span><span class="sxs-lookup"><span data-stu-id="96fa7-108">An Overview of the Bulk User Profile Update Process</span></span>
<span data-ttu-id="96fa7-109"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="96fa7-109"></span></span>

![Bulk UPA update flow](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess.png)

1. <span data-ttu-id="96fa7-111">User attributes are synchronized from the corporate Active Directory to the Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="96fa7-111">User attributes are synchronized from the corporate Active Directory to the Azure Active Directory.</span></span> <span data-ttu-id="96fa7-112">You can select which attributes are replicated across on-premises and Azure.</span><span class="sxs-lookup"><span data-stu-id="96fa7-112">You can select which attributes are replicated across on-premises and Azure.</span></span>
2. <span data-ttu-id="96fa7-113">A standardized set of attributes are replicated from Azure Active Directory to the SharePoint Online User Profile Store within Office 365.</span><span class="sxs-lookup"><span data-stu-id="96fa7-113">A standardized set of attributes are replicated from Azure Active Directory to the SharePoint Online User Profile Store within Office 365.</span></span> <span data-ttu-id="96fa7-114">Unlke on-premises SharePoint, these attributes cannot be customized.</span><span class="sxs-lookup"><span data-stu-id="96fa7-114">Unlke on-premises SharePoint, these attributes cannot be customized.</span></span>
3. <span data-ttu-id="96fa7-115">A custom synchronization tool taking advantage of the new bulk update APIs.</span><span class="sxs-lookup"><span data-stu-id="96fa7-115">A custom synchronization tool taking advantage of the new bulk update APIs.</span></span> <span data-ttu-id="96fa7-116">This tool uploads a JSON file to the Office 365 tenant and queues the import process.</span><span class="sxs-lookup"><span data-stu-id="96fa7-116">This tool uploads a JSON file to the Office 365 tenant and queues the import process.</span></span> <span data-ttu-id="96fa7-117">This tool can be implemented using managed code (.NET) or as a PowerShell script using the new CSOM APIs.</span><span class="sxs-lookup"><span data-stu-id="96fa7-117">This tool can be implemented using managed code (.NET) or as a PowerShell script using the new CSOM APIs.</span></span>
4. <span data-ttu-id="96fa7-118">A Line of Business (LOB) system, or any external system, which is the source of the information in the JSON file.</span><span class="sxs-lookup"><span data-stu-id="96fa7-118">A Line of Business (LOB) system, or any external system, which is the source of the information in the JSON file.</span></span> <span data-ttu-id="96fa7-119">This could also be a combination of data from Active Directory and any external system.</span><span class="sxs-lookup"><span data-stu-id="96fa7-119">This could also be a combination of data from Active Directory and any external system.</span></span> <span data-ttu-id="96fa7-120">Notice that from an API perspective, the LOB system could even be an on-premises SharePoint 2013 or 2016 farm.</span><span class="sxs-lookup"><span data-stu-id="96fa7-120">Notice that from an API perspective, the LOB system could even be an on-premises SharePoint 2013 or 2016 farm.</span></span>
5. <span data-ttu-id="96fa7-121">An out of the box server side timer job running in SharePoint online which checks for queued import requests and will perform the actual import operation based on the API calls and the information within the provided JSON file.</span><span class="sxs-lookup"><span data-stu-id="96fa7-121">An out of the box server side timer job running in SharePoint online which checks for queued import requests and will perform the actual import operation based on the API calls and the information within the provided JSON file.</span></span>
6. <span data-ttu-id="96fa7-122">Extended user profile information is available within user profiles and can be used for any out of the box or custom functionality in SharePoint online.</span><span class="sxs-lookup"><span data-stu-id="96fa7-122">Extended user profile information is available within user profiles and can be used for any out of the box or custom functionality in SharePoint online.</span></span>

> [!NOTE] 
> <span data-ttu-id="96fa7-123">The import only works for user profile properties which have **not** been set to be editable by end users.</span><span class="sxs-lookup"><span data-stu-id="96fa7-123">The import only works for user profile properties which have **not** been set to be editable by end users.</span></span> <span data-ttu-id="96fa7-124">This is to prevent the user profile import process from overriding any information which an end user has already updated.</span><span class="sxs-lookup"><span data-stu-id="96fa7-124">This is to prevent the user profile import process from overriding any information which an end user has already updated.</span></span> <span data-ttu-id="96fa7-125">Additionally, the import only allows custom properties that are not active directory core properties.</span><span class="sxs-lookup"><span data-stu-id="96fa7-125">Additionally, the import only allows custom properties that are not active directory core properties.</span></span> <span data-ttu-id="96fa7-126">These must be synchronized to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="96fa7-126">These must be synchronized to Azure Active Directory.</span></span> <span data-ttu-id="96fa7-127">For the list of these core directory properties, see the table listed in the FAQ section below.</span><span class="sxs-lookup"><span data-stu-id="96fa7-127">For the list of these core directory properties, see the table listed in the FAQ section below.</span></span>

<span data-ttu-id="96fa7-128">Below is a brief video that demonstrates using the new CSOM API from both managed code (.NET) and from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96fa7-128">Below is a brief video that demonstrates using the new CSOM API from both managed code (.NET) and from PowerShell.</span></span> <span data-ttu-id="96fa7-129">You can find the sample code used, including the sample PowerShell script, in the [Office Dev PnP Code Gallery](http://dev.office.com/patterns-and-practices-detail/7202).</span><span class="sxs-lookup"><span data-stu-id="96fa7-129">You can find the sample code used, including the sample PowerShell script, in the [Office Dev PnP Code Gallery](http://dev.office.com/patterns-and-practices-detail/7202).</span></span>

<iframe id="ytplayer" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/-X_2T0SRUBk?autoplay=0&origin=https://msdn.microsoft.com" frameborder="0"></iframe>

## <a name="import-file-format"></a><span data-ttu-id="96fa7-130">Import File Format</span><span class="sxs-lookup"><span data-stu-id="96fa7-130">Import File Format</span></span>
<span data-ttu-id="96fa7-131"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="96fa7-131"></span></span>

<span data-ttu-id="96fa7-132">The import process uses a JSON file containing the properties and their values.</span><span class="sxs-lookup"><span data-stu-id="96fa7-132">The import process uses a JSON file containing the properties and their values.</span></span> <span data-ttu-id="96fa7-133">Below is the expected structure of that file:</span><span class="sxs-lookup"><span data-stu-id="96fa7-133">Below is the expected structure of that file:</span></span>   

```JSON
{
   "value": [
     {
       "<IdName>": "<UserIdValue_1>",
       "<AttributeName_1>": "<User1_AttributeValue_1>",
       "<AttributeName_2>": "<User1_AttributeValue_2>",
     },
     {
       "<IdName>": "<UserIdValue_2>",
       "<AttributeName_1>": "<User2_AttributeValue_1>",
       "<AttributeName_2>": "<User2_AttributeValue_2>",
     },
     {
       "<IdName>": "<UserIdValue_n>",
       "<AttributeName_1>": "<Usern_AttributeValue_1>",
       "<AttributeName_2>": "<Usern_AttributeValue_2>",
     }
   ]
}
```

<span data-ttu-id="96fa7-134">Below is a simple example file using the format above:</span><span class="sxs-lookup"><span data-stu-id="96fa7-134">Below is a simple example file using the format above:</span></span>

```JSON
{
  "value": [
    {
      "IdName": "vesaj@contoso.com",
      "City": "Helsinki",
      "Office": "Viper"
    },
    {
      "IdName": "bjansen@contoso.com",
      "City": "Brussels",
      "Office": "Beetle"
    },
    {
      "IdName": "unknowperson@contoso.com",
      "City": "None",
      "Office": ""
    },
    {
      "IdName": "erwin@contoso.com",
      "City": "Stockholm",
      "Office": "Elite"
    }
  ]
}
```

<span data-ttu-id="96fa7-135">In the example above, identity resolution is based on the `IdName` property and there are two properties which are being updated called `City` and `Office`.</span><span class="sxs-lookup"><span data-stu-id="96fa7-135">In the example above, identity resolution is based on the `IdName` property and there are two properties which are being updated called `City` and `Office`.</span></span> <span data-ttu-id="96fa7-136">The file contains information for four different accounts within the tenant.</span><span class="sxs-lookup"><span data-stu-id="96fa7-136">The file contains information for four different accounts within the tenant.</span></span> <span data-ttu-id="96fa7-137">Property names used in this source file are not necessarily the same as the names used within the SharePoint Online User Profile Service since we will provide correct property mapping within our code.</span><span class="sxs-lookup"><span data-stu-id="96fa7-137">Property names used in this source file are not necessarily the same as the names used within the SharePoint Online User Profile Service since we will provide correct property mapping within our code.</span></span> 

### <a name="source-data-file-restrictions"></a><span data-ttu-id="96fa7-138">Source Data File Restrictions</span><span class="sxs-lookup"><span data-stu-id="96fa7-138">Source Data File Restrictions</span></span>
<span data-ttu-id="96fa7-139">There are few restrictions on individual source data files:</span><span class="sxs-lookup"><span data-stu-id="96fa7-139">There are few restrictions on individual source data files:</span></span>
- <span data-ttu-id="96fa7-140">Maximum file size: 2GB</span><span class="sxs-lookup"><span data-stu-id="96fa7-140">Maximum file size: 2GB</span></span>
- <span data-ttu-id="96fa7-141">Maximum number of properties: 500,000</span><span class="sxs-lookup"><span data-stu-id="96fa7-141">Maximum number of properties: 500,000</span></span>
- <span data-ttu-id="96fa7-142">The source file must be uploaded to the same SharePoint Online tenant where the process is started</span><span class="sxs-lookup"><span data-stu-id="96fa7-142">The source file must be uploaded to the same SharePoint Online tenant where the process is started</span></span>


## <a name="user-profile-property-import-process"></a><span data-ttu-id="96fa7-143">User Profile Property Import Process</span><span class="sxs-lookup"><span data-stu-id="96fa7-143">User Profile Property Import Process</span></span>
<span data-ttu-id="96fa7-144"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="96fa7-144"></span></span>

<span data-ttu-id="96fa7-145">Here’s the full process:</span><span class="sxs-lookup"><span data-stu-id="96fa7-145">Here’s the full process:</span></span>

1. <span data-ttu-id="96fa7-146">Create or synchronize users in an Office 365 tenant or to the Azure AD associated to it</span><span class="sxs-lookup"><span data-stu-id="96fa7-146">Create or synchronize users in an Office 365 tenant or to the Azure AD associated to it</span></span>
     - <span data-ttu-id="96fa7-147">When users are synchronized to Azure AD, it will also synchronize a standardized set of attributes to the SharePoint Online User Profile Service.</span><span class="sxs-lookup"><span data-stu-id="96fa7-147">When users are synchronized to Azure AD, it will also synchronize a standardized set of attributes to the SharePoint Online User Profile Service.</span></span>
2. <span data-ttu-id="96fa7-148">Create any needed custom properties within the User Profile Service</span><span class="sxs-lookup"><span data-stu-id="96fa7-148">Create any needed custom properties within the User Profile Service</span></span>
     - <span data-ttu-id="96fa7-149">Since there’s no remote APIs for creating custom properties in the User Profile Service, this step must be performed manually for each of the tenants where custom user profile properties are needed (this only needs to be done once per tenant).</span><span class="sxs-lookup"><span data-stu-id="96fa7-149">Since there’s no remote APIs for creating custom properties in the User Profile Service, this step must be performed manually for each of the tenants where custom user profile properties are needed (this only needs to be done once per tenant).</span></span>
     - <span data-ttu-id="96fa7-150">Only user profile properties which are not “allowed to be edited by end users” can be imported.</span><span class="sxs-lookup"><span data-stu-id="96fa7-150">Only user profile properties which are not “allowed to be edited by end users” can be imported.</span></span> <span data-ttu-id="96fa7-151">Trying to import a JSON object property to a user profile property which is marked as “editable by end users” will result in an exception when the CSOM API is called.</span><span class="sxs-lookup"><span data-stu-id="96fa7-151">Trying to import a JSON object property to a user profile property which is marked as “editable by end users” will result in an exception when the CSOM API is called.</span></span>
3. <span data-ttu-id="96fa7-152">Create and upload the JSON file to the Office 365 tenant</span><span class="sxs-lookup"><span data-stu-id="96fa7-152">Create and upload the JSON file to the Office 365 tenant</span></span>
     - <span data-ttu-id="96fa7-153">You’ll need to upload the JSON data file containing the information to be updated to the Office 365 tenant.</span><span class="sxs-lookup"><span data-stu-id="96fa7-153">You’ll need to upload the JSON data file containing the information to be updated to the Office 365 tenant.</span></span>
     - <span data-ttu-id="96fa7-154">In the case of any exception during the import process, SharePoint will provide additional logging information saved in the same document library where the file existed within a new sub folder.</span><span class="sxs-lookup"><span data-stu-id="96fa7-154">In the case of any exception during the import process, SharePoint will provide additional logging information saved in the same document library where the file existed within a new sub folder.</span></span>
     - <span data-ttu-id="96fa7-155">Cleaning of the log files and JSON files are not done automatically and is the responsibility of the custom solution using the API.</span><span class="sxs-lookup"><span data-stu-id="96fa7-155">Cleaning of the log files and JSON files are not done automatically and is the responsibility of the custom solution using the API.</span></span> <span data-ttu-id="96fa7-156">You should consider the life cycle of these files within your implementation.</span><span class="sxs-lookup"><span data-stu-id="96fa7-156">You should consider the life cycle of these files within your implementation.</span></span> <span data-ttu-id="96fa7-157">These files are stored in document libraries so they will be consuming a portion of the assigned storage for the site collection.</span><span class="sxs-lookup"><span data-stu-id="96fa7-157">These files are stored in document libraries so they will be consuming a portion of the assigned storage for the site collection.</span></span>
4. <span data-ttu-id="96fa7-158">Call the bulk UPA Import API for queuing the import job</span><span class="sxs-lookup"><span data-stu-id="96fa7-158">Call the bulk UPA Import API for queuing the import job</span></span>
     - <span data-ttu-id="96fa7-159">Use the CSOM API to queue the import process.</span><span class="sxs-lookup"><span data-stu-id="96fa7-159">Use the CSOM API to queue the import process.</span></span> <span data-ttu-id="96fa7-160">This can be achieved by executing CSOM code using either managed code (.NET) or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96fa7-160">This can be achieved by executing CSOM code using either managed code (.NET) or PowerShell.</span></span>
     - <span data-ttu-id="96fa7-161">The method to queue the job requires property mapping information and the location of the data file.</span><span class="sxs-lookup"><span data-stu-id="96fa7-161">The method to queue the job requires property mapping information and the location of the data file.</span></span> <span data-ttu-id="96fa7-162">This method will quickly execute because it just queues the actual import process, which will later be executed as part of a back end process in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="96fa7-162">This method will quickly execute because it just queues the actual import process, which will later be executed as part of a back end process in SharePoint Online.</span></span>
5. <span data-ttu-id="96fa7-163">Check the status of the import job</span><span class="sxs-lookup"><span data-stu-id="96fa7-163">Check the status of the import job</span></span>
     - <span data-ttu-id="96fa7-164">You can also use remote APIs to check the status of a specific import job or all of the recent import jobs.</span><span class="sxs-lookup"><span data-stu-id="96fa7-164">You can also use remote APIs to check the status of a specific import job or all of the recent import jobs.</span></span> <span data-ttu-id="96fa7-165">To be able to check the status of a specific call, you should store the unique job identifier received as a return value when the job is queued.</span><span class="sxs-lookup"><span data-stu-id="96fa7-165">To be able to check the status of a specific call, you should store the unique job identifier received as a return value when the job is queued.</span></span>


## <a name="csom-api-for-the-bulk-import-process"></a><span data-ttu-id="96fa7-166">CSOM API for the Bulk Import Process</span><span class="sxs-lookup"><span data-stu-id="96fa7-166">CSOM API for the Bulk Import Process</span></span>
<span data-ttu-id="96fa7-167"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="96fa7-167"></span></span>

### <a name="queue-import"></a><span data-ttu-id="96fa7-168">Queue Import</span><span class="sxs-lookup"><span data-stu-id="96fa7-168">Queue Import</span></span>
<span data-ttu-id="96fa7-169">You can queue the import process by calling the [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span><span class="sxs-lookup"><span data-stu-id="96fa7-169">You can queue the import process by calling the [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="96fa7-170">This is an asynchronous call in that it doesn’t download the source data or perform the import, it simply adds a work item to the queue for doing this later.</span><span class="sxs-lookup"><span data-stu-id="96fa7-170">This is an asynchronous call in that it doesn’t download the source data or perform the import, it simply adds a work item to the queue for doing this later.</span></span> <span data-ttu-id="96fa7-171">Here’s the full signature of the method:</span><span class="sxs-lookup"><span data-stu-id="96fa7-171">Here’s the full signature of the method:</span></span>

```c#
public ClientResult<Guid> QueueImportProfileProperties(
                          ImportProfilePropertiesUserIdType idType, 
                          string sourceDataIdProperty, 
                          IDictionary<string, string> propertyMap, 
                          string sourceUri);
```

#### <a name="parameters"></a><span data-ttu-id="96fa7-172">Parameter</span><span class="sxs-lookup"><span data-stu-id="96fa7-172">Parameters</span></span>

<span data-ttu-id="96fa7-173">**idType**: _[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_</span><span class="sxs-lookup"><span data-stu-id="96fa7-173">**idType**: _[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_</span></span>

<span data-ttu-id="96fa7-174">The type of id to use when looking up the user profile.</span><span class="sxs-lookup"><span data-stu-id="96fa7-174">The type of id to use when looking up the user profile.</span></span> <span data-ttu-id="96fa7-175">Possible values are `Email`, `CloudId`, and `PrincipalName`.</span><span class="sxs-lookup"><span data-stu-id="96fa7-175">Possible values are `Email`, `CloudId`, and `PrincipalName`.</span></span> <span data-ttu-id="96fa7-176">Note that regardless of the type, the user must already exist in the User Profile Service for the import to work.</span><span class="sxs-lookup"><span data-stu-id="96fa7-176">Note that regardless of the type, the user must already exist in the User Profile Service for the import to work.</span></span> <span data-ttu-id="96fa7-177">It’s recommended to use the `CloudId` to ensure uniqueness.</span><span class="sxs-lookup"><span data-stu-id="96fa7-177">It’s recommended to use the `CloudId` to ensure uniqueness.</span></span>

<span data-ttu-id="96fa7-178">Property mapping between ID Type and Azure AD property:</span><span class="sxs-lookup"><span data-stu-id="96fa7-178">Property mapping between ID Type and Azure AD property:</span></span>

<span data-ttu-id="96fa7-179">UPA Bulk Import ID Type</span><span class="sxs-lookup"><span data-stu-id="96fa7-179">UPA Bulk Import ID Type</span></span> | <span data-ttu-id="96fa7-180">Azure Directory Attribute</span><span class="sxs-lookup"><span data-stu-id="96fa7-180">Azure Directory Attribute</span></span>
--- | ---
<span data-ttu-id="96fa7-181">CloudId</span><span class="sxs-lookup"><span data-stu-id="96fa7-181">CloudId</span></span> | <span data-ttu-id="96fa7-182">ObjectID</span><span class="sxs-lookup"><span data-stu-id="96fa7-182">ObjectID</span></span>
<span data-ttu-id="96fa7-183">PrincipalName</span><span class="sxs-lookup"><span data-stu-id="96fa7-183">PrincipalName</span></span> | <span data-ttu-id="96fa7-184">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="96fa7-184">userPrincipalName</span></span>
<span data-ttu-id="96fa7-185">E-Mail</span><span class="sxs-lookup"><span data-stu-id="96fa7-185">Email</span></span> | <span data-ttu-id="96fa7-186">mail</span><span class="sxs-lookup"><span data-stu-id="96fa7-186">mail</span></span>

<span data-ttu-id="96fa7-187">**sourceDataIdProperty**: _`System.String`_</span><span class="sxs-lookup"><span data-stu-id="96fa7-187">**sourceDataIdProperty**: _`System.String`_</span></span>

<span data-ttu-id="96fa7-188">The name of the id property in the source data.</span><span class="sxs-lookup"><span data-stu-id="96fa7-188">The name of the id property in the source data.</span></span> <span data-ttu-id="96fa7-189">The value of the property from the source data will be used to lookup the user.</span><span class="sxs-lookup"><span data-stu-id="96fa7-189">The value of the property from the source data will be used to lookup the user.</span></span> <span data-ttu-id="96fa7-190">The User Profile Service property used for the lookup depends on the value of `idType`.</span><span class="sxs-lookup"><span data-stu-id="96fa7-190">The User Profile Service property used for the lookup depends on the value of `idType`.</span></span>

<span data-ttu-id="96fa7-191">**propertyMap**: _`IDictionary<string, string>`_</span><span class="sxs-lookup"><span data-stu-id="96fa7-191">**propertyMap**: _`IDictionary<string, string>`_</span></span>

<span data-ttu-id="96fa7-192">A map from the source property name to the User Profile Service property name.</span><span class="sxs-lookup"><span data-stu-id="96fa7-192">A map from the source property name to the User Profile Service property name.</span></span> <span data-ttu-id="96fa7-193">Note that the User Profile Service properties must already exist.</span><span class="sxs-lookup"><span data-stu-id="96fa7-193">Note that the User Profile Service properties must already exist.</span></span> <span data-ttu-id="96fa7-194">The key is the property name used in the source file, the value is the property name used in the User Profile Service.</span><span class="sxs-lookup"><span data-stu-id="96fa7-194">The key is the property name used in the source file, the value is the property name used in the User Profile Service.</span></span>

<span data-ttu-id="96fa7-195">**sourceUri**: _`System.String`_</span><span class="sxs-lookup"><span data-stu-id="96fa7-195">**sourceUri**: _`System.String`_</span></span>

<span data-ttu-id="96fa7-196">The URI of the source data file to import.</span><span class="sxs-lookup"><span data-stu-id="96fa7-196">The URI of the source data file to import.</span></span> <span data-ttu-id="96fa7-197">The file should not be moved or deleted right away as it may not be downloaded for some time.</span><span class="sxs-lookup"><span data-stu-id="96fa7-197">The file should not be moved or deleted right away as it may not be downloaded for some time.</span></span>

#### <a name="return-value"></a><span data-ttu-id="96fa7-198">Return value</span><span class="sxs-lookup"><span data-stu-id="96fa7-198">Return value</span></span>
<span data-ttu-id="96fa7-199">A Guid that identifies the import job that has been queued.</span><span class="sxs-lookup"><span data-stu-id="96fa7-199">A Guid that identifies the import job that has been queued.</span></span>

#### <a name="example"></a><span data-ttu-id="96fa7-200">Beispiel</span><span class="sxs-lookup"><span data-stu-id="96fa7-200">Example</span></span>
<span data-ttu-id="96fa7-201">Below is an example using C# of how to start the process using the sample input file above:</span><span class="sxs-lookup"><span data-stu-id="96fa7-201">Below is an example using C# of how to start the process using the sample input file above:</span></span>

```c#
// Create an instance of the Office 365 Tenant object. Loading this object is not technically needed for this operation. 
Office365Tenant tenant = new Office365Tenant(ctx);
ctx.Load(tenant);
ctx.ExecuteQuery();

// Type of user identifier ["PrincipalName", "Email", "CloudId"] in the 
// User Profile Service. In this case, we use Email as the identifier at the UPA storage
ImportProfilePropertiesUserIdType userIdType = 
      ImportProfilePropertiesUserIdType.Email;

// Name of the user identifier property within the JSON file
var userLookupKey = "IdName";

var propertyMap = new System.Collections.Generic.Dictionary<string, string>();

// The key is the property in the JSON file, 
// The value is the user profile property Name in the User Profile Service
// Notice that we have 2 custom properties in UPA called 'City' and 'OfficeCode'
propertyMap.Add("City", "City");
propertyMap.Add("Office", "OfficeCode");

// Returns a GUID which can be used to check the status of the execution and the end results
var workItemId = tenant.QueueImportProfileProperties(
      userIdType, userLookupKey, propertyMap, fileUrl
      );

ctx.ExecuteQuery();
```

### <a name="check-the-status-of-an-import-job"></a><span data-ttu-id="96fa7-202">Check the Status of an Import Job</span><span class="sxs-lookup"><span data-stu-id="96fa7-202">Check the Status of an Import Job</span></span>
<span data-ttu-id="96fa7-203">You can also check the status of the User Profile Service import jobs by using the new CSOM APIs.</span><span class="sxs-lookup"><span data-stu-id="96fa7-203">You can also check the status of the User Profile Service import jobs by using the new CSOM APIs.</span></span> <span data-ttu-id="96fa7-204">There are two new methods for this in the Tenant object.</span><span class="sxs-lookup"><span data-stu-id="96fa7-204">There are two new methods for this in the Tenant object.</span></span>

<span data-ttu-id="96fa7-205">You can check status of an individual import job by using the [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span><span class="sxs-lookup"><span data-stu-id="96fa7-205">You can check status of an individual import job by using the [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="96fa7-206">You will need to have the unique identifier of a specific import job provided as a parameter to this method.</span><span class="sxs-lookup"><span data-stu-id="96fa7-206">You will need to have the unique identifier of a specific import job provided as a parameter to this method.</span></span> <span data-ttu-id="96fa7-207">Here’s the full signature of the method:</span><span class="sxs-lookup"><span data-stu-id="96fa7-207">Here’s the full signature of the method:</span></span>

```c#
public ImportProfilePropertiesJobInfo GetImportProfilePropertyJob(Guid jobId);
```

#### <a name="parameters"></a><span data-ttu-id="96fa7-208">Parameter</span><span class="sxs-lookup"><span data-stu-id="96fa7-208">Parameters</span></span>
<span data-ttu-id="96fa7-209">**jobID**: _`System.Guid`_</span><span class="sxs-lookup"><span data-stu-id="96fa7-209">**jobID**: _`System.Guid`_</span></span>

<span data-ttu-id="96fa7-210">The id of the job for which to get the high-level status.</span><span class="sxs-lookup"><span data-stu-id="96fa7-210">The id of the job for which to get the high-level status.</span></span>

#### <a name="return-value"></a><span data-ttu-id="96fa7-211">Return value</span><span class="sxs-lookup"><span data-stu-id="96fa7-211">Return value</span></span>

<span data-ttu-id="96fa7-212">An [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) object with high level status information about the specified job.</span><span class="sxs-lookup"><span data-stu-id="96fa7-212">An [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) object with high level status information about the specified job.</span></span>

#### <a name="example"></a><span data-ttu-id="96fa7-213">Beispiel</span><span class="sxs-lookup"><span data-stu-id="96fa7-213">Example</span></span>
<span data-ttu-id="96fa7-214">Below is an example using C# of retrieving the status of a specific import job using a stored identifier:</span><span class="sxs-lookup"><span data-stu-id="96fa7-214">Below is an example using C# of retrieving the status of a specific import job using a stored identifier:</span></span>

```c#
// Check the status of a specific request based on the job id received when we queued the job
Office365Tenant tenant = new Office365Tenant(ctx);
var job = tenant.GetImportProfilePropertyJob(workItemId);
ctx.Load(job);
ctx.ExecuteQuery();
```

<span data-ttu-id="96fa7-215">You can check the status of all import jobs by using the [`GetImportProfilePropertyJobs`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjobs.aspx) method located in the [Office365Tenant](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span><span class="sxs-lookup"><span data-stu-id="96fa7-215">You can check the status of all import jobs by using the [`GetImportProfilePropertyJobs`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjobs.aspx) method located in the [Office365Tenant](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="96fa7-216">Here’s the full signature of the method:</span><span class="sxs-lookup"><span data-stu-id="96fa7-216">Here’s the full signature of the method:</span></span>

```c#
public ImportProfilePropertiesJobStatusCollection GetImportProfilePropertyJobs(); 
```

#### <a name="return-value"></a><span data-ttu-id="96fa7-217">Return value</span><span class="sxs-lookup"><span data-stu-id="96fa7-217">Return value</span></span>
<span data-ttu-id="96fa7-218">An [`ImportProfilePropertiesJobStatusCollection`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstatuscollection.aspx) object which is a collection of [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) objects with high level status information about each of the jobs.</span><span class="sxs-lookup"><span data-stu-id="96fa7-218">An [`ImportProfilePropertiesJobStatusCollection`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstatuscollection.aspx) object which is a collection of [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) objects with high level status information about each of the jobs.</span></span>

#### <a name="example"></a><span data-ttu-id="96fa7-219">Beispiel</span><span class="sxs-lookup"><span data-stu-id="96fa7-219">Example</span></span>
<span data-ttu-id="96fa7-220">Below is an example using C# of getting the status of all import jobs currently saved in the tenant.</span><span class="sxs-lookup"><span data-stu-id="96fa7-220">Below is an example using C# of getting the status of all import jobs currently saved in the tenant.</span></span> <span data-ttu-id="96fa7-221">These could be already processed or queued jobs:</span><span class="sxs-lookup"><span data-stu-id="96fa7-221">These could be already processed or queued jobs:</span></span>

```c#
// Load all import jobs – old and queued ones
Office365Tenant tenant = new Office365Tenant(ctx);
var jobs = tenant.GetImportProfilePropertyJobs();
ctx.Load(jobs);
ctx.ExecuteQuery();
foreach (var item in jobs)
{
   // Check whatever properties needed
   var state = item.State;
}
```

<span data-ttu-id="96fa7-222">An [`ImportProfilePropertiesJobInfo`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) object returned with the import status information has the following properties.</span><span class="sxs-lookup"><span data-stu-id="96fa7-222">An [`ImportProfilePropertiesJobInfo`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) object returned with the import status information has the following properties.</span></span> 

<span data-ttu-id="96fa7-223">**JobId**: _`System.Guid`_</span><span class="sxs-lookup"><span data-stu-id="96fa7-223">**JobId**: _`System.Guid`_</span></span>

<span data-ttu-id="96fa7-224">The Id of the import job</span><span class="sxs-lookup"><span data-stu-id="96fa7-224">The Id of the import job</span></span>

<span data-ttu-id="96fa7-225">**State**: _[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_</span><span class="sxs-lookup"><span data-stu-id="96fa7-225">**State**: _[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_</span></span>

<span data-ttu-id="96fa7-226">An enum with following values:</span><span class="sxs-lookup"><span data-stu-id="96fa7-226">An enum with following values:</span></span>
- <span data-ttu-id="96fa7-227">`Unknown` - We cannot determine the state of the job</span><span class="sxs-lookup"><span data-stu-id="96fa7-227">`Unknown` - We cannot determine the state of the job</span></span>
- <span data-ttu-id="96fa7-228">`Submitted` - The job has been submitted to the system</span><span class="sxs-lookup"><span data-stu-id="96fa7-228">`Submitted` - The job has been submitted to the system</span></span>
- <span data-ttu-id="96fa7-229">`Processing` - The job is being processed</span><span class="sxs-lookup"><span data-stu-id="96fa7-229">`Processing` - The job is being processed</span></span>
- <span data-ttu-id="96fa7-230">`Queued` - The job has passed validation and queued for import to UPA</span><span class="sxs-lookup"><span data-stu-id="96fa7-230">`Queued` - The job has passed validation and queued for import to UPA</span></span>
- <span data-ttu-id="96fa7-231">`Succeeded` - The job completed with no error</span><span class="sxs-lookup"><span data-stu-id="96fa7-231">`Succeeded` - The job completed with no error</span></span>
- <span data-ttu-id="96fa7-232">`Error` - The job completed with error</span><span class="sxs-lookup"><span data-stu-id="96fa7-232">`Error` - The job completed with error</span></span>

<span data-ttu-id="96fa7-233">**SourceUri**: _`System.String`_</span><span class="sxs-lookup"><span data-stu-id="96fa7-233">**SourceUri**: _`System.String`_</span></span>

<span data-ttu-id="96fa7-234">The URI to the data source file</span><span class="sxs-lookup"><span data-stu-id="96fa7-234">The URI to the data source file</span></span>

<span data-ttu-id="96fa7-235">**Error**: _[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_</span><span class="sxs-lookup"><span data-stu-id="96fa7-235">**Error**: _[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_</span></span>

<span data-ttu-id="96fa7-236">An enum representing the possible error:</span><span class="sxs-lookup"><span data-stu-id="96fa7-236">An enum representing the possible error:</span></span>
- <span data-ttu-id="96fa7-237">`NoError` - No error found</span><span class="sxs-lookup"><span data-stu-id="96fa7-237">`NoError` - No error found</span></span>
- <span data-ttu-id="96fa7-238">`InternalError` - The error was caused by a failure in the service</span><span class="sxs-lookup"><span data-stu-id="96fa7-238">`InternalError` - The error was caused by a failure in the service</span></span>
- <span data-ttu-id="96fa7-239">`DataFileNotExist` - The data source file could not be found</span><span class="sxs-lookup"><span data-stu-id="96fa7-239">`DataFileNotExist` - The data source file could not be found</span></span>
- <span data-ttu-id="96fa7-240">`DataFileNotInTenant` - The data source file did not belong to the same tenant</span><span class="sxs-lookup"><span data-stu-id="96fa7-240">`DataFileNotInTenant` - The data source file did not belong to the same tenant</span></span>
- <span data-ttu-id="96fa7-241">`DataFileTooBig` - The size of the data file was too big</span><span class="sxs-lookup"><span data-stu-id="96fa7-241">`DataFileTooBig` - The size of the data file was too big</span></span>
- <span data-ttu-id="96fa7-242">`InvalidDataFile` - The data source file did not pass validation (There may be additional details in the log file)</span><span class="sxs-lookup"><span data-stu-id="96fa7-242">`InvalidDataFile` - The data source file did not pass validation (There may be additional details in the log file)</span></span>
- <span data-ttu-id="96fa7-243">`ImportCompleteWithError` - The data has been imported, but there was an error encountered</span><span class="sxs-lookup"><span data-stu-id="96fa7-243">`ImportCompleteWithError` - The data has been imported, but there was an error encountered</span></span>

<span data-ttu-id="96fa7-244">**ErrorMessage**: _`System.String`_</span><span class="sxs-lookup"><span data-stu-id="96fa7-244">**ErrorMessage**: _`System.String`_</span></span>

<span data-ttu-id="96fa7-245">The error message</span><span class="sxs-lookup"><span data-stu-id="96fa7-245">The error message</span></span>

<span data-ttu-id="96fa7-246">**LogFileUri**: _`System.String`_</span><span class="sxs-lookup"><span data-stu-id="96fa7-246">**LogFileUri**: _`System.String`_</span></span>

<span data-ttu-id="96fa7-247">The Uri to the folder where the logs have been written</span><span class="sxs-lookup"><span data-stu-id="96fa7-247">The Uri to the folder where the logs have been written</span></span>

## <a name="calling-the-import-api-from-powershell"></a><span data-ttu-id="96fa7-248">Calling the Import API from PowerShell</span><span class="sxs-lookup"><span data-stu-id="96fa7-248">Calling the Import API from PowerShell</span></span>
<span data-ttu-id="96fa7-249"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="96fa7-249"></span></span>

<span data-ttu-id="96fa7-250">You can take advantage of the User Profile Service bulk import API with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96fa7-250">You can take advantage of the User Profile Service bulk import API with PowerShell.</span></span> <span data-ttu-id="96fa7-251">This means that you’ll use the CSOM code directly in a PowerShell script using the necessary parameters.</span><span class="sxs-lookup"><span data-stu-id="96fa7-251">This means that you’ll use the CSOM code directly in a PowerShell script using the necessary parameters.</span></span> <span data-ttu-id="96fa7-252">This requires that the updated CSOM redistributable package has been installed on the computer where the script is executed.</span><span class="sxs-lookup"><span data-stu-id="96fa7-252">This requires that the updated CSOM redistributable package has been installed on the computer where the script is executed.</span></span>

<span data-ttu-id="96fa7-253">By using PowerShell, you do not need to compile your code within Visual Studio, which may be a more suitable model for some customers.</span><span class="sxs-lookup"><span data-stu-id="96fa7-253">By using PowerShell, you do not need to compile your code within Visual Studio, which may be a more suitable model for some customers.</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="96fa7-254">Sample PowerShell Script</span><span class="sxs-lookup"><span data-stu-id="96fa7-254">Sample PowerShell Script</span></span>
<span data-ttu-id="96fa7-255">Below is a sample PowerShell script which performs the same operations as the code above:</span><span class="sxs-lookup"><span data-stu-id="96fa7-255">Below is a sample PowerShell script which performs the same operations as the code above:</span></span> 

```Powershell
# Get needed information from the end user
$adminUrl = Read-Host -Prompt 'Enter the admin URL of your tenant'
$userName = Read-Host -Prompt 'Enter your user name'
$pwd = Read-Host -Prompt 'Enter your password' -AsSecureString
$importFileUrl = Read-Host -Prompt 'Enter the URL to the file located in your tenant'

# Get instances to the Office 365 tenant using CSOM
$uri = New-Object System.Uri -ArgumentList $adminUrl
$context = New-Object Microsoft.SharePoint.Client.ClientContext($uri)

$context.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($userName, $pwd)
$o365 = New-Object Microsoft.Online.SharePoint.TenantManagement.Office365Tenant($context)
$context.Load($o365)

# Type of user identifier ["Email", "CloudId", "PrincipalName"] in the User Profile Service
$userIdType=[Microsoft.Online.SharePoint.TenantManagement.ImportProfilePropertiesUserIdType]::Email

# Name of user identifier property in the JSON
$userLookupKey="idName"

# Create property mapping between the source file property name and the O365 property name
# Notice that we have here 2 custom properties in UPA called 'City' and 'OfficeCode'
$propertyMap = New-Object -type 'System.Collections.Generic.Dictionary[String,String]'
$propertyMap.Add("City", "City")
$propertyMap.Add("Office", "OfficeCode")

# Call to queue UPA property import 
$workItemId = $o365.QueueImportProfileProperties($userIdType, $userLookupKey, $propertyMap, $importFileUrl);

# Execute the CSOM command for queuing the import job
$context.ExecuteQuery();

# Output the unique identifier of the job
Write-Host "Import job created with the following identifier:" $workItemId.Value 
```

## <a name="handling-exceptions"></a><span data-ttu-id="96fa7-256">Handling Exceptions</span><span class="sxs-lookup"><span data-stu-id="96fa7-256">Handling Exceptions</span></span>
<span data-ttu-id="96fa7-257"><a name="sectionSection5"> </a> There are two levels of validation when this API is used.</span><span class="sxs-lookup"><span data-stu-id="96fa7-257"><a name="sectionSection5"> </a> There are two levels of validation when this API is used.</span></span> <span data-ttu-id="96fa7-258">When you queue the import process with CSOM there will be an initial level of validation of the provided values.</span><span class="sxs-lookup"><span data-stu-id="96fa7-258">When you queue the import process with CSOM there will be an initial level of validation of the provided values.</span></span> <span data-ttu-id="96fa7-259">This includes confirmation that the provided mapping properties exist in the User Profile Service and that these properties are not editable by the end user.</span><span class="sxs-lookup"><span data-stu-id="96fa7-259">This includes confirmation that the provided mapping properties exist in the User Profile Service and that these properties are not editable by the end user.</span></span> <span data-ttu-id="96fa7-260">When the queue API is called, only an initial level of validation is applied and final validation of the provided information is performed when the import job is actually executed.</span><span class="sxs-lookup"><span data-stu-id="96fa7-260">When the queue API is called, only an initial level of validation is applied and final validation of the provided information is performed when the import job is actually executed.</span></span>

<span data-ttu-id="96fa7-261">If there are any exceptions during the actual import job execution, a logging file with additional details is generated in the same document library where the import file was located.</span><span class="sxs-lookup"><span data-stu-id="96fa7-261">If there are any exceptions during the actual import job execution, a logging file with additional details is generated in the same document library where the import file was located.</span></span> <span data-ttu-id="96fa7-262">Log files for specific import jobs are saved to sub folders named using the unique identifier of the specific import job.</span><span class="sxs-lookup"><span data-stu-id="96fa7-262">Log files for specific import jobs are saved to sub folders named using the unique identifier of the specific import job.</span></span>

<span data-ttu-id="96fa7-263">Below is an example of the results of running an import job.</span><span class="sxs-lookup"><span data-stu-id="96fa7-263">Below is an example of the results of running an import job.</span></span> <span data-ttu-id="96fa7-264">In the picture below, you can see two sub folders for two different executions created in the document library where the import file is stored:</span><span class="sxs-lookup"><span data-stu-id="96fa7-264">In the picture below, you can see two sub folders for two different executions created in the document library where the import file is stored:</span></span>

![Job Exception Sub Folders](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-folders.png)

<span data-ttu-id="96fa7-266">The actual log file is saved in the sub folder and you can download that from Office 365 for detailed analysis:</span><span class="sxs-lookup"><span data-stu-id="96fa7-266">The actual log file is saved in the sub folder and you can download that from Office 365 for detailed analysis:</span></span>

![Job Exception Log File](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-LogFile.png)

### <a name="common-exceptions"></a><span data-ttu-id="96fa7-268">Common Exceptions</span><span class="sxs-lookup"><span data-stu-id="96fa7-268">Common Exceptions</span></span>

<span data-ttu-id="96fa7-269">Following table contains typical exceptions which you could encounter when you start using the User Profile Service bulk API.</span><span class="sxs-lookup"><span data-stu-id="96fa7-269">Following table contains typical exceptions which you could encounter when you start using the User Profile Service bulk API.</span></span>

<span data-ttu-id="96fa7-270">Example Exception</span><span class="sxs-lookup"><span data-stu-id="96fa7-270">Example Exception</span></span> | <span data-ttu-id="96fa7-271">Details</span><span class="sxs-lookup"><span data-stu-id="96fa7-271">Details</span></span>
--- | ---
<span data-ttu-id="96fa7-272">_Property Names [AboutMe] are editable by user._</span><span class="sxs-lookup"><span data-stu-id="96fa7-272">_Property Names [AboutMe] are editable by user._</span></span> | <span data-ttu-id="96fa7-273">This would be thrown by the CSOM API when you call the `ExecuteQuery` method when submitting the job to your tenant.</span><span class="sxs-lookup"><span data-stu-id="96fa7-273">This would be thrown by the CSOM API when you call the `ExecuteQuery` method when submitting the job to your tenant.</span></span> <span data-ttu-id="96fa7-274">The API will validate that all properties currently being mapped are NOT user editable.</span><span class="sxs-lookup"><span data-stu-id="96fa7-274">The API will validate that all properties currently being mapped are NOT user editable.</span></span> <span data-ttu-id="96fa7-275">The exception will point out the property which cannot be used.</span><span class="sxs-lookup"><span data-stu-id="96fa7-275">The exception will point out the property which cannot be used.</span></span> <span data-ttu-id="96fa7-276">In this example, we have tried to map a JSON property to the `AboutMe` property in the User Profile Service properties, but this is not allowed since `AboutMe` is a user editable property.</span><span class="sxs-lookup"><span data-stu-id="96fa7-276">In this example, we have tried to map a JSON property to the `AboutMe` property in the User Profile Service properties, but this is not allowed since `AboutMe` is a user editable property.</span></span>
<span data-ttu-id="96fa7-277">_InvalidProperty - vesaj@contoso.com Property 'AboutMe' is not mapped to any property in the user profile application._</span><span class="sxs-lookup"><span data-stu-id="96fa7-277">_InvalidProperty - vesaj@contoso.com Property 'AboutMe' is not mapped to any property in the user profile application._</span></span> | <span data-ttu-id="96fa7-278">The JSON data file contained a property which has not been mapped to the User Profile Service property in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="96fa7-278">The JSON data file contained a property which has not been mapped to the User Profile Service property in SharePoint Online.</span></span> <span data-ttu-id="96fa7-279">This means that the source data file contains properties for which you have not provided a mapping in the `propertyMap` parameter.</span><span class="sxs-lookup"><span data-stu-id="96fa7-279">This means that the source data file contains properties for which you have not provided a mapping in the `propertyMap` parameter.</span></span> <span data-ttu-id="96fa7-280">You will need to have a mapping definition for each of the properties in the JSON data object.</span><span class="sxs-lookup"><span data-stu-id="96fa7-280">You will need to have a mapping definition for each of the properties in the JSON data object.</span></span>
<span data-ttu-id="96fa7-281">_MissingIdentity - The identity is missing for the user object_</span><span class="sxs-lookup"><span data-stu-id="96fa7-281">_MissingIdentity - The identity is missing for the user object_</span></span> | <span data-ttu-id="96fa7-282">The identity property could not be found in the user object.</span><span class="sxs-lookup"><span data-stu-id="96fa7-282">The identity property could not be found in the user object.</span></span> <span data-ttu-id="96fa7-283">The most likely cause is that the `sourceDataIdProperty` attribute is wrongly set for the `QueueImportProfileProperties` method.</span><span class="sxs-lookup"><span data-stu-id="96fa7-283">The most likely cause is that the `sourceDataIdProperty` attribute is wrongly set for the `QueueImportProfileProperties` method.</span></span> <span data-ttu-id="96fa7-284">Ensure that you have the right property in the JSON source file and that your code/script is assigning this attribute accordingly.</span><span class="sxs-lookup"><span data-stu-id="96fa7-284">Ensure that you have the right property in the JSON source file and that your code/script is assigning this attribute accordingly.</span></span>
<span data-ttu-id="96fa7-285">_IdentityNotResolvable unknown@contoso.com User identity cannot be resolved_</span><span class="sxs-lookup"><span data-stu-id="96fa7-285">_IdentityNotResolvable unknown@contoso.com User identity cannot be resolved_</span></span> | <span data-ttu-id="96fa7-286">The data file contained an identity, which could not be resolved or was not present in the User Profile Service.</span><span class="sxs-lookup"><span data-stu-id="96fa7-286">The data file contained an identity, which could not be resolved or was not present in the User Profile Service.</span></span> <span data-ttu-id="96fa7-287">In this case, the user profile with email of _unknown@contoso.com_ could not be located in the User Profile Service.</span><span class="sxs-lookup"><span data-stu-id="96fa7-287">In this case, the user profile with email of _unknown@contoso.com_ could not be located in the User Profile Service.</span></span>
<span data-ttu-id="96fa7-288">_DataFileNotJson - JsonToken EndObject is not valid for closing JsonType Array. Path 'value', line 8, position 10._</span><span class="sxs-lookup"><span data-stu-id="96fa7-288">_DataFileNotJson - JsonToken EndObject is not valid for closing JsonType Array. Path 'value', line 8, position 10._</span></span> | <span data-ttu-id="96fa7-289">Your import file format is not valid JSON and does not match the expected format.</span><span class="sxs-lookup"><span data-stu-id="96fa7-289">Your import file format is not valid JSON and does not match the expected format.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="96fa7-290">Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="96fa7-290">Frequently Asked Questions</span></span>
<span data-ttu-id="96fa7-291"><a name="sectionSection6"> </a></span><span class="sxs-lookup"><span data-stu-id="96fa7-291"></span></span>

<span data-ttu-id="96fa7-292">**Can I execute the code using app-only/add-in only permissions?**</span><span class="sxs-lookup"><span data-stu-id="96fa7-292">**Can I execute the code using app-only/add-in only permissions?**</span></span>

<span data-ttu-id="96fa7-293">Yes, you’ll need to register the client id and secret to be able to execute the APIs.</span><span class="sxs-lookup"><span data-stu-id="96fa7-293">Yes, you’ll need to register the client id and secret to be able to execute the APIs.</span></span> <span data-ttu-id="96fa7-294">Since the actual import of the file does not occur synchronously with the identity of the caller, this works without any issues.</span><span class="sxs-lookup"><span data-stu-id="96fa7-294">Since the actual import of the file does not occur synchronously with the identity of the caller, this works without any issues.</span></span>

<span data-ttu-id="96fa7-295">**This API is updating properties in the User Profile Service, but how would I create those properties in the tenant?**</span><span class="sxs-lookup"><span data-stu-id="96fa7-295">**This API is updating properties in the User Profile Service, but how would I create those properties in the tenant?**</span></span>

<span data-ttu-id="96fa7-296">There’s no remote API to create custom user profile properties programmatically, so this is manual operation which needs to be completed once per given tenant.</span><span class="sxs-lookup"><span data-stu-id="96fa7-296">There’s no remote API to create custom user profile properties programmatically, so this is manual operation which needs to be completed once per given tenant.</span></span> <span data-ttu-id="96fa7-297">You can refer to [this article](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) for instructions on how to create these custom properties.</span><span class="sxs-lookup"><span data-stu-id="96fa7-297">You can refer to [this article](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) for instructions on how to create these custom properties.</span></span>

<span data-ttu-id="96fa7-298">**Is this capability available in on-premises SharePoint?**</span><span class="sxs-lookup"><span data-stu-id="96fa7-298">**Is this capability available in on-premises SharePoint?**</span></span>

<span data-ttu-id="96fa7-299">Unfortunately, this capability is currently only for SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="96fa7-299">Unfortunately, this capability is currently only for SharePoint Online.</span></span> <span data-ttu-id="96fa7-300">In on-premises SharePoint this capability would be useful but not as critical since you can modify the attribute mapping in the on-premises User Profile Service Application.</span><span class="sxs-lookup"><span data-stu-id="96fa7-300">In on-premises SharePoint this capability would be useful but not as critical since you can modify the attribute mapping in the on-premises User Profile Service Application.</span></span> <span data-ttu-id="96fa7-301">You can also take advantage of importing user profile attributes using the Business Connectivity Service (BCS) in SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="96fa7-301">You can also take advantage of importing user profile attributes using the Business Connectivity Service (BCS) in SharePoint 2013.</span></span> <span data-ttu-id="96fa7-302">However, this option is not available in SharePoint 2016, which means that for SharePoint 2016 the only option currently is to implement customizations which take advantage of the user profile web services.</span><span class="sxs-lookup"><span data-stu-id="96fa7-302">However, this option is not available in SharePoint 2016, which means that for SharePoint 2016 the only option currently is to implement customizations which take advantage of the user profile web services.</span></span>

<span data-ttu-id="96fa7-303">**Could I use this API for synchronizing user profile property values from my on-premises SharePoint 2013 or 2016 farm(s) to SharePoint Online?**</span><span class="sxs-lookup"><span data-stu-id="96fa7-303">**Could I use this API for synchronizing user profile property values from my on-premises SharePoint 2013 or 2016 farm(s) to SharePoint Online?**</span></span>
<span data-ttu-id="96fa7-304">Yes, on-premises SharePoint can be used just like any other source system.</span><span class="sxs-lookup"><span data-stu-id="96fa7-304">Yes, on-premises SharePoint can be used just like any other source system.</span></span> <span data-ttu-id="96fa7-305">You'll need to export the user profile values from your on-premises SharePoint to the JSON file format and then the process would be exactly the same as importing values from any other system.</span><span class="sxs-lookup"><span data-stu-id="96fa7-305">You'll need to export the user profile values from your on-premises SharePoint to the JSON file format and then the process would be exactly the same as importing values from any other system.</span></span>

<span data-ttu-id="96fa7-306">**Can I import string based, multi-value properties?**</span><span class="sxs-lookup"><span data-stu-id="96fa7-306">**Can I import string based, multi-value properties?**</span></span>
<span data-ttu-id="96fa7-307">No, this is not currently supported with this API.</span><span class="sxs-lookup"><span data-stu-id="96fa7-307">No, this is not currently supported with this API.</span></span>

<span data-ttu-id="96fa7-308">**What permissions are required for executing this API??**</span><span class="sxs-lookup"><span data-stu-id="96fa7-308">**What permissions are required for executing this API??**</span></span>
<span data-ttu-id="96fa7-309">You will need to have Global Admin permissions currently.</span><span class="sxs-lookup"><span data-stu-id="96fa7-309">You will need to have Global Admin permissions currently.</span></span> <span data-ttu-id="96fa7-310">SharePoint Admin is not sufficient.</span><span class="sxs-lookup"><span data-stu-id="96fa7-310">SharePoint Admin is not sufficient.</span></span>

<span data-ttu-id="96fa7-311">**Can I import taxonomy based properties?**</span><span class="sxs-lookup"><span data-stu-id="96fa7-311">**Can I import taxonomy based properties?**</span></span>
<span data-ttu-id="96fa7-312">No, this is not currently supported with this API.</span><span class="sxs-lookup"><span data-stu-id="96fa7-312">No, this is not currently supported with this API.</span></span>

<span data-ttu-id="96fa7-313">**What if I define a mapping in the code which is not used or have properties in the JSON file which are not mapped?**</span><span class="sxs-lookup"><span data-stu-id="96fa7-313">**What if I define a mapping in the code which is not used or have properties in the JSON file which are not mapped?**</span></span>
<span data-ttu-id="96fa7-314">If your code/script defines a mapping which is not used or the data file does not contain properties for that mapping, execution will continue without any exceptions and the import will be applied based on the mapped properties.</span><span class="sxs-lookup"><span data-stu-id="96fa7-314">If your code/script defines a mapping which is not used or the data file does not contain properties for that mapping, execution will continue without any exceptions and the import will be applied based on the mapped properties.</span></span> <span data-ttu-id="96fa7-315">If you, however, have a property in the JSON file which is not mapped, the import process will be aborted and exception details will be provided in the log file for the specific job execution.</span><span class="sxs-lookup"><span data-stu-id="96fa7-315">If you, however, have a property in the JSON file which is not mapped, the import process will be aborted and exception details will be provided in the log file for the specific job execution.</span></span>

<span data-ttu-id="96fa7-316">**What if I have a need to update custom properties that are beyond the size limitations of this bulk API (i.e. >2 GB file or >500,000 properties)?**</span><span class="sxs-lookup"><span data-stu-id="96fa7-316">**What if I have a need to update custom properties that are beyond the size limitations of this bulk API (i.e. >2 GB file or >500,000 properties)?**</span></span>
<span data-ttu-id="96fa7-317">You would need to batch your jobs accordingly by triggering multiple jobs in sequence (i.e. finishing one job at a time with the maximum limit on this API).</span><span class="sxs-lookup"><span data-stu-id="96fa7-317">You would need to batch your jobs accordingly by triggering multiple jobs in sequence (i.e. finishing one job at a time with the maximum limit on this API).</span></span> <span data-ttu-id="96fa7-318">You should expect these high bandwidth imports will take a long time to complete.</span><span class="sxs-lookup"><span data-stu-id="96fa7-318">You should expect these high bandwidth imports will take a long time to complete.</span></span> <span data-ttu-id="96fa7-319">Also, you should optimize the import jobs only for delta changes in custom profile properties rather than importing a full set of values in all jobs.</span><span class="sxs-lookup"><span data-stu-id="96fa7-319">Also, you should optimize the import jobs only for delta changes in custom profile properties rather than importing a full set of values in all jobs.</span></span>

<span data-ttu-id="96fa7-320">**Which Azure Active Directory attributes are being sync’d to SharePoint Online user profile by default?**</span><span class="sxs-lookup"><span data-stu-id="96fa7-320">**Which Azure Active Directory attributes are being sync’d to SharePoint Online user profile by default?**</span></span>
<span data-ttu-id="96fa7-321">See the following table for the official list of synchronized attributes and their mapping between Azure Active Directory and the SharePoint Online User Profile Service.</span><span class="sxs-lookup"><span data-stu-id="96fa7-321">See the following table for the official list of synchronized attributes and their mapping between Azure Active Directory and the SharePoint Online User Profile Service.</span></span>

<span data-ttu-id="96fa7-322">Azure Directory Attribute</span><span class="sxs-lookup"><span data-stu-id="96fa7-322">Azure Directory Attribute</span></span>  | <span data-ttu-id="96fa7-323">SharePoint Online Profile Property</span><span class="sxs-lookup"><span data-stu-id="96fa7-323">SharePoint Online Profile Property</span></span>
---------|----------
<span data-ttu-id="96fa7-324">ObjectSid</span><span class="sxs-lookup"><span data-stu-id="96fa7-324">ObjectSid</span></span> | <span data-ttu-id="96fa7-325">SPS-SavedSID</span><span class="sxs-lookup"><span data-stu-id="96fa7-325">SPS-SavedSID</span></span>
<span data-ttu-id="96fa7-326">msonline-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="96fa7-326">msonline-UserPrincipalName</span></span> | <span data-ttu-id="96fa7-327">UserName</span><span class="sxs-lookup"><span data-stu-id="96fa7-327">UserName</span></span>
<span data-ttu-id="96fa7-328">msonline-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="96fa7-328">msonline-UserPrincipalName</span></span> | <span data-ttu-id="96fa7-329">AccountName</span><span class="sxs-lookup"><span data-stu-id="96fa7-329">AccountName</span></span>
<span data-ttu-id="96fa7-330">msonline-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="96fa7-330">msonline-UserPrincipalName</span></span> | <span data-ttu-id="96fa7-331">SPS-ClaimID</span><span class="sxs-lookup"><span data-stu-id="96fa7-331">SPS-ClaimID</span></span>
<span data-ttu-id="96fa7-332">msonline-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="96fa7-332">msonline-UserPrincipalName</span></span> | <span data-ttu-id="96fa7-333">SPS-UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="96fa7-333">SPS-UserPrincipalName</span></span>
<span data-ttu-id="96fa7-334">GivenName</span><span class="sxs-lookup"><span data-stu-id="96fa7-334">GivenName</span></span> | <span data-ttu-id="96fa7-335">FirstName</span><span class="sxs-lookup"><span data-stu-id="96fa7-335">FirstName</span></span>
<span data-ttu-id="96fa7-336">sn</span><span class="sxs-lookup"><span data-stu-id="96fa7-336">sn</span></span> | <span data-ttu-id="96fa7-337">LastName</span><span class="sxs-lookup"><span data-stu-id="96fa7-337">LastName</span></span>
<span data-ttu-id="96fa7-338">Manager</span><span class="sxs-lookup"><span data-stu-id="96fa7-338">Manager</span></span> | <span data-ttu-id="96fa7-339">Manager</span><span class="sxs-lookup"><span data-stu-id="96fa7-339">Manager</span></span>
<span data-ttu-id="96fa7-340">DisplayName</span><span class="sxs-lookup"><span data-stu-id="96fa7-340">DisplayName</span></span> | <span data-ttu-id="96fa7-341">PreferredName</span><span class="sxs-lookup"><span data-stu-id="96fa7-341">PreferredName</span></span>
<span data-ttu-id="96fa7-342">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="96fa7-342">telephoneNumber</span></span> | <span data-ttu-id="96fa7-343">WorkPhone</span><span class="sxs-lookup"><span data-stu-id="96fa7-343">WorkPhone</span></span>
<span data-ttu-id="96fa7-344">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="96fa7-344">proxyAddresses</span></span> | <span data-ttu-id="96fa7-345">WorkEmail</span><span class="sxs-lookup"><span data-stu-id="96fa7-345">WorkEmail</span></span>
<span data-ttu-id="96fa7-346">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="96fa7-346">proxyAddresses</span></span> | <span data-ttu-id="96fa7-347">SPS-SIPAddress</span><span class="sxs-lookup"><span data-stu-id="96fa7-347">SPS-SIPAddress</span></span>
<span data-ttu-id="96fa7-348">PhysicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="96fa7-348">PhysicalDeliveryOfficeName</span></span> | <span data-ttu-id="96fa7-349">Office</span><span class="sxs-lookup"><span data-stu-id="96fa7-349">Office</span></span>
<span data-ttu-id="96fa7-350">Titel</span><span class="sxs-lookup"><span data-stu-id="96fa7-350">Title</span></span> | <span data-ttu-id="96fa7-351">Titel</span><span class="sxs-lookup"><span data-stu-id="96fa7-351">Title</span></span>
<span data-ttu-id="96fa7-352">Titel</span><span class="sxs-lookup"><span data-stu-id="96fa7-352">Title</span></span> | <span data-ttu-id="96fa7-353">SPS-JobTitle</span><span class="sxs-lookup"><span data-stu-id="96fa7-353">SPS-JobTitle</span></span>
<span data-ttu-id="96fa7-354">Abteilung</span><span class="sxs-lookup"><span data-stu-id="96fa7-354">Department</span></span> | <span data-ttu-id="96fa7-355">Abteilung</span><span class="sxs-lookup"><span data-stu-id="96fa7-355">Department</span></span>
<span data-ttu-id="96fa7-356">Abteilung</span><span class="sxs-lookup"><span data-stu-id="96fa7-356">Department</span></span> | <span data-ttu-id="96fa7-357">SPS-Department</span><span class="sxs-lookup"><span data-stu-id="96fa7-357">SPS-Department</span></span>
<span data-ttu-id="96fa7-358">ObjectGuid</span><span class="sxs-lookup"><span data-stu-id="96fa7-358">ObjectGuid</span></span> | <span data-ttu-id="96fa7-359">ADGuid</span><span class="sxs-lookup"><span data-stu-id="96fa7-359">ADGuid</span></span>
<span data-ttu-id="96fa7-360">WWWHomePage</span><span class="sxs-lookup"><span data-stu-id="96fa7-360">WWWHomePage</span></span> | <span data-ttu-id="96fa7-361">PublicSiteRedirect</span><span class="sxs-lookup"><span data-stu-id="96fa7-361">PublicSiteRedirect</span></span>
<span data-ttu-id="96fa7-362">DistinguishedName</span><span class="sxs-lookup"><span data-stu-id="96fa7-362">DistinguishedName</span></span> | <span data-ttu-id="96fa7-363">SPS-DistinguishedName</span><span class="sxs-lookup"><span data-stu-id="96fa7-363">SPS-DistinguishedName</span></span>
<span data-ttu-id="96fa7-364">msOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="96fa7-364">msOnline-ObjectId</span></span> | <span data-ttu-id="96fa7-365">msOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="96fa7-365">msOnline-ObjectId</span></span>
<span data-ttu-id="96fa7-366">PreferredLanguage</span><span class="sxs-lookup"><span data-stu-id="96fa7-366">PreferredLanguage</span></span> | <span data-ttu-id="96fa7-367">SPS-MUILanguages</span><span class="sxs-lookup"><span data-stu-id="96fa7-367">SPS-MUILanguages</span></span>
<span data-ttu-id="96fa7-368">msExchHideFromAddressList</span><span class="sxs-lookup"><span data-stu-id="96fa7-368">msExchHideFromAddressList</span></span> | <span data-ttu-id="96fa7-369">SPS-HideFromAddressLists</span><span class="sxs-lookup"><span data-stu-id="96fa7-369">SPS-HideFromAddressLists</span></span>
<span data-ttu-id="96fa7-370">msExchRecipientTypeDetails</span><span class="sxs-lookup"><span data-stu-id="96fa7-370">msExchRecipientTypeDetails</span></span> | <span data-ttu-id="96fa7-371">SPS-RecipientTypeDetails</span><span class="sxs-lookup"><span data-stu-id="96fa7-371">SPS-RecipientTypeDetails</span></span>
<span data-ttu-id="96fa7-372">msonline-groupType</span><span class="sxs-lookup"><span data-stu-id="96fa7-372">msonline-groupType</span></span> | <span data-ttu-id="96fa7-373">IsUnifiedGroup</span><span class="sxs-lookup"><span data-stu-id="96fa7-373">IsUnifiedGroup</span></span>
<span data-ttu-id="96fa7-374">msOnline-IsPublic</span><span class="sxs-lookup"><span data-stu-id="96fa7-374">msOnline-IsPublic</span></span> | <span data-ttu-id="96fa7-375">IsPublic</span><span class="sxs-lookup"><span data-stu-id="96fa7-375">IsPublic</span></span>
<span data-ttu-id="96fa7-376">msOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="96fa7-376">msOnline-ObjectId</span></span> | <span data-ttu-id="96fa7-377">msOnline-ObjectId</span><span class="sxs-lookup"><span data-stu-id="96fa7-377">msOnline-ObjectId</span></span>
<span data-ttu-id="96fa7-378">msOnline-UserType</span><span class="sxs-lookup"><span data-stu-id="96fa7-378">msOnline-UserType</span></span> | <span data-ttu-id="96fa7-379">SPS-UserType</span><span class="sxs-lookup"><span data-stu-id="96fa7-379">SPS-UserType</span></span>
<span data-ttu-id="96fa7-380">GroupType</span><span class="sxs-lookup"><span data-stu-id="96fa7-380">GroupType</span></span> | <span data-ttu-id="96fa7-381">GroupType</span><span class="sxs-lookup"><span data-stu-id="96fa7-381">GroupType</span></span>
<span data-ttu-id="96fa7-382">SPO-IsSharePointOnlineObject</span><span class="sxs-lookup"><span data-stu-id="96fa7-382">SPO-IsSharePointOnlineObject</span></span> | <span data-ttu-id="96fa7-383">SPO-IsSPO</span><span class="sxs-lookup"><span data-stu-id="96fa7-383">SPO-IsSPO</span></span>

