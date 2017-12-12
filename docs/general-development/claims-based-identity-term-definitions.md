---
title: "Anspruchsbasierte Identität: Begriffsdefinitionen"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0f3decb5-dcd8-432f-9bb8-533f2d01bef7
ms.openlocfilehash: ab9e96d73a694747f42ee21797e8db032e12b670
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="claims-based-identity-term-definitions"></a>Anspruchsbasierte Identität: Begriffsdefinitionen

Tabelle 1 enthält Definitionen wichtiger Begriffe im Zusammenhang mit der anspruchsbasierten Identität.
  
    
    


**Tabelle 1. Definitionen von Begriffen im Zusammenhang mit anspruchsbasierter Identität**


|**Begriff**|**Definition**|
|:-----|:-----|
|Anspruch  <br/> |Eine Aussage, die ein Subjekt über sich selbst oder ein anderes Subjekt macht. Die Aussage kann beispielsweise einen Namen, eine Identität, einen Schlüssel, eine Gruppe, eine Berechtigung oder eine Fähigkeit betreffen. Ansprüche werden von einem Anbieter ausgestellt, erhalten einen Wert oder auch mehrere Werte und werden dann in Sicherheitstoken verpackt, die von einem Sicherheitstokendienst ausgestellt werden. Sie werden außerdem von einem Anspruchswerttyp und u. U. zugehörigen Metadaten definiert.  <br/> |
|Anspruchsname  <br/> |Ein benutzerfreundlicher Name für den Anspruchstyp.  <br/> |
|Anspruchstyp  <br/> |Der Typ der Anweisung in den Anspruch. Beispiele für Anspruch, die zuerst gehören nennen, Rolle, und e-Mail-Adresse. Der Anspruchstyp wird ein Kontext zu den Anspruchswert und in der Regel als Uniform Resource Identifier (URI) ausgedrückt wird. Der e-Mail-Adresse Anspruchstyp wird beispielsweise als  `http://schemas.microsoft.com/ws/2008/06/identity/claims/email`dargestellt.<br/> |
|Anspruchswert  <br/> |Der Wert der Anweisung in den Anspruch. Beispielsweise kann der Anspruchstyp **-Rolle** ist, einen Wert **Mitwirkender** handeln. Wenn der Forderungstyp **Vorname** ist, kann einen Wert **Matt** handeln. <br/> |
|Anspruchstyp  <br/> |Der Typ des Werts im Anspruch. Wenn beispielsweise der Anspruchswert **Mitwirkender** lautet, ist der Anspruchstypwert **String**. <br/> |
|Ansprüche unterstützende Anwendung  <br/> |Eine Softwareanwendung einer vertrauenden Seite, die Ansprüche zur Verwaltung der Identität und des Zugriffs für Benutzer verwendet.  <br/> |
|Anspruchsbasierte Identität  <br/> |Ein eindeutiger Bezeichner für einen bestimmten Benutzer, eine Anwendung, einen Computer oder eine andere Entität. Die anspruchsbasierte Identität ermöglicht der Entität den Zugriff auf mehrere Ressourcen wie Anwendungen und Netzwerkressourcen, ohne dass mehrfach die Anmeldeinformationen eingegeben werden müssen. Außerdem ermöglicht sie Ressourcen die Validierung von Anforderungen einer Entität.  <br/> |
|Anspruchsanbieter  <br/> |Eine Softwarekomponente oder Dienst, der einen oder mehrere Ansprüche während der Anmeldung Vorgänge ausstellen verwendet werden kann. Es wird auch angezeigt, auflösen und Bereitstellen von Funktionen für die Suche nach Forderungen in einer Auswahl Karte (beispielsweise im Auswahlsteuerelement Personen in SharePoint). Weitere Informationen finden Sie unter  [Anspruchsanbieter in SharePoint](claims-provider-in-sharepoint.md).<br/> |
|Forderungsanbieterschema  <br/> |Ein Schema, das angibt, welche Felder als Metadaten für einen Anspruch zurückgegeben werden müssen, der von einem bestimmten Forderungsanbieter ausgestellt wird.  <br/> |
|Forderungsanbieter - Sicherheitstokendienst  <br/> |Eine Softwarekomponente oder ein Dienst, die bzw. der von einem Forderungsanbieter genutzt wird, der Ansprüche ausstellt und in Sicherheitstoken verpackt.  <br/> |
|Delegieren  <br/> |Ein rich-Client, der auf einem anderen Client impersonate berechtigt ist. Beispiel: haben Sie eine Situation, in der eine Website Benutzern wahrgenommenen **Web1**, einen Infrastruktur Datendienst **Data2** aufruft. Es kann Vorteil für **Web1** ihren Benutzern beim Zugriff auf **Data2** Identitätswechsel sein. **Web1** kontaktiert ein Verbundservers um Ansprüche zu erhalten, die einen Benutzer dar. Wenn hergestellt wurde, kann der Verbundserver festlegen, ob **Web1** ist ein autorisierten Delegat, ist dies der Fall ist, sie den Identitätswechsel können. Wenn es autorisiert ist, greift **Web1** **Data2** beim fungieren als des Benutzers auf. <br/> |
|Identitätsanbieter  <br/> |Ein Identitätsanbieter ist eine Art Forderungsanbieter, die einmaliges Anmelden Funktionen zwischen einer Organisation und andere Forderungsanbieter und vertrauende Seiten bereitstellt.  <br/> |
|Sicherheitstokendienst für Identitätsanbieter oder vertrauende Seiten  <br/> |Eine Softwarekomponente oder ein Dienst, die bzw. der von einem Identitätsanbieter verwendet wird, um Token von einem Verbundpartner zu akzeptieren und anschließend Ansprüche und Sicherheitstoken für die Inhalte des eingehenden Sicherheitstokens in einem Format zu generieren, das von der vertrauenden Seite verbraucht werden kann. Ein Sicherheitstokendienst empfängt Sicherheitstoken vom Sicherheitstokendienst eines vertrauenswürdigen Verbundpartners oder Forderungsanbieters. Anschließend stellt der Sicherheitstokendienst der vertrauenden Seite neue Sicherheitstoken für eine lokale Anwendung der vertrauenden Seite aus.  <br/> |
|Vertrauende Seite  <br/> |Eine Anwendung, die Ansprüchen in von einem Forderungsanbieter ausgestellten Sicherheitstoken vertraut und diese verwendet. Beispielsweise könnte eine Organisation mit einer Website für Onlineauktionen ein Sicherheitstoken mit Ansprüchen empfangen, die bestimmen, ob ein Subjekt vollständig oder teilweise auf die Anwendung der vertrauenden Seite zugreifen kann.  <br/> |
|Anwendung der vertrauenden Seite  <br/> |Software, die Ansprüche verbrauchen kann, um Authentifizierungs- und Autorisierungsentscheidungen zu treffen. Die Anwendung der vertrauenden Seite empfängt die Ansprüche von einem Forderungsanbieter.  <br/> |
|Rich Client  <br/> |Ein Client, der das WS-Trust-Protokoll verwenden kann.  <br/> |
|Passive SAML-Anmeldung  <br/> |SAML passiven Anmeldung beschreibt den Prozess der anmelden. Wenn eine Anmeldung für eine Webanwendung für Token aus einen vertrauenswürdigen Anmeldeanbieter akzeptieren konfiguriert ist, wird diese Art der Anmeldung SAML passiven Anmeldung aufgerufen. Weitere Informationen finden Sie unter  [Eingehende Ansprüche: Anmelden bei SharePoint](incoming-claims-signing-into-sharepoint.md).<br/> |
|SAML-Sicherheitstoken (Security Assertion Markup Language)  <br/> |Das Datenformat für die Kommunikation von Ansprüchen zwischen einem Forderungsanbieter und einer vertrauenden Seite.  <br/> |
|Security Assertion Markup Language (SAML)  <br/> |Das WebSSO-Protokoll, das in der SAML 2.0-Kernspezifikation definiert ist. Das SAML-Protokoll bestimmt, wie HTTP-Webbrowserumleitungen zum Austausch von Assertionsdaten verwendet werden. SAML dient zur Authentifizierung und Autorisierung von Benutzern über sichere Grenzen hinweg.  <br/> |
|Sicherheitstoken  <br/> |Eine Repräsentation von Ansprüchen über das Netzwerk, die vom Aussteller kryptografisch signiert wird und gegenüber vertrauenden Seiten als starker Nachweis für die Integrität der Ansprüche und die Identität des Ausstellers gilt.  <br/> |
|Sicherheitstokendienst  <br/> |Ein Webdienst, der Ansprüche ausstellt und in verschlüsselten Sicherheitstoken verpackt. Weitere Informationen finden Sie unter  [WS-Sicherheit](http://www.oasis-open.org/committees/tc_home.php?wg_abbrev=wss) und [WS-Trust](http://www.oasis-open.org/committees/tc_home.php?wg_abbrev=ws-sx). <br/> |
|Herstellen einer Vertrauensstellung  <br/> |Ein Prozess, mit dem Vertrauensstellungen zwischen Forderungsanbietern und Anwendungen vertrauender Seiten hergestellt werden. Dieser Prozess umfasst den Austausch von Identifizierungszertifikaten, die es der vertrauenden Seite ermöglichen, dem Inhalt von Ansprüchen zu vertrauen, die der Forderungsanbieter ausstellt.  <br/> |
|Vertrauenswürdiger Anmeldeanbieter  <br/> |Ein externer (nicht zu SharePoint gehörender) Sicherheitstokendienst, dem SharePoint vertraut.  <br/> |
|Einmalige Webanmeldung (Web-SSO)  <br/> |Ein Prozess, der zum Austauschen von Authentifizierung und Autorisierung Benutzerdaten gemeinsam Organisationen ermöglicht. Web-SSO verwenden, können Benutzer in Partnerorganisationen zwischen Domänen ohne Anmeldeinformationen an jeder Domäne Grenze präsentieren sichere Web Übergang.  <br/> |
|WS-Verbund  <br/> |Die Organisation für die standard Weiterentwicklung von strukturierten Informationen Standards (OASIS-)-Spezifikation, die definiert, das Passive WS-Federation-Protokoll und andere Protokoll-Erweiterungen, die für den Verbund verwendet werden. Der WS-Federation-Standard definiert Mechanismen, die als Identität, Attribut, Authentifizierung und Autorisierung in unterschiedlichen Vertrauensstellungsbereichen verbunddomäne verwendet werden. Weitere Informationen zum WS-Verbund finden Sie unter  [Grundlegendes zu WS-Federation](http://msdn.microsoft.com/de-DE/library/bb498017.aspx).<br/> |
|Passiver WS-Verbund  <br/> |Das Protokoll zum Anfordern von Ansprüchen von einem Forderungsanbieter über HTTP-Webbrowserumleitungen. Dieses Protokoll wird in Abschnitt 13 der WS-Verbundspezifikation 1.2 beschrieben.  <br/> |
|WS-Verbund-PRP (Passive Requester Profile)  <br/> |Das WS-Federation Passive Requestor Profile beschreibt, wie die Vertrauenswürdigkeit Cross-Realm-Identität, Authentifizierung und Autorisierung Verbund Mechanismen, die in WS-Federation definiert sind von passiven anfordernden Personen, beispielsweise einen Webbrowser, verwendet werden können Identitätsdienste bereitstellen. Passive anfordernden Personen dieses Profils können nur das HTTP-Protokoll.  <br/> |
|WS-Sicherheit  <br/> |Der WS-Security Standard ist ein Satz von Protokollen, die sichere Web-Service-Kommunikation mithilfe von SOAP unterstützen. Weitere Informationen zu WS-Security finden Sie auf der Website OASIS-  [OASIS-Web Services Security (WSS) TC](http://www.oasis-open.org/committees/tc_home.php?wg_abbrev=wss) .<br/> |
|WS-Trust  <br/> |Ein Standard, der WS-Security-Webdienste mit Methoden zum Erstellen und Überprüfen von Vertrauensstellungen bereitstellen verwendet. Weitere Informationen zum WS-Trust finden Sie auf der Website OASIS-  [OASIS-Web Services Secure Exchange (WS-SX) TC](http://www.oasis-open.org/committees/tc_home.php?wg_abbrev=ws-sx) .<br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-osl#_Toc223175002)
    
  
-  [Anspruchsbasierte Identität und-Konzepte in SharePoint](claims-based-identity-and-concepts-in-sharepoint.md)
    
  
-  [Stellvertretung, Verbund und Authentifizierung Beispielszenario SharePoint](sample-delegation-federation-and-authentication-scenario-in-sharepoint.md)
    
  

