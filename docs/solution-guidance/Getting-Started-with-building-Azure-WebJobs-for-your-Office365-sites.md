---
title: "Erste Schritte mit Azure WebJobs (\"Zeitgeberaufträge\") für Ihre Office 365-Websites #"
ms.date: 11/03/2017
ms.openlocfilehash: 34adf8616224a7f098f336165f120dcb3cde1a6f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="getting-started-with-azure-webjobs-timer-jobs-for-your-office-365-sites"></a>Erste Schritte mit Azure WebJobs ("Zeitgeberaufträge") für Ihre Office 365-Websites #

### <a name="summary"></a>Summary ###
In diesem Beitrag werde ich über wie ein Azure WebJob als ein geplanter Auftrag für Ihre Office 365 verwenden erstellt werden kann (oder Prem, sollten Sie gern) SharePoint-Installation. Mit Office 365 ausführen, wenn Sie und im SharePoint Online-Dienst nutzen, Sie die erneut weiterführen müssen Sie die Aktionen, die verwendet, um *Zeitgeberaufträge* in Ihrer herkömmlichen farmlösungen werden. Führen Sie entlang, während wir die grundlegenden Konzepte von Erste Schritte mit der Erstellung von benutzerdefinierten Aufträge für Office 365-Websites durchlaufen.

# <a name="introduction-to-azure-webjob-as-a-timer-job-for-your-office-365-sites"></a>Einführung in Azure WebJob als einen Zeitgeberauftrag für die Office 365-Websites #
In herkömmlichen SharePoint-Entwicklung haben wir [Zeitgeberaufträge](http://tz.nu/1DNtqH8), die in der SharePoint-Farmen geplante Aufgaben ausgeführt werden. Eine häufig verwendete Methode ist zum Entwickeln von benutzerdefinierten Zeitgeberaufträge, um kontinuierlich oder iterativ in Ihrer Umgebung bestimmte Aufgaben ausführen.

Mit Office 365 und SharePoint Online müssen Sie nicht entscheidender Vorteil, Bereitstellen von farmlösungen ist, auf dem die herkömmlichen Zeitgeberaufträge normalerweise live. Stattdessen wir haben, erhalten eine andere Möglichkeit zum Planen von unseren Tasks – Dies führt zu dem Konzept einer [Azure WebJob](http://tz.nu/1ueFvMZ).

## <a name="steps-for-building-the-webjob-using-visual-studio-2015-preview"></a>Schritte zum Erstellen von der WebJob mithilfe von Visual Studio 2015 (Preview)  ##
Um eine neue WebJob von Grund auf zu erstellen, müssen wir, nur erstellen eine neue Konsolenanwendung, und stellen Sie sicher, dass wir die erforderlichen Assemblys zum Projekt hinzufügen. In diesem Beispiel wird [Visual Studio 2015 (Preview)](http://tz.nu/1CagngX)verwendet, wie der Name schon sagt derzeit eine Beta-Version ist.

### <a name="step-1-create-your-console-application"></a>Schritt 1: Erstellen der Konsolenanwendung ###
Starten Sie, indem Sie ein neues Projekt erstellen, und stellen Sie sicher, dass Sie die Vorlage "**Console Application**" ausgewählt haben. Darüber hinaus und dies ist wichtig, stellen Sie sicher, dass Sie **.NET Framework 4.5**gewählten!

![Das Dialogfeld Neues Projekt, so erstellen Sie eine Konsolenanwendung, die mit den Punkt festgelegt net Framework 4.5](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/1.Create-Console-Application.png)

### <a name="step-2-add-the-sharepoint-specific-assemblies-from-nuget"></a>Schritt 2: Hinzufügen der SharePoint-spezifische Assemblys aus NuGet ###
Wenn Sie Visual Studio 2015 wie ich mache verwenden, sieht das NuGet-Paket-Manager-Dialogfeld geringfügig von früheren Versionen von Visual Studio, aber das Konzept des identisch.

 - Wechseln Sie zu**"Extras**"->"**NuGet-Paket-Manager**-">"**Verwalten von NuGet-Pakete für Lösung..."**
 - Suchen Sie nach "**App für SharePoint**"
 - Installieren Sie das Paket "**AppForSharePointWebToolkit**" dem installieren die erforderlichen Hilfsklassen für die Arbeit mit dem SharePoint-Clientobjektmodells aufgerufen.

![Die NuGet Package Manager-Dialogfeld mit den Suchbegriff App für SharePoint. App für SharePoint Web Toolkit wird hervorgehoben, und die Schaltfläche "installieren" geklickt werden kann.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/2.Add-App-For-SharePoint-Web-Toolkit-from-Nuget.png)
Stellen Sie sicher, dass das NuGet-Paket erfolgreich war, indem Sie sicherstellen, dass diese beiden neuen Klassen in Ihrer Konsolenanwendungsprojekt vorhanden ist: ![der Projektmappen-Explorer zeigt die neu hinzugefügten Klassen Share Point Kontext und Hilfsprogramm-Token.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/3.Project-Overview-With-Added-Files.png)

### <a name="step-3-add-the-required-code-to-execute-the-job-on-your-office-365-site"></a>Schritt 3: Hinzufügen des erforderlichen Codes zum Ausführen des Auftrags auf Ihrer Office 365-Website ###
An dieser Stelle haben wir unsere Konsolenanwendung erstellt, und wir haben die erforderlichen Assemblys, die für uns zur Kommunikation mit SharePoint vereinfachen werden hinzugefügt. Nächste Schritte stellen sind der Hilfsklassen, um das Ausführen von Befehlen im unseren SharePoint-Umgebung über unsere Console Application verwenden. Markieren Sie entlang.

***Hinweis:*** In diesem Beispiel nach Abschluss des Vorgangs ich werde verwenden ein Konto + Kennwort Ansatz (wie ein Dienstkonto). Authentifizierung erläutert Optionen weiter unten im Artikel und Links zu anderen alternativen Auschecken.

#### <a name="wire-up-the-calls-to-the-sharepoint-online-site-collection"></a>Definieren der Anrufe für die SharePoint Online-Websitesammlung ####

Der folgende Code veranschaulicht den Anruf an Ihre Website leicht verbinden kann, nun, da wir die Hilfsklassen aus unseren NuGet-Paket hinzugefügt haben.

```C#
 static void Main(string[] args)
  {
      using (ClientContext context = new ClientContext("https://redacted.sharepoint.com"))
      {
          // Use default authentication mode
          context.AuthenticationMode = ClientAuthenticationMode.Default;
          // Specify the credentials for the account that will execute the request
          context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());

          // TODO: Add your logic here!
      }
  }
 
 
  private static SecureString GetSPOSecureStringPassword()
  {
      try
      {
          Console.WriteLine(" --> Entered GetSPOSecureStringPassword()");
          var secureString = new SecureString();
          foreach (char c in ConfigurationManager.AppSettings["SPOPassword"])
          {
              secureString.AppendChar(c);
          }
          Console.WriteLine(" --> Constructed the secure password");
 
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
          Console.WriteLine(" --> Entered GetSPOAccountName()");
          return ConfigurationManager.AppSettings["SPOAccount"];
      }
      catch
      {
          throw;
      }
   }
``` 

In der beispielanwendung finden Sie, dass ich zwei Hilfsmethoden für das Abrufen von den Kontonamen und das Kennwort des Kontos aus der App.config.Datei hinzugefügt haben. Diese werden im Abschnitt Authentifizierung erläutert weiter unten in diesem Artikel.

Wie bei der main-Methode ist, müssen wir nur Dinge bis zu unserem Portal verbinden. Bevor wir tiefer wie wir SharePoint in unseren Code bearbeiten können untersuchen, Erläuterung der Optionen für die Authentifizierung.

## <a name="authentication-considerations"></a>Überlegungen zur Authentifizierung ##
Wir sehen Sie sich zwei Optionen für die Authentifizierung und finden Sie, wie sie sich unterscheiden. Weitere Optionen für die Authentifizierung in der Zukunft möglicherweise, aber hier sind zwei Ansätze häufig verwendete.

### <a name="option-1-use-a-service-account-username--password"></a>Option 1: Verwenden eines Dienstkontos (Username + Kennwort) ###
Dieser Ansatz ist relativ einfach und ermöglicht es Ihnen, geben Sie einfach ein Konto und Kennwort Ihrem Office 365-Mandanten und verwenden Sie beispielsweise CSOM zum Ausführen von Code für Ihre Websites. Dies ist, was Sie auch in meinem Beispielcode oben angezeigt.

#### <a name="create-a-new-service-account-in-office-365"></a>Erstellen eines neuen Dienstkontos in Office 365 ####
In der Reihenfolge zu diesem Zweck sollte ein bestimmtes Konto erstellt werden, die fungiert als Dienstkonto – entweder für dieses bestimmte Anwendung oder eine generische dienstanwendungskonto, die alle Aufträge und Dienste verwenden können.

Aus Gründen der in dieser Demo habe ich ein neues Konto namens "**SP WebJob**" erstellt: ![das Dashboard zeigt das neu erstellte SP WebJob Konto.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/4.Service-Account-Overview.png)

Je nach den Auftrag auf welche Berechtigungen sollten haben, müssen Sie die Berechtigungen des Benutzerkontos bearbeiten, beim Einrichten von.

#### <a name="store-credentials-in-your-appconfig"></a>Speichern von Anmeldeinformationen in der Datei app.config ####
Innerhalb des Projekts ' App.config ' Datei können Sie die Anmeldeinformationen angeben, damit sie auf einfache Weise fetchable aus dem ausführbaren Code sind. Dies ist mein app.config aussieht:
```XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
 <startup> 
   <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
 </startup>
 <appSettings>
   <add key="SPOAccount" value="spwebjob@redacted.onmicrosoft.com"/>
   <add key="SPOPassword" value="redacted"/>
 </appSettings>
</configuration>

```
Sie können die zwei Einstellungen in App.config finden Sie unter:

 - SPOAccount
 - SPOPassword

Wenn Sie den ersten Codeausschnitt überprüfen, erhalte ich diese Einstellungen aus der App.config.Datei abgerufen. Beachten Sie, dass das Speichern von den Kontonamen und das Kennwort in Klartext in der Datei app.config bedeutet halten. Sie müssen Treffen einer Entscheidung in eigene Projekte dafür, wie und wo Sie gespeichert und schützen Sie Ihre Kennwörter sollten Sie diesen Ansatz wählen.

#### <a name="the-job-runs-under-the-specified-account"></a>Der Auftrag wird unter dem angegebenen Konto ausgeführt. ####
Sobald die Anwendung ausgeführt wird, sehen Sie, dass er ausgeführt wird, mit dem Konto im Konstruktor SharePointOnlineCredentials() angegeben:

![Automatische Konvertierung Protokoll zeigt vier Text Übersetzungen SP WebJob zugeordnet.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/5.Running-Job-Overview.png)

In diesem Beispiel oben bin ich eine WebJob angezeigt, die auf eine benutzerdefinierte Liste in einem der "Meine Websites" in meiner SharePoint Online-Websitesammlung gehostet Aktionen ausgeführt wird.

Aus diesem Grund erhalten wir einen guten zurückverfolgt werden Änderungen können im Portal unsere Dienstkonto ausgeführt. Hierbei handelt es sich deshalb Achten Sie darauf, nennen Sie das Konto mit Bedacht – jeder kennt, dass die Änderungen automatisch von unseren Dienst durchgeführt wurden, indem Sie einfach auf die Metadaten geändert/erstellt.

### <a name="option-2-use-oauth-and-include-authentication-tokens-in-your-requests-to-avoid-specifying-accountpassword"></a>Option 2: Verwendung OAuth und enthalten Authentifizierungstoken in Ihre Anforderungen zu vermeiden, Konto und Kennwort angeben ###
Dies wurde durch schätze [Kirk Evans](http://blogs.msdn.com/b/kaevans/) bei Microsoft ausführlich erläutert.

In seinem buchen gewählte "[Erstellen eines SharePoint-Add-Ins als einen Zeitgeberauftrag](http://tz.nu/1xBA76K)" erläutert er das können Sie nutzen und Durchlauf entlang des Zugriffs für das Token, um zu vermeiden und Kennwort Setupprogrammen wie bereits erwähnt, falls Sie nicht die Kennwörter speichern möchten und Anmeldeinformationen in die Anwendung.

## <a name="extending-the-code-with-some-csom-magic"></a>Erweitern Sie den Code mit einigen magischen CSOM ##
An dieser Stelle haben wir eine funktionsfähige Console Application authentifizieren und Anforderungen an den Office 365-Websites ausführen kann. Nicht besonders interessant ausgeführt wurde im Code noch, sodass hier ist ein Beispiel-Ausschnitt, Abrufen von Informationen aus einer Liste bezeichnet "Automatische Übersetzungen", die ich erstellt haben, und die Codelogik wird angezeigt, wenn alle Elemente in der Liste, die übersetzt wurde noch nicht vorhanden ist und dann Es werden führen Sie einen Anruf an einen Übersetzungsdienst und den Text, der die gewünschte Ausgabe Sprache übersetzen.
```C#
static void Main(string[] args)
{
   try
   {
      Console.WriteLine("Initiating Main()");

      using (ClientContext context = new ClientContext("https://redacted.sharepoint.com"))
      {
         Console.WriteLine("New ClientContext('https://redacted.sharepoint.com') opened. ");

         context.AuthenticationMode = ClientAuthenticationMode.Default;
         context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());

         Console.WriteLine("Authentication Mode and Credentials configured");

         List translationlist = context.Web.Lists.GetByTitle("Automatic Translations");
         context.Load(translationlist);
         context.ExecuteQuery();

         Console.WriteLine("TranslationList fetched, loaded and ExecuteQuery'ed");

         if (translationlist != null && translationlist.ItemCount > 0)
         {
             Console.WriteLine("The list exist, let's do some magic");

             CamlQuery camlQuery = new CamlQuery();
             camlQuery.ViewXml =
             @"<View>  
             <Query> 
                 <Where><Eq><FieldRef Name='IsTranslated' /><Value Type='Boolean'>0</Value></Eq></Where> 
             </Query> 
         </View>";

             ListItemCollection listItems = translationlist.GetItems(camlQuery);
             context.Load(listItems);
             context.ExecuteQuery();

             Console.WriteLine("Query for listItems executed.");

             foreach (ListItem item in listItems)
             {
                 item["Output"] = TranslatorHelper.GetTranslation(item["Title"], item["Target Language"], item["Original Language"]);
                 item["IsTranslated"] = true;
                 item.Update();
             }


             context.ExecuteQuery();
             Console.WriteLine("Updated all the list items we found. Carry on...");
         }
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

```
Die **TranslatorHelper** -Klasse ist eine Hilfsklasse, die eine benutzerdefinierte Übersetzung API ruft aber es nicht erläutert ausführlich in diesem Beitrag, da es sehr weit außerhalb des Bereichs ist.

**Hinweis:** *Ressourcenverfügbarkeitsdaten aus dem Code Dies ist eine Demo definitiv nicht für die Verwendung in der Produktion, überprüfen sie und passen Sie entsprechend Ihrer codieren Standards und Sicherheitsprinzipien. Jedoch alle Console.WriteLine Ergänzungen für uns, überprüfen Sie die Ausführung der Aufträge auf einfache Weise über das Portal Azure hinzugefügt werden. Klicken Sie auf Protokollierung und Überwachung weiteren unten in diesem Artikel weitere.*

## <a name="publishing-your-webjob-to-azure"></a>Veröffentlichen Sie Ihre WebJob in Azure ##
Wenn Sie Ihre WebJob entwickelt haben, und Sie können sie auf der Azure-Umgebung bereitstellen (an eine Azure-WebSite bereitgestellt), können Sie zwei grundlegende Optionen wie unten beschrieben.

### <a name="option-1-upload-a-zip-file-with-the-webjob-binaries-to-your-azure-portal"></a>Option 1: Hochladen einer Zip-Datei mit den WebJob Binärdateien in der Azure-Verwaltungsportal ###
Verwenden der Azure-Verwaltungsportal, in dem Sie alle Ihre Awesomeness in Azure aufbewahren, können Sie eine Zip-Datei, enthält die Ausgabe aus Visual Studio Build hochladen. Dies ist eine einfache Möglichkeit zum Kompilieren und Versand von Ihrem Code an eine andere Person, die die Bereitstellung für Sie ausgeführt wird.

#### <a name="create-the-zip-file"></a>Erstellen Sie die Zipdatei ####
Einfach abgerufen Sie werden, der die Ausgabedateien aus Ihrem Visual Studio (normalerweise im Ordner Bin/Debug oder Bin-Version) zu erstellen:

![Eine Windows Explorer-Ansicht Bin/Debug-Ordner wird angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/6.Zip-File-Overview.png)
Komprimieren Sie, damit eine gute Zip-Datei für Ihre Arbeit Web Sie erzielen:

![Windows Explorer-Ansicht einer abgeschlossenen ZIP-Datei wird angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/7.Zip-File-Created.png)

#### <a name="find-a-web-site-where-the-job-should-be-deployed"></a>Suchen nach einer Website, in dem der Auftrag bereitgestellt werden ####

Gut, damit Sie Ihr Paket haben. Das ist einfach. Nächste Schritt besteht darin, gleich https://portal.azure.com und melden Sie sich Ihre Windows Azure-Verwaltungsportal. Sie müssen entweder eine neue Website erstellen, oder verwenden Sie eine vorhandene – dieser Website werden den Host für unsere Webauftrag, von dort aus.

In unserem Fall habe ich bereits eine Azure-WebSite für einige der Demos für meine Office 365 damit ich, dass eine gerade verwenden werden.

Wenn Sie unten im Einstellungsbereich für Ihre Website navigieren, finden Sie eine etwas "**WebJobs**" unter der Kopfzeile "**Vorgänge**" aufgerufen:

![Des Autors Azure-Verwaltungsportal wird angezeigt, mit einem Pfeil auf WebJobs zeigen. ](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/8.Find-WebJobs-in-Azure-Portal.png)
 **Klicken, auf dem der Pfeil zeigt!**

#### <a name="upload-your-webjob"></a>Hochladen der WebJob ####

Hochladen der Webauftrag durch Klicken auf das Zeichen **[+ hinzufügen]** :

![Die WebJobs Azure-Verwaltungsportal wird angezeigt, mit einem Pfeil auf Hinzufügen.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/9.Upload-Azure-WebJob-from-Azure-Portal.png)

Wählen Sie einen Namen, wie der Auftrag ausgeführt werden soll und die tatsächlichen Zip-Datei:

![Das Dialogfeld WebJob hinzufügen wird angezeigt. Das Feld Name den Text Zimmergren-O365-WebJobSample enthält und How to Run Feld enthält den Text On Demand.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/10.Configure-Name-of-Uploaded-WebJob.png)

***Wichtig:*** Die Alternative "Wie zur Ausführung" nur bietet "On Demand" oder "Fortlaufend" zu diesem Zeitpunkt, aber bald vorhanden sein Support für "Geplant" sowie – das ist wirklich möchten.

*(Hinweis: im nächsten Abschnitt für die Veröffentlichung direkt von Azure, Planen Sie es aus in VS).*

Okay, können geschieht – Sie nun Ihre Webjob aus der Azure-Verwaltungsportal ausführen:

![Die WebJobs Azure-Verwaltungsportal wird mit der neuen Liste angezeigt. Ein Kontextmenü wird über den Auftrag mit den Optionen ausführen und löschen.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/11.Run-WebJob-from-Azure-Portal.png)

Dies ist zwar schön und Sicherheitsdeskriptor, da das Portal verfügt nicht über die Dialogfelder für die Unterstützung der Planung noch – ich würden Sie Informationen zum Veröffentlichen von auszuchecken intensiv über in Visual Studio 2015 stattdessen (oder 2013, wenn das Ihrer Wahl ist).

### <a name="option-2-publish-directly-to-azure-from-visual-studio"></a>Option 2: Veröffentlichen Sie direkt in Azure von Visual Studio ###
Dies ist meine bevorzugten zu diesem Zeitpunkt, da ich die Tools in Visual Studio verwenden können, um alle Änderungen direkt mit einem gehosteten Dienst schnell veröffentlichen. Ein weiterer Vorteil werden deaktivieren bald, wie Sie auch den Auftrag planen können, genau wie Sie direkt in den Dialogfeldern in Visual Studio ausführen soll.

#### <a name="choose-to-publish-the-webjob-from-visual-studio-2015"></a>Wählen Sie die WebJob von Visual Studio 2015 veröffentlichen ####

***Hinweis:*** *Diese Dialogfelder abweichen etwas, wenn Sie eine frühere Version von Visual Studio ausführen. Darüber hinaus habe ich bereits angemeldet, wenn Sie dies zum ersten Mal tun ein Anmeldedialogfeld abrufen kann, um Azure-Konto anmelden. Dies ist eine Voraussetzung.*

Klicken Sie einfach mit der rechten Maustaste in des Projekts, und wählen Sie "**Veröffentlichen als einem Azure WebJob...**":

![Im Kontextmenü Projektmappen-Explorer wird angezeigt, mit der veröffentlichen als Azure WebJob Option hervorgehoben.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/12.Publish-WebJob-from-Visual-Studio-2015.png)

#### <a name="add-azure-webjob"></a>Hinzufügen von Azure WebJob ####
Dadurch gelangen Sie zu einer neuen Dialogfeld, in denen können Sie den Auftrag konfigurieren, und da wir ein wiederkehrendes Projekt soll, die nach einem Zeitplan (in meinem Fall einmal für jeden Abend) ausgeführt wird, können Sie den Zeitplan direkt in den Dialogfeldern konfigurieren: ![das Hinzufügen von Azure WebJob Dialogfeld Benachrichtigung wird ayed. Das Namensfeld WebJob enthält den Text Zimmergren-O365-WebJobSample, Feld Modus ausführen WebJob enthält die Option nach einem Zeitplan ausführen, serienfelds enthält den Option periodisch Auftrag und das Kontrollkästchen kein Enddatum wird überprüft, die als Serie festlegen jedes Feld auf 1 gesetzt ist Tage , und die starten Datum 9 Januari 2015 ist.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/13.Add-Azure-WebJob-Dialog.png)

 - Stellen Sie sicher, dass der Name angezeigten Web ist
 - Wählen Sie Ihre Ausführmodus, ich bin "Auf einen Zeitplan", da es in einem bestimmten Zeitpunkt täglich kommen haben sollen
 - Der Auftrag ein wiederkehrendes Projekt oder einen einmaligen Auftrag sein sollte? Da wir möchten, können Sie einen Zeitgeberauftrag das wiederholt werden, muss in meinem Fall ohne jedes Enddatum, da es immer nachts ausgeführt werden kann
 - Sie können die Serie nach unten zu einer Minute, planen möchten, sollten.
 - Wenn starte wir? :-)

Trefferposition **OK** und Sie sehen, dass Sie Visual Studio eine Meldung "**Installieren von WebJobs Publishing NuGet-Paket**" ablegen.

#### <a name="visual-studio-added-webjobs-publishing-nuget-package"></a>Visual Studio hinzugefügt WebJobs Publishing NuGet-Paket ####
![Klicken Sie im Dialogfeld WebJobs NuGet-Paket zu installieren wird angezeigt, der ein Drehfeld und der Text, Installieren von WebJobs Publishing NuGet-Paket angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/14.WebJobs-NuGet-Package-Install.png)

Dadurch wird eine neue Datei mit dem Namen "**Webjob veröffentlichen settings.json**", um unseren Projekt, mit der Konfiguration für den Auftrag tatsächlich hinzugefügt.

Die Datei sieht folgendermaßen aus:
```json
{
  "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
  "webJobName": "Zimmergren-O365-WebJobSample",
  "startTime": "2015-01-09T01:00:00+01:00",
  "endTime": null,
  "jobRecurrenceFrequency": "Day",
  "interval": 1,
  "runMode": "Scheduled"
}
```
Rechts, müssen wir nicht mit dieser Datei gegenwärtig Mühe, da es bereits konzipiert, die Planung in Dialogfeldern.

#### <a name="select-publishingdeployment-target"></a>Wählen Sie Ziel Veröffentlichung-Bereitstellung ####
Im nächste Schritt im Dialogfeld werden, wo Sie veröffentlichen/Bereitstellen Ihrer WebJob. Sie können ein Veröffentlichungsprofil importieren oder Microsoft Azure-WebSites, um zu authentifizieren, und wählen Sie eine vorhandene Websites aktivieren.

Seit ich eine auch immer Meine Veröffentlichungsprofile von Meine Azure-Verwaltungsportal heruntergeladen haben, ich fahren Sie fort, und wählen Sie "**Import**" und geben Sie einfach die Veröffentlichung Profildatei, die ich meine Azure-Website heruntergeladen haben:

![Klicken Sie im Dialogfeld Web veröffentlichen wird mit der Registerkarte Verbindung sichtbar angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/15.Publish-Web-Dialog.png)

Anschließend müssen wir nur auf die Schaltfläche "Veröffentlichen" klicken. Keine Angst, es nicht kompakten. Ich denke.

#### <a name="publish"></a>Veröffentlichen ####
Nachdem Sie veröffentlichen treffen, wird das Dialogfeld "Web veröffentlichen Aktivität" den Fortschritt der Bereitstellung Webauftrag angezeigt: ![im Dialogfeld Web veröffentlichen Aktivität wird angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/16.Publish-Progress-Visual-Studio-2015.png)

Nachdem es erfolgt ist, sollte die WebJob in der Azure-Verwaltungsportal angezeigt: ![der Azure-Verwaltungsportal zeigt Zimmergren-O365-WebJobSample in der Liste der WebJobs mit dem Status abgeschlossen 2 Minuten vor.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/17.Web-Job-Published-as-seen-in-Azure-Portal.png)

Der Status WebJob wird nun als abgeschlossen angezeigt. Sie würden Fehler/sagen, wenn er nicht behandelten Ausnahmen auslösen oder anderweitig zur Verfügung fehlerhaft Verhalten stellen würde.

Er tut weiterhin "On Demand", aber dieser Auftrag wird stündlich jetzt tatsächlich ausgeführt.

## <a name="monitoring-the-job-and-reviewing-logs"></a>Überwachung des Auftrags und Protokolle überprüfen ##
Wenn Sie die oben beschriebenen Schritte durchgeführt haben, haben Sie einen Auftrag für Sie als geplante Aufgabe in der Cloud arbeiten Ausführen von Aktionen in Richtung der Office 365-Sites.

### <a name="view-all-job-executions-and-status"></a>Zeigen Sie aller Auftrag Ausführungen und Status an ###
Wenn Sie überprüfen, wenn der Auftrag letzten Ausführung was das Ergebnis der jeder Ausführung des Auftrags war oder während der Ausführung des Auftrags für Änderungen überprüfen möchten, Sie können klicken Sie auf den Link unter "Protokolle" klicken Sie in der Übersicht über die WebJobs Vorgangs: ![der WebJobs-Dialogfeld , mit einem Pfeil auf den Link "Upgradeprotokolle" zeigen.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/18.View-All-WebJobs-and-status-of-execution.png)

Dadurch erhalten Sie eine Übersicht über alle Ausführungen der ausgewählten Aufträge, einschließlich der /outcome Status:

![Die WebJob Details, einschließlich der letzte Auftrag ausgeführt wird.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/19.WebJob-Details-Overview.png)

Auf den hervorgehobenen Link klicken, können Sie nach unten Architekturprinzipien eine bestimmte Ausführung zum Überprüfen der Protokolle des Auftrags und stellen Sie sicher, dass Dinge kein Problem. Dies ist wahrscheinlich mehr relevant, wenn der Auftrag tatsächlich einen Fehler verursacht, und Sie benötigen, Fehlerursache untersuchen, wenn das Ergebnis des Auftrags falsch ist oder nicht wie erwartet.

Sie können auch sehen, dass die Console.WriteLine-Anweisungen, die ich so gut in Meine Console Application für diese Demo jetzt verwendet wird im Protokoll Ausführung Auftrag:

![Die WebJob-Details die Zeilen in der Protokolldatei angezeigt.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/20.Review-Logs-and-Monitor-WebJob-Execution.png)

## <a name="tips--tricks"></a>Tipps und Tricks ##
Alle mit früheren Versionen von Visual Studio ausgeführt werden können, habe ich alles mit Visual Studio 2015 arbeiten. Aber dabei, die es einige Punkte wurden, ich bin Hinzufügen dieser hier für den Fall, dass Sie in das gleiche umbricht.

### <a name="exit-code--2146232576-problem-when-running-the-job"></a>Exit Code-2146232576 Problem bei der Ausführung des Auftrags ###
Seit dem Start eines Projekts Visual Studio 2015 (Preview) Serverstart es das Projekt als eine Konsolenanwendung, die auf **.NET Framework 4.5.3**basiert.

Ausführen des Auftrags lokal funktioniert, da .NET Framework 4.5.3 auf meinem Computer Dev vorhanden sind. Wenn ich den Auftrag zur eigene Windows Azure-Website als eine WebJob bereitgestellt, ist fehlgeschlagen, es mit "**Code-2146232576 beenden**".

#### <a name="solution-make-sure-youre-on-the-correct-net-version"></a>Lösung: Stellen Sie sicher, dass Sie die richtige Version .NET sind ####
Eine Weile gedauert hat, bevor ich, wenn ich in **.NET Framework 4.5**geändert, funktioniert aber nicht Azure .NET Framework, Version 4.5.3 gefallen realisiert.

Sie in das Problem umbricht, stellen Sie nur sicher, dass Ihre Arbeit unter die richtige .NET Framework-Version ausgeführt wird.
![Zeigt die Eigenschaften von Visual Studio-Projekt-Seite, Registerkarte Anwendung, mit der Ziel-Framework-Dropdown-, Hervorheben Punkt NET Framework 4.5.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/21.Change-NET-Framework-In-Visual-Studio-2015.png)

# <a name="summary"></a>Summary #
Es ist, zwar nicht sehr viel bis hin zum Erstellen einer Azure WebJob können Sie sie sehr komplex haben. Das allgemeine Konzept sehr gerade vorwärts ist jedoch klicken Sie dann als alle komplexe Projekte im Lieferumfang der Entscheidungen um Authentifizierung, Code Stabilität und Zuverlässigkeit, hohe Verfügbarkeit Szenarien, Wartungsfreundlichkeit und so weiter. Diese Variablen für jedes Projekt eindeutig sind und vor dem "nur Bereitstellen von" sorgfältig geplant werden sollte einen Auftrag zum Azure.

### <a name="related-links"></a>Verwandte links ###
-  [Ursprüngliche Blogbeitrag auf Azure WebJobs](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites) , indem Sie Tobias Zimmergren
-  [Empfohlene Ressourcen für Azure WebJobs](http://azure.microsoft.com/en-us/documentation/articles/websites-webjobs-resources/)
-  [Visual Studio 2015 (Preview) herunterladen](http://www.visualstudio.com/en-us/downloads/visual-studio-2015-downloads-vs.aspx)
-  [Erstellen einer SharePoint-Add-Ins als einen Zeitgeberauftrag](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx) , indem Kirk Evans
-  [Zum Bereitstellen von Azure WebJobs zu Azure-Websites:](http://azure.microsoft.com/en-us/documentation/articles/websites-dotnet-deploy-webjobs/)
-  [Einfache remote Zeitgeberauftrag, die Interaktion mit SharePoint Online,](http://channel9.msdn.com/Blogs/Office-365-Dev/Simple-remote-timer-job-that-interacts-with-SharePoint-Online-Office-365-Developer-Patterns-and-Prac) von Andrew Connell auf Channel 9

### <a name="applies-to"></a>Gilt für ###
-  Office 365 mit mehreren Mandanten (MT)
-  Office 365 dedizierte (D)
-  SharePoint 2013 lokal 
