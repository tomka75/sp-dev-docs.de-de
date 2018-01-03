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
# <a name="configure-item-level-security-in-sharepoint"></a>Konfigurieren der Sicherheit auf Elementebene in SharePoint

In diesem Artikel erfahren Sie, wie Sie die Sicherheit auf Elementebene konfigurieren, wenn externe Daten mit BCS-Indizierungsconnectors in SharePoint durchforstet werden.

## <a name="external-systems-with-ntlm-authentication"></a>Externe Systeme mit NTLM-Authentifizierung
<a name="ItemLevelSecurity_NTLMAuth"> </a>

Für externe Systeme, die die NTLM-Authentifizierung unterstützen, kann der Sicherheitsdeskriptor jeder Instanz des externen Inhaltstyps zum Durchforstungszeitpunkt abgerufen und im Inhaltsindex gespeichert werden. Zum Abfragezeitpunkt wird der Sicherheitsdeskriptor des Benutzers, der die Suchabfrage übermittelt, mit dem gespeicherten Sicherheitsdeskriptor verglichen, um zu bestimmen, ob der Benutzer Zugriff auf das Element hat. Dies ist die schnellste Möglichkeit zum Anwenden der sicherheitsbezogenen Einschränkung auf das Resultset. Das Metadatenmodell des externen Systems muss angeben, in dem der Sicherheitsdeskriptor als externe(s) Inhaltstypfeld bzw. Inhaltstypmethode gefunden werden kann.
  
    
    

### <a name="external-content-type-field"></a>Externes Inhaltstypfeld
<a name="ItemLevelSecurity_ExtTypeField"> </a>

Microsoft SharePoint speichert den Sicherheitsdeskriptor, wenn das Feld des externen Inhaltstyps, das den Deskriptor enthält markiert wird mithilfe der **WindowsSecurityDescriptorField** -Eigenschaft, wie im folgenden Beispiel dargestellt.
  
    
    

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
> Der Grund hierfür ist, dass zwischengespeicherte Elemente auf eine bestimmte Größe beschränkt sind, die Zugriffssteuerungslisten (ACLs) überschreiten können. Daher ignoriert das Suchconnectorframework Anforderungen zum Zwischenspeichern von Elementen, wenn diese ein Feld mit der Sicherheitsbeschreibung enthalten. 
  
    
    


### <a name="external-content-type-method"></a>Methode für externen Inhaltstyp
<a name="ItemLevelSecurity_ExtTypeMethod"> </a>

Wenn im Metadatenmodell eine Methode definiert ist, die den Sicherheitsdeskriptor eines Elements basierend auf dessen ID zurückgibt, können Sie den Stereotyp der **BinarySecurityDescriptorAccessor**-Methode verwenden (siehe das folgende Beispiel).
  
    
    

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

Der folgende Code ist die Methodensignatur der im vorherigen Beispiel angegebenen Methode.
  
    
    



```cs

Public static Byte[]GetItemSecurity (string  id)
{

}
```


## <a name="external-systems-with-authentication-schemes-that-can-be-mapped-to-ntlm-authentication"></a>Externe Systeme mit Authentifizierungsschemas, die der NTLM-Authentifizierung zugeordnet werden können
<a name="ItemLevelSecurity_MappedToNTLM"> </a>

Wenn das externe System nicht die NTLM-Authentifizierung unterstützt, die Benutzer des externen Systems aber über eine Zuordnungstabelle Windows-Benutzern zugeordnet werden können, kann zum Bereitstellen von Sicherheit auf Elementebene der in den beiden vorherigen Codebeispielen beschriebene Ansatz befolgt werden. Damit dies funktioniert, muss der Web- oder Windows Communication Foundation (WCF)-Dienst, der vom externen System verfügbar gemacht wird, eine Methode enthalten, die die Benutzer des externen Systems intern in Windows-Benutzer umwandelt und anschließend für jede URL einen Windows-Sicherheitsdeskriptor zurückgibt. Das folgende Beispiel veranschaulicht, wie Sie diese Methode codieren können. 
  
    
    

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


## <a name="see-also"></a>Siehe auch
<a name="SP15Itemlevelsec_addlresources"> </a>


-  [Connector Framework für die Suche in SharePoint](search-connector-framework-in-sharepoint.md)
    
  
-  [Implementieren von "BinarySecurityDescriptorAccessor"]((http://msdn.microsoft.com/library/6cf70490-dd3c-49cd-bb13-ed33e938435d%28Office.15%29.aspx))
    
  
-  [Optimieren der BDC-Modelldatei für die Suche in SharePoint](enhancing-the-bdc-model-file-for-search-in-sharepoint.md)
    
  

