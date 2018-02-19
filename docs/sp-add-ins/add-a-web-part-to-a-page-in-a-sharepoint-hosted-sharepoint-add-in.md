---
title: "Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In"
description: "Fügen Sie ein Webpart zu einer Seite hinzu, führen Sie das Add-In aus und testen Sie es."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 335e68f24e7bc4ba9bd8a7777b48473542e8fc26
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in"></a>Hinzufügen eines Webparts zu einer Seite in einem in SharePoint gehosteten SharePoint-Add-In

Dies ist der fünfte einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-Ins. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins.md) und den vorherigen Artikeln dieser Reihe vertraut, die Sie unter [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md#Nextsteps) finden. 
    
> [!NOTE]
> Wenn Sie unsere Artikelreihe zum Thema SharePoint-gehostete Add-Ins durchgearbeitet haben, haben Sie bereits eine Visual Studio-Lösung, die Sie für diesen Artikel verwenden können. Sie können auch das Repository von [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeWebPart.sln“ öffnen.

In diesem Artikel fügen Sie der Standardseite des SharePoint-Add-Ins „Orientierung für Mitarbeiter“ ein Webpart hinzu.

## <a name="add-a-web-part-to-a-page"></a>Hinzufügen eines Webparts zu einer Seite

1. Öffnen Sie im **Projektmappen-Explorer** die Datei „Default.aspx“. 

2. Da wir einen Listenansicht-Webpart zu der Seite hinzufügen, das die Liste „Neue Mitarbeiter in Seattle“ berücksichtigt, benötigen wir keinen Link zu der Seite „Listenansicht“ für die Liste. Entfernen Sie das Element **<asp: HyperLink>** aus dem Element **<asp:Content>**, dessen **ContentPlaceHolderId** `PlaceHolderMain` ist. 

3. Fügen Sie innerhalb desselben **<asp:Content>**-Elements die folgende **WebPartZone** hinzu. 
    
    ```XML
      <WebPartPages:WebPartZone runat="server" FrameType="TitleBarOnly" 
          ID="HomePage1" Title="loc:full" />
    ```

4. Speichern und schließen Sie die Datei.

5. Öffnen Sie im **Projektmappen-Explorer** die Datei „elements.xml“ für die Seite im Knoten **Seiten**.

6. Wenn das Element **File** selbstschließend ist, entfernen Sie das Zeichen „/“ daraus, und fügen Sie das Endetag `</File>` hinzu.

7. Fügen Sie im **Datei**-Element ein untergeordnetes **AllUsersWebPart**-Element hinzu, und legen Sie seine **WebPartZoneID** auf die ID der Webpartzone fest, die Sie auf der Seite erstellt haben. Die Inhalte der Datei sollten jetzt wie folgt aussehen. Dieses Markup fordert SharePoint auf, ein **AllUsersWebPart** mit dem Namen „HomePage1“ in die Webpartzone einzufügen.
    
    ```
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <Module Name="Pages">
        <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" >
          <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">

          </AllUsersWebPart>
        </File>
      </Module>
    </Elements>

    ```

8. Fügen Sie ein **CDATA**-Element als untergeordnetes Element von **AllUsersWebPart** hinzu, und fügen Sie dann ein **webParts**-Element als untergeordnetes Element von **CDATA** hinzu, wie im folgenden Markup gezeigt. 
    
    ```
    <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">
      <![CDATA[
        <webParts>

        </webParts>
      ]]>
    </AllUsersWebPart>
    ```

9. Fügen Sie das folgende **webPart**-Markup als untergeordnetes Element des **webParts**-Elements hinzu. Dieses Markup fügt ein **XsltListViewWebPart** hinzu und fordert das Webpart auf, die Liste **Neue Mitarbeiter in Seattle** anzuzeigen. Beachten Sie, dass der **ViewContentTypeId**-Eigenschaftswert nur `0x` und nicht die tatsächliche ID des **NewEmployee**-Inhaltstyps ist.
    
    ```
      <webPart xmlns="http://schemas.microsoft.com/WebPart/v3">
        <metaData>
          <type name="Microsoft.SharePoint.WebPartPages.XsltListViewWebPart, 
                       Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, 
                       PublicKeyToken=71e9bce111e9429c" />
        </metaData>
        <data>
          <properties>
            <property name="ListUrl">Lists/NewEmployeesInSeattle</property>
            <property name="IsIncluded">True</property>
            <property name="NoDefaultStyle">True</property>
            <property name="Title">New Employees in Seattle</property>
            <property name="PageType">PAGE_NORMALVIEW</property>
            <property name="Default">False</property>
            <property name="ViewContentTypeId">0x</property>
          </properties>
        </data>
      </webPart>
    ```


## <a name="run-and-test-the-add-in"></a>Ausführen und Testen des Add-Ins

1. Verwenden Sie die F5-TASTE, um Ihr Add-In bereitzustellen und auszuführen. Visual Studio führt eine temporäre Installation des Add-Ins auf Ihrer SharePoint-Testwebsite durch und führt das Add-In sofort aus. 

2. Wenn die Standardseite des Add-Ins geöffnet wird, enthält sie das Listenansicht-Webpart, und die Liste wird angezeigt. 
    
   *Abbildung 1. Standardseite mit Listenansicht-Webpart*

   ![Standardseite des Add-Ins mit Anzeige der Liste „Neue Mitarbeiter in Seattle“ in einem Webpart](../images/31e8e4b1-e2e6-416b-b360-9979a1f16fc7.PNG)

3. Versuchen Sie, der Liste neue Elemente hinzuzufügen und vorhandene Elemente zu bearbeiten.

4. Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.

5. Da Sie mit diesem Add-In und dieser Visual Studio-Lösung in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Zurückziehen** aus.


## <a name="next-steps"></a>Nächste Schritte 
<a name="Nextsteps"> </a>

Im nächsten Artikel dieser Reihe [fügen Sie einen Workflow zu einem von SharePoint gehosteten SharePoint-Add-In hinzu](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md).
 

 

