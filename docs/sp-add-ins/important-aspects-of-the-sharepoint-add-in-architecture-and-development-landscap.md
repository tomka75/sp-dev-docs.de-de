
# <a name="important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape"></a>Wichtige Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins
Dieser Artikel enthält Informationen zur Architektur von SharePoint-Add-Ins und zum Modell für SharePoint-Add-Ins, einschließlich Add-In-Hostingoptionen, Benutzeroberflächenoptionen, Bereitstellungssystem, Sicherheitssystem und Lebenszyklus. Dieser Artikel ergänzt den Inhalt des Artikels  [SharePoint-Add-Ins](sharepoint-add-ins).
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint#bk_newname).
 


## <a name="sharepoint-add-ins-hosting-options"></a>Hostingoptionen für SharePoint Add-Ins
<a name="SPAppModelArch_SPCenteredVsCloudCentered"> </a>

Das SharePoint-Add-In-Modell bietet folgende Möglichkeiten zum Hosten der Komponenten eines SharePoint-Add-Ins: 
 

 

-  **Vom Anbieter gehostet:** Add-In, die mindestens eine Remotekomponente und möglicherweise auch SharePoint-Komponenten enthalten. Add-In, deren SharePoint-fremde Komponenten von Ihrer Logik auf Ihrem Hardware- oder Cloudkonto bereitgestellt werden, oder auf dem Hardware- oder Cloudkonto des Kunden mithilfe von Installationsprogrammen und Anleitungen, die Sie bereitstellen.
    
 
-  **Von SharePoint-gehostet:** Add-Ins, die nur SharePoint-Komponenten und -Logik enthalten, die auf dem Client ausgeführt werden.
    
 
Ausführlichere Informationen über Hostingoptionen sowie Anleitungen für die Wahl der geeigneten Option finden Sie unter  [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in).
 

 

## <a name="add-in-webs-host-webs-features-and-sharepoint-components-in-add-ins"></a>Add-In-Webs, Hostwebs, Features und SharePoint-Komponenten in Add-Ins
<a name="SPComponents"> </a>

Die Website, auf der ein SharePoint-Add-In installiert wird, wird als Hostwebsite bezeichnet. Die signifikanten Teile des SharePoint-Add-In werden jedoch, gleichgültig, ob es sich um SharePoint-Komponenten oder externe Komponenten handelt, nicht auf der Hostwebsite bereitgestellt. Externe Teile werden auf externen Servern oder Cloudkonten bereitgestellt. SharePoint-Komponenten werden auf einer speziellen Website mit eigener Domäne bereitgestellt. Diese wird als Add-In-Website bezeichnet. Nur eine begrenzte Gruppe von UI-Elementen, die Benutzern Zugriff zu den anderen Komponenten des Add-Ins ermöglichen, werden für die Hostwebsite bereitgestellt. Diese UI-Komponenten in der Hostwebsite werden als Teil eines Hostweb-Features bereitgestellt - ein Feature, das sich lose im Add-In-Paket anstatt in einer WSP-Datei befindet. Die Komponenten, die für die Add-In-Website bereitgestellt werden, sind immer in Features enthalten, die sich in einer WSP-Datei befinden. Beide Arten von Features müssen über **Web**-Bereich verfügen. Ein anderer Bereich ist für Features in SharePoint-Add-Ins nicht möglich.
 

 
Als allgemeine Regel gilt: Jede SharePoint-Komponente, die keinen benutzerdefinierten Code enthält, der auf SharePoint-Servern ausgeführt wird, kann einem SharePoint-Add-In hinzugefügt werden (und für die Add-In-Website bereitgestellt werden). Es gibt jedoch einige Ausnahmen und Feinheiten im Hinblick darauf, wie und wo die Komponenten bereitgestellt werden. Weitere Informationen zu diesen Feinheiten sowie über Hostwebsites, die isolierten Add-In-Websites und Features in Add-Ins finden Sie unter  [Hostwebsites, Add-In-Websites und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013).
 

 

## <a name="accessing-the-add-in-from-the-ui"></a>Zugreifen auf das Add-In über die Benutzeroberfläche
<a name="AccessingApp"> </a>

Wenn ein SharePoint-Add-In auf einer Website installiert ist, wird das Add-In auf der Seite **Websiteinhalt** der Hostwebsite aufgeführt. Benutzer können das Add-In auf dieser Seite starten. Wenn das Add-In auf diese Weise geöffnet wird, wird es im Vollbildmodus ausgeführt.
 

 
Eine andere Möglichkeit zum Anzeigen eines SharePoint-Add-In ist über ein Add-In-Part. Ein Add-In-Part ist ein Webpart-Typ, der durch die Klasse **ClientWebPart** repräsentiert wird. Diese Art von Webpart ist im Wesentlichen ein Wrapper für ein IFrame-Element, das eine Seite des Add-Ins hostet. Im einfachsten Fall ist die einzige wichtige Eigenschaft des Webparts eine URL, die auf die Seite verweist. Webparts können jedoch über benutzerdefinierte Eigenschaften verfügen, die Benutzer in einem Toolpart festlegen können. Solche Eigenschaften können z. B. verwendet werden, um Kontextinformationen, wie die Postleitzahl des Benutzers, festzulegen. Um Ihrem Add-In ein solches Add-In-Part hinzuzufügen, erstellen Sie ein Hostweb-Feature im Add-In und fügen deklaratives Webpart-Markup hinzu. Wie jedes andere Webpart wird es in der SharePoint-Benutzeroberfläche angezeigt, über die Benutzer Webparts hinzufügen. Sie können mehr als ein Add-In-Part mit Ihrem Add-In bereitstellen, wenn Sie noch mehr Variabilität benötigen. Beispielsweise kann ein Wetter-Add-In über ein Add-In-Part verfügen, das das aktuelle Wetter anzeigt, und ein zweites Add-In-Part, das eine Wettervorhersage für eine Woche anzeigt. Die beiden Parts können sich in Größe und Funktionalität unterscheiden.
 

 

 **Hinweis** Sie können Add-In-Parts auch für die Add-In-Website bereitstellen. Dazu muss das Markup für das Webpart Teil eines Features in einer WSP-Datei im Add-In-Paket sein, nicht im Hostweb-Feature.
 

Es wird empfohlen, dass Sie das Erscheinungsbild Ihrer Add-Ins so weit wie möglich an SharePoint orientieren. Dies ist jedoch nicht zwingend erforderlich und möglicherweise nicht immer die beste Möglichkeit.Weitere Informationen zu den UX-Richtlinien finden Sie unter  [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins). 
 

 
Beispielsweise gibt es eine spezielle Masterseite mit dem Namen app.master. Diese Seite ist für die Verwendung durch die Seiten von Add-Ins optimiert. Die app.master-Seite ist Teil einer neuen Websitedefinition, die in SharePoint enthalten ist. 
 

 
Ein anderes Tool, das Sie verwenden können, um für Ihre Add-Ins ein einheitliches Aussehen und Verhalten mit SharePoint zu erreichen, ist das Chromsteuerelement, das im Lieferumfang von SharePoint enthalten ist. Dieses Steuerelement ermöglicht es Ihnen, Ihren Add-In-Seiten den SharePoint-Navigationsheaderbereich hinzuzufügen, dies gilt auch für extern gehostete Seiten. Weitere Informationen zum UX-Design in SharePoint-Add-Ins finden Sie unter  [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins). Weitere Informationen über das Chromsteuerelement finden Sie unter  [Verwenden des Client-Chromsteuerelements in Add-Ins für SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins).
 

 

## <a name="add-in-package-structure"></a>Add-In-Paketstruktur
<a name="SPAppModelArch_Package"> </a>

Ein SharePoint-Add-In-Paket ist eine Datei, die die Erweiterung „.app" hat und mit  [OPC (Open Packaging Conventions)](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx) kompatibel ist. (Sie können die Datei öffnen, indem Sie „.zip" als zusätzliche Erweiterung zum Dateinamen hinzufügen und die Datei dann im Windows Explorer öffnen.) Das Paket enthält ein Add-In-Manifest, das bestimmte Eigenschaften des Add-Ins und Anweisungen für die SharePoint-Installationsinfrastruktur spezifiziert. Weitere Informationen über das Add-In-Manifest und -Paket finden Sie unter [Hinweise zur App-Manifeststruktur und zum Paket eines SharePoint-Add-Ins](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in).
 

 

## <a name="permissions-authentication-and-authorization-for-sharepoint-add-ins"></a>Berechtigungen, Authentifizierung und Autorisierung für SharePoint-Add-Ins
<a name="SPAppModelArch_Running"> </a>

SharePoint führt ein neues Add-In-Berechtigungs- und Sicherheitssystem ein.
 

 

### <a name="add-in-permissions"></a>Add-In-Berechtigungen
<a name="AppPermissions"> </a>

SharePoint-Add-Ins verfügen wie Benutzer und Gruppen über Berechtigungen. Dadurch kann ein Add-In über eine Gruppe von Berechtigungen verfügen, die sich von den Berechtigungen des Benutzers, der das Add-In ausführt, unterscheiden. 
 

 
Sie müssen in der Add-In-Manifest-Datei die Berechtigungen anfordern, die ein Add-In für die Ausführung benötigt. Der Benutzer, der das Add-In hinzufügt, muss diese Rechte erteilen, wobei er nur die Berechtigungen erteilen kann, über die er selbst als Benutzer verfügt. Die Erteilung muss für alle angeforderten Berechtigungen oder für keine davon erfolgen, um die Berechtigungsverwaltung für Benutzer und Entwickler zu vereinfachen. (Der Add-In-Prinzipal verfügt grundsätzlich über Vollzugriffsrecht für die Add-In-Website, daher müssen nur Berechtigungen für SharePoint-Ressourcen in der Hostwebsite oder Positionen außerhalb der Add-In-Website angefordert werden.)
 

 
Weitere Informationen über Add-In-Berechtigungen finden Sie unter [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint-2013).
 

 

### <a name="selective-delegation-and-authorization"></a>Selektive Delegierung und Autorisierung
<a name="SelectiveAuthorization"> </a>

Weder Benutzer, die ein Add-In starten, noch Ressourcenbesitzer, die einem Add-In Zugriffsrechte für eine Ressource erteilen, benötigen für das Add-In Anmeldeinformationen oder ein Kennwort. Stattdessen ermöglicht SharePoint Benutzern und Ressourcenbesitzern, nur die spezifischen Berechtigungen zu erteilen, welche das Add-In anfordert. Möglich wird dies, weil SharePoint das Transaktionsprotokoll  [OAuth 2.0](http://tools.ietf.org/html/draft-ietf-oauth-v2-22) verwendet. Weitere Informationen über OAuth in SharePoint finden Sie unter [OAuth-Ablauf mit Kontexttoken für Add-Ins in SharePoint](context-token-oauth-flow-for-sharepoint-add-ins).
 

 

### <a name="cross-domain-access"></a>Domainübergreifender Zugriff
<a name="SelectiveAuthorization"> </a>

Ein SharePoint-Add-In, das eine Remote-Webanwendung umfasst, welche JavaScript für seine Datenzugriffslogik verwendet, kann eine domänenübergreifende JavaScript-Bibliothek nutzen, um autorisierten Zugriff auf SharePoint-Daten innerhalb der Mandanteneinheit zu erhalten, in der das Add-In installiert ist. Weitere Informationen finden Sie unter  [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library).
 

 

## <a name="add-in-lifecycle"></a>Add-In-Lebenszyklus
<a name="SPAppModelArch_Lifecycle"> </a>

Der Lebenszyklus eines SharePoint-Add-In umfasst die Schritte der Veröffentlichung, Installation, Aktualisierung und Deinstallation. Weitere Informationen über diese Themen finden Sie unter  [Veröffentlichen von SharePoint-Add-Ins](publish-sharepoint-add-ins),  [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options) und [Aktualisierungsverfahren für Add-Ins für SharePoint](sharepoint-add-ins-update-process). Beachten Sie außerdem, dass es einen Mechanismus gibt, der Mandantenadministratoren die Stapelinstallation eines SharePoint-Add-In für mehrere Websites ermöglicht. Weitere Informationen finden Sie unter  [Mandantschaften und Bereitstellungsbereiche von Add-Ins für SharePoint](tenancies-and-deployment-scopes-for-sharepoint-add-ins).
 

 

## <a name="data-storage-in-sharepoint-add-ins"></a>Datenspeicheroptionen in SharePoint-Add-Ins
<a name="Data"> </a>

SharePoint-Add-Ins können alle möglichen Arten von Daten erstellen oder darauf zugreifen, darunter strukturierte Daten, Dokumente, und Multimedia-Dateien. Diese Daten können in SharePoint oder einem externen Speicherort gespeichert werden. 
 

 

### <a name="structured-data-storage-options"></a>Optionen zum Speichern von strukturierten Daten
<a name="StructuredData"> </a>

Ein SharePoint-Add-In kann nahezu jede Art von strukturiertem Datenspeicher verwenden, in und außerhalb von SharePoint und auf Microsoft- und nicht-Microsoft-Plattformen. Im folgenden finden Sie  *some*  -Speicherorte, an denen Sie strukturierte Daten für ein SharePoint-Add-In speichern können:
 

 

- SharePoint-Listen in einem Add-In-Web
    
 
- SQL Azure
    
 
- Externe mit SharePoint über Microsoft Business Connectivity Services (BCS) verbundene Datenquellen
    
 
- Ein nicht-Microsoft-Clouddienst
    
 
- Eine Datenbank auf Ihrem eigenen Server
    
 

 **Tipp** Zu einem bestimmten Zeitpunkt werden Sie Ihr SharePoint-Add-In aktualisieren. Wenn ein SharePoint-Add-In SharePoint-Komponenten in einem Add-In-Web umfasst, erstellt der Upgradeprozess eine vollständige Kopie des Add-In-Webs. Deshalb ist der Upgradeprozess durch die großen SharePoint-Listen im Add-In-Web sehr zeitaufwendig und prozessorintensiv auf dem Inhaltsdatenbankserver. Sie sollten es also vermeiden, „große Datenmengen“ in SharePoint-Listen im Add-In-Web abzulegen.
 


### <a name="unstructured-data-storage-options"></a>Optionen zum Speichern von unstrukturierten Daten
<a name="UnStructuredData"> </a>

Dokumente, Bilder, Videos, Audiodateien und andere Arten von nicht strukturierten Daten, die erzeugt oder von einem SharePoint-Add-In verwendet werden, können in oder außerhalb von SharePoint gespeichert werden. Dokumentbibliotheken sind eine gute Wahl für Dokumente und können über die SharePoint-Suche durchsucht werden. Eine Website-Objektbibliothek ist oftmals eine gute Wahl für Multimediadateien. 
 

 
Zu den anderen Optionen gehört der BLOB-Speicher in Ihrem Microsoft Azure-Konto oder auf Ihren eigenen Servern. Sie können Dateien auch auf einigen nicht-Microsoft-Plattformen oder in Clouddiensten speichern.
 

 

### <a name="add-in-settings-and-other-metadata-storage-options"></a>Add-In-Einstellungen und andere Speicheroptionen für Metadaten
<a name="AppMetadata"> </a>

Metadaten für ein SharePoint-Add-In, wie z. B. Benutzereinstellungen, Standortinformatioenn und andere Einstellungen können an verschiedenen Orten gespeichert werden. Eine ausgeblendete SharePoint-Liste ist manchmal eine gute Wahl. Sie können die Eigenschaftensammlung des Add-In-Webs verwenden. Eine andere Option für ein vom Anbieter gehostetes Add-In ist die Verwendung des Microsoft Azure-Tabellenspeichers. 
 

 

### <a name="secure-data-access-options"></a>Optionen für den sichere Datenzugriff
<a name="DataAccess"> </a>

Ihre Optionen für den sicheren Datenzugriff hängen natürlich von der Speicherwahl ab. Der Datenzugriff und die Suche weren detalliert in verschiedenen anderen Artikeln behandelt. Weitere Informationen finden Sie unter  [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins).
 

 

## <a name="managing-add-ins"></a>Verwalten von Add-Ins
<a name="SPAppModelArch_Managing"> </a>

Websitesammlungsadministratoren und Mandantenadministratoren können Add-Ins überwachen und die ihnen zugewiesenen Ressourcen ändern. Außerdem können Microsoft-Mitarbeiter des Add-In-Stores Add-Ins mit Flags versehen und sie deaktivieren.
 

 
Weitere Informationen zum Verwalten von Add-Ins finden Sie unter [Installieren und Verwalten von SharePoint-Add-Ins](http://msdn.microsoft.com/en-us/library/733647a3-a5d3-475b-967d-3bb627c2a0c2) auf TechNet.
 

 

### <a name="monitoring-add-ins"></a>Überwachen von Add-Ins
<a name="SPAppModelArch_Monitoring"> </a>

SharePoint bietet Integritätsüberwachung von Add-Ins und macht diese Informationen auf der Benutzeroberfläche für Websitebesitzer, Mandantenadministratoren und Farmadministratoren verfügbar. Die meiste Dokumentation für das Überwachungssystem befindet sich auf TechNet, z. B.  [Überwachen von Add-Ins für SharePoint](http://technet.microsoft.com/library/3adafdd2-f276-4a9d-8a74-e06b8916bbc2). Dieser Abschnitt ist nur eine kurze Einführung, um zu erläutern, wie Add-Ins, die Sie verkaufen, überwacht werden.
 

 
Einige Arten von Daten werden pro App gemeldet, andere dagegen pro App-Instanz. Folgendes sind die primären Elemente, die das Überwachungs-Framework meldet:
 

 

- Verwendung des Add-Ins, z. B. wie oft es installiert wurde (Erstellen einer neuen Instanz). 
    
 
- Serverressourcenverbrauch jeder Add-In-Instanz.
    
 
- Installations-, Aktualisierungs- und Laufzeitfehler jeder Add-In-Instanz.
    
 
- Ein Hinweis auf die Gesamtintegrität jeder Add-In-Instanz durch grüne, gelbe und rote Farbanzeige.
    
 
Wenn das Add-In Azure-Website-Komponenten umfasst, fragt das Überwachungs-Framework außerdem Microsoft Azure stündlich nach Fehlerdaten ab und meldet kritische Fehler und Speicherkontingentdaten auf der SharePoint-Benutzeroberfläche. Microsoft Azure SQL-Datenbank-Fehler werden nicht gemeldet.
 

 
Mit den durch das Überwachungs-Framework bereitgestellten Informationen können Administratoren bestimmen, ob ihr Budget zum Kauf von Add-Ins klug verwendet wird, ob sie weitere Ressourcen für Add-Ins bereitstellen müssen, und ob sie ein nicht einwandfrei funktionierendes Add-In deaktivieren sollten.
 

 

## <a name="registering-add-in-dependencies"></a>Registrieren von Add-In-Abhängigkeiten
<a name="RegisterDependency"> </a>

Wenn Ihr SharePoint-Add-In von einer SharePoint-Funktion abhängt, die nicht verfügbar ist und im Add-In-Web nicht verfügbar gemacht werden kann, funktioniert das Add-In nicht richtig, was zu Beschwerden von Seiten der Kunden führen kann. Sie können sicherstellen, dass das Add-In nicht installiert wird, wenn die erforderlichen Dienste und Features nicht verfügbar sind: Registrieren Sie hierzu die Abhängigkeiten des Add-Ins im Add-In-Manifest. Die Installationsinfrastruktur für SharePoint-Add-Ins sucht nach diesen Voraussetzungen und verhindert die Installation des Add-Ins, wenn eine davon nicht erfüllt wird.
 

 
Bei Diensten wie Excel, Access oder Visio prüft die Infrastruktur, ob der Dienst installiert und lizenziert ist.
 

 
Für Features wie die Aufgabenliste überprüft die Infrastruktur, dass das Feature bereitgestellt und dass es:
 

 
im **Farm**-, **WebApplication**- oder **Site**-Bereich (Websitesammlung) aktiviert ist,
 

 
oder
 

 
(mit dem **Web**-Bereich) im Add-In-Web aktivierbar ist, das beim Installieren des Add-Ins erstellt wird.
 

 

 **Hinweis** Die Add-In-Installationsinfrastruktur aktiviert diese Features im Add-In-Web automatisch, wenn es erstellt wird.
 

Die folgenden Abschnitte enthalten die Details, die Sie benötigen, um die erforderlichen Komponenten registrieren zu können.
 

 

### <a name="implicitly-register-dependencies-with-permission-requests"></a>Impliziertes Registrieren von Abhängigkeiten mit Berechtigungsanforderungen
<a name="PermAsPreq"> </a>

Wenn Ihr Add-In Zugriff auf SharePoint-Komponenten außerhalb des Add-In-Webs benötigt, muss es die Berechtigung für diese Ressourcen im Abschnitt **AppPermissionRequests** des Add-In-Manifests anfordern. Diese Berechtigungsanforderungen dienen auch als Voraussetzungsregistrierungen, da SharePoint aus den von Ihrem Add-In angeforderten Berechtigungen ableitet, dass für das Add-In bestimmte SharePoint-Funktionen verfügbar sein müssen. In vielen Fällen kann SharePoint alle vom Add-In benötigten Funktionen ableiten, sodass Sie die verbleibenden Abschnitte dieses Themas nicht benötigen. Redundante Abhängigkeitsregistrierungen haben jedoch keine negativen Auswirkungen.
 

 

### <a name="explicitly-register-dependencies-with-appprerequisites"></a>Explizites Registrieren von Abhängigkeiten mit AppPrerequisites
<a name="Explicit"> </a>

Falls Ihr Add-In über eine Abhängigkeit verfügt, die nicht anhand ihrer Berechtigungsanforderungen impliziert wird, können Sie jede Abhängigkeit mit einem **AppPrerequisite**-Element im Add-In-Manifest registrieren. Dieses Element umfasst drei Attribute: **Type**, **ID** und (optional) **MinimumVersion**. 
 

 
Es gibt drei mögliche Voraussetzungswerte für **Type**, `Feature`, `Capablility` und `AutoProvisioning`. Eine Featurevoraussetzung ist lediglich ein SharePoint-Feature, das im Add-In-Web oder in einem größeren Kontext, dessen Teil das Add-In-Web ist, bereitgestellt und aktiviert werden muss. Bei einer Funktion handelt es sich um eine Gruppe verwandter Features und Dienste, die im Add-In-Web verfügbar sein müssen. ( `AutoProvisioning` wird im nächsten Abschnitt behandelt.)
 

 
Mit dem optionalen **MinimumVersion**-Attribut wird die niedrigste Version des für das Add-In erforderlichen Features bzw. der Funktion angegeben. Die Attributwerte haben das Format „n.n.n.n“; z. B.  `15.0.0.0`.
 

 
Mit der **ID** wird angegeben, welches Feature oder welche Funktion erforderlich ist. Wenn **Type** auf `Feature` festgelegt ist, ist die **ID** die in Klammern gesetzte und mit Bindestrichen verbundene GUID des Features, z. B. `{151D22D9-95A8-4904-A0A3-22E4DB85D1E0}`. Wenn **Type** auf `Capability` festgelegt ist, entspricht die **ID** der GUID der Funktion. Die Funktionen sind weiter unten aufgelistet. Informationen für die Suche nach der GUID einer Funktion finden Sie unter [AppPrerequisite-Element (AppPrerequisiteCollection complexType) (SharePoint-Add-In-Manifest)](http://msdn.microsoft.com/library/791be402-981f-519e-fcde-f24cc3cb4139%28Office.15%29.aspx)
 

 

- Access Services 2010
    
 
- Access Services
    
 
- Verwalteter Metadatenwebdienst
    
 
- PowerPoint Services
    
 
- Secure Store Services
    
 
- Maschineller Übersetzungsdienst
    
 
- Benutzerprofildienst
    
 
- Visio-Grafikdienst
    
 
- Arbeitsverwaltungsdienst
    
 
- Duet
    
 
- Workflow
    
 
- Suche
    
 
- EDU
    
 
Dies ist ein Beispiel für eine Rohversion des **AppPrerequisites**-Markups, mit dem die Workflow-Funktion registriert wird. Wenn Sie Visual Studio verwenden, bearbeiten Sie das Add-In-Manifest in einem Designertool.
 

 



```
<AppPrerequisites>
  <AppPrerequisite Type="Capability" ID="{CDD8F991-B459-4512-8048-03D5A03FF27E}" MinimumVersion="15.0.0.0" />
</ AppPrerequisites>
```


## <a name="in-this-section"></a>Inhalt dieses Abschnitts
<a name="RegisterDependency"> </a>


-  [Auswählen von Mustern für die Entwicklung und das Hosten Ihres SharePoint-Add-Ins](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in)
    
 
-  [Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SPAppModelArch_AdditionalResources"> </a>


-  [SharePoint-Add-Ins](sharepoint-add-ins)
    
 
-  [SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen](http://msdn.microsoft.com/library/0e9efadb-aaf2-4c0d-afd5-d6cf25c4e7a8%28Office.15%29.aspx)
    
 
-  [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint-2013)
    
 
-  [OAuth-Ablauf mit Kontexttoken für SharePoint-Add-Ins](context-token-oauth-flow-for-sharepoint-add-ins)
    
 
-  [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins)
    
 
-  [IFrame](http://www.w3schools.com/tags/tag_iframe.asp)
    
 
-  [Hinweise zur App-Manifeststruktur und zum Paket eines SharePoint-Add-Ins](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in)
    
 
-  [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options)
    
 
-  [Aktualisierungsverfahren für SharePoint-Add-Ins](sharepoint-add-ins-update-process)
    
 
-  [Mandantschaften und Bereitstellungsbereiche von SharePoint- Add-Ins](tenancies-and-deployment-scopes-for-sharepoint-add-ins)
    
 

