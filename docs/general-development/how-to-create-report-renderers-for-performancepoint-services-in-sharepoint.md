---
title: "Erstellen von Berichtsrenderern für PerformancePoint-Dienste in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 44a84b222c6bb661b1b4560ab7b72a9063507d4e
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="create-report-renderers-for-performancepoint-services-in-sharepoint"></a>Erstellen von Berichtsrenderern für PerformancePoint-Dienste in SharePoint

In diesem Artikel erfahren Sie, wie die Rendererkomponente in einer benutzerdefinierten Berichtserweiterung für PerformancePoint-Dienste erstellt wird.

## <a name="what-are-custom-report-renderers-for-performancepoint-services"></a>Was sind benutzerdefinierte Berichtsrenderer für PerformancePoint-Dienste ?
<a name="bk_intro"> </a>

In PerformancePoint-Dienste sind benutzerdefinierte Berichtsrenderer Webserver-Steuerelemente, die einen benutzerdefinierten Bericht in einem Webpart zu rendern. Ein Renderer schreibt den HTML-Code für die berichtvisualisierung (beispielsweise eine Tabelle oder ein Diagramm), stellt die Logik zur Verarbeitung von Berichtsparametern und das Report-Objekt aus dem Repository abgerufen.
  
    
    
Die folgenden Vorgehensweisen und Codebeispiele basieren auf der **SampleReportRenderer**-Klasse aus dem [Beispiel für benutzerdefinierte Objekte](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx). Der Renderer rendert eine Tabelle und füllt sie mit den Werten aus einem verknüpften Filter. Den vollständigen Code für die Klasse finden Sie unter [Codebeispiel: Erstellen eines Renderers für benutzerdefinierte PerformancePoint-Dienste-Berichte in SharePoint](#bk_example)
  
    
    
Es wird empfohlen, dass Sie die Berichtsrenderer Beispiel als Vorlage verwenden. Das Beispiel zeigt, wie Objekte in der PerformancePoint-Dienste-API-aufrufen und bewährte Methoden für die Entwicklung von PerformancePoint-Dienste veranschaulicht.
  
    
    

## <a name="create-renderers-for-custom-performancepoint-services-reports"></a>Erstellen von Renderern für benutzerdefinierte PerformancePoint-Dienste Berichte
<a name="BKMK_ConfigRenderer"> </a>


  
    
    

1. Installieren Sie PerformancePoint-Dienste, oder kopieren Sie die DLLs, die die Erweiterung verwendet (siehe Schritt 3) auf Ihrem Computer. Weitere Informationen finden Sie unter  [PerformancePoint-Dienste-DLLs in Entwicklungsszenarios](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx). 
    
  
2. Erstellen Sie in Visual Studio eine C#-Klassenbibliothek. Sollten Sie bereits eine Klassenbibliothek für die Erweiterung erstellt haben, fügen Sie eine neue C#-Klasse hinzu.
    
    Sie müssen die DLL mit einem starken Namen signieren. Stellen Sie außerdem sicher, dass alle Assemblys, auf die von der DLL verwiesen wird, ebenfalls starke Namen haben. Informationen dazu, wie Sie eine Assembly mit einem starken Namen signieren und ein öffentliches/privates Schlüsselpaar erstellen, finden Sie unter  [How to: Create a Public/Private Key Pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).
    
  
3. Fügen Sie die folgenden PerformancePoint-Dienste DLLs als Assemblyverweise zum Projekt hinzu:
    
  - Microsoft.PerformancePoint.Scorecards.Client.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.Server.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.Store.dll
    
  

    Je nach Funktionalität der Erweiterung sind u. U. andere Projektverweise erforderlich.
    
  
4. Fügen Sie in der Rendererklasse **using** Direktiven für die folgenden PerformancePoint-Dienste-Namespaces hinzu:
    
  -  [Microsoft.PerformancePoint.Scorecards](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.aspx)
    
  
  -  [Microsoft.PerformancePoint.Scorecards.Server.Extensions](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.aspx)
    
  
  -  [Microsoft.PerformancePoint.Scorecards.Store](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.aspx)
    
  

    Je nach Funktionalität der Erweiterung sind u. U. andere **using**-Direktiven erforderlich.
    
  
5. Sie muss von der  [ParameterizableControl](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.aspx) -Basisklasse erben.
    
  
6. Überschreiben Sie die  [GetElement](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.GetElement.aspx) -Methode, um das Berichtsobjekt aus dem Repository abzurufen.
    
  
7. Überschreiben Sie die  [SetData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.ParameterizableControl.SetData.aspx) -Methode, um das Berichtsdataset einzurichten und eingehende Parameterwerte abzurufen.
    
  
8. Überschreiben Sie die [Render](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebControl.Render.aspx)-Methode, um den HTML-Code für die Berichtvisualisierung zu rendern.
    
  

## <a name="code-example-create-a-renderer-for-custom-performancepoint-services-reports-in-sharepoint"></a>Codebeispiel: Erstellen eines Renderers für benutzerdefinierte PerformancePoint-Dienste-Berichte in SharePoint
<a name="bk_example"> </a>

Mit der Klasse im folgenden Codebeispiel wird ein Berichtsrenderer erstellt, mit dem über den Beispielfilter übergebene Aktieninformationen angezeigt werden.
  
    
    
Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie die Entwicklungsumgebung wie unter  [So erstellen und konfigurieren Sie die Rendererklasse](#BKMK_ConfigRenderer) beschrieben konfigurieren.
  
    
    



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


## <a name="next-steps"></a>Nächste Schritte
<a name="bk_next"> </a>

Nach dem Erstellen Sie eines Berichtsrenderers und eines Bericht-Editors (einschließlich der Benutzeroberfläche, falls erforderlich), Bereitstellen Sie die Erweiterung, wie in  [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)beschrieben.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addResources"> </a>


-  [Vorgehensweise: Erstellen von berichtsrenderern für PerformancePoint Services in SharePoint](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [PerformancePoint-Dienste in SharePoint](performancepoint-services-in-sharepoint.md)
    
  

