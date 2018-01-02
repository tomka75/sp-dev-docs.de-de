---
title: Add-in-bezogenen externen Inhaltstypen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a34cbbba-dc38-4d3d-b796-d54b5848bdfb
ms.openlocfilehash: 32f456c117615566a1b63b8991a231121ae2164f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="add-in-scoped-external-content-types-in-sharepoint"></a>Add-in-bezogenen externen Inhaltstypen in SharePoint
Erfahren Sie mehr über externe Inhaltstypen, die installiert oder auf der Ebene-Add-Ins in SharePoint ausgelegt sind, und aktivieren Sie reichhaltige SharePoint-Add-Ins mit externen Datenquellen erstellen.
## <a name="overview-of-add-in-scoped-external-content-types-in-sharepoint"></a>Übersicht über die add-in-bezogenen externen Inhaltstypen in SharePoint
<a name="Appscopedect_overview"> </a>

In SharePoint 2010 können Sie installieren und Verwenden von externen Inhaltstypen nur auf Farmebene. Daraufhin wird häufig Probleme für Entwickler, da auch für einfache Applications Administrator beteiligten aufgrund der Zugriffsrechte sein, die erforderlich sind musste, um auf Farmebene zu installieren.
  
    
    
In SharePoint sind Anwendungen im Wesentlichen in mehr autonomen Einheiten mit dem Namen -add-insisoliert. -Add-ins enthalten alle Ressourcen, die sie ausführen müssen. Dieser Ansatz ermöglicht eine aktive Anwendung auf aus anderen Anwendungen isoliert werden. Die Vorteile dieser Architektur sind wie folgt:
  
    
    

- Erstellen Sie add-ins, die an das neue Anwendungsmodell des SharePoint ausgerichtet werden.
    
  
- Erstellen Sie add-ins, die Zugriff auf externe Daten von SAP, Netflix, und proprietäre und andere Typen von Daten ohne im Zusammenhang mit der mandantenadministrator.
    
  
- Zugriff auf externe Anwendungen wird durch Business Connectivity Services (BCS), beibehalten, die eine konsistente und einheitliche Benutzeroberfläche bereitstellt, die von anderen SharePoint-Anwendungen verwendet werden kann.
    
  
Add-in-bezogenen externe Inhaltstypen ermöglichen den Zugriff auf externe Daten in einer app.
  
    
    

## <a name="prerequisites-for-working-with-add-in-scoped-external-content-types"></a>Erforderliche Komponenten für die Arbeit mit der add-in-bezogenen externen Inhaltstypen
<a name="Appscopedect_Prereq"> </a>

Im folgenden sind die Anforderungen für die Entwicklung von externen Inhaltstypen, die auf der Ebene der Add-in-Bereich haben:
  
    
    

- Visual Studio 2012
    
  
- Office Developer Tools für Visual Studio 2012
    
  
- SharePoint
    
  
Informationen dazu, wie Sie Ihre SharePoint-Entwicklungsumgebung einrichten, finden Sie unter  [Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

### <a name="add-in-scoped-external-content-type-essentials"></a>Add-in-bezogenen externen Inhaltstyp essentials

Tabelle 1 enthält einige wichtige Konzepte, denen Sie mit vertraut beim Arbeiten mit der add-in-bezogenen externen Inhaltstypen sein sollten.
  
    
    

**In Tabelle 1. Kernkonzepte für das Verständnis von add-in-bezogenen externer Inhaltstypen**


|**Artikel**|**Beschreibung**|
|:-----|:-----|
| [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md) <br/> |Erfahren Sie, wie BCS externen Inhaltstypen erstellen.  <br/> |
| [SharePoint-Add-Ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |Hier finden Sie Informationen über das neue Add-In-Modell in SharePoint, das es Ihnen ermöglicht, Add-Ins als kompakte, einfach zu verwendende Lösungen für Endbenutzer zu erstellen.  <br/> |
| [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](http://msdn.microsoft.com/library/1b992485-6efe-4ea4-a18c-221689b0b66f%28Office.15%29.aspx) <br/> |Informationen Sie zur Erstellung eines einfachen SharePoint-Hosting add-Ins mithilfe der Office Developer Tools für Visual Studio 2012.  <br/> |
   

## <a name="what-can-you-do-with-add-in-scoped-external-content-types"></a>Was können Sie mit der add-in-bezogenen externen Inhaltstypen?
<a name="Appscopedect_Tasks"> </a>

Der Hauptgrund für das Hinzufügen eines Add-in-bezogenen externen Inhaltstyps ist für den Zugriff auf externe Daten aus einer einzelnen-Add-in. Hiermit können Sie folgende Aktionen ausführen: 
  
    
    

- Einschränken des Zugriffs auf externe Inhaltstypen zu einer bestimmten app.
    
  
- Bereitstellen von externen Inhaltstypen in einer app.
    
  

### <a name="create-add-in-scoped-external-content-types"></a>Erstellen von add-in-bezogenen externen Inhaltstypen
<a name="Appscopedect_createect"> </a>

Das Konzept eines Katalogs dateibasierten Metadaten wurde in SharePoint 2010 eingeführt. Es können Sie angeben, dass eine Datei mit dem XML benötigt, um externe Inhaltstypen zu definieren. Diese Datei in eine WSP-Paket bereitgestellt werden kann und bezieht sich nur auf die Anwendung, der sie für ausgelegt ist. Mithilfe dieser Metadatendatei können externe Inhaltstypen auf die-Add-in-Ebene beschränkt.
  
    
    
In SharePoint wurde **SPListDataSource** geändert, um eine Eigenschaft hinzuzufügen, die den Bereich der Anwendung angibt.
  
    
    
Diese Klasse dient als die Brücke zwischen **SPList** und einer externen Liste. Verwenden Sie die zugeordneten **SPList** Entitätsfelder und Daten abgerufen. Eine Instanz des **SPListDataSource** aus der **HasExternalDataSource** -Eigenschaft abrufen. Wenn **HasExternalDataSource** nicht null ist, ist das **SPList** -Objekt Daten außerhalb SharePoint.
  
    
    
Wenn Sie einen Add-in-bezogenen externen Inhaltstyp hinzufügen möchten, ist diese Eigenschaft auf **Add-in**festgelegt.
  
    
    
Die **MetadataCatalogFileName** -Eigenschaft wird verwendet, um die BDC-Modelldatei zu definieren, die die Definition des externen Inhaltstyps enthält. Diese Eigenschaft kann deklarativ oder programmgesteuert definiert werden, aber nicht in der SharePoint-Benutzeroberfläche (UI).
  
    
    
Im folgenden Beispiel wird gezeigt, wie Sie die **MetadataCatalogFileName**-Eigenschaft deklarativ festlegen können.
  
    
    



```XML

<DataSource>
  <Property Name="Entity" Value="Customer" />
  <Property Name="EntityNamespace" Value="SAP" />
  <Property Name="LobSystemInstanceName" Value="SAPClient1" />
  <Property Name="SpecificFinder" Value="ReadCustomer" />
  <Property Name=" MetadataCatalogFileName" Value="BDCMetadata.bdcm" />
</DataSource>
```


> [!NOTE]
> Websiteadministratoren können Add-Ins installieren, die App-bezogene externe Inhaltstypen verwenden, nur SiteCollection-Administratoren können jedoch Apps Berechtigungen zum Verwenden von BCS-Verbindungen gewähren. 
  
    
    


### <a name="deploy-an-add-in-scoped-external-content-type-in-a-custom-feature-in-a-wsp-file"></a>Bereitstellen eines Add-In-bezogenen externen Inhaltstyps in einer benutzerdefinierten Funktion in einer WSP-Datei
<a name="Appscopedect_deployect"> </a>

Sie können ein BDC-Modell in eine WSP-Datei für die Bereitstellung einschließen. Im folgenden Beispiel wird veranschaulicht, wie ein BDC-Modell in der app werden soll.
  
    
    

```XML

<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <BdcModel Path="BDCMetadata.bdcm">
  </BdcModel>
</Elements>

```


> [!IMPORTANT]
> Es kann nur eine BDC-Modelldatei pro Add-In verwendet werden. In diesem Beispiel lautet der Dateiname BDCMetadata.bdcm, der Modelldateiname kann beliebig sein, solange dieser dem Dateinamen im **Path**-Attribut der BDC-Modelldatei entspricht.
  
    
    


> [!NOTE]
> Nur Open Data Protocol (OData)-Verbindungen sind für Add-In-bezogene externe Inhaltstypen zulässig. 
  
    
    


### <a name="set-security-credentials-for-an-external-system"></a>Festlegen von Sicherheitsanmeldeinformationen für ein externes System
<a name="Appscopedect_deployect"> </a>

Um Daten für eine sichere externe System zugreifen zu können, müssen Sie das BDC-Modell mit den entsprechenden Anmeldeinformationen konfigurieren.
  
    
    
Im folgenden Beispiel wird gezeigt, wie durch Bearbeiten der Datei "Elements.xml" der app Sicherheitsanmeldeinformationen für ein externes System add-in-bezogenen externen Inhaltstypen festgelegt.
  
    
    



```XML

<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <BdcModel Path="BDCMetadata.bdcm">
    <LobSystem Name="SAP">
       <LobSystemInstance Name="SAPInst" RequireCredentials="true" CredentialsDescription="Credentials to connect to SAP"/>
    </LobSystem>
    <LobSystem Name="SQL">
       <LobSystemInstance Name="App Database" DataSource="SQL-Azure" RequireCredentials="true" />
    </LobSystem>
  </BdcModel>
</Elements>

```


## <a name="in-this-section"></a>Inhalt dieses Abschnitts
<a name="Appscopedect_inthissection"> </a>


-  [Vorgehensweise: erstellen ein Add-in-bezogenen externes Inhaltstyps in SharePoint](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [Vorgehensweise: Zugriff auf externe Daten mit REST in der SharePoint](how-to-access-external-data-with-rest-in-sharepoint.md)
    
  

## <a name="see-also"></a>Siehe auch
<a name="Appscopedect_Addres"> </a>


-  [Business Connectivity Services in SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Business Connectivity Services-Programmierreferenz für SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [SharePoint-Add-Ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [Externe Inhaltstypen in SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Externe Ereignisse und Warnungen in SharePoint](external-events-and-alerts-in-sharepoint.md)
    
  
-  [Was ist neu in Business Connectivity Services in SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Erste Schritte mit den Business Connectivity Services in SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  

