---
title: Verwenden von SAP-Berichterstellung mit Duet Enterprise 2.0
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a54c6cd2-2283-440d-af55-e98e3212caa1
ms.openlocfilehash: 089a22b0f96c4dd2cb5d4a7ad1808b4307986fb2
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="use-sap-reporting-with-duet-enterprise-20"></a>Verwenden von SAP-Berichterstellung mit Duet Enterprise 2.0

## <a name="introduction"></a>Einführung
<a name="bkmk_Introduction"> </a>

Duet Enterprise 2.0 ermöglicht die Duet-Berichtsfeatures innerhalb Ihrer SharePoint-Add-In integrieren, indem Sie wie folgt ein wenig Anpassung.
  
    
    
Das Kennwort für die Aktivierung der berichterstellung für Ihre app ist mithilfe von einem ausgeblendeten Feature von Duet installiert. Sie müssen dieses Feature benutzerdefinierte Features Heften, damit die Instanziierung die app wird der SAP-Berichterstellungsfeatures die app zur Verfügung gestellt werden werden.
  
    
    

## <a name="enabling-the-features"></a>Aktivieren Sie die Funktionen
<a name="bkmk_EnablingTheFeatures"> </a>

Um die reporting Duet-Funktionen zu aktivieren, muss die Abfolge der Aktivierung sorgfältig folgen.
  
    
    

### <a name="to-create-a-feature-to-add-the-app-scoped-external-content-type"></a>So erstellen Sie eine Funktion, um den app-bezogenen externen Inhaltstyp hinzuzufügen:


1. Innerhalb Ihrer app, die Sie im **Projektmappen-Explorer** reporting Duet klicken Sie mit der rechten Maustaste auf den Projektnamen. Wählen Sie **Hinzufügen**, **Inhaltstypen für eine externe Datenquelle**. Klicken Sie auf **Weiter**.
    
  
2. Geben Sie die URL für den Endpunkt SAP Reporting als OData-Quelle.
    
  
3. Wählen Sie die Entitäten, und wählen Sie **Fertig stellen**.
    
  
4. Öffnen Sie den neu erstellten externen Inhaltstyp, um die LSI-Eigenschaften anzuzeigen. Sie sehen, dass sie die gleichen wie für die Farm-bezogenen externen Inhaltstyp mit Ausnahme der **ODataconnectionSettingsId**sind.
    
  

### <a name="to-create-a-feature-to-enable-the-hidden-duet-features"></a>So erstellen Sie ein Feature, das die ausgeblendeten Duet-Funktionen zu aktivieren:


1. Fügen Sie dem Projekt ein weiteres neues Feature hinzu. Name des Titels **AddDuetReporting**.
    
    Dieses Feature wird eine Abhängigkeit von der **AddReportingModel** und die **DuetReportingForApps** Features haben.
    
  
2. Fügen Sie den folgenden Code in die Datei **Elemente**.
    
```
  
<?xml version="1.0" encoding="utf-8"?>
<Feature xmlns="http://schemas.microsoft.com/sharepoint/" Title="AddDuetReporting" Id="6a55705c-af12-455a-914b-8cf3a31c820e" Scope="Web">
  <ActivationDependencies>
    <ActivationDependency FeatureId="e1fe41d3-7fc3-458f-9a66-6ecf6a39bb2c" FeatureTitle="AddReportingModel" />
    <ActivationDependency FeatureId="9b60ccba-ebfd-4e38-87c8-3dea9cc2680a" FeatureTitle="SAPReportingForApps" />
  </ActivationDependencies>
</Feature>

```

Beachten Sie, dass die Reihenfolge in aktivierungsabhängigkeit wichtig ist. Zunächst müssen Sie den externen Inhaltstyp erstellen und aktivieren Sie das Feature **SAPReportingForApps**. Beachten Sie außerdem, dass das zweite Feature (ID: **9b60ccba-ebfd-4e38-87c8-3dea9cc2680a**) ist im Lieferumfang von Duet Enterprise 2.0, ist aber markiert als ausgeblendet. Bei diesem Ansatz kann Entwickler stellen dieses Feature und können auch die in Duet Reporting-Funktionen zu einer app.
  
    
    
Sobald das **DuetReportingForApps** -Feature aktiviert ist, es bringt die Artefakte (Berichtsliste, Lib, Formulare usw.) und Anpassung auf der Website apps jedoch wie die app-Websitevorlage standard Navigationslinks nicht vorhanden ist, muss der app-Entwickler benutzerdefinierte Seitenelemente, aufzurufen, die Duet-Features (z. B. Berichtseinstellungen, Bibliothek Listenansicht und Formulare) hinzufügen. Der Entwickler sollte in der standard Duet-Dokumentation für Berichtsfeature erfahren Sie mehr über das Feature und seine Elemente der Benutzeroberfläche. Entwickler kann auswählen, um eine benutzerdefinierte Benutzeroberfläche für Einstiegspunkte Feature erstellen, wodurch die besser mit dem allgemeinen Design der app entspricht kann.
  
    
    

## <a name="viewing-the-results"></a>Anzeigen der Ergebnisse
<a name="bkmk_ViewingTheResults"> </a>

Um die Einstellungen die Standardseite-Bericht angezeigt wird, navigieren Sie zu: **~/Lists/ReportSetting/AllReportTemplate.aspx**.
  
    
    
Um die Standardansicht für die Dokumentbibliothek Bericht angezeigt wird, navigieren Sie zu: **~/ReportsLib/Forms/AllItems.aspx**.
  
    
    

## <a name="customizing-the-reports"></a>Anpassen der Berichte
<a name="bkmk_CustomizingTheReports"> </a>

Innerhalb einer app ein Entwickler auch erstellen Sie eigene benutzerdefinierte Benutzeroberfläche (mit HTML/JavaScript/Jquery usw.) und der BCS-CSOM verwenden, um ein besseres Benutzererlebnis zu erstellen. Eine ähnliche-app, in dem benutzerdefinierte HTML Benutzeroberfläche basierend, baut auf folgenden Screenshots zeigt mit Hilfe von OOB Artefakte und clientseitigen BCS-APIs.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Bei der Entwicklung mit Duet Enterprise 2.0](developing-with-duet-enterprise-2-0.md)
    
  
-  [Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  

