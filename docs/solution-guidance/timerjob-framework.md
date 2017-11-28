---
title: 'Das Timer Job-Framework #'
ms.date: 11/03/2017
ms.openlocfilehash: d6db7e8e9eb50006d8abb6d02ccfd9a0d12b736c
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="the-timer-job-framework"></a>Das Timer Job-Framework #

Die Plug & Play-Timer Job-Framework ist ein Satz von Klassen entwickelt, um einfache Erstellung Hintergrundprozesse, die Arbeiten mit SharePoint-Websites. Den Timer Job-Framework ist vergleichbar mit lokalen voll vertrauenswürdiger Code Timer Jobs (`SPJobDefinition`). Der Hauptunterschied zwischen den Timer Job-Framework und den Code volle Vertrauenswürdigkeit Zeitgeberauftrag mit ist, den Timer Job-Framework nur Client-seitigen APIs verwendet und daher können (und sollten) außerhalb von SharePoint ausgeführt werden. Den Timer Job-Framework ermöglicht die Zeitgeberaufträge erstellen, die mit SharePoint Online arbeiten.

Sobald ein Zeitgeberauftrag, es erstellt wurden muss geplant und ausgeführt werden. Die beiden am häufigsten verwendeten Optionen sind:

- Wenn **Microsoft Azure** die Hostingplattform ist, können Zeitgeberaufträge bereitgestellt und als **Azure WebJobs**ausgeführt werden.
- Wenn **Windows Server** ist kann im **Windows-Taskplaner**die Zeitgeberaufträge für hosting-Plattform (z. B. für lokale SharePoint) bereitgestellt und ausgeführt werden.

Video eine Einführung in die Zeitgeberaufträge [in diesem Video Plug & Play-](http://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-the-PnP-timer-job-framework) führt den Timer Job-Framework und das Zeitgeberauftrag für die einfachen Beispiel veranschaulicht.

## <a name="simple-timer-job-example"></a>Einfaches Beispiel für Zeitgeberauftrag ##
In diesem Kapitel erfahren Sie, wie Sie eine sehr einfache Zeitgeberauftrag zum Erstellen: das Ziel der in diesem Beispiel wird dem Leser einen schnellen Einblick in bereitstellen, später bieten wir eine ausführlichere Erläuterung der den Timer Job-Framework. 

**Hinweis:** Eine umfangreichere Plug & Play-Lösung mit zehn einzelne Zeitgeberauftrag-Beispiele von "Hello World" herunter, die tatsächliche Inhaltsablauf Aufträge finden Sie unter https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples

Die folgenden wird beschrieben, wie eine einfache Zeitgeberauftrag zu erstellen:

### <a name="step-1-create-a-console-project-and-reference-pnp-core"></a>Schritt 1: Erstellen eines Konsolenprojekts und verweisen auf Plug & Play-Core ###
Erstellen Sie in diesem ersten Schritt ein neues Projekt vom Typ "Konsole" und verweisen Sie die Plug & Play-Core-Bibliothek zu, indem Sie einen der folgenden Schritte ausführen:

- Fügen Sie Sie dem Projekt das Office 365 Developer Mustern und Methoden Core Nuget-Paket. Es wird ein [Nuget-Paket für v15 (lokal) und für v16 (Office 365)](https://www.nuget.org/packages?q=pnp). Dies ist die bevorzugte Option.
- Fügen Sie Sie dem Projekt das vorhandene Plug & Play-Kern-Source-Projekt. Dadurch können Sie den Plug & Play-Kerncode schrittweise beim Debuggen. **Hinweis:** Dafür verantwortlich ist dieser Code aktualisiert mit den neuesten Änderungen Plug & Play-hinzugefügt werden.

### <a name="step-2-create-a-timer-job-class-and-add-your-timer-job-logic"></a>Schritt 2: Erstellen Sie eine Zeitgeberauftrag-Klasse und fügen Ihre Zeitgeberauftrag Logik hinzu ###
1. Fügen Sie eine Klasse für den Zeitgeberauftrag mit dem Namen `SimpleJob`.
2. Klasse erben die `TimerJob` abstrakte Basisklasse.
3. In den Konstruktor benennen Sie den Zeitgeberauftrag (`base("SimpleJob")`) und Verbinden der `TimerJobRun` -Ereignishandler.
4. Die Zeitgeberauftrag für die Logik zum Hinzufügen der `TimerJobRun` -Ereignishandler.

Das Ergebnis wird ähnlich der folgenden sein:
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using OfficeDevPnP.Core.Framework.TimerJobs;

namespace Core.TimerJobs.Samples.SimpleJob
{
    public class SimpleJob: TimerJob
    {
        public SimpleJob() : base("SimpleJob")
        {
            TimerJobRun += SimpleJob_TimerJobRun;
        }

        void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            e.WebClientContext.Load(e.WebClientContext.Web, p => p.Title);
            e.WebClientContext.ExecuteQueryRetry();
            Console.WriteLine("Site {0} has title {1}", e.Url, e.WebClientContext.Web.Title);
        }
    }
}
```

### <a name="step-3-update-programcs-to-use-the-timer-job"></a>Schritt 3: Update Program.cs, verwenden Sie den Zeitgeberauftrag ###
Der Zeitgeberauftrag mit dem im vorherigen Schritt erstellten weiterhin soll ausgeführt werden. Aktualisieren Sie dazu `Program.cs` mithilfe der folgenden Schritte aus:

1. Die Zeitgeberauftrag für die Klasse zu instanziieren.
2. Geben Sie die Authentifizierungsdetails für den Zeitgeberauftrag. In diesem Beispiel verwendet den Benutzernamen und das Kennwort, um die Authentifizierung für SharePoint Online.
3. Fügen Sie einen oder mehrere Standorte für das Programm Zeitgeberauftrag für den Zugriff auf. In diesem Beispiel wird ein Platzhalterzeichen in der URL. Der Zeitgeberauftrag wird auf alle Websites ausgeführt, die mit dieser Platzhalter URL übereinstimmen.
4. Starten Sie den Zeitgeberauftrag durch Aufrufen der `Run` Methode.

```C#
static void Main(string[] args)
{
    // Instantiate the Timer Job class
    SimpleJob simpleJob = new SimpleJob();
    
    // The provided credentials need access to the site collections you want to use
    simpleJob.UseOffice365Authentication("user@tenant.onmicrosoft.com", "pwd");

    // Add one or more sites to operate on
    simpleJob.AddSite("https://<tenant>.sharepoint.com/sites/d*");
    
    // Run the job
    simpleJob.Run();
}
```

## <a name="timer-job-deployment-options"></a>Timer-Job-Bereitstellungsoptionen ##
Im vorherige Schritt veranschaulicht eine einfache Zeitgeberauftrag. Der nächste Schritt besteht darin, den Zeitgeberauftrag bereitzustellen.

Ein Zeitgeberauftrag ist eine .exe-Datei, die auf einer Hostingplattform eingeplant werden muss. Abhängig von der gewählten Hostingplattform unterscheidet sich in die Bereitstellung. In den folgenden Abschnitten werden die beiden am häufigsten verwendeten Plattform Hostingoptionen beschrieben:
- Verwenden von Microsoft Azure als die hosting-Plattform
- Mithilfe von Windows Server als hosting-Plattform

### <a name="deploying-timer-jobs-to-microsoft-azure-using-azure-webjobs"></a>Bereitstellen von Zeitgeberaufträgen in Microsoft Azure mithilfe von Azure WebJobs ###
Bevor Sie einen Zeitgeberauftrag bereitstellen, stellen Sie sicher, dass der Auftrag ohne Benutzereingriff ausgeführt werden kann. Im Beispiel in diesem Artikel der Benutzer aufgefordert, ein Kennwort oder den Clientsecret angeben (Siehe auch bei der **Authentifizierung**) welche funktioniert while testen, aber die funktionieren nicht, wenn bereitgestellt. Die alle vorhandenen Beispielen ermöglichen Benutzern das Geben Sie ein Kennwort oder Clientsecret mithilfe der `app.config` Datei:

```XML
  <appSettings>
    <add key="user" value="user@tenant.onmicrosoft.com"/>
    <add key="password" value="your password goes here!"/>
    <add key="domain" value="Contoso"/>
    <add key="clientid" value="a4cdf20c-3385-4664-8302-5eab57ee6f14"/>
    <add key="clientsecret" value="your clientsecret goes here!"/>
  </appSettings>
```

Nachdem diese Änderungen hinzugefügt werden die `app.config` Datei, und führen Sie den Zeitgeberauftrag von Visual Studio zu bestätigen, dass sie ohne Benutzereingriff ausgeführt wird. 

Die tatsächliche Bereitstellung in Azure basiert auf Azure Webaufträge. In diesem Beispiel der Zeitgeberauftrag für die Bereitstellung die folgenden Schritte aus:

1. Klicken Sie mit der rechten Maustaste auf das Projekt in Visual Studio, und wählen Sie **Veröffentlichen als Azure WebJob...**
2. Geben Sie einen Zeitplan für den Zeitgeberauftrag, und klicken Sie auf **OK**
3. Wählen Sie **Microsoft Azure-Websites** als Veröffentlichungsziel. Sie werden aufgefordert, in Azure anmelden, und wählen Sie die Azure-Website, die den Zeitgeberauftrag hostet (Sie können auch einen neuen Anwendungspool erstellen, die benötigt werden)
4. Drücken Sie **Veröffentlichen** , drücken Sie die WebJob in Azure
5. Nachdem der Zeitgeberauftrag veröffentlicht wurde können Sie den Auftrag auslösen und überprüfen Sie die Ausführung des Auftrags aus Visual Studio oder dem [Azure-Verwaltungsportal](https://manage.windowsazure.com).

![Azure-Verwaltungsportal](media/timerjob-framework/4xDUvXv.png)

Darüber hinaus kann der Zeitgeberauftrag, indem Markieren des Auftrags und **Führen Sie**über das neue [Portal Azure](https://portal.azure.com) ausgeführt werden. Weitere Informationen zum Arbeiten mit WebJobs über das neue Portal finden Sie im Artikel [Hintergrund ausführen von Aufgaben mit WebJobs](https://azure.microsoft.com/en-us/documentation/articles/web-sites-create-web-jobs/).

![Azure-portal](media/timerjob-framework/n4wGS5x.png)

**Hinweis:** Ausführliche Anleitungen ein Azure WebJob bereitstellen finden Sie unter [Erste Schritte mit Azure WebJobs ("Zeitgeberaufträge") für Ihre Office 365-Websites](https://github.com/SharePoint/PnP-Guidance/blob/master/articles/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites.md). 

### <a name="deploying-timer-jobs-to-windows-server-using-the-windows-scheduler"></a>Bereitstellen von Zeitgeberaufträgen in Windows Server mithilfe der Windows-Taskplaner ###
Wenn in Windows Server bereitgestellt wird, müssen den Zeitgeberauftrag ohne Benutzereingriff ausführen. Ändern der `app.config` speichern unter **Bereitstellen von Zeitgeberaufträgen für Microsoft Azure mithilfe von Azure WebJobs**beschrieben. 

Kopieren Sie die endgültige Produktversion von Ihre Arbeit an den Server, auf ausführen soll. **Wichtig:** Kopieren Sie alle relevanten Assemblys, die .exe-Datei und die .config-Datei, um sicherzustellen, dass der Auftrag auf dem Server ausführen kann, ohne zusätzliche Dateien oder Programme auf dem Server installieren. 

Planen Sie die Ausführung des Zeitgeberauftrags. Es wird empfohlen, die integrierte [Windows-Taskplaner](https://technet.microsoft.com/en-us/library/cc721871.aspx)verwendet. Um die Windows-Taskplaner verwenden zu können, müssen Sie die folgenden Schritte aus:

1. Öffnen Sie den Taskplaner (Control Panel-Taskplaner >).
2. Klicken Sie auf **Aufgabe erstellen** , und geben Sie einen Namen und ein Konto, das die Aufgabe ausgeführt wird.
3. Klicken Sie auf **Trigger** , und fügen Sie einen neuen Trigger hinzu. Geben Sie den Zeitplan für den Zeitgeberauftrag gewünschten.
4. Klicken Sie auf **Aktionen** und wählen Sie die Aktion "Einen Programm starten", wählen Sie die Zeitgeberauftrag .exe-Datei ein, und legen Sie den Start im Ordner.
5. Klicken Sie auf **OK** , um den Vorgang zu speichern.

![Die Windows-Taskplaner](media/timerjob-framework/hkRc0Bo.png)

## <a name="timer-job-framework-in-depth"></a>Timer-Job-Framework fundierte ##
In diesem Abschnitt Details wie den Timer Job Framework-Features und deren Funktionsweise.

### <a name="structure"></a>Struktur ###
Die `TimerJob` Klasse ist eine abstrakte Basisklasse, die die folgenden öffentlichen Eigenschaften, Methoden und Ereignisse enthält:

![Die Struktur einer allgemeinen](media/timerjob-framework/4XsZ1pN.png)

Die meisten Eigenschaften und Methoden werden in den folgenden Abschnitten ausführlich erläutert. Hier werden die restlichen Eigenschaften und Methoden beschrieben:

- **IsRunning** -Eigenschaft: Ruft einen Wert zurück, der angibt, ob der Zeitgeberauftrag ausgeführt wird. Der Wert **true,** Wenn ausgeführt; **false,** wenn er nicht ausgeführt.
- **Name** -Eigenschaft: Ruft den Namen des Zeitgeberauftrags ab. Der Name wird in den Zeitgeberauftrag Konstruktor ursprünglich festgelegt.
- **SharePointVersion** -Eigenschaft: Dient zum Abrufen oder festlegen die SharePoint-Version. Diese Eigenschaft wird automatisch festgelegt, basierend auf der Version von der geladenen Microsoft.SharePoint.Client.dll und im Allgemeinen sollten nicht ändern. Sie können diese Eigenschaft jedoch ändern, falls Sie beispielsweise die v16 CSOM Bibliotheken in einem v15 verwenden möchten (lokal)-Bereitstellung.
- **Version** -Eigenschaft: Ruft die Version des diesen Zeitgeberauftrag. Die Version im Konstruktor Zeitgeberauftrag ursprünglich festgelegt ist oder in der Standardeinstellung werden 1.0, wenn nicht über den Konstruktor festgelegt.

Vorbereiten für einen Zeitgeberauftrag führen Sie erste **Konfigurieren** müssen sie:

1. Geben Sie **Authentifizierungseinstellungen** .
2. Geben Sie einen **Bereich**, der eine Liste der Websites ist.
3. Festlegen Sie **Zeitgeberauftrag für die Eigenschaften**optional.

Aus der Sicht Ausführung werden die folgenden allgemeinen Schritte übernommen, wenn eine Ausführung des Zeitgeberauftrags gestartet wurde:

1. **Beheben von Websites**: Platzhalter Website-Urls (beispielsweise https://tenant.sharepoint.com/sites/d *) in eine aktuelle Liste der vorhandenen Websites aufgelöst werden. Wenn Sub Website erweitern angefordert wurde, wird die Websiteliste aufgelöst mit allen Unterwebsites erweitert.
2. **Erstellen der Arbeit Batches** basierend auf der aktuellen Einstellungen treading sowie einen Thread pro Batch.
3. Das **Threads Arbeit Batches ausführen** , und rufen die `TimerJobRun` -Ereignis für jeden Standort in der Liste.

Weitere Informationen zu den einzelnen Schritten finden Sie unter.

### <a name="authentication"></a>Authentifizierung ###
Bevor ein Zeitgeberauftrag verwendet werden können muss den Zeitgeberauftrag wissen, wie Sie SharePoint authentifiziert. Das Framework unterstützt derzeit die Ansätze im **AuthenticationType** -Enumeration. **Office365**, **Netzwerk-Anmeldeinformationen weisen** und **AppOnly**. Mit den Methoden die **AuthenticationType** -Eigenschaft auf den entsprechenden Wert von **Office365**, **Netzwerk-Anmeldeinformationen weisen** und **AppOnly**, folgenden auch automatisch dargestellt. Im folgenden Flussdiagramm zeigt die Schritte. Ausführliche Erklärungen auf jeder Ansatz finden Sie unter.

![Flussdiagramm für die Authentifizierung Schritte](media/timerjob-framework/rt4dZa3.png)

#### <a name="user-credentials"></a>Anmeldeinformationen des Benutzers ####
Zum Angeben der Anmeldeinformationen des Benutzers zum Ausführen für **Office 365** können Sie diese 2 Methoden verwenden:
```C#
public void UseOffice365Authentication(string userUPN, string password)
public void UseOffice365Authentication(string credentialName)
```

Die erste Methode akzeptiert einfach einen Benutzernamen und ein Kennwort ein. Im zweiten Beispiel können Sie eine generische Anmeldeinformationen gespeichert im Windows-Anmeldeinformations-Manager angeben. Der Screenshot zeigt die `bertonline` generische Anmeldeinformationen. Um, die zum Authentifizieren der Zeitgeberauftrag verwenden, geben Sie "Bertonline" als Parameter für die zweite Methode.

![Der Anmeldeinformations-Manager für Windows](media/timerjob-framework/HdqvsHy.png)

Es gibt ähnliche Methoden, um für **SharePoint lokal**auszuführen:
```C#
public void UseNetworkCredentialsAuthentication(string samAccountName, string password, string domain)
public void UseNetworkCredentialsAuthentication(string credentialName)
```

#### <a name="app-only"></a>Nur-App ####
App ist nur die **bevorzugte Methode** , wie Sie Mandanten bezogenen Berechtigungen gewähren können. Für Benutzeranmeldeinformationen muss das Benutzerkonto die erforderlichen Berechtigungen verfügen. 

**Hinweis:** Bestimmte Website lösen mit nur-App-Authentifizierung Logik funktionieren nicht. Ausführliche Informationen finden Sie im nächsten Abschnitt. 

Um den Auftrag für nur-app-Authentifizierung zu konfigurieren, verwenden Sie eine der folgenden Methoden:
```C#
public void UseAppOnlyAuthentication(string clientId, string clientSecret)
public void UseAzureADAppOnlyAuthentication(string clientId, string clientSecret)
```

Die gleiche-Methode kann für Office 365 oder SharePoint lokal Zeitgeberaufträge mithilfe der nur-app-Authentifizierung auf einfache Weise zwischen Umgebungen Portable wodurch verwendet werden.

**Hinweis:** Bei Verwendung der nur-app-wird die Logik Zeitgeberauftrag misslingen, wenn APIs verwendet werden, die mit **AuthenticationType.AppOnly**nicht funktionsfähig. Standardsamples sind die Such-API, an den Taxonomie-Store schreiben und das Benutzerprofil API verwenden.

### <a name="sites-to-operate-on"></a>Websites für den Betrieb ###
Der Ausführung eines Zeitgeberauftrags benötigt es einen oder mehrere Standorte für ausführen. Um einen Zeitgeberauftrag Websites hinzuzufügen, verwenden Sie die unten Satz von Methoden.

```C#
public void AddSite(string site)
public void ClearAddedSites()
```

Geben Sie zum Hinzufügen einer Website eine vollqualifizierte URL (beispielsweise https://tenant.sharepoint.com/sites/dev) oder eine Platzhalter-URL ein. Ein Platzhalter-URL ist eine URL mit der Endung ein * (nur eine einzige * ist zulässig, und es muss das letzte Zeichen der Url). Ein Beispiel Platzhalter-URL ist https://tenant.sharepoint.com/sites/ *, durch den **Alle** Websitesammlungen unterhalb der verwaltete Pfad dieser Website zurückgegeben wird. Ein weiteres Beispiel gibt https://tenant.sharepoint.com/sites/dev * alle Websitesammlungen zurück, bei denen die URL "Developer" enthält.

In der Regel werden die Websites von der Anwendung hinzugefügt, die das Objekt Zeitgeberauftrag, außer wenn instanziiert der Zeitgeberauftrag zum Steuern der übergebenen Liste der Websites ergreifen können, benötigt. Fügen Sie eine Methode zum Überschreiben für die `UpdateAddedSites`virtuelle-Methode, wie im folgenden Beispiel:

```C#
public override List<string> UpdateAddedSites(List<string> addedSites)
{
    // Let's assume we're not happy with the provided list of sites, so first clear it
    addedSites.Clear();

    // Manually adding a new wildcard Url, without an added URL the Timer Job will do...nothing
    addedSites.Add("https://bertonline.sharepoint.com/sites/d*");

    // Return the updated list of sites
    return addedSites;
}
```

Geben Sie nach dem hinzufügen einen Platzhalter-URL und die Einstellung Authentifizierung nur-app, die Enumeration Anmeldeinformationen ein. Enumeration Anmeldeinformationen werden verwendet, um eine Liste der Websitesammlungen abgerufen, die in der entsprechenden Website-Algorithmus verwendet werden, um eine echte Liste der Websites zurückzugeben. Um eine Liste der Websitesammlungen erhalten das Timer-Framework unterschiedlich zwischen Office 365 (v16) und lokale (v15) verhält sich:
- Office 365: Die `Tenant.GetSiteProperties` Methode dient dazu, lesen Sie die "normaler" Websitesammlungen, die Such-API wird verwendet, um die OneDrive for Business-Websitesammlungen zu lesen.
- Lokal: Such-API wird verwendet, um alle Websitesammlungen zu lesen.

Wenn die API für die Suche nicht mit einem Benutzerkontext funktioniert, greift den Zeitgeberauftrag auf der angegebenen Enumeration Anmeldeinformationen zurück. 

Zum Angeben der Anmeldeinformationen des Benutzers zum Ausführen für **Office 365** können Sie diese 2 Methoden verwenden:
```C#
public void SetEnumerationCredentials(string userUPN, string password)
public void SetEnumerationCredentials(string credentialName)
```

Es gibt ähnliche Methoden, um für **SharePoint lokal**auszuführen:
```C#
public void SetEnumerationCredentials(string samAccountName, string password, string domain)
public void SetEnumerationCredentials(string credentialName)
```

Die erste Methode akzeptiert einfach ein Benutzername, Kennwort und optional Domäne (in der lokalen). Die zweite gibt die generische Anmeldeinformationen, die in der Windows-Anmeldeinformationsverwaltung gespeichert. Finden Sie das **Authentifizierung** Kapitel erhalten Sie weitere Informationen zum Anmeldeinformations-Manager.

#### <a name="sub-site-expanding"></a>Sub-Website erweitern ####
Häufig soll der Zeitgeberauftrag für Code, der Stammwebsite der Websitesammlung und mit den alle Unterwebsites dieser Websitesammlung ausgeführt werden soll. Zu diesem Zweck müssen Sie die **ExpandSubSites** -Eigenschaft auf **true**festgelegt. Dadurch wird der Zeitgeberauftrag für die Sub-Websites als Teil der Website Auflösen von Schritt zu erweitern.

#### <a name="override-resolved-andor-expanded-sites"></a>Außer Kraft setzen Sie aufgelöst und/oder erweiterte Websites ####
Sobald das Timer-Framework die Platzhalter-Websites löst und optional die Sub-Websites erweitert, besteht der nächste Schritt die Liste der Websites zu verarbeiten. Vor der Verarbeitung der Liste der Websites, empfiehlt es sich um die Liste der Websites zu ändern. Angenommen, möchten Sie der Liste weitere Websites hinzufügen oder Entfernen von bestimmten Websites. Hierfür kann durch Überschreiben der `ResolveAddedSites` virtuelle Methode. Im folgenden Beispiel wird das Überschreiben der `ResolveAddedSites` -Methode, um einen Standort aus der Liste zu entfernen. 

```C#
public override List<string> ResolveAddedSites(List<string> addedSites)
{
    // Use default TimerJob base class site resolving
    addedSites = base.ResolveAddedSites(addedSites);

    //Delete the first one from the list...simple change. A real life case could be reading the site scope 
    //from a SQL (Azure) DB to prevent the whole site resolving. 
    addedSites.RemoveAt(0);

    // return the updated list of resolved sites...this list will be processed by the Timer Job
    return addedSites;
}
```

### <a name="timerjobrun-event"></a>TimerJobRun-Ereignis ###
Den Timer Job-Framework wird die Liste der Websites in Batches Arbeit geteilt. Jedem Batch von Websites werden in einem eigenen Thread ausgeführt. In der Standardeinstellung erstellt das Framework fünf Batches und fünf Threads an, die diese fünf Batches ausgeführt. Siehe Abschnitt **Threading** erfahren Sie mehr über Zeitgeberauftrag threading-Optionen. Wenn ein Thread einen Batch verarbeitet die `TimerJobRun` -Ereignis wird ausgelöst, durch den Timer-Framework und bietet die erforderliche Informationen zum Ausführen des Zeitgeberauftrags. Zeitgeberaufträge als Ereignisse, ausgeführt werden, sodass der Code einen Ereignishandler für eine Verbindung herstellen muss die `TimerJobRun` Ereignis:

```C#
public SimpleJob() : base("SimpleJob")
{
    TimerJobRun += SimpleJob_TimerJobRun;
}

void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
{
    // your Timer Job logic goes here
}
```

Ein alternativer Ansatz ist einen Inline-Delegaten wie folgt verwenden:

```C#
public SimpleJob() : base("SimpleJob")
{
    // Inline delegate
    TimerJobRun += delegate(object sender, TimerJobRunEventArgs e)
    {
        // your Timer Job logic goes here
    };
}
```

Wenn die `TimerJobRun` -Ereignis ausgelöst wird eine `TimerJobRunEventArgs` Objekt, das die erforderliche Informationen zum Schreiben der Zeitgeberauftrag für die Logik ermöglicht. Die folgenden Attribute und Methoden sind in dieser Klasse verfügbar:

![Die Struktur der TimerJobRunEventArgs-Klasse](media/timerjob-framework/CRFBdwS.png)

Mehrere Eigenschaften und alle Methoden sind in die optionale State Management-Funktion verwendet, die im nächsten Abschnitt erläutert werden. Die folgenden Eigenschaften können jedoch immer in jedes Ereignis, unabhängig von der verwendeten Konfiguration verfügbar sein:
- **URL** -Eigenschaft: Dient zum Abrufen oder Festlegen der URL der Website für den Zeitgeberauftrag auswirken. Dies kann der Stammwebsite der Websitesammlung sein, aber eine Unterwebsite kann auch sein, für den Fall, dass Website erweitern vorgenommen wurde.
- **ConfigurationData** -Eigenschaft: Dient zum Abrufen oder Festlegen zusätzlicher Timer Job-Konfigurationsdaten (optional). Diese Konfigurationsdaten werden als Teil des übergeben der `TimerJobRunEventArgs` Objekt.
- **WebClientContext** -Eigenschaft: Dient zum Abrufen oder Festlegen der `ClientContext` -Objekt für den aktuellen URL. Diese Eigenschaft ist ein `ClientContext` -Objekt für die Website in der *Url* -Eigenschaft definiert. Dies ist üblicherweise der `ClientContext` -Objekt, das Sie in Ihrem Code Zeitgeberauftrag verwenden würden.
- **SiteClientContext** -Eigenschaft: Dient zum Abrufen oder Festlegen der `ClientContext` -Objekt für die Stammwebsite der Websitesammlung. Diese Eigenschaft bietet Zugriff auf die Stammwebsite der Zeitgeberauftrag zum Zugriff darauf erforderlich sein soll. Beispielsweise kann der Zeitgeberauftrag für ein Seitenlayout Gestaltungsvorlagenkatalog mithilfe der *SiteClientContext* -Eigenschaft hinzufügen.
- **TenantClientContext** -Eigenschaft: Dient zum Abrufen oder Festlegen der `ClientContext` -Objekt mit der Mandanten-API zu arbeiten. Diese Eigenschaft bietet eine `ClientContext`-Objekt, mit dem Mandanten Admin-Website-URL erstellt. Verwenden der `Tenant` -API in den Zeitgeberauftrag `TimerJobRun` -Ereignishandler erstellen Sie ein neues `Tenant` Objekt unter Verwendung dieser Eigenschaft TenantClientContext.

Alle `ClientContext`Objekte verwenden, die Authentifizierungsinformationen angeben im Abschnitt **Authentifizierung** beschrieben. Wenn Sie, für die Anmeldeinformationen des Benutzers entschieden haben stellen Sie sicher, dass das verwendete Konto die erforderlichen Berechtigungen für die angegebenen Websites ausgeführt werden. Wenn Sie nur-app-verwenden, empfiehlt es sich für den nur-app-Prinzipal mandantenbereichsbezogenen Berechtigungen festzulegen.

### <a name="state-management"></a>State management ###
Beim Schreiben von Zeitgeberauftrag Logik müssen Sie häufig Zustand beizubehalten. Beispielsweise aufzeichnen, wenn der letzten Verarbeitung einer Website oder zum Speichern von Daten, um Ihre Geschäftslogik Zeitgeberauftrag zu unterstützen. Aus diesem Grund hat den Timer Job-Framework State Management-Funktionen. State Management speichert und ruft eine Reihe von standardmäßigen und benutzerdefinierten Eigenschaften als serialisierten JSON-Zeichenfolge in der Web-Eigenschaftensammlung der verarbeiteten Website (Name = "_Properties" + Zeitgeberauftrag Name). Im folgenden sind die Standardeigenschaften des der `TimerJobRunEventArgs`Objekt:
- **PreviousRun** -Eigenschaft: Dient zum Abrufen oder festlegen, das Datum und die Uhrzeit der vorherigen Ausführung.
- **PreviousRunSuccessful** -Eigenschaft: Dient zum Abrufen oder Festlegen eines Werts, der angibt, ob die vorherige Ausführung erfolgreich war. Beachten Sie, dass der Zeitgeberauftrag zum Autor für kennzeichnen ein Projekt als erfolgreich ausführen, indem Sie die **CurrentRunSuccessful** -Eigenschaft als Teil der Zeitgeberauftrag für die Implementierung von zuständig ist
- **PreviousRunVersion** -Eigenschaft: Dient zum Abrufen oder festlegen die Zeitgeberauftrag für die Version von der vorherigen Ausführung.

Neben diesen Standardeigenschaften haben Sie auch die Möglichkeit, Ihre eigenen Eigenschaften festlegen, indem Sie Schlüsselwort - Wert-Paare an die `Properties` -Auflistung der `TimerJobRunEventArgs`Objekt. Dies erleichtert es gibt drei Methoden, die Sie unterstützen:
- **SetProperty** fügt oder eine Eigenschaft aktualisiert.
- **GetProperty** gibt den Wert einer Eigenschaft zurück.
- **DeleteProperty** entfernt eine Eigenschaft aus der Auflistung Eigenschaften.

Der folgende Code zeigt, wie Statusverwaltung verwendet werden kann:

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
{
    try
    {
        string library = "";

        // Get the number of admins
        var admins = e.WebClientContext.Web.GetAdministrators();

        Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

        // grab reference to list
        library = "SiteAssets";
        List list = e.WebClientContext.Web.GetListByUrl(library);

        if (!e.GetProperty("ScriptFileVersion").Equals("1.0", StringComparison.InvariantCultureIgnoreCase))
        {
            if (list == null)
            {
                // grab reference to list
                library = "Style%20Library";
                list = e.WebClientContext.Web.GetListByUrl(library);
            }

            if (list != null)
            {
                // upload js file to list
                list.RootFolder.UploadFile("sitegovernance.js", "sitegovernance.js", true);

                e.SetProperty("ScriptFileVersion", "1.0");
            }
        }

        if (admins.Count < 2)
        {
            // Oops, we need at least 2 site collection administrators
            e.WebClientContext.Site.AddJsLink(SiteGovernanceJobKey, BuildJavaScriptUrl(e.Url, library));
            Console.WriteLine("Site {0} marked as incompliant!", e.Url);
            e.SetProperty("SiteCompliant", "false");
        }
        else
        {
            // We're all good...let's remove the notification
            e.WebClientContext.Site.DeleteJsLink(SiteGovernanceJobKey);
            Console.WriteLine("Site {0} is compliant", e.Url);
            e.SetProperty("SiteCompliant", "true");
        }

        e.CurrentRunSuccessful = true;
        e.DeleteProperty("LastError");
    }
    catch(Exception ex)
    {
        e.CurrentRunSuccessful = false;
        e.SetProperty("LastError", ex.Message);
    }
}
```

Der Status wird gespeichert, wie eine einzelne JSON Eigenschaft, d. h. serialisiert dieser von anderen Anpassungen als auch verwendet werden kann. Wenn der Zeitgeberauftrag für den Zustandseintrag geschrieben haben beispielsweise "SiteCompliant = False", eine JavaScript-Routine konnte fordert den Benutzer auf, da der Zeitgeberauftrag festgestellt, dass die Website incompliant wurde fungieren.

### <a name="threading"></a>Threading ###
Den Timer Job-Framework standardmäßig verwendet Threads, um Arbeit zu parallelisieren. Threading wird für beide die Sub-Website-Erweiterung (falls erforderlich) und für die Ausführung verwendet die eigentliche Zeitgeberauftrag Logik (`TimerJobRun` -Ereignis) für jeden Standort. Die folgenden Eigenschaften können zur Steuerung der Threads Implementierung verwendet werden:
- **UseThreading** -Eigenschaft: Dient zum Abrufen oder Festlegen eines Werts, der angibt, ob threading verwendet werden soll. Der Standardwert ist **true**.  Alle Aktionen ausführen, mithilfe des Hauptfensters der Anwendungsthreads auf **false** festgelegt.
- **MaximumThreads** -Eigenschaft: Ruft ab oder legt die Anzahl der Threads an, die für diesen Zeitgeberauftrag verwenden. Gültige Werte sind 2 bis 100. Der Standardwert ist 5. Viele der Threads ist nicht unbedingt schneller, und klicken Sie dann mit nur wenigen Threads. Die optimale Anzahl sollte über Tests mit einer Vielzahl von Thread zählt erworben werden. Der Standardwert von 5 Threads wurde erheblich steigern der Leistung in den meisten Szenarien gefunden. 

#### <a name="throttling"></a>Drosselung ####
Da Zeitgeberauftrag threading verwendet und Zeitgeberauftrag Vorgänge in der Regel ressourcenintensive Vorgänge sind, konnte eine Ausführung des Zeitgeberauftrags gedrosselt. Um ordnungsgemäß befassen sich mit den Timer Job-Framework und dem gesamten verwendet Plug & Play-Core-Einschränkung der `ExecuteQueryRetry` Methode anstatt vom standardmäßigen `ExecuteQuery`Methode.

**Hinweis:** Es ist wichtig, verwenden Sie `ExecuteQueryRetry` in Ihrem Code zur Implementierung des Zeitgeberauftrags.

#### <a name="concurrency-issues---process-all-sub-sites-of-a-site-collection-in-the-same-thread"></a>Parallelität Probleme mit – verarbeiten alle Unterwebsites einer Websitesammlung in demselben thread ####

Zeitgeberaufträge möglicherweise Parallelitätsprobleme bei der Verwendung von mehreren Threads zum Verarbeiten von Unterwebsites. Nehmen Sie dieses Beispiel: Thread A verarbeitet den ersten Satz von Sub-Websites aus der Websitesammlung 1 und Thread B die restlichen die Sub-Websites aus der Websitesammlung 1 verarbeitet. Wenn der Zeitgeberauftrag für die Unterwebsite und der Stammwebsite verarbeitet (mithilfe der `SiteClientContext` Object), es kann ein Problem Parallelität seit beide Thread A und Thread B Verarbeiten der Stammwebsite. Die Verwendung der Parallelität Problem (ohne den Timer Jobs in einen einzelnen Thread ausgeführt) vermeiden der `GetAllSubSites` Methode innerhalb des Zeitgeberauftrags.

Der folgende Code zeigt, wie Sie mit der `GetAllSubSites` Methode innerhalb eines Zeitgeberauftrags:

```C#
public class SiteCollectionScopedJob: TimerJob
{
    public SiteCollectionScopedJob() : base("SiteCollectionScopedJob")
    {
        // ExpandSites *must* be false as we'll deal with that at TimerJobEvent level
        ExpandSubSites = false;
        TimerJobRun += SiteCollectionScopedJob_TimerJobRun;
    }

    void SiteCollectionScopedJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
    {
        // Get all the sub sites in the site we're processing
        IEnumerable<string> expandedSites = GetAllSubSites(e.SiteClientContext.Site);

        // Manually iterate over the content
        foreach (string site in expandedSites)
        {
            // Clone the existing ClientContext for the sub web
            using (ClientContext ccWeb = e.SiteClientContext.Clone(site))
            {
                // Here's the Timer Job logic, but now a single site collection is handled in a single thread which 
                // allows for further optimization or prevents race conditions
                ccWeb.Load(ccWeb.Web, s => s.Title);
                ccWeb.ExecuteQueryRetry();
                Console.WriteLine("Here: {0} - {1}", site, ccWeb.Web.Title);
            }
        }
    }
}
```

### <a name="logging"></a>Protokollierung ###
Den Timer Job-Framework verwendet die Protokollierung Plug & Play-Core-Komponenten als Teil der die Plug & Play-Core-Bibliothek. Um die integrierten Plug & Play-Kern-Protokollierung zu aktivieren, konfigurieren sie mithilfe der entsprechenden Konfigurationsdatei (app.config oder web.config). Das folgende Beispiel zeigt die erforderliche Syntax:

```XML
  <system.diagnostics>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="DebugListenter" type="System.Diagnostics.TextWriterTraceListener" initializeData="trace.log" />
        <!--<add name="consoleListener" type="System.Diagnostics.ConsoleTraceListener" />-->
      </listeners>
    </trace>
  </system.diagnostics>
```

Mithilfe der oben genannten Konfigurationsdatei den Timer Job-Framework verwendet die `System.Diagnostics.TextWriterTraceListener` , Protokolle in eine Datei namens trace.log im selben Ordner wie die .exe-Zeitgeberauftrag zu schreiben. Andere Trace-Listener sind verfügbar, wie beispielsweise:
- **ConsoleTraceListener** schreibt Protokolle in der Konsole angezeigt.
- Die Methode in der [Cloud Diagnose - Steuerelement übernehmen der Protokollierung werden und Verfolgung in Windows Azure](https://msdn.microsoft.com/en-us/magazine/ff714589.aspx)beschrieben. Diese Methode wird die Microsoft.WindowsAzure.Diagnostics verwendet. **DiagnosticMonitorTraceListener**. Zusätzliche Ressourcen Azure finden Sie hier:
    - [Aktivieren Sie das Diagnoseprotokoll für Azure-Websites](http://azure.microsoft.com/en-us/documentation/articles/web-sites-enable-diagnostic-log/)
    - [Problembehandlung von Azure Websites in Visual Studio](http://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

Es wird dringend empfohlen, den gleichen Ansatz für die Protokollierung für den benutzerdefinierten Zeitgeberauftrag Code verwenden, wie für den Timer Job-Framework. In Ihrem Code Zeitgeberauftrag können die Plug & Play-Core `Log` Klasse:

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
{
    try
    {
        string library = "";

        // Get the number of admins
        var admins = e.WebClientContext.Web.GetAdministrators();

        Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

        // Additional Timer Job logic...

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
