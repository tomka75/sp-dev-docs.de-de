---
title: Arbeiten mit Benutzerprofilen in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7437a7a8-85cb-4233-84af-1eec30dd54b2
ms.openlocfilehash: ba2c4023a1a164ca4313d3adc10ce0a0abbbfa85
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="work-with-user-profiles-in-sharepoint"></a>Arbeiten mit Benutzerprofilen in SharePoint
In diesem Artikel werden gängige Programmieraufgaben für die Arbeit mit Benutzerprofilen in SharePoint beschrieben.
## <a name="apis-for-working-with-user-profiles-in-sharepoint"></a>APIs für die Arbeit mit Benutzerprofilen in SharePoint
<a name="bkmk_APIversions"> </a>

Benutzerprofile und Benutzerprofileigenschaften enthalten Informationen zu SharePoint-Benutzern. SharePoint stellt die folgenden APIs zur programmgesteuerten Arbeit mit Benutzerprofilen bereit:
  
    
    

- Clientobjektmodelle für verwalteten Code
    
  - .NET-Clientobjektmodell
    
  
  - Silverlight-Clientobjektmodell
    
  
  - Mobiles Clientobjektmodell
    
  
- JavaScript-Objektmodell
    
  
- REST (Representational State Transfer)-Dienst
    
  
- Serverobjektmodell
    
  
Verwenden Sie als bewährtes Verfahren bei der SharePoint-Entwicklung, wenn immer möglich, Client-APIs. Client-APIs enthalten das .NET-Clientmodell, das JavaScript-Objektmodell und den REST-Dienst. Weitere Informationen zu APIs finden Sie unter SharePoint. Informationen zur Verwendungsweise finden Sie unter  [Auswählen des richtigen API-Satzes in SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
> [!NOTE] 
> Nicht alle Funktionen in der Assembly **Microsoft.Office.Server.UserProfiles** lassen sich über Client-APIs nutzen. Zur Erstellung oder Anpassung von Benutzerprofilen beispielsweise müssen Sie das Serverobjektmodell verwenden, da Client-APIs nur schreibgeschützten Zugriff auf die Profile haben. (Ausgenommen hiervon sind lediglich Benutzerprofilbilder.) Auch auf manche Namespaces ist kein clientseitiger Zugriff möglich. Das gilt beispielsweise für [Microsoft.Office.Server.Audience]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Audience.aspx)), [Microsoft.Office.Server.ReputationModel]((https://msdn.microsoft.com/library/Microsoft.Office.Server.ReputationModel.aspx)) und [Microsoft.Office.Server.SocialData]((https://msdn.microsoft.com/library/Microsoft.Office.Server.SocialData.aspx)). Eine Liste der in Client-APIs unterstützten Funktionen finden Sie unter [Microsoft.SharePoint.Client.Social]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx)) und [Microsoft.SharePoint.Client.UserProfiles]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx)).
  
    
    

Jede API schließt ein verwaltetes Objekt mit ein, das Sie zum Ausführen von wichtigen profilbezogenen Aufgaben verwenden.
  
> [!NOTE] 
> Die Silverlight- und mobilen Clientobjektmodelle sind in Tabelle 1 oder Tabelle 2 nicht enthalten, da sie dieselben Kernfunktionen wie das .NET-Clientobjektmodell bereitstellen und dieselben Signaturen verwenden. Das Silverlight-Clientobjektmodell ist in Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll definiert und das mobile Clientobjektmodell in Microsoft.SharePoint.Client.UserProfiles.Phone.dll. 
  
    
    


**Tabelle 1: SharePoint-APIs für programmgesteuertes Arbeiten mit Benutzerprofilen**

|**API**|**Schlüsselobjekt**|
|:-----|:-----|
|.NET-Clientobjektmodell  <br/> Weitere Informationen:  [Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)|Manager-Objekt:            [PeopleManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.aspx)) <br/> Primärer Namespace:            [Microsoft.SharePoint.Client.UserProfiles]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx)) <br/> Sonstige Schlüsselobjekte:            [PersonProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx)) , [ProfileLoader]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.ProfileLoader.aspx)) , [UserProfile]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx)) <br/> Klassenbibliothek:           Microsoft.SharePoint.Client.UserProfiles.dll |
|JavaScript-Objektmodell  <br/> Weitere Informationen:  [Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)|Manager-Objekt:            [PeopleManager]((http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx)) <br/> Primärer Namespace:            [SP.UserProfiles]((http://msdn.microsoft.com/library/8c1fcceb-cd9a-b25c-32f4-1cfb0578278c%28Office.15%29.aspx)) <br/> Sonstige Schlüsselobjekte:            [PersonProperties]((http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx)),  [ProfileLoader]((http://msdn.microsoft.com/library/c8dd9919-66a9-fffc-1100-14472d2ec2cb%28Office.15%29.aspx)),  [UserProfile]((http://msdn.microsoft.com/library/f8c4a219-fbaa-2e50-1bd5-fdc80051b33d%28Office.15%29.aspx)) <br/> Klassenbibliothek:           SP.UserProfiles.js |
|REST-Dienst  <br/> Siehe:  [Benutzerprofile - REST-API-Referenz]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx))|Manager-Ressource:            [PeopleManager]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_PeopleManager) <br/> Endpunkt-URI:            `http://<siteUri>/_api/SP.UserProfiles.PeopleManager` <br/> Primärer Namespace:           **SP.UserProfiles** <br/> Sonstige Schlüsselobjekte:            [PersonProperties]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_PersonProperties),  [ProfileLoader]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_ProfileLoader),  [UserProfile]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_UserProfile)|
|Serverobjektmodell  <br/> Weitere Informationen:  [Vorgehensweise: Arbeiten mit Benutzerprofilen und Organisationsprofilen mithilfe des Serverobjektmodells in SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)|Manager-Objekte:            [UserProfileManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.aspx)) , [PeopleManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx)) <br/> Primärer Namespace:            [Microsoft.Office.Server.UserProfiles]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.aspx)) <br/> Sonstige Schlüsselobjekte:            [UserProfile]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx)) , [CorePropertyManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CorePropertyManager.aspx)) , [ProfilePropertyManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfilePropertyManager.aspx)) , [ProfileSubtypeManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeManager.aspx)) , [ProfileSubtypePropertyManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypePropertyManager.aspx)) , [ProfileTypePropertyManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypePropertyManager.aspx)) <br/> Klassenbibliothek:           Microsoft.Office.Server.UserProfiles.dll |
   

## <a name="common-programming-tasks-for-working-with-user-profiles-in-sharepoint"></a>Allgemeine Programmierungsaufgaben für das Arbeiten mit Benutzerprofilen in SharePoint
<a name="bkmk_CommonTasks"> </a>

Tabelle 2 zeigt allgemeine Programmierungsaufgaben für das Arbeiten mit Benutzerprofilen sowie die Elemente, die Sie zur Ausführung verwenden. Die Elemente stammen aus dem .NET-Clientobjektmodell (CSOM), dem JavaScript-Objektmodell (JSOM), dem REST-Dienst und dem Serverobjektmodell (SSOM).
  
    
    

**Tabelle 2. API für allgemeine Programmierungsaufgaben für das Arbeiten mit Benutzerprofilen**


|**Aufgabe**|**Elemente**|
|:-----|:-----|
|Erstellen einer Instanz eines Manager-Objekts im Kontext des aktuellen Benutzers |CSOM:  [PeopleManager]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.aspx)) <br/> JSOM: [PeopleManager]((http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx)) <br/> REST: **GET** [`http://<siteUri>/_api/SP.UserProfiles.PeopleManager`]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_PeopleManager)<br/> SSOM: [UserProfileManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.aspx)) (überladen) oder [PeopleManager]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx))|
|Ändern des aktuellen Benutzerprofilbilds |CSOM:  [SetMyProfilePicture]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.SetMyProfilePicture.aspx)) <br/> JSOM: [setMyProfilePicture]((http://msdn.microsoft.com/library/a4f8d745-f211-e750-4fd0-047091804683%28Office.15%29.aspx)) <br/> REST: **POST** [`http://<siteUri>/_api/SP.UserProfiles.PeopleManager/SetMyProfilePicture`]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_PeopleManagerSetMyProfilePicture) mit Übergabe des Parameters _picture_ im Anforderungstext <br/> SSOM: [UserProfile]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx)) [PropertyConstants.PictureUrl].Value oder [SetMyProfilePicture]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.SetMyProfilePicture.aspx))|
|Abrufen der aktuellen Benutzereigenschaften |CSOM:  [GetMyProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx)) <br/> JSOM: [getMyProperties]((http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx)) <br/> REST: **GET** [`http://<siteUri>/_api/SP.UserProfiles.PeopleManager/GetMyProperties`]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_PeopleManagerGetMyProperties) (oder Abruf grundlegender Benutzereigenschaften aus `/_api/social.feed/my` oder `/_api/social.following/my`)  <br/> SSOM: [GetUserProfile]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.GetUserProfile.aspx))|
|Abrufen bestimmter Benutzereigenschaften |CSOM:  [GetPropertiesFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx)) <br/> JSOM: [getPropertiesFor]((http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx)) <br/> REST: **GET** [`http://<siteUri>/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)?@v='domain\\user'`]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_PeopleManagerGetPropertiesFor) <br/> SSOM: [GetUserProfile]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.GetUserProfile.aspx)) (überladen) oder [GetPropertiesFor]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.GetPropertiesFor.aspx))|
|Abrufen der Benutzerprofileigenschaften eines bestimmten Benutzers |CSOM:  [GetUserProfilePropertiesFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx)) <br/> JSOM: [getUserProfilePropertiesFor]((http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx)) <br/> REST: Nicht implementiert. Rufen Sie [GetPropertiesFor]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_PeopleManagerGetPropertiesFor) auf, und rufen Sie anschließend die Benutzerprofileigenschaften aus der Eigenschaft **UserProfileProperties** des zurückgegebenen Objekts **PersonProperties** ab. <br/> SSOM: [GetEnumerator]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.GetEnumerator.aspx))|
|Abrufen einer bestimmten Benutzerprofileigenschaft eines Benutzers |CSOM:  [GetUserProfilePropertyFor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx)) <br/> JSOM: [getUserProfilePropertyFor]((http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx)) <br/> REST: **GET** [`http://<siteUri>/_api/SP.UserProfiles.PeopleManager/GetUserProfilePropertyFor(accountName=@v,propertyName='PreferredName')?@v='domain\\user'`]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_PeopleManagerGetUserProfilePropertyFor) <br/> SSOM: [UserProfile]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx)) (überladen) unter Angabe des Eigenschaftennamens im Indexer|
|Abrufen eines Benutzerprofils |CSOM:  [GetUserProfile]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.ProfileLoader.GetUserProfile.aspx)) (gibt nur das [clientseitige Benutzerprofil](work-with-user-profiles-in-sharepoint.md#bkmk_NewUserObjects)für den aktuellen Benutzer zurück) <br/> JSOM: [getUserProfile]((http://msdn.microsoft.com/library/8e30e811-5da1-b6d0-a8b5-befea9b22496%28Office.15%29.aspx)) (Gibt nur das [clientseitige Benutzerprofil](work-with-user-profiles-in-sharepoint.md#bkmk_NewUserObjects) des aktuellen Benutzers zurück.) <br/> REST: **POST** [`http://<siteUri>/_api/SP.UserProfiles.ProfileLoader.GetProfileLoader/GetUserProfile`]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx).md#bk_ProfileLoaderGetProfileLoader) (Gibt nur das [clientseitige Benutzerprofil](work-with-user-profiles-in-sharepoint.md#bkmk_NewUserObjects) des aktuellen Benutzers zurück.) <br/> SSOM: [GetUserProfile]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.GetUserProfile.aspx)) (überladen)|
|Ermitteln, ob ein Benutzerkonto vorhanden ist |CSOM: nicht implementiert  <br/> JSOM: nicht implementiert  <br/> REST: nicht implementiert  <br/> SSOM:  [UserExists]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.UserExists.aspx))|
|Erstellen oder Ändern von Benutzerprofilen und Benutzerprofileigenschaften und -attributen  <br/> (Client-APIs können das Profilbild ändern. Siehe auch die Aufgabe "Ändern des Benutzerprofilbilds" in dieser Tabelle.) |CSOM: nicht implementiert  <br/> JSOM: nicht implementiert  <br/> REST: nicht implementiert  <br/> SSOM: mehrere??? (Siehe [How to: Work with user profiles and organization profiles by using the server object model in SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)|
|Löschen eines Benutzerprofils |CSOM: nicht implementiert  <br/> JSOM: nicht implementiert  <br/> REST: nicht implementiert  <br/> SSOM:  [RemoveProfile]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.RemoveProfile.aspx)) oder [RemoveUserProfile]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.RemoveUserProfile.aspx)) (überladen)|
|Bereitstellen einer persönlichen Benutzerwebsite |CSOM:  [CreatePersonalSiteEnque]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.CreatePersonalSiteEnque.aspx)) (überladen) <br/> JSOM: [createPersonalSiteEnque]((http://msdn.microsoft.com/library/f4bcb82d-4048-0b29-9bc6-ce70ead49988%28Office.15%29.aspx)) (überladen) <br/> REST: **POST** [`http://<siteUri>/_api/SP.UserProfiles.ProfileLoader.GetProfileLoader/GetUserProfile/CreatePersonalSiteEnqueue`]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)#bk_UserProfileCreatePersonalSiteEnque) <br/> SSOM: [CreatePersonalSite()]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.CreatePersonalSite.aspx)) (überladen)|
|Bereitstellen von mindestens einer persönlichen Benutzerwebsite  <br/> Nur verfügbar für Meine Website Hostadministratoren in SharePoint Online |CSOM:  [CreatePersonalSiteEnqueueBulk](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md#bk_CreatePersonalSiteEnqueueBulk) <br/> JSOM: **createPersonalSiteEnqueueBulk** <br/> REST: **POST** [`https://<domain>-admin.sharepoint.com/_api/SP.UserProfiles.ProfileLoader.GetProfileLoader/CreatePersonalSiteEnqueueBulk`]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx).md#bk_ProfileLoaderCreatePersonalSiteEnqueueBulk) mit Übergabe eines Zeichenfolgenarrays von E-Mail-Adressen im Parameter _emailIDs_ (maximal 200 Zeichen) im Anforderungstext (Beispiel: `{'emailIDs':['usera@contoso.onmicrosoft.com','userb@contoso.onmicrosoft.com']}`)  <br/> SSOM: **CreatePersonalSiteEnqueueBulk**|
   

## <a name="new-objects-for-users-and-user-properties-in-sharepoint"></a>Neue Objekte für Benutzer und Benutzereigenschaften in SharePoint
<a name="bkmk_NewUserObjects"> </a>

SharePoint umfasst die folgenden neuen Objekte, die Benutzer und Benutzereigenschaften darstellen:
  
    
    

- Das Objekt [SocialActor]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx)) und das Objekt [SocialActorInfo]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx)) stellen Benutzer (sowie Dokumente, Websites und Aufgaben) für Feed- und Folgeaktivitäten dar.
    
  
- Ein neues clientseitiges  [UserProfile]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx)) -Objekt stellt Methoden bereit, mit denen Sie eine persönliche Website für den aktuellen Benutzer erstellen können. Es enthält aber nicht alle Benutzereigenschaften, die das serverseitige [UserProfile]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx)) -Objekt enthält.
    
  
- Das  [PersonProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx)) -Objekt enthält allgemeine Benutzereigenschaften und die [UserProfileProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx)) -Eigenschaft enthält Benutzerprofileigenschaften. [PersonProperties]((https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx)) ist die primäre API für den Zugriff auf Benutzereigenschaften aus dem clientseitigen Code.
    
> [!NOTE] 
> Entsprechende Versionen im Serverobjektmodell sind das Objekt [SPSocialActor]((https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx)) und das Objekt [PersonProperties]((https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PersonProperties.aspx)).
  
    
    


## <a name="see-also"></a>Siehe auch
<a name="bkmk_AdditionalResources"> </a>


-  [Soziale Funktionen und Zusammenarbeit in SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Erste Schritte bei der Entwicklung mit thematischen Features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des .NET-Clientobjektmodells in SharePoint](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)
    
  
-  [Vorgehensweise: Abrufen von Benutzerprofileigenschaften mithilfe des JavaScript-Objektmodells in SharePoint](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)
    
  
-  [Benutzerprofile - REST-API-Referenz]((http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx))
    
  
-  [Vorgehensweise: Arbeiten mit Benutzerprofilen und Organisationsprofilen mithilfe des Serverobjektmodells in SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)
    
  
-  [Folgen von Personen in SharePoint](follow-people-in-sharepoint.md)
    
  
