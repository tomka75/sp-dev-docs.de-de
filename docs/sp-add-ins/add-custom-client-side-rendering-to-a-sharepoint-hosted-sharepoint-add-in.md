---
title: "Hinzufügen des benutzerdefinierten clientseitigen Renderings zu einem von SharePoint gehosteten SharePoint-Add-In"
description: "Passen Sie das Rendering und die Prüfung von Steuerelementen in SharePoint-Add-In-Seiten an, erstellen und registrieren Sie JavaScript-Code, führen Sie das Add-In aus und testen Sie es."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: a3bbe8333e4caef11a479d89627ff8307dde659f
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2017
---
# <a name="add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in"></a>Hinzufügen des benutzerdefinierten clientseitigen Renderings zu einem von SharePoint gehosteten SharePoint-Add-In
 
Dies ist der achte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln in dieser Reihe vertraut:
 
-  [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
-  [Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
-  [Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md)
-  [Hinzufügen eines Workflows zu einem von SharePoint gehosteten Add-In für SharePoint](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [Hinzufügen einer benutzerdefinierten Seite und Formatvorlage zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in.md)

> [!NOTE]
> Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, können Sie das Thema mit einer Visual Studio-Lösung weiter vertiefen. Sie können auch das Repository von [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeClientRenderedControl.sln“ öffnen.
 
Sie können clientseitigen JavaScript-Code verwenden, um das Rendering der Webparts, die meisten Feldtypen (Spalten) und einige andere Steuerelemente anzupassen, indem Sie der **JSLink**-Eigenschaft des Steuerelements eine JavaScript-Datei wie z. B. **SPField.JSLink** zuweisen. Auf diese Weise können Sie auch clientseitige Überprüfungslogik hinzufügen. In diesem Artikel passen Sie das Rendering eines Feldes in einer Liste des SharePoint-Add-Ins „Orientierung für Mitarbeiter“ mit clientseitigem Rendering an.
 
> [!NOTE]
> - Wenn der Endbenutzer JavaScript in seinem Browser deaktiviert hat, greift SharePoint auf das serverseitige Rendern und Prüfen zurück.
> - Die JSLink-Eigenschaft wird nicht für Umfrage- oder Ereignislisten unterstützt. Ein SharePoint-Kalender ist eine Ereignisliste.

## <a name="create-and-register-the-javascript"></a>Erstellen und Registrieren des JavaScript-Codes

1. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Knoten **Skripts**, und wählen Sie **Hinzufügen** > **Neues Element** > **Web** aus. 

2. Wählen Sie **JavaScript-Datei**, und nennen Sie sie **OrientationStageRendering.js**. 

3. Ihr benutzerdefiniertes Rendern des Felds sollte automatisch erfolgen. Verwenden Sie daher den folgenden Code, um eine anonyme Methode zum JavaScript hinzufügen, die automatisch ausgeführt wird, wenn die Datei geladen wird:

    ```
      (function () {

      })();
    ```

4. Fügen Sie im Textkörper dieser Methode (zwischen den {}-Zeichen) den folgenden Code zum Erstellen von JSON-Objekten (Javascript Object Notation) für den Renderingüberschreibungskontext, die Vorlagen in dem Kontext und die Vorlagen für die Felder hinzu.
    
    ```
      var customRenderingOverride = {};
    customRenderingOverride.Templates = {};
    customRenderingOverride.Templates.Fields = {

    }
    ```

5. Fügen Sie im Text des **Felder**-Vorlageobjekts die folgende JSON ein.

    ```
      "OrientationStage": { "View": renderOrientationStage }
    ```

   - Der Eigenschaftenname `OrientationStage` gibt das Feld mit dem angepassten Rendering an. 
   - Der Wert der Eigenschaft ist ein weiteres JSON-Objekt. 
   - Die `View`-Eigenschaft gibt den Seiteninhalt an, auf den das benutzerdefinierte Rendering angewendet wird. In diesem Fall teilt das Objekt SharePoint mit, das angepasste Rendering bei Listenansichten zu verwenden. (Es gibt weitere Optionen für die Formulare Bearbeiten, Neu und Anzeigen.) 
   - Der Wert der Eigenschaft `renderOrientationStage` ist der Name der benutzerdefinierten Renderingmethode, die Sie in einem späteren Schritt erstellen.

6. Die letzte Aktion, die die anonyme Methode durchführen muss, besteht darin, den Vorlagen-Manager von SharePoint die Renderingüberschreibung zu informieren. Fügen Sie die folgende Zeile am Ende des Hauptteils der Methode hinzu.
    
    ```
      SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride);
    ```

   Die Methode sollte jetzt wie folgt aussehen.
    
    ```
      (function () {
        var customRenderingOverride = {};
        customRenderingOverride.Templates = {};
        customRenderingOverride.Templates.Fields = {
            "OrientationStage": { "View": renderOrientationStage }
        }

        SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride);
    })();
    ```

7. Fügen Sie die folgende Methode zur Datei hinzu. Sie legt die Farbe des Spaltenwerts **Orientierungsphase** auf Rot fest, wenn der Wert `Not Started` ist, und auf Grün, wenn der Wert `Completed` ist. (Das `ctx`-Objekt ist ein Clientkontextobjekt, das vom In-the-Box-SharePoint-Skript deklariert wird.)
    
    ```
      function renderOrientationStage(ctx) {
        var orientationStageValue = ctx.CurrentItem[ctx.CurrentFieldSchema.Name];
        if (orientationStageValue == "Not Started")  {
            return "<span style='color:red'>" + orientationStageValue + "</span>"
        }
        else if (orientationStageValue == "Completed") {
            return "<span style='color:green'>" + orientationStageValue + "</span>"
        }
        else {
            return orientationStageValue;
        }
    }
    ```

8. Erweitern Sie im **Projektmappen-Explorer** **Websitespalten** und **OrientationStage**, und öffnen Sie dann die Datei „elements.xml“. 

9. Um SharePoint anzuweisen, Ihren benutzerdefinierten JavaScript-Code zu verwenden, fügen Sie eine neues **JSLink**-Attribut zum **Feld**-Element hinzu, und weisen dann die folgende URL als Wert zu: `~site/Scripts/OrientationStageRendering.js`.
    
   > [!NOTE]
   > Die **JSLink**-Eigenschaft ist immer eine Datei und keine Methode. Es gibt keine Möglichkeit, SharePoint mitzuteilen, welche Methode ausgeführt werden soll, und aus diesem Grund enthält die Datei eine Methode, die automatisch ausgeführt wird.

   Das Start-Tag für das Element **Feld** sieht nun wie folgt aus.
    
    ```
      <Field
           ID="{some_guid_here}"
           Name="OrientationStage"
           Title="OrientationStage"
           DisplayName="Orientation Stage"
           Description="The current orientation stage of the employee."
           Type="Choice"
           Required="TRUE"
           Group="Employee Orientation" 
           JSLink="~site/Scripts/OrientationStageRendering.js">
    <!-- child elements and end tag omitted -->
    ```

10. Öffnen Sie die Seite Default.aspx, und fügen Sie den folgenden Code als letztes untergeordnetes Element des **asp:Content**-Elements hinzu, dessen **ContentPlaceHolderID** auf **PlaceHolderMain** festgelegt ist. 
    
    ```XML
      <p><asp:HyperLink runat="server" NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
        Text="List View Page for New Employees in Seattle" /></p>

    ```

## <a name="run-and-test-the-add-in"></a>Ausführen und Testen des Add-Ins

1. Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus. 
 
2. Das von Ihnen konfigurierte clientseitige Rendering wirkt sich lediglich auf das Rendering des Felds der Seite Listenansicht aus und nicht auf das Listenansicht-Webpart, das wir auf der Homepage hinzugefügt haben. Dies liegt daran, dass das Webpart standardmäßig auf serverseitiges Rendering zurückgesetzt wird. Es gibt Möglichkeiten, dies rückgängig zu machen, aber dies würde den Rahmen dieses einfachen Beispiels sprengen. Um das clientseitige Rendering in Aktion zu sehen, wählen Sie den Link unten auf der Seite **Seite mit der Listenansicht für neue Mitarbeiter in Seattle**.
 
3. Wenn die Listenansichtsseite geöffnet wird, legen Sie den Wert **Einführungsphase** für einige Elemente auf **Nicht gestartet** und für andere auf **Abgeschlossen** fest, um das benutzerdefinierte Farbrendering anzuzeigen.
    
   *Abbildung 1. Liste mit benutzerdefiniertem clientseitigem Rendering*

   ![Liste "Neue Mitarbeiter in Seattle" mit den Orientierungsphasewerten "Nicht gestartet" in Rot und "Abgeschlossen" in Grün. Andere Werte in Schwarz.](../images/dc8e2b7d-1747-4b65-aab4-6fc93c6867d4.PNG)
  
4. Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.
    
5. Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.

## <a name="next-steps"></a>Nächste Schritte
<a name="Nextsteps"> </a>

Im nächsten Artikel dieser Reihe erstellen Sie [eine benutzerdefinierten Menüband-Schaltfläche im Hostweb einer SharePoint-Add-In](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in.md).
 
