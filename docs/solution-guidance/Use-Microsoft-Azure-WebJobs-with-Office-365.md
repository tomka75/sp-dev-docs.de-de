---
title: Verwenden Sie Microsoft Azure WebJobs mit Office 365
ms.date: 11/03/2017
ms.openlocfilehash: 0b3eb304efb291dfa4c0bb7c0809f2c5b044d28f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="use-microsoft-azure-webjobs-with-office-365"></a>Verwenden Sie Microsoft Azure WebJobs mit Office 365

Verwenden von Azure WebJobs Zeitgeberaufträge implementieren, die SharePoint Online zugreifen können.

_**Gilt für:** Add-Ins für SharePoint | SharePoint 2013 | SharePoint Online_

**Bereitgestellt von:** Tobias Zimmergren

Implementieren Sie Timer Job Funktionen mit [Microsoft Azure WebJobs](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/) oder Windows-Taskplaner zum Ausführen von Aufgaben in SharePoint Online. Ein Zeitgeberauftrag ist ein wiederholte, geplanten, Hintergrundprozess, der in SharePoint für bestimmte Aufgaben ausgeführt werden. Beispielsweise sollten Sie einen Zeitgeberauftrag zum Kopieren von Daten in einer SharePoint-Liste in eine Datenbank eingegeben. In SharePoint Online und kann nicht farmlösungen, bereitgestellt werden, also wie Zeitgeberaufträge in der Vergangenheit bereitgestellt wurden. Um ähnliche Timer Job-Funktionen in SharePoint Online zu implementieren, müssen Sie eine Konsolenanwendung als ein WebJob Azure ausgeführt werden. Die Konsolenanwendung greift auf SharePoint Online mit dem clientseitigen Objektmodell (CSOM). Dieser Artikel enthält Informationen zu den grundlegenden Konzepten vertraut, die bei der Bereitstellung von konsolenanwendungen als Azure WebJobs zum Ausführen von und Zugreifen auf SharePoint Online-Websites und den Inhalt.

## <a name="create-and-run-a-console-application-as-an-azure-webjob"></a>Erstellen Sie und führen Sie eine Konsolenanwendung als ein WebJob Azure
<a name="sectionSection0"> </a>

Informationen zum Einrichten der Konsolenanwendung zum Ausführen als einem Azure WebJob müssen Sie:

1. Erstellen eines Kontos Organisation für die Azure WebJob zu verwenden, um SharePoint-Websites und Inhalte zuzugreifen.
    
2. Erstellen und Einrichten der Konsolenanwendung.
    
3. Fügen Sie Code hinzu, um die Konsolenanwendung.
    
4. Veröffentlichen Sie die Konsolenanwendung als einem Azure WebJob.
    
5. Führen Sie aus, und überprüfen Sie Ihre Azure WebJob.

## <a name="create-an-organization-account"></a>Erstellen Sie ein Konto für die Organisation
<a name="sectionSection1"> </a>

Sie müssen zum Erstellen eines Kontos für die Azure WebJob beim Zugriff auf SharePoint-Websites und Inhalte verwenden. Weitere Informationen finden Sie unter [Hinzufügen von Benutzern einzeln zu Office 365-Admin-Hilfe](https://support.office.microsoft.com/article/Add-users-individually-to-Office-365---Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec). Wenn der Azure-WebJob ausgeführt wird, wird das Feld **Geändert von** speichert und zeigt den Wert im **Anzeigename den Namen** des Kontos Organisation eingegeben. Stellen Sie sicher, dass Sie einen Anzeigenamen auswählen, den Ihre Benutzer auf einfache Weise als das Konto für den Zugriff auf SharePoint, die WebJob Azure verwendet identifizieren können.

## <a name="create-and-set-up-the-console-application"></a>Erstellen und Einrichten der Konsolenanwendung
<a name="sectionSection2"> </a>

So erstellen Sie eine Konsolenanwendung zum Ausführen als einem Azure WebJob, führen Sie die folgenden Schritte aus:

1. Erstellen Sie ein neues Konsolenanwendungsprojekt durch:
    
    1. Wählen Sie **Neues Projekt**in Visual Studio > **Visual C#-** > **Konsolenanwendung** > **OK**.
    
    2. Nachdem die Konsolenanwendung erstellt wurde, wählen Sie **Extras** > **NuGet Package Manager** > **Manage NuGet Packages for Solution...**  >  **Online** > **Alle**.
    
    3. Suche für **App für SharePoint Web Toolkit**.
    
    4. Wählen Sie **Installieren aus**, und wählen Sie dann **OK**.
    
    5. Wählen Sie **Schließen**.
    
    6. Stellen Sie sicher, dass die Konsolenanwendungsprojekt SharePointContext.cs und TokenHelper.cs hinzugefügt wurden.
    
2. Speichern Sie Ihre Kontoinformationen in app.config durch Hinzufügen des **AppSettings** -Elements dargestellt. Ändern Sie **SPOAccount** und **SPOPassword** in den Benutzernamen und das Kennwort des Kontos Organisation an, die Sie zuvor erstellt haben.
    
    ```XML
    <?xml version="1.0" encoding="utf-8" ?>
     <configuration>
      <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
      </startup>
      <appSettings>
        <add key="SPOAccount" value="admin@contoso.onmicrosoft.com"/>
        <add key="SPOPassword" value="Contoso"/>
      </appSettings>
     </configuration>
    ```

    **Vorsicht**  App.config werden Benutzernamen und das Kennwort des Kontos der Organisation in Klartext gespeichert. Diese Methode wird nur zur Veranschaulichung verwendet und sollte nicht in der produktionsbereitstellung von Ihrer WebJobs Azure verwendet werden. Es wird empfohlen, das Kennwort verschlüsseln oder authentifizieren Zugriffstoken mit OAuth. Weitere Informationen finden Sie unter Kirk Evans Blogbeitrag zum [Erstellen eines SharePoint-Add-Ins als einen Zeitgeberauftrag](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx).

## <a name="add-code-to-the-console-application"></a>Fügen Sie Code hinzu, um die Konsolenanwendung
<a name="sectionSection3"> </a>

Fügen Sie den folgenden Code in Program.cs um die Konsolenanwendung.

**Hinweis** Der Code in diesem Artikel wird wie besehen und ohne jegliche Garantie zur Verfügung gestellt, gleich ob ausdrücklich oder konkludent, einschließlich jedweder stillschweigenden Gewährleistung der Eignung für einen bestimmten Zweck, Marktgängigkeit oder Nichtverletzung von Rechten.


1. Fügen Sie **using** -Anweisungen hinzu.
    
    ```C#
    using Microsoft.SharePoint.Client;
    using System.Security;
    using System.Configuration; 
    ```

2. Fügen Sie der Klasse die folgenden Methoden:
    
    -  **Main** meldet sich in Ihrer SharePoint-Website, und klicken Sie dann das CSOM zum Ausführen von Aufgaben auf Ihrer Website oder einer Inhaltsdatenbank verwendet. In diesem Codebeispiel wird das CSOM zum Hier finden eine Liste und die Ausgabe der Gesamtanzahl der Elemente, die in der Liste im Konsolenfenster sind verwendet. Bei Verwendung von Azure WebJobs sehen Sie die Ausgabe im Konsolenfenster WebJob führen Sie nähere Informationen dazu, die in [führen, und überprüfen Sie Ihre Azure WebJob](Use-Microsoft-Azure-WebJobs-with-Office-365.md#runandverify)erläutert wird.
    
  -  **GetSPOSecureStringPassword** liest das Kennwort aus app.config.
    
  -  **GetSPOAccountName** liest Ihren Benutzernamen in app.config.

    ```C#
    static void Main(string[] args)
        {
            using (ClientContext context = new ClientContext("https://contoso.sharepoint.com"))
            {
                // Use default authentication mode.
                context.AuthenticationMode = ClientAuthenticationMode.Default;                 
                context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());
    
                // Add your CSOM code to perform tasks on your sites and content.
    
                try
                {
                    List objList = context.Web.Lists.GetByTitle("Docs");
                    context.Load(objList);
                    context.ExecuteQuery();
    
                    if (objList != null &amp;&amp; objList.ItemCount > 0)
                    {
                        Console.WriteLine(objList.Title.ToString() + " has " + objList.ItemCount + " items.");
                    }
    
                }
                catch (Exception ex)
                {
                    Console.WriteLine("ERROR: " + ex.Message);
                    Console.WriteLine("ERROR: " + ex.Source);
                    Console.WriteLine("ERROR: " + ex.StackTrace);
                    Console.WriteLine("ERROR: " + ex.InnerException);
    
                }
            }
                
        }
    
    private static SecureString GetSPOSecureStringPassword()
    {
      try
      {
          Console.WriteLine("Entered GetSPOSecureStringPassword.");
          var secureString = new SecureString();
          foreach (char c in ConfigurationManager.AppSettings["SPOPassword"])
          {
              secureString.AppendChar(c);
          }
          Console.WriteLine("Constructed the secure password.");
    
          return secureString;
      }
      catch
      {
          throw;
      }
    }
    
    private static string GetSPOAccountName()
    {
      try
      {
          Console.WriteLine("Entered GetSPOAccountName.");
          return ConfigurationManager.AppSettings["SPOAccount"];
      }
      catch
      {
          throw;
      }
    }
    
    ```

## <a name="publish-your-console-application-as-an-azure-webjob"></a>Veröffentlichen Sie die Konsolenanwendung als einem Azure WebJob
<a name="sectionSection4"> </a>

Sie abschließend Konsolenanwendung entwickeln, müssen Sie die Konsolenanwendung als einem Azure WebJob bereitstellen. Zum Bereitstellen der Konsolenanwendung als einem Azure WebJob können Sie folgende Aktionen ausführen:

- Hochladen der Binärdateien zu einer Azure-Web-App, und Erstellen einer Azure WebJob mithilfe des [Microsoft Azure-Verwaltungsportal](https://portal.azure.com/). Die Binärdateien für Visual Studio-Projekt befindet sich im Bin/Debug oder Bin/Release Ordner der Visual Studio-Projekt. Zum Erstellen der Azure-Web-App, und Laden Sie die Binärdateien hoch, führen Sie die Schritte in [Erstellen einer ASP.NET Web-app in Azure App-Dienst](http://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/). So erstellen Sie Ihre auf Anforderung, fortlaufenden oder geplanten Azure WebJob, finden Sie unter [Hintergrund ausführen von Aufgaben mit WebJobs](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).
    
- Veröffentlichen Sie Ihre Azure WebJob von Visual Studio. Weitere Informationen finden Sie unter [Aktivieren WebJobs Bereitstellung ohne ein Webprojekt](http://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#convertnolink).
    
## <a name="run-and-verify-your-azure-webjob"></a>Führen Sie aus und überprüfen Sie Ihre Azure WebJob
<a name="runandverify"> </a>

Klicken Sie nach Abschluss der vorherigen Schritte aus, sollte Ihre WebJob Azure ausgeführt und Aufgaben in Office 365-Abonnements. Unter Umständen müssen Sie zum Ausführen der Wartung oder Problembehandlung Ihrer Azure WebJobs. So überprüfen, dass Ihre WebJob Azure ausgeführt wird:

- Wenn Ihre Azure WebJob ein SharePoint-Element, wie ein Listenelement aktualisiert wird das Feld **Geändert von** der Organisation Konto an, dem die Azure WebJob verwendet, um Zugriff auf SharePoint angezeigt.
    
- Überprüfen Sie die Protokolle WebJob Details für Ihre Azure WebJob. Mit dem WebJob Details Protokolle können Sie überprüfen, wenn ein Auftrag ausgeführt haben, den Erfolg oder Misserfolg eines Auftrags für den führen keine Ausgabe aus der WebJob (beispielsweise beim Aufruf von Console.WriteLine) sowie andere Details des Auftrags ausgeführt. Weitere Informationen finden Sie im Abschnitt Auftragsverlauf anzeigen für [Vorgänge mit WebJobs Hintergrund ausführen](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Office 365 Development Mustern und Methoden ausgesprochen](Office-365-development-patterns-and-practices-solution-guidance.md).
    
-  [Erstellen Sie eine .NET WebJob in Azure App-Dienst](http://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).
    
-  [Azure WebJobs Ressourcen](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/).
