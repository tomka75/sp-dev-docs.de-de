---
title: Beispieldelegierung-, Verbund- und Authentifizierungsszenario in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6e1b643582a9ae4df479ffc0e4016ca3ec5446aa
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sample-delegation-federation-and-authentication-scenario-in-sharepoint"></a>Beispieldelegierung-, Verbund- und Authentifizierungsszenario in SharePoint
Dieser Artikel enthält Beispielszenarien für identitätsdelegierung und Identitätsverbund.
## <a name="sample-scenarios"></a>Beispielszenarien
<a name="SP15_SampleDelegation_SampleScenarios"> </a>

Die folgenden fiktiven Unternehmen und ihren geschäftsanforderungen werden die Anforderungen in den Beispielszenarien verwendet, die in diesem Artikel beschrieben werden:
  
    
    

- **Contoso Hybrid** ist ein internationaler Autohändler Engine Kooperation von Unternehmen, die spezialisierte sich auf manufacturing elektrische und Brennstoffe Zelle-basierte Hybrid Module, Auto Hersteller innerhalb und außerhalb der USA. Die IT-Abteilung bei Contoso wird in eine strategische Aufwand für die Teile Sortierung optimierte seiner Kunden zu erfüllen damit beauftragt, mit dem Entwickeln und Bereitstellen einer sicheren Internet zugänglichen Webparts Sortierung-Anwendung über dem Hostnamen "contoso.com". Diese Anwendung muss auch mehrere Zugriffsebenen für verschiedene interne Benutzer (Contoso Mitarbeiter) und externe Benutzer (Auto Hersteller Mitarbeiter) bereitstellen. Minimieren der Kosten für die Verwaltung von den Teilen der Anwendung, Sortierung IT vermeiden Sie müssen auch die Notwendigkeit für die Anwendung verwenden und einen zusätzliche Kontospeicher für interne und externe Benutzer auf die Anwendung zugreifen.
    
  
- **Fabrikam Motors** ist ein Schwedisch Hersteller von sparsamsten compact Autos und kleine Autos, der bei seiner niedrigem Preis auf Hybrid Automobilen weltweit bekannt ist. Obwohl Sales konsistent jedes Jahr für Fabrikam eine schnellere haben, hat eine bedeutende Zunahme Hybrid Engine Fehlerraten im ersten Jahr, in Autos an Kunden verkauft wurde. Für Fabrikam vermeiden der Standard für high-Level des Diensts verwalten muss er eine effizientere Möglichkeit für hybride Engine Teile über Contoso Hybrid bestellt werden implementieren.
    
  
Die beiden folgenden Konzepte sind verwandt:
  
    
    

- **Identitätsverbund**. Dieses Szenario erläutert die Einrichtung eines Verbunds zwischen Contoso Hybrid und Fabrikam Motors, damit Fabrikam-Benutzer für den Zugriff auf Contoso Hybrid-Ressourcen eine Umgebung mit einmaliger Anmeldung erhalten.
    
  
- **Identitätsdelegierung**. Dieses Szenario veranschaulicht die Möglichkeit, auf Ressourcen eines Webdiensts von Contoso Hybrid zuzugreifen, der ein "ActAs"-Token erfordert. Dies bedeutet, dass der Dienst die Identität des unmittelbaren Aufrufers (in der Regel die Identität des Diensts) und des ursprünglichen Benutzers benötigt, von dem die Anforderung durchgeführt wurde (in der Regel die Identität des interaktiven Benutzers).
    
  

## <a name="identity-delegation"></a>Identitätsdelegation
<a name="SP15_SampleDelegation_IdentityDelegation"> </a>

In diesem Szenario wird eine Anwendung, die auf Back-End-Ressourcen zugreifen, die erfordern die Identität Delegierung Kette Access Control Prüfungen ausführen muss. Die Informationen auf dem ursprünglichen Anrufer und die Identität des Aufrufers sofortige besteht in der Regel eine einfache Identität Delegierung Kette aus. 
  
    
    
Mit dem Kerberos-Delegierung Objektmodell auf der Windows-Plattform heute stehen die Back-End-Ressourcen Zugriff nur für die Identität des Aufrufers sofortige und nicht auf, die mit dem ursprünglichen Aufrufer. Bei diesem Modell wird häufig als des vertrauenswürdigen Subsystems bezeichnet. Windows Identity Foundation (WIF) behält die Identität des dem ursprünglichen Anrufer und der direkte Aufrufer in der Kette Delegierung mithilfe der  [Delegate()](https://msdn.microsoft.com/en-us/library/cc310252.aspx) -Eigenschaft.
  
    
    
Abbildung 1 zeigt ein typisches identitätsdelegationsszenario in dem Fabrikam-Mitarbeiter in einer Anwendung Contoso.com verfügbar gemachten Ressourcen zugreift. **Abbildung 1. Forderungsbasierte Verbundauthentifizierung**

  
    
    

  
    
    
![Szenario der Forderungsidentitätsdelegierung](../images/44928b39-5683-4bce-8ddf-31d886243b87.gif)
  
    
    
Die folgenden fiktiven Benutzer sind an diesem Szenario beteiligt:
- Frank: Ein Fabrikam-Mitarbeiter, der auf Contoso-Ressourcen zugreifen möchte.
    
  
- Daniel: Ein Contoso-Anwendungsentwickler, der die notwendigen Änderungen in die Anwendung implementiert.
    
  
- Adam: Der IT-Administrator von Contoso.
    
  
Die folgenden Komponenten sind an diesem Szenario beteiligt:
- web1: Eine Webanwendung mit Links zu Back-End-Ressourcen, die die delegierte Identität des ursprünglichen Aufrufers erfordern. Diese Anwendung wurde mit ASP.NET erstellt.
    
  
- Ein Webdienst, der greift auf einem Computer mit Microsoft SQL Server, die die delegierte Identität mit dem ursprünglichen Aufrufer und der direkte Aufrufer erforderlich sind. Dieser Dienst wird mit Windows Communication Foundation (WCF) erstellt.
    
  
- sts1: Ein Sicherheitstokendienst (Security Token Service, STS) mit der Rolle des Verbundanbieters, der die von der Anwendung (web1) erwarteten Ansprüche ausgibt. Er hat eine Vertrauensstellung zu Fabrikam.com und zur Anwendung hergestellt.
    
  
- sts2: Ein STS mit der Rolle des Identitätsanbieters für Fabrikam.com, der einen vom Fabrikam-Mitarbeiter zur Authentifizierung verwendeten Endpunkt bereitstellt. Er hat eine Vertrauensstellung zu Contoso.com hergestellt, sodass Fabrikam-Mitarbeiter auf die Ressourcen von Contoso.com zugreifen können.
    
  
Beachten Sie, dass der Begriff "ActAs Token" auf ein Token verweist, die von einem STS ausgestellt wurde, und die Identität des Benutzers enthält. Die  [Delegate()](https://msdn.microsoft.com/en-us/library/cc310252.aspx) -Eigenschaft enthält die STS-Identität.Wie in Abbildung 1 dargestellt, ist der Ablauf in diesem Szenario:
  
    
    

1. Die Contoso-Anwendung wird für das Abrufen eines ActAs-Tokens konfiguriert, das die Identität des Fabrikam-Mitarbeiters und des unmittelbaren Aufrufers in der  [Delegate()](https://msdn.microsoft.com/en-us/library/cc310252.aspx) -Eigenschaft enthält. Daniel implementiert diese Änderungen in die Anwendung.
    
  
2. Die Contoso-Anwendung wird für die Weitergabe des ActAs-Tokens an den Back-End-Dienst konfiguriert. Daniel implementiert diese Änderungen in die Anwendung.
    
  
3. Der Contoso-Webdienst wird für die Überprüfung des ActAs-Tokens durch Aufrufen von sts1 konfiguriert. Adam hat sts1 zur Verarbeitung von Delegationsanforderungen aktiviert.
    
  
4. Der Fabrikam-Benutzer Frank greift auf die Contoso-Anwendung zu und erhält Zugriff auf die Back-End-Ressourcen.
    
  

## <a name="federated-authentication"></a>Verbundauthentifizierung
<a name="SP15_SampleDelegation_FederatedAuth"> </a>

Verbundauthentifizierung ermöglicht eine Sicherheitstokendienst (Security Token Service, STS) in einer vertrauenswürdigen Domäne Authentifizierungsinformationen für einen STS in einer anderen vertrauenswürdigen Domäne bereitstellen, wenn es eine Vertrauensstellung zwischen den beiden Domänen ist. Ein Beispiel hierfür ist in Abbildung 2 dargestellt.
  
    
    

**Abbildung 2. Forderungsbasiertes Verbundszenario**

  
    
    

  
    
    
![Forderungsbasierte Verbundauthentifizierung](../images/f0a9be9a-434a-4650-ad57-1fb90b016dd1.gif)
  
    
    

  
    
    

1. Von einem Client in der vertrauenswürdigen Domäne von Fabrikam wird eine Anforderung an eine Anwendung einer vertrauenden Seite innerhalb der vertrauenswürdigen Domäne von Contoso gesendet.
    
  
2. Der Client wird von der vertrauenden Seite an einen STS in der vertrauenswürdigen Domäne von Contoso weitergeleitet. Der Client ist dem STS nicht bekannt.
    
  
3. Der Client wird vom STS von Contoso an einen STS in der vertrauenswürdigen Domäne von Fabrikam weitergeleitet, mit dem die vertrauenswürdige Domäne von Contoso über eine Vertrauensstellung verfügt.
    
  
4. Die Identität des Clients wird durch den STS von Fabrikam überprüft, und anschließend wird ein Sicherheitstoken an den STS von Contoso ausgestellt.
    
  
5. Mithilfe des Tokens von Fabrikam wird vom STS von Contoso ein eigenes Token erstellt, das an die vertrauende Seite gesendet wird.
    
  
6. Die Kundenansprüche werden von der vertrauenden Seite aus dem Sicherheitstoken extrahiert, und es wird eine Authentifizierungsentscheidung gefällt.
    
  
Dieses Szenario beschreibt eine Anmeldung für einen Mitarbeiter der Partner, wenn er Zugriff auf Ressourcen von einem anderen Partnerdomäne versucht. Er muss nur einmal anmelden. Es gibt drei wichtigsten Spieler in einem Verbundszenario: Identitätsanbieter, verbundanbieter und eine vertrauende Seite. WIF bietet APIs, um alle drei Spieler zu erstellen.Abbildung 3 zeigt eine typische Verbundszenario, in dem ein Fabrikam-Mitarbeiter "contoso.com" Ressourcen zugreifen, ohne dass Sie Re-Anmeldung möchte; d. h., der Mitarbeiter von Fabrikam einmaliges Anmelden verwenden möchte. **Abbildung 3. Szenario für forderungsidentitätsdelegierung**

  
    
    

  
    
    
![Forderungsbasiertes Verbundszenario](../images/903d3109-d567-4156-a44f-29793c42ae45.gif)
  
    
    
Die folgenden fiktiven Benutzer sind an diesem Szenario beteiligt:
- Frank: Ein Fabrikam-Mitarbeiter, der auf Contoso-Ressourcen zugreifen möchte.
    
  
- Daniel: Ein Contoso-Anwendungsentwickler, der die notwendigen Änderungen in die Anwendung implementiert.
    
  
- Adam: Der IT-Administrator von Contoso.
    
  
Die folgenden Komponenten sind an diesem Szenario beteiligt:
- web1: Eine Webanwendung zur Bestellung von Teilen, die mit ASP.NET erstellt wurde und die Steuerung des Zugriffs auf die entsprechenden Teile ermöglicht.
    
  
- sts1: Einen STS, der Verbundanbieter bei Contoso.com ist und Ansprüche ausgibt, die von der Anwendung (web1) erwartet werden. Zwischen dem STS und Fabrikam.com besteht eine Vertrauensstellung, und der STS ist so konfiguriert, dass er Mitarbeitern von Fabrikam Zugriff gewährt.
    
  
- sts2: ein Sicherheitstokendienst, dem die Rolle des Identitätsanbieters in Fabrikam.com und bietet einen Endpunkt, der der Mitarbeiter von Fabrikam authentifiziert wird. Es wurde Vertrauensstellung mit Contoso.com festgestellt, sodass Mitarbeiter von Fabrikam "contoso.com"-Ressourcen zugreifen dürfen.
    
  
Wie in Abbildung 3 gezeigt, ist der Ablauf in diesem Szenario:
  
    
    

1. Der Contoso-Administrator Adam konfiguriert die Vertrauensstellung zwischen der Anwendung (vertrauende Seite) und sts1.
    
  
2. Peter, der Administrator von Contoso, konfiguriert die Vertrauensstellung mit sts2 als Identitätsanbieter.
    
  
3. Der Fabrikam-Administrator Frank konfiguriert die Vertrauensstellung mit sts1 als Verbundanbieter und greift dann auf die Anwendung zu.
    
  

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15_SampleDelegation_AdditionalResources"> </a>


-  [Anspruchsbasierte Identität und-Konzepte in SharePoint](claims-based-identity-and-concepts-in-sharepoint.md)
    
  
-  [Anspruchsbasierte Identität - Begriffsdefinitionen](claims-based-identity-term-definitions.md)
    
  

