---
title: Konfigurieren der Sicherheit auf Elementebene in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ffd730f2-e7b7-4707-b677-d073da7df7d7
ms.openlocfilehash: a04fac042531932e2fefad7c820aee16f3d3386e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="configure-item-level-security-in-sharepoint"></a><span data-ttu-id="8131f-102">Konfigurieren der Sicherheit auf Elementebene in SharePoint</span><span class="sxs-lookup"><span data-stu-id="8131f-102">How to: Configure item-level security in SharePoint</span></span>

<span data-ttu-id="8131f-103">In diesem Artikel erfahren Sie, wie Sie die Sicherheit auf Elementebene konfigurieren, wenn externe Daten mit BCS-Indizierungsconnectors in SharePoint durchforstet werden.</span><span class="sxs-lookup"><span data-stu-id="8131f-103">Learn how to configure item level security when crawling external data with BCS indexing connectors in SharePoint.</span></span>

## <a name="external-systems-with-ntlm-authentication"></a><span data-ttu-id="8131f-104">Externe Systeme mit NTLM-Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="8131f-104">External systems with NTLM authentication</span></span>
<span data-ttu-id="8131f-105"><a name="ItemLevelSecurity_NTLMAuth"> </a></span><span class="sxs-lookup"><span data-stu-id="8131f-105"><a name="ItemLevelSecurity_NTLMAuth"> </a></span></span>

<span data-ttu-id="8131f-p101">Für externe Systeme, die die NTLM-Authentifizierung unterstützen, kann der Sicherheitsdeskriptor jeder Instanz des externen Inhaltstyps zum Durchforstungszeitpunkt abgerufen und im Inhaltsindex gespeichert werden. Zum Abfragezeitpunkt wird der Sicherheitsdeskriptor des Benutzers, der die Suchabfrage übermittelt, mit dem gespeicherten Sicherheitsdeskriptor verglichen, um zu bestimmen, ob der Benutzer Zugriff auf das Element hat. Dies ist die schnellste Möglichkeit zum Anwenden der sicherheitsbezogenen Einschränkung auf das Resultset. Das Metadatenmodell des externen Systems muss angeben, in dem der Sicherheitsdeskriptor als externe(s) Inhaltstypfeld bzw. Inhaltstypmethode gefunden werden kann.</span><span class="sxs-lookup"><span data-stu-id="8131f-p101">For external systems that support NTLM authentication, the security descriptor can be obtained for each instance of the external content type at crawl time and stored in the content index. During query time, the security descriptor of the user who is submitting the search query is compared to the stored security descriptor to determine whether the user has access to the item. This is the fastest way to perform security trimming on the result set. The metadata model for the external system must indicate where the security descriptor can be found as an external content type field or method.</span></span>
  
    
    

### <a name="external-content-type-field"></a><span data-ttu-id="8131f-110">Externes Inhaltstypfeld</span><span class="sxs-lookup"><span data-stu-id="8131f-110">External content type field</span></span>
<span data-ttu-id="8131f-111"><a name="ItemLevelSecurity_ExtTypeField"> </a></span><span class="sxs-lookup"><span data-stu-id="8131f-111"><a name="ItemLevelSecurity_ExtTypeField"> </a></span></span>

<span data-ttu-id="8131f-112">Microsoft SharePoint speichert den Sicherheitsdeskriptor, wenn das Feld des externen Inhaltstyps, das den Deskriptor enthält markiert wird mithilfe der **WindowsSecurityDescriptorField** -Eigenschaft, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="8131f-112">Microsoft SharePoint stores the security descriptor if the field of the external content type that contains the descriptor is marked by using the **WindowsSecurityDescriptorField** property, as shown in the following example.</span></span>
  
    
    

```XML

<Method Name="Item SpecificFinder ">
  <Properties>
    <Property Name="RdbCommandType" Type="System.Data.CommandType, System.Data, 
 Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">Text</Property>
    <Property Name="RdbCommandText" Type="System.String">SELECT [Identifier] , 
 [SecurityDescriptor] FROM [Test].[dbo].[Items] WHERE [Identifier] = @Identifier</Property>
    <Property Name="BackEndObjectType" Type="System.String">SqlServerTable</Property>
    <Property Name="BackEndObject" Type="System.String">Items</Property>
    <Property Name="Schema" Type="System.String">dbo</Property>
  </Properties>
  <Parameters>
    <Parameter Direction="In" Name="@Identifier">
      <TypeDescriptor TypeName="System.Int32" IdentifierName="Identifier" Name="Identifier" />
    </Parameter>
    <Parameter Direction="Return" Name="BaseItemsRead Item">
      <TypeDescriptor TypeName="System.Data.IDataReader, System.Data, Version=2.0.0.0, 
Culture=neutral, PublicKeyToken=b77a5c561934e089" IsCollection="true" Name="BaseItemsRead Item">
        <TypeDescriptors>
          <TypeDescriptor TypeName="System.Data.IDataRecord, System.Data, Version=2.0.0.0, 
Culture=neutral, PublicKeyToken=b77a5c561934e089" Name="BaseItemsRead ItemElement">
          <TypeDescriptors>
            <TypeDescriptor TypeName="System.Int32" IdentifierName="Identifier" Name="Identifier"/>
            <TypeDescriptor TypeName="System.Byte[], mscorlib, Version=2.0.0.0, 
Culture=neutral, PublicKeyToken=b77a5c561934e089" IsCollection="true" Name="SecurityDescriptor">
              <TypeDescriptors>
                <TypeDescriptor TypeName="System.Byte" Name="SecurityDescriptorElement" />
              </TypeDescriptors>
            </TypeDescriptor>
            </TypeDescriptors>
          </TypeDescriptor>
          </TypeDescriptors>
        </TypeDescriptor>
      </Parameter>
    </Parameters>
    <MethodInstances>
      <MethodInstance Type="SpecificFinder" ReturnParameterName="BaseItemsRead Item"
 ReturnTypeDescriptorName="BaseItemsRead ItemElement" Name="BaseItemsRead Item"
DefaultDisplayName="ReadSecurity">
        <Properties>
          <Property Name="WindowsSecurityDescriptorField" Type="System.String">
                SecurityDescriptor
          </Property>
        </Properties>
      </MethodInstance>
    </MethodInstances>
</Method>
```

> [!NOTE]
> <span data-ttu-id="8131f-113">Der Grund hierfür ist, dass zwischengespeicherte Elemente auf eine bestimmte Größe beschränkt sind, die Zugriffssteuerungslisten (ACLs) überschreiten können.</span><span class="sxs-lookup"><span data-stu-id="8131f-113">This is because cached items are limited to a specific size, which access control lists (ACL) can easily exceed.</span></span> <span data-ttu-id="8131f-114">Daher ignoriert das Suchconnectorframework Anforderungen zum Zwischenspeichern von Elementen, wenn diese ein Feld mit der Sicherheitsbeschreibung enthalten.</span><span class="sxs-lookup"><span data-stu-id="8131f-114">Therefore, the Search connector framework ignores requests to cache items if they contain a security descriptor field.</span></span> 
  
    
    


### <a name="external-content-type-method"></a><span data-ttu-id="8131f-115">Methode für externen Inhaltstyp</span><span class="sxs-lookup"><span data-stu-id="8131f-115">External content type method</span></span>
<span data-ttu-id="8131f-116"><a name="ItemLevelSecurity_ExtTypeMethod"> </a></span><span class="sxs-lookup"><span data-stu-id="8131f-116"></span></span>

<span data-ttu-id="8131f-117">Wenn im Metadatenmodell eine Methode definiert ist, die den Sicherheitsdeskriptor eines Elements basierend auf dessen ID zurückgibt, können Sie den Stereotyp der **BinarySecurityDescriptorAccessor**-Methode verwenden (siehe das folgende Beispiel).</span><span class="sxs-lookup"><span data-stu-id="8131f-117">If you have a method defined in the metadata model that returns the security descriptor for an item based on its identifier, you can use the **BinarySecurityDescriptorAccessor** method stereotype, as shown in the following example.</span></span>
  
    
    

```XML

<Method Name="GetItemSecurity" LobName="GetItemSecurity">
  <Parameters>
    <Parameter Name="itemId" Direction="In">
      <TypeDescriptor Name="itemId" TypeName="System.Int32, mscorlib, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" 
IdentifierEntityNamespace="MS.Internal.Test.Automation.Search.Scater" 
IdentifierEntityName="Item" IdentifierName="ItemId" /> 
    </Parameter>
    <Parameter Name="Return" Direction="Return">
      <TypeDescriptor Name="SecurityDescriptor" TypeName="System.Byte[],
mscorlib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" 
IsCollection="true">
        <TypeDescriptors>
          <TypeDescriptor Name="Item" TypeName="System.Byte, mscorlib, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
        </TypeDescriptors>
      </TypeDescriptor>
    </Parameter>
  </Parameters>
  <MethodInstances>
    <MethodInstance Name="GetItemSecurity_Instance" Type="BinarySecurityDescriptorAccessor"
 ReturnParameterName="Return" ReturnTypeDescriptorName="SecurityDescriptor" 
ReturnTypeDescriptorLevel="0">
      <Properties>
        <Property Name="WindowsSecurityDescriptorField" Type="System.String">
            SecurityDescriptor
        </Property>
      </Properties>
      <AccessControlList>
        <AccessControlEntry Principal="NT AUTHORITY\\Authenticated Users">
          <Right BdcRight="Execute" />
        </AccessControlEntry>
      </AccessControlList>
    </MethodInstance>
  </MethodInstances>
</Method>
```

<span data-ttu-id="8131f-118">Der folgende Code ist die Methodensignatur der im vorherigen Beispiel angegebenen Methode.</span><span class="sxs-lookup"><span data-stu-id="8131f-118">The following code is the method signature for the method that is specified in the previous example.</span></span>
  
    
    



```cs

Public static Byte[]GetItemSecurity (string  id)
{

}
```


## <a name="external-systems-with-authentication-schemes-that-can-be-mapped-to-ntlm-authentication"></a><span data-ttu-id="8131f-119">Externe Systeme mit Authentifizierungsschemas, die der NTLM-Authentifizierung zugeordnet werden können</span><span class="sxs-lookup"><span data-stu-id="8131f-119">External systems with authentication schemes that can be mapped to NTLM authentication</span></span>
<span data-ttu-id="8131f-120"><a name="ItemLevelSecurity_MappedToNTLM"> </a></span><span class="sxs-lookup"><span data-stu-id="8131f-120"></span></span>

<span data-ttu-id="8131f-p103">Wenn das externe System nicht die NTLM-Authentifizierung unterstützt, die Benutzer des externen Systems aber über eine Zuordnungstabelle Windows-Benutzern zugeordnet werden können, kann zum Bereitstellen von Sicherheit auf Elementebene der in den beiden vorherigen Codebeispielen beschriebene Ansatz befolgt werden. Damit dies funktioniert, muss der Web- oder Windows Communication Foundation (WCF)-Dienst, der vom externen System verfügbar gemacht wird, eine Methode enthalten, die die Benutzer des externen Systems intern in Windows-Benutzer umwandelt und anschließend für jede URL einen Windows-Sicherheitsdeskriptor zurückgibt. Das folgende Beispiel veranschaulicht, wie Sie diese Methode codieren können.</span><span class="sxs-lookup"><span data-stu-id="8131f-p103">If the external system does not support NTLM authentication, but the external system users can be mapped to Windows users by using a mapping table, you can use the approach described in the previous two code examples to provide item level security. For this to work, the web service or Windows Communication Foundation (WCF) service exposed by the external system must include a method that converts the external system users to Windows users internally, and then returns a Windows security descriptor for each URL. The following example shows how you could code this method.</span></span> 
  
    
    

```cs

/// Returns the security descriptor for a user.
/// </summary>
/// <param name="domain"></param>
/// <param name="username"></param>
/// <returns></returns>

private Byte[] GetSecurityDescriptor(string domain, string username)
{
   NTAccount acc = new NTAccount(domain, username);
   SecurityIdentifier sid = (SecurityIdentifier)acc.Translate(typeof(SecurityIdentifier));
   CommonSecurityDescriptor sd = new CommonSecurityDescriptor(false, false, ControlFlags.None,
sid, null, null, null);
   sd.SetDiscretionaryAclProtection(true, false);

//Deny access to all users.
   SecurityIdentifier everyone = new SecurityIdentifier(WellKnownSidType.WorldSid, null);
   sd.DiscretionaryAcl.RemoveAccess(AccessControlType.Allow, everyone, 
unchecked((int)0xffffffffL), InheritanceFlags.None, PropagationFlags.None);

//Grant full access to a specified user.
   sd.DiscretionaryAcl.AddAccess(AccessControlType.Allow, sid, 
unchecked((int)0xffffffffL), InheritanceFlags.None, PropagationFlags.None);
 
   byte[] secDes = new Byte[sd.BinaryLength];
   sd.GetBinaryForm(secDes, 0);

   return secDes;
}
```


## <a name="see-also"></a><span data-ttu-id="8131f-124">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="8131f-124">See also</span></span>
<span data-ttu-id="8131f-125"><a name="SP15Itemlevelsec_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="8131f-125"></span></span>


-  [<span data-ttu-id="8131f-126">Connector Framework für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="8131f-126">Search connector framework in SharePoint</span></span>](search-connector-framework-in-sharepoint.md)
    
  
-  <span data-ttu-id="8131f-127">[Implementieren von "BinarySecurityDescriptorAccessor"](http://msdn.microsoft.com/library/6cf70490-dd3c-49cd-bb13-ed33e938435d%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="8131f-127">[Implementing a BinarySecurityDescriptorAccessor](http://msdn.microsoft.com/library/6cf70490-dd3c-49cd-bb13-ed33e938435d%28Office.15%29.aspx)</span></span>
    
  
-  [<span data-ttu-id="8131f-128">Optimieren der BDC-Modelldatei für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="8131f-128">Enhancing the BDC model file for Search in SharePoint</span></span>](enhancing-the-bdc-model-file-for-search-in-sharepoint.md)
    
  

