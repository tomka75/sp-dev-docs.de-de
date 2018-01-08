---
title: "Erstellen eines vollständigen SharePoint-Websitedesigns mithilfe des PnP-Bereitstellungsmoduls"
description: "Erstellen eines vollständigen SharePoint-Websitedesigns mithilfe des PnP-Bereitstellungsmoduls"
ms.date: 12/14/2017
ms.openlocfilehash: 303aca9f0103634e247ec75a0323321a77709113
ms.sourcegitcommit: 28690b54f1ef7c811d64393d2eaaff0a8635cc72
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="calling-the-pnp-provisioning-engine-from-a-site-script"></a>Aufrufen des PnP-Bereitstellungsmoduls aus einem Websiteskript

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich derzeit in der Vorschau und können ohne vorherige Ankündigung geändert werden. Sie werden in Produktionsumgebungen derzeit nicht unterstützt.

Websitedesigns bieten eine hervorragende Möglichkeit, das Aussehen und Verhalten Ihrer Websitesammlungen zu standardisieren. Wenn Sie jedoch noch einen Schritt weitergehen möchten, indem Sie beispielsweise jeder Seite eine Fußzeile hinzufügen, werden Sie feststellen, dass Websitedesigns diese Option nicht bieten. Mit dem PnP-Bereitstellungsmodul können Sie eine Vorlage erstellen, mit der Sie einen Application Customizer für eine Website bereitstellen können. Dieser Application Customizer kann dann auf jeder Seite eine Fußzeile registrieren. In diesem Artikel erfahren Sie, wie ein Websitedesign erstellt wird, das eine PnP-Bereitstellungsvorlage auf eine Website anwendet, die wiederum einen Application Customier zum Rendern einer Fußzeile hinzufügt.

In unserem Setup werden die folgenden Komponenten verwendet:

1. Ein Websitedesign und ein Websiteskript
1. Ein Microsoft-Fluss
1. Eine Azure-Speicherwarteschlange
1. Eine Azure-Funktion
1. Eine SPFX-Lösung
1. Eine PnP-Bereitstellungsvorlage
1. Ein PnP-PowerShell-Skript
1. Eine AppID und ein AppSecret mit Verwaltungsrechten auf Ihrem Mandanten.

Wir benötigen alle diese Komponenten, damit wir den PnP-Bereitstellungscode in kontrollierter Weise auslösen können, direkt nachdem die Website erstellt und das Websitedesign angewendet wurde.

## <a name="setting-up-app-only-access-to-your-tenant"></a>Einrichten des Nur-App-Zugriffs auf Ihren Mandanten

Hierfür müssen Sie zwei unterschiedliche Seiten auf Ihrem Mandanten öffnen, eine, die sich in einer normalen Website befindet, und eine andere, die sich in Ihrer SharePoint-Administrationswebsite befindet.

1. Navigieren Sie zu der folgenden URL in Ihrem Mandanten: https://[IhrMandant].sharepoint.com/_layouts/appregnew.aspx (Sie können zu einer beliebigen Website navigieren, aber vorerst sollten Sie die Stammwebsite auswählen).
1. Klicken Sie auf die beiden Schaltflächen **Generieren**.
1. Geben Sie einen Titel für Ihre App ein, z. B. „Websitebereitstellung“.
1. Geben Sie als App-Domäne **localhost** ein.
1. Geben Sie für den Umleitungs-URI **https://localhost** ein.

    ![App erstellen](images/pnpprovisioning-createapponly.png)

1. Klicken Sie auf **Erstellen**, und kopieren Sie die Werte für **Client-ID** und **Geheimer Clientschlüssel**, da Sie diese später benötigen.

Nun vertrauen wir dieser App, dass sie über den entsprechenden Zugriff auf Ihren Mandanten verfügt:
1. Navigieren Sie zu „https://[IhrMandant]-admin.sharepoint.com/_layouts/appinv.aspx“ (beachten Sie den Abschnitt „-admin“ in der URL).
1. Fügen Sie die oben kopierte Client-ID in das Feld **App-ID**, und wählen Sie **Nachschlagen** aus.
1. Fügen Sie den folgenden XML-Code in das Feld **Berechtigungsanforderungs-XML** ein.

    ```xml
    <AppPermissionRequests AllowAppOnlyPolicy="true" >
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
    </AppPermissionRequests>
    ```

1. Wählen Sie **Erstellen** aus.
1. Es wird die Frage angezeigt, ob Sie der App vertrauen möchten. Bestätigen Sie dies, indem Sie **Vertrauen** auswählen.


## <a name="creating-the-azure-storage-queue"></a>Erstellen der Azure-Speicherwarteschlange

In diesem Szenario verwenden wir eine Azure-Speicherwarteschlange, um Nachrichten von einem Microsoft-Flow zu empfangen. Jedes Mal, wenn eine Nachricht in der Speicherwarteschlange angezeigt wird, wird eine Azure-Funktion zum Ausführen eines PowerShell-Skripts ausgelöst. Lassen Sie uns aber zunächst die Speicherwarteschlange einrichten:

1. Navigieren Sie zum Azure-Portal unter „https://portal.azure.com“, und melden Sie sich an.
1. Wählen Sie **+Neu** aus.
1. Wählen Sie aus den Azure Marketplace-Angeboten **Speicher** aus, und wählen Sie in der Spalte „Unterstützt“ **Speicherkonto – Blob, Datei, Tabelle, Warteschlange**
1. Geben Sie für die erforderlichen Felder entsprechende Werte ein. Wählen Sie unbedingt **An Dashboard anheften** aus, um die Option später leichter zu finden, und klicken Sie auf **Erstellen**. Das Speicherkonto wird erstellt. Das kann einige Minuten dauern.
1. Öffnen Sie das Speicherkonto, nachdem es erstellt wurde, und navigieren Sie in der Navigation zu **Warteschlangen**
1. Wählen Sie oben im Hauptbereich des Bildschirms **+ Warteschlange** aus.
1. Geben Sie **pnpprovisioningqueue** als Name ein, oder geben Sie einen eigenen Namen gemäß dem erzwungenen Benennungsstandard ein. Notieren Sie sich den Warteschlangennamen, da Sie diesen Wert später beim Erstellen der Azure-Funktion benötigen.
1. Navigieren Sie zu **Zugriffsschlüssel**, und notieren Sie sich den **Speicherkontonamen** und den **key1-Schlüsselwert**, da Sie diese Werte im nächsten Schritt beim Erstellen des Flusses benötigen.


## <a name="the-flow"></a>Der Fluss

Um eine Nachricht in der Warteschlange zu platzieren, müssen Sie einen Fluss erstellen. 

1. Navigieren Sie zu **https://flow.microsoft.com**, melden Sie sich an, und erstellen Sie einen neuen Fluss, indem Sie oben auf  **Ohne Vorlage erstellen** klicken.
1. Klicken Sie auf **Hunderte von Connectors und Triggern durchsuchen**, um den Auslöser auszuwählen.
1. Suchen Sie nach **Anforderung**, und wählen Sie **Anforderung - Beim Empfang einer HTTP-Anforderung** aus.
1. Geben Sie den folgenden JSON-Code als Anforderungstext ein:

    ```json
    {
        "type": "object",
        "properties": {
            "webUrl": {
                "type": "string"
            },
            "parameters": {
                "type": "object",
                "properties": {
                    "event": {
                        "type": "string"
                    },
                    "product": {
                        "type": "string"
                    }
                }
            }
        }
    }
    ``` 

1. Wählen Sie **+ Neuer Schritt** aus, und klicken Sie dann auf **Aktion hinzufügen**.
1. Suchen Sie nach **Azure-Warteschlangen**, und wählen Sie **Azure-Warteschlangen - Nachricht in einer Warteschlange ablegen** aus.
1. Geben Sie einen beliebigen aussagekräftigen Namen für die Verbindung ein. 
1. Geben Sie den Speicherkontonamen ein, den Sie im vorherigen Abschnitt kopiert haben.
1. Geben Sie den freigegebenen Speicherschlüssel ein, bei dem es sich um den Wert des **Key1-Schlüsselwerts** Ihres Speicherkontos handelt.
1. Klicken Sie auf **Erstellen**.
1. Wählen Sie **pnpprovisioningqueue** als Warteschlangenname aus.
1. In dem in Schritt 4 angegebenen Text haben wir einen eingehenden Parameter mit dem Namen „webUrl“ angegeben. Wir werden den Wert dieses Parameters in der Warteschlange ablegen. Klicken Sie in das Feld **Nachricht**, und wählen Sie aus der Auswahl für dynamische Inhalte **webUrl** aus.
1. Klicken Sie auf **Flow speichern**. Daraufhin wird die URL generiert, die wir im nächsten Schritt kopieren werden.
1. Klicken Sie auf den ersten Schritt in Ihrem Flow („Beim Empfang einer HTTP-Anforderung), und kopieren Sie die URL. Wir benötigen diese, um zum späteren Testen in unserem Websitedesign.
1. Speichern Sie Ihren Flow.

Dieser sollte wie folgt aussehen:

![Hyperion](images/pnpprovisioning-flow-overview.png)

## <a name="testing-the-flow"></a>Testen des Flows

Um Ihren Flow zu testen, müssen Sie eine POST-Anforderung stellen. Am einfachsten ist hierfür auf einem Windows-Computer die Verwendung von PowerShell:

```powershell
$uri = "[the URI you copied in step 8 when creating the flow]"
$body = "{webUrl:'somesiteurl'}
Invoke-RestMethod -Uri $uri -Method Post -ContentType "application/json" -Body $body
```

Wenn Sie nun zum Hauptbildschirm des Flows navigieren, sehen Sie einen Ausführungsverlauf. Wenn alles ordnungsgemäß verlief, sollte dieser „Succeeded“ lauten.
Navigieren Sie nun zur Warteschlange, die Sie soeben in Azure erstellt haben, und klicken Sie auf **Aktualisieren**. Es sollte ein Eintrag vorhanden sein, der angibt, dass Sie den Flow korrekt aufgerufen haben.

## <a name="provision-the-spfx-solution"></a>Bereitstellen der SPFX-Lösung

Für diese exemplarische Vorgehensweise verwenden wir eine vorhandene SPFX-Lösung, die unter „https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer“ verfügbar ist.

Befolgen Sie die Schritte wie in der „README.MD“, die in diesem Repository verfügbar ist, um die Lösung zu erstellen und bereitzustellen.

# <a name="create-a-pnp-provisioning-template"></a>Erstellen einer PnP-Bereitstellungsvorlage

Kopieren Sie den folgenden XML-Code in eine neue Datei, und speichern Sie die Datei als „FlowDemoTemplate.xml“

```xml
<?xml version="1.0"?>
<pnp:Provisioning xmlns:pnp="http://schemas.dev.office.com/PnP/2017/05/ProvisioningSchema">
  <pnp:Preferences Generator="OfficeDevPnP.Core, Version=2.20.1711.0, Culture=neutral, PublicKeyToken=3751622786b357c2" />
  <pnp:Templates ID="CONTAINER-FLOWDEMO">
    <pnp:ProvisioningTemplate ID="TEMPLATE-FLOWDEMO" Version="1" BaseSiteTemplate="GROUP#0" Scope="RootSite">
      <pnp:CustomActions>
        <pnp:WebCustomActions>
          <pnp:CustomAction Name="spfx-react-app-customizer" Description="Custom action for Application Customizer" Location="ClientSideExtension.ApplicationCustomizer" Title="spfx-react-app-customizer" Sequence="0" Rights="" RegistrationType="None" ClientSideComponentId="67fd1d01-84e8-4fbf-85bd-4b80768c6080" ClientSideComponentProperties="{&quot;SourceTermSetName&quot;:&quot;Regions&quot;}" />
        </pnp:WebCustomActions>
      </pnp:CustomActions>
    </pnp:ProvisioningTemplate>
</pnp:Provisioning>
```

> [!NOTE]
> Die Vorlage fügt eine benutzerdefinierte Aktion zu dem Web hinzu, auf das sie angewendet wird. Sie verweist auf „ClientSideComponentId“, die aus der SPFX-Lösung stammt, die Sie zuvor bereitgestellt haben. Wenn Sie diese Demo mit Ihrer eigenen SPFX-Lösung ausführen, müssen Sie die „ClientSideComponentId“ und optional die Attributwerte „ClientSideComponentProperties“ in der XML ändern.

## <a name="create-the-azure-function"></a>Erstellen der Azure-Funktion

1. Navigieren Sie zum Azure-Portal unter „https://portal.azure.com“.
1. Suchen Sie nach „Funktionen-App“, und erstellen Sie eine neue Funktionen-App. Wählen Sie im Feld **Speicher** die Option, dass das vorhandene Speicherkonto ****verwendet wird, und wählen Sie das zuvor erstellte Speicherkonto aus. Legen Sie die anderen Werte wie erforderlich fest.
1. Nachdem die Funktionen-App erstellt wurde, öffnen Sie sie, und wählen Sie **Funktionen** und dann **Neue Funktion** aus.

  ![Erstellen einer neuen Funktion](images/pnpprovisioning-create-function.png)

1. Wählen Sie aus der Dropdownliste „Sprache“ die Option **PowerShell** aus.
1. Wählen Sie **QueueTrigger - PowerShell** aus.
1. Geben Sie der Funktion den Namen **ApplyPnPProvisioningTemplate**. 
1. Geben Sie den Namen der Warteschlange ein, die Sie in den vorherigen Schritten erstellt haben.
1. Wählen Sie **Erstellen** aus.
1. Es wird ein Editor angezeigt, in dem Sie PowerShell-Cmdlets eingeben können. Wir laden nun das PnP-PowerShell-Modul hoch, damit wir es in der Azure-Funktion verwenden können.

## <a name="uploading-pnp-powershell-for-your-azure-function"></a>Hochladen von PnP-PowerShell für Ihre Azure-Funktion

Wir müssen zuerst das PnP-PowerShell-Modul herunterladen, damit es später einfach hochgeladen werden kann.

1. Erstellen sie einen temporären Ordner auf Ihrem Computer.
1. Starten Sie PowerShell.
    ```powershell
    Save-Module -Name SharePointPnPPowerShellOnline -Path [pathtoyourfolder]
    ```
1. Die PowerShell-Moduldateien werden in einen Ordner innerhalb des soeben ausgewählten Ordners heruntergeladen. 

Nun können Sie diese Dateien hochladen, damit die Azure-Funktion das Modul verwenden kann.

1. Navigieren Sie zur Hauptseite der Funktionen-App, und wählen Sie **Plattformfeatures** aus.

    ![Navigieren Sie zu „Plattformfeatures“.](images/pnpprovisioning-platform-features.png)

1. Wählen Sie **Erweiterte Tools (Kudu)** aus.

    ![Wählen Sie „Erweiterte Tools (Kudu)“ aus.](images/pnpprovisioning-select-kudu.png)

1. Wählen Sie auf der Kudu-Hauptseite **Debugging-Konsole** aus, und klicken Sie entweder auf **CMD** oder auf **PowerShell**.
1. Im oberen Teil der Seite wird ein Datei-Explorer angezeigt. Navigieren Sie zu **site\wwwroot\\[NameIhrerAzure-Funktion]**
1. Erstellen Sie einen neuen Ordner, und geben Sie diesem den Namen **modules**.
    
    ![Neuen Ordner erstellen](images/pnpprovisioning-kudu-create-folder.png)

1. Erstellen Sie in diesem Ordner einen weiteren Ordner mit dem Namen **SharePointPnPPowerShellOnline**, und navigieren Sie zu dem Ordner.
1. Navigieren Sie im Datei-Explorer auf Ihrem Computer zu dem Ordner, aus dem Sie alle PnP-PowerShell-Moduldateien heruntergeladen haben. Öffnen Sie den Ordner **SharePointPnPPowerShellOnline\2.20.1711.0** (beachten Sie, dass die Versionsnummer anders sein kann, wenn Sie diese exemplarische Vorgehensweise befolgen).
1. Laden Sie alle Dateien in diesen Ordner hoch, indem Sie alle Dateien aus dem Ordner in den Ordner in Kudu ziehen und dort ablegen.

   ![Neuen Ordner erstellen](images/pnpprovisioning-module-files-uploaded.png)

## <a name="finishing-the-azure-function"></a>Abschließen der Azure-Funktion

1. Navigieren Sie zurück zur Azure-Funktion, und erweitern Sie die Registerkarte „Dateien“ rechts.

    ![Dateien anzeigen](images/pnpprovisioning-view-files.png)

1. Klicken Sie auf **Hochladen**, und laden Sie Ihre Bereitstellungsvorlagendatei hoch, die Sie zuvor erstellt haben.
1. Ersetzen Sie das PowerShell-Skript durch Folgendes:

```powershell
$in = Get-Content $triggerInput -Raw
Write-Output "Incoming request for '$in'"
Connect-PnPOnline -AppId $env:SPO_AppId -AppSecret $env:SPO_AppSecret -Url $in
Write-Output "Connected to site"
Apply-PnPProvisioningTemplate -Path D:\home\site\wwwroot\ApplyPnPProvisioningTemplate\FlowDemoTemplate.xml
```

Beachten Sie, dass wir zwei Umgebungsvariablen verwenden, eine mit dem Namen ```SPO_AppId```, die andere mit dem Namen ```SPO_AppSecret```. Um diese Variablen festzulegen, navigieren Sie zur Hauptseite der Funktionen-App in Ihrem Azure-Portal, wählen Sie **Anwendungseinstellungen** aus, und fügen Sie zwei neue Anwendungseinstellungen hinzu:

1. ```SPO_AppId```: Legen Sie den Wert auf die im ersten Schritt beim Erstellen der App auf dem Mandanten kopierte Client-ID fest.
2. ```SPO_AppSecret```: Legen Sie den Wert auf den im ersten Schritt beim Erstellen der App auf dem Mandanten kopierten geheimen Clientschlüssel fest.

## <a name="creating-the-site-design"></a>Erstellen des Websitedesigns

Öffnen Sie PowerShell, und vergewissern Sie sich, dass Sie die Microsoft Office 365-Verwaltungsshell installiert haben.

Stellen Sie zuerst über Connect-SPOService eine Verbindung zu Ihrem Mandanten her:

```powershell
Connect-SPOService -Url https://[yourtenant]-admin.sharepoint.com
```

Nun können Sie die vorhandenen Websitedesigns abrufen. 

```powershell
Get-SPOSiteDesign
```

Um ein Websitedesign zu erstellen, müssen Sie zuerst ein Websiteskript erstellen. Ein Websitedesign können Sie sich als Container vorstellen, der auf ein oder mehrere Webskripts verweist.
1. Kopieren Sie den folgenden JSON-Code in die Zwischenablage, und ändern Sie ihn. Legen Sie die url-Eigenschaft auf den beim Erstellen des Flows kopierten Wert fest. Die URL sieht wie `https://prod-27.westus.logic.azure.com:443/workflows/ef7434cf0d704dd48ef5fb6...oke?api-version=2016-06-01&sp=%2Ftriggers%2Fmanual%2Frun` aus.

    ```json
    {
        "$schema": "schema.json",
        "actions": [
           {
                "verb": "triggerFlow",
                "url": "[paste the workflow trigger URL here]",
                "name": "Apply Template",
                "parameters": {
                    "event":"",
                    "product":""
                }
           }
        ],
        "bindata": {},
        "version": 1
    }
    ```

1. Nach dem Bearbeiten des JSON-Codes durch Einfügen der korrekten URL zum Auslösen des Flows, wählen Sie alles aus, und kopieren alles erneut in die Zwischenablage.
1. Öffnen Sie PowerShell, und geben Sie Folgendes ein, um das Skript in eine Variable zu kopieren und das Websiteskript zu erstellen.

    ```powershell
    $script = Get-Clipboard -Raw
    Add-SPOSiteScript -Title "Apply PnP Provisioning Template" -Content $script
    Get-SPOSiteScript
    ```

1. Es sollte eine Liste mit einem oder mehreren Skripts angezeigt werden, einschließlich des soeben erstellten Websiteskripts.
1. Wählen Sie die ID des soeben erstellten Websiteskripts aus, und kopieren Sie sie in die Zwischenablage.
1. Erstellen Sie das Websitedesigns:

    ```powershell
    Add-SPOSiteDesign -Title "Site with footer" -SiteScripts [Paste the ID of the Site Script here] -WebTemplate "64"
    ```

Durch „ Add-SPOSiteDesign“ wird das Websitedesign der Teamwebsite zugewiesen. Wenn Sie das Design einer Kommunikationswebsite zuweisen möchten, verwenden Sie „68“.

## <a name="conclusion"></a>Schlussbemerkung

Nachdem Sie die Speicherwarteschlange erstellt haben, haben Sie die App-ID für den Nur-App-Zugriff erstellt. Anschließend haben Sie die Azure-Funktion und das Websitedesign erstellt und den korrekten Microsoft-Flow vom Websitedesign ausgelöst. Sie sind jetzt startklar! 

Versuchen Sie, eine neue Website zu erstellen, indem Sie zu Ihrem SharePoint-Mandanten navigieren. Wählen Sie **SharePoint**, **Website erstellen** und **Teamwebsite** aus. Ihr neu erstelltes Websitedesign sollte nun als mögliche Designoption angezeigt werden. Erstellen Sie Ihre Website, und beachten Sie das Websitedesign, das angewendet wird, nachdem die Website erstellt wurde.  Wenn Sie alles korrekt konfiguriert haben, sollte Ihr Flow nun ausgelöst werden. Sie können den Ausführungsverlauf des Flows überprüfen, um zu sehen, ob er korrekt ausgeführt wurde.  Da es etwas dauern kann, bis die PnP-Bereitstellungsvorlage angewendet wird, kann es sein, dass die Fußzeile nicht sofort angezeigt wird. Warten Sie einen Moment, und laden Sie die Website erneut.


