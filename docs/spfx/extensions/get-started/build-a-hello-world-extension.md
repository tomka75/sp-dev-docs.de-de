# <a name="build-your-first-sharepoint-framework-extension-hello-world-part-1"></a>Erstellen Ihrer ersten SharePoint-Framework-Erweiterung (Hello World, Teil 1)

>**Hinweis:** SharePoint-Framework-Erweiterungen befinden sich derzeit in der Vorschauphase. Änderungen sind vorbehalten. Ihre Verwendung in Produktionsumgebungen wird aktuell nicht unterstützt.

SharePoint-Framework (SPFx)-Erweiterungen sind clientseitige Komponenten, die im Kontext einer SharePoint-Seite ausgeführt werden. Sie können Erweiterungen in SharePoint Online bereitstellen und mithilfe aktueller JavaScript-Tools und -Bibliotheken erstellen.

Sie können die in diesem Artikel beschriebenen Schritte anhand des Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV) nachvollziehen. 

<a href="https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV">
<img src="../../../../images/spfx-ext-youtube-tutorial1.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="create-an-extension-project"></a>Erstellen eines Erweiterungsprojekts

1. Erstellen Sie an einem Speicherort Ihrer Wahl ein neues Projektverzeichnis:

    ```
    md app-extension
    ```

2. Wechseln Sie in das Projektverzeichnis:

    ```
    cd app-extension
    ```

3. Führen Sie den Yeoman-SharePoint-Generator aus, um eine neue HelloWorld-Erweiterung zu erstellen:

    ```
    yo @microsoft/sharepoint
    ```

4. Es werden verschiedene Eingabeaufforderungen angezeigt. Gehen Sie wie folgt vor:

    * Übernehmen Sie den Standardwert **app-extension** als Lösungsnamen, und drücken Sie die **EINGABETASTE**.
    * Wählen Sie **Use the current folder** aus, und drücken Sie die **EINGABETASTE**.
    * Wählen Sie **N**, damit die Erweiterung auf jeder Website explizit installiert werden muss, wenn sie verwendet wird. 
    * Wählen Sie **Extension (Preview)** als den zu erstellenden clientseitigen Komponententyp aus. 
    * Wählen Sie **Application Customizer (Preview)** als den zu erstellenden Erweiterungstyp aus.

5. Über die nächsten Eingabeaufforderungen werden spezifische Informationen zu der Erweiterung abgefragt. Gehen Sie wie folgt vor:

    * Übernehmen Sie den Standardwert **HelloWorld** als Namen für Ihre Erweiterung, und drücken Sie die **EINGABETASTE**.
    * Übernehmen Sie den Standardwert **HelloWorld description** als Beschreibung Ihrer Erweiterung, und drücken Sie die **EINGABETASTE**.

    ![Yeoman-SharePoint-Generator fordert zur Erstellung einer Erweiterungslösung auf](../../../../images/ext-yeoman-app-prompts.png)

    > **Hinweis:** Wenn der verwendete Erweiterungsname zu lang ist, können Probleme auftreten. Mit den bereitgestellten Eingaben wird ein Aliaseintrag für die JSON-Manifestdatei des Application Customizer generiert. Falls der Alias mehr als 40 Zeichen enthält, wird eine Ausnahme ausgelöst, wenn Sie versuchen, die Erweiterung mit `gulp serve --nobrowser` zu verarbeiten. Sie können dieses Problem beheben, indem Sie den Aliaseintrag später aktualisieren.

    An diesem Punkt installiert Yeoman die erforderlichen Abhängigkeiten und erstellt ein Gerüst für die Lösungsdateien sowie die **HelloWorld**-Erweiterung. Das kann einige Minuten dauern. 

    Nach Abschluss der Gerüsterstellung sollte folgende Erfolgsmeldung angezeigt werden:

    ![Erfolgreiche Erstellung eines Gerüsts für die clientseitige SharePoint-Lösung](../../../../images/ext-yeoman-app-complete.png)

    Informationen zur Behebung etwaiger Fehler finden Sie unter [Bekannte Probleme](../basics/known-issues).

6. Geben Sie nach der Erstellung des Lösungsgerüsts Folgendes in die Konsole ein, um Visual Studio Code zu starten:

    ```
    code .
    ```

    >**Hinweis:** Da die clientseitige SharePoint-Lösung auf HTML/TypeScript basiert, können Sie zur Erstellung Ihrer Erweiterung jeden Code-Editor verwenden, der clientseitige Entwicklung unterstützt.

    Wie Sie sehen, sieht die Standardlösungsstruktur wie die Lösungsstruktur clientseitiger Webparts aus. Hierbei handelt es sich um die grundlegende SharePoint-Framework-Lösungsstruktur, die für alle Lösungstypen vergleichbare Konfigurationsoptionen bereitstellt.

    ![SharePoint-Framework-Lösung nach der Erstellung des anfänglichen Gerüsts](../../../../images/ext-app-vscode-solution-structure.png)

7. Öffnen Sie **HelloWorldApplicationCustomizer.manifest.json** im Ordner „src\extensions\helloWorld“.

    In dieser Datei sind der Erweiterungstyp und ein eindeutiger Bezeichner für die Erweiterung definiert. Sie benötigen diese ID später, um die Erweiterung zu debuggen und in SharePoint bereitzustellen.

    ![JSON-Inhalt des Application Customizer-Manifests](../../../../images/ext-app-vscode-manifest.png)

## <a name="code-your-application-customizer"></a>Codieren des Application Customizer 
Öffnen Sie die Datei **HelloWorldApplicationCustomizer.ts** im Ordner **src\extensions\helloWorld**.

Beachten Sie, dass die Basisklasse für den Application Customizer aus dem **sp-application-base**-Paket importiert wird, das den SharePoint-Framework-Code enthält, der für den Application Customizer erforderlich ist.

![Import-Anweisung für BaseApplicationCustomizer aus @microsoft/sp-application-base](../../../../images/ext-app-vscode-app-base.png)

Die Logik für den Application Customizer ist in der **onInit**-Methode enthalten.

- **onInit()** wird aufgerufen, wenn die clientseitige Erweiterung erstmals auf der Seite aktiviert wird. Dieses Ereignis tritt nach Zuweisung von ```this.context``` und ```this.properties``` ein. Wie bei Webparts gibt ```onInit()``` eine Zusage zurück, die Sie verwenden können, um asynchrone Operationen ausführen.

>**Hinweis:** Der Klassenkonstruktor wird in einer frühen Phase aufgerufen, wenn ```this.context``` und ```this.properties``` noch nicht definiert sind. Benutzerdefinierte Initiierungslogik wird an dieser Stelle nicht unterstützt.

Im Folgenden werden die Inhalte von **onInit()** in der Standardlösung aufgelistet. Die Standardlösung schreibt ein Protokoll in das Dev Dashboard und zeigt dann beim Rendern der Seite eine einfache JavaScript-Warnung an.

![Standardmäßige onInit-Methode im Code](../../../../images/ext-app-vscode-methods.png)

Wenn Ihr Application Customizer die JSON-Eingabe **ClientSideComponentProperties** verwendet, erfolgt die Deserialisierung in das **BaseExtension.properties**-Objekt. Sie können eine Benutzeroberfläche definieren, um dies zu beschreiben. Die Standardvorlage sucht nach einer Eigenschaft mit dem Namen **testMessage**. Wenn diese Eigenschaft bereitgestellt wird, wird sie in einer Warnmeldung ausgegeben.

## <a name="debug-your-application-customizer-using-gulp-serve-and-query-string-parameters"></a>Debuggen Ihres Application Customizer mit „gulp serve“ und Abfragezeichenfolgen-Parametern
SharePoint-Framework-Erweiterungen können derzeit nicht mit der lokalen Workbench getestet werden. Sie müssen sie mit einer SharePoint Online-Live-Website testen. Hierzu ist es nicht erforderlich, die Anpassung im App-Katalog bereitzustellen, was das Debugging vereinfacht und beschleunigt. 

Zunächst führen Sie den folgenden Befehl aus, um den Code zu kompilieren und die kompilierten Dateien auf Ihrem lokalen Computer zu hosten:

```
gulp serve --nobrowser
```

>**Hinweis:** Wenn Sie das SPFx-Entwicklerzertifikat noch nicht installiert haben, meldet Workbench, dass das Laden von Skripts von „localhost“ nicht konfiguriert ist. Halten Sie in diesem Fall den aktuell im Konsolenfenster ausgeführten Prozess an, und führen Sie in der Konsole des Projektverzeichnisses den Befehl `gulp trust-dev-cert` aus, um das Entwicklerzertifikat zu installieren; führen Sie dann den Befehl `gulp serve --nobrowser` erneut aus.

Sie verwenden die Option ```--nobrowser```, da ein Start der lokalen Workbench nicht nötig ist, weil Erweiterungen nicht lokal gedebuggt werden können.

Wenn der Code ohne Fehler kompiliert wurde, verarbeitet er das resultierende Manifest von http://localhost:4321.

![Gulp serve](../../../../images/ext-app-gulp-serve.png)

Zum Testen der Erweiterung wechseln Sie zu einer Seite mit der modernen Listenansicht in Ihrer SharePoint-Umgebung, und fügen Sie die folgenden Abfragezeichenfolgen-Parameter an die URL an: Beachten Sie, dass Sie die ID entsprechend Ihrem eigenen Erweiterungsbezeichner aktualisieren müssen. Dieser ist in der Datei **HelloWorldApplicationCustomizer.manifest.json** verfügbar.

```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"testMessage":"Hello as property!"}}}
```

Weitere Details zu den URL-Abfrageparametern:

* **loadSPFX=true** – Dieser Parameter stellt sicher, dass das SharePoint-Framework auf der Seite geladen wird. Aus Leistungsgründen wird das Framework erst geladen, wenn mindestens eine Erweiterung registriert ist. Da keine Komponenten registriert sind, müssen Sie das Framework explizit laden.

* **debugManifestsFile** – Dieser Parameter gibt an, dass lokal verarbeitete SPFx-Komponenten geladen werden sollen. Das Ladeprogramm sucht nur an zwei Stellen nach Komponenten: im App-Katalog (nach Komponenten der bereitgestellten Lösung) und auf dem SharePoint-Manifestserver (nach den Systembibliotheken).

* **customActions:** – Simuliert eine benutzerdefinierte Aktion. Wenn Sie diese Komponente auf einer Website bereitstellen und registrieren, erstellen Sie dieses **CustomAction**-Objekt und beschreiben die verschiedenen Eigenschaften, die Sie dafür festlegen können. 
    * **Key** – Verwenden Sie die GUID der Erweiterung als Schlüssel, der der benutzerdefinierten Aktion zuzuordnen ist. Dieser muss dem ID-Wert der Erweiterung entsprechen, der in der JSON-Manifestdatei der Erweiterung zur Verfügung steht.
    * **Location** – Der Typ der benutzerdefinierten Aktion. Verwenden Sie „ClientSideExtension.ApplicationCustomizer“ für die Application Customizer-Erweiterung.
    * **Properties** – Ein optionales JSON-Objekt mit Eigenschaften, die über das Mitglied **this.properties** zur Verfügung stehen. In diesem „HelloWorld“-Beispiel definiert es eine Eigenschaft „testMessage“.


Wechseln Sie zu einer modernen Liste in SharePoint Online. Dies kann eine Liste oder eine Bibliothek sein. Application Customizers werden ebenfalls auf modernen Seiten und auf der Seite „Websiteinhalte“ unterstützt. 

Erweitern Sie die URL mit den beschriebenen zusätzlichen Abfrageparametern. Beachten Sie, dass Sie die GUID entsprechend der ID des benutzerdefinierten Application Customizer aktualisieren müssen. 

Die vollständige URL sollte ähnlich wie im folgenden Beispiel aussehen:

```
contoso.sharepoint.com/Lists/Contoso/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"testMessage":"Hello as property!"}}}
```

![Abfragen des Debugging-Manifests für die Seite zulassen](../../../../images/ext-app-debug-manifest-message.png)

Wählen Sie **Load debug scripts**, um weiter Skripts von Ihrem lokalen Host zu laden.

Die Warnmeldung sollte nun auf Ihrer Seite angezeigt werden.

![Warnmeldung „Hello as property“](../../../../images/ext-app-alert-sp-page.png)

Diese Warnung wird von der SharePoint-Framework-Erweiterung ausgelöst. Da Sie die **testMessage**-Eigenschaft als Teil der Debug-Abfrageparameter bereitgestellt haben, ist sie in der Warnmeldung enthalten. Sie können Ihre Erweiterungsinstanzen auf Grundlage der Clientkomponenteneigenschaften konfigurieren, die für die Instanz auch im Laufzeitmodus übergeben werden. 

> **Hinweis:** Wenn Sie Probleme beim Debuggen haben, überprüfen Sie die URL-Abfrageparameter für die Abfrage. Einige Browser codieren die Parameter, und in einigen Fällen wirkt sich dies auf das Verhalten aus. 

## <a name="next-steps"></a>Nächste Schritte
Herzlichen Glückwunsch! Ihre erste SharePoint-Framework-Erweiterung läuft. Informationen zum weiteren Ausbau der Erweiterung erfahren Sie unter [Verwenden von Seitenplatzhaltern aus dem Application Customizer (Hello World, Teil 2)](./using-page-placeholder-with-extensions.md). Dort verwenden Sie dasselbe Projekt und nutzen spezifische Inhaltsplatzhalter zum Ändern der Benutzeroberfläche von SharePoint. Beachten Sie, dass der Befehl ```gulp serve``` immer noch im Konsolenfenster ausgeführt wird (oder in Visual Studio Code, falls Sie den Editor verwenden). Sie können ihn einfach weiterlaufen lassen und zum nächsten Artikel wechseln.
