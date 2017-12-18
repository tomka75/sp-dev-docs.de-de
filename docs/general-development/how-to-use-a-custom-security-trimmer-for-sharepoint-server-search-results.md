---
title: "Verwenden eines benutzerdefinierten Security Trimmers für Suchergebnisse für SharePoint Server"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e1a8664e-fb43-45c2-83aa-9635fe1efc99
ms.openlocfilehash: f661cf012664960bc703e9bebed1cb9e0d00c214
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="use-a-custom-security-trimmer-for-sharepoint-server-search-results"></a>Verwenden eines benutzerdefinierten Security Trimmers für Suchergebnisse für SharePoint Server

Dieser Artikel führt Sie durch die Schritte zum Implementieren, Erstellen, Bereitstellen und Registrieren eines benutzerdefinierten Security Trimmers für die Suche in SharePoint mithilfe von Microsoft Visual Studio 2010.

Die Suche in SharePoint führt eine Sicherheitskürzung von Suchergebnissen zur Abfragezeit durch. Es gibt jedoch Szenarios, in denen Sie eine benutzerdefinierte Sicherheitskürzung durchführen möchten. Die Suche in SharePoint bietet über die folgenden Schnittstellen im [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx)-Namespace Unterstützung für diese Szenarios: [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) , [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx)  und [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) (veraltet).
  
    
    

Es gibt zwei Arten von benutzerdefinierten Einschränkung aus Sicherheitsgründen: Trimming vor und nach dem Zuschneiden. Vor dem Zuschneiden bezieht sich auf vor der Abfrage Evaluierungshandbuch und exemplarische Vorgehensweisen, in dem die Abfrage umgeschrieben wird Sicherheitsinformationen hinzufügen, bevor die Abfrage mit dem Suchindex abgeglichen wird. Nach der Einschränkung aus Sicherheitsgründen bezieht sich auf die nach der Abfrage Evaluierungshandbuch und exemplarische Vorgehensweisen, in denen die Suchergebnisse gelöscht werden, bevor sie an den Benutzer zurückgegeben werden. Wir empfehlen die Verwendung von vor Einschränkung aus Sicherheitsgründen für Leistung und allgemeine Korrektheit; nach der Einschränkung aus Sicherheitsgründen wird verhindert, dass Informationslecks für Einschränkung Daten und Anzahl der Zugriffe Instanzen.
  
    
    

Der Security Trimmer-Registrierungsprozess können Sie für den benutzerdefinierten Security Trimmer Konfigurationseigenschaften angeben.
## <a name="overview"></a>Übersicht

Benutzerdefinierte Security Trimming in Suche in SharePoint besteht aus zwei Schnittstellen, die verwendet werden können, um vor dem Zuschneiden oder nach der Trimming der Suchergebnisse auszuführen. Diese Vorgehensweise konzentriert sich auf beide Schnittstellen, beschreibt die erforderlichen Schritte zum Erstellen und registrieren Ihre eigene Security Trimmer ab.
  
    
    

## <a name="prerequisites"></a>Voraussetzungen
<a name="PreReq"> </a>

Um diese Vorgehensweise ausführen zu können, müssen Sie Folgendes in Ihrer Entwicklungsumgebung installiert sein:
  
    
    

- Suche in Microsoft SharePoint
    
  
- Microsoft Visual Studio 2010 oder ähnliche Microsoft .NET Framework - kompatibles Entwicklungstool
    
  

## <a name="set-up-a-custom-security-trimmer-project"></a>Einrichten eines benutzerdefinierten Security Trimmer-Projekts
<a name="SetUp"> </a>

In diesem Schritt werden Sie erstellen des Projekts für den benutzerdefinierten Security Trimmer, und fügen Sie die erforderlichen Verweise auf das Projekt.
  
    
    

### <a name="to-create-the-project-for-a-custom-security-trimmer"></a>So erstellen Sie das Projekt für einen benutzerdefinierten Security trimmer


1. Öffnen Sie Visual Studio, und wählen Sie **Datei**, **neu**, **Projekt**.
    
  
2. Wählen Sie in **Projekttypen** unter **c#** **SharePoint** aus.
    
  
3. Wählen Sie unter **Vorlagen** **Leeres SharePoint-Projekt**. Klicken Sie im Feld **Name** Geben Sie **CustomSecurityTrimmerSample**, und wählen Sie dann auf die Schaltfläche **OK**.
    
  
4. Klicken Sie im **Assistenten zum Anpassen von SharePoint**-Wählen Sie **als Farmlösung bereitstellen**, und wählen Sie dann auf **Fertig stellen**.
    
  

### <a name="to-add-references-to-the-custom-security-trimmer-project"></a>So fügen Sie dem Projekt für den benutzerdefinierten Security Trimmer Verweise hinzu


1. Wählen Sie im **Projekt** auf **Verweis hinzufügen**.
    
  
2. Klicken Sie auf der Registerkarte **.NET** Wählen Sie die Verweise mit den folgenden Komponentennamen aus, und wählen Sie dann auf die Schaltfläche **OK**:
    
  - **Microsoft Search-Komponente**
    
    Auf der Registerkarte **.NET** mit den Namen der Komponente **Microsoft Search-Komponente** sollte zwei Einträge angezeigt werden. Wählen Sie den Eintrag, in die Spalte Pfad \\ISAPI\\Microsoft.Office.Server.Search.dll ist. Wenn dieser Eintrag auf der Registerkarte **.NET** im Dialogfeld **Verweise hinzufügen** nicht vorhanden ist, müssen Sie den Verweis von der Registerkarte **Durchsuchen** mithilfe des Pfads zu der Microsoft.Office.Server.Search.dll hinzufügen.
    
  
  - **Microsoft.IdentityModel**
    
    Wenn **Microsoft.IdentityModel** auf der Registerkarte **.NET** nicht aufgeführt ist, müssen Sie den Verweis auf die Microsoft.IdentityModel.dll über die Registerkarte **Durchsuchen** unter Verwendung des folgenden Pfads hinzufügen:
    
     `%ProgramFiles%\\Reference Assemblies\\Microsoft\\Windows Identity Foundation\\v4.0.`
    
  

## <a name="create-a-custom-security-pre-trimmer"></a>Erstellen eines vor dem benutzerdefinierten Security trimmers
<a name="CreatePreTrimmer"> </a>


### <a name="to-create-the-class-file-for-the-security-pre-trimmer"></a>Die Klassendatei für den Security Trimmer vor dem Erstellen


1. Wählen Sie im Menü **PROJEKT** die Option **Neues Element hinzufügen** aus.
    
  
2. Klicken Sie unter **Visual C#-Elemente** in **Installierte Vorlagen** Wählen Sie **Code** aus, und wählen Sie dann auf **Klasse**.
    
  
3. Geben Sie **CustomSecurityPreTrimmer.cs** ein, und wählen Sie dann auf **Hinzufügen**.
    
  

### <a name="writing-the-custom-security-pre-trimmer-code"></a>Schreiben den benutzerdefinierten Security Trimmer Pre-code

Ihre benutzerdefinierten Security Trimmer muss die **ISecurityTrimmerPre** -Schnittstelle implementieren. Im folgenden Codebeispiel wird eine einfache Implementierung dieser Schnittstelle.
  
    
    

### <a name="to-modify-the-default-code-in-customsecuritypretrimmer"></a>So ändern Sie den Standardcode in CustomSecurityPreTrimmer


1. Fügen Sie am Anfang der Klasse die folgenden **using**-Direktiven hinzu:
    
```cs
  
using System;
using System.Collections;
using System.Collections.Generic;
using System.Collections.Specialized;
using System.Security.Principal;
using Microsoft.IdentityModel.Claims;
using Microsoft.Office.Server.Search.Query;
using Microsoft.Office.Server.Search.Administration;

```

2. Geben Sie an, dass die **CustomSecurityPreTrimmer** -Klasse die [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) -Schnittstelle in der Klassendeklaration implementiert, wie im folgenden Code dargestellt.
    
```cs
  
public class CustomSecurityPreTrimmer : ISecurityTrimmerPre
```


### <a name="to-implement-the-isecuritytrimmerpre-interface-methods"></a>Implementieren die ISecurityTrimmerPre-Schnittstellenmethoden


1. Fügen Sie den folgenden Code hinzu, um die Methode [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) zu deklarieren:
    
```cs
  public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{

}
```


    The basic version of this sample does not include any code in the **Initialize** method.
    
  
2. Fügen Sie den folgenden Code hinzu, um die Methode [AddAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) zu deklarieren:
    
```cs
  
public IEnumerable<Tuple<Claim, bool>> AddAccess(
                IDictionary<string, object> sessionProperties, IIdentity passedUserIdentity)
{
//AddAccess method implementation, see steps 3-5.
}
```

3. Im ersten Teil des Codes für die Methode **AddAccess** können wir dem Wert _passedUserIdentity_ die Identität des Benutzers entnehmen.
    
```cs
  
if (passedUserIdentity == null)
{
   throw new ArgumentException("AddAccess method is called with invalid user identity
   parameter", "passedUserIdentity");
}
            
   String strUser = null;
   var claimsIdentity = (IClaimsIdentity)passedUserIdentity;
   if (claimsIdentity != null)
   {
      foreach (var claim in claimsIdentity.Claims)
      {
         if (claim == null) 
         {
            continue;
         }
         
         // strUser is "domain\\\\user" format when web app is in Claims Windows Mode
         if (SPClaimTypes.Equals(claim.ClaimType, SPClaimTypes.UserLogonName))
         {
            strUser = claim.Value;
            break;
         }

         // strUser2 is "S-1-5-21-2127521184-1604012920-1887927527-66602" when web app is   
            in Legacy Windows Mode
         // In this case we need to convert it into NT user format.
         if (SPClaimTypes.Equals(claim.ClaimType, ClaimTypes.PrimarySid))
         {
            strUser = claim.Value;
            SecurityIdentifier sid = new SecurityIdentifier(strUser);
            strUser = sid.Translate(typeof(NTAccount)).Value;
            break;
         }
      }
}            

```

4. Erstellen Sie eine Liste, befüllen Sie die Liste mit Ansprüchen, und geben Sie sie anschließend zurück, wie im folgenden Codebeispiel demonstriert:
    
```cs
  
var claims = new LinkedList<Tuple<Claim, bool>>();
if (!string.IsNullOrEmpty(strUser))
   {
      var groupMembership = GetMembership(strUser);
      if (!string.IsNullOrEmpty(groupMembership))
      {
         var groups = groupMembership.Split(new[] {';'},
         StringSplitOptions.RemoveEmptyEntries);
         foreach (var group in groups)
         {
            claims.AddLast(new Tuple<Claim, bool>(
            new Claim("http://schemas.happy.bdc.microsoft.com/claims/acl", group), false));
         }
      }
   }
   return claims;
}

```


    The **GetMembership** method contains the custom logic of your trimmer.
    
  

## <a name="create-a-custom-security-post-trimmer"></a>Erstellen eines benutzerdefinierten Security Post-Trimmers
<a name="CreatePostTrimmer"> </a>


### <a name="to-create-the-class-file-for-the-security-post-trimmer"></a>Erstellen Sie die Klassendatei für den nach der Security trimmer


1. Wählen Sie im Menü **PROJEKT** die Option **Neues Element hinzufügen** aus.
    
  
2. Klicken Sie unter **Visual C#-Elemente** in **Installierte Vorlagen** Wählen Sie **Code** aus, und wählen Sie dann **Klasse**.
    
  
3. Geben Sie CustomSecurityPostTrimmer.csein, und wählen Sie dann auf **Hinzufügen**.
    
  

### <a name="writing-the-custom-security-post-trimmer-code"></a>Den benutzerdefinierten Security Trimmer nach der Code zu schreiben

Ihre benutzerdefinierten Security Trimmer muss die **ISecurityTrimmerPost** -Schnittstelle implementieren. Das Codebeispiel in diesem Abschnitt wird eine einfache Implementierung dieser Schnittstelle.
  
    
    

### <a name="to-modify-the-default-code-in-customsecurityposttrimmer"></a>So ändern Sie den Standardcode in CustomSecurityPostTrimmer


1. Fügen Sie am Anfang der Klasse die folgenden **using**-Direktiven hinzu:
    
```cs
  
using System;
using System.Collections;
using System.Collections.Generic;
using System.Collections.Specialized;
using System.Security.Principal;
using Microsoft.IdentityModel.Claims;
using Microsoft.Office.Server.Search.Query;
using Microsoft.Office.Server.Search.Administration;

```

2. Festlegen Sie, dass die **CustomSecurityPostTrimmer** -Klasse die [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) -Schnittstelle in der Klassendeklaration wie folgt implementiert:
    
```cs
  
public class CustomSecurityPostTrimmer : ISecurityTrimmerPost
```


### <a name="to-implement-the-isecuritytrimmerpost-interface-methods"></a>Implementieren die ISecurityTrimmerPost-Schnittstellenmethoden


1. Fügen Sie den folgenden Code hinzu, um die Methode [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) zu deklarieren:
    
```cs
  public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{

}
```


    The basic version of this sample does not include any code in the Initialize method.
    
  
2. Fügen Sie den folgenden Code hinzu, um die Methode [CheckAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.CheckAccess.aspx) zu deklarieren:
    
```cs
  
public BitArray CheckAccess(IList<string> documentCrawlUrls, IList<string> documentAcls, IDictionary<string, object> sessionProperties, IIdentity passedUserIdentity)
{
//CheckAccess method implementation, see steps 3-5.
}
```

3. Für den ersten Teil der Implementierung der **CheckAccess** -Methode deklarieren und Initialisieren einer Variablen **BitArray** zum Speichern der Ergebnisse der Zugriffsüberprüfung für jede URL in der Auflistung **documentCrawlUrls** und Abrufen des Benutzers, der die Suchabfrage übermittelt hat, wie im folgenden Code dargestellt.
    
```cs
  
if (documentCrawlUrls == null)
{
   throw new ArgumentException("CheckAccess method is called with invalid URL list",
   "documentCrawlUrls");
}
if (documentAcls == null)
{
   throw new ArgumentException("CheckAccess method is called with invalid documentAcls   
   list", "documentAcls");
}
if (passedUserIdentity == null)
{
   throw new ArgumentException("CheckAccess method is called with invalid user identity
   parameter", "passedUserIdentity");
}

```

4. Durchlaufen Sie jede Durchforstungs-URL in der Auflistung, und führen Sie die Zugriffsüberprüfung, um festzustellen, ob der Benutzer, übermittelt hat, dass die Abfrage der Durchforstungs-URLs zugreifen kann, Inhaltselemente verknüpft ist, wie im folgenden Code dargestellt. 
    
```cs
  
// Initialize the bit array with TRUE value which means all results are visible by default.
var urlStatusArray = new BitArray(documentCrawlUrls.Count, true);
var claimsIdentity = (IClaimsIdentity)passedUserIdentity;
if (claimsIdentity != null)
{
   var userGroups = GetGroupList(claimsIdentity.Claims);
   var numberDocs = documentCrawlUrls.Count;
   for (var i = 0; i < numberDocs; ++i)
   {
      if (!string.IsNullOrEmpty(documentAcls[i]))
      {
         urlStatusArray[i] = VerifyAccess(documentAcls[i], userGroups);
      }
   }
}

```


    If the user has access to the content item, set the value of the **BitArray** item at that index, **urlStatusArray[i]**, to **true**; otherwise, set it to **false**.
    
  
5. Setzen Sie den Rückgabewert der Methode **CheckAccess** auf **urlStatusArray**, wie im folgenden Codebeispiel demonstriert:
    
```cs
  
return urlStatusArray;
```


## <a name="register-the-custom-security-trimmer"></a>Registrieren des benutzerdefinierten Security Trimmers.
<a name="RegisterTrimmer"> </a>

Dieser Schritt beschreibt, wie Sie den benutzerdefinierten Security Trimmer konfigurieren und umfasst die folgenden Aufgaben:
  
    
    

- Registrieren des benutzerdefinierten Security trimmers für die Suchdienstanwendung mithilfe der Windows PowerShell-Cmdlets.
    
  
- Neustarten des SharePoint Search Host Controllers (SPSearchHostController).
    
  

### <a name="register-the-custom-security-trimmer"></a>Registrieren des benutzerdefinierten Security Trimmers

Benutzerdefinierte Security Trimmer werden mithilfe des Parameters _ClassName_ in der SharePoint-Verwaltungsshell registriert. In unserem Fall kann der Wert für _ClassName_ entweder **CustomSecurityPreTrimmer** oder **CustomSecurityPostTrimmer** sein. Die nachfolgende Anleitung beschreibt, wie Sie einen benutzerdefinierten Security Trimmer registrieren. Als ID für die Suchdienstanwendung wird 1 gesetzt.
  
    
    

### <a name="to-register-the-custom-security-trimmer"></a>So registrieren Sie den benutzerdefinierten Security Trimmer


1. Navigieren Sie im Windows-Explorer zur Datei „CustomSecurityTrimmerSample.dll“ unter dem Pfad „_<Local_Drive>_:\\WINDOWS\\assembly“.
    
  
2. Öffnen Sie das Kontextmenü für die Datei, und wählen Sie dann auf Eigenschaften.
    
  
3. Wählen Sie im Dialogfeld **Eigenschaften** auf der Registerkarte **Allgemein** das Token aus, und kopieren Sie es.
    
  
4. Open the SharePoint-Verwaltungsshell. For information about using this tool, see  [Administering Service Applications Using the SharePoint 2010 Management Shell.](http://msdn.microsoft.com/library/aff64855-7377-4e4a-b3a9-b620c9047076%28Office.15%29.aspx)
    
  
5. Geben Sie den folgenden Befehl in die Eingabeaufforderung ein:
    
```
  New-SPEnterpriseSearchSecurityTrimmer -SearchApplication "Search Service Application"
-typeName "CustomSecurityTrimmerSample.ClassName, CustomSecurityTrimmerSample, 
Version=1.0.0.0, Culture=neutral, PublicKeyToken=token" -RulePath "xmldoc://*"
```


    In the command, replace  _ClassName_ either with **CustomSecurityPreTrimmer** or **CustomSecurityPostTrimmer** and _token_ with the Public Key Token for the CustomSecurityTrimmerSample.dll file. You must associate all post-trimmers with a crawl rule, _"xmldoc://*"_; but this is optional for pre-trimmers.
    
    > **Note:**
      > If you have multiple front-end web servers, you must deploy your security trimmer to the global assembly cache on all the front-end web servers in the farm. 
6. Überprüfen Sie, ob der Security Trimmer in den folgenden PowerShell-Cmdlets registriert ist:
    
```
  
$searchApp = Get-SPEnterpriseSearchServiceApplication
$searchApp | Get-SPEnterpriseSearchSecurityTrimmer
```


    Your security trimmer must be visible in the results.
    
  

### <a name="to-restart-the-sharepoint-search-host-controller"></a>So starten Sie den Hostcontroller der SharePoint-Suche neu


- Sie können den Suchdienst neu starten, durch Eingabe des folgenden PowerShell-Cmdlets.
    
```
  
net restart sphostcontrollerservice

```


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_sectrimmer_addlresources"> </a>


-  [Benutzerdefinierte Sicherheitskürzung für die Suche in SharePoint](custom-security-trimming-for-search-in-sharepoint-server.md)
    
  
-  [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx)
    
  
-  [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx)
    
  
-  [Microsoft.Office.Server.Search.Query.PluggableAccessCheckException](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.PluggableAccessCheckException.aspx)
    
  

