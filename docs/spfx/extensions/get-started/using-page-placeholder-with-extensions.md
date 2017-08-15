# <a name="using-page-placeholders-from-application-customizer-hello-world-part-2"></a>Verwenden von Seitenplatzhaltern aus dem Anwendungsanpasser (Hello World, Teil 2)

>**Hinweis:** Die SharePoint Framework-Erweiterungen befinden sich derzeit in der Preview-Phase. Änderungen sind vorbehalten. Die Verwendung von SharePoint Framework-Erweiterungen in Produktionsumgebungen wird aktuell nicht unterstützt.

Anwendungsanpasser ermöglichen auch den Zugriff auf bekannte Positionen auf der Seite, die Sie basierend auf Ihren geschäftlichen und funktionalen Anforderungen ändern können. Typische Szenarien sind dynamische Kopf- und Fußzeilen, die auf allen Seiten in SharePoint Online sichtbar sind. 

Dieses Modell ist vergleichbar mit der Verwendung einer UserCustomAction-Sammlung auf einer Website oder in einem Webobjekt zum Zuordnen von benutzerdefiniertem JavaScript-Code, der zum Ändern der Benutzererfahrung auf der Seite dient. Der Hauptunterschied bzw. der Vorteil bei der Verwendung von SPFx-Erweiterung liegt darin, dass bestimmte Elemente immer auf der Seite vorhanden sind, unabhängig von Änderungen an der HTML-/DOM-Struktur bei künftigen Änderungen in SharePoint Online.

In diesem Artikel erweitern wir die Hello World-Erweiterung, die wir im vorherigen Artikel [Erstellen Ihrer ersten SharePoint Framework Erweiterung (Hallo Welt Teil 1)](./build-a-hello-world-extension.md) erstellt haben, um die Verwendung von Seitenplatzhaltern. 

## <a name="getting-access-to-page-placeholders"></a>Zugreifen auf Seitenplatzhalter

Die Erweiterungen des Anwendungsanpassers werden in den Bereichen `Site`, `Web` und `List` unterstützt. Sie können den Bereich steuern, indem Sie entscheiden, wo und wie der Anwendungsanpasser im SharePoint-Mandanten registriert werden soll. Wenn Anwendungsanpasse im Bereich vorhanden ist und gerendert wird, können Sie die folgende Methode verwenden, um auf den Platzhalter zuzugreifen. Nachdem Sie das Platzhalterobjekt erhalten haben, haben Sie die vollständige Kontrolle darüber, was dem Endbenutzer angezeigt wird.

Beachten Sie, dass wir einen bekannten Platzhalter anfordern, indem wir den entsprechenden bekannten Bezeichner verwenden. In diesem Fall greift der Code auf den Kopfzeilenbereich der Seite mit dem Bezeichner `PageHeader` zu. 

```ts
    // Handling the header placeholder
    if (!this._headerPlaceholder) {
      this._headerPlaceholder = this.context.placeholders.tryAttach(
        'PageHeader',
        {
          onDispose: this._onDispose
        });
    }
```

In den folgenden Schritten ändern wir den zuvor erstellten Hello World-Anwendungsanpasser, um auf Platzhalter zuzugreifen und ihren Inhalt zu ändern, indem wir ihnen benutzerdefinierte HTML-Elemente hinzufügen. 

Wechseln Sie in Visual Studio Code (oder Ihre bevorzugte IDE), und öffnen Sie **src\extensions\helloWorld\HelloWorldApplicationCustomizer.ts.**

Fügen Sie `Placeholder` zum Import aus `@microsoft/sp-application-base` hinzu, indem Sie die Importanweisung wie folgt aktualisieren:

```ts
import {
  BaseApplicationCustomizer,
  Placeholder
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
  .header {
    height:60px; 
    text-align:center; 
    line-height:2.5; 
    font-weight:bold;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .footer {
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
  Header: string;
  Footer: string;
}
```

Fügen Sie die folgenden privaten Variablen in der **HelloWorldApplicationCustomizer**-Klasse hinzu. In diesem Szenario können dies lokale Variablen in einer `onRender`-Methode sein. Wenn sie jedoch gemeinsam mit anderen Objekten verwendet werden sollen, definieren Sie sie als private Variablen. 

```ts
export default class HelloWorldApplicationCustomizer
  extends BaseApplicationCustomizer<IHelloWorldApplicationCustomizerProperties> {
  
  // These have been added
  private _headerPlaceholder: Placeholder;
  private _footerPlaceholder: Placeholder;
```

Aktualisieren Sie die `onRender`-Methode mit dem folgenden Code:

* Wir verwenden `this.context.placeholders.tryAttach`, um auf den Platzhalter zuzugreifen.
* Erweiterungscode sollte nicht davon ausgehen, dass der erwartete Platzhalter verfügbar ist.
* Der Code erwartet benutzerdefinierte Eigenschaften mit dem Namen `Header` und `Footer`. Wenn die Eigenschaften vorhanden sind, werden sie innerhalb des Platzhalters gerendert.
* Beachten Sie, dass der Codepfad für die Kopfzeile und die Fußzeile in der Methode unten beinahe identisch ist. Er unterscheidet sich nur durch die verwendeten Variablen und Formatvorlagendefinitionen.

```ts
  @override
  public onRender(): void {

    console.log('CustomHeader.onRender()');
    console.log('Available placeholders: ',
      this.context.placeholders.placeholderNames.join(', '));

    // Handling the header placeholder
    if (!this._headerPlaceholder) {
      this._headerPlaceholder = this.context.placeholders.tryAttach(
        'PageHeader',
        {
          onDispose: this._onDispose
        });

      // The extension should not assume that the expected placeholder is available.
      if (!this._headerPlaceholder) {
        console.error('The expected placeholder (PageHeader) was not found.');
        return;
      }

      if (this.properties) {
        let headerString: string = this.properties.Header;
        if (!headerString) {
          headerString = '(Header property was not defined.)';
        }

        if (this._headerPlaceholder.domElement) {
          this._headerPlaceholder.domElement.innerHTML = `
                <div class="${styles.app}">
                  <div class="ms-bgColor-themeDark ms-fontColor-white ${styles.header}">
                    <i class="ms-Icon ms-Icon--Info" aria-hidden="true"></i> ${escape(headerString)}
                  </div>
                </div>`;
        }
      }
    }

    // Handling the footer placeholder
    if (!this._footerPlaceholder) {
      this._footerPlaceholder = this.context.placeholders.tryAttach(
        'PageFooter',
        {
          onDispose: this._onDispose
        });

      // The extension should not assume that the expected placeholder is available.
      if (!this._footerPlaceholder) {
        console.error('The expected placeholder (PageFooter) was not found.');
        return;
      }

      if (this.properties) {
        let footerString: string = this.properties.Footer;
        if (!footerString) {
          footerString = '(Footer property was not defined.)';
        }

        if (this._footerPlaceholder.domElement) {
          this._footerPlaceholder.domElement.innerHTML = `
                <div class="${styles.app}">
                  <div class="ms-bgColor-themeDark ms-fontColor-white ${styles.footer}">
                    <i class="ms-Icon ms-Icon--Info" aria-hidden="true"></i> ${escape(footerString)}
                  </div>
                </div>`;
        }
      }
    }
  }

```

Fügen Sie die folgende Methode nach der `onRender`-Methode hinzu. In diesem Fall geben wir eine einfache Konsolenmeldung aus, wenn die Erweiterung von der Seite entfernt wird. 

```ts
 private _onDispose(): void {
    console.log('[CustomHeader._onDispose] Disposed custom header.');
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
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"5fc73e12-8085-4a4b-8743-f6d02ffe1240":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"Header":"Header area of the page","Footer":"Footer area in the page"}}}
```
Die vollständige anzufordernde URL sähe in etwa wie folgt aus:

```
contoso.sharepoint.com/Lists/Contoso/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"5fc73e12-8085-4a4b-8743-f6d02ffe1240":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"Header":"Header area of the page","Footer":"Footer area in the page"}}}
```

![Abfragen des Debugging-Manifests für die Seite zulassen](../../../../images/ext-app-debug-manifest-message.png)

Klicken Sie auf die Schaltfläche zum **Laden von Debugging-Skripts**, um weiter Skripts von Ihrem lokalen Host zu laden.

Sie sollten jetzt den benutzerdefinierten Kopf- und Fußzeileninhalt auf der Seite sehen. 

![Benutzerdefinierte Kopf- und Fußzeilenelemente, auf der Seite gerendert](../../../../images/ext-app-header-footer-visible.png)

## <a name="next-steps"></a>Nächste Schritte
Herzlichen Glückwunsch, Sie haben Ihre erste benutzerdefinierte Kopf- und Fußzeile mithilfe des Anwendungsanpassers erstellt! Sie können Ihre Hello World-Erweiterung im nächsten Thema [Bereitstellen Ihrer Erweiterung für die Websitesammlung (Hello World, Teil 3)](./serving-your-extension-from-sharepoint.md) noch weiter entwickeln. Sie erfahren, wie Sie die Hello World-Erweiterung in einer SharePoint-Websitesammlung mit **Debug**-Abfrageparametern bereitstellen und in der Vorschau anzeigen. 
