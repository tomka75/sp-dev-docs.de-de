---
title: "Erstellen von SharePoint-Add-Ins, die eine Autorisierung mit hoher Vertrauenswürdigkeit verwenden"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: d39ab5425d0ba60f47dbf2902e4c3cd1e6d4c689
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="creating-sharepoint-add-ins-that-use-high-trust-authorization"></a>Erstellen von SharePoint-Add-Ins, die eine Autorisierung mit hoher Vertrauensstellung verwenden
Erfahren Sie mehr über besonders vertrauenswürdige SharePoint-Add-Ins, die digitale Zertifikate verwenden, um eine Vertrauensstellung zwischen SharePoint und den Remotekomponenten einzurichten, die auf SharePoint zugreifen.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 

 **Von:**
 
Steve Peschka, Microsoft Corporation

Siew Moi Khor, Microsoft Corporation
 

## <a name="overview-of-high-trust-sharepoint-add-ins"></a>Übersicht über besonders vertrauenswürdige SharePoint-Add-Ins
<a name="Overview"> </a>

Ein besonders vertrauenswürdiges Add-In ist eine vom Anbieter gehostete SharePoint-Add-In, die in einer lokalen SharePoint-Farm installiert wird. Sie kann nicht in Microsoft SharePoint Online installiert werden oder über den Office Store vertrieben werden. Für ein besonders vertrauenswürdiges Add-In wird zum Einrichten der Vertrauensstellung anstelle eines Kontexttoken ein Zertifikat verwendet.
 

 

 **Hinweis** In diesem Thema erfahren Sie mehr über das besonders vertrauenswürdige Autorisierungssystem für SharePoint-Add-Ins. Praktische Informationen zur Erstellung und Bereitstellung besonders vertrauenswürdiger Add-Ins finden Sie in den folgenden Themen: [Erstellen besonders vertrauenswürdiger SharePoint-Add-Ins](create-high-trust-sharepoint-add-ins.md) [Packen und Veröffentlichen besonders vertrauenswürdiger SharePoint-Add-Ins](package-and-publish-high-trust-sharepoint-add-ins.md)
 

In SharePoint liefert der Sicherheitstokendienst Zugriffstoken für Server-zu-Server-Authentifizierung. Der Sicherheitstokendienst aktiviert vorübergehende Zugriffstoken, um auf andere Anwendungsdienste wie Exchange 2013, Lync 2013 und SharePoint-Add-Ins zuzugreifen. Ein Farmadministrator richtet eine Vertrauensstellung zwischen SharePoint und der anderen Anwendung oder dem Add-In ein, indem er Windows PowerShell-Cmdlets und ein Zertifikat verwendet. Jedes Zertifikat, das verwendet wird, muss von SharePoint mithilfe des Cmdlets  `New-SPTrustedRootAuthority` als vertrauenswürdig eingestuft werden. Außerdem muss jedes Zertifikat bei SharePoint mithilfe des Cmdlets `New-SPTrustedSecurityTokenIssuer` als ein Tokenherausgeber registriert werden.
 

 

 **Hinweis** Der Sicherheitstokendienst ist nicht für die Benutzerauthentifizierung vorgesehen. Daher wird der Sicherheitstokendienst weder auf der Benutzeranmeldeseite, noch im Abschnitt **Authentifizierungsanbieter** der Zentraladministration oder in der Personenauswahl in SharePoint angezeigt.
 


## <a name="two-kinds-of-token-issuers"></a>Zwei Arten von Tokenherausgebern
<a name="TwoKindsOfIssuers"> </a>

Die Remotewebanwendung einer besonders vertrauenswürdigen SharePoint-Add-In ist an ein digitales Zertifikat gebunden. (Informationen zur entsprechenden Vorgehensweise finden Sie in den beiden oben verlinkten Themen.) Das Zertifikat wird von der Remotewebanwendung verwendet, um die Zugriffstoken zu signieren, die sie in alle Anforderungen an SharePoint einfügt. Die Webanwendung signiert das Token mit dem privaten Schlüssel des Zertifikats, und SharePoint validiert es mit dem öffentlichen Schlüssel des Zertifikats. Das Zertifikat muss als vertrauenswürdiger Tokenherausgeber registriert sein, bevor SharePoint den Token vertraut, die von diesem ausgestellt werden. Es gibt zwei Arten von Tokenherausgebern: Die einen können nur Token für eine bestimmte SharePoint-Add-In ausstellen, die anderen, die als Vertrauensbroker bezeichnet werden, können Token für mehrere SharePoint-Add-Ins ausstellen.
 

 
In der Praxis legen SharePoint-Farmadministratoren anhand der Switches und Parameterwerte, die sie mit dem Cmdlet  `New-SPTrustedSecurityTokenIssuer` verwenden, fest, welche Art von Tokenherausgeber erstellt wird. Um einen Tokenherausgeber zu erstellen, der ein Vertrauensbroker ist, fügen Sie der Befehlszeile den Switch `-IsTrustBroker` hinzu, und verwenden Sie für den `-Name`-Parameter einen eindeutigen Wert, der nicht mit der Client-ID des Add-Ins identisch ist. Hier sehen Sie ein bearbeitetes Beispiel.
 

 



```
New-SPTrustedSecurityTokenIssuer -IsTrustBroker -RegisteredIssuerName "<full_token_issuer_name> " --other parameters omitted--
```

Um einen Tokenherausgeber zu erstellen, der kein Broker ist, wird der Switch  `-IsTrustBroker` nicht verwendet. Es besteht ein weiterer Unterschied. Der Wert des `-RegisteredIssuerName`-Parameters weist stets die Form zweier GUIDs auf, die durch das Zeichen "@" getrennt sind;  _GUID_@ _GUID_. Die GUID auf der rechten Seite ist immer die ID des Authentifizierungsbereichs der SharePoint-Farm (oder des Websiteabonnements). Die GUID auf der linken Seite ist immer eine bestimmte ID für einen Tokenherausgeber. Es handelt sich um eine zufällige GUID, wenn ein Tokenherausgeber erstellt wird, der ein  *Vertrauensbroker*  ist. Wenn jedoch ein Tokenherausgeber erstellt wird, der kein Vertrauensbroker ist, muss die spezifische Herausgeber-GUID mit der GUID identisch sein, die als Client-ID der SharePoint-Add-In verwendet wird. Dieser Parameter liefert nicht nur einen Namen für den Herausgeber, sondern er informiert SharePoint auch darüber, welche SharePoint-Add-In die einzige ist, für die das Zertifikat Token ausstellen kann. Hier ein unvollständiges Beispiel:
 

 



```
$fullIssuerIdentifier = "<client_ID_of_SP_app> " + "@" + "<realm_GUID> "
New-SPTrustedSecurityTokenIssuer -RegisteredIssuerName $fullIssuerIdentifier --other parameters omitted--
```

Normalerweise wird das Cmdlet  `New-SPTrustedSecurityTokenIssuer` in einem Skript verwendet, das andere Aufgaben durchführt, um SharePoint für besonders vertrauenswürdige Add-Ins zu konfigurieren. Weitere Informationen zu diesen Skripts und vollständige Beispiele für das Cmdlet `New-SPTrustedSecurityTokenIssuer` finden Sie unter [Besonders vertrauenswürdige Konfigurationsskripts für SharePoint](high-trust-configuration-scripts-for-sharepoint.md).
 

 

## <a name="deciding-between-using-one-certificate-or-many-for-high-trust-sharepoint-add-ins"></a>Entscheiden zwischen der Verwendung eines oder mehrerer Zertifikate für besonders vertrauenswürdige SharePoint-Add-Ins
<a name="Deciding"> </a>

SharePoint- und Netzwerkadministratoren können zwischen zwei grundlegenden Strategien wählen, wenn sie Zertifikate zur Verwendung durch besonders vertrauenswürdige SharePoint-Add-Ins abrufen und verwalten:
 

 

- Verwenden des gleichen Zertifikats für mehrere SharePoint-Add-Ins
    
 
- Verwenden eines separaten Zertifikats für jede SharePoint-Add-In
    
 
In diesem Abschnitt werden die Vor- und Nachteile der jeweiligen Strategie erläutert.
 

 
Der Vorteil der Verwendung des gleichen Zertifikats für mehrere SharePoint-Add-Ins ist, dass ein Administrator weniger Zertifikate hat, die als vertrauenswürdig eingestuft und verwaltet werden müssen. Der Nachteil dieses Ansatzes ist, dass Sie im Falle, dass der Administrator einer bestimmten SharePoint-Add-In das Vertrauen entziehen möchte, nur die Möglichkeit haben, das Zertifikat als Tokenherausgeber oder als Stammautorisierungsstelle zu entfernen. Wenn Sie das Zertifikat entfernen, wird aber auch allen anderen SharePoint-Add-Ins, die das gleiche Zertifikat verwenden, das Vertrauen entzogen, sodass sie nicht mehr verwendet werden können.
 

 
Damit die weiterhin vertrauenswürdigen SharePoint-Add-Ins wieder verwendet werden können, müsste der Administrator  *mithilfe eines neuen Zertifikats*  ein `New-SPTrustedSecurityTokenIssuer`-Objekt erstellen und die Kennzeichnung  `-IsTrustBroker` hinzufügen. Dann müsste das neue Zertifikat bei jedem Server registriert werden, der eines der vertrauenswürdigen Add-Ins hostet, und jedes dieser Add-Ins müsste an das neue Zertifikat gebunden werden.
 

 
Der Vorteil der Verwendung eines Zertifikats pro Add-In ist, dass es einfacher ist, einem bestimmten Add-In das Vertrauen zu entziehen, da die von den weiterhin vertrauenswürdigen Add-Ins verwendeten Zertifikate nicht betroffen sind, wenn der Administrator dem Zertifikat des einen Add-Ins das Vertrauen entzieht. Der Nachteil dieser Strategie besteht darin, dass ein Administrator mehr Zertifikate beschaffen muss und SharePoint so konfiguriert sein muss, dass jedes der Zertifikate verwendet wird, was mithilfe eines wiederverwendbaren Skripts erfolgen kann (siehe  [Besonders vertrauenswürdige Konfigurationsskripts für SharePoint](high-trust-configuration-scripts-for-sharepoint.md)).
 

 

## <a name="certificates-are-root-authorities-in-sharepoint"></a>Zertifikate sind Stammzertifizierungsstellen in SharePoint
<a name="RootAuthorities"> </a>

Wie kurz weiter oben in diesem Artikel erwähnt, müssen SharePoint-Farmadministratoren das Zertifikat der Remotewebanwendung in dem besonders vertrauenswürdigen Add-In zu einer vertrauenswürdigen Stammzertifizierungsstelle in SharePoint sowie zu einem vertrauenswürdigen Tokenherausgeber machen. Wenn es hinter dem Zertifikat der Webanwendung eine Hierarchie von Zertifizierungsstellen gibt, müssen alle Zertifikate in der Kette zur Liste der vertrauenswürdigen Stammzertifizierungsstellen in SharePoint hinzugefügt werden.
 

 
Jedes Zertifikat in der Kette wird durch den Aufruf des Cmdlets  `New-SPTrustedRootAuthority` zur Liste der vertrauenswürdigen Stammzertifizierungsstellen in SharePoint hinzugefügt. Nehmen wir beispielsweise an, dass das Zertifikat der Webanwendung ein Domänenzertifikat ist, das von einer Zertifizierungsstelle einer Unternehmensdomäne im LAN ausgestellt wurde, und dass dessen Zertifikat wiederum von einer eigenständigen Zertifizierungsstelle der obersten Ebene im LAN ausgestellt wurde. In diesem Szenario müssen sämtliche Zertifikate, d. h. das Zertifikat der Zertifizierungsstelle der obersten Ebene, der mittleren Ebene und der Webanwendung, der Liste der vertrauenswürdigen Stammzertifizierungsstellen in SharePoint hinzugefügt werden. Dazu könnte der folgende Windows PowerShell-Code verwendet werden.
 

 



```
$rootCA = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("<path_to_top-level_CA's_cer_file>")
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $rootCA

$intermediateCA = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("path_to_intermediate_CA's_cer_file")
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $intermediateCA

$certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("path_to_web_application's_cer_file") 
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $certificate 

```

Das Stammzertifikat und das Zertifikat der mittleren Ebene sollten nur einmal in einer SharePoint-Farm hinzugefügt werden. Normalerweise wird das Zertifikat der Webanwendung in einem separaten Skript hinzugefügt, das auch andere Konfigurationen vornimmt, wie dem Aufruf von  `New-SPTrustedSecurityTokenIssuer`. Beispiele finden Sie unter  [Besonders vertrauenswürdige Konfigurationsskripts für SharePoint](high-trust-configuration-scripts-for-sharepoint.md).
 

 
Wenn das Zertifikat der Webanwendung selbstsigniert ist, wie das z. B. der Fall ist, wenn das Add-In entwickelt und debuggt wird, gibt es keine Zertifikatskette, sodass nur das Zertifikat der Webanwendung der Liste der Stammauthentifizierungsstellen hinzugefügt werden muss.
 

 
Weitere Informationen finden Sie im Blog-Post  [Fehler: Dem Stamm der Zertifikatskette wird bei anspruchsbasierter Authentifizierung nicht vertraut](http://blogs.technet.com/b/speschka/archive/2010/02/13/root-of-certificate-chain-not-trusted-error-with-claims-authentication.aspx). (Überblättern Sie den Abschnitt zum Exportieren des Zertifikats aus Active Directory-Verbunddiensten, wobei davon ausgegangen wird, dass Sie Ihr Zertifikat für Ihre besonders vertrauenswürdigen Add-Ins auf anderem Weg erstellt haben, z. B. mithilfe eines durch eine Zertifizierungsstelle ausgestellten kommerziellen Zertifikats, eines selbstsignierten Zertifikats oder eines von der Domäne ausgestellten Zertifikats.)
 

 

## <a name="web-application-needs-to-know-that-it-is-a-token-issuer"></a>Die Webanwendung muss wissen, dass es sich um einen Tokenherausgeber handelt
<a name="AppIsTokenIssuer"> </a>

Die Remotewebanwendungs-Komponente des SharePoint-Add-Ins ist an ihr Zertifikat in IIS gebunden. Dies ist für die herkömmlichen Zwecke von Zertifikaten ausreichend: sicheres Identifizieren der Webanwendung und Kodieren der HTTP-Anforderungen und -Antworten. In einem besonders vertrauenswürdigen SharePoint-Add-In hat das Zertifikat jedoch die zusätzliche Aufgabe, offizieller „Aussteller“ der Zugriffstoken zu sein, die von der Webanwendung an SharePoint gesendet werden. Dazu muss die Webanwendung die Aussteller-ID des Zertifikats kennen, das verwendet wird, wenn das Zertifikat bei SharePoint als Tokenherausgeber registriert wird. Die Webanwendung findet diese ID im Abschnitt **appSettings** der Datei „web.config“, in dem sich ein Schlüssel mit der Bezeichnung **IssuerId** befindet. Anweisungen dazu, wie der Add-In-Entwickler diesen Wert festlegt und wie das Zertifikat an die Webanwendung in IIS gebunden wird, finden Sie unter [Packen und Veröffentlichen besonders vertrauenswürdiger SharePoint-Add-Ins](package-and-publish-high-trust-sharepoint-add-ins.md). Wenn der Kunde die Strategie verwendet, für jedes besonders vertrauenswürdige SharePoint-Add-In ein separates Zertifikat zu haben, wird der **ClientId**-Wert auch als der **IssuerId**-Wert verwendet. Dies gilt nicht, wenn mehrere Add-Ins das gleiche Zertifikat verwenden, da jedes SharePoint-Add-In seine eigene eindeutige Client-ID aufweisen muss, während die Aussteller-ID der Bezeichner für ein **SPTrustedSecurityTokenIssuer**-Objekt ist.
 

 
Es folgt ein Beispiel für einen **appSettings**-Abschnitt für ein besonders vertrauenswürdiges SharePoint-Add-In. In diesem Beispiel wird ein Zertifikat von mehreren Add-Ins gemeinsam verwendet. Daher ist die **IssuerId** nicht mit der **ClientId** identisch. Beachten Sie, dass ein besonders vertrauenswürdiges SharePoint-Add-In keinen **ClientSecret**-Schlüssel enthält.
 

 



```XML
<appSettings>
  <add key="ClientId" value="6569a7e8-3670-4669-91ae-ec6819ab461" />
  <add key="ClientSigningCertificatePath" value="C:\MyCerts\HighTrustCert.pfx" />
  <add key="ClientSigningCertificatePassword" value="3VeryComplexPa$$word82" />
  <add key="IssuerId" value="e9134021-0180-4b05-9e7e-0a9e5a524965" />
</appSettings>

```


 **Sicherheitshinweis** Im vorherigen Beispiel wird davon ausgegangen, dass das Zertifikat im Dateisystem gespeichert ist. Dies ist akzeptabel für Entwicklung und Debugging. In einem besonders vertrauenswürdigen SharePoint-Add-In für die Produktion wird das Zertifikat in der Regel im Windows-Zertifikatspeicher gespeichert, und die Schlüssel **ClientSigningCertificatePath** und **ClientSigningCertificatePassword** werden in der Regel durch einen **ClientSigningCertificateSerialNumber**-Schlüssel ersetzt.
 


## <a name="it-staff-responsibilities-in-the-high-trust-system"></a>Aufgaben der IT-Mitarbeiter im besonders vertrauenswürdigen System
<a name="ITPro"> </a>

Entwickler müssen die Anforderungen für Anwendungssicherheit, wie oben beschrieben, verstehen, während IT-Experten die Infrastruktur implementieren, die zur Unterstützung erforderlich ist. IT-Experten müssen die folgenden betrieblichen Anforderungen einplanen:
 

 

- Erstellen oder Erwerben mindestens eines Zertifikats, das für vertrauenswürdige SharePoint-Add-Ins verwendet wird.
    
 
- Sicherstellen, dass die Zertifikate sicher auf den Webanwendungsservern gespeichert werden. Bei Verwendung eines Windows-Betriebssystems bedeutet dies das Speichern der Zertifikate im Windows-Zertifikatspeicher.
    
 
- Verwalten der Verteilung dieser Zertifikate an Entwickler, die SharePoint-Add-Ins erstellen.
    
 
- Verfolgen der Stellen, an die jedes Zertifikat verteilt wird, sowohl für die Add-Ins, die es verwenden, als auch für die Entwickler, die eine Kopie erhalten haben. Wenn ein Zertifikat zurückgerufen werden muss, muss der IT-Mitarbeiter in Zusammenarbeit mit jedem Entwickler einen verwalteten Übergang zu einem neuen Zertifikat planen.
    
 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="AR"> </a>


-  [Erstellen von besonders vertrauenswürdigen SharePoint-Add-Ins](create-high-trust-sharepoint-add-ins.md)
    
 
-  [Packen und Veröffentlichen besonders vertrauenswürdiger SharePoint-Add-Ins](package-and-publish-high-trust-sharepoint-add-ins.md)
    
 
-  [Tipps zur Problembehandlung für besonders vertrauenswürdige Add-Ins unter SharePoint](http://blogs.technet.com/b/speschka/archive/2012/11/01/more-troubleshooting-tips-for-high-trust-apps-on-sharepoint-2013.aspx)
    
 
-  [Autorisierung und Authentifizierung für Add-Ins in SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md)
    
 

