---
title: "Erstellen eines vollständigen SharePoint-Websitedesigns mithilfe des PnP-Bereitstellungsmoduls"
description: "Erstellen eines vollständigen SharePoint-Websitedesigns mithilfe des PnP-Bereitstellungsmoduls"
ms.date: 01/08/2018
ms.openlocfilehash: 102eec9fa09afa28bbdc5b40f73a9e254dd52bce
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="calling-the-pnp-provisioning-engine-from-a-site-script"></a>Aufrufen des PnP-Bereitstellungsmoduls über ein Websiteskript

> [!NOTE]
> Websitedesigns und Websiteskripts befinden sich derzeit in der Preview-Phase und können jederzeit geändert verwenden. Sie werden in Produktionsumgebungen derzeit nicht unterstützt.

Websitedesigns sind eine hervorragende Möglichkeit, das Aussehen und Verhalten Ihrer Websitesammlungen zu standardisieren. Bestimmte Dinge lassen sich mit Websitedesigns jedoch nicht umsetzen. Beispielsweise ist es nicht möglich, jeder Seite eine Fußzeile hinzuzufügen. Mit dem PnP-Bereitstellungsmodul können Sie eine Vorlage erstellen, mit der Sie einen Application Customizer für eine Website bereitstellen können. Ein solcher Application Customizer kann das Seitendesign aktualisieren und so beispielsweise eine Fußzeile auf jeder Seite registrieren. 

In diesem Artikel wird beschrieben, wie Sie ein Websitedesign erstellen können, das eine PnP-Bereitstellungsvorlage auf eine Website anwendet. Die Vorlage wird einen Application Customizer hinzufügen, der eine Fußzeile rendert.

In der Anleitung in diesem Artikel verwenden wir die folgenden Komponenten:

- Ein Websitedesign und ein Websiteskript
- Microsoft Flow
- Azure Queue-Speicher
- Eine Azure-Funktion
- Eine SharePoint-Framework-Lösung (SPFx-Lösung)
- Eine PnP-Bereitstellungsvorlage
- Ein PnP-PowerShell-Skript
- Eine App-ID und einen geheimen App-Schlüssel mit Administratorrechten in Ihrem Mandanten

Mithilfe dieser Komponenten wird der PnP-Bereitstellungscode ausgelöst, sobald Sie die Website erstellt und das Websitedesign angewendet haben.

## <a name="set-up-app-only-access-to-your-tenant"></a>Einrichten von App-exklusivem Zugriff auf Ihren Mandanten

Zur Einrichtung von App-exklusivem Zugriff benötigen Sie zwei unterschiedliche Seiten in Ihrem Mandanten: eine Seite auf der regulären Website und eine Seite auf Ihrer SharePoint-Administrationswebsite.

1. Rufen Sie in Ihrem Mandanten die folgende URL auf: `https://[yourtenant].sharepoint.com/_layouts/appregnew.aspx`. (Sie können jede beliebige Seite aufrufen; für dieses Tutorial verwenden wir hier die Stammwebsite.)
1. Klicken Sie neben den Feldern **Client-ID** und **Geheimer Clientschlüssel** jeweils auf die Schaltfläche **Generieren**.
1. Geben Sie einen Titel für Ihre App ein, beispielsweise „Site Provisioning“.
1. Geben Sie in das Feld **App-Domäne** die Zeichenfolge **localhost** ein.
1. Geben Sie in das Feld **Umleitungs-URI** die Adresse **https://localhost** ein.

    ![Seite „App erstellen“ mit den Feldern „Client-ID“, „Geheimer Clientschlüssel“, „Titel“, „App-Domäne“ und „Umleitungs-URI“](images/pnpprovisioning-createapponly.png)

1. Klicken Sie auf **Erstellen**. 
1. Notieren Sie sich die Werte für **Client-ID** und **Geheimer Clientschlüssel**. Sie werden sie später noch brauchen.

Stufen Sie nun die App als vertrauenswürdig ein, damit Sie die entsprechenden Zugriffsrechte für Ihren Mandanten hat:

1. Rufen Sie `https://[yourtenant]-admin.sharepoint.com/_layouts/appinv.aspx` auf. (Wichtig hierbei ist der Teil `-admin` in der URL.)
1. Fügen Sie in das Feld **App-ID** die **Client-ID** ein, die Sie sich notiert haben, und klicken Sie auf **Lookup**.
1. Fügen Sie den folgenden XML-Code in das Feld **Berechtigungsanforderungs-XML** ein:

    ```xml
    <AppPermissionRequests AllowAppOnlyPolicy="true" >
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
    </AppPermissionRequests>
    ```

1. Klicken Sie auf **Erstellen**.
1. Bestätigen Sie mit einem Klick auf **Trust It**, dass Sie der App vertrauen.


## <a name="create-the-azure-queue-storage"></a>Erstellen des Azure Queue-Speichers

In diesem Szenario verwenden wir Azure Queue-Speicher als Empfänger für Microsoft Flow-Nachrichten. Wann immer eine Nachricht im Queue-Speicher angezeigt wird, wird eine Azure-Funktion ausgelöst, die ein PowerShell-Skript ausführt. 

So richten Sie den Azure Queue-Speicher ein

1. Rufen Sie das [Azure-Portal](https://portal.azure.com) auf, und melden Sie sich an.
1. Klicken Sie auf **+ Neu**.
1. Wählen Sie aus den Azure Marketplace-Angeboten die Option **Storage** aus. Klicken Sie in der Spalte „Empfohlen“ auf **Speicherkonto – Blob, Datei, Tabelle, Warteschlange**.
1. Tragen Sie Werte in die Pflichtfelder ein. Klicken Sie auf **Pin to dashboard** und anschließend auf **Erstellen**. Es kann einige Minuten dauern, bis das Speicherkonto erstellt wird.
1. Öffnen Sie das Speicherkonto, und klicken Sie auf **Warteschlangen**.
1. Klicken Sie oben im Bildschirm auf **+ Warteschlange**.
1. Geben Sie als Namen **pnpprovisioningqueue** oder einen eigenen Wert ein. Beachten Sie dabei auf jeden Fall die Namenskonvention. Notieren Sie sich den Namen der Warteschlange; Sie benötigen diesen Wert, wenn Sie die Azure-Funktion erstellen.
1. Klicken Sie auf **Zugriffsschlüssel**, und notieren Sie sich die Werte für **Speicherkontoname** sowie **key1 Key value**. Sie benötigen diese Werte, wenn Sie den Flow erstellen.


## <a name="create-the-flow"></a>Erstellen des Flows

Damit Nachrichten in die Warteschlange gestellt werden können, müssen Sie zunächst einen Flow erstellen. 

1. Rufen Sie die [Microsoft Flow](https://flow.microsoft.com)-Website auf, melden Sie sich an, und klicken Sie oben auf der Seite auf **Create from Blank**.
1. Klicken Sie auf **Hunderte von Connectors und Triggern durchsuchen**, um einen Trigger auszuwählen.
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

1. Klicken Sie auf **+ Neuer Schritt** und anschließend auf **Aktion hinzufügen**.
1. Suchen Sie nach **Azure-Warteschlangen**, und wählen Sie **Azure-Warteschlangen - Nachricht in einer Warteschlange ablegen** aus.
1. Geben Sie einen aussagekräftigen Namen für die Verbindung ein.
1. Geben Sie den Namen des Speicherkontos ein, den Sie sich im vorherigen Abschnitt notiert haben.
1. Geben Sie den freigegebenen Speicherschlüssel ein, also den Wert aus dem Feld **Key1 key value** in Ihrem Speicherkonto.
1. Klicken Sie auf **Erstellen**.
1. Geben Sie **pnpprovisioningqueue** als Namen für die Warteschlange ein.
1. Im Anforderungstext haben Sie einen Eingangsparameter *webUrl* angegeben. Der Wert dieses Felds soll in die Warteschlange gestellt werden. Klicken Sie dazu in das Feld **Nachricht**, und wählen Sie aus der dynamischen Inhaltsauswahl die Option **webUrl** aus.
1. Klicken Sie auf **Flow speichern**. Es wird eine URL generiert. Diese URL notieren Sie sich im nächsten Schritt.
1. Klicken Sie auf den ersten Schritt in Ihrem Flow („Beim Empfang einer HTTP-Anforderung“), und notieren Sie sich die URL.
1. Speichern Sie Ihren Flow.

Ihr Flow sollte in etwa wie folgt aussehen:

![Screenshot eines Flows mit dem Namen „Beim Empfang einer HTTP-Anforderung“, mit den Feldern „URL“, „Anforderungstext“, „Warteschlangenname“ und „Nachricht“](images/pnpprovisioning-flow-overview.png)

## <a name="test-the-flow"></a>Testen des Flows

Zum Testen Ihres Flows müssen Sie eine POST-Anforderung senden. Das können Sie über die PowerShell tun, wie im Beispiel unten demonstriert:

```powershell
$uri = "[the URI you copied in step 14 when creating the flow]"
$body = "{webUrl:'somesiteurl'}
Invoke-RestMethod -Uri $uri -Method Post -ContentType "application/json" -Body $body
```

Wenn Sie zum Hauptbildschirm des Flows navigieren, sehen Sie einen Ausführungsverlauf. Wurde Ihr Flow korrekt ausgeführt, wird `Succeeded` angezeigt.
Navigieren Sie nun zu der Warteschlange, die Sie soeben in Azure erstellt haben, und klicken Sie auf **Aktualisieren**. Sie sollten nun einen Eintrag sehen. Ist das der Fall, wurde der Flow korrekt aufgerufen.

## <a name="provision-the-spfx-solution"></a>Bereitstellen der SPFx-Lösung

In diesem Abschnitt verwenden Sie eine vorhandene SPFx-Lösung, den [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer). Befolgen Sie die Anleitung in der Datei [Readme](https://github.com/SharePoint/sp-dev-fx-extensions/blob/master/samples/react-application-regions-footer/README.md) im Beispielrepository, um die Lösung zu erstellen und bereitzustellen.

## <a name="create-a-pnp-provisioning-template"></a>Erstellen einer PnP-Bereitstellungsvorlage

Kopieren Sie die folgende XML-Bereitstellungsvorlage in eine neue Datei, und speichern Sie die Datei als „FlowDemoTemplate.xml“.

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
  </pnp:Templates>
</pnp:Provisioning>
```

> [!NOTE]
> Die Bereitstellungsvorlage fügt einer Lösung eine benutzerdefinierte Aktion hinzu. Dabei ist **ClientSideComponentId** mit dem [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer) verknüpft, den Sie zuvor bereitgestellt haben. Wenn Sie diese Demo mit einer eigenen SPFx-Lösung ausführen, müssen Sie im XML-Code den Wert von **ClientSideComponentId** und optional auch die Attributwerte von **ClientSideComponentProperties** ändern.

## <a name="create-the-azure-function"></a>Erstellen der Azure-Funktion

1. Rufen Sie das [Azure-Portal](https://portal.azure.com) auf.
1. Suchen Sie nach **Funktionen-App**, und erstellen Sie eine neue Funktionen-App. Wählen Sie im Feld **Speicher** die Option **Use existing** aus. Wählen Sie dann das Speicherkonto aus, das Sie zuvor erstellt haben. Legen Sie die anderen Werte wie erforderlich fest.
1. Öffnen Sie die Funktionen-App, und klicken Sie auf **Funktionen** > **Neue Funktion**.

    ![Screenshot des Azure-Portals mit hervorgehobener Option „Neue Funktion“](images/pnpprovisioning-create-function.png)

1. Wählen Sie aus dem Dropdownfeld „Sprache“ die Option **PowerShell** aus.
1. Wählen Sie **QueueTrigger - PowerShell** aus.
1. Geben Sie der Funktion den Namen **ApplyPnPProvisioningTemplate**. 
1. Geben Sie den Namen der Warteschlange ein, die Sie zuvor erstellt haben.
1. Klicken Sie auf **Erstellen**. Es wird ein Editor geöffnet, in den Sie PowerShell-Cmdlets eingeben können. 

Im nächsten Schritt laden Sie das PnP-PowerShell-Modul hoch, damit Sie es in der Azure-Funktion verwenden können.

## <a name="upload-the-pnp-powershell-module-for-your-azure-function"></a>Hochladen des PnP-PowerShell-Moduls für Ihre Azure-Funktion

Sie müssen das PnP-PowerShell-Modul zunächst herunterladen, bevor Sie es für Ihre Azure-Funktion hochladen können.

1. Erstellen sie einen temporären Ordner auf Ihrem Computer.
1. Starten Sie PowerShell, und geben Sie den folgenden Befehl ein:
    ```powershell
    Save-Module -Name SharePointPnPPowerShellOnline -Path [pathtoyourfolder]
    ```
Die Dateien des PowerShell-Moduls werden in einen Unterordner des von Ihnen erstellten Ordners heruntergeladen. 

Als Nächstes laden Sie die Dateien hoch, damit Ihre Azure-Funktion das Modul verwenden kann.

1. Navigieren Sie zur Hauptseite Ihrer Funktionen-App, und klicken Sie auf **Plattformfeatures**.

    ![Screenshot der Funktionen-App mit hervorgehobener Option „Plattformfeatures“](images/pnpprovisioning-platform-features.png)

1. Klicken Sie auf **Erweiterte Tools (Kudu)**.

    ![Screenshot der Liste „Entwicklungstools“ mit hervorgehobener Option „Erweiterte Tools (Kudu)“](images/pnpprovisioning-select-kudu.png)

1. Klicken Sie auf der Kudu-Hauptseite auf **Debugging-Konsole**, und wählen Sie entweder **CMD** oder **PowerShell** aus.
1. Klicken Sie in den Datei-Explorer oben auf der Seite, und rufen Sie **site\wwwroot\\[NameIhrerAzureFunktion]** auf.
1. Erstellen Sie einen neuen Ordner mit dem Namen **modules**.
    
    ![Screenshot mit der hervorgehobenen Option „Neuer Ordner“](images/pnpprovisioning-kudu-create-folder.png)

1. Erstellen Sie im Ordner „modules“ einen Ordner mit dem Namen **SharePointPnPPowerShellOnline**, und wechseln Sie in diesen Ordner.
1. Navigieren Sie im Datei-Explorer auf Ihrem Computer zu dem Ordner, in den Sie die Dateien des PnP-PowerShell-Moduls heruntergeladen haben. Öffnen Sie den Ordner **SharePointPnPPowerShellOnline\2.20.1711.0**. (Die Versionsnummer ist möglicherweise eine andere.)
1. Ziehen Sie alle Dateien aus diesem Ordner per Drag-and-Drop in den Ordner in Kudu, um sie hochzuladen.

   ![Screenshot des Kudu-Ordners mit 40 hinzugefügten Dateien](images/pnpprovisioning-module-files-uploaded.png)

## <a name="finish-the-azure-function"></a>Fertigstellen der Azure-Funktion

1. Wechseln Sie wieder zu Ihrer Azure-Funktion, und erweitern Sie die Registerkarte mit den Dateien.

    ![Screenshot der Registerkarte „Dateien anzeigen“](images/pnpprovisioning-view-files.png)

1. Klicken Sie auf **Hochladen**, und laden Sie die Bereitstellungsvorlagendatei hoch, die Sie zuvor erstellt haben.
1. Ersetzen Sie das PowerShell-Skript durch folgenden Code:

    ```powershell
    $in = Get-Content $triggerInput -Raw
    Write-Output "Incoming request for '$in'"
    Connect-PnPOnline -AppId $env:SPO_AppId -AppSecret $env:SPO_AppSecret -Url $in
    Write-Output "Connected to site"
    Apply-PnPProvisioningTemplate -Path D:\home\site\wwwroot\ApplyPnPProvisioningTemplate\FlowDemoTemplate.xml
    ```

Wie Sie sehen, verwenden Sie zwei Umgebungsvariablen: ```SPO_AppId``` und ```SPO_AppSecret```. Zum Festlegen dieser Variablen navigieren Sie zur Hauptseite der Funktionen-App im Azure-Portal, klicken auf **Anwendungseinstellungen** und fügen zwei neue Anwendungseinstellungen hinzu:

1. ```SPO_AppId```: Tragen Sie hier als Wert die Client-ID ein, die Sie sich im ersten Schritt notiert haben, als Sie die App auf Ihrem Mandanten erstellt haben.
2. ```SPO_AppSecret```: Tragen Sie hier als Wert den geheimen Clientschlüssel ein, den Sie sich im ersten Schritt notiert haben, als Sie die App auf Ihrem Mandanten erstellt haben.

## <a name="create-the-site-design"></a>Erstellen des Websitedesigns

Öffnen Sie PowerShell, und vergewissern Sie sich, dass Sie die Microsoft Office 365-Verwaltungsshell installiert haben.

Stellen Sie über **Connect-SPOService** eine Verbindung zu Ihrem Mandanten her.

```powershell
Connect-SPOService -Url https://[yourtenant]-admin.sharepoint.com
```

Nun können Sie die vorhandenen Websitedesigns abrufen. 

```powershell
Get-SPOSiteDesign
```

Bevor Sie ein Websitedesign erstellen können, müssen Sie zuerst ein Websiteskript erstellen. Ein Websitedesign ist ein Container, der ein oder mehrere Websiteskripts referenziert.

1. Kopieren Sie den folgenden JSON-Code in die Zwischenablage, und ändern Sie ihn. Geben Sie für die Eigenschaft **url** den Wert ein, den Sie sich bei der Erstellung des Flows notiert haben. Die URL sieht in etwa wie folgt aus:

    `https://prod-27.westus.logic.azure.com:443/workflows/ef7434cf0d704dd48ef5fb6...oke?api-version=2016-06-01&sp=%2Ftriggers%2Fmanual%2Frun`

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

1. Markieren Sie den JSON-Code erneut, und kopieren Sie ihn nochmals in die Zwischenablage.
1. Öffnen Sie PowerShell, und geben Sie Folgendes ein, um das Skript in eine Variable zu kopieren und das Websiteskript zu erstellen:

    ```powershell
    $script = Get-Clipboard -Raw
    Add-SPOSiteScript -Title "Apply PnP Provisioning Template" -Content $script
    Get-SPOSiteScript
    ```

1. Es wird eine Liste mit einem oder mehreren Skripts angezeigt, einschließlich des soeben erstellten Websiteskripts. Markieren Sie die ID des Websiteskripts, das Sie soeben erstellt haben, und kopieren Sie sie in die Zwischenablage.
1. Erstellen Sie mithilfe des folgenden Befehls das Websitedesign:

    ```powershell
    Add-SPOSiteDesign -Title "Site with footer" -SiteScripts [Paste the ID of the Site Script here] -WebTemplate "64"
    ```

Das Cmdlet **Add-SPOSiteDesign** verknüpft das Websitedesign mit der Teamwebsite. Wenn Sie das Design mit einer Kommunikationswebsite verknüpfen möchten, müssen Sie den Wert „68“ verwenden.

## <a name="verify-the-results"></a>Überprüfen der Ergebnisse

Nachdem Sie Ihren Azure Queue-Speicher erstellt haben, haben Sie eine App-ID für App-exklusiven Zugriff, die Azure-Funktion und das Websitedesign erstellt. Anschließend haben Sie über das Websitedesign Microsoft Flow ausgelöst. 

Um die Ergebnisse zu testen, müssen Sie nun eine neue Website erstellen. Klicken Sie in Ihrem SharePoint-Mandanten auf **SharePoint** > **Website erstellen** > **Teamwebsite**. Ihr neues Websitedesign sollte als Designoption angezeigt werden. Dabei ist zu beachten, dass das Websitedesign nach der Erstellung der Website angewendet wird. Wenn Sie es ordnungsgemäß konfiguriert haben, wird Ihr Flow ausgelöst. Ob der Flow korrekt ausgeführt wurde, können Sie in seinem Ausführungsverlauf überprüfen. Die Fußzeile wird möglicherweise nicht sofort angezeigt. Falls sie nicht angezeigt wird: Warten Sie eine Minute, und laden Sie Ihre Website neu, um es nochmals zu versuchen.


