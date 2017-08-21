# <a name="add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in"></a>Hinzufügen eines Webparts zu einer Seite in einem von SharePoint gehosteten SharePoint-Add-In
Erfahren Sie, wie Sie Webparts auf einer Seite in einem SharePoint-Add-In einfügen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 

Dies ist der fünfte in einer Reihe von Artikeln über die Grundlagen der Entwicklung von von SharePoint gehosteten SharePoint-Add-In. Machen Sie sich zunächst mit [SharePoint-Add-Ins](sharepoint-add-ins) und den vorherigen Artikeln in dieser Reihe vertraut:
 

-  [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [Hinzufügen von benutzerdefinierten Spalten zu einem von SharePoint gehosteten SharePoint-Add-In](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
    
 
-  [Hinzufügen eines benutzerdefinierten Inhaltstyps zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
    
 

 **Hinweis** Wenn Sie diese Reihe zu von SharePoint gehosteten Add-Ins durchgearbeitet haben, haben Sie eine Visual Studio-Projektmappe, die Sie verwenden können, um mit diesem Thema fortzufahren. Sie können außerdem das Repository unter [SharePoint_SP-Hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) herunterladen und die Datei „BeforeWebPart.sln“ öffnen.
 

In diesem Artikel fügen Sie der Standardseite des SharePoint-Add-Ins „Orientierung für Mitarbeiter“ ein Webpart hinzu.
 

## <a name="add-a-web-part-to-a-page"></a>Hinzufügen eines Webparts zu einer Seite


 

 

1. Öffnen Sie im **Projektmappen-Explorer** die Datei „Default.aspx“. 
    
 
2. Wir fügen ein Listenansicht-Webpart zu der Seite hinzu, auf der die Liste Neue Mitarbeiter in Seattle angezeigt wird, damit kein Link zur Listenansichtsseite für die Liste mehr erforderlich ist. Entfernen Sie das Element **<asp:HyperLink>** aus dem Element **<asp:Content>**, dessen **ContentPlaceHolderId** `PlaceHolderMain` lautet. 
    
 
3. Fügen Sie innerhalb desselben **<asp:Content>**-Elements die folgende **WebPartZone** hinzu. 
    
```XML
  <WebPartPages:WebPartZone runat="server" FrameType="TitleBarOnly" 
      ID="HomePage1" Title="loc:full" />

```

4. Speichern und schließen Sie die Datei.
    
 
5. Öffnen Sie im **Projektmappen-Explorer** die Datei „elements.xml“ für die Seite im Knoten **Seiten**.
    
 
6. Wenn das Element **File** selbstschließend ist, entfernen Sie das Zeichen „/“ daraus, und fügen Sie das Endetag `</File>` hinzu.
    
 
7. Fügen Sie im Element **File** ein untergeordnetes **AllUsersWebPart**-Element hinzu, und legen Sie dessen **WebPartZoneID** auf die ID der Webpartzone fest, die Sie auf der Seite erstellt haben. Der Inhalt der Datei sollte nun wie folgt aussehen. Dieses Markup weist SharePoint an, ein **AllUsersWebPart** in der Webpartzone namens „HomePage1" einzufügen.
    
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

9. Fügen Sie das folgende **webPart**-Markup als untergeordnetes Element des Elements **webParts** hinzu. Dieses Markup fügt ein **XsltListViewWebPart** hinzu und weist das Webpart an, die ListeNeue Mitarbeiter in Seattle anzuzeigen. Beachten Sie, dass der Eigenschaftswert **ViewContentTypeId** nur „0x" und nicht die tatsächliche ID des InhaltstypsNewEmployee ist.
    
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
    
    **Standardseite mit Listenansicht-Webpart**

 

     ![Standardseite des Add-Ins mit Anzeige der Liste „Neue Mitarbeiter in Seattle“ in einem Webpart](../../images/31e8e4b1-e2e6-416b-b360-9979a1f16fc7.PNG)
 

    
    
 
3. Versuchen Sie, der Liste neue Elemente hinzuzufügen und vorhandene Elemente zu bearbeiten.
    
 
4. Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.
    
 
5. Da Sie mit diesem Add-In und dieser Visual Studio-Projektmappe in anderen Artikeln arbeiten werden, hat es sich bewährt, das Add-In ein letztes Mal zurückzuziehen, wenn Sie Ihre Arbeit daran für eine Weile abgeschlossen haben. Klicken Sie mit der rechten Maustaste auf das Projekt im **Projektmappen-Explorer**, und wählen Sie **Zurückziehen** aus.
    
 

## 
<a name="Nextsteps"> </a>

Im nächsten Artikel dieser Reihe fügen Sie dem SharePoint-Add-In einen Workflow hinzu: [Hinzufügen eines Workflows zu einem von SharePoint gehosteten SharePoint-Add-In](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in).
 

 

