---
title: "Vorgehensweise erstellen Bericht-Editoren für PerformancePoint Services in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: f9675950d272a1bd90efa4eb26a6772f13dd24bc
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-report-editors-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="3ab3c-102">Vorgehensweise: erstellen Bericht-Editoren für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ab3c-102">How to: Create report editors for PerformancePoint Services in SharePoint</span></span>
<span data-ttu-id="3ab3c-103">In diesem Artikel erfahren Sie, wie die Editor-Komponente einer benutzerdefinierten Berichtserweiterung für PerformancePoint-Dienste erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-103">Learn how to create the editor component of a custom report extension for PerformancePoint Services.</span></span>
## <a name="what-are-custom-report-editors-for-performancepoint-services"></a><span data-ttu-id="3ab3c-104">Was sind benutzerdefinierte Bericht-Editoren für PerformancePoint-Dienste ?</span><span class="sxs-lookup"><span data-stu-id="3ab3c-104">What are custom report editors for PerformancePoint Services?</span></span>
<span data-ttu-id="3ab3c-105"><a name="bi_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="3ab3c-105"></span></span>

<span data-ttu-id="3ab3c-p101">Benutzerdefinierter Bericht-Editoren aktivieren PerformancePoint-Dienste Benutzer Eigenschaften für benutzerdefinierte Berichte fest. Bericht-Editoren initialisieren auch den berichtendpunkt, der Parameterwerte von Scorecard- und filteranbietern empfängt. Weitere Informationen zu Editor Anforderungen und Funktionen finden Sie unter  [Editoren für benutzerdefinierte PerformancePoint Services-Objekte](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p101">In PerformancePoint Services, custom report editors enable users to set properties on custom reports. Report editors also initialize the report endpoint, which receives parameter values from scorecard and filter providers. For more information about editor requirements and functionality, see  [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="3ab3c-109">Die folgenden Verfahren und Beispiele basieren auf der **SampleReportViewEditor**-Klasse aus dem [Beispiel für benutzerdefinierte Objekte](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ab3c-109">The following procedures and examples are based on the **SampleReportViewEditor** class from the [custom objects sample](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span></span> <span data-ttu-id="3ab3c-110">Der Editor ist eine schlanke Webanwendung, die es Benutzern ermöglicht, den Namen und die Beschreibung des Berichts zu ändern.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-110">The editor is a thin web application that enables users to modify the report's name and description.</span></span> <span data-ttu-id="3ab3c-111">Den vollständigen Code für die Klasse finden Sie unter [Codebeispiel: Erstellen, Abrufen und Aktualisieren von benutzerdefinierten PerformancePoint-Dienste-Berichten in SharePoint](#bk_example)</span><span class="sxs-lookup"><span data-stu-id="3ab3c-111">For the complete code for the class, see  [Code example: Create, retrieve, and update custom PerformancePoint Services reports in SharePoint](#bk_example).</span></span>
  
    
    
<span data-ttu-id="3ab3c-p103">Es wird empfohlen, dass Sie den Beispiel-Editor als Vorlage verwenden. Das Beispiel zeigt wie Objekte aufrufen PerformancePoint-Dienste-API bietet Hilfsobjekte, die vereinfachen von Anrufen für Repository-Vorgänge (wie erstellen und Aktualisieren der Objekte), und bewährte Methoden für die Entwicklung von PerformancePoint-Dienste veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p103">We recommend that you use the sample editor as a template. The sample shows how to call objects in the PerformancePoint Services API, provides helper objects that simplify calls for repository operations (such as creating and updating objects), and demonstrates best practices for PerformancePoint Services development.</span></span>
  
    
    

## <a name="create-editors-for-custom-performancepoint-services-reports"></a><span data-ttu-id="3ab3c-114">Erstellen von Editoren für benutzerdefinierte PerformancePoint-Dienste Berichte</span><span class="sxs-lookup"><span data-stu-id="3ab3c-114">Create editors for custom PerformancePoint Services reports</span></span>
<span data-ttu-id="3ab3c-115"><a name="BKMK_ConfigREditor"> </a></span><span class="sxs-lookup"><span data-stu-id="3ab3c-115"></span></span>


  
    
    

1. <span data-ttu-id="3ab3c-p104">Installieren Sie PerformancePoint-Dienste, oder kopieren Sie die DLLs, die die Erweiterung verwendet (siehe Schritt 3) auf Ihrem Computer. Weitere Informationen finden Sie unter  [PerformancePoint-Dienste-DLLs in Entwicklungsszenarios](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p104">Install PerformancePoint Services, or copy the DLLs that your extension uses (listed in step 3) to your computer. For more information, see  [DLLs with Class Libraries](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span></span>
    
  
2. <span data-ttu-id="3ab3c-p105">Erstellen Sie in Visual Studio eine C#-Klassenbibliothek. Sollten Sie bereits eine Klassenbibliothek für die Erweiterung erstellt haben, fügen Sie eine neue C#-Klasse hinzu.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p105">In Visual Studio, create a C# class library. If you have already created a class library for your extension, add a new C# class.</span></span>
    
    <span data-ttu-id="3ab3c-p106">Sie müssen die DLL mit einem starken Namen signieren. Stellen Sie außerdem sicher, dass alle Assemblys, auf die von der DLL verwiesen wird, ebenfalls starke Namen haben. Informationen dazu, wie Sie eine Assembly mit einem starken Namen signieren und ein öffentliches/privates Schlüsselpaar erstellen, finden Sie unter  [How to: Create a public/private key pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p106">You must sign your DLL with a strong name. In addition, ensure that all assemblies referenced by your DLL have strong names. For information about how to sign an assembly with a strong name and how to create a public/private key pair, see  [How to: Create a public/private key pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span></span>
    
  
3. <span data-ttu-id="3ab3c-123">Fügen Sie dem Projekt die folgenden DLLs als Assemblyverweise hinzu:</span><span class="sxs-lookup"><span data-stu-id="3ab3c-123">Add the following DLLs as assembly references to the project:</span></span>
    
  - <span data-ttu-id="3ab3c-124">Microsoft.PerformancePoint.Scorecards.Client.dll</span><span class="sxs-lookup"><span data-stu-id="3ab3c-124">Microsoft.PerformancePoint.Scorecards.Client.dll</span></span>
    
  
  - <span data-ttu-id="3ab3c-125">Microsoft.PerformancePoint.Scorecards.ServerCommon.dll</span><span class="sxs-lookup"><span data-stu-id="3ab3c-125">Microsoft.PerformancePoint.Scorecards.ServerCommon.dll</span></span>
    
  
  - <span data-ttu-id="3ab3c-126">Microsoft.PerformancePoint.Scorecards.Store.dll (von Hilfsklassen verwendet)</span><span class="sxs-lookup"><span data-stu-id="3ab3c-126">Microsoft.PerformancePoint.Scorecards.Store.dll (used by helper classes)</span></span>
    
  
  - <span data-ttu-id="3ab3c-127">Microsoft.SharePoint.dll (von Hilfsklassen verwendet)</span><span class="sxs-lookup"><span data-stu-id="3ab3c-127">Microsoft.SharePoint.dll (used by helper classes)</span></span>
    
  

    <span data-ttu-id="3ab3c-p107">Der Beispiel-Editor enthält auch Assemblyverweise auf System.Web.dll und System.Web.Services.dll. Je nach der Funktionalität Ihrer Erweiterung werden möglicherweise andere Projektverweise benötigt.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p107">The sample editor also contains assembly references to System.Web.dll and System.Web.Services.dll. Depending on your extension's functionality, other project references may be required.</span></span>
    
  
4. <span data-ttu-id="3ab3c-p108">Fügen Sie dem Projekt die folgenden Klassen aus dem Beispiel. Im Editor wird für die Interaktion mit dem Repository PerformancePoint-Dienste Hilfsklassen verwendet:</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p108">Add the following classes from the sample to the project. The editor uses these helper classes to interact with the PerformancePoint Services repository:</span></span>
    
  - <span data-ttu-id="3ab3c-132">DataSourceConsumerHelper.cs</span><span class="sxs-lookup"><span data-stu-id="3ab3c-132">DataSourceConsumerHelper.cs</span></span>
    
  
  - <span data-ttu-id="3ab3c-133">ExtensionRepositoryHelper.cs</span><span class="sxs-lookup"><span data-stu-id="3ab3c-133">ExtensionRepositoryHelper.cs</span></span>
    
  
  - <span data-ttu-id="3ab3c-134">ReportViewRepositoryHelper.cs</span><span class="sxs-lookup"><span data-stu-id="3ab3c-134">ReportViewRepositoryHelper.cs</span></span>
    
  
  - <span data-ttu-id="3ab3c-135">IDataSourceConsumer.cs</span><span class="sxs-lookup"><span data-stu-id="3ab3c-135">IDataSourceConsumer.cs</span></span>
    
  

    > <span data-ttu-id="3ab3c-136">**Hinweis:** Der Beispielbericht erhält Daten aus einem Filter, daher werden keine **DataSourceConsumerHelper**- oder **IDataSourceConsumer**-Objekte verwendet.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-136">**Note:** The sample report obtains data from a filter, so it does not use **DataSourceConsumerHelper** or **IDataSourceConsumer** objects.</span></span> <span data-ttu-id="3ab3c-137">Aber wenn Ihr Bericht Daten aus einer PerformancePoint-Dienste-Datenquelle erhält, können Sie die von der **DataSourceConsumerHelper**-Klasse verfügbar gemachten Methoden verwenden, um Datenquellen abzurufen, wie in [Vorgehensweise: Erstellen von Filter-Editoren für PerformancePoint-Dienste in SharePoint](https://officedevcentersite-release.azurewebsites.net/sharepoint/docs/general-development/how-to-create-report-editors-for-performancepoint-services-in-sharepoint) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-137">Note The sample report obtains data from a filter, so it does not use DataSourceConsumerHelper or IDataSourceConsumer objects. However, if your report obtains data from a PerformancePoint Services data source, you can use the methods that are exposed by the **DataSourceConsumerHelper** class to retrieve data sources as described in [How to: Create filter editors for PerformancePoint Services in SharePoint](https://officedevcentersite-release.azurewebsites.net/sharepoint/docs/general-development/how-to-create-report-editors-for-performancepoint-services-in-sharepoint).</span></span> 
5. <span data-ttu-id="3ab3c-138">Fügen Sie in Ihrer Editor-Klasse **using**-Direktiven für die folgenden PerformancePoint-Dienste-Namespaces hinzu:</span><span class="sxs-lookup"><span data-stu-id="3ab3c-138">In your editor class, add **using** directives for the following PerformancePoint Services namespaces:</span></span>
    
  - <span data-ttu-id="3ab3c-139">**Microsoft.PerformancePoint.Scorecards**</span><span class="sxs-lookup"><span data-stu-id="3ab3c-139">**Microsoft.PerformancePoint.Scorecards**</span></span>
    
  
  - <span data-ttu-id="3ab3c-140">**Microsoft.PerformancePoint.Scorecards.ServerCommon**</span><span class="sxs-lookup"><span data-stu-id="3ab3c-140">**Microsoft.PerformancePoint.Scorecards.ServerCommon**</span></span>
    
  

    <span data-ttu-id="3ab3c-141">Je nach Funktionalität der Erweiterung sind u. U. andere **using**-Direktiven erforderlich.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-141">Depending on your extension's functionality, other **using** directives may be required.</span></span>
    
  
6. <span data-ttu-id="3ab3c-p110">Übernehmen Sie von der Basisklasse, die die Implementierung Ihres Editors unterstützt. Da es sich bei dem Beispielbericht-Editor um eine Webanwendung handelt, erbt diese von der  [Page](https://msdn.microsoft.com/library/System.Web.UI.Page.aspx) -Klasse. Andere Implementierungen können von Basisklassen wie der [UserControl](https://msdn.microsoft.com/library/System.Windows.Forms.UserControl.aspx) -Klasse oder der [WebPart](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebParts.WebPart.aspx) -Klasse erben.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p110">Inherit from the base class that supports your editor implementation. Because the sample report editor is a web application, it inherits from the  [Page](https://msdn.microsoft.com/library/System.Web.UI.Page.aspx) class. Other implementations can derive from base classes such as the [UserControl](https://msdn.microsoft.com/library/System.Windows.Forms.UserControl.aspx) or [WebPart](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebParts.WebPart.aspx) class.</span></span>
    
  
7. <span data-ttu-id="3ab3c-p111">Deklarieren Sie Variablen für die Steuerelemente, die die Eigenschaften offenlegen, die Benutzer anzeigen oder ändern sollen. Vom Beispielbericht-Editor werden zunächst Variablen für die Webserversteuerelemente deklariert, die in der Benutzeroberflächenkomponente - einer ASPX-Seite - definiert sind. Vom Beispiel-Editor wird auch ein Schaltflächen-Steuerelement definiert, das es Benutzern ermöglicht, Änderungen zu übermitteln. Der Editor ruft dann die  [CreateChildControls()](https://msdn.microsoft.com/library/System.Web.UI.Control.CreateChildControls.aspx) -Methode auf, um die Steuerelemente auf der Seite zur Verfügung zu stellen.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p111">Declare variables for the controls that expose the properties that you want users to view or modify. The sample report editor first declares variables for the web server controls that are defined in the user interface component, which is an ASPX page. The sample editor also defines a button control that enables users to submit changes. Then, the editor calls the  [CreateChildControls()](https://msdn.microsoft.com/library/System.Web.UI.Control.CreateChildControls.aspx) method to make the controls available on the page.</span></span>
    
    > <span data-ttu-id="3ab3c-149">**Hinweis:** Im Editor wird die Programmierlogik separat von der Benutzeroberfläche definiert.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-149">**Note:** The editor defines programming logic separately from the user interface.</span></span> <span data-ttu-id="3ab3c-150">Anweisungen zum Erstellen der Benutzeroberflächenkomponente würden den Rahmen dieser Dokumentation sprengen.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-150">The editor defines programming logic separately from the user interface. Instructions for creating the user interface component of the editor are beyond the scope of this documentation.</span></span> 

    <span data-ttu-id="3ab3c-p113">Beispiel-Bericht-Editors führt die Schritte 8 bis 12 in der **Page_Load** -Methode. **Page_Load** wird auch initialisieren und Variablen und Steuerelemente zu überprüfen, füllen Sie Steuerelemente und Statusinformationen für den benutzerdefinierten Bericht und Helper-Objekten zu speichern.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p113">The sample report editor performs steps 8 through 12 in the **Page_Load** method. **Page_Load** is also used to initialize and validate variables and controls, populate controls, and save state information for the custom report and helper objects.</span></span>
    
  
8. <span data-ttu-id="3ab3c-p114">Legen Sie die  [AllowUnsafeUpdates](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ServerCommon.ServerUtils.AllowUnsafeUpdates.aspx) -Eigenschaft auf **true**. Auf diese Weise können die Bericht-Editors zum Schreiben von Daten an das Repository ohne Verwendung des Formulars **POST** Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p114">Set the  [AllowUnsafeUpdates](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ServerCommon.ServerUtils.AllowUnsafeUpdates.aspx) property to **true**. This enables the report editor to write data to the repository without using form **POST** operations.</span></span>
    
  
9. <span data-ttu-id="3ab3c-155">Rufen Sie die Parameter aus der Abfragezeichenfolge ab, und legen Sie diese als Werte für lokale Variablen fest, wie im folgenden Codebeispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-155">Retrieve the parameters from the query string and set them as values for local variables, as shown in the following code example.</span></span>
    
```cs
  
// The URL of the site collection that contains the PerformancePoint Services repository.
string server = Request.QueryString[ClickOnceLaunchKeys.SiteCollectionUrl];

// The location of the report in the repository.
string itemLocation = Request.QueryString[ClickOnceLaunchKeys.ItemLocation];

// The operation to perform: OpenItem or CreateItem.
string action = Request.QueryString[ClickOnceLaunchKeys.LaunchOperation];
```


    For information about the query string parameters, see  [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).
    
  
10. <span data-ttu-id="3ab3c-156">Rufen Sie das **ReportViewRepositoryHelper**-Objekt ab, das für Aufrufe des Repositorys verwendet wird, wie im folgenden Codebeispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-156">Retrieve the **ReportViewRepositoryHelper** object, which is used to make calls to the repository, as shown in the following code example.</span></span>
    
```cs
  
reportviewRepositoryHelper = new ReportViewRepositoryHelper();
```

11. <span data-ttu-id="3ab3c-157">Legen Sie den Speicherort für den Bericht basierend auf dem Abfragezeichenfolgenparameter fest, wie im folgenden Codebeispiel veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-157">Set the report location based on the query string parameter, as shown in the following code example.</span></span>
    
```cs
  RepositoryLocation repositoryReportViewLocation = RepositoryLocation.CreateFromUriString(itemLocation);
```

12. <span data-ttu-id="3ab3c-158">Vorgang ( _OpenItem_ oder _CreateItem_) aus der Abfragezeichenfolge abzurufen und abzurufen oder einen benutzerdefinierten Bericht erstellen.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-158">Retrieve the operation to perform ( _OpenItem_ or _CreateItem_) from the query string, and then retrieve or create the custom report.</span></span>
    
  - <span data-ttu-id="3ab3c-159">Zum Abrufen des benutzerdefinierten Berichts verwenden Sie die **ReportViewRepositoryHelper.Get**-Methode.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-159">To retrieve the custom report, use the **ReportViewRepositoryHelper.Get** method.</span></span>
    
  
  - <span data-ttu-id="3ab3c-160">Zum Erstellen des benutzerdefinierten Berichts verwenden Sie den **ReportView()**-Konstruktor, und definieren Sie dann die Eigenschaften  [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.RendererClassName.aspx) und [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.SubTypeId.aspx) des Berichts.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-160">To create the custom report, use the **ReportView()** constructor and then define the report's [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.RendererClassName.aspx) , and [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.SubTypeId.aspx) properties.</span></span>
    
     <span data-ttu-id="3ab3c-p115">[SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.SubTypeId.aspx) ist der eindeutige Bezeichner für den Bericht, und es muss übereinstimmen, das **subType** -Attribut, das Sie für den benutzerdefinierten Bericht in der PerformancePoint-Dienste web.config-Datei angeben. [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.RendererClassName.aspx) ist den vollqualifizierten Namen der Klasse, die das Webserversteuerelement Renderer definiert. Wenn im Editor nicht definiert ist, ist die Standardeinstellung der Rendererklasse in der Datei web.config angegeben.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p115">[SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.SubTypeId.aspx) is the unique identifier for the report, and it must match the **subType** attribute that you specify for your custom report in the PerformancePoint Services web.config file. [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.RendererClassName.aspx) is the fully qualified name of the class that defines the renderer web server control. If not defined in the editor, this value defaults to the renderer class specified in the web.config file.</span></span>
    
  

```cs
  if (ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase))
    {

        // Use the repository-helper object to retrieve the report.
        reportview = reportviewRepositoryHelper.Get(repositoryReportViewLocation);
        if (reportview == null)
        {
            displayError("Could not retrieve the report view for editing.");
            return;
        }
    }
    else if (ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase))
    {
        reportview = new ReportView
        {
            RendererClassName = typeof(SampleReportRenderer).AssemblyQualifiedName, 
            SubTypeId = "SampleReportView"
        };
    }
    else
    {
        displayError("Invalid Action.");
        return;
    }
```


    > **Note:**
      > By default, users can create custom objects from PerformancePoint Dashboard Designer only. To enable users to create a custom object outside of Dashboard Designer, you must add a menu item that sends a  _CreateItem_ request to your editor from the content type in the repository. For more information, see [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx). 
13. <span data-ttu-id="3ab3c-p116">Definieren Sie den Endpunkt des Berichts, damit der Bericht Daten von Filtern und Scorecards empfangen kann. Die erforderlichen Eigenschaften für den Endpunkt werden vom Beispielbericht-Editor definiert, wie im folgenden Codebeispiel veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p116">Define the report's endpoint, which enables the report to receive data from filters and scorecards. The sample report editor defines the required properties for the endpoint, as shown in the following code example.</span></span>
    
```cs
  
if (0 == reportview.EndPoints.Count)
{
    EndPoint endpoint = new EndPoint
    {
        Category = EndPointCategory.None,
        UniqueName = "SampleReportView_EndPoint",

        // The display name is shown to users in Dashboard Designer.
        // It represents the endpoint that can be connected 
        // to a filter or scorecard.
        DisplayName = "Sample Report View EndPoint"
    };

    reportview.EndPoints.Add(endpoint);
}
```


    The sample editor defines the endpoint in the **VerifyReportView** method. It also uses **VerifyReportView** to verify that required properties are set and to define the optional [CustomData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.CustomData.aspx) property, which you can use to store information for your report.
    
  
14. <span data-ttu-id="3ab3c-p117">Aktualisieren Sie den Bericht durch benutzerdefinierte Änderungen. Die **ReportViewRepositoryHelper.Update**-Methode wird von der **buttonOK_Click**-Methode im Beispielbericht-Editor aufgerufen, um die Eigenschaften  [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) und [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) des Berichts im Repository zu aktualisieren. **buttonOK_Click** wird ebenfalls zum Überprüfen der Inhalte der Steuerelemente und zum Abrufen von Statusinformationen für den benutzerdefinierten Bericht und das Hilfsobjekt verwendet.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p117">Update the report with user-defined changes. The **buttonOK_Click** method in the sample report editor calls the **ReportViewRepositoryHelper.Update** method to update the report's [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) and [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) properties in the repository. **buttonOK_Click** is also used to validate the contents of the controls and retrieve state information for the custom report and the helper object.</span></span>
    
    > <span data-ttu-id="3ab3c-169">**Hinweis;** Benutzer können die  [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx)-, [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx)- und [Owner](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Owner.aspx)- (**Person Responsible**)-Eigenschaften eines benutzerdefinierten Objekts bearbeiten und benutzerdefinierte Objekte direkt im Dashboard-Designer und im PerformancePoint-Dienste-Repository löschen.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-169">**Note** Users can edit a custom object's  [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) , and [Owner](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Owner.aspx) ( **Person Responsible**) properties and delete custom objects directly from Dashboard Designer and the PerformancePoint Services repository.</span></span> 

## <a name="code-example-create-retrieve-and-update-custom-performancepoint-services-reports-in-sharepoint"></a><span data-ttu-id="3ab3c-170">Codebeispiel: Erstellen, Abrufen und Aktualisieren von benutzerdefinierten PerformancePoint-Dienste-Berichten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ab3c-170">Code example: Create, retrieve, and update custom PerformancePoint Services reports in SharePoint Server 2013</span></span>
<span data-ttu-id="3ab3c-171"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="3ab3c-171"></span></span>

<span data-ttu-id="3ab3c-p118">Im folgenden Codebeispiel wird erstellt, abgerufen und aktualisiert die benutzerdefinierte Berichte. Dieser Code hat ihren Ursprung im Editor CodeBehind-Klasse, die die Programmierlogik für Steuerelemente bereitstellt, die in einer ASPX-Seite definiert sind.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-p118">The following code example creates, retrieves, and updates custom reports. This code is from the editor's code-behind class, which provides the programming logic for controls that are defined in an ASPX page.</span></span>
  
    
    
<span data-ttu-id="3ab3c-174">Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie Ihre Entwicklungsumgebung konfigurieren, wie beschrieben in  [Erstellen von Editoren für benutzerdefinierte PerformancePoint-Dienste Berichte](#BKMK_ConfigREditor).</span><span class="sxs-lookup"><span data-stu-id="3ab3c-174">Before you can compile this code example, you must configure your development environment as described in  [Create editors for custom PerformancePoint Services reports](#BKMK_ConfigREditor).</span></span>
  
    
    



```cs

using System;
using System.Web.UI;
using System.Web.UI.WebControls;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.ServerCommon;

namespace Microsoft.PerformancePoint.SDK.Samples.SampleReport
{

    // Represents the class that defines the sample report editor. 
    public class SampleReportViewEditor : Page
    {

        // Declare private variables for the ASP.NET controls defined in the user interface.
        // The sample's user interface is an ASPX page that defines the controls in HTML.
        private TextBox textboxName;
        private TextBox textboxDescription;
        private Label labelErrorMessage;
        private Button buttonOK;

        // Make the controls available to this class.
        protected override void CreateChildControls()
        {
            base.CreateChildControls();

            if (null == textboxName)
                textboxName = FindControl("textboxName") as TextBox;
            if (null == textboxDescription)
                textboxDescription = FindControl("textboxDescription") as TextBox;
            if (null == labelErrorMessage)
                labelErrorMessage = FindControl("labelErrorMessage") as Label;
            if (null == buttonOK)
                buttonOK = FindControl("buttonOK") as Button;
        }

        // Handles the Load event of the Page control.
        // Methods that use a control variable should call the Control.EnsureChildControls
        // method before accessing the variable for the first time.
        protected void Page_Load(object sender, EventArgs e)
        {

            // Required to enable custom report and filter editors to
            // write data to the repository.
            ServerUtils.AllowUnsafeUpdates = true;

            // Initialize controls the first time the page loads only.
            if (!IsPostBack)
            {
                EnsureChildControls();
                ReportViewRepositoryHelper reportviewRepositoryHelper = null;
                try
                {

                    // Get information from the query string parameters.
                    string server = Request.QueryString[ClickOnceLaunchKeys.SiteCollectionUrl];
                    string itemLocation = Request.QueryString[ClickOnceLaunchKeys.ItemLocation];
                    string action = Request.QueryString[ClickOnceLaunchKeys.LaunchOperation];

                    // Validate the query string parameters.
                    if (string.IsNullOrEmpty(server) ||
                        string.IsNullOrEmpty(itemLocation) ||
                        string.IsNullOrEmpty(action))
                    {
                        displayError("Invalid URL.");
                        return;
                    }

                    // Retrieve the repository-helper object.
                    reportviewRepositoryHelper =
                        new ReportViewRepositoryHelper();

                    // Set the report location by using the location from the query string.
                    RepositoryLocation repositoryReportViewLocation = RepositoryLocation.CreateFromUriString(itemLocation);

                    ReportView reportview;

                    // Retrieve or create the report object, depending on the operation
                    // passed in the query string (OpenItem or CreateItem).
                    if (ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase))
                    {

                        // Retrieve the report object by using the repository-helper object.
                        reportview = reportviewRepositoryHelper.Get(repositoryReportViewLocation);
                        if (reportview == null)
                        {
                            displayError("Could not retrieve the report view for editing.");
                            return;
                        }
                    }
                    else if (ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase))
                    {

                        // Create a report view.
                        // CreateItem requests can be sent from a SharePoint list, but
                        // you must create a custom menu item to send the request.
                        // Dashboard Designer can send edit requests only.
                        reportview = new ReportView
                        {
                            RendererClassName = typeof(SampleReportRenderer).AssemblyQualifiedName, 
                            SubTypeId = "SampleReportView"
                        };
                    }
                    else
                    {
                        displayError("Invalid Action.");
                        return;
                    }

                    VerifyReportView(reportview);

                    // Save the original report and helper objects across page postbacks.
                    ViewState["action"] = action;
                    ViewState["reportview"] = reportview;
                    ViewState["reportviewrepositoryhelper"] = reportviewRepositoryHelper;
                    ViewState["itemlocation"] = itemLocation;

                    // Populate the child controls.
                    textboxName.Text = reportview.Name.ToString();
                    textboxDescription.Text = reportview.Description.ToString();
                }
                catch (Exception ex)
                {
                    displayError("An error has occurred. Please contact your administrator for more information.");
                    if (reportviewRepositoryHelper != null)
                    {

                        // Add the exception detail to the server event log.
                        reportviewRepositoryHelper.HandleException(ex);
                    }
                }
            }
        }

        // Handles the Click event of the buttonOK control.
        protected void buttonOK_Click(object sender, EventArgs e)
        {
            EnsureChildControls();

            // Verify that the textboxName control contains a value.
            if (string.IsNullOrEmpty(textboxName.Text))
            {
                labelErrorMessage.Text = "A report view name is required.";
                return;
            }

            // Clear any pre-existing error message.
            labelErrorMessage.Text = string.Empty;

            // Retrieve the report and helper objects from view state.
            string action = (string)ViewState["action"];
            string itemLocation = (string) ViewState["itemlocation"];
            ReportView reportview = (ReportView)ViewState["reportview"];
            ReportViewRepositoryHelper reportviewRepositoryHelper = (ReportViewRepositoryHelper)ViewState["reportviewrepositoryhelper"];

            // Update the report object with form changes.
            reportview.Name.Text = textboxName.Text;
            reportview.Description.Text = textboxDescription.Text;

            // Save the report object to the PerformancePoint Services repository.
            try
            {
                reportview.Validate();
                if (ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase))
                {
                    reportview.CreatedDate = DateTime.Now;
                    ReportView newReportView = reportviewRepositoryHelper.Create(
                        string.IsNullOrEmpty(reportview.Location.ItemUrl) ? itemLocation : reportview.Location.ItemUrl, 
                        reportview);
                    ViewState["reportview"] = newReportView;
                    ViewState["action"] = ClickOnceLaunchValues.OpenItem;
                }
                else
                {
                    reportviewRepositoryHelper.Update(reportview);
                }
            }
            catch (Exception ex)
            {
                displayError("An error has occurred. Please contact your administrator for more information.");
                if (reportviewRepositoryHelper != null)
                {
                    // Add the exception detail to the server event log.
                    reportviewRepositoryHelper.HandleException(ex);
                }
            }
        }

        // Displays the error string in the labelErrorMessage label. 
        void displayError(string msg)
        {
            EnsureChildControls();

            labelErrorMessage.Text = msg;

            // Disable the OK button because the page is in an error state.
            buttonOK.Enabled = false;
            return;
        }

        // Verifies that the properties for the report object are set.
        static void VerifyReportView(ReportView reportview)
        {

            // Verify that all required properties are set. 
            if (string.IsNullOrEmpty(reportview.SubTypeId))
            {

                // This value must match the subType attribute specified
                // in the web.config file.
                reportview.SubTypeId = "SampleReportView";
            }

            if (string.IsNullOrEmpty(reportview.RendererClassName))
            {
                reportview.RendererClassName = typeof (SampleReportRenderer).AssemblyQualifiedName;
            }

            // Reports are consumers and do not use provider endpoints.
           reportview.BeginPoints.Clear();

            // If there are no consumer endpoints, create one so we can connect a filter or a scorecard to the report.
            if (0 == reportview.EndPoints.Count)
            {
                EndPoint endpoint = new EndPoint
                {
                    Category = EndPointCategory.None,
                    UniqueName = "SampleReportView_EndPoint",

                    // The display name is shown to users in Dashboard
                    // Designer to represent the endpoint that can be 
                    // connected to a filter or scorecard.
                    DisplayName = "Sample Report View EndPoint"
                };

                reportview.EndPoints.Add(endpoint);
            }
            
            // Set optional properties for reports.
            reportview.CustomData = "You can use this property to store custom information for this filter as a string or a serialized object.";
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="3ab3c-175">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="3ab3c-175">Next steps</span></span>
<span data-ttu-id="3ab3c-176"><a name="bk_next"> </a></span><span class="sxs-lookup"><span data-stu-id="3ab3c-176"></span></span>

<span data-ttu-id="3ab3c-177">Nach dem Erstellen Sie eines Bericht-Editors (einschließlich der Benutzeroberfläche, falls erforderlich) und eines berichtrenderers, Bereitstellen Sie die Erweiterung, wie in  [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="3ab3c-177">After you create a report editor (including its user interface, if required) and a report renderer, deploy the extension as described in  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="3ab3c-178">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="3ab3c-178">Additional resources</span></span>
<span data-ttu-id="3ab3c-179"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="3ab3c-179"></span></span>


-  [<span data-ttu-id="3ab3c-180">Vorgehensweise: Erstellen von berichtsrenderern für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ab3c-180">How to: Create report renderers for PerformancePoint Services in SharePoint</span></span>](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3ab3c-181">PerformancePoint-Dienste in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ab3c-181">PerformancePoint Services in SharePoint</span></span>](performancepoint-services-in-sharepoint.md)
    
  

