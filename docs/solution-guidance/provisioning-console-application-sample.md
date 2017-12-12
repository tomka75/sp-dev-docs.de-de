---
title: Beispiel einer Anwendung in Konsole-Bereitstellung
ms.date: 11/03/2017
ms.openlocfilehash: f55962b55972312a421b8e153221f8b73bcf76b8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="provisioning-console-application-sample"></a>Beispiel einer Anwendung in Konsole-Bereitstellung

Grundlagen Sie der Verwendung des Plug & Play-provisioning-Moduls zum Erstellen und beibehalten, und wenden Sie dann provisioning Vorlagen für neue SharePoint-Websitesammlungen.

Um das neue Add-In-Modell zu unterstützen, hat die Anwendung Office 365 Developer Mustern und Methoden (Plug & Play-) einer Bereitstellung Framework eingeführt, das ermöglicht es Benutzern, benutzerdefinierte Websitevorlagen erstellen, indem Sie einfach auf den in einem Website-Modell, das Modell als provisioning Vorlage beibehalten, und klicken Sie dann die benutzerdefinierte Vorlage für neue oder vorhandene Websitesammlungen übernehmen, je nach Bedarf.

In diesem Beispiel erstellen wir eine grundlegende Konsolenanwendung, die Klassen in der Bereitstellung Plug & Play-Hauptbibliothek das Bereitstellung Plug & Play-Modul für die Durchführung dieser Bereitstellung wichtige Aufgaben aktiviert implementiert wird: 

- Entwerfen und modellieren einer Website Anpassungstools. Dies kann ein neues Design der Website sein, oder Sie können zu einer vorhandenen Website zeigen und als provisioning Vorlage zu speichern.
    
- Speichern und das Modell für die Website als Vorlage provisioning beibehalten von, damit Sie wiederverwendet werden können.
    
- Die Bereitstellung Vorlage auf einer neuen oder vorhandenen Websitesammlung anzuwenden.
    
> [!NOTE] 
> Diese exemplarische Vorgehensweise ist eine Ergänzung zu einer Stichprobe, die derzeit auf GitHub: [Erste Schritte mit der Plug & Play-Bereitstellung Engine](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Framework.Console). Den Code (Program.cs) und die Lösungsdateien für das Beispiel stehen zum Download zur Verfügung. Auch steht eine 20 Minuten video Präsentation dieses Prozesses (mit geringfügig Code) auf der Website Microsoft Channel 9: [Erste Schritte mit der Plug & Play-Bereitstellung Engine](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine).

## <a name="remote-provisioning-walkthrough"></a>Remote provisioning Exemplarische Vorgehensweise

Erstellen Sie zunächst ein Visual Studio-Projekt. In diesem Beispiel zur Vereinfachung erstellen wir eine standardkonsolenanwendung, die die Plug & Play-Bereitstellung Engine mithilfe der Plug & Play-Hauptbibliothek provisioning Framework implementiert. Um die beispiellösung zu unterstützen, müssen wir jedoch herunterladen und installieren die Bereitstellung Framework Plug & Play-Kern-Bibliothek. Führen Sie die Anweisungen zur Folge.

### <a name="create-and-prepare-a-visual-studio-project"></a>Erstellen und Vorbereiten eines Visual Studio-Projekts

1. Starten Sie Visual Studio, und wählen Sie dann **Datei** > **New** > **Projekt**.
    
2. Assistenten **Neues Projekt** wählen Sie **Visual c#**, und wählen Sie dann **Konsolenanwendung**.
    
3. Nennen Sie das Projekt "Programm", und klicken Sie dann auf **OK**. (Sie können das Projekt einen beliebigen, aber beim Beachten Sie, dass dieser exemplarischen Vorgehensweise verweisen Sie auf den Projektnamen als "Program." wird, Namen)
    
4. Herunterladen und installieren Sie die Plug & Play-Core-Bibliothek, die als ein NuGet-Paket zur Verfügung steht: [OfficeDevPnP.Core Pakete](https://www.nuget.org/profiles/officedevpnp).
    
    > [!NOTE] 
    > Es gibt zwei Versionen der Kernbibliothek. Eine Version ist der **OfficeDevPnP.Core** -Bibliothek, die SharePoint Online und Office 365 beruht. Die zweite Version ist **OfficeDevPnP.Core (lokal)**, die SharePoint 2013 lokal beruht. Hier ist ein Screenshot der verfügbaren Optionen aus.

    ![Zwei zentrale Bibliothek Download-Optionen](media/provisioning-console-application-sample/5b1adb8d-52e5-4c67-8792-6ef0ae41d655.png)

Im folgenden Beispiel wird die erste Option in SharePoint Online-Ziel verwendet.

1. Installieren Sie zuerst den NuGet-Client durch das Aufrufen der [NuGet-Clientinstallationsprogramm](http://docs.nuget.org/consume/installing-nuget).

2. Nach der NuGet ist führen Sie den **NuGet-Paket-Manager-**Client installiert. Maustaste auf den Knoten **Verweise** im Visual Studio- **Projektmappen-Explorer**, und wählen Sie dann **NuGet-Pakete verwalten**aus.

3. Wählen Sie im Paket-Manager **Online**, klicken Sie dann **EntityFramework**, und geben Sie den Suchbegriff "OfficeDev", um die Bibliothek OfficeDevPnP.Core verfügbar zu machen.

4. Führen Sie die Schritte zum Herunterladen und Installieren der **OfficeDevPnP.Core** -Bibliothek nach der angegebenen Richtung.

   Nachdem die Plug & Play-Core-Bibliothek in Visual Studio-Projekt verwiesen wird, werden alle Bibliotheksmitglieder als [Erweiterungsmethoden](https://msdn.microsoft.com/en-us/library/bb383977.aspx) für vorhandene Objektinstanzen, zum **Beispiel, **Web** und** Listeninstanzen zur Verfügung.

5. Stellen Sie sicher, dass Ihre Datei Program.cs die folgenden enthält `using` Anweisungen.

    ```c#
    using Microsoft.SharePoint.Client;
    using OfficeDevPnP.Core.Framework.Provisioning.Connectors;
    using OfficeDevPnP.Core.Framework.Provisioning.Model;
    using OfficeDevPnP.Core.Framework.Provisioning.ObjectHandlers;
    using OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml;
    using System;
    using System.Net;
    using System.Security;
    using System.Threading;
    ```

**Nachdem wir das Projekt eingerichtet haben**

Nachdem Sie Ihrem Projekt eingerichtet haben, können Sie Ihre websiteanpassungen erstellen. Sie können dies manuell tun oder zeigen Sie auf einer Website, deren Design verwendet werden soll. Speichern Sie den Entwurf der gewünschten Website einfach als provisioning Vorlage. Oder Sie können eine Mischung aus beiden Ansätze verwenden. Für dieses Beispiel wird es einfach zu einer vorhandenen Website, und speichern Sie die zusammengesetztes Design und websiteartefakte (nicht jedoch seinen Inhalt) als provisioning Vorlage verweisen.

Zunächst müssen wir für die Verbindung zu der Website, die wir als Grundlage unserer Vorlage provisioning modellieren möchten. Zunächst Sammeln der Verbindungsinformationen, einschließlich Benutzername, Kennwort und die Quell-URL.

### <a name="create-and-extract-and-persist-the-provisioning-template"></a>Erstellen und extrahieren und die Bereitstellung Vorlage beibehalten

1. Sammeln von Informationen zur Verbindung vom Benutzer. Beachten Sie, dass in der Anwendung `Main` routinemäßige, wir drei einfachen Dinge tun: Sammeln der Verbindungsinformationen, die Bereitstellung Vorlage erhalten möchten, und die Bereitstellung Vorlage anwenden. Die schwierigsten wird von den Methoden **GetProvisioningTemplate** und **ApplyProvisioningTemplate** durchgeführt, die wir unten definieren.
    
    ```C#
    static void Main(string[] args)
        {
            ConsoleColor defaultForeground = Console.ForegroundColor;
    
            // Collect information 
            string templateWebUrl = GetInput("Enter the URL of the template site: ", false, defaultForeground);
            string targetWebUrl = GetInput("Enter the URL of the target site: ", false, defaultForeground);
            string userName = GetInput("Enter your user name:", false, defaultForeground);
            string pwdS = GetInput("Enter your password:", true, defaultForeground);
            SecureString pwd = new SecureString();
            foreach (char c in pwdS.ToCharArray()) pwd.AppendChar(c);
    
            // GET the template from existing site and serialize
            // Serializing the template for later reuse is optional
            ProvisioningTemplate template = GetProvisioningTemplate(defaultForeground, templateWebUrl, userName, pwd);
    
            // APPLY the template to new site from 
            ApplyProvisioningTemplate(defaultForeground, targetWebUrl, userName, pwd, template);
    
            // Pause and modify the UI to indicate that the operation is complete
            Console.ForegroundColor = ConsoleColor.White;
            Console.WriteLine("We're done. Press Enter to continue.");
            Console.ReadLine();
        }
    ```

2. Erstellen Sie und verwenden Sie eine private **GetInput** -Methode, um die erforderlichen Anmeldeinformationen abzurufen.
    
    ```c#
    private static string GetInput(string label, bool isPassword, ConsoleColor defaultForeground)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine("{0} : ", label);
            Console.ForegroundColor = defaultForeground;
    
            string value = "";
    
            for (ConsoleKeyInfo keyInfo = Console.ReadKey(true); keyInfo.Key != ConsoleKey.Enter; keyInfo = Console.ReadKey(true))
            {
                if (keyInfo.Key == ConsoleKey.Backspace)
                {
                    if (value.Length > 0)
                    {
                        value = value.Remove(value.Length - 1);
                        Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                        Console.Write(" ");
                        Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                    }
                }
                else if (keyInfo.Key != ConsoleKey.Enter)
                {
                    if (isPassword)
                    {
                        Console.Write("*");
                    }
                    else
                    {
                        Console.Write(keyInfo.KeyChar);
                    }
                    value += keyInfo.KeyChar;
    
                }
    
            }
            Console.WriteLine("");
    
            return value;
        }
    ```

3. Zeigen Sie auf der Website, die das Modell für die Bereitstellung der Grundlage unserer Vorlage ist. Während der GET auf der Quellwebsite mit einer einzelnen Codezeile, sehen Sie sich `GetProvisioningTemplate()`, der GET-Methode, die wir definiert. 
    
    ```c#
    private static ProvisioningTemplate GetProvisioningTemplate(ConsoleColor defaultForeground, string webUrl, string userName, SecureString pwd)
        {
            using (var ctx = new ClientContext(webUrl))
            {
                // ctx.Credentials = new NetworkCredentials(userName, pwd);
                ctx.Credentials = new SharePointOnlineCredentials(userName, pwd);
                ctx.RequestTimeout = Timeout.Infinite;
    
                // Just to output the site details
                Web web = ctx.Web;
                ctx.Load(web, w => w.Title);
                ctx.ExecuteQueryRetry();
    
                Console.ForegroundColor = ConsoleColor.White;
                Console.WriteLine("Your site title is:" + ctx.Web.Title);
                Console.ForegroundColor = defaultForeground;
    
                ProvisioningTemplateCreationInformation ptci
                        = new ProvisioningTemplateCreationInformation(ctx.Web);
    
                // Create FileSystemConnector to store a temporary copy of the template 
                ptci.FileConnector = new FileSystemConnector(@"c:\temp\pnpprovisioningdemo", "");
                ptci.PersistComposedLookFiles = true;
                ptci.ProgressDelegate = delegate(String message, Int32 progress, Int32 total)
                {
                    // Only to output progress for console UI
                    Console.WriteLine("{0:00}/{1:00} - {2}", progress, total, message);
                };
    
                // Execute actual extraction of the template
                ProvisioningTemplate template = ctx.Web.GetProvisioningTemplate(ptci);
    
                // We can serialize this template to save and reuse it
                // Optional step 
                XMLTemplateProvider provider =
                        new XMLFileSystemTemplateProvider(@"c:\temp\pnpprovisioningdemo", "");
                provider.SaveAs(template, "PnPProvisioningDemo.xml");
    
                return template;
            }
        }
    ```

    Im obigen Codeausschnitt definiert wir auch eine Variable, **ProvisioningTemplateCreationInformation** - **Pcti**. Die Variable liefert uns die Option zum Speichern von Informationen über Artefakte, die zusammen mit der Vorlage gespeichert werden können.
    
4. Erstellen Sie ein File System Connector-Objekt, sodass wir eine temporäre Kopie der Bereitstellung Vorlage speichern können, die wir zu einer anderen Website anwenden möchten.
    
    > [!NOTE] 
    > Dieser Schritt ist optional. Es ist nicht erforderlich, dass Sie die Bereitstellung Vorlage XML serialisieren. Zu diesem Zeitpunkt ist die Vorlage einfach C#-Code. Nicht nur Serialisierung optional ist, sondern auch können Serialisierungsformat werden soll.

5. Führen Sie die Extrahierung der Bereitstellung Vorlage mithilfe von nur diese einzelnen Codezeile.      `ProvisioningTemplate template = ctx.Web.GetProvisioningTemplate(ptci);`
    
6. (Optional) Speichern Sie und speichern Sie eine serialisierte Version der Bereitstellung Vorlage zu, damit Sie wiederverwendet werden können. Sie können die Bereitstellung Vorlage in Standarddateiformate serialisieren gewünschte. In diesem Beispiel haben wir in eine XML-Datei mit dem Namen **PnPProvisioningDemo.xml**serialisiert. Die Datei selbst ist ein **XMLFileSystemTemplateProvider** -Objekt für die wir einen Speicherort im Dateisystem bereitgestellt haben.
    
**Nachdem wir extrahieren, speichern und die Bereitstellung Vorlage beibehalten**

Nachdem wir extrahieren, speichern und die Bereitstellung Vorlage beibehalten, ist der nächste und letzte Schritt der Bereitstellung Vorlage auf einer neuen SharePoint-Websitesammlung an, mit der **ApplyProvisioningTemplate** -Methode.

### <a name="apply-the-provisioning-template-to-a-new-or-existing-site"></a>Wenden Sie die Bereitstellung Vorlage zu einer neuen oder vorhandenen Website

1. Anmeldeinformationen für die Zielwebsite zu erhalten.
    
    ```c#
    // ctx.Credentials = new NetworkCredentials(userName, pwd);
                ctx.Credentials = new SharePointOnlineCredentials(userName, pwd);
                ctx.RequestTimeout = Timeout.Infinite;
    ```

2. Erfassen Sie websiteartefakte, die mit der **ProvisioningTemplateCreationInformation** -Methode mit der **ProvisioningTemplateApplyingInformation**-Methode Companion gespeichert wurden.
    
    ```c#
    ProvisioningTemplateApplyingInformation ptai
                        = new ProvisioningTemplateApplyingInformation();
                ptai.ProgressDelegate = delegate(String message, Int32 progress, Int32 total)
                {
                    Console.WriteLine("{0:00}/{1:00} - {2}", progress, total, message);
                };
    ```

3. Rufen Sie eine Zuordnung und der Datei-Konnektor für die Objekte.
    
    ```c#
    // Associate file connector for assets
                FileSystemConnector connector = new FileSystemConnector(@"c:\temp\pnpprovisioningdemo", "");
                template.Connector = connector;
    
    ```

4. (Optional) Da Bereitstellung eine Objektinstanz verwendet wird, können wir Code, um websiteartefakte dynamisch anpassen schreiben. In diesem Fall haben wir eine neue "Kontaktliste" hinzufügen.
    
    ```c#
    // Since template is actual object, we can modify this using code as needed
                template.Lists.Add(new ListInstance()
                {
                    Title = "PnP Sample Contacts",
                    Url = "lists/PnPContacts",
                    TemplateType = (Int32)ListTemplateType.Contacts,
                    EnableAttachments = true
                });
    ```

5.  Anzuwenden Sie die Bereitstellung Vorlage auf die neue Website erneut mit einer Codezeile.
    
    ```c#
        web.ApplyProvisioningTemplate(template, ptai);
    ```

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [Plug & Play-Bereitstellung framework](pnp-provisioning-framework.md)
    
- [Plug & Play-Bereitstellung Modul- und die Core-Bibliothek](pnp-provisioning-engine-and-the-core-library.md)
