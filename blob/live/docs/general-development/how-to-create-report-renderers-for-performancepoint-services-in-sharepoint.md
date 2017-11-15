---
title: "Erstellen von Berichtsrenderern für PerformancePoint-Dienste in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: eeab12ad6c73463b15e9086b18cc054b501b71d5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-report-renderers-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="59fd6-102">Vorgehensweise: Erstellen von Berichtsrenderern für PerformancePoint-Dienste in SharePoint</span><span class="sxs-lookup"><span data-stu-id="59fd6-102">How to: Create report renderers for PerformancePoint Services in SharePoint</span></span>
<span data-ttu-id="59fd6-103">In diesem Artikel erfahren Sie, wie die Rendererkomponente in einer benutzerdefinierten Berichtserweiterung für PerformancePoint-Dienste erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="59fd6-103">Learn how to create the renderer component in a custom report extension for PerformancePoint Services.</span></span>
## <a name="what-are-custom-report-renderers-for-performancepoint-services"></a><span data-ttu-id="59fd6-104">Was sind benutzerdefinierte Berichtsrenderer für PerformancePoint-Dienste ?</span><span class="sxs-lookup"><span data-stu-id="59fd6-104">What are custom report renderers for PerformancePoint Services?</span></span>
<span data-ttu-id="59fd6-105"><a name="bk_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="59fd6-105"></span></span>

<span data-ttu-id="59fd6-p101">In PerformancePoint-Dienste sind benutzerdefinierte Berichtsrenderer Webserver-Steuerelemente, die einen benutzerdefinierten Bericht in einem Webpart zu rendern. Ein Renderer schreibt den HTML-Code für die berichtvisualisierung (beispielsweise eine Tabelle oder ein Diagramm), stellt die Logik zur Verarbeitung von Berichtsparametern und das Report-Objekt aus dem Repository abgerufen.</span><span class="sxs-lookup"><span data-stu-id="59fd6-p101">In PerformancePoint Services, custom report renderers are web server controls that render a custom report in a Web Part. A renderer writes the HTML for the report visualization (such as a table or chart), provides logic to handle report parameters, and retrieves the report object from the repository.</span></span>
  
    
    
<span data-ttu-id="59fd6-108">Die folgenden Vorgehensweisen und Codebeispiele basieren auf der **SampleReportRenderer**-Klasse aus dem [Beispiel für benutzerdefinierte Objekte](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="59fd6-108">The following procedures and code examples are based on the **SampleReportRenderer** class from the [custom objects sample](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span></span> <span data-ttu-id="59fd6-109">Der Renderer rendert eine Tabelle und füllt sie mit den Werten aus einem verknüpften Filter.</span><span class="sxs-lookup"><span data-stu-id="59fd6-109">The renderer renders a table and populates it with values received from a linked filter.</span></span> <span data-ttu-id="59fd6-110">Den vollständigen Code für die Klasse finden Sie unter [Codebeispiel: Erstellen eines Renderers für benutzerdefinierte PerformancePoint-Dienste-Berichte in SharePoint](#bk_example)</span><span class="sxs-lookup"><span data-stu-id="59fd6-110">For the complete code for the class, see  [Code example: Create a renderer for custom PerformancePoint Services reports in SharePoint](#bk_example).</span></span>
  
    
    
<span data-ttu-id="59fd6-p103">Es wird empfohlen, dass Sie die Berichtsrenderer Beispiel als Vorlage verwenden. Das Beispiel zeigt, wie Objekte in der PerformancePoint-Dienste-API-aufrufen und bewährte Methoden für die Entwicklung von PerformancePoint-Dienste veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="59fd6-p103">We recommend that you use the sample report renderer as a template. The sample shows how to call objects in the PerformancePoint Services API and demonstrates best practices for PerformancePoint Services development.</span></span>
  
    
    

## <a name="create-renderers-for-custom-performancepoint-services-reports"></a><span data-ttu-id="59fd6-113">Erstellen von Renderern für benutzerdefinierte PerformancePoint-Dienste Berichte</span><span class="sxs-lookup"><span data-stu-id="59fd6-113">Create renderers for custom PerformancePoint Services reports</span></span>
<span data-ttu-id="59fd6-114"><a name="BKMK_ConfigRenderer"> </a></span><span class="sxs-lookup"><span data-stu-id="59fd6-114"></span></span>


  
    
    

1. <span data-ttu-id="59fd6-p104">Installieren Sie PerformancePoint-Dienste, oder kopieren Sie die DLLs, die die Erweiterung verwendet (siehe Schritt 3) auf Ihrem Computer. Weitere Informationen finden Sie unter  [PerformancePoint-Dienste-DLLs in Entwicklungsszenarios](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="59fd6-p104">Install PerformancePoint Services, or copy the DLLs that your extension uses (listed in step 3) to your computer. For more information, see  [DLLs with Class Libraries](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span></span> 
    
  
2. <span data-ttu-id="59fd6-p105">Erstellen Sie in Visual Studio eine C#-Klassenbibliothek. Sollten Sie bereits eine Klassenbibliothek für die Erweiterung erstellt haben, fügen Sie eine neue C#-Klasse hinzu.</span><span class="sxs-lookup"><span data-stu-id="59fd6-p105">In Visual Studio, create a C# class library. If you have already created a class library for your extension, add a new C# class.</span></span>
    
    <span data-ttu-id="59fd6-p106">Sie müssen die DLL mit einem starken Namen signieren. Stellen Sie außerdem sicher, dass alle Assemblys, auf die von der DLL verwiesen wird, ebenfalls starke Namen haben. Informationen dazu, wie Sie eine Assembly mit einem starken Namen signieren und ein öffentliches/privates Schlüsselpaar erstellen, finden Sie unter  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span><span class="sxs-lookup"><span data-stu-id="59fd6-p106">You must sign your DLL with a strong name. In addition, ensure that all assemblies referenced by your DLL have strong names. For information about how to sign an assembly with a strong name and how to create a public/private key pair, see  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span></span>
    
  
3. <span data-ttu-id="59fd6-122">Fügen Sie die folgenden PerformancePoint-Dienste DLLs als Assemblyverweise zum Projekt hinzu:</span><span class="sxs-lookup"><span data-stu-id="59fd6-122">Add the following PerformancePoint Services DLLs as assembly references to the project:</span></span>
    
  - <span data-ttu-id="59fd6-123">Microsoft.PerformancePoint.Scorecards.Client.dll</span><span class="sxs-lookup"><span data-stu-id="59fd6-123">Microsoft.PerformancePoint.Scorecards.Client.dll</span></span>
    
  
  - <span data-ttu-id="59fd6-124">Microsoft.PerformancePoint.Scorecards.Server.dll</span><span class="sxs-lookup"><span data-stu-id="59fd6-124">Microsoft.PerformancePoint.Scorecards.Server.dll</span></span>
    
  
  - <span data-ttu-id="59fd6-125">Microsoft.PerformancePoint.Scorecards.Store.dll</span><span class="sxs-lookup"><span data-stu-id="59fd6-125">Microsoft.PerformancePoint.Scorecards.Store.dll (used by helper classes)</span></span>
    
  

    <span data-ttu-id="59fd6-126">Je nach Funktionalität der Erweiterung sind u. U. andere Projektverweise erforderlich.</span><span class="sxs-lookup"><span data-stu-id="59fd6-126">Depending on your extension's functionality, other project references may be required.</span></span>
    
  
4. <span data-ttu-id="59fd6-127">Fügen Sie in der Rendererklasse **using** Direktiven für die folgenden PerformancePoint-Dienste-Namespaces hinzu:</span><span class="sxs-lookup"><span data-stu-id="59fd6-127">In your renderer class, add **using** directives for the following PerformancePoint Services namespaces:</span></span>
    
  -  [<span data-ttu-id="59fd6-128">Microsoft.PerformancePoint.Scorecards</span><span class="sxs-lookup"><span data-stu-id="59fd6-128">Microsoft.PerformancePoint.Scorecards</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [<span data-ttu-id="59fd6-129">Microsoft.PerformancePoint.Scorecards.Server.Extensions</span><span class="sxs-lookup"><span data-stu-id="59fd6-129">Microsoft.PerformancePoint.Scorecards.Server.Extensions</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.aspx)
    
  
  -  [<span data-ttu-id="59fd6-130">Microsoft.PerformancePoint.Scorecards.Store</span><span class="sxs-lookup"><span data-stu-id="59fd6-130">Microsoft.PerformancePoint.Scorecards.Store</span></span>](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.aspx)
    
  

    <span data-ttu-id="59fd6-131">Je nach Funktionalität der Erweiterung sind u. U. andere **using**-Direktiven erforderlich.</span><span class="sxs-lookup"><span data-stu-id="59fd6-131">Depending on your extension's functionality, other **using** directives may be required.</span></span>
    
  
5. <span data-ttu-id="59fd6-132">Sie muss von der  [ParameterizableControl](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.aspx) -Basisklasse erben.</span><span class="sxs-lookup"><span data-stu-id="59fd6-132">Inherit from the  [ParameterizableControl](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.aspx) base class.</span></span>
    
  
6. <span data-ttu-id="59fd6-133">Überschreiben Sie die  [GetElement](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.GetElement.aspx) -Methode, um das Berichtsobjekt aus dem Repository abzurufen.</span><span class="sxs-lookup"><span data-stu-id="59fd6-133">Override the  [GetElement](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.GetElement.aspx) method to retrieve the report object from the repository.</span></span>
    
  
7. <span data-ttu-id="59fd6-134">Überschreiben Sie die  [SetData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.SetData.aspx) -Methode, um das Berichtsdataset einzurichten und eingehende Parameterwerte abzurufen.</span><span class="sxs-lookup"><span data-stu-id="59fd6-134">Override the  [SetData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.SetData.aspx) method to set up the report dataset and retrieve incoming parameter values.</span></span>
    
  
8. <span data-ttu-id="59fd6-135">Überschreiben Sie die [Render](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebControl.Render.aspx)-Methode, um den HTML-Code für die Berichtvisualisierung zu rendern.</span><span class="sxs-lookup"><span data-stu-id="59fd6-135">Override the  [Render](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebControl.Render.aspx) method to render the HTML for the report visualization.</span></span>
    
  

## <a name="code-example-create-a-renderer-for-custom-performancepoint-services-reports-in-sharepoint"></a><span data-ttu-id="59fd6-136">Codebeispiel: Erstellen eines Renderers für benutzerdefinierte PerformancePoint-Dienste-Berichte in SharePoint</span><span class="sxs-lookup"><span data-stu-id="59fd6-136">Code example: Create a renderer for custom PerformancePoint Services reports in SharePoint Server 2013</span></span>
<span data-ttu-id="59fd6-137"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="59fd6-137"></span></span>

<span data-ttu-id="59fd6-138">Mit der Klasse im folgenden Codebeispiel wird ein Berichtsrenderer erstellt, mit dem über den Beispielfilter übergebene Aktieninformationen angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="59fd6-138">The class in the following code example creates a report renderer that displays stock information passed in from the sample filter.</span></span>
  
    
    
<span data-ttu-id="59fd6-139">Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie die Entwicklungsumgebung wie unter  [So erstellen und konfigurieren Sie die Rendererklasse](#BKMK_ConfigRenderer) beschrieben konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="59fd6-139">Before you can compile this code example, you must configure your development environment as described in  [To create and configure the renderer class](#BKMK_ConfigRenderer).</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.Data;
using System.Web.UI;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.Server.Extensions;
using Microsoft.PerformancePoint.Scorecards.Store;

namespace Microsoft.PerformancePoint.SDK.Samples.SampleReport
{

    // The class that define the sample report's renderer.
    public class SampleReportRenderer : ParameterizableControl 
    {
        private ReportView reportView;

        private ReportView ReportView
        {
            get
            {

                // The GetElement method is used internally by this property, which is used
                // in turn by the SetData method.
                reportView = GetElement(ElementLocation) as ReportView;
                return reportView;
            }
        }

        // Initializes the current instance according to a standard interface. This method
        // sets up the dataset.
        public override void SetData(RepositoryLocation elementLocation, string resourcePath, string targetControlId, BIDataContainer dataContainer, bool accessibilityMode)
        {

            // The renderer must call the base implementation of the SetData method
            // to set report properties.
            base.SetData(elementLocation, resourcePath, targetControlId, dataContainer, accessibilityMode);
        
            if (null != ReportView)
            {

                // If the report view's custom data represents a serialized object, deserialize
                // it, and then use it to access a data source or other object.
                string customData = ReportView.CustomData;
                if (!string.IsNullOrEmpty(customData))
                {
                    System.Diagnostics.Debug.WriteLine(string.Format("Report view '{0}' has the following custom data: {1}", ReportView.Name.Text, customData));
                }
                
                // Iterate through the user's selections sent by the filter. 
                // The MultiSelectTreeControl filter control can send multiple
                // rows of data but other native controls send one message only.
                foreach (ParameterMessage message in BIDataContainer.ParameterMessages)
                {
                    // This line demonstrates how to do something with each incoming parameter message.
                    System.Diagnostics.Debug.WriteLine(string.Format("Parameter message: {0}", message.DisplayName));
                }
            }
        }
        
        // Render page content using the specified writer.
        protected override void Render(HtmlTextWriter output)
        {
            try
            {
                if (null != ReportView &amp;&amp; !string.IsNullOrEmpty(ReportView.CustomData))
                {
                    output.RenderBeginTag(HtmlTextWriterTag.P);
                    output.RenderBeginTag(HtmlTextWriterTag.B);

                    // This line shows how to retrieve the content of the
                    // report's optional CustomData property. CustomData can store
                    // information that the report does not store elsewhere.
                    output.Write(string.Format("The ReportView &amp;quot;{0}&amp;quot; has CustomData information. The CustomData is &amp;quot;{1}&amp;quot;", 
                        ReportView.Name.Text, ReportView.CustomData));
                    output.RenderEndTag(); // B
                    output.RenderEndTag(); // P
                }

                Dictionary<Guid, ParameterMessage> parametersIndex =
                    IndexParameterMessages(BIDataContainer.ParameterMessages.ToArray());

                // Each connection gets a unique identifier.
                foreach (Guid parameterMappingId in parametersIndex.Keys)
                {
                    ParameterMessage message = parametersIndex[parameterMappingId];

                    output.RenderBeginTag(HtmlTextWriterTag.Table);
                    
                    output.AddAttribute(HtmlTextWriterAttribute.Style, "ms-partline");
                    output.RenderBeginTag(HtmlTextWriterTag.Tr);

                    output.AddAttribute(HtmlTextWriterAttribute.Colspan, "5");
                    output.RenderBeginTag(HtmlTextWriterTag.Td);
                    
                    output.RenderBeginTag(HtmlTextWriterTag.B);
                    output.Write(string.Format("EndPoint name is: {0}", message.Values.TableName));

                    output.RenderEndTag();  // B
                    output.RenderEndTag();  // Td
                    output.RenderEndTag();  // Tr

                    output.AddAttribute(HtmlTextWriterAttribute.Style, "\\"border-bottom:solid 10px #ffdd00; background:PapayaWhip\\"");
                    output.RenderBeginTag(HtmlTextWriterTag.Tr);

                    // Read the message.Values data table and print the column names.
                    foreach (DataColumn col in message.Values.Columns)
                    {
                        output.RenderBeginTag(HtmlTextWriterTag.Td);
                        output.Write(string.IsNullOrEmpty(col.Caption) ? "&amp;nbsp;" : col.Caption);
                        output.RenderEndTag();
                    }
                    output.RenderEndTag();  // Tr

                    // Print the data from the Values property, which is a data table.
                    foreach (DataRow row in message.Values.Rows)
                    {
                        output.RenderBeginTag(HtmlTextWriterTag.Tr);
                        for (int i = 0; i < message.Values.Columns.Count; i++)
                        {
                            output.RenderBeginTag(HtmlTextWriterTag.Td);
                            output.Write(string.IsNullOrEmpty(row[i].ToString()) ? "&amp;nbsp;" : row[i].ToString());
                            output.RenderEndTag();
                        }
                        output.RenderEndTag();  // Tr
                    }
                    output.RenderEndTag(); // table
                }
            }
            catch (Exception e)
            {
                output.RenderBeginTag(HtmlTextWriterTag.H1);
                output.Write("Error! An exception has occurred!");
                output.RenderEndTag();
                
                output.RenderBeginTag(HtmlTextWriterTag.P);
                output.Write(e.Message);
                output.RenderEndTag();

                output.RenderBeginTag(HtmlTextWriterTag.P); 
                output.Write(e.StackTrace);
                output.RenderEndTag();
            }
        }

        // Get the report object.
        protected override Element GetElement(RepositoryLocation elementLocation)
        {
            ReportView rv = null;
            if (!RepositoryLocation.IsNullOrEmpty(elementLocation))
            {
                rv = SPDataStore.GlobalDataStore.GetReportViewForExecution(elementLocation);
            }
            return (rv);
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="59fd6-140">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="59fd6-140">Next steps</span></span>
<span data-ttu-id="59fd6-141"><a name="bk_next"> </a></span><span class="sxs-lookup"><span data-stu-id="59fd6-141"></span></span>

<span data-ttu-id="59fd6-142">Nach dem Erstellen Sie eines Berichtsrenderers und eines Bericht-Editors (einschließlich der Benutzeroberfläche, falls erforderlich), Bereitstellen Sie die Erweiterung, wie in  [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="59fd6-142">After you create a report renderer and a report editor (including its user interface, if required), deploy the extension as described in  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="59fd6-143">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="59fd6-143">Additional resources</span></span>
<span data-ttu-id="59fd6-144"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="59fd6-144"></span></span>


-  [<span data-ttu-id="59fd6-145">Vorgehensweise: Erstellen von berichtsrenderern für PerformancePoint Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="59fd6-145">How to: Create report renderers for PerformancePoint Services in SharePoint</span></span>](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="59fd6-146">PerformancePoint-Dienste in SharePoint</span><span class="sxs-lookup"><span data-stu-id="59fd6-146">PerformancePoint Services in SharePoint</span></span>](performancepoint-services-in-sharepoint.md)
    
  

