---
title: "Anspruchsbasierte Identität in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 32b6af2a-72f3-4302-a6af-5f00143cbf67
ms.openlocfilehash: 7df5c259861cb43a36d5c7290a45698614ebfd20
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="claims-based-identity-in-sharepoint"></a><span data-ttu-id="6e4f7-102">Anspruchsbasierte Identität in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6e4f7-102">Claims-based identity in SharePoint</span></span>
<span data-ttu-id="6e4f7-103">Informationen Sie zu den Grundlagen der anspruchsbasierten identitätsarchitektur in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6e4f7-103">Learn about the fundamentals of claims-based identity architecture in SharePoint.</span></span>
## <a name="claims-based-authentication"></a><span data-ttu-id="6e4f7-104">Anspruchsbasierte Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="6e4f7-104">Claims-based authentication</span></span>

<span data-ttu-id="6e4f7-p101">Die anspruchsbasierte Authentifizierung ermöglicht Systemen und Anwendungen die Authentifizierung eines Benutzers, ohne mehr persönliche Informationen (wie Sozialversicherungsnummer und Geburtsdatum) als nötig von ihm zu erfragen. Beispiele für die anspruchsbasierte Authentifizierung sind etwa, wenn jemand behauptet, über 18 Jahre alt zu sein oder der Marketinggruppe eines Unternehmens anzugehören. Ein externes System (vertrauende Seite) muss nur der Authentifizierungsstelle vertrauen, die diese Ansprüche überprüfen kann, um die Authentifizierung des Benutzers für bestimmte Funktionen zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="6e4f7-p101">Claims-based authentication enables systems and applications to authenticate a user without requiring the user to disclose more personal information (such as social security number and date of birth) than necessary. An example of claims-based authentication is someone claiming to be over 18 years old or someone claiming to be in a company's marketing group. An external system (relying party) needs only to trust the authentication authority that can validate those claims to allow the user to be authenticated for specific functions.</span></span>
  
    
    

### <a name="claims-a-set-of-information-about-a-subject"></a><span data-ttu-id="6e4f7-108">Ansprüche: Eine Reihe von Informationen zu einem Thema</span><span class="sxs-lookup"><span data-stu-id="6e4f7-108">Claims: A set of information about a subject</span></span>

<span data-ttu-id="6e4f7-p102">Am einfachsten lassen sich Ansprüche als ein Satz von Informationen über ein bestimmtes Subjekt betrachten. Bei diesem Subjekt handelt es sich meist um eine Person, es könnte jedoch auch eine Anwendung, ein Computer oder etwas anderes sein. Wenn eine Identität im Netzwerk übertragen wird, wird sie durch eine Art Token (auch als Sicherheitstoken bezeichnet) dargestellt.</span><span class="sxs-lookup"><span data-stu-id="6e4f7-p102">The clearest way to think about claims is as a set of information about some subject. This subject is most often a person, but it might also be an application, a computer, or something else. When an identity is transmitted on the network, it is represented by some kind of token (also known as a security token).</span></span> 
  
    
    
<span data-ttu-id="6e4f7-p103">Ein Anspruch ist eine Information zu einem Thema, die bestätigt ein Anspruchsanbieters zu diesem Thema. Es ist eine Anweisung zu einem Thema (beispielsweise Name), die erfolgt nach einem Betreff über sich selbst oder einer anderen Thema. Sie können eine Forderung als Identitätsinformationen, wie e-Mail-Adresse, Name, Alter oder die Mitgliedschaft in der sales-Rolle auszudrücken vorstellen. Es ist ein eindeutiger Bezeichner, der einen bestimmten Benutzer, eine Anwendung, Computer oder sonstige Entität darstellt. Es ermöglicht den Zugriff auf mehrere Ressourcen, wie Anwendungen und Netzwerkressourcen, ohne Anmeldeinformationen mehrfach eingeben dieser Entität. Darüber hinaus können Ressourcen, um Anfragen aus einer Entität zu überprüfen. Mehrere Ansprüche, dass eine Anwendung empfängt, wissen Sie mehr über Ihre Benutzer.</span><span class="sxs-lookup"><span data-stu-id="6e4f7-p103">A claim is a piece of information about a subject that a claims provider asserts about that subject. It is a statement about a subject (for example, a name) that is made by a subject about itself or another subject. You can think of a claim as a bit of identity information, such as email address, name, age, or membership in the sales role. It is a unique identifier that represents a specific user, application, computer, or other entity. It enables that entity to gain access to multiple resources, such as applications and network resources, without entering credentials multiple times. It also enables resources to validate requests from an entity. The more claims that an application receives, the more you know about your user.</span></span>
  
    
    
<span data-ttu-id="6e4f7-119">Ein Anspruch wird mit einem oder mehreren Werte versehen und anschließend in Sicherheitstoken gepackt, die von einem Sicherheitstokendienst (Security Token Service, STS) ausgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="6e4f7-119">A claim is given one or more values and then packaged in security tokens that are issued by a security token service (STS).</span></span>
  
    
    
<span data-ttu-id="6e4f7-p104">Das Wort Anspruch wird aufgrund der Übermittlungsmethode anstelle des BegriffsAttribute verwendet, der mehr im Kontext der Unternehmensverzeichnisse gängig ist. In diesem Modell werden Benutzerattribute nicht von einer Anwendung in einem Verzeichnis nachgeschlagen. Vielmehr übermittelt der Benutzer Ansprüche an die Anwendung. Jeder Anspruch wird von einem Aussteller erhoben, und Sie vertrauen dem Anspruch nur so weit, wie Sie dem Aussteller vertrauen. Beispielsweise vertrauen Sie einem Anspruch, der vom Domänencontroller des Unternehmens gestellt wird, mehr als einem Anspruch des Benutzers. Die Anspruchs-API verfügt über eine Ausstellereigenschaft, über die Sie herausfinden können, wer den Anspruch gestellt hat.</span><span class="sxs-lookup"><span data-stu-id="6e4f7-p104">The word claim is used, instead of the wordattributes that is more commonly used in the enterprise directory world, because of the delivery method. In this model, your application does not look up user attributes in a directory. Instead, the user delivers claims to your application. Each claim is made by an issuer, and you trust the claim only as much as you trust the issuer. For example, you trust a claim made by your company's domain controller more than a claim made by the user. The claims API has an issuer property that enables you to find out who issued the claim.</span></span>
  
    
    

### <a name="tokens-information-about-an-identity"></a><span data-ttu-id="6e4f7-126">Token: Informationen über eine Identität</span><span class="sxs-lookup"><span data-stu-id="6e4f7-126">Tokens: Information about an identity</span></span>

<span data-ttu-id="6e4f7-p105">Ein Token ist ein Satz von Bytes, der Informationen über eine Identität darstellt. Diese Informationen bestehen aus einem oder mehreren Ansprüchen, die jeweils Informationen über das Subjekt enthalten, für das dieses Token gilt. Die Ansprüche in einem Token enthalten üblicherweise Informationen wie den Namen des Benutzers, der es vorweist. Darüber hinaus können unterschiedliche andere Informationen enthalten sein - Ansprüche sind nicht beschränkt auf den Namen eines Subjekts und müssen diesen auch nicht enthalten. Wie das Wort Ansprüche nahe legt, akzeptiert eine Anwendung, die ein Token empfängt, nicht automatisch die darin enthaltenen Informationen. Stattdessen wird ein empfangenes Token in der Regel auf irgendeine Art überprüft, bevor eine Anwendung von darin enthaltenen Ansprüchen Gebrauch macht.</span><span class="sxs-lookup"><span data-stu-id="6e4f7-p105">A token is a set of bytes that expresses information about an identity. This information consists of one or more claims, each of which contains some information about the subject to which this token applies. The claims in a token commonly contain information such as the name of the user who presents it. They can also contain many sorts of other information—claims are not limited to, and do not even need to include, a subject's name. And, as the word claims suggests, an application that receives a token does not automatically accept the information that it contains. Instead, a received token is usually validated in some way before an application uses any claims that it contains.</span></span>
  
    
    
<span data-ttu-id="6e4f7-p106">Das Schlüsselkonzept liegt darin, dass ein Anspruch nicht nur ein eindeutiger Bezeichner ist, der die Ressource, die Anwendung oder den Benutzer identifiziert. Vielmehr wird die Ressource, die Anwendung oder der Benutzer durch einen Satz von Ansprüchen (d. h. Werten) beschrieben. Die Ansprüche werden auch zur Autorisierung des Zugriffs verwendet.</span><span class="sxs-lookup"><span data-stu-id="6e4f7-p106">The key concept is that a claim is not just a unique identifier that identifies the resource, application, or user. It is a set of claims (that is, values) that is used to describe the resource, application, or user. The claims are also used to authorize access.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="6e4f7-136">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="6e4f7-136">Additional resources</span></span>
<span data-ttu-id="6e4f7-137"><a name="SP15_RoleInheritance_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="6e4f7-137"><a name="SP15_RoleInheritance_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="6e4f7-138">Authentifizierung, Autorisierung und Sicherheit in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6e4f7-138">Authentication, authorization, and security in SharePoint</span></span>](authentication-authorization-and-security-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6e4f7-139">Eingehende Ansprüche: Anmelden bei SharePoint</span><span class="sxs-lookup"><span data-stu-id="6e4f7-139">Incoming claims: Signing into SharePoint</span></span>](incoming-claims-signing-into-sharepoint.md)
    
  
-  [<span data-ttu-id="6e4f7-140">Anspruchsanbieter in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6e4f7-140">Claims provider in SharePoint</span></span>](claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6e4f7-141">Vorgehensweise: Erstellen ein anspruchsanbieters in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6e4f7-141">How to: Create a claims provider in SharePoint</span></span>](how-to-create-a-claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="6e4f7-142">Vorgehensweise: POST eines anspruchsanbieters in SharePoint</span><span class="sxs-lookup"><span data-stu-id="6e4f7-142">How to: Deploy a claims provider in SharePoint</span></span>](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

