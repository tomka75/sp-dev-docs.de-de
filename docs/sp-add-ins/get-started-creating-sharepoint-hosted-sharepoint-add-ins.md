---
title: Erste Schritte beim Erstellen von SharePoint gehosteten SharePoint-Add-Ins
description: "Hier erfahren Sie, wie Sie eine Entwicklungsumgebung einrichten und Ihr erstes SharePoint-gehostetes SharePoint-Add-In erstellen können."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 7cf441bb18f0c4b6658a57be4e949eafce9a3260
ms.sourcegitcommit: 074f3a7983a7b253f56f8c670a0290c27bb7734b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="get-started-creating-sharepoint-hosted-sharepoint-add-ins"></a>Erste Schritte zum Erstellen SharePoint-gehosteter SharePoint-Add-Ins

SharePoint-gehostete Add-Ins sind einer der zwei Haupttypen von SharePoint-Add-Ins. Einen Überblick über SharePoint-Add-Ins und die zwei Add-In-Typen finden Sie unter [SharePoint Add-ins](sharepoint-add-ins.md). Hier die wichtigsten Punkte zu SharePoint-gehosteten Add-Ins:

- Sie enthalten SharePoint-Listen, Webparts, Workflows, benutzerdefinierte Seiten und andere Komponenten, die auf einer Unterwebsite mit der Bezeichnung Add-In-Web der SharePoint-Website installiert sind, wo das Add-In installiert ist.

- Sie bestehen ausschließlich aus JavaScript-Code auf benutzerdefinierten SharePoint-Seiten.

- Schritt 1: Einrichten der Entwicklungsumgebung 

- Schritt 2: Erstellen des App-Projekts 

- Schritt 3: Programmieren der App

<a name="Setup"> </a>
## <a name="set-up-your-dev-environment"></a>Einrichten der Entwicklungsumgebung

Es gibt zahlreiche verschiedene Möglichkeiten, eine Entwicklungsumgebung für SharePoint-Add-Ins einzurichten. In diesem Abschnitt wird die einfachste von ihnen beschrieben.

### <a name="get-the-tools"></a>Installieren der Tools

- Falls Sie **Visual Studio 2013** oder höher noch nicht installiert haben: Installieren Sie es mithilfe der Anweisungen unter [Installieren von Visual Studio](https://docs.microsoft.com/de-DE/visualstudio/install/install-visual-studio). Wir empfehlen die Verwendung der [aktuellen Version aus dem Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).

- Visual Studio umfasst die **Microsoft Office Developer Tools für Visual Studio**. Gelegentlich wird jedoch zwischen zwei Updates von Visual Studio eine neue Version der Tools veröffentlicht. Führen Sie das [Installationsprogramm für Office Developer Tools für Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) oder das [Installationsprogramm für Office Developer Tools für Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015) aus, um sicherzustellen, dass Sie die aktuelle Version der Tools haben. 

<a name="o365_signup"> </a>
### <a name="sign-up-for-an-office-365-developer-site"></a>Registrieren für eine Office 365-Entwicklerwebsite

> [!NOTE]
> Möglicherweise haben Sie bereits Zugriff auf eine Office 365-Entwicklerwebsite:
> - **Sind Sie MSDN-Abonnent?** Visual Studio Ultimate und Visual Studio Premium mit MSDN-Abonnenten erhalten als Bonus ein einjähriges Office 365 Developer-Abonnement. [Lösen Sie Ihren Bonus heute ein.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) 
> - **Besitzen Sie einen der folgenden Office 365-Abonnementpläne?** Wenn ja, kann ein Administrator des jeweiligen Office 365-Abonnements über das [Office 365 Admin Center](https://portal.microsoftonline.com/admin/default.aspx) eine Entwicklerwebsite für Sie erstellen. Weitere Informationen finden Sie unter [Erstellen einer Entwicklerwebsite in einem vorhandenen Office 365-Abonnement](create-a-developer-site-on-an-existing-office-365-subscription.md). 

Sie haben drei Möglichkeiten, einen Office 365-Plan zu erhalten: 

- Sie können die [kostenlose 30-Tage-Testversion](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) nutzen, die eine einzige Benutzerlizenz enthält.

- Sie können ein [Office 365-Entwicklerabonnement](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK) erwerben. 

- Sie können sich über das Office 365-Entwicklerprogramm für ein kostenloses Office 365-Entwicklerkonto mit einem Jahr Laufzeit registrieren. Weitere Informationen finden Sie [hier](http://dev.office.com/devprogram). Alternativ können Sie direkt das [Registrierungsformular](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170) ausfüllen. Nach der Registrierung für das Entwicklerprogramm erhalten Sie eine E-Mail mit einem Link, unter dem Sie sich für ein Entwicklerkonto registrieren können. Nachfolgend finden Sie eine Anleitung.

> [!TIP]
> Öffnen Sie diese Links in einem anderen Fenster oder auf einer anderen Registerkarte, damit Sie die Anleitung jederzeit einsehen können.

1. Die erste Seite des Registrierungsformulars ist selbsterklärend. Geben Sie die geforderten Informationen ein, und klicken Sie anschließend auf **Next**.

2. Geben Sie auf der zweiten Seite (siehe Abbildung 1) eine Benutzer-ID für den Administrator des Abonnements ein.
   
   *Abbildung 1: Domänenname der Office 365-Entwicklerwebsite*

   ![Seite 2 des Registrierungsformulars für ein Office 365-Konto](../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
   
3. Erstellen Sie eine Unterdomäne von **.onmicrosoft.com**, zum Beispiel „contoso.onmicrosoft.com“.
    
   Sobald die Registrierung abgeschlossen ist, können Sie sich mit den daraus resultierenden Anmeldeinformationen (im Format *Benutzer-ID@ihredomäne.onmicrosoft.com*) bei Ihrer Office 365-Portalwebsite anmelden und dort Ihr Konto verwalten. Ihre SharePoint Online-Entwicklerwebsite wird in Ihrer neuen Domäne eingerichtet: `http://yourdomain.sharepoint.com`.
    
4. Klicken Sie auf **Next**, und füllen Sie die letzte Seite des Formulars aus. Wenn Sie sich telefonisch einen Bestätigungscode durchgeben lassen möchten, können Sie wahlweise eine Mobiltelefonnummer oder eine Festnetznummer angeben. VoIP-Nummern (Voice over Internet Protocol) werden jedoch *nicht* unterstützt.
    
   > [!NOTE]
   > Falls Sie zum Zeitpunkt Ihrer Registrierung für ein Entwicklerkonto noch bei einem anderen Microsoft-Konto angemeldet sind, wird unter Umständen die folgende Meldung angezeigt: „Sorry, that user ID you entered didn‘t work. It looks like it's not valid. Be sure you enter the user ID that your organization assigned to you. Your user ID usually looks like *someone@example.com* or *someone@example.onmicrosoft.com*.“ 

   > Sollte diese Meldung angezeigt werden, müssen Sie sich von dem betreffenden Microsoft-Konto abmelden und die Registrierung erneut versuchen. Wird Ihnen die Meldung weiterhin angezeigt: Leeren Sie den Cache Ihres Browsers, oder schalten Sie um auf **InPrivate-Browsen**, und füllen Sie das Formular erneut aus.

   Sobald der Registrierungsprozess abgeschlossen ist, wird in Ihrem Browser die Office 365-Installationsseite geöffnet. Klicken Sie auf das Symbol „Admin“, um das Admin Center zu öffnen.

   *Abbildung 2: Office 365 Admin Center-Seite*

   ![Screenshot mit dem Office 365 Admin Center](../images/SP15_Office365AdminInset_border.png)
 
5. Warten Sie, bis die Entwicklerwebsite eingerichtet ist. Aktualisieren Sie die Admin Center-Seite in Ihrem Browser, sobald die Bereitstellung abgeschlossen ist.

6. Klicken Sie oben links auf der Seite auf **Build Add-ins**, um Ihre Entwicklerwebsite zu öffnen. Nun sollten Sie eine Website sehen, die wie Abbildung 3 aussieht. Dass die Liste **Add-ins in Testing** auf der Seite angezeigt wird, ist der Beleg dafür, dass die Website auf Basis der Vorlage für SharePoint-Entwicklerwebsites erstellt wurde. Falls stattdessen eine normale Teamwebsite angezeigt wird: Warten Sie einige Minuten, und starten Sie dann die Website neu.

7. Notieren Sie sich die URL der Website. Sie benötigen sie, um SharePoint-Add-In-Projekte in Visual Studio zu erstellen.

   *Abb. 3: Die Startseite Ihrer Entwicklerwebsite mit der Liste der Add-Ins im Test*

   ![Screenshot der Entwicklerwebsite-Startseite](../images/SP15_DeveloperSiteHome_border.png)

<a name="Create"> </a>
## <a name="create-the-add-in-project"></a>Erstellen des Add-In-Projekts

1. Starten Sie Visual Studio mit der Option **Als Administrator ausführen**.

2. Klicken Sie in Visual Studio auf **Datei** > **Neu** > **Neues Projekt**.
 
3. Erweitern Sie im Dialogfeld **Neues Projekt** zunächst den Knoten **Visual C#** und dann den Knoten **Office/SharePoint**. Klicken Sie nun auf **Add-Ins** > **Add-in for SharePoint**.

4. Geben Sie dem Projekt den Namen **EmployeeOrientation**, und klicken Sie auf **OK**.

5. Geben Sie im Dialogfeld **Specify the Add-in for SharePoint Settings** die vollständige URL der SharePoint-Website ein, die Sie zum Debuggen Ihres Add-Ins verwenden möchten. Gemeint ist die URL der Entwicklerwebsite. (Verwenden Sie HTTPS in der URL, nicht HTTP.) Wählen Sie unter **Wie soll Ihr SharePoint-Add-In gehostet werden?** die Option **Von SharePoint gehostet** aus, und klicken Sie auf **Fertig stellen**.

6. Möglicherweise werden Sie aufgefordert, sich bei Ihrer Entwicklerwebsite anzumelden. Verwenden Sie in diesem Fall die Anmeldeinformationen des Abonnementadministrators.

7. Das Projekt wird erstellt. Öffnen Sie im Stammverzeichnis des Projekts die Datei **/Pages/Default.aspx**. Unter anderem lädt diese generierte Datei eines oder beide der zwei Skripts, die in SharePoint gehostet werden: „sp.runtime.js“ und „sp.js“. Das Markup zum Laden dieser Dateien befindet sich im Steuerelement des Typs **Content** mit der ID **PlaceHolderAdditionalPageHead** am Anfang der Datei. Dieses Markup unterscheidet sich je nach der verwendeten Version von **Microsoft Office Developer Tools für Visual Studio**. Für diese Tutorialreihe müssen beide Dateien geladen werden. Zudem müssen die Dateien mit herkömmlichen HTML-Tags des Typs **\<script\>** geladen werden statt mit Tags des Typs **\<SharePoint:ScriptLink\>**. 

    Stellen Sie sicher, dass das Steuerelement **PlaceHolderAdditionalPageHead** die nachfolgenden Zeilen enthält, und zwar *direkt oberhalb* der Zeile `<meta name="WebPartPageExpansion" content="full" />`:
    
    ```
      <script type="text/javascript" src="/_layouts/15/sp.runtime.js"></script> 
      <script type="text/javascript" src="/_layouts/15/sp.js"></script> 
    ```

8. Suchen Sie in der Datei nach anderem Markup, das ebenfalls eine dieser Dateien lädt, und entfernen Sie dieses redundante Markup. Speichern und schließen Sie die Datei.

<a name="Code"> </a>
## <a name="code-your-add-in"></a>Programmieren des Add-Ins

In Ihr erstes SharePoint-gehostetes SharePoint-Add-In integrieren wir die klassische SharePoint-Erweiterung: eine benutzerdefinierte Liste und eine Instanz dieser Liste.

1. Öffnen Sie im **Projektmappen-Explorer** die Datei „AppManifest.xml".

2. Der Manifest-Designer wird geöffnet. Ändern Sie die Zeichenfolge im Feld **Titel** in **Orientierung für Mitarbeiter**. (Ändern Sie *keinesfalls* das Feld **Name**.)

3. Speichern und schließen Sie die Datei.

4. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Hinzufügen** > **Neuer Ordner** aus. Geben Sie dem Ordner den Namen „Listen“.

5. Klicken Sie mit der rechten Maustaste auf den neuen Ordner, und wählen Sie die Option **Hinzufügen** > **Neues Element** aus. Das Dialogfeld **Neues Element hinzufügen** wird geöffnet, und der Knoten **Office/SharePoint** wird angezeigt.

6. Klicken Sie auf **Liste**. Geben Sie der Liste den Namen **NewEmployeeOrientation**, und klicken Sie auf **Hinzufügen**. 
 
7. Übernehmen Sie im Assistent zum Anpassen von SharePoint auf der Seite **Listeneinstellungen auswählen** den Standardwert **NewEmployeeOrientation** als Anzeigename der Liste, und aktivieren Sie das Optionsfeld **Anpassbare Listenvorlage und eine Listeninstanz davon erstellen**. Wählen Sie dann aus der Dropdownliste die Option **Standard (benutzerdefinierte Liste)** aus, und klicken Sie auf **Fertig stellen**.

8. Der Assistent erstellt eine **NewEmployeeOrientation**-Listenvorlage mit einer untergeordneten Listeninstanz mit der Bezeichnung **NewEmployeeOrientationInstance**. Möglicherweise wird ein Listen-Designer geöffnet. Dieser wird in einem späteren Schritt verwendet.

9. Erweitern Sie den Knoten **NewEmployeeOrientationInstance** im **Projektmappen-Explorer**, sofern dies noch nicht geschehen ist, damit Sie die Datei „elements.xml“, die ein untergeordnetes Element der Liste *Instanz* ist, klar von der Datei „elements.xml“ unterscheiden können, die ein untergeordnetes Element der Liste *Vorlage* ist.
    
    *Abbildung 4: Knoten „Listen“ im Projektmappen-Explorer*

    ![Listenordner mit der untergeordneten Vorlage "NewEmployeeOrientation", die wiederum über drei untergeordnete Elemente verfügt: eine NewEmployeeOrientationInstance, die Datei "elements.xml" und die Datei "schema.xml". Die Instanz selbst ist ein untergeordnetes Element mit dem Namen "elements.xml".](../images/10e5d116-d24b-4a44-bfff-cfbf2f971b1e.PNG)

10. Öffnen Sie das untergeordnete Element „elements.xml“ der Listenvorlage **NewEmployeeOrientation**.

11. Fügen Sie in das Attribut **DisplayName** (nicht in das Attribut **Name**) Leerzeichen ein, damit es besser lesbar ist: „New Employee Orientation“.

12. Tragen Sie als Wert für das Attribut **Description** die Zeichenfolge „Orientation information about new employees“ ein.

13. Übernehmen Sie für alle anderen Attribute jeweils den Standardwert, speichern Sie die Datei, und schließen Sie sie.

14. Falls der Listen-Designer noch nicht geöffnet ist: Klicken Sie im **Projektmappen-Explorer** auf den Knoten **NewEmployeeOrientation**.

15. Öffnen Sie im Designer die Registerkarte **Liste**. Auf dieser Registerkarte werden bestimmte Werte der *Listeninstanz* festgelegt, nicht der *Listenvorlage*. Einige Standardwerte werden jedoch von der Vorlage vererbt.

16. Ändern Sie die Werte auf der Registerkarte **Liste** wie folgt:
    
    -  **Titel:** Neue Mitarbeiter in Seattle
    -  **Listen-URL:** Listen/NewEmployeesInSeattle
    -  **Beschreibung:** Die neuen Mitarbeiter in Seattle

17. Übernehmen Sie den Standardstatus der Kontrollkästchen, speichern Sie die Datei, und schließen Sie den Designer.

18. Im **Projektmappen-Explorer** wird möglicherweise noch der alte Name der Listeninstanz angezeigt. Sollte das der Fall sein: Öffnen Sie das Kontextmenü von **NewEmployeeOrientationInstance**, klicken Sie auf **Umbenennen**, und ändern Sie den Namen in **NewEmployeesInSeattle**.

19. Öffnen Sie die Datei „schema.xml“.

20. Ersetzen Sie im Element des Typs **View** mit „0“ als Wert für **BaseViewID** das vorhandene Element des Typs **ViewFields** durch das unten aufgeführte Markup. (Verwenden Sie exakt diese GUID für das Element **FieldRef** mit dem Namen `Title`.) Zeilenumbrüche können in der automatisch generierten Datei „schema.xml“ an ungewöhnlichen Stellen gesetzt sein. Vergewissern Sie sich, dass Sie wirklich das Starttag und das Endtag des Elements **ViewFields** gefunden haben. Fügen Sie Zeilenumbrüche ein, um den Code besser lesbar zu machen. 

    ```
      <ViewFields>
         <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Employee" />
      </ViewFields>
    ```

21. Ersetzen Sie in der Datei „schema.xml“ im Element des Typs **View** mit „1“ als Wert für **BaseViewID** das vorhandene Element des Typs **ViewFields** durch das folgende Markup. (Verwenden Sie exakt diese GUID für das Element **FieldRef** mit dem Namen `LinkTitle`.)
    
    ```
      <ViewFields>
         <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
      </ViewFields>
    ```

22. Speichern und schließen Sie die Datei „schema.xml“.

23. Öffnen sie die Datei „elements.xml“, die ein untergeordnetes Element der *Listeninstanz* **NewEmployeesInSeattle** ist (nicht die Datei „elements.xml“, die ein untergeordnetes Element der *Listenvorlage* **NewEmployeeOrientation** ist).

24. Füllen Sie in dieser Datei die Liste mit einigen Ausgangsdaten. Hierzu fügen Sie folgendes **Data**-Elementmarkup als untergeordnetes Element des **ListInstance**-Elements hinzu.
    
    ```
      <Data>
      <Rows>
        <Row>
          <Field Name="Title">Tom Higginbotham</Field>
        </Row>
        <Row>
          <Field Name="Title">Satomi Hayakawa</Field>
        </Row>
        <Row>
          <Field Name="Title">Cassi Hicks</Field>
        </Row>
        <Row>
          <Field Name="Title">Lertchai Treetawatchaiwong</Field>
        </Row>
      </Rows>
    </Data>
    ```

25. Speichern und schließen Sie die Datei.

26. Doppelklicken Sie im **Projektmappen-Explorer** auf **Feature1**, um den Feature-Designer zu öffnen. Legen Sie im Designer als **Titel** die Zeichenfolge **Orientierungskomponenten für neue Mitarbeiter** fest und als **Beschreibung** die Zeichenfolge **Listen und andere Komponenten, die zur Orientierung neuer Mitarbeiter im Unternehmen dienen**. Speichern Sie die Datei, und schließen Sie den Designer.

27. Falls **Feature1** im **Projektmappen-Explorer** nicht automatisch umbenannt wurde: Öffnen Sie das Kontextmenü des Elements, klicken Sie auf **Umbenennen**, und geben Sie ihm den Namen **NewEmployeeOrientationComponents**.

28. Öffnen Sie die Datei „Default.aspx“.

29. Suchen Sie das ASP.NET-Element des Typs **Content** mit der ID **PlaceHolderPageTitleInTitleArea**. Ersetzen Sie die Standardzeichenfolge **Page Title** durch **Neue Mitarbeiter nach Standort**.

30. Suchen Sie das ASP.NET-Element des Typs **Content** mit der ID **PlaceHolderMain**. *Ersetzen* Sie dessen Inhalt durch das unten aufgeführte Markup. `_spPageContextInfo` ist ein JavaScript-Objekt, das von SharePoint automatisch in die Seite integriert wird. Die Eigenschaft `webAbsoluteUrl` dieses Objekts gibt die URL des Add-In-Webs zurück.
    
    ```XML
        <p><asp:HyperLink runat="server" 
        NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
        Text="New Employees in Seattle" /></p>
    ```

<a name="Code"> </a>
## <a name="run-the-add-in-and-test-the-list"></a>Ausführen des Add-Ins und Testen der Liste

1. Drücken Sie die Taste F5, um das Add-In bereitzustellen und auszuführen. Visual Studio installiert das Add-In vorübergehend auf Ihrer SharePoint-Testwebsite und führt das Add-In sofort aus. (Weitere Informationen dazu, wie Endbenutzer ein installiertes SharePoint-Add-In ausführen können, finden Sie unter [Nächste Schritte](#Nextsteps)).

2. Die Standardseite des Add-Ins wird geöffnet. Klicken Sie auf **Neue Mitarbeiter in Seattle**, um die Instanz der benutzerdefinierten Liste zu öffnen.
    
    *Abbildung 5: Standardseite und die Seite mit der Listenansicht*

    ![Die Standardseite des Add-Ins mit dem Titel "Neue Mitarbeiter nach Standort" wird angezeigt. Es gibt einen Link mit der Bezeichnung "Neue Mitarbeiter in Seattle". Ein Pfeil von diesem Link zeigt auf die Listenansichtsseite für die Liste. Diese hat den Titel "Neue Mitarbeiter in Seattle" und weist die folgende Liste auf.](../images/9dc5cefe-083a-4807-bee6-473001f23db9.png)

3. Fügen Sie der Liste Elemente hinzu, und löschen Sie Elemente aus der Liste.

4. Schließen Sie zum Beenden der Debugsitzung das Browserfenster, oder beenden Sie das Debuggen in Visual Studio. Jedes Mal, wenn Sie F5 drücken, zieht Visual Studio die vorherige Version des Add-Ins zurück und installiert die neueste.

5. Da Sie mit diesem Add-In und dieser Visual Studio-Lösung auch in anderen Artikeln arbeiten werden, empfiehlt es sich, das Add-In ein letztes Mal zurückzuziehen, sobald Sie eine Weile nicht mehr an ihm arbeiten werden. Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie die Option **Zurückziehen** aus.

## <a name="additional-resources"></a>Weitere Ressourcen

- [Installieren älterer Versionen von Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx)
- [Visual Studio-Dokumentation](https://docs.microsoft.com/de-DE/visualstudio/)

## <a name="next-steps"></a>Nächste Schritte
<a name="Nextsteps"> </a>

Aktuell enthält die Liste noch nicht sehr viele Orientierungsinformationen. Wir werden in den noch folgenden Artikeln dieser Reihe Informationen hinzufügen. Zunächst machen wir jedoch eine kleine Programmierpause und beschäftigen uns mit der Bereitstellung von SharePoint-Add-Ins, im Artikel [Bereitstellung und Installation eines von SharePoint gehosteten SharePoint-Add-Ins](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md).
 
