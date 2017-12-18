---
title: "Erstellen von tabellarischen Datenquellen-Editoren für PerformancePoint-Dienste in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3136420a-f8a2-4677-8b69-1d5d9705d96f
ms.openlocfilehash: 2ea178c0f757520bb65ac2d840022fcd2891b1fe
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="create-tabular-data-source-editors-for-performancepoint-services-in-sharepoint"></a>Erstellen von tabellarischen Datenquellen-Editoren für PerformancePoint-Dienste in SharePoint

In diesem Artikel erfahren Sie, wie die Editor-Komponente einer benutzerdefinierten Datenquellenerweiterung in Tabellenform für PerformancePoint-Dienste erstellt wird.

## <a name="what-are-custom-data-source-editors-for-performancepoint-services"></a>Was sind benutzerdefinierte Daten Editoren für PerformancePoint-Dienste ?
<a name="bk_intro"> </a>

Editoren für benutzerdefinierte Daten aktivieren PerformancePoint-Dienste Benutzer auf benutzerdefinierten tabellarischen Datenquellen Eigenschaften festlegen. Weitere Informationen zu Editor Anforderungen und Funktionen finden Sie unter  [Editoren für benutzerdefinierte PerformancePoint Services-Objekte](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).
  
    
    
Die folgenden Verfahren und Codebeispiele basieren auf der **SampleDataSourceEditor** -Klasse aus der [benutzerdefinierten Objekte (Beispiel)](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx). Der Editor ist eine dünne Anwendung, die ermöglicht Benutzern den Namen und eine Beschreibung der Datenquelle ändern, geben Aktiensymbole, und einen Proxy-Server-Adresse und der Cache die Dateispeicherort angeben. Den vollständigen Code für die Klasse, finden Sie unter  [Codebeispiel: Abrufen und Aktualisieren von benutzerdefinierten tabellarischen Datenquellen](#bk_example).
  
    
    
Es wird empfohlen, dass Sie den Beispiel-Editor als Vorlage verwenden. Das Beispiel zeigt wie Objekte aufrufen PerformancePoint-Dienste-API bietet Hilfsobjekte, die vereinfachen von Anrufen für Repository-Vorgänge (wie erstellen und Aktualisieren der Objekte), und bewährte Methoden für die Entwicklung von PerformancePoint-Dienste veranschaulicht.
  
    
    

## <a name="create-editors-for-custom-performancepoint-services-tabular-data-sources"></a>Erstellen von Editoren für benutzerdefinierte PerformancePoint-Dienste tabellarische Datenquellen
<a name="BKMK_ConfigDSEditor"> </a>


  
    
    

1. Installieren Sie PerformancePoint-Dienste, oder kopieren Sie die DLLs, die die Erweiterung verwendet (siehe Schritt 3) auf Ihrem Computer. Weitere Informationen finden Sie unter  [PerformancePoint-Dienste-DLLs in Entwicklungsszenarios](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).
    
  
2. Erstellen Sie in Visual Studio eine C#-Klassenbibliothek. Sollten Sie bereits eine Klassenbibliothek für die Erweiterung erstellt haben, fügen Sie eine neue C#-Klasse hinzu.
    
    Sie müssen die DLL mit einem starken Namen signieren. Stellen Sie außerdem sicher, dass alle Assemblys, auf die von der DLL verwiesen wird, ebenfalls starke Namen haben. Informationen dazu, wie Sie eine Assembly mit einem starken Namen signieren und ein öffentliches/privates Schlüsselpaar erstellen, finden Sie unter  [How to: Create a public/private key pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).
    
  
3. Fügen Sie dem Projekt die folgenden DLLs als Assemblyverweise hinzu:
    
  - Microsoft.PerformancePoint.Scorecards.Client.dll
    
  
  - Microsoft.SharePoint.dll (von Hilfsklassen verwendet)
    
  

    Der Beispieleditor enthält ebenfalls Assemblyverweise auf System.Core.dll, System.Web.dll, System.Web.Services.dll und System.Xml.Linq.dll. Je nach Funktionalität Ihrer Erweiterung sind u. U. weitere Projektverweise erforderlich.
    
  
4. Fügen Sie dem Projekt die folgenden Klassen aus dem Beispiel. Editor wird zur Interaktion mit dem Repository PerformancePoint-Dienste und die Cachedatei Hilfsklassen verwendet:
    
  - ExtensionRepositoryHelper.cs
    
  
  - DataSourceRepositoryHelper.cs
    
  
  - SampleDSCacheHandler.cs
    
  
5. Fügen Sie in Ihrer Editorklasse eine **using**-Direktive für den **Microsoft.PerformancePoint.Scorecards**-Namespace hinzu. Je nach Funktionalität der Erweiterung sind u. U. andere **using**-Direktiven erforderlich.
    
  
6. Erben Sie von der Basisklasse, die Ihre Editorimplementierung unterstützt. Da es sich beim Beispiel-Datenquellen-Editor um eine Webanwendung handelt, wird von der  [Page](https://msdn.microsoft.com/library/System.Web.UI.Page.aspx) -Klasse geerbt. Andere Implementierungen können von Basisklassen wie z. B. der [UserControl](https://msdn.microsoft.com/library/System.Windows.Forms.UserControl.aspx) - oder [WebPart](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebParts.WebPart.aspx) -Klasse abgeleitet werden.
    
  
7. Deklarieren Sie Variablen für die Steuerelemente, mit denen die Eigenschaften verfügbar gemacht werden, die die Benutzer anzeigen oder ändern sollen. Mit dem Beispiel-Datenquellen-Editor werden zunächst Variablen für die Webserversteuerelemente deklariert, die in der Benutzeroberflächenkomponente definiert sind, wobei es sich um eine ASPX-Seite handelt. Außerdem wird mit dem Beispieleditor ein Schaltflächensteuerelement definiert, mit dem Benutzer Änderungen senden können. Anschließend ruft der Editor die  [CreateChildControls()](https://msdn.microsoft.com/library/System.Web.UI.Control.CreateChildControls.aspx) -Methode auf, um die Steuerelemente auf der Seite verfügbar zu machen.
    
    > **Hinweis:** Im Editor wird die Programmierlogik separat von der Benutzeroberfläche definiert. Anweisungen zum Erstellen der Benutzeroberflächenkomponenten würden den Rahmen dieser Dokumentation sprengen. 

    Das Beispiel Datenquellen-Editors führt die Schritte 8 bis 11 in der **Page_Load** -Methode. **Page_Load** wird auch initialisieren und Variablen und Steuerelemente zu überprüfen, füllen Sie Steuerelemente und Statusinformationen für die benutzerdefinierte Daten Quell- und Helper-Objekte zu speichern.
    
  
8. Rufen Sie die Parameter aus der Abfragezeichenfolge ab, und legen Sie sie als Werte für lokale Variablen fest, wie im folgenden Codebeispiel dargestellt.
    
```cs
  
// The URL of the site collection that contains the PerformancePoint Services repository.
string server = Request.QueryString[ClickOnceLaunchKeys.SiteCollectionUrl];

// The location of the data source in the repository.
string itemLocation = Request.QueryString[ClickOnceLaunchKeys.ItemLocation];

// The operation to perform: OpenItem or CreateItem.
string action = Request.QueryString[ClickOnceLaunchKeys.LaunchOperation];
```


    For information about the query string parameters, see  [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).
    
  
9. Rufen Sie das **DataSourceRepositoryHelper** -Objekt, das Tätigen von Anrufen an das Repository verwendet wird, wie im folgenden Codebeispiel gezeigt.
    
```cs
  
DataSourceRepositoryHelper = new DataSourceRepositoryHelper();
```

10. Legen Sie wie im folgenden Codebeispiel dargestellt den Speicherort für die Datenquelle basierend auf dem Abfragezeichenfolgen-Parameter fest.
    
```cs
  RepositoryLocation repositoryDataSourceLocation = RepositoryLocation.CreateFromUriString(itemLocation);
```

11. Abzurufen Sie Vorgang ( _OpenItem_ oder _CreateItem_) aus der Abfragezeichenfolge und rufen Sie ab, oder erstellen Sie die benutzerdefinierte Datenquelle.
    
  - Verwenden Sie die **DataSourceRepositoryHelper.Get**-Methode zum Abrufen der benutzerdefinierten Datenquelle.
    
  
  - Um die benutzerdefinierte Datenquelle zu erstellen, verwenden Sie den Konstruktor **DataSource()** und definieren Sie dann die Eigenschaften für die Datenquelle [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) und [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SubTypeId.aspx) . [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SubTypeId.aspx) ist der eindeutige Bezeichner für die Datenquelle, und es muss übereinstimmen, das **subType** -Attribut, das Sie für die benutzerdefinierte Datenquelle in der PerformancePoint-Dienste web.config-Datei angeben.
    
    > **Hinweis:** Der Beispiel-Datenquellen-Editor enthält keine Logik zum Erstellen eines Datenquellenobjekts. Beispiele zum Erstellen eines benutzerdefinierten Objekts finden Sie unter  [Vorgehensweise: Erstellen von Bericht-Editoren für PerformancePoint-Dienste in SharePoint](how-to-create-report-editors-for-performancepoint-services-in-sharepoint.md) oder [Vorgehensweise: Erstellen von Filter-Editoren für PerformancePoint-Dienste in SharePoint](how-to-create-filter-editors-for-performancepoint-services-in-sharepoint.md). 

```cs
  if (ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase))
{
    // Use the repository-helper object to retrieve the data source.
    datasource = dataSourceRepositoryHelper.Get(repositoryDataSourceLocation);
    if (datasource == null)
    {
        displayError("Could not retrieve the data source for editing.");
        return;
    }
}
else
{
    displayError("Invalid Action.");
    return;
}
```


    > **Note:**
      > By default, users can create custom objects from PerformancePoint Dashboard Designer only. To enable users to create a custom object outside of Dashboard Designer, you must add a menu item that sends a  _CreateItem_ request to your editor from the content type in the repository. For more information, see [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx). 

    The sample data source editor performs steps 12 and 13 in the **buttonOK_Click** and **CreateCacheFile** methods. **buttonOK_Click** is also used to call the **AreAllInputsValid** method to validate the contents of the controls and to retrieve state information for the custom data source and the helper object.
    
  
12. Aktualisieren Sie die Datenquelle mit benutzerdefinierten Änderungen. Der Beispiel-Datenquellen-Editor ruft die **DataSourceRepositoryHelper.Update**-Methode auf, um die Eigenschaften  [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) und [CustomData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.CustomData.aspx) des Datenquellenobjekts im Repository zu aktualisieren. Mit [CustomData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.CustomData.aspx) können Sie ein serialisiertes Objekt oder eine serialisierte Zeichenfolge speichern. Der Beispiel-Editor speichert damit benutzerdefinierte Aktiensymbole, den Speicherort der Cachedatei, in der Aktienkurswerte gespeichert werden, sowie die Adresse des Proxyservers.
    
    > **HINWEIS** Benutzer können die  [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx)-, [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx)- und [Owner](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Owner.aspx)- (**Person Responsible**)-Eigenschaften eines benutzerdefinierten Objekts bearbeiten und benutzerdefinierte Objekte direkt in Dashboard-Designer und die PerformancePoint-Dienste-Repository löschen. 
13. Rufen Sie den Datenquellenanbieter auf, um Spaltenzuordnungen zu definieren, falls noch nicht geschehen.
    
  

## <a name="code-example-retrieve-and-update-custom-performancepoint-services-tabular-data-sources-in-sharepoint"></a>Codebeispiel: Abrufen und Aktualisieren von benutzerdefinierten PerformancePoint-Dienstdatenquellen in Tabellenform in SharePoint
<a name="bk_example"> </a>

Im folgenden Codebeispiel wird abgerufen und benutzerdefinierten tabellarischen Datenquellen aktualisiert. Dieser Code hat ihren Ursprung im Editor CodeBehind-Klasse, die die Programmierlogik für Steuerelemente bereitstellt, die in einer ASPX-Seite definiert sind.
  
    
    
Bevor Sie dieses Codebeispiel kompilieren können, müssen Sie Ihre Entwicklungsumgebung konfigurieren, wie beschrieben in  [Erstellen und konfigurieren Sie die Editorklasse für eine tabellarische Datenquellen in PerformancePoint Services-Editor](#BKMK_ConfigDSEditor).
  
    
    



```cs

using System;
using System.IO;
using System.Web.UI;
using System.Web.UI.WebControls;
using Microsoft.PerformancePoint.Scorecards;
using System.Xml.Linq;

namespace Microsoft.PerformancePoint.SDK.Samples.SampleDataSource
{
    // Represents the class that defines the sample data source editor.
    public class SampleDataSourceEditor : Page
    {

        #region Members
        // Declare private variables for the ASP.NET controls defined in the user interface.
        // The user interface is an ASPX page that defines the controls in HTML.
        private TextBox textboxName;
        private TextBox textboxDescription;
        private TextBox textboxStockSymbols;
        private TextBox textboxXMLLocation;
        private TextBox textboxProxy;
        private Label labelErrorMessage;
        private Button buttonOK;
        #endregion

        #region Page methods and events
        // Make the controls available to this class.
        protected override void CreateChildControls()
        {
            base.CreateChildControls();

            if (null == textboxProxy)
                textboxProxy = FindControl("textboxProxy") as TextBox;
            if (null == textboxName)
                textboxName = FindControl("textboxName") as TextBox;
            if (null == textboxDescription)
                textboxDescription = FindControl("textboxDescription") as TextBox;
            if (null == textboxStockSymbols)
                textboxStockSymbols = FindControl("textboxStockSymbols") as TextBox;
            if (null == textboxXMLLocation)
                textboxXMLLocation = FindControl("textboxXMLLocation") as TextBox;
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
            // Initialize controls the first time the page loads only.
            if (!IsPostBack)
            {
                EnsureChildControls();

                DataSourceRepositoryHelper dataSourceRepositoryHelper = null;
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
                    dataSourceRepositoryHelper =
                        new DataSourceRepositoryHelper();

                    // Set the data source location.
                    RepositoryLocation repositoryDataSourceLocation = RepositoryLocation.CreateFromUriString(itemLocation);

                    DataSource datasource;

                    // Retrieve the data source object by
                    // using the repository-helper object.
                    if (ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase))
                    {
                        datasource = dataSourceRepositoryHelper.Get(repositoryDataSourceLocation);
                        if (datasource == null)
                        {
                            displayError("Could not retrieve the data source for editing.");
                            return;
                        }
                    }
                    else
                    {
                        displayError("Invalid Action.");
                        return;

                    }

                    // Save the original data source and helper objects across page postbacks.
                    ViewState["action"] = action;
                    ViewState["datasource"] = datasource;
                    ViewState["datasourcerepositoryhelper"] = dataSourceRepositoryHelper;

                    // Populate the child controls.
                    if (null != datasource.Name)
                        textboxName.Text = datasource.Name.ToString();

                    if (null != datasource.Description)
                        textboxDescription.Text = datasource.Description.ToString();

                    if (null != datasource.CustomData)
                    {
                        string[] splitCustomData = datasource.CustomData.Split('&amp;');
                        if (splitCustomData.Length > 2)
                        {
                            textboxStockSymbols.Text = splitCustomData[0];
                            textboxXMLLocation.Text = splitCustomData[1].Replace(@"\\SampleStockQuotes.xml", string.Empty);
                            textboxProxy.Text = splitCustomData[2];
                        }
                    }
                }
                catch (Exception ex)
                {
                    displayError("An error has occurred. Please contact your administrator for more information.");
                    if (dataSourceRepositoryHelper != null)
                    {
                        // Add the exception detail to the server
                        // event log.
                        dataSourceRepositoryHelper.HandleException(ex);
                    }
                }
            }
        }

        // Handles the Click event of the buttonOK control.
        protected void buttonOK_Click(object sender, EventArgs e)
        {
            EnsureChildControls();

            // Verify that the required fields contain values.
            if (!AreAllInputsValid())
                return;

            // Clear any pre-existing error message.
            labelErrorMessage.Text = string.Empty;

            // Retrieve the data source and helper objects from view state.
            string action = (string)ViewState["action"];
            DataSource datasource = (DataSource)ViewState["datasource"];
            DataSourceRepositoryHelper datasourcerepositoryhelper = (DataSourceRepositoryHelper)ViewState["datasourcerepositoryhelper"];

            // Update the data source object with form changes.
            datasource.Name.Text = textboxName.Text;
            datasource.Description.Text = textboxDescription.Text;

            // Define column mappings if they aren't already defined.
            if (datasource.DataTableMapping.ColumnMappings.Count <= 0)
            {
                datasource.DataTableMapping = WSTabularDataSourceProvider.CreateDataColumnMappings();
            }

            // Save the data source to the repository
            // by using the repository-helper object.
            try
            {
                CreateCacheFile(datasource);

                datasource.Validate();

                if (ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase))
                {
                    datasourcerepositoryhelper.Update(datasource);
                }
                else
                {
                    displayError("Invalid Action.");
                }
            }
            catch (Exception ex)
            {
                displayError("An error has occurred. Please contact your administrator for more information.");
                if (datasourcerepositoryhelper != null)
                {
                    // Add the exception detail to the server event log.
                    datasourcerepositoryhelper.HandleException(ex);
                }
            }
        }
        #endregion

        #region Helper methods
        // Display the error string in the labelErrorMessage label.
        void displayError(string msg)
        {
            EnsureChildControls();

            labelErrorMessage.Text = msg;

            // Disable the OK button because the page is in an error state.
            buttonOK.Enabled = false;
            return;
        }

        // Validate the text box inputs.
        bool AreAllInputsValid()
        {
            if (string.IsNullOrEmpty(textboxProxy.Text))
            {
                labelErrorMessage.Text = "The proxy server address is required.";
                return false;
            }

            if (string.IsNullOrEmpty(textboxXMLLocation.Text))
            {
                labelErrorMessage.Text = "The location to save the cache file to is required.";
                return false;
            }

            if (string.IsNullOrEmpty(textboxName.Text))
            {
                labelErrorMessage.Text = "A data source name is required.";
                return false;
            }

            if (string.IsNullOrEmpty(textboxStockSymbols.Text))
            {
                labelErrorMessage.Text = "A stock symbol is required.";
                return false;
            }

            return true;
        }

        // Create the XML cache file at the specified location and
        // store it and the stock symbols in the CustomData
        // property of the data source.
        void CreateCacheFile(DataSource datasource)
        {
            string cacheFileLocation = string.Format("{0}\\\\{1}", textboxXMLLocation.Text.TrimEnd('\\\\'),
                                                     "SampleStockQuotes.xml");

            datasource.CustomData = string.Format("{0}&amp;{1}&amp;{2}", textboxStockSymbols.Text, cacheFileLocation, textboxProxy.Text);

            // Check if the cache file already exists.
            if (!File.Exists(cacheFileLocation))
            {
                // Create the cache file if it does not exist.
                XDocument doc = SampleDSCacheHandler.DefaultCacheFileContent;
                doc.Save(cacheFileLocation);
            }
        }
        #endregion
    }
}
```


## <a name="next-steps"></a>Nächste Schritte
<a name="bk_next"> </a>

Nachdem Sie eine Datenquelle-Editors (einschließlich der Benutzeroberfläche, falls erforderlich) und Datenquellenanbieter, Sie die Erweiterung wie unter  [Gewusst wie: Manuelles Registrieren von PerformancePoint-Dienste-Erweiterungen](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)bereitstellen.
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_resources"> </a>


-  [Vorgehensweise: Erstellen von Anbietern für tabellarische Datenquellen für PerformancePoint Services in SharePoint](how-to-create-tabular-data-source-providers-for-performancepoint-services-in-sha.md)
    
  
-  [PerformancePoint-Dienste in SharePoint](performancepoint-services-in-sharepoint.md)
    
  

