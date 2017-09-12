# <a name="using-page-placeholders-from-application-customizer-hello-world-part-2"></a>Verwenden von Seitenplatzhaltern aus dem Anwendungsanpasser (Hello World, Teil 2)

>**Hinweis:** Die SharePoint Framework-Erweiterungen befinden sich derzeit in der Preview-Phase. Änderungen sind vorbehalten. Die Verwendung von SharePoint Framework-Erweiterungen in Produktionsumgebungen wird aktuell nicht unterstützt.

Anwendungsanpasser ermöglichen auch den Zugriff auf bekannte Positionen auf der Seite, die Sie basierend auf Ihren geschäftlichen und funktionalen Anforderungen ändern können. Typische Szenarien sind dynamische Kopf- und Fußzeilen, die auf allen Seiten in SharePoint Online sichtbar sind. 

Dieses Modell ist vergleichbar mit der Verwendung einer UserCustomAction-Sammlung auf einer Website oder in einem Webobjekt zum Zuordnen von benutzerdefiniertem JavaScript-Code, der zum Ändern der Benutzererfahrung auf der Seite dient. Der Hauptunterschied bzw. der Vorteil bei der Verwendung von SPFx-Erweiterung liegt darin, dass bestimmte Elemente immer auf der Seite vorhanden sind, unabhängig von Änderungen an der HTML-/DOM-Struktur bei künftigen Änderungen in SharePoint Online.

In diesem Artikel erweitern wir die Hello World-Erweiterung, die wir im vorherigen Artikel [Erstellen Ihrer ersten SharePoint Framework Erweiterung (Hallo Welt Teil 1)](./build-a-hello-world-extension.md) erstellt haben, um die Verwendung von Seitenplatzhaltern.

Sie können die nachfolgend beschriebene Anleitung auch anhand dieses Videos in unserem [YouTube-Kanal „SharePoint Patterns & Practices“](https://www.youtube.com/watch?v=ipRw6o6bOTw&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV) nachvollziehen:

<a href="https://www.youtube.com/watch?v=ipRw6o6bOTw&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV">
<img src="../../../../images/spfx-ext-youtube-tutorial2.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="getting-access-to-page-placeholders"></a>Zugreifen auf Seitenplatzhalter

Die Erweiterungen des Anwendungsanpassers werden in den Bereichen `Site`, `Web` und `List` unterstützt. Sie können den Bereich steuern, indem Sie entscheiden, wo und wie der Anwendungsanpasser im SharePoint-Mandanten registriert werden soll. Wenn Anwendungsanpasse im Bereich vorhanden ist und gerendert wird, können Sie die folgende Methode verwenden, um auf den Platzhalter zuzugreifen. Nachdem Sie das Platzhalterobjekt erhalten haben, haben Sie die vollständige Kontrolle darüber, was dem Endbenutzer angezeigt wird.

Beachten Sie, dass wir einen bekannten Platzhalter anfordern, indem wir den entsprechenden bekannten Bezeichner verwenden. In diesem Fall greift der Code auf den Fußzeilenbereich der Seite mit dem Bezeichner `Bottom` zu. 

```ts
    // Handling the Bottom placeholder
    if (!this._bottomPlaceholder) {
      this._bottomPlaceholder =
        this.context.placeholderProvider.tryCreateContent(
          PlaceholderName.Bottom,
          { onDispose: this._onDispose });
    ...
    }
```

In den folgenden Schritten ändern wir den zuvor erstellten Hello World-Anwendungsanpasser, um auf Platzhalter zuzugreifen und ihren Inhalt zu ändern, indem wir ihnen benutzerdefinierte HTML-Elemente hinzufügen.

Wechseln Sie in Visual Studio Code (oder Ihre bevorzugte IDE), und öffnen Sie **src\extensions\helloWorld\HelloWorldApplicationCustomizer.ts.**

Fügen Sie `PlaceholderContent` und and `PlaceholderName` zum Import aus `@microsoft/sp-application-base` hinzu, indem Sie die Importanweisung wie folgt aktualisieren:

```ts
import {
  BaseApplicationCustomizer, 
  PlaceholderContent,
  PlaceholderName
} from '@microsoft/sp-application-base';
```

Fügen Sie außerdem die folgenden Importanweisungen nach dem `strings`-Import oben in der Datei hinzu:

* In den folgenden Schritten erstellen wir Formatvorlagendefinitionen für die Ausgabe.
* `escape` wird verwendet, um die Eigenschaften des Anwendungsanpassers auzukommentieren.  

```ts
import styles from './AppCustomizer.module.scss';
import { escape } from '@microsoft/sp-lodash-subset'; 
```

Erstellen Sie eine neue Datei mit dem Namen **AppCustomizer.module.scss** im Ordner **src\extensions\helloWorld**. 

Aktualisieren Sie **AppCustomizer.module.scss** wie folgt:

* Hierbei handelt es sich um die Formatvorlagen, die im Ausgabe-HTML-Code für die Kopf- und Fußzeilenplatzhalter verwendet werden.

```css
.app {
  .top {
    height:60px;
    text-align:center;
    line-height:2.5;
    font-weight:bold;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .bottom {
    height:40px;
    text-align:center;
    line-height:2.5;
    font-weight:bold;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
```

Wechseln Sie zurück zu **HelloWorldApplicationCustomizer.ts**, und aktualisieren Sie die **IHelloWorldApplicationCustomizerProperties**-Oberfläche wie folgt, damit sie bestimmte Eigenschaften für Kopf- und Fußzeile hat.

* Wenn Ihr Befehlssatz die ClientSideComponentProperties JSON-Eingabe verwendet, wird sie in das Objekt `BaseExtension.properties` deserialisert. Sie können eine Benutzeroberfläche definieren, um sie zu beschreiben.

```ts
export interface IHelloWorldApplicationCustomizerProperties {
  Top: string;
  Bottom: string;
}
```

Fügen Sie die folgenden privaten Variablen in der **HelloWorldApplicationCustomizer**-Klasse hinzu. In diesem Szenario können dies lokale Variablen in einer `onRender`-Methode sein. Wenn sie jedoch gemeinsam mit anderen Objekten verwendet werden sollen, definieren Sie sie als private Variablen. 

```ts
export default class HelloWorldApplicationCustomizer
  extends BaseApplicationCustomizer<IHelloWorldApplicationCustomizerProperties> {
  
  // These have been added
  private _topPlaceholder: PlaceholderContent | undefined;
  private _bottomPlaceholder: PlaceholderContent | undefined;
```

Aktualisieren Sie den Code der `onInit`-Methode wie folgt:

```ts
  @override
  public onInit(): Promise<void> {
    Log.info(LOG_SOURCE, `Initialized ${strings.Title}`);

    // Added to handle possible changes on the existence of placeholders
    this.context.placeholderProvider.changedEvent.add(this, this._renderPlaceHolders);

    // Call render method for generating the needed html elements
    this._renderPlaceHolders();
    return Promise.resolve<void>();
  }
```


Erstellen Sie eine neue private `_renderPlaceHolders`-Methode mit dem folgenden Code:

* Wir verwenden `this.context.placeholderProvider.tryCreateContent`, um auf den Platzhalter zuzugreifen.
* Erweiterungscode sollte nicht davon ausgehen, dass der erwartete Platzhalter verfügbar ist.
* Der Code erwartet benutzerdefinierte Eigenschaften mit dem Namen `Top` und `Bottom`. Wenn die Eigenschaften vorhanden sind, werden sie innerhalb des Platzhalters gerendert.
* Beachten Sie, dass der Codepfad für die oberen und unteren Platzhalter in der folgenden Methode beinahe identisch ist. Er unterscheidet sich nur durch die verwendeten Variablen und Formatvorlagendefinitionen.

```ts
   private _renderPlaceHolders(): void {

    console.log('HelloWorldApplicationCustomizer._renderPlaceHolders()');
    console.log('Available placeholders: ',
      this.context.placeholderProvider.placeholderNames.map(name => PlaceholderName[name]).join(', '));

    // Handling the top placeholder
    if (!this._topPlaceholder) {
      this._topPlaceholder =
        this.context.placeholderProvider.tryCreateContent(
          PlaceholderName.Top,
          { onDispose: this._onDispose });

      // The extension should not assume that the expected placeholder is available.
      if (!this._topPlaceholder) {
        console.error('The expected placeholder (Top) was not found.');
        return;
      }

      if (this.properties) {
        let topString: string = this.properties.Top;
        if (!topString) {
          topString = '(Top property was not defined.)';
        }

        if (this._topPlaceholder.domElement) {
          this._topPlaceholder.domElement.innerHTML = `
                <div class="${styles.app}">
                  <div class="ms-bgColor-themeDark ms-fontColor-white ${styles.top}">
                    <i class="ms-Icon ms-Icon--Info" aria-hidden="true"></i> ${escape(topString)}
                  </div>
                </div>`;
        }
      }
    }

    // Handling the bottom placeholder
    if (!this._bottomPlaceholder) {
      this._bottomPlaceholder =
        this.context.placeholderProvider.tryCreateContent(
          PlaceholderName.Bottom,
          { onDispose: this._onDispose });

      // The extension should not assume that the expected placeholder is available.
      if (!this._bottomPlaceholder) {
        console.error('The expected placeholder (Bottom) was not found.');
        return;
      }

      if (this.properties) {
        let bottomString: string = this.properties.Bottom;
        if (!bottomString) {
          bottomString = '(Bottom property was not defined.)';
        }

        if (this._bottomPlaceholder.domElement) {
          this._bottomPlaceholder.domElement.innerHTML = `
                <div class="${styles.app}">
                  <div class="ms-bgColor-themeDark ms-fontColor-white ${styles.bottom}">
                    <i class="ms-Icon ms-Icon--Info" aria-hidden="true"></i> ${escape(bottomString)}
                  </div>
                </div>`;
        }
      }
    }
  }

```

Fügen Sie die folgende Methode nach der `_renderPlaceHolders`-Methode hinzu. In diesem Fall geben wir eine einfache Konsolenmeldung aus, wenn die Erweiterung von der Seite entfernt wird. 

```ts
  private _onDispose(): void {
    console.log('[HelloWorldApplicationCustomizer._onDispose] Disposed custom top and bottom placeholders.');
  }
```

Der Code kann nun in SharePoint Online getestet werden.

Wechseln Sie in das Konsolenfenster, in dem `gulp serve` ausgeführt wird, und schauen Sie nach, ob Fehler gemeldet wurden. gulp meldet alle Fehler in der Konsole. Sie müssen sie dann zuerst beheben, bevor Sie fortfahren können.

Wenn Sie die Lösung derzeit noch nicht ausgeführt wird, führen Sie den folgenden Befehl aus, und stellen Sie sicher, dass keine Fehler auftreten.

```
gulp serve --nobrowser
```

Navigieren Sie zu einer sofort einsatzfähigen modernen Liste in SharePoint Online. Dies kann eine Liste oder Bibliothek für die anfänglichen Tests sein. 

Um die Erweiterung zu testen, hängen Sie die folgende Abfragezeichenfolgenparameter an die URL an:

* Beachten Sie, dass die in diesem Abfrageparameter verwendete GUID mit dem ID-Attribut Ihres Anwendungsanpassers übereinstimmen muss, die Sie in **HelloWorldApplicationCustomizer.manifest.json** finden.
* Wir verwenden darüber hinaus Kopf- und Fußzeilen-JSON-Eigenschaften, um dem Anwendungsanpasser Parameter oder Konfigurationen bereitzustellen. In diesem Fall geben wir diese Werte einfach aus, wobei Sie das Verhalten jedoch basierend auf den Eigenschaften in der eigentlichen Produktionsumgebung anpassen können. 

```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"Top":"Top area of the page","Bottom":"Bottom area in the page"}}}
```
Die vollständige anzufordernde URL sähe in etwa wie folgt aus:

```
contoso.sharepoint.com/Lists/Contoso/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"Top":"Top area of the page","Bottom":"Bottom area in the page"}}}
```

![Abfragen des Debugging-Manifests für die Seite zulassen](../../../../images/ext-app-debug-manifest-message.png)

Klicken Sie auf die Schaltfläche zum **Laden von Debugging-Skripts**, um weiter Skripts von Ihrem lokalen Host zu laden.

Sie sollten jetzt den benutzerdefinierten Kopf- und Fußzeileninhalt auf der Seite sehen. 

![Benutzerdefinierte Kopf- und Fußzeilenelemente, auf der Seite gerendert](../../../../images/ext-app-header-footer-visible.png)

## <a name="next-steps"></a>Nächste Schritte
Herzlichen Glückwunsch, Sie haben Ihre erste benutzerdefinierte Kopf- und Fußzeile mithilfe des Anwendungsanpassers erstellt! Sie können Ihre Hello World-Erweiterung im nächsten Thema [Bereitstellen Ihrer Erweiterung für die Websitesammlung (Hello World, Teil 3)](./serving-your-extension-from-sharepoint.md) noch weiter entwickeln. Sie erfahren, wie Sie die Hello World-Erweiterung in einer SharePoint-Websitesammlung mit **Debug**-Abfrageparametern bereitstellen und in der Vorschau anzeigen. 
