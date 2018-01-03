---
title: "Anspruchsbasierte Identität und Konzepte in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d96c7cf4-2e48-4223-a3c0-42368d079b74
ms.openlocfilehash: 45834f7699463a2ee849edc78e9c7d34166d3bbb
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="claims-based-identity-and-concepts-in-sharepoint"></a>Anspruchsbasierte Identität und Konzepte in SharePoint

## <a name="claims-based-identity-model"></a>Anspruchsbasiertes Identitätsmodell

Wenn Sie die Ansprüche unterstützende Anwendungen erstellen, bietet dem Benutzer eine Identität für Ihre Anwendung als eine Reihe von Ansprüchen aus. Ein Anspruch den Namen des Benutzers kann, eine andere möglicherweise eine e-Mail-Adresse. Die Idee ist, dass der Anwendung, die von der Anwendung empfangenen Identitätsdaten von einer vertrauenswürdigen Quelle stammen alle Informationen, die sie benötigt, über den Benutzer bei jeder Anforderung zusammen mit kryptografischen Assurance zuweisen ein externen Identitäts-Systems konfiguriert ist.
  
    
    
Bei diesem Modell ist eine einmalige Anmeldung viel leichter durchzusetzen, und Ihre Anwendung ist nicht mehr für Folgendes zuständig:
  
    
    

- Authentifizierung von Benutzern
    
  
- Speicherung von Benutzerkonten und Kennwörtern
    
  
- Aufruf von Unternehmensverzeichnissen zum Nachschlagen von Benutzeridentitätsdetails
    
  
- Integration mit Identitätssystemen anderer Plattformen oder Unternehmen
    
  
Bei diesem Modell entscheidet die Anwendung identitätsbezogene basierend auf vom Benutzer bereitgestellte Ansprüche. Dies könnte aus einfachen Anwendung Personalisierung mit den Vornamen des Benutzers, für das die Benutzer Zugriff auf einer höheren Wert Features und Ressourcen in der Anwendung zu autorisieren.
  
    
    
Die folgenden Abschnitte erläutern die Terminologie und Konzepte, die Ihnen das Verständnis der anspruchsbasierten identitätsarchitektur erleichtern.
  
    
    

### <a name="identity-a-set-of-attributes-that-describe-an-entity"></a>Identität: Eine Reihe von Attributen, die eine Entität beschreiben

Unter "Identität" ist in diesem Kontext eine Gruppe von Attributen zu verstehen, die einen Benutzer oder eine andere Entität in einem System beschreibt, das Sie absichern möchten.
  
    
    

### <a name="claim-a-piece-of-identity-information"></a>Forderung: Eine Information Identität

Stellen Sie sich eine Forderung als eine Information Identität (beispielsweise Name, e-Mail-Adresse, Alter oder die Mitgliedschaft in der Rolle ""). Die weitere Ansprüche Ihrer Anwendung empfängt, je mehr Sie wissen über Ihre Benutzer. Diese werden "Ansprüchen" statt "Attribute" bezeichnet, wie häufig zum Beschreiben von Unternehmensverzeichnissen, aufgrund der Übermittlungsmethode verwendet wird. In diesem Modell wird die Anwendung nicht Benutzerattribute in einem Verzeichnis nachgeschlagen werden. Stattdessen der Benutzer bietet Forderungen an den die Anwendung und Ihre Anwendung überprüft werden. Jeder Anspruch erfolgt durch einen Aussteller, und nur ähnlich, wie Sie den Aussteller vertrauen, vertrauen den Anspruch. Beispielsweise verlassen Sie eine Forderung vorgenommene Ihres Unternehmens Domänencontroller mehr als eine Forderung vertrauenswürdigen vom Benutzer vorgenommen.
  
    
    

### <a name="security-token-a-serialized-set-of-claims"></a>Sicherheitstoken: einen serialisierten Satz von Ansprüchen

Der Benutzer bietet eine Reihe von Ansprüchen Ihrer Anwendung mit einer Anforderung. In einem Webdienst werden diese Ansprüche in der Kopfzeile der Sicherheit von SOAP-Umschlag übermittelt. In einer browserbasierten Webanwendung die Ansprüche von Browser des Benutzers über HTTP POST eintreffen, und möglicherweise später in einem Cookie zwischengespeichert werden, bei Bedarf eine Sitzung ist. Unabhängig davon, wie diese Ansprüche zu gelangen müssen sie serialisiert werden. Ein Sicherheitstoken ist ein serialisierten Ansprüche, die von der ausstellenden Zertifizierungsstelle signiert wurde. Die Signatur ist wichtig: können Sie sicherstellen, dass der Benutzer nicht nur von Ansprüchen und an Sie werden gesendet. In niedrige Sicherheitsstufe Situationen, in dem Kryptografie nicht erforderlich oder erwünscht ist, können nicht signierte Token, aber dieses Szenario wird in diesem Artikel nicht beschrieben.
  
    
    
Eine der Hauptfunktionen in Windows Identity Foundation (WIF) ist die Möglichkeit des Erstellens und Lesens von Sicherheitstoken. WIF und Microsoft .NET Framework sind für sämtliche kryptografischen Aufgaben zuständig und legen Ihrer Anwendung eine Gruppe von Ansprüchen vor, die diese lesen kann.
  
    
    

### <a name="security-token-service-sts"></a>Sicherheitstokendienst

Ein Sicherheitstokendienst (STS) ist die Grundstruktur, die erstellt, auf Anzeichen für und Sicherheitstoken entsprechend die interoperablen Protokolle im Abschnitt "Standards" dieses Artikels beschriebenen Probleme. Es gibt viele arbeiten bei Implementierung dieser Protokolle, aber WIF all dies für Sie lässt sich für eine Person, die keiner Protokolle ist ein STS Einstieg Experten und mit minimalem Aufwand ausgeführt wird. 
  
    
    
WIF macht das Erstellen eines eigenen STS einfach. Sie müssen lediglich bestimmen, wie die Logik samt Durchsetzungsregeln (d. h. die Sicherheitsrichtlinie) implementiert werden soll.
  
    
    

### <a name="issuing-authority"></a>Ausstellende Stelle

Es gibt viele verschiedene Typen von ausstellenden Behörden, von Domänencontrollern, die Kerberos-Tickets Zertifizierungsstellen ausstellen, die x. 509-Zertifikate aus. Welche Art von Autorität erläutert in diesem Artikel Aspekte Sicherheitstoken, die Ansprüche enthalten. Diese ausstellende Stelle ist a Web Application oder Webdienst, der Sicherheitstoken ausstellt. Es muss die richtige Ansprüche erhält das Ziel relying Party und der Benutzer, der die Anforderung ausstellen, und möglicherweise verantwortlich für die Interaktion mit Benutzerspeichern zum Nachschlagen von Ansprüchen und Authentifizieren von Benutzern.
  
    
    
Unabhängig davon, welche ausstellende Stelle Sie wählen, spielt diese eine Kernrolle in Ihrer Identitätslösung. Wenn Sie die Authentifizierung aus Ihrer Anwendung ausklammern, indem Sie auf Ansprüche setzen, übergeben Sie die Zuständigkeit an diese Stelle und fordern sie auf, die Authentifizierung von Benutzern in Ihrem Auftrag zu übernehmen.
  
    
    

### <a name="relying-parties"></a>Vertrauende Seiten

Bei der Erstellung einer Anwendung, die Ansprüche abhängt, erstellen Sie eine relying Party-Anwendung. Synonyme für eine vertrauende Seite einschließen "Ansprüche unterstützende Anwendung" und "Claims-based Application". Webanwendungen und Webdienste können beide vertrauenden Seiten sein.
  
    
    
Eine relying Party-Anwendung von einem STS ausgestellte Token verbraucht und extrahiert Ansprüche von Token für die Identität für die Nutzung Aufgaben im Zusammenhang mit. STS unterstützt zwei Arten von relying party Anwendung: ASP.NET Webanwendungen und Windows Communication Foundation (WCF)-Webdienste.
  
    
    

### <a name="standards"></a>Standards

All dies interoperable, tätigen WS-* Standards im vorherigen Szenario verwendet werden. Richtlinie wird mithilfe von WS-MetadataExchange abgerufen, und die Richtlinie selbst wird gemäß der Spezifikation WS-Policy strukturiert. Der STS stellt Endpunkte, die die Spezifikation WS-Trust implementieren, die beschreibt, wie zum Anfordern und Empfangen von Sicherheitstoken zur Verfügung. Die meisten Security Token services heute Problem Token mit Security Assertion Markup Language (SAML) formatiert. SAML ist ein anerkannten XML-Vokabular, die zur Darstellung von Ansprüchen Authentifizierungsdienste verwendet werden können. Oder in einer Situation für mehrere Plattformen Dadurch können Sie die Kommunikation mit einem STS auf eine vollständig andere Plattform und einmaliges Anmelden in allen Anwendungen, unabhängig von der Plattform zu erzielen.
  
    
    

### <a name="browser-based-applications"></a>Browserbasierte Anwendungen

Nicht nur intelligente Clients können mit dem anspruchsbasierten Identitätsmodell arbeiten. Browserbasierte Anwendungen (die als passive Clients bezeichnet werden) können dies auch, was im folgenden Abschnitt beschrieben wird.
  
    
    
Zunächst verweist ein Benutzer einen Browser an eine Ansprüche unterstützende Anwendung (die Anwendung mit vertrauender Seite). Die Webanwendung leitet den Browser an den Sicherheitstokendienst um, damit der Benutzer authentifiziert werden kann. Der Sicherheitstokendienst wird in einer einfachen Webanwendung gehostet, welche die eingehende Anforderung liest, den Benutzer mittels HTTP-Standardmechanismen authentifiziert und anschließend ein SAML-Token erstellen. Danach antwortet die Webanwendung mit einem ECMAScript (JavaScript, JScript)-Codefragment, das bewirkt, dass der Browser einen HTTP POST-Befehl auslöst, der das SAML-Token zurück zur vertrauenden Seite sendet. Der Hauptteil dieses POST-Befehls enthält die Ansprüche, die die vertrauende Seite angefordert hat. An dieser Stelle fügt die vertrauende Seite die Ansprüche häufig einem Cookie hinzu, damit der Benutzer nicht bei jeder Anforderung umgeleitet werden muss.
  
    
    

### <a name="claims-to-windows-token-service-c2wts"></a>Forderungen an den Windows-Tokendienst (c2WTS)

Der Forderungen an den Windows-Tokendienst (c2WTS) ist eine Komponente von Windows Identity Foundation (WIF). Der c2WTS extrahiert UPN-Ansprüche (User Principal Name, Benutzerprinzipalname) aus Nicht-Windows-Sicherheitstoken (z. B. SAML- und X.509-Token) und generiert Windows-Sicherheitstoken auf Identitätswechselebene. Dadurch kann die Anwendung auf der vertrauenden Seite die Identität des Benutzers übernehmen. Dies ist ggf. für den Zugriff auf Back-End-Ressourcen wie Computer mit Microsoft SQL Server erforderlich, die für den Computer mit der Anwendung der vertrauenden Seite als extern gelten.
  
    
    
Die c2WTS ist ein Windowsdienst, der als Teil des WIF installiert ist. Aus Sicherheitsgründen arbeitet die c2WTS nur für eine einzelne Opt in. Manuell gestartet werden müssen, und er wird als lokales Systemkonto ausgeführt. Ein Administrator muss die c2WTS mit einer Liste der zulässigen Anrufer auch manuell konfigurieren. Standardmäßig ist die Liste leer. 
  
    
    
Wenn die relying Party-Anwendung als lokales Systemkonto ausgeführt wird, muss es nicht die c2WTS verwenden. Jedoch ist die relying Party-Anwendung wird als das Netzwerkdienstkonto ausgeführt, oder einer Anwendung ASP.NET, beispielsweise es müssen möglicherweise die c2WTS Zugriff auf Ressourcen auf einem anderen Computer verwenden.
  
    
    
Nehmen Sie an, dass Sie über eine Webfarm verfügen, die von einem Server besteht, die eine Anwendung ASP.NET greift auf einer SQL-Datenbank auf einem Back-End-Server ausgeführt. Diese Anwendung Ansprüche unterstützenden werden sollen. Aber die Anwendung kann nicht mit den Anspruch, den sie aus einem STS erhält die SQL-Datenbank zugreifen. Stattdessen wird die c2WTS umzuwandelnde UPN-Anspruch auf einem Windows-Sicherheitstoken verwendet. Dies ermöglicht es Zugriff auf die SQL-Datenbank.
  
> [!NOTE]
> Wenn Sie den Zugriff auf Ressourcen auf einem anderen Server für eine Anwendung ermöglichen, muss ein Domänenadministrator den Active Directory-Verzeichnisdienst für eingeschränkte Delegierung konfigurieren. Informationen zum Aktivieren der eingeschränkten Delegierung finden Sie unter [Gewusst wie: Verwenden des Protokollübergangs und der eingeschränkten Delegierung in ASP.NET 2.0]((http://msdn.microsoft.com/de-DE/library/ms998355.aspx)). 
  
    
    


## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Authentifizierung, Autorisierung und Sicherheit in SharePoint](authentication-authorization-and-security-in-sharepoint.md)
    
  
-  [Stellvertretung, Verbund und Authentifizierung Beispielszenario SharePoint](sample-delegation-federation-and-authentication-scenario-in-sharepoint.md)
    
  
-  [Anspruchsbasierte Identität - Begriffsdefinitionen](claims-based-identity-term-definitions.md)
    
  

