# <a name="team-based-development-on-the-sharepoint-framework"></a>Teambasierte Entwicklung mit dem SharePoint Framework

SharePoint Framework ist ein neues Entwicklungsmodell zum Erstellen von SharePoint-Anpassungen. Im Gegensatz zu anderen bisher verfügbaren SharePoint-Entwicklungsmodellen konzentriert sich das SharePoint Framework auf die clientseitige Entwicklung und basiert auf beliebten Open Source-Tools, wie z. B. gulp und webpack. Ein wesentlicher Vorteil dieser Änderung besteht darin, dass Entwickler SharePoint-Anpassungen auf einer beliebigen Plattform erstellen können.

SharePoint Framework ist ein Entwicklungsmodell, und trotz der Unterschiede in der zugrunde liegenden Technologie gelten die gleichen Konzepte bei der Verwendung des Modells zum Erstellen von Lösungen wie auch bei anderen Entwicklungsmodellen, die bisher von SharePoint-Entwicklern verwendet wurden. Entwickler verwenden die Toolkette von SharePoint Framework, um ihre Lösungen zu erstellen und zu testen. Wenn sie fertig sind, übergeben Sie das Lösungspaket, das auf dem SharePoint-Mandanten bereitgestellt werden soll, für weitere Tests und zur Veröffentlichung.

SharePoint Framework besteht aus ein paar unterschiedlichen Paketen. Aus diesen Paketen (jedes in seiner eigenen spezifischen Version) besteht eine Version des SharePoint Framework. Release Candidate (RC0) des SharePoint Framework besteht beispielsweise aus den folgenden Paketversionen:

- @microsoft/sp-client-base v1.0.0
- @microsoft/sp-core-library v1.0.0
- @microsoft/sp-webpart-base v1.0.0
- @microsoft/sp-build-web v1.0.0
- @microsoft/sp-module-interfaces v1.0.0
- @microsoft/sp-webpart-workbench v1.0.0

Damit ein Projekt auf eine bestimmte Version von SharePoint Framework abzielt, muss es auf all die unterschiedlichen Pakete in der korrekten Version verweisen. Beim Erstellen von Gerüsten für neue Projekte fügt der Yeoman-Generator von SharePoint Framework automatisch die erforderlichen Verweise auf das Paket aus der entsprechenden Version von SharePoint Framework hinzu. Wenn das Projekt allerdings auf eine neuere Version von SharePoint Framework aktualisiert wird, müssen Entwickler besonders darauf Acht geben, die Versionsnummern der SharePoint Framework-Pakete korrekt zu aktualisieren.

## <a name="preparing-the-development-environment"></a>Vorbereiten der Entwicklungsumgebung

Um die SharePoint Framework-Lösungen zu erstellen, benötigen Entwickler bestimmte Tools auf den Entwicklungscomputern. Im Vergleich zu anderen SharePoint-Entwicklungsmodellen ist das SharePoint Framework weniger restriktiv und ermöglicht es Entwicklern, die Tools zu verwenden, mit denen sie am produktivsten arbeiten können; sie können sogar das Betriebssystem auswählen.

Es gibt ein paar Möglichkeiten, wie Entwickler ihre Entwicklungsumgebung konfigurieren können. Jede Umgebung hat andere Vorteile, und es ist wichtig, dass Entwicklerteams die unterschiedlichen Optionen kennen.

### <a name="sharepoint-framework-toolchain"></a>SharePoint Framework-Toolkette

Zum Erstellen von SharePoint Framework-Lösungen müssen Entwickler eine bestimmte Reihe von Tools verwenden. In der folgenden Liste sind die grundlegenden Tools aufgeführt, die in allen SharePoint Framework-Entwicklungsumgebungen erforderlich sind.

#### <a name="nodejs"></a>Node.js

Für SharePoint Framework muss Node.js auf dem Entwicklercomputer installiert sein. Node.js wird als Laufzeit für Entwurfszeittools verwendet, die zum Erstellen und Verpacken des Projekts verwendet werden. Node.js wird global auf dem Entwicklercomputer installiert, und es gibt Lösungen, die bei Bedarf das parallele Ausführen mehrerer Versionen von Node.js unterstützen.

> Weitere Informationen zum Installieren von Node.js und zu den unterstützten Versionen stehen unter [https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) zur Verfügung.

#### <a name="npm"></a>npm

npm entspricht NuGet in .NET Projekten: Es ermöglicht Entwicklern, Pakete zur Verwendung in SharePoint Framework-Projekten zu erwerben und zu installieren. Npm wird auch zum Installieren der SharePoint Framework-Toolkette verwendet. Entwickler verwenden in der Regel die neueste Version von npm und installieren es global auf ihrem Computer. npm selbst ist ein Node.js-Paket, wenn Sie also mehrere Versionen von Node.js parallel ausführen, installiert jedes Paket seine eigene Version von npm.

#### <a name="gulp"></a>gulp

gulp entspricht MSBuild in .NET-Projekten und ist für das Ausführen von Aufgaben wie das Erstellen oder Verpacken eines SharePoint Framework-Projekts verantwortlich. gulp wird als Node.js-Paket verteilt und in der Regel global mithilfe von npm installiert.

#### <a name="yeoman-and-sharepoint-framework-yeoman-generator"></a>Yeoman und der Yeoman-Generator von SharePoint Framework

Mithilfe von Yeoman und dem Yeoman-Generator von SharePoint Framework erstellen Entwickler neue SharePoint Framework-Projekte. Sowohl Yeoman als euch seine Generatoren werden als Node.js-Pakete verteilt und werden in der Regel mithilfe von npm als globale Pakete installiert. Der Vorteil einer globalen Installation besteht darin, dass Entwickler Yeoman und die Generatoren einmal installieren und diese dann verwenden können, um ganz einfach neue Projekte zu erstellen.

Der Yeoman-Generator von SharePoint Framework ist an eine bestimmte Version von SharePoint Framework gebunden. Projekte, deren Gerüste mit dem Generator erstellt wurden, verweisen auf die bestimmten Versionen der SharePoint Framework-Pakete, und die generierten Webparts verweisen auf die bestimmten Teile des Frameworks. Der Yeoman-Generator von SharePoint Framework wird zum Erstellen neuer Projekte, aber auch zum Hinzufügen von Webparts zu vorhandenen Projekten verwendet. Wenn Sie diesen global installieren und ein neues Webpart zu einem vorhandenen Projekt hinzufügen müssten, das in der Vergangenheit erstellt wurde, ist das neu erstellte Webpart möglicherweise nicht mit dem Rest des Projekts konsistent, was möglicherweise sogar zu Buildfehlern führen könnte. Es gibt mehrere Möglichkeiten, um diese Einschränkung zu umgehen, die später in diesem Artikel beschrieben werden.

#### <a name="typescript"></a>TypeScript

SharePoint Framework verwendet TypeScript, um Entwicklern zu mehr Produktivität zu verhelfen, indem sie besseren Code schreiben und Fehler bereits während der Entwicklung entdecken. SharePoint Framework wird mit seiner eigenen Version von TypeScript ausgeliefert, die im Buildprozess verwendet wird. Entwickler müssen TypeScript daher nicht separat installieren.

### <a name="building-a-sharepoint-framework-development-environment"></a>Erstellen einer SharePoint Framework-Entwicklungsumgebung

Bisher verwendeten SharePoint-Entwickler normalerweise virtuelle Computer als Entwicklungsumgebungen. Mit virtuellen Computern konnte sichergestellt werden, dass die erstellte Lösung in der von der jeweiligen Organisation verwendeten Umgebung funktioniert. Auf den virtuellen Computern installierten Entwickler SharePoint und patchten es auf die gleiche Ebene wie die Produktionsumgebung, die von der jeweiligen Organisation verwendet wurde. In einigen Fällen installierten sie zusätzliche Software, die so gut wie möglich mit der Zielumgebung übereinstimmen sollte, auf der die Lösung ausgeführt werden sollte. Mit diesem Ansatz konnten Entwickler frühzeitig Fehler ausfindig machen, die durch die unterschiedlichen Umgebungen entstanden. Dies ging allerdings zulasten der Komplexität und der Verwaltung der unterschiedlichen Umgebungen.

Der Umstieg auf die Entwicklung von Lösungen für die Cloud löste diese Probleme nur teilweise. Entwickler mussten zwar keine SharePoint-Farm mehr auf ihren Entwicklungscomputern ausführen, sie mussten aber berücksichtigen, wie die Lösung gehostet werden und wie diese mit SharePoint Online kommunizieren würde.

Da sich SharePoint Framework auf die clientseitige Entwicklung konzentriert, muss SharePoint nicht mehr auf den Entwicklungscomputern installiert werden. Mit einigen wenigen Ausnahmen sind alle Abhängigkeiten vom Framework und anderen Paketen im Projekt angegeben und im Projektordner enthalten. Da das SharePoint Framework seinen Ursprung in der Cloud hat und sich ständig weiterentwickelt, müssen Entwickler sicherstellen, dass sie die korrekte Version der Toolkette verwendet, die ihrem SharePoint Framework-Projekt entspricht.

#### <a name="shared-or-a-personal-development-environment"></a>Freigegebene oder persönliche Entwicklungsumgebung

SharePoint-Anpassungen reichen von einfachen Skripts, die direkt zu der Seite hinzugefügt werden, bis hin zu fortschrittlichen Lösungen, die als Lösungspakete bereitgestellt werden. SharePoint Framework ist ein Entwicklungsmodell, das auf das strukturierte und wiederholbare Entwicklungsmodell von SharePoint-Anpassungen abzielt. Beim Erstellen von SharePoint Framework-Lösungen verwendet jeder Entwickler im Team seine eigene Entwicklungsumgebung und gibt den Quellcode des Projekts für andere Entwickler im Team über ein Quellcodeverwaltungssystem frei. Auf diese Weise können Entwickler gleichzeitig am gleichen Projekt arbeiten und ihre Lösung testen, ohne sich gegenseitig die Produktivität zu beeinträchtigen.

Bisher war es für viele Organisationen schwierig rechtzufertigen, dass SharePoint-Entwicklern sehr leistungsstarke Entwicklungscomputer zur Verfügung gestellt werden, und in manchen Fällen mussten sich mehrere Entwickler den gleichen Computer teilen, was zu einer niedrigeren Produktivität führte. Mit SharePoint Framework können Entwickler Computer nach Marktstandard zum Erstellen von SharePoint-Anpassungen verwenden.

#### <a name="developing-on-the-host"></a>Entwickeln auf dem Host

Die einfachste Option zum Einrichten einer Entwicklungsumgebung für SharePoint Framework-Projekte besteht wahrscheinlich darin, alle Tools direkt auf dem Hostcomputer zu installieren. Wenn Ihr Team nur an SharePoint Framework-Projekten arbeitet, können sie Node.js auf ihren Computern installieren. Wenn auch an anderen Node.js-Projekten gearbeitet wird, können sie Drittanbieterlösungen, z. B. [nvm](https://github.com/creationix/nvm) verwenden, um mehrere Versionen von Node.js-parallel auszuführen.

Entsprechend den Tools, die für die SharePoint Framework-Toolkette erforderlich sind, würden Entwickler Yeoman und den Yeoman-Generator von SharePoint Framework installieren. In der Regel werden beide Tools global installiert. Angesichts der Tatsache, dass der Yeoman-Generator des SharePoint Framework an eine bestimmte Version  von SharePoint Framework gebunden ist und Entwickler möglicherweise mit Projekten arbeiten müssen, die unter Verwendung einer anderen Version erstellt wurden, müsste jedoch die Version des Generators deinstalliert und installiert werden, die für das jeweilige Projekt spezifisch ist, an dem gerade gearbeitet wird. Ein praktikablerer Ansatz wäre, sowohl Yeoman als auch den Yeoman-Generator des SharePoint Framework lokal im angegebenen Projekt zu installieren. Dies bedeutet zwar einen Mehraufwand, hilft Entwicklern aber sicherzustellen, dass neue Elemente, die dem Projekt möglicherweise in der Zukunft hinzugefügt werden müssen, mit dem Rest des Projekts kompatibel sind.

Der große Vorteil der Entwicklung auf dem Host besteht darin, dass Entwickler ihren Computer einmal mit den gewünschten Einstellungen konfigurieren können und diese dann in allen Projekten verwenden können. Da die Software auf dem Host ausgeführt wird, hat diese direkten Zugriff auf die CPU, den Arbeitsspeicher und Datenträger-E/A ohne Virtualisierungsebene, was zu einer besseren Leistung führt als das Ausführen derselben Software in virtualisierter Form.

#### <a name="developing-in-a-virtual-machine"></a>Entwickeln auf einem virtuellen Computer

Bisher bestand der am häufigsten verwendete Ansatz unter SharePoint-Entwicklern darin, virtuelle Computer als primäre Entwicklungsumgebung zum Erstellen von SharePoint-Lösungen zu verwenden. Mithilfe von virtuellen Computern konnten Entwickler die unterschiedlichen Anforderungen für die unterschiedlichen Projekten berücksichtigen.

Beim Erstellen von Lösungen im SharePoint Framework können Organisationen von denselben Vorteilen wie bisher beim Erstelle von SharePoint-Lösungen profitieren. Mithilfe von virtuellen Computern kann die Entwicklungssoftware vom Hostbetriebssystem isoliert werden, was eine häufige Anforderung, insbesondere in großen Organisationen, darstellt. Durch Erstellen eines separaten virtuellen Computers für jedes Projekt können Entwickler sicherstellen, dass die verwendete Toolkette mit dem Projekt kompatibel ist, auch dann, wenn das Projekt in der Zukunft wieder aufgegriffen werden muss.

Die Verwendung von virtuellen Computern hat auch Nachteile. Virtuelle Computer sind groß, und Entwickler müssen für produktives Arbeiten leistungsstarke Computer verwenden. Außerdem müssen Entwickler über längere Zeiträume hinweg das Betriebssystem auf dem aktuellen Stand halten und sicherstellen, dass alle erforderlichen Sicherheitsupdates ausgeführt werden. Da Entwickler auf einem virtuellen Computer arbeiten, müssen sie entweder zu Beginn eines neuen Projekts etwas Zeit aufwenden, um den virtuellen Standardcomputer mit ihren gewünschten Einstellungen zu konfigurieren, oder sie müssen zulasten ihrer Produktivität die standardmäßige Einrichtung akzeptieren. Da auf virtuellen Computern ein vollständiges Betriebssystem mit allen Komponenten ausgeführt wird, ist es wesentlich schwieriger sicherzustellen, dass alle virtuellen Computer, die von allen Entwicklern im Team verwendet werden, konsistent sind. Verglichen mit anderen Typen von Entwicklungsumgebungen ist die Verwendung von virtuellen Computern zum Erstellen von SharePoint Framework-Lösungen kostspielig und zeitaufwändig.

#### <a name="developing-using-docker"></a>Entwickeln mit Docker

Ein interessanter Kompromiss zwischen der Entwicklung auf dem Host und auf einem virtuellen Computer ist die Verwendung von Docker. Docker ist eine Softwarevirtualisierungstechnologie, die virtuellen Computern ähnlich ist, aber ein paar wesentliche Unterschiede aufweist. Die wichtigsten Vorteile der Verwendung von Docker-Images im Vergleich zu virtuellen Computern bestehen darin, dass Docker-Images einfacher zu erstellen, zu verwalten und zu verteilen sind, sie sind leichter (ein paar Hundert MB im Vergleich zu Tausenden von GB Festplattenspeicher, der für virtuelle Computer erforderlich ist), und Entwickler können die Tools und Einstellungen verwenden, die sie bereits auf dem Hostcomputer installiert und konfiguriert haben.

Ähnlich wie bei virtuellen Computern werden Docker-Container auf einer virtualisierten Instanz eines Betriebssystems (meistens basierend auf Linux) ausgeführt. Die gesamte in dem Image installierte Software, die zum Erstellen des Containers verwendet wird, wird isoliert innerhalb dieses Containers ausgeführt und hat nur Zugriff auf den Teil des Hostdateisystems, der explizit für den Container freigegeben ist. Da alle Änderungen an dem Dateisystem innerhalb eines Docker-Containers verworfen werden, sobald der Container geschlossen, geben Entwickler Ordner von ihrem Host frei, in denen der Quellcode gespeichert wird.

Lesen Sie weitere Informationen [zur Verwendung von Docker zum Erstellen von SharePoint Framework-Lösungen](https://www.spcaf.com/blog/try-sharepoint-framework-without-installing/).

## <a name="development-workflow-in-sharepoint-framework-projects"></a>Entwicklungsworkflow in SharePoint Framework-Projekten

SharePoint Framework basiert auf einer Open Source-Toolkette und folgt dem allgemeinen Entwicklungsworkflow, den es auch in anderen Projekten gibt, die auf dem gleichen Stapel basieren. Nachfolgend finden Sie eine Beschreibung dieses Workflows in einem typischen SharePoint Framework-Projekt.

### <a name="create-new-sharepoint-framework-project"></a>Erstellen eines neuen SharePoint Framework-Projekts

Beim Erstellen von SharePoint-Anpassungen mithilfe von SharePoint Framework besteht der erste Schritt darin, ein Gerüst für das neue SharePoint Framework-Projekt zu erstellen. Dies erfolgt über den Yeoman-Generator von SharePoint Framework. In dem Generator werden Sie aufgefordert, ein paar Fragen bezügliches des Namens des Projekts oder des Speicherorts zu beantworten. Sie können auch das erste Webpart erstellen. Beachten Sie, dass das Framework, das Sie zum Erstellen des ersten Webparts auswählen, automatisch für alle anderen Webparts verwendet wird, die Sie dem Projekt später hinzufügen. Sie können das Framework zwar manuell ändern, es wird jedoch empfohlen, pro SharePoint Framework-Projekt ein einzelnes Framework zu verwenden.

### <a name="lock-dependencies-version"></a>Sperren der Abhängigkeitenversion

Ein neues SharePoint Framework-Projekt, für das mit dem Yeoman-Generator von SharePoint Framework ein Gerüst erstellt wurde, weist Abhängigkeiten von den SharePoint Framework-Paketen sowie von anderen Paketen auf, die für das korrekte Ausführen erforderlich sind. Beim Erstellen von Webparts möchten Sie vielleicht zusätzliche Abhängigkeiten, wie z. B. Angular oder jQuery, einschließen. In SharePoint Framework-Projekten werden Abhängigkeiten mithilfe von npm installiert. Jede Abhängigkeit ist ein Node.js-Paket mit einer bestimmten Version. Auf Abhängigkeiten wird standardmäßig mithilfe eines Versionsbereichs verwiesen, wodurch Entwickler ihre Abhängigkeiten leichter auf dem aktuellen Stand halten können. Eine Konsequenz dieses Ansatzes besteht darin, dass das Wiederherstellen von Abhängigkeiten für dasselbe Projekt zu zwei Zeitpunkten möglicherweise unterschiedliche Ergebnisse zurückgibt, was dazu führen könnte, dass das Projekt beschädigt wird.

Eine allgemeine Lösung für Projekte, die auf der Open Source-Toolkette basieren, mit der das Risiko minimiert werden kann, dass sich Abhängigkeiten während des Projekts ändern, besteht darin, die Version aller Abhängigkeiten zu sperren. Beim Hinzufügen einer Abhängigkeit zum Projekt können Entwickler die Abhängigkeit mit einer bestimmten Version und nicht mit einem Versionsbereich installieren, indem sie den `npm install`-Befehl mit dem `--save-exact`-Argument aufrufen. Dies hat jedoch keine Auswirkungen auf die untergeordneten Abhängigkeiten des jeweiligen Projekts. Um die Version aller Abhängigkeiten und deren untergeordnete Elemente im Projekt effektiv zu sperren, können Entwickler den `npm shrinkwrap`-Befehl verwenden. Sobald dieser ausgeführt wird, wird eine Liste aller Abhängigkeiten und ihrer Versionen zum Zeitpunkt der Ausführung erstellt und in der Datei **npm-shrinkwrap.json** aufgezeichnet, die in die Quellcodeverwaltung aufgenommen werden sollte. Beim Wiederherstellen von Abhängigkeiten verwendet npm die genauen Versionen aus dieser Datei anstelle der neuesten Version, sodass der jeweilige Versionsbereich erfüllt wird.

> Hinweis: Wenn Sie im Ordner **node_modules** Pakete installiert haben, die nicht als Abhängigkeiten in der Datei **package.json** aufgeführt sind oder keine Abhängigkeit eines der Pakete darstellen, wird beim Erstellen der Datei **npm-shrinkwrap.json** mit großer Wahrscheinlichkeit ein Fehler angezeigt. In diesem Fall können Sie entweder die Pakete sehen, die den Fehler verursachen und diese der Datei **package.json** hinzufügen oder sie aus dem Ordner **node_modules** entfernen, oder Sie löschen den Ordner **node_modules** komplett, stellen alle Abhängigkeiten wieder her, und generieren dann die shrinkwrap-Datei.

### <a name="add-the-project-to-source-control"></a>Hinzufügen des Projekts zur Quellcodeverwaltung

Damit das restliche Team an demselben Projekt arbeiten kann, fügen Sie es dem Quellcodeverwaltungssystem hinzu, das Ihr Team verwendet. Die genauen Schritte variieren in Abhängigkeit von dem System, das Ihr Team verwendet.

Gerüste für SharePoint Framework-Projekte werden mit der Datei **.gitignore** erstellt, die beschreibt, welche Dateien von der Quellcodeverwaltung ausgeschlossen werden sollten. Wenn Ihr Team ein anderes Quellcodeverwaltungssystem als Git verwendet (z. B. Visual Studio Team System mit Team Foundation System-Repositorys), sollten Sie sicherstellen, dass Sie die korrekten Dateien aus dem Projekt in die Quellcodeverwaltung einschließen. Durch Ausschließen der Abhängigkeiten und automatisch generierten Dateien während des Buildprozesses können Sie auch sicherstellen, dass Ihr Team effizient arbeitet.

Insbesondere den Ordner **node_modules** sollten Entwickler nicht in die Quellcodeverwaltung einschließen. Dieser Ordner enthält Pakete, von denen das Paket abhängig ist und die automatisch beim Wiederherstellen von Abhängigkeiten mithilfe des `npm install`-Befehl installiert werden. Einige Pakete werden zu Binärdateien kompiliert, und der Kompilierungsprozess ist vom Betriebssystem abhängig. Wenn das Team auf unterschiedlichen Betriebssystemen arbeitet, kann durch Einschließen des Ordners **node_modules** in die Quellcodeverwaltung der Buildvorgang für einige Teammitglieder unterbrochen werden.

### <a name="get-the-project-from-source-control"></a>Abrufen des Projekts aus der Quellcodeverwaltung

Wenn Sie das Projekt zum ersten Mal aus der Quellcodeverwaltung abrufen, rufen Sie den Quellcode des Projekts, aber keine SharePoint Framework-Bibliotheken ab, die zum Erstellen des Projekts erforderlich sind. Ähnlich wie beim Arbeiten mit .NET-Projekten und der Verwendung von NuGet-Paketen, müssen Sie zuerst Abhängigkeiten wiederherstellen. In SharePoint Framework-Projekten erfolgt dies, ähnlich wie bei allen anderen Projekten, die auf Node.js basieren, indem Sie `npm install` in der Befehlszeile ausführen. npm verwendet die Informationen aus der Datei **package.json** in Kombination mit den Informationen aus der Datei **npm-shrinkwrap.json** und installiert alle Pakete.

> Hinweis: In der Regel ist für das Wiederherstellen der Abhängigkeiten mithilfe des `npm install`-Befehls eine Verbindung zum Internet erforderlich, da Pakete von _registry.npmjs.org_ heruntergeladen werden. Wenn Probleme mit der Netzwerkkonnektivität auftreten oder die npmjs-Registrierung nicht verfügbar ist, schlägt der Build fehl. Es gibt mehrere Möglichkeiten, um diese Einschränkung zu umgehen. Eine besteht darin, [shrinkpack](https://github.com/JamieMason/shrinkpack) zu verwenden, um Tarballs aller Abhängigkeiten herunterzuladen und diese in der Quellcodeverwaltung zu speichern. Shrinkpack aktualisiert automatisch die Datei „npm-shrinkwrap.json“, um die lokalen Tarballs zu verwenden, sodass eine Offlineinstallation der Projektabhängigkeiten möglich ist.

Einige der Pakete werden während des Installationsvorgangs in Binärdateien kompiliert. Dieser Kompilierungsvorgang ist von der Architektur und dem Betriebssystem abhängig. Wenn Sie Abhängigkeiten beispielsweise in einem Docker-Container wiederherstellen würden, in dem Linux ausgeführt wird, und Sie würden dann versuchen, das Projekt in Ihrem Windows-host zu erstellen, so würde eine Fehlermeldung angezeigt, die Sie auf den Konflikt in dem Umgebungstyp hinweist, der zum Erstellen und Ausführen der Binärdateien verwendet wurde.

Während der Entwicklung der Lösung durch das Team werden möglicherweise neue oder aktualisierte Abhängigkeiten zum Projekt hinzugefügt. Wenn sich die Datei **package.json** geändert hat, seit Sie das Projekt zuletzt aus der Quellcodeverwaltung abgerufen haben, müssen Sie `npm install` in der Befehlszeile ausführen, um die fehlenden Abhängigkeiten zu installieren. Wenn Sie nicht sicher sind, ob sich die Datei **package.json** geändert hat, können Sie `npm install` in der Befehlszeile, um sicherzustellen, dass Sie über die neuesten Abhängigkeiten verfügen, ohne das Projekt zu beeinträchtigen.

### <a name="add-packages-to-your-project"></a>Hinzufügen von Paketen zum Projekt

Sie können produktiver arbeiten, wenn Sie vorhandene Pakete verwenden, um bestimmte Aufgaben zu erledigen. npmjs.com ist eine öffentliche Registrierung von Paketen, die Sie in Ihrem Projekt verwenden können.

> Hinweis: Da es keinen formalen Überprüfungsprozess gibt, bevor ein Paket in „npmjs.com“ veröffentlicht wird, sollten Sie besonders sorgfältig prüfen, ob Sie das bestimmte Paket sowohl bezüglich seiner Inhalte als auch der Lizenzen verwenden können.

Um ein Paket zu Ihrem SharePoint Framework-Projekt hinzuzufügen, führen Sie den Befehl `npm install <package> --save` oder `npm install <package> --save-dev` in der Befehlszeile aus, z. B. `npm install angular --save`. Durch Verwendung des Arguments `--save` oder `--save-dev` wird sichergestellt, dass das Paket der Datei **package.json** hinzugefügt wird und dass andere Entwickler in Ihrem Team dieses beim Wiederherstellen von Abhängigkeiten auch erhalten. Ohne dieses Argument tritt beim Erstellen des Projekts auf einem anderen Computer als Ihrem eigenen ein Fehler auf. Beim Hinzufügen von Paketen, für Ihre Lösung oder Laufzeit erforderlich sind, z. B. Angular oder jQuery, sollten Sie das `--save`-Argument verwenden. Pakete, die für den Buildvorgang erforderlich sind, z. B. zusätzliche gulp-Aufgaben, sollten mit dem `--save-dev`-Argument installiert werden.

Wenn Sie beim Installieren eines Pakets keine Version angeben, installiert npm die letzte in der Paketregistrierung verfügbare Version (standardmäßig „npmjs.com“). Dies ist in der Regel die gewünschte Version. Ein spezieller Fall, in dem Sie die Version des Pakets angeben müssen, besteht dann, wenn Sie **npm-shrinkwrap.json** verwenden und das vorhandene Paket auf eine neue Version aktualisieren möchten. npm installiert standardmäßig die Version, die in der Datei **npm-shrinkwrap.json** aufgeführt ist. Durch Angeben der Versionsnummer im `npm install`-Befehl, z. B. `npm install angular@1.5.9 --save` wird dieses Paket installiert, und die Versionsnummer in der Datei **npm-shrinkwrap.json** wird aktualisiert.

## <a name="working-with-internal-packages"></a>Arbeiten mit internen Paketen

Da Ihr Team clientseitige Lösungen entwickelt, erstellen Sie mit großer Wahrscheinlichkeit allgemeine Codebibliotheken, die Sie im gesamten Projekt wiederverwenden möchten. In vielen Fällen enthalten solche Bibliotheken neben den für die Produktion bereitgestellten Bundles proprietären Code, der nicht außerhalb der Organisation freigegeben wird. Beim Arbeiten mit SharePoint Framework-Projekten gibt es eine Reihe von Möglichkeiten, wie Ihr Team die internen Bibliotheken in seinen Projekten nutzen kann.

### <a name="hosting-private-package-registry"></a>Hosten einer privaten Paketregistrierung

Bisher haben viele Organisationen, die .NET-Lösungen erstellen, private NuGet-Repositorys gehostet, um von dem NuGet-Paketverwaltungssystem für interne Pakete zu profitieren. Da SharePoint Framework npm für die Paketverwaltung verwendet, könnten Organisationen in ähnlicher Weise eine private Registrierung für ihre internen Pakete verwenden. Intern entwickelte Pakete würden in der privaten Registrierung veröffentlicht und könnten in allen Projekten innerhalb der Organisation verwendet werden.

Bei der Verwendung privater Paketregistrierungen können Organisationen zwischen unterschiedlichen Angeboten wählen, die in der Cloud gehostet werden, oder sie können eine eigene Registrierung in ihrer eigenen Infrastruktur hosten.

Mit einer privaten Paketregistrierung können Organisationen gemeinsamen Code zentral über die unterschiedlichen Projekte hinweg verwalten. Durch Definieren eines separaten Governance-Plans zum Beisteuern von Änderungen an der freigegebenen Codebasis können Organisationen sicherstellen, dass die Codebibliothek eine hohe Qualität aufweist und allen Entwicklern Vorteile liefert, anstatt Projekte zu verlangsamen.

[npm Enterprise](https://www.npmjs.com/enterprise) ist eine beliebte private Registrierung, die in der Cloud gehostet wird. Organisationen, die daran interessiert sind, ihre Registrierung selbst zu hosten, können aus einer Reihe von Open Source-Implementierungen wie [Sinopia](https://github.com/rlidwka/sinopia) oder Abspaltungen wie [Verdaccio](https://github.com/verdaccio/verdaccio) oder [Nexus](https://www.sonatype.com/nexus-repository-oss) wählen.

> Hinweis: Unterschiedliche Module zum Hosten privater Paketregistrierungen befinden sich in unterschiedlichen Entwicklungsstufen. Sie sollten sorgfältig prüfen, dass das jeweilige Modul Ihren Anforderungen in Hinblick auf Funktionalität, Lizenz und Support entspricht.

Zur Vereinfachung der Installation und Verwaltung einer privaten Paketregistierung bietet die meisten Module einsatzbereite Docker-Images. 

### <a name="linking-packages-using-npm-link"></a>Verknüpfen von Paketen mithilfe der npm-Verknüpfung

Eine Alternative zur Verwendung einer privaten Registrierung ist das Verknüpfen von Paketen. Hierfür muss zwar keine Registrierung eingerichtet werden, auf allen Entwicklercomputern und dem Buildserver ist aber eine sorgfältige Koordination erforderlich.

Zunächst muss jeder Entwickler im Team eine Kopie des freigegebenen Pakets auf seinem Entwicklungscomputer abrufen. In der Befehlszeile muss das Arbeitsverzeichnis auf das des freigegebenen Pakets geändert werden. Anschließend muss der`npm link`-Befehl ausgeführt werden. Dieser Befehl registriert das jeweilige Paket als globales Paket auf diesem bestimmten Entwicklungscomputer. Als Nächstes müssen Entwickler das Arbeitsverzeichnis in das Verzeichnis des Projekts ändern, in dem Sie das freigegebene Paket verwenden möchten. Das Paket kann dann genau so wie jedes andere Paket durch Ausführen des `npm install <shared_package> --save`-Befehls in der Befehlszeile installiert werden. Da das freigegebene Paket global installiert wird, verwendet npm diese Version als Quelle, aus der das Paket installiert wird. Aus Sicht des Projekts wird das Paket zu diesem Zeitpunkt genau so wie jedes andere öffentliche Paket installiert, und Entwickler können auswählen, wie das Paket mit dem Projekt gebündelt werden soll.

Das Verknüpfen des Pakets muss auf allen Entwicklungscomputern und auch auf dem Buildserver ausgeführt werden. Wenn das freigegebene Paket nicht über den `npm link`-Befehl verknüpft wird, treten beim Wiederherstellen der Projektabhängigkeiten Fehler auf und der Buildvorgang wird unterbrochen.

Das Verweisen auf verknüpfte Paketen ist insbesondere frühzeitig im Projekt hilfreich, wenn Sie das freigegebene Paket und das Projekt gleichzeitig entwickeln. Dank der Verknüpfung müssen Sie die neue Version des Pakets nicht in der Registrierung veröffentlichen, um den neuesten Code in Ihrem Projekt zu verwenden. Ein Risiko, das Sie beachten sollten, besteht dann, wenn Entwickler auf eine Version der freigegebenen Bibliothek verweisen, die sie lokal geändert und nicht in die Quellcodeverwaltung eingecheckt haben. Dadurch würde der Buildvorgang für das restliche Team unterbrochen.

### <a name="combining-private-package-registry-and-linking-packages"></a>Kombinieren der privaten Paketregistrierung und der Verknüpfung von Paketen

Das Verknüpfen von Paketen kann mit einer privaten Registrierung kombiniert werden. Sie könnten beispielsweise so arbeiten, dass Entwickler auf ein verknüpftes Paket verweisen, und der Buildserver ruft die freigegebene Bibliothek aus einer privaten Registrierung ab. Aus Projektperspektive ändert nichts: Der Paketverweis in der Datei **package.json** kann sowohl von einem verknüpften Paket als auch von einer privaten Registrierung gelöst werden. Das einzige, was Ihr Team beachten muss, ist, dass die letzten Änderungen an der freigegebenen Bibliothek in der privaten Registrierung veröffentlicht werden müssen, bevor der Build ausgeführt wird.

Wenn der Code der freigegebenen Bibliothek im Laufe der Zeit stabiler wird und weniger Änderungen vorgenommen werden müssen, um die Anforderungen von bestimmten Projekten zu erfüllen, können Entwickler einfach nur auf das veröffentlichte Paket aus der privaten Registrierung verweisen, anstatt es zu ändern.

## <a name="ensuring-code-consistency-and-quality"></a>Sicherstellen von Codekonsistenz und -qualität

Für Softwareentwicklungsteams ist das Aufrechterhalten der Konsistenz und hohen Qualität ihrer Projekte häufig ein Problem. Unterschiedliche Entwickler haben einen unterschiedlichen Programmierungsstil und andere Vorlieben. In jedem Team gibt es fachlich erfahrenere Mitglieder und auch Entwickler, die in der speziellen Domäne weniger erfahren sind. Außerdem haben viele Organisationen oder Sparten spezifische Vorschriften, die die Software erfüllen muss. All diese Herausforderungen erschweren Entwicklern das Leben. Insbesondere dann, wenn der Fertigstellungstermin näher rückt, neigen Entwickler dazu, ihre Arbeit zulasten der Qualität fertigzustellen, was langfristig negativere Folgen hat als Nichteinhalten des Termins hat.

### <a name="choose-javascript-library-for-your-team-and-use-coding-standards"></a>Auswählen der JavaScript-Bibliothek für Ihr Team und Verwenden von Codestandards

Wenn Ihr Team bisher SharePoint-Anpassungen erstellt hat, verfügen Sie aller Wahrscheinlichkeit nach über Codierungsstandards, in denen beschrieben wird, wie Anpassungen erstellt und welche Tools und Bibliotheken in Ihren Projekten verwendet werden. Mithilfe von Codierungsstandards können Sie die persönlichen Vorlieben der einzelnen Entwickler aus dem Code beseitigen, sodass es für die anderen Teammitglieder viel leichter ist, die Arbeit daran fortzusetzen. In Ihren Codierungsstandards spiegeln sich auch die Erfahrungen Ihres Teams wider, die es im Laufe der Jahre gesammelt hat, sodass Sie Anpassungen effizienter und mit besserer Qualität erstellen können.

Im Gegensatz zu anderen SharePoint-Anpassungsmodellen, die bisher verfügbar sind, konzentriert sich SharePoint Framework auf die clientseitige Entwicklung. Die Verwendung von TypeScript ist zwar nicht zwingend erforderlich, wird aber für SharePoint Framework empfohlen, damit Entwickler besseren Code schreiben und Inkonsistenzen bereits im Buildprozess abfangen können. Es gibt auch zahlreiche clientseitige Bibliotheken, die hierfür zur Verfügung stehen. Wenn Ihr Team bisher an clientseitigen Entwicklungen gearbeitet hat, haben Sie vielleicht schon eine bestimmte Bibliothek gefunden, die Ihnen zusagt. Wenn nicht, wäre es von Vorteil, wenn Sie sich einige der beliebtesten Bibliotheken näher ansehen und eine für Ihr Team oder vorzugsweise für die gesamte Organisation auswählen.

Wenn Sie in allen Projekten dieselbe Bibliothek verwenden, können Sie neue Teammitglieder leichter einbinden und Teammitglieder zwischen Projekten austauschen. Wenn Sie weitere Erfahrungen mit der clientseitigen Entwicklung sammeln, kann Ihre Organisation davon bei allen Projekten profitieren. Indem Sie Ihre Projekte in der gesamten Organisation standardisieren, wird auch die Zeit bis zur Bereitstellung verkürzt, und die Kosten für die Wartung Ihrer Projekte verringern sich. Jeden Tag werden im Internet neue Bibliotheken veröffentlicht. Wenn Sie ständig zu den neuesten Bibliotheken wechseln, arbeiten Sie ineffizient und liefern Lösungen mit geringer Qualität.

Durch eine Standardisierung, welche Bibliotheken in Ihrer Organisation verwendet werden, optimieren Sie auch die Leistung Ihrer Lösungen. Da die gleiche Bibliothek in der gesamten Organisation verwendet wird, müssen Benutzer sie nur einmal herunterladen, wodurch die Ladezeit der Lösungen wesentlich verringert und folglich die Benutzerfreundlichkeit stark verbessert wird.

Indem Sie eine der beliebtesten Bibliotheken auswählen, können Sie von dem Wissen und der Erfahrung anderer Entwickler profitieren, die diese Bibliothek bereits seit längerer Zeit verwenden und einige der Probleme gelöst haben, mit denen auch Sie konfrontiert würden. Für die am häufigsten verwendeten Bibliotheken gibt es auch Codierungsstandards, die Ihr Team übernehmen kann. Indem Sie vorhandene Marktstandards für die jeweilige Bibliothek verwenden, ist es für Ihre Organisation leichter, Ihr Team zu vergrößern, indem Entwickler eingestellt und diesen schneller zu produktiver Arbeit verholfen wird.

Für das Erstellen von Erstanbieterlösungen im SharePoint Framework hat sich Microsoft beispielsweise für React entschieden. Viele andere Teams bei Microsoft, wie etwa OneDrive oder Delve, verwenden React in ihren Projekten. Dies bedeutet nicht, dass Sie in allen SharePoint Framework-Projekten auch React verwenden sollen, es zeigt jedoch, wie wichtig es ist, eine clientseitige Bibliothek auszuwählen, die für Ihre Organisation funktioniert. Wenn Ihr Team z. B. Erfahrung mit Angular oder Knockout hat, besteht kein Grund, warum Sie nicht von diesen Erfahrungen profitieren und beim Erstellen von SharePoint Framework-Lösungen produktiv arbeiten sollten.

### <a name="enforce-coding-standards-and-policies-throughout-the-whole-lifecycle-of-your-solution"></a>Erzwingen von Codierungsstandards und Richtlinien über den gesamten Lebenszyklus Ihrer Lösung

Die Verwendung von Codierungsstandard liefert Ihnen klare Vorteile, das bloße Vorhandensein von Codierungsstandard bedeutet jedoch nicht, dass diese aktiv während des gesamten Entwicklungs- und Testprozesses einer SharePoint-Anpassung verwendet werden. Je länger Entwickler warten und je schwierigerer es für Ihr Team ist zu überprüfen, ob die Lösung den Codierungsstandards des Teams sowie Organisationsrichtlinien entspricht, desto kostspieliger wird es, Fehler, die in dem Projekt gefunden werden, zu korrigieren. Nachfolgend finden Sie ein paar Möglichkeiten, die Ihr Team im Rahmen des Entwicklungsprozesses verwenden sollte, um den Governance-Plan für die SharePoint-Lösung zu erzwingen.

#### <a name="linting"></a>Linting

Als „Linting“ wird der Prozess der Überprüfung bezeichnet, dass der Code bestimmten Regeln entspricht. Standardmäßig basieren SharePoint Framework-Projekte auf TypeScript. In jedem Build-TSLint - dem Linter für TypeScript - wird das Projekt anhand der vordefinierten Regeln analysiert, und Inkonsistenzen werden gemeldet. Entwickler können auswählen, welche Regeln aktiviert werden sollen, und sie können bei Bedarf eigene Regeln erstellen, die die Richtlinien des Teams oder der Organisation widerspiegeln.

Entwickler können Linting nicht nur verwenden, um die Inhalte von TypeScript-Dateien zu überprüfen. Es gibt auch Linter für die meisten beliebten Sprachen wie CSS, JavaScript oder Markdown, und wenn Ihr Team bestimmte Richtlinie für diese Sprachen hat, wäre es von Vorteil, diese in einen Linter zu implementieren, damit sie automatisch jedes Mal überprüft werden, wenn ein Entwickler das Projekt erstellt.

#### <a name="automated-testing"></a>Automatische Tests

Mithilfe von automatischen Tests können Entwickler einfach überprüfen, ob nach dem Anwenden der neuesten Änderungen auf das Projekt alle Elemente weiterhin erwartungsgemäß arbeiten. Mit dem Projekt wächst auch die Bedeutung automatischer Tests: Wenn sich die Codebasis erweitert, hat jede Änderung größere Auswirkungen, und das Risiko, dass andere Codestücke betroffen sind, wächst. Mit automatischen Tests können Entwickler überprüfen, ob die Lösung korrekt funktioniert, und mögliche Probleme frühzeitig abfangen.

SharePoint Framework bietet standardmäßige Unterstützung für den [Karma](http://karma-runner.github.io/1.0/index.html) Test Runner und das [Mocha](http://mochajs.org)-Framework, das Entwickler zum Schreiben von Tests verwenden können. Bei Bedarf können Entwickler zusätzliche Bausteine verwenden, die mit SharePoint Framework bereitgestellt werden, z. B. [PhantomJS](http://phantomjs.org), um die Reichweite der Tests zu vergrößern. Alle Tests in SharePoint Framework-Projekten können mithilfe der `gulp test`-Standardaufgabe ausgeführt werden.

#### <a name="code-analysis"></a>Codeanalyse

Linting ist zwar hilfreich, um die korrekte Syntax der jeweiligen Datei zu überprüfen, häufig benötigen Entwickler aber weitere Unterstützung, um zu überprüfen, ob das Projekt als Ganzes den Richtlinien entspricht. Im Allgemeinen konzentrieren sich Linter auf den Code selbst, können aber den Kontext der jeweiligen Codedatei nicht interpretieren. In SharePoint Framework-Lösungen haben Artefakte bestimmte Anforderungen, ein Webpart sollte beispielsweise eine eindeutige ID im Projekt aufweisen. Organisationen haben möglicherweise auch andere Anforderungen, z. B. nicht auf Skripts aus CDN zu verweisen oder nur eine bestimmte Version der jeweiligen Bibliothek zu verwenden. An diesen Punkten sind Linter in der Regel nicht ausreichend, und Entwickler benötigen andere Tools.

[SharePoint Code Analysis Framework](https://spcaf.com) (SPCAF) ist eine Drittanbieterlösung, die häufig von SharePoint-Entwicklern, Administratoren und Mitarbeitern in Qualitätssicherungs- und Sicherheitsrollen verwendet wird, um zu überprüfen, dass SharePoint-Anpassungen den Qualitätsrichtlinien der Organisation entsprechen. SPCAF wird in den gesamten Lebenszyklusprozess der Anwendung integriert, sodass Unternehmen die Gesamtbetriebskosten von SharePoint-Anpassungen senken können. SPCAF bietet eine Reihe von Regeln, die speziell auf SharePoint Framework-Lösungen abzielen.

## <a name="upgrading-sharepoint-framework-projects"></a>Aktualisieren von SharePoint Framework-Projekten

Das Bereitstellen einer SharePoint-Anpassung in der Produktion stellt in der Regel nicht das Ende ihres Lebenszyklus dar. Häufig ändern sich die Anforderungen, oder es werden neue Anforderungen hinzugefügt, was in beiden Fällen zu Änderungen in der Lösung führt. Um eine Anpassung, die zuvor in der Produktion bereitgestellt wurde, ordnungsgemäß zu aktualisieren, müssen Entwickler mehrere Dinge berücksichtigen.

### <a name="semantic-versioning-semver"></a>Semantische Versionsverwaltung (SemVer)

SharePoint Framework verwendet mit wenigen Ausnahmen die semantische Versionsverwaltung (SemVer) für die Nachverfolgung von Versionsnummern. Die semantische Versionsverwaltung ist ein Versionsverwaltungsmuster, mit dem Softwareentwickler weltweit arbeiten. Eine SemVer-Nummer besteht aus den drei Zahlen MAJOR.MINOR.PATCH und optionalen Bezeichnungen, z. b. 1.0.1.

> Hinweis: SharePoint Framework unterstützt derzeit nur für die Verwendung der drei Zahlen ohne Bezeichnungen.

Unterschiedliche Teile einer SemVer-Zahl werden je nach Typ der Änderung, der auf die Lösung angewendet wird, erhöht:

- MAJOR, wenn die Änderungen nicht abwärtskompatibel sind
- MINOR, wenn die Änderungen neue Funktionen einführen, die abwärtskompatibel sind
- PATCH, wenn es sich bei den Änderungen um abwärtskompatible Fehlerkorrekturen handelt

Sie dürfen nicht vergessen, dass es sich bei SemVer lediglich um einen Vertrag handelt. Es liegt an Ihrem Team, sich an diesen zu halten, um die Änderungen in der neuesten Version zu verdeutlichen.

Weitere Informationen zur semantischen Versionsverwaltung finden Sie unter [http://semver.org](http://semver.org).

### <a name="increase-version-number"></a>Erhöhen der Versionsnummer

Wenn Sie einen Teil einer SharePoint Framework-Lösung aktualisieren, sollten Entwickler Versionsnummern der betroffenen Datenelemente erhöhen, um deutlich zu kennzeichnen, welche Elemente geändert wurden und was die Auswirkungen dieser Änderungen sind.

#### <a name="increase-package-version-in-packagejson"></a>Erhöhen der Paketversion in „packet.json“

Ein SharePoint Framework-Paket ist wie ein Node.js-Paket strukturiert. Alle zugehörigen Abhängigkeiten und Metadaten werden in der Datei **package.json** im Projektordner gespeichert. Eine der Eigenschaften in der Datei **package.json** ist die Version-Eigenschaft, die die Version des gesamten Projekts bezeichnet. Obwohl die Versionsnummer rein zu Informationszwecken dient und nicht von den bereitgestellten Artefakten verwendet wird, sollten Entwickler die Versionsnummer in der Datei **package.json** jedes Mal erhöhen, wenn eine neue Version des Projekts gemäß der SemVer-Konvention geplant ist.

#### <a name="increase-solution-package-version-in-package-solutionjson"></a>Erhöhen der Lösungspaketversion in „package-solution.json“

SharePoint Framework-Lösungen werden mithilfe einer **.spapp**-Datei bereitgestellt, die im App-Katalog eines SharePoint-Mandanten installiert wird. Eine **.spapp**-Datei ist vergleichbar mit einem SharePoint-Add-In-Paket und folgt denselben Versionsverwaltungskonventionen. Die aktuelle Version des **.spapp**-Pakets wird unter Verwendung einer vierteiligen Zahl (MAJOR.MINOR.REVISION.BUILD) definiert, die in der Datei **config/Paket-solution.json** gespeichert wird. Aus Gründen der Übersichtlichkeit sollten Entwickler diese Nummer synchron mit der Versionsnummer in der Datei **package.json** halten, da beide Nummern auf die Version des Projekts als Ganzes verweisen.

> Hinweis: Das Erhöhen der Versionsnummer in der Datei „package-solution.json“ zwischen den einzelnen Versionen ist erforderlich, damit die neue Version des Pakets in SharePoint korrekt bereitgestellt wird.

#### <a name="increase-web-part-version-in-the-web-part-manifest"></a>Erhöhen der Webpartversion im Webpartmanifest

Jedes clientseitige Webpart, das auf SharePoint Framework basiert, enthält ein Manifest, dem SharePoint Framework Informationen über das Webpart bereitstellt, z. B. Titel, Symbol, Eigenschaften und wo sich das Codebundle befindet. Jedes Webpart verfügt auch über seine eigene Versionsnummer, die im Manifest des einzelnen Webparts in der **Version**-Eigenschaft gespeichert wird. Die **Version**-Eigenschaft folgt dem SemVer-Schema mit drei Zahlen ohne Bezeichnung. Das Webpartmanifest ist im **.spapp**-Paket enthalten, das in SharePoint bereitgestellt wird.

Beim Aktualisieren eines Webparts sollten Entwickler die Versionsnummer so ändern, dass diese dem Umfang der angewendeten Änderungen entspricht. Wenn das Projekt mehrere Webparts enthält und das Webpart zwischen den einzelnen Versionen nicht geändert wurde, sollte die Versionsnummer dieses Webparts nicht geändert werden.

### <a name="update-dependencies"></a>Aktualisieren von Abhängigkeiten

Einer der Gründe für eine Aktualisierung eines SharePoint Framework-Projekts kann eine Änderung an einer der zugrunde liegenden Abhängigkeiten sein, z. B. eine neue Version von Angular mit Fehlerkorrekturen und Leistungsverbesserungen. Wenn Ihr Team den empfohlenen Ansatz verwendet, bei dem npm shrinkwrap zum Sperren der Abhängigkeitenversionen verwendet wird, so würden Sie den `npm install <package>@<version> --save`-Befehl verwenden, um Ihre Abhängigkeit auf die bestimmte Version zu aktualisieren und Ihr Projekt testen, um zu überprüfen, ob es wie erwartet mit den neuesten Updates funktioniert. Je nachdem, welche Auswirkungen die Änderungen an den zugrunde liegenden Abhängigkeiten auf das Projekt haben, kann das gesamte Projektupdate von einem Patch bin zu einer vollständigen Hauptversion reichen.

### <a name="build-and-package-project-in-release-mode"></a>Erstellen und Verpacken des Projekts im Releasemodus

Nachdem Sie überprüft haben, dass die Lösung wie erwartet funktioniert, erstellen Sie das Projekt im Releasemodus mithilfe des `gulp bundle --ship`-Befehls. Erstellen Sie dann ein neues Paket mit dem `gulp package-solution --ship`-Befehl. Ohne zuerst den `gulp bundle --ship`-Befehl auszuführen, umfasst das Paket frühere Versionen Ihres Projekts.

### <a name="deploy-new-version-of-your-solution"></a>Bereitstellen der neuen Version Ihrer Lösung

Nach dem Erstellen und Verpacken des Projekts besteht der nächste Schritte darin, das Projekt bereitzustellen. Stellen Sie zuerst die aktualisierten Webpartbundle bereit, die sich im Ordner **./temp/deploy** in Ihrem Projekt befinden. Veröffentlichen Sie die Dateien neben Webpartbundles der früheren Version Ihrer Lösung.

> Hinweis: Sie sollten die früheren Versionen Ihrer Lösung nicht entfernen, solange aktive Instanzen von Webparts diese verwenden. Jede Version der Bundledateien hat einen eindeutigen Namen, und durch Entfernen früherer Versionen vor dem Aktualisieren von Webparts werden diese Webparts zerstört.

Stellen Sie als Nächstes das neue Lösungspaket im SharePoint-App-Katalog bereit. Dies ist erforderlich, um SharePoint über die neue Version der Lösung zu benachrichtigen, die angewendet werden soll.