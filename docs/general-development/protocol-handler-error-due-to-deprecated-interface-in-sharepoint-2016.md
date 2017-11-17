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
# <a name="protocol-handler-error-due-to-deprecated-interface-in-sharepoint-2016"></a>Protokollhandlerfehler aufgrund von nicht mehr unterstützter SharePoint 2016-Oberfläche

Protokollhandlerimplementierungen mithilfe der in diesem Artikel in der Header-Datei **srchprth.h** aufgeführten Schnittstellen werden in SharePoint 2016 jetzt nicht mehr unterstützt. Vor allem der Protokollhandler für nicht mehr unterstützte Schnittstellen generiert die Fehlermeldung "Der Protokollhandler kann nicht geladen werden".
  
    
    


## <a name="symptom"></a>Symptom

Wenn Sie den Protokollhandler laden die, wird die folgende Fehlermeldung angezeigt:
  
    
    

```

The protocol handler <name of custom protocol handler> cannot be loaded. Error description: No such interface supported.
```


### <a name="cause"></a>Ursache

Sie verwenden die Header-Datei **srchprth.h** bei Ihrer Protokollhandlerimplementierung. Diese Datei enthält Schnittstellen, die in SharePoint 2016 nicht mehr unterstützt werden.
  
    
    

### <a name="resolution"></a>Auflösung

Ersetzen Sie die veralteten Schnittstellen in Ihrer Protokollhandlerimplementierung mit Schnittstellen, die derzeit unterstützt werden:
  
    
    

- **srchprth.h** (aktualisiert)
    
  
- **urlaccsdk.h** (neu)
    
  

## <a name="deprecated-interfaces"></a>Veraltete Schnittstellen
<a name="bk_addresources"> </a>

Zu diesen nicht mehr unterstützten Schnittstellen gehören unter anderem:
  
    
    
 **interface ISearchProtocol : IUnknown**
  
    
    



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

 **IProtocolHandler: public IUnknown**
  
    
    



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

* AccessorInitParams enthält zahlreiche Parameter, von denen einige möglicherweise optional sind. Diese Parameter sind hauptsächlich eine Erweiterung von früheren veralteten Strukturen.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

Weitere Informationen finden Sie unter [Enterprise Search-Protokollhandler](https://msdn.microsoft.com/en-us/library/office/aa981260%28v=office.12%29.aspx).
  
    
    

