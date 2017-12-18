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
# <a name="use-sap-reporting-with-duet-enterprise-20"></a><span data-ttu-id="c6459-102">Verwenden von SAP-Berichterstellung mit Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="c6459-102">How to: Use SAP Reporting with Duet Enterprise 2.0</span></span>

## <a name="introduction"></a><span data-ttu-id="c6459-103">Einführung</span><span class="sxs-lookup"><span data-stu-id="c6459-103">Introduction</span></span>
<span data-ttu-id="c6459-104"><a name="bkmk_Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="c6459-104"><a name="bkmk_Introduction"> </a></span></span>

<span data-ttu-id="c6459-105">Duet Enterprise 2.0 ermöglicht die Duet-Berichtsfeatures innerhalb Ihrer SharePoint-Add-In integrieren, indem Sie wie folgt ein wenig Anpassung.</span><span class="sxs-lookup"><span data-stu-id="c6459-105">Duet Enterprise 2.0 gives you the ability to integrate the Duet reporting features within your SharePoint Add-in by doing a little customization.</span></span>
  
    
    
<span data-ttu-id="c6459-p101">Das Kennwort für die Aktivierung der berichterstellung für Ihre app ist mithilfe von einem ausgeblendeten Feature von Duet installiert. Sie müssen dieses Feature benutzerdefinierte Features Heften, damit die Instanziierung die app wird der SAP-Berichterstellungsfeatures die app zur Verfügung gestellt werden werden.</span><span class="sxs-lookup"><span data-stu-id="c6459-p101">The secret to enabling reporting for your app is by using a hidden feature installed by Duet. You will need to staple this feature to custom features, so that when the app is instantiated, the SAP reporting features will be made available to the app.</span></span>
  
    
    

## <a name="enabling-the-features"></a><span data-ttu-id="c6459-108">Aktivieren Sie die Funktionen</span><span class="sxs-lookup"><span data-stu-id="c6459-108">Enabling the features</span></span>
<span data-ttu-id="c6459-109"><a name="bkmk_EnablingTheFeatures"> </a></span><span class="sxs-lookup"><span data-stu-id="c6459-109"><a name="bkmk_EnablingTheFeatures"> </a></span></span>

<span data-ttu-id="c6459-110">Um die reporting Duet-Funktionen zu aktivieren, muss die Abfolge der Aktivierung sorgfältig folgen.</span><span class="sxs-lookup"><span data-stu-id="c6459-110">To enable the Duet reporting features, the sequence of activation must be carefully followed.</span></span>
  
    
    

### <a name="to-create-a-feature-to-add-the-app-scoped-external-content-type"></a><span data-ttu-id="c6459-111">So erstellen Sie eine Funktion, um den app-bezogenen externen Inhaltstyp hinzuzufügen:</span><span class="sxs-lookup"><span data-stu-id="c6459-111">To create a feature to add the app-scoped external content type:</span></span>


1. <span data-ttu-id="c6459-p102">Innerhalb Ihrer app, die Sie im **Projektmappen-Explorer** reporting Duet klicken Sie mit der rechten Maustaste auf den Projektnamen. Wählen Sie **Hinzufügen**, **Inhaltstypen für eine externe Datenquelle**. Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="c6459-p102">Inside your Duet reporting app, in the **Solution Explorer**, right click the project name. Choose **Add**, **Content Types for an External Data Source**. Click **Next**.</span></span>
    
  
2. <span data-ttu-id="c6459-115">Geben Sie die URL für den Endpunkt SAP Reporting als OData-Quelle.</span><span class="sxs-lookup"><span data-stu-id="c6459-115">Enter the URL for the SAP Reporting endpoint as the OData Source.</span></span>
    
  
3. <span data-ttu-id="c6459-116">Wählen Sie die Entitäten, und wählen Sie **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="c6459-116">Select the Entities, and choose **Finish**.</span></span>
    
  
4. <span data-ttu-id="c6459-p103">Öffnen Sie den neu erstellten externen Inhaltstyp, um die LSI-Eigenschaften anzuzeigen. Sie sehen, dass sie die gleichen wie für die Farm-bezogenen externen Inhaltstyp mit Ausnahme der **ODataconnectionSettingsId**sind.</span><span class="sxs-lookup"><span data-stu-id="c6459-p103">Open the newly created external content type to view the LSI properties. You will notice that they are the same as for the farm-scoped external content type except for the **ODataconnectionSettingsId**.</span></span>
    
  

### <a name="to-create-a-feature-to-enable-the-hidden-duet-features"></a><span data-ttu-id="c6459-119">So erstellen Sie ein Feature, das die ausgeblendeten Duet-Funktionen zu aktivieren:</span><span class="sxs-lookup"><span data-stu-id="c6459-119">To create a feature to enable the hidden Duet features:</span></span>


1. <span data-ttu-id="c6459-p104">Fügen Sie dem Projekt ein weiteres neues Feature hinzu. Name des Titels **AddDuetReporting**.</span><span class="sxs-lookup"><span data-stu-id="c6459-p104">Add another new feature to your project. Name the title **AddDuetReporting**.</span></span>
    
    <span data-ttu-id="c6459-122">Dieses Feature wird eine Abhängigkeit von der **AddReportingModel** und die **DuetReportingForApps** Features haben.</span><span class="sxs-lookup"><span data-stu-id="c6459-122">This feature will have a dependency on the **AddReportingModel** and the **DuetReportingForApps** features.</span></span>
    
  
2. <span data-ttu-id="c6459-123">Fügen Sie den folgenden Code in die Datei **Elemente**.</span><span class="sxs-lookup"><span data-stu-id="c6459-123">Add the following code to the **Elements** file.</span></span>
    
```
  
<?xml version="1.0" encoding="utf-8"?>
<Feature xmlns="http://schemas.microsoft.com/sharepoint/" Title="AddDuetReporting" Id="6a55705c-af12-455a-914b-8cf3a31c820e" Scope="Web">
  <ActivationDependencies>
    <ActivationDependency FeatureId="e1fe41d3-7fc3-458f-9a66-6ecf6a39bb2c" FeatureTitle="AddReportingModel" />
    <ActivationDependency FeatureId="9b60ccba-ebfd-4e38-87c8-3dea9cc2680a" FeatureTitle="SAPReportingForApps" />
  </ActivationDependencies>
</Feature>

```

<span data-ttu-id="c6459-p105">Beachten Sie, dass die Reihenfolge in aktivierungsabhängigkeit wichtig ist. Zunächst müssen Sie den externen Inhaltstyp erstellen und aktivieren Sie das Feature **SAPReportingForApps**. Beachten Sie außerdem, dass das zweite Feature (ID: **9b60ccba-ebfd-4e38-87c8-3dea9cc2680a**) ist im Lieferumfang von Duet Enterprise 2.0, ist aber markiert als ausgeblendet. Bei diesem Ansatz kann Entwickler stellen dieses Feature und können auch die in Duet Reporting-Funktionen zu einer app.</span><span class="sxs-lookup"><span data-stu-id="c6459-p105">Please note that the sequence in activation dependency is important. First, you must create the external content type and then activate the **SAPReportingForApps** feature. Also, note that the second feature (ID: **9b60ccba-ebfd-4e38-87c8-3dea9cc2680a**) is shipped with Duet Enterprise 2.0, but it is marked as hidden. With this approach, a developer can make use of this feature and can bring in Duet Reporting capabilities to an app.</span></span>
  
    
    
<span data-ttu-id="c6459-p106">Sobald das **DuetReportingForApps** -Feature aktiviert ist, es bringt die Artefakte (Berichtsliste, Lib, Formulare usw.) und Anpassung auf der Website apps jedoch wie die app-Websitevorlage standard Navigationslinks nicht vorhanden ist, muss der app-Entwickler benutzerdefinierte Seitenelemente, aufzurufen, die Duet-Features (z. B. Berichtseinstellungen, Bibliothek Listenansicht und Formulare) hinzufügen. Der Entwickler sollte in der standard Duet-Dokumentation für Berichtsfeature erfahren Sie mehr über das Feature und seine Elemente der Benutzeroberfläche. Entwickler kann auswählen, um eine benutzerdefinierte Benutzeroberfläche für Einstiegspunkte Feature erstellen, wodurch die besser mit dem allgemeinen Design der app entspricht kann.</span><span class="sxs-lookup"><span data-stu-id="c6459-p106">Once the **DuetReportingForApps** feature is activated, it will bring all the artifacts (Report List, Lib, forms, etc.) and customization on the apps site but as the app site template does not have standard navigation links, the app developer needs to add custom page elements to bring out the Duet features (e.g. Report Settings, library list view, and forms). The developer should consult standard Duet documentation for Reporting feature to learn more about the feature and its UI elements. A developer may choose to build up a custom UI for feature entry points which may suit better with the general theme of the app.</span></span>
  
    
    

## <a name="viewing-the-results"></a><span data-ttu-id="c6459-131">Anzeigen der Ergebnisse</span><span class="sxs-lookup"><span data-stu-id="c6459-131">Viewing the results</span></span>
<span data-ttu-id="c6459-132"><a name="bkmk_ViewingTheResults"> </a></span><span class="sxs-lookup"><span data-stu-id="c6459-132"><a name="bkmk_ViewingTheResults"> </a></span></span>

<span data-ttu-id="c6459-133">Um die Einstellungen die Standardseite-Bericht angezeigt wird, navigieren Sie zu: **~/Lists/ReportSetting/AllReportTemplate.aspx**.</span><span class="sxs-lookup"><span data-stu-id="c6459-133">To see the default report settings page, navigate to: **~/Lists/ReportSetting/AllReportTemplate.aspx**.</span></span>
  
    
    
<span data-ttu-id="c6459-134">Um die Standardansicht für die Dokumentbibliothek Bericht angezeigt wird, navigieren Sie zu: **~/ReportsLib/Forms/AllItems.aspx**.</span><span class="sxs-lookup"><span data-stu-id="c6459-134">To see the default view for the report document library, navigate to: **~/ReportsLib/Forms/AllItems.aspx**.</span></span>
  
    
    

## <a name="customizing-the-reports"></a><span data-ttu-id="c6459-135">Anpassen der Berichte</span><span class="sxs-lookup"><span data-stu-id="c6459-135">Customizing the reports</span></span>
<span data-ttu-id="c6459-136"><a name="bkmk_CustomizingTheReports"> </a></span><span class="sxs-lookup"><span data-stu-id="c6459-136"><a name="bkmk_CustomizingTheReports"> </a></span></span>

<span data-ttu-id="c6459-p107">Innerhalb einer app ein Entwickler auch erstellen Sie eigene benutzerdefinierte Benutzeroberfläche (mit HTML/JavaScript/Jquery usw.) und der BCS-CSOM verwenden, um ein besseres Benutzererlebnis zu erstellen. Eine ähnliche-app, in dem benutzerdefinierte HTML Benutzeroberfläche basierend, baut auf folgenden Screenshots zeigt mit Hilfe von OOB Artefakte und clientseitigen BCS-APIs.</span><span class="sxs-lookup"><span data-stu-id="c6459-p107">Inside an app, a developer can also create his own custom UI (using HTML/JavaScript/Jquery etc.) and make use of BCS CSOM to build a richer user experience. Following screenshots shows a similar app where custom HTML based UI is built with the help of OOB artifacts and client side BCS APIs.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="c6459-139">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c6459-139">Additional resources</span></span>
<span data-ttu-id="c6459-140"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c6459-140"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="c6459-141">Bei der Entwicklung mit Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="c6459-141">Developing with Duet Enterprise 2.0</span></span>](developing-with-duet-enterprise-2-0.md)
    
  
-  [<span data-ttu-id="c6459-142">Gewusst wie: Erstellen eines externen Inhaltstyps aus einer OData-Quelle in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c6459-142">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c6459-143">Verwenden von OData-Quellen mit Business Connectivity Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c6459-143">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  

