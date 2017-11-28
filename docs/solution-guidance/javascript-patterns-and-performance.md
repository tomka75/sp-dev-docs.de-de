---
title: JavaScript-Muster und Leistung
ms.date: 11/03/2017
ms.openlocfilehash: d9f125657f65da7da770e36e7c1c314759a05c29
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="javascript-patterns-and-performance"></a>JavaScript-Muster und Leistung

Vor Jahren ASP.NET erhielten wir die serverseitige UI-Steuerelement rendern, und es wurde eine gute. Diese serverseitige rendern, erfordert jedoch voll vertrauenswürdiger Code. Nun, da wir auf SharePoint und Office 365 gewechselt haben, ist voll vertrauenswürdiger Code nicht mehr eine Option. Dies bedeutet, dass mehr nicht serverseitige Benutzeroberfläche Steuerelementwiedergabe für uns funktionieren.

Noch, benötigen Unternehmen noch benutzerdefinierten UI-Funktionalität für ihre Websites und apps. Dies bedeutet, dass benutzerdefinierte Funktionen der Benutzeroberfläche von der Serverseite in die clientseitige verschoben werden muss. 

Clientseitige JavaScript ist nun die bessere Wahl für das Rendern der UI-Steuerelement.

## <a name="JavaScriptPatterns"></a>JavaScript-Muster

Da clientseitige JavaScript der Pfad ist, was die besten Möglichkeiten zum Implementieren des clientseitigen JavaScript sind? Wie Einstieg eine?

Es gibt mehrere Optionen aus:

|Option|Beschreibung|
|:---|:---|
|Einbetten von JavaScript | [Site.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.site.usercustomactions.aspx) oder [Web.UserCustomActions](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.web.usercustomactions.aspx) für die Aufnahme Skript direkt in das Seitenmarkup zu erlauben. Dies wird in dem [Startladeprogramm Muster](#LoaderPattern) erläutert verwendet.|
|Anzeigevorlagen | Gilt für Ansichten und Suche. Sie müssen keine Art von einer app oder Anbieter bereitstellen Code gehostet. Es ist einfach eine JavaScript-Datei, die in der Formatbibliothek (z. b) zum Anpassen von Ansichten hochgeladen werden kann. Sie können eine beliebige Ansicht mithilfe von JavaScript erforderlich erstellen.|
|Gehostete SharePoint-Add-Ins | Verwendet JSOM für die Kommunikation mit der Hostwebsite oder über das Web-Add-in. Es ermöglicht den Zugriff auf den Webproxy für cross-Domain-Aufrufe|
|Vom Anbieter gehosteten-Add-Ins | Ermöglicht die Erstellung von komplexen Anwendungen für eine Vielzahl von Technologie-Stapel - Beibehaltung sichere Integration in SharePoint|
|JSLink | Ermöglicht es Ihnen, laden eine oder mehrere JavaScript-Dateien in vielen OOTB-Webparts und Ansichten|
|ScriptEditor-Webpart | Fügen Sie das Skript direkt oder über Script-Tags durch Markup zum Erstellen komplexer einseitige Applications vollständig in die SharePoint-Website gehostet geladen|

Sind nicht der Meinung, dass Sie in diese Auswahlmöglichkeiten gesperrt sind, wenn Sie glauben, dass eine andere Option für Ihre Situation besser wäre. 

## <a name="JavaScriptPerformance"></a>JavaScript-Leistung

In jedem Schritt des Entwicklungsprozesses ist es wichtig, Leistung im Hinterkopf behalten. Hier sind einige Punkte, die einen großen Unterschied in JavaScript Leistung vornehmen:

|Option|Beschreibung|
|:---|:---|
|[Reduzieren Sie die Anzahl von Anforderungen](#ReduceTheNumberOfRequests) | Weniger Anfragen bedeutet weniger Roundtrips zum Server reduziert die Latenz.|
|[Rufen Sie nur die benötigten Daten ab](#RetrieveOnlyTheDataYouNeed) | Reduzieren Sie die Menge der Daten, die über das Netzwerk gesendet. Außerdem wird die Serverlast reduziert.|
|[Eine gute Seite Load-Erfahrung bereitstellen](#ProvideAGoodUserExperience) | Behalten Sie die Benutzeroberfläche für den Benutzer schnell. Zum Beispiel aktualisiert die Menüs auf der Seite *vor dem* starten Sie des Herunterladens von 100 Einträge.|
|[Verwenden Sie asynchrone Aufrufe und Muster nach Möglichkeit](#EverythingIsAsynchronous) | Abruf ist eine schwerer Belastung auf die Leistung als die Verwendung eines asynchronen Aufrufs oder Rückruf.| 
|[Das Zwischenspeichern der ist Schlüssel](#ClientSideCaching) | Zwischenspeichern verringert die Belastung der Server weiter und sofortige Leistungssteigerung.|
|[Vorbereiten Sie für weitere Ansichten von Seiten als jemals gedacht.](#PriceOfPopularity) | Eine Daten fett Angebotsseite ist Ordnung, wenn Sie nur ein paar Treffer verfügen. Aber wenn Sie Tausende von aufrufen möchten, können, die wirklich Leistung beeinflussen.|

## <a name="WhatIsMyCodeDoing"></a>Was ist mein Code tun

Aus Leistungsgründen ist es wichtig, wissen ausgeführten Code zu einem beliebigen Zeitpunkt. Auf diese Weise können Sie die Möglichkeiten zur Verbesserung der Effizienz zu identifizieren. Im folgenden sind einige Methoden genau das, was ein.

### <a name="ReduceTheNumberOfRequests"></a>Reduzieren Sie die Anzahl von Anforderungen

Stellen Sie die wenigsten und kleinsten Anfragen immer möglich. Jeder Anforderung, den Sie ausschließen reduziert die Leistung Last auf dem Server und auf dem Client. Und die Belastung der Leistung durch Ausführen einer kleineren Anforderung weiter reduziert.

Es gibt verschiedene Möglichkeiten, Anfragen und reduziert Anforderungsgröße.

- Die Anzahl der JavaScript-Dateien in der Produktion. Trennen die JavaScript-Dateien funktioniert auch für die Entwicklung, jedoch nicht so gut für die Produktion. Kombinieren von JavaScript-Dateien in einer einzigen JavaScript-Datei oder als wenige JavaScript-Dateien wie möglich.
- Dateigrößen zu reduzieren. Minimieren Sie die Produktion JavaScript-Dateien durch Zeilenumbrüche, Leerzeichen und Kommentare entfernen. Es gibt verschiedene JavaScript minify Programme und Websites, die Sie verwenden können, um Ihre JavaScript Dateigrößen erheblich verringert.
- Verwenden Sie die Browser Zwischenspeichern von Dateien, um Anfragen zu verringern. Die aktualisierte [Ladeprogramm Muster](#LoaderPattern) unten ist eine gute Möglichkeit, diese Idee erweitern.

### < einen Namen "RetrieveOnlyTheDataYouNeed" ></a> nur die benötigten Daten abrufen

Wenn Sie Daten anfordern, denken Sie daran, konzentrieren Sie sich Ihre Anforderungen an, was Sie tatsächlich benötigen. Download einen gesamten Artikel zum Abrufen des Titels, beispielsweise verringert Leistung erheblich.

- Verwenden Sie Server zu filtern, wählen und Grenzwerte Datenverkehr über das Netzwerk zu minimieren.
- Anzufordern Sie nicht alle Artikel, wenn Sie nur die ersten fünf als weiteres Beispiel möchten.
- Stellen Sie nicht für die gesamte Eigenschaftenbehälter, wenn Sie nur eine Eigenschaft möchten. Ein Beispiel ein Skripts benötigt nur eine Eigenschaft, aber angefordert gesamte Eigenschaftensammlung der herausstellte 800 KB sein. Beachten Sie außerdem, dass die Größe eines Objekts kann jetzt Neuigkeiten nur ein paar Kilobyte Megabyte weiter unten in den Produktlebenszyklus werden im Laufe der Zeit ändern kann. 

### <a name="DontRequestDataYouWillDiscard"></a>Keine Daten anfordern, dass Sie nicht verwendete verwerfen werden

Wenn Sie mehr Daten abrufen, als Sie tatsächlich verwenden, betrachten Sie es als eine Möglichkeit zum verbessern die ursprüngliche Abfrage filtern. 

- Fordern Sie nur die Felder, die Sie benötigen, wie Namen und die Adresse, die nicht den gesamten Datensatz.
- Stellen Sie bestimmte, absichtliche Filter Anforderungen. Beispielsweise, wenn Sie die verfügbaren Artikel auflisten möchten, rufen Sie den Titel, PublishingDate und Autor. Lassen Sie die restlichen Felder aus der Anforderung.

### <a name="ProvideAGoodUserExperience"></a>Geben Sie eine gute benutzererfahrung

Darstellung, inkonsistente Benutzeroberflächen beeinträchtigen nicht nur Leistung, sondern auch wahrgenommenen Leistung. Schreiben von Code in so, dass eine reibungslose Umgebung zu schaffen.

- Verwenden Sie ein Drehfeld, um anzugeben, dass Dinge laden oder Zeit.
- Die Reihenfolge der Ausführung für den Code verstehen, und es für die beste benutzerumgebung Form. Angenommen, wenn große Datenmengen vom Server abgerufen werden soll, und Sie die Benutzeroberfläche durch ein Menü Ausblenden von ändern möchten, blenden Sie aus, klicken Sie im Menü zuerst. Verhindert, die eine versetzte UI-Erfahrung für den Benutzer ein.

## <a name="EverythingIsAsynchronous"></a>Alles wird asynchron

Jede Codeaktivität im Browser sollte asynchronen betrachtet werden. Laden Ihre Dateien in einer Reihenfolge, müssen Sie warten, bis das DOM geladen und Ihre Anfragen an SharePoint werden mit verschiedenen Geschwindigkeit abgeschlossen. 

- Verstehen der Funktionsweise des Codes in der Zeit.
- Verwenden von Ereignissen und Rückrufen anstelle von Abfragen.
- Versprechen verwenden. In jQuery sind sie **Zurückgestellt** -Objekten aufgerufen. Ähnliche Konzepte in Q, WinJS und ES6 sind vorhanden.
- Verwenden des asynchronen Aufrufs wird nicht asynchronen Aufrufs an.
- Verwenden Sie asynchrone jedes Mal, wenn eine Verzögerung könnte:
    - Während einer AJAX-Anforderung.
    - Während eine erhebliche DOM-Bearbeitung.

Asynchrone Muster Verbesserung von Leistung und erhöhen die Reaktionsgeschwindigkeit und das effektive Verketten von abhängigen Aktionen ermöglichen.

## <a name="ClientSideCaching"></a>Das clientseitige Zwischenspeichern

Das clientseitige Zwischenspeichern ist der meisten häufig verpassten Leistungssteigerungen, den, die Sie dem Code hinzufügen können.

Es gibt drei unterschiedliche Standorten Ihre Daten zwischengespeichert werden können:

|Option|Beschreibung|
|:---|:---|
|Sitzungsinformationen|Speichert Daten als Schlüssel/Wert-Paar auf dem Client. Dies ist pro Sitzungsspeicher, die immer als Zeichenfolgen gespeichert ist. <br /> JSON.stringify() konvertiert JavaScript-Objekte in Zeichenfolgen, das zum Speichern von Objekten unterstützt.
|Lokaler Speicher|<p>Speichert Daten als Schlüssel/Wert-Paar auf dem Client. Dies ist dauerhaft in allen Sitzungen, die immer als Zeichenfolgen gespeichert ist.</p><p>JSON.stringify() konvertiert JavaScript-Objekte in Zeichenfolgen, das zum Speichern von Objekten unterstützt.</p>|
|Lokale Datenbank|Speichert relationale Daten auf dem Client. Als Datenbank-Engine wird häufig SQL-Lite verwendet.<br>Lokale Datenbankspeicher ist nicht immer verfügbar auf allen Browsern&mdash;Ziel Browserunterstützung überprüfen

Zwischenspeichern, berücksichtigen Sie beim die Speichergrenzwerte für Sie verfügbar und Aktualität Ihrer Daten. 
- Wenn Sie das Ende der Speichergrenzwerte erreicht, kann es ratsam, entfernen Sie die zwischengespeicherten Daten älteren oder weniger wichtigen sein. 
- Verschiedene Arten von Daten können schneller als andere veralten. Eine Liste mit Newsartikeln veraltete in fünf bis zehn Minuten werden kann, jedoch Profilname eines Benutzers kann für mindestens 24 Stunden häufig sicher zwischengespeichert. 

Lokale und Sitzung Speicher nicht integrierten Ablauf haben, aber führen Sie Cookies. Sie können Ihre Daten in ein Cookie Ablauf in Ihrer lokalen Kopie und Sitzung Speicher hinzufügen binden. Sie können einen Speicher-Wrapper, der ein Ablaufdatum umfasst auch aktivieren Sie dieses Kontrollkästchen in Ihrem Code.

## <a name="PriceOfPopularity"></a>Der Preis des Beliebtheit

Wie oft werden Ihre Seite angezeigt? In der klassischen Szenario wird auf der Homepage für des Unternehmens als Startseite für alle Browser in der gesamten Organisation festgelegt. Klicken Sie dann erhalten Sie plötzlich weitaus größere Datenverkehr, als Sie schon einmal gedacht. Jedes Byte des Inhalts wird plötzlich im Server-Leistung und Bandbreite, der Ihre Homepage vergrößert.

Lösung: wechseln Licht auf der Homepage und ein Link zu den anderen Inhalt.

Daten fett Dashboards sind auch ein Kandidat für eine vom Anbieter gehosteten app die unabhängig voneinander zu skalieren kann.

## <a name="LoaderPattern"></a>Das Muster Ladeprogramm

Das Ziel des Musters Ladeprogramm ist, geben Sie eine Möglichkeit, eine unbekannte Anzahl von remote-Skripts in einer Website einbetten, ohne dass Sie die Website aktualisieren. Die Updates auf dem CDN remote ausgeführt werden können und alle Websites aktualisiert.

Das Muster Ladeprogramm erstellt eine URL mit Datums- und Zeitstempel am Ende, damit die Datei nicht zwischengespeichert werden. Richtet jQuery als Abhängigkeit auf die Datei, und dann führt eine Funktion im Ladeprogramm aus. Dadurch wird sichergestellt, dass Ihre benutzerdefinierte JavaScript geladen wird, nachdem jQuery geladen ist.

PnP-dev\Samples\Core.JavaScript\Core.JavaScript.Embedder\Program.cs:

```csharp
static void Main(string[] args)
{
    ContextManager.WithContext((context) =>
        // this is the script block that will be embedded into the page
        // in practice this can be done during provisioning of the site/web
        // make sure to include ';' at end to play nice with page embedding
        // using the script on demand feature built into SharePoint we load jQuery, then our remote loader(pnp-loader.js or pnp-loader-cached.js) file using a dependency
        var script = @"(function (loaderFile, nocache) {
                                var url = loaderFile + ((nocache) ? '?' + encodeURIComponent((new Date()).getTime()) : '');
                                SP.SOD.registerSod('pnp-jquery.js', 'https://localhost:44324/js/jquery.js');
                                SP.SOD.registerSod('pnp-loader.js', url);
                                SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');
                                SP.SOD.executeFunc('pnp-loader.js', null, function() {});
                        })('https://localhost:44324/pnp-loader.js', true);";


        // this version of the script along with pnp-loaderMDS.js (or pnp-loaderMDS-cached.js) handles pages where the minimum download strategy is active
        var script2 = @"ExecuteOrDelayUntilBodyLoaded(function () {
                            var url = 'https://localhost:44324/js/pnp-loaderMDS.js?' + encodeURIComponent((new Date()).getTime());
                            SP.SOD.registerSod('pnp-jquery.js', 'https://localhost:44324/js/jquery.js');
                            SP.SOD.registerSod('pnp-loader.js', url);
                            SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');
                            SP.SOD.executeFunc('pnp-loader.js', null, function () {
                                if (typeof pnpLoadFiles === 'undefined') {
                                    RegisterModuleInit('https://localhost:44324/js/pnp-loaderMDS.js', pnpLoadFiles);
                                } else {
                                    pnpLoadFiles();
                                }
                            });    
                        });";

        // load the collection of existing links
        var links = context.Site.RootWeb.UserCustomActions;
        context.Load(links, ls => ls.Include(l => l.Title));
        context.ExecuteQueryRetry();

        // this block handles deleting previous test custom actions
        var doDelete = false;

        foreach (var link in links.ToArray().Where(l => l.Title.Equals("MyTestCustomAction", StringComparison.OrdinalIgnoreCase)))
        {
            link.DeleteObject();
            doDelete = true;
        }

        if (doDelete)
        {
            context.ExecuteQueryRetry();
        }

        // now we embed our script into the user custom action
        var newLink = context.Site.RootWeb.UserCustomActions.Add();
        newLink.Title = "MyTestCustomAction";
        newLink.Description = "Doing some testing.";
        newLink.ScriptBlock = script2;
        newLink.Location = "ScriptLink";
        newLink.Update();
        context.ExecuteQueryRetry();
    });
}
```

Die `SP.SOD.registerSodDep('pnp-loader.js', 'pnp-jquery.js');` richtet die Abhängigkeit und `SP.SOD.executeFunc('pnp-loader.js', null, function() {});` erzwingt jQuery vor dem Laden des benutzerdefinierten JavaScript vollständig geladen.

Die `newLink.ScriptBlock = script2;` und `newLink.Location = "ScriptLink";` sind die wichtigsten Punkte dies in die Aktion des Benutzers Kunden hinzufügen.

Die Datei pnp loader.js lädt dann eine Liste der JavaScript-Dateien mit eine Zusage, die ausgeführt werden kann, wenn jeder Datei geladen wird.

PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js:

```javascript
(function () {

    var urlbase = 'https://localhost:44324';
    var files = [
        '/js/pnp-settings.js',
        '/js/pnp-core.js',
        '/js/pnp-clientcache.js',
        '/js/pnp-config.js',
        '/js/pnp-logging.js',
        '/js/pnp-devdashboard.js',
        '/js/pnp-uimods.js'
    ];

    // create a promise
    var promise = $.Deferred();

    // this function will be used to recursively load all the files
    var engine = function () {

        // maintain context
        var self = this;

        // get the next file to load
        var file = self.files.shift();

        var fullPath = urlbase + file;

        // load the remote script file
        $.getScript(fullPath).done(function () {
            if (self.files.length > 0) {
                engine.call(self);
            }
            else {
                self.promise.resolve();
            }
        }).fail(self.promise.reject);
    };

    // create our "this" we will apply to the engine function
    var ctx = {
        files: files,
        promise: promise
    };

    // call the engine with our context
    engine.call(ctx);

    // give back the promise
    return promise.promise();

})().done(function () {
    /* all scripts are loaded and I could take actions here */
}).fail(function () {
    /* something failed, take some action here if needed */
});
```

Die Datei pnp loader.js werden nicht zwischengespeichert und dem eignet sich gut für eine Entwicklungsumgebung. Die Datei pnp-Ladeprogramm-cached.js ersetzt die `$.getScript` -Funktion mit einer `$.ajax` -Funktion die ermöglicht die Browser Zwischenspeichern von Dateien und ist besser geeignet für die Produktion.

Aus PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-loader.js

```javascript
    // load the remote script file
    $.ajax({
        type: 'GET',
        url: fullPath,
        cache: true,
        dataType: 'script'
    }).done(function () {
        if (self.files.length > 0) {
            engine.call(self);
        }
        else {
            self.promise.resolve();
        }
    }).fail(self.promise.reject);
```

Dieses Muster vereinfacht die Bereitstellung und auf Websites aktualisiert. Es ist besonders hilfreich beim Bereitstellen von oder in Tausenden von Websitesammlungen aktualisieren.

## <a name="CachingCurrentUserInfo"></a>Den aktuellen Benutzer Zwischenspeichern

Wenn die Benutzerinformationen bereits zwischengespeichert wird, ruft diese Funktion die Daten aus dem Sitzungscache ab. Wenn die Benutzerinformationen nicht im Cache gespeichert ist, ruft es die bestimmte Benutzerinformationen wir müssen und in den Cache gespeichert.

Es wird auch zurückgestellt (jQuery-Version des Zusage) verwendet. Wenn wir die Daten aus dem Cache oder vom Server erhalten möchten, ist die verzögerte behoben. Wenn ein Fehler vorliegt, wird die verzögerte abgelehnt.

Aus PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-core.js:

```javascript
    getCurrentUserInfo: function (ctx) {

        var self = this;

        if (self._currentUserInfoPromise == null) {

            self._currentUserInfoPromise = $.Deferred(function (def) {

                var cachingTest = $pnp.session !== 'undefined' && $pnp.session.enabled;

                // if we have the caching module loaded
                if (cachingTest) {
                    var userInfo = $pnp.session.get(self._currentUserInfoCacheKey);
                    if (userInfo !== null) {
                        self._currentUserInfo = userInfo;
                        def.resolveWith(ctx || self._currentUserInfo, [self._currentUserInfo]);
                        return;
                    }
                }

                // send the request and allow caching
                $.ajax({
                    method: 'GET',
                    url: '/_api/SP.UserProfiles.PeopleManager/GetMyProperties?$select=AccountName,DisplayName,Title',
                    headers: { "Accept": "application/json; odata=verbose" },
                    cache: true
                }).done(function (response) {

                    // we also parse and add some custom properties as an example
                    self._currentUserInfo = $.extend(response.d,
                        {
                            ParsedLoginName: $pnp.core.getUserIdFromLogin(response.d.AccountName)
                        });

                    if (cachingTest) {
                        $pnp.session.add(self._currentUserInfoCacheKey, self._currentUserInfo);
                    }

                    def.resolveWith(ctx || self._currentUserInfo, [self._currentUserInfo]);

                }).fail(function (jqXHR, textStatus, errorThrown) {

                    console.error('[PNP]=>[Fatal Error] Could not load current user data data from /_api/SP.UserProfiles.PeopleManager/GetMyProperties. status: ' + textStatus + ', error: ' + errorThrown);
                    def.rejectWith(ctx || null);
                });
            });
        }

        return this._currentUserInfoPromise.promise();
    }
}
```

## <a name="CachingPatternUsingAsynchronousAndDeferred"></a>Zwischenspeichern von asynchronen und zurückgestellte Muster

Ein weiteres Zwischenspeicherns Muster pnp clientcache.js StorageTest, finden Sie in die die Modernizer StorageTest entnommen wird. Es enthält Funktionen zum Hinzufügen, abrufen, entfernen und GetOrAdd der die zwischengespeicherten Daten zurückgegeben wird, wenn im Cache ist oder die Daten vom Server ab und dem Cache hinzufügen, wenn sie nicht im Cache ist dem Schreiben von sich wiederholendem Code in der aufrufenden Funktion gespeichert. Get wird JSON.parse zum Ablauf zu testen, da Ablaufdatum in lokaler Speicher nicht wird verwendet. _createPersistable speichert das JavaScript-Objekt im Cache lokalen Speicher.

Aus PnP-dev\Samples\Core.JavaScript\Core.JavaScript.CDN\js\pnp-clientcache.js:

```javascript
// adds the client cache capability
caching: {

    // determine if we have local storage once
    enabled: storageTest(),

    add: function (/*string*/ key, /*object*/ value, /*datetime*/ expiration) {

        if (this.enabled) {
            localStorage.setItem(key, this._createPersistable(value, expiration));
        }
    },

    // gets an item from the cache, checking the expiration and removing the object if it is expired
    get: function (/*string*/ key) {

        if (!this.enabled) {
            return null;
        }

        var o = localStorage.getItem(key);

        if (o == null) {
            return o;
        }

        var persistable = JSON.parse(o);

        if (new Date(persistable.expiration) <= new Date()) {

            this.remove(key);
            o = null;

        } else {

            o = persistable.value;
        }

        return o;
    },

    // removes an item from local storage by key
    remove: function (/*string*/ key) {

        if (this.enabled) {
            localStorage.removeItem(key);
        }
    },

    // gets an item from the cache or adds it using the supplied getter function
    getOrAdd: function (/*string*/ key, /*function*/ getter) {

        if (!this.enabled) {
            return getter();
        }

        if (!$.isFunction(getter)) {
            throw 'Function expected for parameter "getter".';
        }

        var o = this.get(key);

        if (o == null) {
            o = getter();
            this.add(key, o);
        }

        return o;
    },

    // creates the persisted object wrapper using the value and the expiration, setting the default expiration if none is applied
    _createPersistable: function (/*object*/ o, /*datetime*/ expiration) {

        if (typeof expiration === 'undefined') {
            expiration = $pnp.core.dateAdd(new Date(), 'minute', $pnp.settings.localStorageDefaultTimeoutMinutes);
        }

        return JSON.stringify({
            value: o,
            expiration: expiration
        });
    }
},
```

Für eine komplexere Verwendung der asynchronen und zurückgestellt können Sie auf das Entwicklerdashboard in pnp clientcache.js verweisen

## <a name="Resources"></a>Ressourcen

### <a name="see-also"></a>Siehe auch
- [JavaScript-Muster und Verwendungsanalyse](http://dev.office.com/blogs/javascript-development-patterns-with-sharepoint)
- [JavaScript – Leistungsaspekte](http://dev.office.com/blogs/javascript-performance-considerations-with-sharepoint)
- [Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint 2013](https://msdn.microsoft.com/EN-US/library/office/jj163201.aspx)
- [Clientseitiges Rendering (JS-Verknüpfung)-Codebeispiele](https://code.msdn.microsoft.com/office/Client-side-rendering-JS-2ed3538a)
- [JavaScript einbetten (Anpassen der Benutzeroberfläche für SharePoint-Website mithilfe von JavaScript)](https://msdn.microsoft.com/EN-US/library/dn913116.aspx)
- [Durchsuchen von Anpassungen für SharePoint](https://msdn.microsoft.com/EN-US/library/mt210901.aspx)
- [SharePoint-Add-in-Anleitung – benutzerdefinierte Feldtyp (mithilfe von Client Side Rendering)](custom-field-type-sharepoint-add-in.md)

### <a name="samples"></a>Beispiele (engl.)

- [Performance.Caching](https://github.com/SharePoint/PnP/tree/master/Samples/Performance.Caching)
- [Core.JavaScript](https://github.com/SharePoint/Pnp/tree/master/Samples/Core.JavaScript)
