---
title: Entwickeln mit Duet Enterprise 2.0
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c3ef38aa-559e-4832-95c7-75e222c77624
ms.openlocfilehash: 15b9ac70484db215dd36a46d3648999aa26664e5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="developing-with-duet-enterprise-20"></a>Entwickeln mit Duet Enterprise 2.0

## <a name="overview"></a>Übersicht
<a name="Overview"> </a>

Duet Enterprise 2.0 ist die neueste Version einer gemeinsamen Initiative zwischen Microsoft- und SAP, SharePoint-Benutzern die Möglichkeit zum Arbeiten mit Daten aus SAP-Systemen zu ermöglichen. Komponenten von SAP sowie SharePoint und SharePoint Online kombiniert. Es ermöglicht Entwicklern die Möglichkeit zum Erstellen von Komponenten, die Benutzern ermöglichen, Daten aus SAP-Systemen in der vertrauten SharePoint-Umgebung zu bringen.
  
    
    

## <a name="features-of-duet-enterprise-20"></a>Features von Duet Enterprise 2.0
<a name="Overview"> </a>

Wenn ordnungsgemäß installiert und konfiguriert ist, wird Duet Enterprise 2.0 folgende Features zu ermöglichen:
  
    
    

- Sie können mit Daten in SAP-Systemen in SharePoint mithilfe von Geschäftsdaten-Webparts, externe Listen und benutzerdefinierten Komponenten arbeiten.
    
  
- Verwenden von SAP-Daten in SharePoint ohne Code mithilfe der integrierte Komponenten.
    
  
- Verwenden von SAP-Systeme innerhalb einer app, die Berichte.
    
  
- Verwenden Sie spezielle Webparts zum Hinzufügen von SAP-Informationen zu SharePoint-Seiten mit Duet Enterprise 2.0 installiert
    
  
- Verwenden von SAP-Workflow in einer app.
    
  
- Entwickler können mithilfe der clientseitigen JavaScript zum interagieren mit SAP externe Daten verwenden.
    
  
- Sichern Sie Daten mithilfe von OAuth zur Authentifizierung.
    
  

## <a name="setting-up-the-development-environment"></a>Einrichten der Entwicklungsumgebung
<a name="SettingUp"> </a>

Die Entwicklung von SharePoint-Add-Ins mit Duet Enterprise 2.0 entspricht in den meisten Fällen der Erstellung von standardmäßigen SharePoint-Add-Ins. Sie können Visual Studio verwenden, um Ihre Apps zu erweitern und in dem stabilen Framework im Rahmen der integrierten Visual Studio-Entwicklungsumgebung zu arbeiten.
  
    
    

## <a name="adding-external-content-types"></a>Hinzufügen externer Inhaltstypen
<a name="AddingECT"> </a>

Um die externen Daten, die diese auf dem SAP-System zugreifen zu können, müssen Sie einen externen Inhaltstyp hinzuzufügen. Da SAP-Daten über OData-Endpunkte verfügbar gemacht werden, können die automatische Generierung Tools in Visual Studio installiert auf  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) verwendet werden, die auf der Ebene der app ausgelegt ist.
  
    
    
Führen Sie die folgenden Schritte aus, um einen externen Inhaltstyp zu erstellen:
  
    
    

### <a name="creating-an-external-content-type-from-an-sap-odata-endpoint"></a>Erstellen eines externen Inhaltstyps aus einem SAP-OData-Endpunkt


1. Öffnen Sie im **Projektmappen-Explorer**das Kontextmenü für das Projekt, und wählen Sie **Hinzufügen** und **Inhaltstypen für externe Datenquelle** aus.
    
  
2. Geben Sie auf der Seite **OData-Quelle anzugeben** die URL der Duet Enterprise-Workflow-Dienst.
    
  
3. Wählen Sie einen Namen für die OData-Quelle.
    
  
4. Wählen Sie die Entitäten, die erforderlich sind.
    
  
5. Wählen Sie **Fertig stellen** aus.
    
  
Visual Studio erstellt einen neuen Ordner mit dem Namen externer Inhaltstypen Sie das neu erstellte BDC-Modell finden.
  
    
    

## <a name="configuring-the-bdc-model"></a>Konfigurieren des BDC-Modells
<a name="ConfiguringProject"> </a>

Stellen Sie das Projekt für die Verwendung der wichtigste wird die **ODataExtensionProvider** -Eigenschaft des BDC-Modells hinzugefügt. Diese Eigenschaft definiert den Erweiterung-Anbieter, der BCS mit den SAP-Erweiterungen für das Erstellen von app-Code benötigt bereitstellt.
  
    
    
In diesem Beispiel werden die Eigenschaften gezeigt, das BDC-Modell hinzugefügt:
  
    
    



```XML

<LobSystem Type="OData" Name="LOB_SYSTEM_NAME">
                     <Properties>
                          <Property Name="ODataServiceMetadataUrl" Type="System.String">
                               https://<DUET_METADATA_URL>:443/sap/opu/odata/sap/ 
                               ZANDY_PO_HEADER_SRV/$metadata</Property>
                          <Property Name="ODataServicesVersion" Type="System.String">2.0</Property>
                          <Property Name="ODataExtensionProvider" Type="System.String"> 
                               OBA.Server.Canary.ObaOdataServerExtensionProvider, 
                               OBA.Server.SSOProvider, 
                               Version=15.0.0.0, 
                               Culture=neutral, 
                               PublicKeyToken=71e9bce111e9429c</Property>
                          <Property Name="TraceHeader" Type="System.String">SAP-PASSPORT</Property>
                     </Properties>

```


## <a name="using-duet-starter-services-to-develop-custom-apps"></a>Entwickeln von benutzerdefinierten apps mithilfe von Duet Starter services
<a name="UsingDuetStarterServices"> </a>

Duet Enterprise 2.0 installiert mehrere Starterdienste im Dateisystem auf dem SharePoint-Server. In einer Standardinstallation befinden sich die Dateien im Verzeichnis C:\\Programme\\Duet Enterprise\\2.0\\Solutions\\Starter Services. Dies sind: 
  
    
    

- OBACustomerWorkspace
    
  
- OBAOrderToCash
    
  
- OBAPortal
    
  
- OBAProductCenter
    
  
Jede dieser Lösungen enthält WSP-Dateien, Lösung und andere unterstützenden Dateien benötigt, sie zu implementieren.
  
    
    
Diese Lösungen werden kann, finden Sie unter Was mit Duet Enterprise 2.0 ausgeführt werden können und was die Entwicklung Muster sind, aber nicht für die Verwendung in SharePoint-Add-Ins unterstützt werden.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="ConNavExample_resources"> </a>


-  
  [Duet Enterprise für Microsoft SharePoint und SAP Server 2.0](http://technet.microsoft.com/en-us/library/ff972436.aspx)
    
  
-  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [Visual Studio Developer Center](http://msdn.microsoft.com/en-us/vstudio/default)
    
  
-  [Office-Entwicklung mit Visual Studio](http://msdn.microsoft.com/en-us/office/hh133430)
    
  

