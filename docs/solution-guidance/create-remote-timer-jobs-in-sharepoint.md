---
title: "Erstellen Sie remote Zeitgeberaufträge in SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 12f4abd507328afd19da562c8dbb569118bc91a9
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="create-remote-timer-jobs-in-sharepoint"></a>Erstellen Sie remote Zeitgeberaufträge in SharePoint

Erstellen Sie remote Zeitgeberaufträge in SharePoint Hintergrund Aufgaben zum Verwalten von oder Ihrer Umgebung steuern.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Erstellen Sie remote Zeitgeberaufträge zum Verwalten von SharePoint durch Überwachung und Aktion zu SharePoint-Daten. Remote Zeitgeberaufträge auf dem SharePoint-Server nicht ausgeführt werden. Stattdessen werden remote Zeitgeberaufträge geplante Vorgänge, die auf einem anderen Server ausgeführt. Beispiele dafür, wie Zeitgeberaufträge verwendet werden können:

- Governance Aufgaben wie auf der Website eine Meldung angezeigt, wenn bestimmte Kriterien nicht erfüllt sind, oder erzwingen Aufbewahrungsrichtlinien ausführen.
    
- Ausgeführt geplanten Prozesse, die intensive Prozessor sind.

## <a name="before-you-begin-to-create-a-remote-timer-job"></a>Bevor Sie beginnen, erstellen Sie einen remote-Zeitgeberauftrag

Laden Sie Sie zuerst [Core.TimerJobs.Samples](https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

Vor der Verwendung der Lösung Core.TimerJobs.Samples, müssen Sie ein Startprojekt, beispielsweise das SimpleJob Projekt auswählen von öffnen das Kontextmenü (Rechtsklick) das **Core.TimerJobs.Samples.SimpleJob**auswählen und dann **festgelegt als Startprojekt**.

**Hinweis:**  Bei der Erstellung eines neuen Projekts in Visual Studio zum Erstellen des neuen remote-Zeitgeberauftrags, das **OfficeDevPnP.Core** NuGet-Paket dem Projekt hinzugefügt. Wählen Sie in Visual Studio **TOOLS** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**.

## <a name="schedule-your-remote-timer-job"></a>Planen des remote-Zeitgeberauftrags

Ein Zeitgeberauftrag einmal ausführen geplant werden kann oder ein wiederkehrendes Projekt handeln. Planen des remote-Zeitgeberauftrags in Ihrer produktionsumgebung, müssen Sie zum Kompilieren des Codes in einer .exe-Datei, und führen Sie die .exe-Datei mithilfe von Windows-Taskplaner oder eine Microsoft Azure WebJob. Erfahren Sie unter [Timer Job-Bereitstellungsoptionen](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#timer-job-deployment-options).

## <a name="use-the-coretimerjobssamplessimplejob-add-in"></a>Verwenden des Core.TimerJobs.Samples.SimpleJob-add-Ins

In Core.TimerJobs.Samples.SimpleJob führt **Main** in Program.cs die folgenden Schritte aus:

1. Erstellt ein SimpleJob-Objekt, das von der Basisklasse [OfficeDevPnP.Core.Framework.TimerJobs.TimerJob](https://github.com/SharePoint/PnP/blob/dev/OfficeDevPnP.Core/OfficeDevPnP.Core/Framework/TimerJobs/TimerJob.cs) erbt.
    
2. Legt die Anmeldeinformationen des Office 365-Benutzer zu verwenden, wenn den Zeitgeberauftrag mit **TimerJob.UseOffice365Authentication**ausführen. Die Anmeldeinformationen des Benutzers benötigen Zugriff auf die Websitesammlungen. Erfahren Sie unter [Authentifizierung](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#authentication).
    
3. Fügt die Websites, die der Zeitgeberauftrag zur Verwendung von **TimerJob.AddSite**Aufgaben auszuführen. Optional können Sie wiederholen Sie die **TimerJob.AddSite** -Anweisung, um mehr als einen Standort hinzuzufügen, oder fügen alle Websites unter einer bestimmten URL mithilfe von Platzhalterzeichen *. Beispielsweise http://contoso.sharepoint.com/sites/* wird auf alle Websites unter der verwaltete **Sites** -Pfad den Zeitgeberauftrag ausgeführt.
    
4. Druckt Timer-Job-Informationen und führt den Zeitgeberauftrag mithilfe von **PrintJobSettingsAndRunJob**.

**Hinweis:**  Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
 static void Main(string[] args)
        {
            SimpleJob simpleJob = new SimpleJob();
            
            // The user credentials must have access to the site collections you supply.
            simpleJob.UseOffice365Authentication(User, Password);

            // Use the following code if you are using SharePoint Server 2013 on-premises. 
            //simpleJob.UseNetworkCredentialsAuthentication(User, Password, Domain);
            
            // Add one or more sites that the timer job should work with.
            simpleJob.AddSite("https://contoso.sharepoint.com/sites/dev");
            
            // Prints timer job information and then calls Run().
            PrintJobSettingsAndRunJob(simpleJob);
        }
```

Wenn das **SimpleJob** -Objekt instanziiert wird, den Konstruktor **SimpleJob** :

1. Ruft den allgemeinen Basisklassenkonstruktor. 
    
2. Weist den **SimpleJob_TimerJobRun** -Ereignishandler die **TimerJobRun** Ereignisse behandeln. **SimpleJob_TimerJobRun** ausgeführt, wenn ein Aufruf **TimerJob.Run**, erfolgt die weiter unten in diesem Artikel ausführlich beschrieben wird.

```C#
public SimpleJob() : base("SimpleJob")
        {
            TimerJobRun += SimpleJob_TimerJobRun;
        }
```

Wenn **PrintJobSettingsAndRunJob** ausgeführt wird, wird die Ausgabe aus der allgemeinen im Konsolenfenster geschrieben, und klicken Sie dann **TimerJob.Run** aufgerufen.

```C#
 private static void PrintJobSettingsAndRunJob(TimerJob job)
        {
            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("************************************************");
            Console.WriteLine("Job name: {0}", job.Name);
            Console.WriteLine("Job version: {0}", job.Version);
            Console.WriteLine("Use threading: {0}", job.UseThreading);
            Console.WriteLine("Maximum threads: {0}", job.MaximumThreads);
            Console.WriteLine("Expand sub sites: {0}", job.ExpandSubSites);
            Console.WriteLine("Authentication type: {0}", job.AuthenticationType);
            Console.WriteLine("Manage state: {0}", job.ManageState);
            Console.WriteLine("SharePoint version: {0}", job.SharePointVersion);
            Console.WriteLine("************************************************");
            Console.ForegroundColor = ConsoleColor.Gray;

            // Run job.
            job.Run();
        }
```

**TimerJob.Run** löst **TimerJobRun** Ereignisse. **TimerJob.Run** ruft **SimpleJob_TimerJobRun** in SimpleJob.cs, der zum Verarbeiten von Ereignissen in den Konstruktor **SimpleJob** **TimerJobRun** als Ereignishandler festgelegt. In **SimpleJob_TimerJobRun**können Sie den benutzerdefinierten Code hinzufügen, den des Zeitgeberauftrags ausführen, wenn der Zeitgeberauftrag ausgeführt werden soll. **SimpleJob_TimerJobRun** führt den benutzerdefinierten Code auf die Websites, die Sie hinzugefügt haben, verwenden **TimerJob.AddSite** in Program.cs. In diesem Codebeispiel wird mit **SimpleJob_TimerJobRun** der **ClientContext** aus der **allgemeinen** den Titel der Website im Konsolenfenster geschrieben. Wenn mehrere Websites mithilfe von **TimerJob.AddSite** hinzugefügt wurden, wird die **SimpleJob_TimerJobRun** für jede Website aufgerufen.

```C#
 void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            e.WebClientContext.Load(e.WebClientContext.Web, p => p.Title);
            e.WebClientContext.ExecuteQueryRetry();
            Console.WriteLine("Site {0} has title {1}", e.Url, e.WebClientContext.Web.Title);
        }
```

## <a name="example-content-type-retention-enforcement-timer-job"></a>Beispiel: Inhaltstyp Aufbewahrung Erzwingung Zeitgeberauftrag

Das Projekt Core.TimerJobs.Samples.ContentTypeRetentionEnforcementJob zeigt, wie Sie SharePoint-Zeitgeberaufträgen zum Erzwingen von Aufbewahrungsrichtlinien für Inhaltstypen verwenden können. Verwenden das **ContentTypeRetentionPolicyPeriod** -Element in app.config, angeben:

-  **Schlüssel**, den Inhaltstyp-ID des Inhaltstyps, für die die Aufbewahrungsdauer gilt.
    
-  **Wert**, der die Aufbewahrungszeit in Tagen darstellt. Die Aufbewahrungsdauer wird für alle Listenelemente mit der im **Schlüssel**angegebene Inhaltstyp erstellt angewendet werden.

```XML
<ContentTypeRetentionPolicyPeriod>
    <!-- Key is the content type ID, and value is the retention period in days -->
    <!-- Specifies an audio content type should be kept for 183 days -->
    <add key="0x0101009148F5A04DDD49cbA7127AADA5FB792B006973ACD696DC4858A76371B2FB2F439A" value="183" />
    <!-- Specifies a document content type should be kept for 365 days -->   
    <add key="0x0101" value="365" />
</ContentTypeRetentionPolicyPeriod>
```

**ContentTypeRetentionEnforcementJob_TimerJobRun** wird als den Ereignishandler für das Ereignis **TimerJobRun** festgelegt. Wenn **TimerJob.Run** in Program.cs aufgerufen wird, führt **ContentTypeRetentionEnforcementJob_TimerJobRun** die folgenden Schritte auf jeder Website durch, die mit **TimerJob.AddSite** in Program.cs hinzugefügt wurde:


1. Ruft alle Dokumentbibliotheken auf der Website ab.
    
2. Für jedes Dokument-Bibliothek auf der Website liest die Konfigurationsinformationen in **ContentTypeRetentionPolicyPeriod** in ' App.config ' angegeben. Für jeden Inhaltstyp-ID und Aufbewahrung Period Pair, die von ' App.config ' gelesen wurde, wird die **ApplyRetentionPolicy** aufgerufen.

```C#
 void ContentTypeRetentionEnforcementJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            try
            {
                Log.Info("ContentTypeRetentionEnforcementJob", "Scanning web {0}", e.Url);

                // Get all document libraries. Lists are excluded.
                var documentLibraries = GetAllDocumentLibrariesInWeb(e.WebClientContext, e.WebClientContext.Web);

                // Iterate through all document libraries.
                foreach (var documentLibrary in documentLibraries)
                {
                    Log.Info("ContentTypeRetentionEnforcementJob", "Scanning library {0}", documentLibrary.Title);

                    // Iterate through configured content type retention policies specified in app.config.
                    foreach (var contentTypeName in configContentTypeRetentionPolicyPeriods.Keys)
                    {
                        var retentionPeriods = configContentTypeRetentionPolicyPeriods.GetValues(contentTypeName as string);
                        if (retentionPeriods != null)
                        {
                            var retentionPeriod = int.Parse(retentionPeriods[0]);
                            ApplyRetentionPolicy(e.WebClientContext, documentLibrary, contentTypeName, retentionPeriod);
                        }
                    }
                }
            }
            catch(Exception ex)
            {
                Log.Error("ContentTypeRetentionEnforcementJob", "Exception processing site {0}. Exception is {1}", e.Url, ex.Message);
            }
        }
```

**ApplyRetentionPolicy** erzwingt Ihrer benutzerdefinierten Retention Policy Aktionen durch:

1. **ValidationDate**zu berechnen. Die **ApplyRetentionPolicy** -Methode erzwingt Retention Policy Aktionen für Dokumente, die vor **ValidationDate**geändert. Klicken Sie dann **ValidationDate** wird als CAML Datum formatiert und **CamlDate**zugewiesen ist.
    
2. CAML-Abfrage zum Filtern von Dokumenten in der Dokumentbibliothek basierend auf den Inhaltstyp-ID, die in ' App.config ' angegeben wurde, und das Datum **Geändert von** kleiner ist als **CamlDate**ausführen.
    
3. Für jedes Listenelement Anwenden von benutzerdefinierten aufbewahrungsaktionen auf die Dokumente mithilfe von benutzerdefiniertem Code ausführen.

```C#
private void ApplyRetentionPolicy(ClientContext clientContext, List documentLibrary, object contentTypeId, int retentionPeriodDays)
        {
            // Calculate validation date. You need to enforce the retention policy on any document modified before validation date.
            var validationDate = DateTime.Now.AddDays(-retentionPeriodDays);
            var camlDate = validationDate.ToString("yyyy-MM-ddTHH:mm:ssZ");

            // Get old documents in the library that match the content type.
            if (documentLibrary.ItemCount > 0)
            {
                var camlQuery = new CamlQuery();
                
                camlQuery.ViewXml = String.Format(
                    @"<View>
                        <Query>
                            <Where><And>
                                <BeginsWith><FieldRef Name='ContentTypeId'/><Value Type='ContentTypeId'>{0}</Value></BeginsWith>
                                <Lt><FieldRef Name='Modified' /><Value Type='DateTime'>{1}</Value></Lt>
                            </And></Where>
                        </Query>
                    </View>", contentTypeId, camlDate);

                var listItems = documentLibrary.GetItems(camlQuery);
                clientContext.Load(listItems,
                    items => items.Include(
                        item => item.Id,
                        item => item.DisplayName,
                        item => item.ContentType));

                clientContext.ExecuteQueryRetry(); 

                foreach (var listItem in listItems)
                {
                    Log.Info("ContentTypeRetentionEnforcementJob", "Document '{0}' has been modified earlier than {1}. Retention policy will be applied.", listItem.DisplayName, validationDate);
                    Console.WriteLine("Document '{0}' has been modified earlier than {1}. Retention policy will be applied.", listItem.DisplayName, validationDate);
                    
                    // Apply your custom retention actions here. For example, archiving documents, or starting a disposition workflow.
                }
            }
        }
```

## <a name="example-governance-timer-job"></a>Beispiel: Governance-Zeitgeberauftrag

Das Projekt Core.TimerJobs.Samples.GovernanceJob Zeitgeberaufträge verwendet, um sicherzustellen, dass zwei Administratoren Ihrer Websitesammlungen zugeordnet sind, und wenn nicht, wird eine Benachrichtigung auf der Website angezeigt.

**SiteGovernanceJob_TimerJobRun** wird als den Ereignishandler für das Ereignis **TimerJobRun** festgelegt. Wenn **TimerJob.Run** in Program.cs aufgerufen wird, führt **SiteGovernanceJob_TimerJobRun** die folgenden Schritte für jede Websitesammlung, die mit **TimerJob.AddSite** in Program.cs hinzugefügt wurde:

1. Ruft die Anzahl der Administratoren in der Websitesammlung mithilfe der Extension-Methode [GetAdministrators](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/SecurityExtensions.cs) [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core)gehört.
    
2. Lädt die JavaScript-Datei in der Liste SiteAssets oder Formatbibliothek mit [UploadFile](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/FileFolderExtensions.cs), der Teil des [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core)ist hoch. 
    
3. Wenn der Standort weniger als zwei Administratoren verfügt, fügt [AddJSLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs) eine Benachrichtigung zu einer Website mithilfe von JavaScript. Erfahren Sie unter [Anpassen der Benutzeroberfläche mithilfe von JavaScript für die SharePoint-Website](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).
    
4. Wenn die Website zwei oder mehr Administratoren verfügt, wird die Benachrichtigung mit [DeleteJsLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs)entfernt.

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
        {
            try
            {
                string library = "";

                // Get the number of administrators.
                var admins = e.WebClientContext.Web.GetAdministrators();

                Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

                // Get a reference to the list.
                library = "SiteAssets";
                List list = e.WebClientContext.Web.GetListByUrl(library);

                if (!e.GetProperty("ScriptFileVersion").Equals("1.0", StringComparison.InvariantCultureIgnoreCase))
                {
                    if (list == null)
                    {
                        // Get a reference to the list.
                        library = "Style%20Library";
                        list = e.WebClientContext.Web.GetListByUrl(library);
                    }

                    if (list != null)
                    {
                        // Upload js file to list.
                        list.RootFolder.UploadFile("sitegovernance.js", "sitegovernance.js", true);

                        e.SetProperty("ScriptFileVersion", "1.0");
                    }
                }

                if (admins.Count < 2)
                {
                    // Show notification message because you need at least two site collection administrators.
                    e.WebClientContext.Site.AddJsLink(SiteGovernanceJobKey, BuildJavaScriptUrl(e.Url, library));
                    Console.WriteLine("Site {0} marked as incompliant!", e.Url);
                    e.SetProperty("SiteCompliant", "false");
                }
                else
                {
                    // Remove the notification message because two administrators are assigned.
                    e.WebClientContext.Site.DeleteJsLink(SiteGovernanceJobKey);
                    Console.WriteLine("Site {0} is compliant", e.Url);
                    e.SetProperty("SiteCompliant", "true");
                }

                e.CurrentRunSuccessful = true;
                e.DeleteProperty("LastError");
            }
            catch(Exception ex)
            {
                Log.Error("SiteGovernanceJob", "Error while processing site {0}. Error = {1}", e.Url, ex.Message);
                e.CurrentRunSuccessful = false;
                e.SetProperty("LastError", ex.Message);
            }
        }
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [Leitfaden zur Verwendung von den Timer Job-Framework](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md)
    
- [Timer-Job-framework](https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples)
