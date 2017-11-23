---
title: "Protokollhandlerfehler aufgrund von nicht mehr unterstützter SharePoint 2016-Oberfläche"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c80cb77c-89db-4c78-b576-f63d39ca330a
ms.openlocfilehash: 1d2a5974bd8bd386c35d7f016cccec0a8237a2ec
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="protocol-handler-error-due-to-deprecated-interface-in-sharepoint-2016"></a><span data-ttu-id="ce046-102">Protokollhandlerfehler aufgrund von nicht mehr unterstützter SharePoint 2016-Oberfläche</span><span class="sxs-lookup"><span data-stu-id="ce046-102">Protocol handler error due to deprecated interface in SharePoint 2016</span></span>

<span data-ttu-id="ce046-103">Protokollhandlerimplementierungen mithilfe der in diesem Artikel in der Header-Datei **srchprth.h** aufgeführten Schnittstellen werden in SharePoint 2016 jetzt nicht mehr unterstützt.</span><span class="sxs-lookup"><span data-stu-id="ce046-103">Protocol handler implementations using the interfaces listed in this article in the **srchprth.h** header file are now deprecated in SharePoint 2016.</span></span> <span data-ttu-id="ce046-104">Vor allem der Protokollhandler für nicht mehr unterstützte Schnittstellen generiert die Fehlermeldung "Der Protokollhandler kann nicht geladen werden".</span><span class="sxs-lookup"><span data-stu-id="ce046-104">Specifically, the protocol handler for deprecated interfaces generates the error "The protocol handler cannot be loaded".</span></span>
  
    
    


## <a name="symptom"></a><span data-ttu-id="ce046-105">Symptom</span><span class="sxs-lookup"><span data-stu-id="ce046-105">Symptom</span></span>

<span data-ttu-id="ce046-106">Wenn Sie den Protokollhandler laden die, wird die folgende Fehlermeldung angezeigt:</span><span class="sxs-lookup"><span data-stu-id="ce046-106">You see the following error message when you load the protocol handler:</span></span>
  
    
    

```

The protocol handler <name of custom protocol handler> cannot be loaded. Error description: No such interface supported.
```


### <a name="cause"></a><span data-ttu-id="ce046-107">Ursache</span><span class="sxs-lookup"><span data-stu-id="ce046-107">Cause</span></span>

<span data-ttu-id="ce046-108">Sie verwenden die Header-Datei **srchprth.h** bei Ihrer Protokollhandlerimplementierung.</span><span class="sxs-lookup"><span data-stu-id="ce046-108">You are using the **srchprth.h** header file in your protocol handler implementation.</span></span> <span data-ttu-id="ce046-109">Diese Datei enthält Schnittstellen, die in SharePoint 2016 nicht mehr unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="ce046-109">This file contains interfaces deprecated in SharePoint 2016.</span></span>
  
    
    

### <a name="resolution"></a><span data-ttu-id="ce046-110">Auflösung</span><span class="sxs-lookup"><span data-stu-id="ce046-110">Resolution</span></span>

<span data-ttu-id="ce046-111">Ersetzen Sie die veralteten Schnittstellen in Ihrer Protokollhandlerimplementierung mit Schnittstellen, die derzeit unterstützt werden:</span><span class="sxs-lookup"><span data-stu-id="ce046-111">Replace the deprecated interfaces in your protocol handler implementation with those that are currently supported:</span></span>
  
    
    

- <span data-ttu-id="ce046-112">**srchprth.h** (aktualisiert)</span><span class="sxs-lookup"><span data-stu-id="ce046-112">**srchprth.h** (updated)</span></span>
    
  
- <span data-ttu-id="ce046-113">**urlaccsdk.h** (neu)</span><span class="sxs-lookup"><span data-stu-id="ce046-113">**urlaccsdk.h** (new)</span></span>
    
  

## <a name="deprecated-interfaces"></a><span data-ttu-id="ce046-114">Veraltete Schnittstellen</span><span class="sxs-lookup"><span data-stu-id="ce046-114">Deprecated Interfaces</span></span>
<span data-ttu-id="ce046-115"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ce046-115"></span></span>

<span data-ttu-id="ce046-116">Zu diesen nicht mehr unterstützten Schnittstellen gehören unter anderem:</span><span class="sxs-lookup"><span data-stu-id="ce046-116">The deprecated interfaces include the following:</span></span>
  
    
    
 <span data-ttu-id="ce046-117">**interface ISearchProtocol : IUnknown**</span><span class="sxs-lookup"><span data-stu-id="ce046-117">**interface ISearchProtocol : IUnknown**</span></span>
  
    
    



```
{

    HRESULT Init([in] TIMEOUT_INFO *pTimeoutInfo,
                 [in] IProtocolHandlerSite *pProtocolHandlerSite,
                 [in] PROXY_INFO *pProxyInfo);

    HRESULT CreateAccessor([in] LPCWSTR pcwszURL,
                           [in] AUTHENTICATION_INFO *pAuthenticationInfo,
                           [in] INCREMENTAL_ACCESS_INFO *pIncrementalAccessInfo,
                           [in] ITEM_INFO *pItemInfo,
                           [out] IUrlAccessor **ppAccessor);

    HRESULT CloseAccessor([in] IUrlAccessor *pAccessor);
    HRESULT ShutDown();
}

TIMEOUT_INFO
{
    DWORD       dwSize;
    DWORD       dwConnectTimeout;
    DWORD       dwDataTimeout;
}

PROXY_INFO
{
    DWORD           dwSize;
    LPCWSTR         pcwszUserAgent;
    PROXY_ACCESS    paUseProxy;
    BOOL            fLocalBypass;
    DWORD           dwPortNumber;
    LPCWSTR         pcwszProxyName;
    LPCWSTR         pcwszBypassList;
}

AUTHENTICATION_INFO
{
    DWORD       dwSize;
    AUTH_TYPE   atAuthenticationType;
    LPCWSTR     pcwszUser;
    LPCWSTR     pcwszPassword;
}

INCREMENTAL_ACCESS_INFO
{
                     DWORD       dwSize;
                     FILETIME    ftLastModifiedTime;
}
```

 <span data-ttu-id="ce046-118">**IProtocolHandler: public IUnknown**</span><span class="sxs-lookup"><span data-stu-id="ce046-118">**IProtocolHandler: public IUnknown**</span></span>
  
    
    



```

{
                     public:
                           HRESULT Init(
                                  /* [in] */ LPCWSTR pwszUserAgent,
                                  /* [in] */ DWORD dwUseProxy,
                                  /* [in] */ DWORD dwConnectTimeout,
                                  /* [in] */ DWORD dwDataTimeout,
                                  /* [in] */ DWORD dwLocalByPassProxy,
                                  /* [in] */ DWORD dwPortNumber,
                                  /* [in] */ LPCWSTR pcwszProxyName,
                                  /* [in] */ LPCWSTR pcwszByPassList,
                                  /* [in] */ LPCWSTR pcwszProxyUserName,
                                  /* [in] */ LPCWSTR pcwszProxyPassword,
                                  /* [in] */ IProtocolHandlerSite *pProtocolHandlerSite) = 0;

                           HRESULT CreateAccessor(
                                  /* [in] */ AccessorInitParams *pParams,
                                  /* [out] */ IUrlAccessor **ppAccessor) = 0;

                           HRESULT CloseAccessor(
                                  /* [in] */ IUrlAccessor *pAccessor) = 0;

                           HRESULT SetProcessMemorySize(
                                  /* [in] */ DWORD dwFltrDmnMemoryQuota) = 0;
                     };

struct AccessorInitParameters
                     {
                           LPCWSTR pwszUrl;
                           LPCWSTR pwszCrawlTarget;
                           BOOL fUseSSLWithCT;
                           BOOL fUseCTForIntranet;
                           DWORD eAuthenticationType;
                           LPCWSTR pwszUser;
                           LPCWSTR pwszPassword;
                           LPCWSTR pwszHttpFrom;
                           FILETIME ftIfModifiedSince;
                           DWORD dwCrawlId;
                           DWORD dwMiniCrawlID;
                           DWORD dwDeletedCount;
                           DWORD dwDeletedCountSync;
                           BOOL fDeletedCountValid;
                           LPCWSTR pwszAppName;
                           LPCWSTR pwszCatName;
                           DWORD dwFilterPipeFlags;
                           LPCWSTR pwszContentClass;
                           LPCWSTR pwszSearchPropertyMappingUrl;
                           BYTE *pbChangeLogCookie;
                           DWORD cbChangeLogCookieLength;
                           BYTE *pbChangeLogCookieEnd;
                           DWORD cbChangeLogCookieEndLength;
                           LPCWSTR pwszFormsAuthURL;
                           LPCWSTR pwszFormsAuthPost;
                           BYTE *pbCachedBlob;
                           DWORD cbCachedBlobLength;
                           DWORD dwPHFlags;
                           LPCWSTR pwszSecurityId;
                           LPCWSTR pwszCorrelationId;
                           CLSID *pTenantID;
                           HANDLE hImpersonationToken;

                     }      AccessorInitParams;
```

* <span data-ttu-id="ce046-119">AccessorInitParams enthält zahlreiche Parameter, von denen einige möglicherweise optional sind.</span><span class="sxs-lookup"><span data-stu-id="ce046-119">AccessorInitParams contains many parameters, some of which may be optional.</span></span> <span data-ttu-id="ce046-120">Diese Parameter sind hauptsächlich eine Erweiterung von früheren veralteten Strukturen.</span><span class="sxs-lookup"><span data-stu-id="ce046-120">These parameters are mostly an expansion of previous deprecated structs.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="ce046-121">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="ce046-121">Additional Resources</span></span>
<span data-ttu-id="ce046-122"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ce046-122"></span></span>

<span data-ttu-id="ce046-123">Weitere Informationen finden Sie unter [Enterprise Search-Protokollhandler](https://msdn.microsoft.com/de-de/library/office/aa981260%28v=office.12%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce046-123">For more information, see  [Enterprise Search Protocol Handlers](https://msdn.microsoft.com/de-de/library/office/aa981260%28v=office.12%29.aspx).</span></span>
  
    
    

