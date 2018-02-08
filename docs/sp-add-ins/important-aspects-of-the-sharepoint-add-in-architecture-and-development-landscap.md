---
title: "Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins"
description: "Die Architektur von und das Modell für SharePoint-Add-Ins, einschließlich Hostingoptionen für Add-Ins, Benutzeroberflächenoptionen, das Bereitstellungssystem, das Sicherheitssystem und der Lebenszyklus."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 62e9b707b65f1f954aa01cf5696e04b13373c3b8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape"></a>Kritische Aspekte der Architektur und der Entwicklungslandschaft für SharePoint-Add-Ins


<a name="SPAppModelArch_SPCenteredVsCloudCentered"> </a> Dieser Artikel dient als Ergänzung zum Artikel [SharePoint-Add-Ins](sharepoint-add-ins.md).

Das SharePoint-Add-In-Modell bietet folgende Möglichkeiten zum Hosten der Komponenten eines SharePoint-Add-Ins: 

-  **Vom Anbieter gehostet:** Add-In, die mindestens eine Remotekomponente und möglicherweise auch SharePoint-Komponenten enthalten. Add-In, deren SharePoint-fremde Komponenten von Ihrer Logik auf Ihrem Hardware- oder Cloudkonto bereitgestellt werden, oder auf dem Hardware- oder Cloudkonto des Kunden mithilfe von Installationsprogrammen und Anleitungen, die Sie bereitstellen.

-  **Von SharePoint-gehostet:** Add-Ins, die nur SharePoint-Komponenten und -Logik enthalten, die auf dem Client ausgeführt werden.

Ausführlichere Informationen über Hostingoptionen sowie Anleitungen für die Wahl der geeigneten Option finden Sie unter [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md).

<a name="SPComponents"> </a>
## <a name="add-in-webs-host-webs-features-and-sharepoint-components-in-add-ins"></a>Add-In-Webs, Hostwebs, Features und SharePoint-Komponenten in Add-Ins

Die Website, auf der das SharePoint-Add-In installiert ist, wird als Hostweb bezeichnet. Die wesentlichen Komponenten des SharePoint-Add-Ins, sowohl SharePoint-Komponenten als auch externe Komponenten, werden nicht für das Hostweb bereitgestellt. Externe Komponenten werden auf externen Servern oder in Cloudkonten bereitgestellt. SharePoint-Komponenten werden auf einer speziellen Website mit einer eigenen Domäne bereitgestellt. Dies wird als Add-In-Web bezeichnet. 

Nur eine begrenzte Anzahl von Benutzeroberflächenelementen, über die Benutzer auf die anderen Komponenten des Add-Ins zugreifen können, wird für das Hostweb bereitgestellt. Diese Benutzeroberflächenkomponenten im Hostweb werden im Rahmen des Hostwebfeatures bereitgestellt, eines Features, das in dem Add-In-Paket separat bereitgestellt wird, statt in einer WSP-Datei. Die Komponenten, die für das Add-In-Web bereitgestellt werden, sind immer in den Features in einer WSP-Datei enthalten. Beide Arten der Features müssen **Web** als Bereich aufweisen. Es ist kein anderer Bereich für Features in SharePoint-Add-Ins möglich.

Als allgemeine Regel kann jede SharePoint-Komponente, die keinen, auf SharePoint-Servern ausgeführten, benutzerdefinierten Code enthält, in einem SharePoint-Add-In einbezogen (und im Add-In-Web bereitgestellt) werden. Es gibt jedoch einige Ausnahmen und bestimmte Nuancen, die dabei berücksichtigt werden müssen, wie und wann die Komponenten bereitgestellt werden. Weitere Informationen zu diesen Nuancen und zum Hostweb, dem isolierten Add-In-Web und Features in Add-Ins finden Sie unter [Hostweb, Add-In-Web und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md).

<a name="AccessingApp"> </a>
## <a name="accessing-the-add-in-from-the-ui"></a>Zugreifen auf das Add-In über die Benutzeroberfläche

Wenn ein SharePoint-Add-In auf einer Website installiert ist, wird das Add-In auf der Seite **Websiteinhalt** der Hostwebsite aufgeführt. Benutzer können das Add-In auf dieser Seite starten. Wenn das Add-In auf diese Weise geöffnet wird, wird es im Vollbildmodus ausgeführt.

SharePoint-Add-Ins können des Weiteren über eine Add-In-Komponente verfügbar gemacht werden, eine Art Webpart, die durch die **ClientWebPart**-Klasse dargestellt wird. Diese Art Webpart ist im Wesentlichen ein Wrapper für ein IFrame, der eine Seite des Add-Ins hosten würde. Im einfachsten Fall ist die einzige wichtige Eigenschaft des Webparts eine URL, die auf die Seite verweist. 

Webparts können jedoch benutzerdefinierte Eigenschaften aufweisen, die Benutzer in einem Toolpart festlegen können. Diese Eigenschaften könnten zum Beispiel zum Festlegen von Kontextinformationen wie Postleitzahl des Benutzers verwendet werden. Um solche Add-In-Komponenten in Ihrem Add-In hinzuzufügen, erstellen Sie ein Hostwebfeature im Add-In und fügen ein deklaratives Webpart-Markup hinzu. Wie alle anderen Webparts wird es in der SharePoint-Benutzeroberfläche angezeigt, über die Benutzer Webparts hinzufügen. Sie können bei Bedarf mehr als ein Add-In-Webpart für das Add-In bereitstellen. Beispielsweise kann ein Wetter-Add-In eine Add-In-Komponente enthalten, die die aktuelle Wettervorhersage anzeigt, und eine zweite Add-In-Komponente, die eine wöchentliche Wettervorhersage anzeigt. Die beiden Komponenten können unterschiedliche Größen und Funktionen aufweisen.

> [!NOTE]
> Sie können Add-In-Parts auch für die Add-In-Website bereitstellen. Dazu muss das Markup für das Webpart Teil eines Features in einer WSP-Datei im Add-In-Paket sein, nicht im Hostweb-Feature.

Es wird empfohlen, dass Sie das Erscheinungsbild Ihrer Add-Ins so weit wie möglich an SharePoint orientieren. Dies ist jedoch nicht zwingend erforderlich und möglicherweise nicht immer die beste Möglichkeit. Weitere Informationen zu den UX-Richtlinien finden Sie unter [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins.md). 

Beispielsweise gibt es eine spezielle Masterseite mit dem Namen app.master. Diese Seite ist für die Verwendung durch die Seiten von Add-Ins optimiert. Die app.master-Seite ist Teil einer neuen Websitedefinition, die in SharePoint enthalten ist. 

Ein anderes Tool, dass Sie für ein einheitliches Aussehen und Verhalten Ihrer Add-Ins mit SharePoint verwenden können, ist das Chromsteuerelement, das im Lieferumfang von SharePoint enthalten ist. Mit diesem Steuerelement können Sie den SharePoint-Navigationsheaderbereich zu Ihren Add-In-Seiten hinzufügen, einschließlich extern gehosteter Seiten. Weitere Informationen zum UX-Design in SharePoint-Add-Ins finden Sie unter [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins.md). Weitere Informationen über das Chromsteuerelement finden Sie unter [Verwenden des Chromsteuerelements in SharePoint-Add-Ins](use-the-client-chrome-control-in-sharepoint-add-ins.md).

<a name="SPAppModelArch_Package"> </a>
## <a name="add-in-package-structure"></a>Add-In-Paketstruktur

Ein SharePoint-Add-In-Paket ist eine Datei mit der Erweiterung „APP“, die dem Standard [Open Packaging Conventions (OPC)](http://msdn.microsoft.com/de-DE/magazine/cc163372.aspx) entspricht. (Sie können die Datei öffnen, indem Sie „ZIP“ als zusätzliche Erweiterung zu dem Dateinamen hinzufügen und sie dann im Windows-Explorer öffnen.) Sie enthält ein Add-In-Manifest, das bestimmte Eigenschaften des Add-Ins und Anweisungen für die SharePoint-Installationsinfrastruktur angibt. Weitere Informationen zum Add-In-Manifest und zum Paket finden Sie unter [Hinweise zur App-Manifeststruktur und zum Paket eines SharePoint-Add-Ins](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md).

<a name="SPAppModelArch_Running"> </a>
## <a name="permissions-authentication-and-authorization-for-sharepoint-add-ins"></a>Berechtigungen, Authentifizierung und Autorisierung für SharePoint-Add-Ins

SharePoint führt ein neues Add-In-Berechtigungs- und Sicherheitssystem ein.

<a name="AppPermissions"> </a>
### <a name="add-in-permissions"></a>Add-In-Berechtigungen

SharePoint-Add-Ins verfügen wie Benutzer und Gruppen über Berechtigungen. Dadurch kann ein Add-In über eine Gruppe von Berechtigungen verfügen, die sich von den Berechtigungen des Benutzers, der das Add-In ausführt, unterscheiden. 

Sie müssen in der Add-In-Manifest-Datei die Berechtigungen anfordern, die ein Add-In für die Ausführung benötigt. Der Benutzer, der das Add-In hinzufügt, muss diese Rechte erteilen, wobei er nur die Berechtigungen erteilen kann, über die er selbst als Benutzer verfügt. Die Erteilung muss für alle angeforderten Berechtigungen oder für keine davon erfolgen, um die Berechtigungsverwaltung für Benutzer und Entwickler zu vereinfachen. (Der Add-In-Prinzipal verfügt grundsätzlich über Vollzugriffsrecht für die Add-In-Website, daher müssen nur Berechtigungen für SharePoint-Ressourcen in der Hostwebsite oder Positionen außerhalb der Add-In-Website angefordert werden.)

Weitere Informationen über Add-In-Berechtigungen finden Sie unter [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint.md).

<a name="SelectiveAuthorization"> </a>
### <a name="selective-delegation-and-authorization"></a>Selektive Delegierung und Autorisierung

Weder Benutzer, die ein Add-In starten, noch Ressourcenbesitzer, die einem Add-In die Berechtigung zum Zugriff auf eine Ressource gewähren, müssen Anmeldeinformationen oder das Kennwort im Add-In angeben. Stattdessen wird in SharePoint ermöglicht, dass Benutzer und Ressourcenbesitzer nur bestimmte Berechtigungen gewähren können, die das Add-In anfordert. Dies ist durch die Verwendung des Transaktionsprotokolls [OAuth 2.0](http://tools.ietf.org/html/draft-ietf-oauth-v2-22) in SharePoint möglich. Weitere Informationen zu OAuth in SharePoint finden Sie unter [Kontexttoken-OAuth-Fluss für SharePoint-Add-Ins](context-token-oauth-flow-for-sharepoint-add-ins.md).

<a name="cross-domain-access"> </a>
### <a name="cross-domain-access"></a>Domänenübergreifender Zugriff

Ein SharePoint-Add-In, das eine Remote-Webanwendung umfasst, welche JavaScript für seine Datenzugriffslogik verwendet, kann eine domänenübergreifende JavaScript-Bibliothek nutzen, um autorisierten Zugriff auf SharePoint-Daten innerhalb der Mandanteneinheit zu erhalten, in der das Add-In installiert ist. Weitere Informationen finden Sie unter [Zugreifen auf SharePoint-Daten über Add-Ins mithilfe der domänenübergreifenden Bibliothek](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).

<a name="SPAppModelArch_Lifecycle"> </a>
## <a name="add-in-lifecycle"></a>Add-In-Lebenszyklus

Der Lebenszyklus für ein SharePoint-Add-In umfasst das Veröffentlichen, Installieren, Aktualisieren und Deinstallieren. Weitere Informationen zu diesen Themen finden Sie unter [Veröffentlichen von SharePoint-Add-Ins](publish-sharepoint-add-ins.md), [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md) und [Aktualisierungsvorgang für SharePoint-Add-Ins](sharepoint-add-ins-update-process.md). 

Beachten Sie den Mechanismus, mit dem Mandantenadministratoren eine Batchinstallation eines SharePoint-Add-Ins auf mehreren Websites durchführen können. Weitere Informationen finden Sie unter [Mandantschaften und Bereitstellungsbereiche von SharePoint-Add-Ins](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md)

<a name="Data"> </a>
## <a name="data-storage-in-sharepoint-add-ins"></a>Datenspeicheroptionen in SharePoint-Add-Ins

SharePoint-Add-Ins können alle möglichen Arten von Daten erstellen oder darauf zugreifen, darunter strukturierte Daten, Dokumente, und Multimedia-Dateien. Diese Daten können in SharePoint oder einem externen Speicherort gespeichert werden. 

<a name="StructuredData"> </a>
### <a name="structured-data-storage-options"></a>Optionen zum Speichern von strukturierten Daten

Ein SharePoint-Add-In kann nahezu jede Art von strukturiertem Datenspeicher verwenden, in und außerhalb von SharePoint und auf Microsoft- und Nicht-Microsoft-Plattformen. Im folgenden finden Sie *einige* Speicherorte, an denen Sie strukturierte Daten für ein SharePoint-Add-In speichern können:

- SharePoint-Listen in einem Add-In-Web
- SQL Azure
- Externe mit SharePoint über Microsoft Business Connectivity Services (BCS) verbundene Datenquellen
- Ein nicht-Microsoft-Clouddienst
- Eine Datenbank auf Ihrem eigenen Server

> [!TIP]
> Sie werden wahrscheinlich zu einem bestimmten Zeitpunkt ein Upgrade für das SharePoint-Add-In durchführen. Wenn ein SharePoint-Add-In SharePoint-Komponenten in einem Add-In-Web enthält, wird beim Upgradevorgang eine vollständige Kopie des Add-In-Web erstellt. Aus diesem Grund führen sehr große SharePoint-Listen im Add-In-Web dazu, dass der Upgradevorgang auf dem Inhaltsdatenbankserver zeitaufwändig und prozessorintensiv ist. Sie sollten keine Big Data zu SharePoint-Listen im Add-In-Web hinzufügen.

<a name="UnStructuredData"> </a>
### <a name="unstructured-data-storage-options"></a>Optionen zum Speichern von unstrukturierten Daten

Dokumente, Bilder, Videos, Audiodateien und andere Arten von nicht strukturierten Daten, die erzeugt oder von einem SharePoint-Add-In verwendet werden, können in oder außerhalb von SharePoint gespeichert werden. Dokumentbibliotheken sind eine gute Wahl für Dokumente und können über die SharePoint-Suche durchsucht werden. Eine Website-Objektbibliothek ist oftmals eine gute Wahl für Multimediadateien. 

Zu den anderen Optionen gehört der BLOB-Speicher in Ihrem Microsoft Azure-Konto oder auf Ihren eigenen Servern. Sie können Dateien auch auf einigen nicht-Microsoft-Plattformen oder in Clouddiensten speichern.

<a name="AppMetadata"> </a>
### <a name="add-in-settings-and-other-metadata-storage-options"></a>Add-In-Einstellungen und andere Speicheroptionen für Metadaten

Metadaten für ein SharePoint-Add-In, u. a. Benutzereinstellungen, Informationen zum Speicherort, und andere Einstellungen können an verschiedenen Orten gespeichert werden. Manchmal ist eine ausgeblendete SharePoint-Liste eine gute Wahl. Sie können auch den Eigenschaftenbehälter des Add-In-Web verwenden. Eine weitere Möglichkeit für ein vom Anbieter gehostetes Add-In stellt der Azure-Tabellenspeicher dar. 

<a name="DataAccess"> </a>
### <a name="secure-data-access-options"></a>Optionen für den sichere Datenzugriff

Die Optionen für den sicheren Datenzugriff hängen selbstverständlich von der Wahl des Speichers ab. Datenzugriff und Suche werden in zahlreichen Artikeln genau erläutert. Weitere Informationen dazu finden Sie unter [Sicherer Datenzugriff und Clientobjektmodelle für SharePoint-Add-Ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md).

<a name="SPAppModelArch_Managing"> </a>
## <a name="managing-add-ins"></a>Verwalten von Add-Ins

Websitesammlungsadministratoren und Mandantenadministratoren können Add-Ins überwachen und die ihnen zugewiesenen Ressourcen ändern. Außerdem können Microsoft-Mitarbeiter des Add-In-Stores Add-Ins mit Flags versehen und sie deaktivieren.

Weitere Informationen zum Verwalten von Add-Ins finden Sie unter [Installieren und Verwalten von SharePoint-Add-Ins](http://msdn.microsoft.com/de-DE/library/733647a3-a5d3-475b-967d-3bb627c2a0c2) auf TechNet.

<a name="SPAppModelArch_Monitoring"> </a>
### <a name="monitoring-add-ins"></a>Überwachen von Add-Ins

SharePoint bietet Integritätsüberwachung für Add-Ins und stellt diese Informationen über die Benutzeroberfläche für Websitebesitzer, Mandanten- und Farmadministratoren zur Verfügung. Die meisten Dokumente zur Systemüberwachung finden Sie auf TechNet, u. a. [Überwachen von SharePoint-Add-Ins](http://technet.microsoft.com/library/3adafdd2-f276-4a9d-8a74-e06b8916bbc2). Dieser Abschnitt enthält nur eine kurze Einführung zur Überwachung von Add-Ins, die Sie verkaufen.

Einige Arten von Daten werden pro App gemeldet, andere dagegen pro App-Instanz. Folgendes sind die primären Elemente, die das Überwachungs-Framework meldet:

- Verwendung des Add-Ins, z. B. wie oft es installiert wurde (Erstellen einer neuen Instanz). 
- Serverressourcenverbrauch jeder Add-In-Instanz.
- Installations-, Aktualisierungs- und Laufzeitfehler jeder Add-In-Instanz.
- Ein Hinweis auf die Gesamtintegrität jeder Add-In-Instanz durch grüne, gelbe und rote Farbanzeige.

Wenn das Add-In Azure-Website-Komponenten umfasst, fragt das Überwachungs-Framework außerdem Azure stündlich nach Fehlerdaten ab und meldet kritische Fehler und Speicherkontingentdaten auf der SharePoint-Benutzeroberfläche. Azure SQL-Datenbank-Fehler werden nicht gemeldet.

Mit den durch das Überwachungs-Framework bereitgestellten Informationen können Administratoren bestimmen, ob ihr Budget zum Kauf von Add-Ins klug verwendet wird, ob sie weitere Ressourcen für Add-Ins bereitstellen müssen, und ob sie ein nicht einwandfrei funktionierendes Add-In deaktivieren sollten.

<a name="RegisterDependency"> </a>
## <a name="registering-add-in-dependencies"></a>Registrieren von Add-In-Abhängigkeiten

Wenn Ihr SharePoint-Add-In von einer SharePoint-Funktion abhängt, die nicht verfügbar ist und im Add-In-Web nicht verfügbar gemacht werden kann, funktioniert das Add-In nicht richtig, was zu Beschwerden von Seiten der Kunden führen kann. Sie können sicherstellen, dass das Add-In nicht installiert wird, wenn die erforderlichen Dienste und Features nicht verfügbar sind: Registrieren Sie hierzu die Abhängigkeiten des Add-Ins im Add-In-Manifest. Die Installationsinfrastruktur für SharePoint-Add-Ins sucht nach diesen Voraussetzungen und verhindert die Installation des Add-Ins, wenn eine davon nicht erfüllt wird.

Bei Diensten wie Excel, Access oder Visio prüft die Infrastruktur, ob der Dienst installiert und lizenziert ist.

Für Features wie die Aufgabenliste überprüft die Infrastruktur, dass das Feature bereitgestellt und dass es:

- im **Farm**-, **WebApplication**- oder **Site**-Bereich (Websitesammlung) aktiviert ist,

oder

- mit dem **Web**-Bereich im Add-In-Web aktivierbar ist, das beim Installieren des Add-Ins erstellt wird.
 
> [!NOTE]
> Die Add-In-Installationsinfrastruktur aktiviert diese Features im Add-In-Web automatisch, wenn es erstellt wird.

Die folgenden Abschnitte enthalten die Details, die Sie benötigen, um die erforderlichen Komponenten registrieren zu können.

<a name="PermAsPreq"> </a>
### <a name="implicitly-register-dependencies-with-permission-requests"></a>Impliziertes Registrieren von Abhängigkeiten mit Berechtigungsanforderungen

Wenn Ihr Add-In Zugriff auf SharePoint-Komponenten außerhalb des Add-In-Webs benötigt, muss es die Berechtigung für diese Ressourcen im Abschnitt **AppPermissionRequests** des Add-In-Manifests anfordern. Diese Berechtigungsanforderungen dienen auch als Voraussetzungsregistrierungen, da SharePoint aus den von Ihrem Add-In angeforderten Berechtigungen ableitet, dass für das Add-In bestimmte SharePoint-Funktionen verfügbar sein müssen. In vielen Fällen kann SharePoint alle vom Add-In benötigten Funktionen ableiten, sodass Sie die verbleibenden Abschnitte dieses Themas nicht benötigen. Redundante Abhängigkeitsregistrierungen haben jedoch keine negativen Auswirkungen.

<a name="Explicit"> </a>
### <a name="explicitly-register-dependencies-with-appprerequisites"></a>Explizites Registrieren von Abhängigkeiten mit AppPrerequisites

Falls Ihr Add-In über eine Abhängigkeit verfügt, die nicht anhand ihrer Berechtigungsanforderungen impliziert wird, können Sie jede Abhängigkeit mit einem **AppPrerequisite**-Element im Add-In-Manifest registrieren. Dieses Element umfasst drei Attribute: **Type**, **ID** und (optional) **MinimumVersion**. 

Es gibt drei mögliche erforderliche Werte für **Type**: `Feature`, `Capablility` und `AutoProvisioning`. Eine Featurevoraussetzung ist einfach ein SharePoint-Feature, das im Add-In-Web oder einem größeren Bereich mit dem Add-In-Web bereitgestellt und aktiviert werden muss. Eine Funktion ist eine Reihe von verwandten Features und Diensten, die im Add-In-Web verfügbar sein müssen. (`AutoProvisioning` wird im nächsten Abschnitt genauer erläutert.)

Mit dem optionalen **MinimumVersion**-Attribut wird die niedrigste Version des für das Add-In erforderlichen Features bzw. der Funktion angegeben. Die Attributwerte haben das Format n.n.n.n; z. B.  `15.0.0.0`.

Die **ID** gibt an, welche Feature oder Funktion erforderlich ist. Wenn **Type** `Feature` ist, ist**ID** die GUID des Features (in Klammern und mit Bindestrich), z. B. `{151D22D9-95A8-4904-A0A3-22E4DB85D1E0}`. Wenn **Type** `Capability` ist, ist **ID** die GUID der Funktion. Die Funktionen werden nachfolgend aufgeführt. Informationen zum Abrufen der GUID einer Funktion finden Sie unter [AppPrerequisite-Element (AppPrerequisiteCollection complexType) (SharePoint-Add-In-Manifest)](http://msdn.microsoft.com/library/791be402-981f-519e-fcde-f24cc3cb4139%28Office.15%29.aspx).

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

- [Auswählen von Mustern für die Entwicklung und das Hosting Ihres Add-Ins für SharePoint](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md)
- [Hostwebs, Add-In-Webs und SharePoint-Komponenten in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)

## <a name="see-also"></a>Siehe auch
<a name="SPAppModelArch_AdditionalResources"> </a>

-  [SharePoint-Add-Ins](sharepoint-add-ins.md)
-  [SharePoint-Add-Ins im Vergleich zu SharePoint-Lösungen](http://msdn.microsoft.com/library/0e9efadb-aaf2-4c0d-afd5-d6cf25c4e7a8%28Office.15%29.aspx)
-  [Add-In-Berechtigungen in SharePoint](add-in-permissions-in-sharepoint.md)
-  [OAuth-Ablauf mit Kontexttoken für SharePoint-Add-Ins](context-token-oauth-flow-for-sharepoint-add-ins.md)
-  [UX-Design für SharePoint-Add-Ins](ux-design-for-sharepoint-add-ins.md)
-  [IFrame](http://www.w3schools.com/tags/tag_iframe.asp)
-  [Hinweise zur App-Manifeststruktur und zum Paket eines SharePoint-Add-Ins](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md)
-  [Bereitstellen und Installieren von SharePoint-Add-Ins: Methoden und Optionen](deploying-and-installing-sharepoint-add-ins-methods-and-options.md)
-  [Aktualisierungsverfahren für SharePoint-Add-Ins](sharepoint-add-ins-update-process.md)
-  [Mandantschaften und Bereitstellungsbereiche von SharePoint- Add-Ins](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md)
    
 

