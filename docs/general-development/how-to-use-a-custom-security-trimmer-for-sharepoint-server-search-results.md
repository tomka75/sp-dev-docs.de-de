---
title: "Verwenden eines benutzerdefinierten Security Trimmers für Suchergebnisse für SharePoint Server"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e1a8664e-fb43-45c2-83aa-9635fe1efc99
ms.openlocfilehash: 55ea7ee4ef785f65cefe436ebe2fbc14eab4bd87
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="use-a-custom-security-trimmer-for-sharepoint-server-search-results"></a><span data-ttu-id="cee0e-102">Verwenden eines benutzerdefinierten Security Trimmers für Suchergebnisse für SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="cee0e-102">Use a custom security trimmer for SharePoint Server search results</span></span>

<span data-ttu-id="cee0e-103">Dieser Artikel führt Sie durch die Schritte zum Implementieren, Erstellen, Bereitstellen und Registrieren eines benutzerdefinierten Security Trimmers für die Suche in SharePoint mithilfe von Microsoft Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="cee0e-103">This how-to guides you through the steps to implement—create, deploy, and register—a custom security trimmer for Search in SharePoint by using Visual Studio 2010.</span></span>

<span data-ttu-id="cee0e-104">Die Suche in SharePoint führt eine Sicherheitskürzung von Suchergebnissen zur Abfragezeit durch.</span><span class="sxs-lookup"><span data-stu-id="cee0e-104">Search in SharePoint performs query-time security trimming of search results.</span></span> <span data-ttu-id="cee0e-105">Es gibt jedoch Szenarios, in denen Sie eine benutzerdefinierte Sicherheitskürzung durchführen möchten.</span><span class="sxs-lookup"><span data-stu-id="cee0e-105">However, there may be scenarios in which you want to perform custom security trimming.</span></span> <span data-ttu-id="cee0e-106">Die Suche in SharePoint bietet über die folgenden Schnittstellen im [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx)-Namespace Unterstützung für diese Szenarios: [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) , [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx)  und [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) (veraltet).</span><span class="sxs-lookup"><span data-stu-id="cee0e-106">Search in SharePoint provides support for these scenarios through the  [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) , [Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) , and [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) (deprecated) interfaces in the [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) namespace.</span></span>
  
    
    

<span data-ttu-id="cee0e-p102">Es gibt zwei Arten von benutzerdefinierten Einschränkung aus Sicherheitsgründen: Trimming vor und nach dem Zuschneiden. Vor dem Zuschneiden bezieht sich auf vor der Abfrage Evaluierungshandbuch und exemplarische Vorgehensweisen, in dem die Abfrage umgeschrieben wird Sicherheitsinformationen hinzufügen, bevor die Abfrage mit dem Suchindex abgeglichen wird. Nach der Einschränkung aus Sicherheitsgründen bezieht sich auf die nach der Abfrage Evaluierungshandbuch und exemplarische Vorgehensweisen, in denen die Suchergebnisse gelöscht werden, bevor sie an den Benutzer zurückgegeben werden. Wir empfehlen die Verwendung von vor Einschränkung aus Sicherheitsgründen für Leistung und allgemeine Korrektheit; nach der Einschränkung aus Sicherheitsgründen wird verhindert, dass Informationslecks für Einschränkung Daten und Anzahl der Zugriffe Instanzen.</span><span class="sxs-lookup"><span data-stu-id="cee0e-p102">There are two kinds of custom security trimming: Pre-trimming and post-trimming. Pre-trimming refers to pre-query evaluation where the query is rewritten to add security information before the query is matched to the search index. Post-trimming refers to post-query evaluation where the search results are pruned before they are returned to the user. We recommend the use of pre-trimming for performance and general correctness; post-trimming prevents information leakage for refiner data and hit count instances.</span></span>
  
    
    

<span data-ttu-id="cee0e-111">Der Security Trimmer-Registrierungsprozess können Sie für den benutzerdefinierten Security Trimmer Konfigurationseigenschaften angeben.</span><span class="sxs-lookup"><span data-stu-id="cee0e-111">The security trimmer registration process enables you to specify configuration properties for the custom security trimmer.</span></span>
## <a name="overview"></a><span data-ttu-id="cee0e-112">Übersicht</span><span class="sxs-lookup"><span data-stu-id="cee0e-112">Overview</span></span>

<span data-ttu-id="cee0e-p103">Benutzerdefinierte Security Trimming in Suche in SharePoint besteht aus zwei Schnittstellen, die verwendet werden können, um vor dem Zuschneiden oder nach der Trimming der Suchergebnisse auszuführen. Diese Vorgehensweise konzentriert sich auf beide Schnittstellen, beschreibt die erforderlichen Schritte zum Erstellen und registrieren Ihre eigene Security Trimmer ab.</span><span class="sxs-lookup"><span data-stu-id="cee0e-p103">Custom Security Trimming in Search in SharePoint consists of two interfaces that can be used to carry out pre-trimming or post-trimming of your search results. This how-to focuses on both interfaces, describing the steps necessary to create and register your own security trimmers.</span></span>
  
    
    

## <a name="prerequisites"></a><span data-ttu-id="cee0e-115">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="cee0e-115">Prerequisites</span></span>
<span data-ttu-id="cee0e-116"><a name="PreReq"> </a></span><span class="sxs-lookup"><span data-stu-id="cee0e-116"><a name="PreReq"> </a></span></span>

<span data-ttu-id="cee0e-117">Um diese Vorgehensweise ausführen zu können, müssen Sie Folgendes in Ihrer Entwicklungsumgebung installiert sein:</span><span class="sxs-lookup"><span data-stu-id="cee0e-117">To complete this how-to, you must have the following installed in your development environment:</span></span>
  
    
    

- <span data-ttu-id="cee0e-118">Suche in Microsoft SharePoint</span><span class="sxs-lookup"><span data-stu-id="cee0e-118">Search in Microsoft SharePoint</span></span>
    
  
- <span data-ttu-id="cee0e-119">Microsoft Visual Studio 2010 oder ähnliche Microsoft .NET Framework - kompatibles Entwicklungstool</span><span class="sxs-lookup"><span data-stu-id="cee0e-119">Microsoft Visual Studio 2010 or similar Microsoft .NET Framework-compatible development tool</span></span>
    
  

## <a name="set-up-a-custom-security-trimmer-project"></a><span data-ttu-id="cee0e-120">Einrichten eines benutzerdefinierten Security Trimmer-Projekts</span><span class="sxs-lookup"><span data-stu-id="cee0e-120">Set up a custom security trimmer project</span></span>
<span data-ttu-id="cee0e-121"><a name="SetUp"> </a></span><span class="sxs-lookup"><span data-stu-id="cee0e-121"><a name="SetUp"> </a></span></span>

<span data-ttu-id="cee0e-122">In diesem Schritt werden Sie erstellen des Projekts für den benutzerdefinierten Security Trimmer, und fügen Sie die erforderlichen Verweise auf das Projekt.</span><span class="sxs-lookup"><span data-stu-id="cee0e-122">In this step, you will create the custom security trimmer project, and then add the required references to the project.</span></span>
  
    
    

### <a name="to-create-the-project-for-a-custom-security-trimmer"></a><span data-ttu-id="cee0e-123">So erstellen Sie das Projekt für einen benutzerdefinierten Security trimmer</span><span class="sxs-lookup"><span data-stu-id="cee0e-123">To create the project for a custom security trimmer</span></span>


1. <span data-ttu-id="cee0e-124">Öffnen Sie Visual Studio, und wählen Sie **Datei**, **neu**, **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="cee0e-124">Open Visual Studio and choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="cee0e-125">Wählen Sie in **Projekttypen** unter **c#** **SharePoint** aus.</span><span class="sxs-lookup"><span data-stu-id="cee0e-125">In **Project types**, under **C#**, choose **SharePoint**.</span></span>
    
  
3. <span data-ttu-id="cee0e-p104">Wählen Sie unter **Vorlagen** **Leeres SharePoint-Projekt**. Klicken Sie im Feld **Name** Geben Sie **CustomSecurityTrimmerSample**, und wählen Sie dann auf die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="cee0e-p104">Under **Templates**, choose **Empty SharePoint Project**. In the **Name** field, type **CustomSecurityTrimmerSample**, and then choose the **OK** button.</span></span>
    
  
4. <span data-ttu-id="cee0e-128">Klicken Sie im **Assistenten zum Anpassen von SharePoint**-Wählen Sie **als Farmlösung bereitstellen**, und wählen Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="cee0e-128">In the **SharePoint Customization Wizard**, choose **Deploy as a farm solution**, and then choose **Finish**.</span></span>
    
  

### <a name="to-add-references-to-the-custom-security-trimmer-project"></a><span data-ttu-id="cee0e-129">So fügen Sie dem Projekt für den benutzerdefinierten Security Trimmer Verweise hinzu</span><span class="sxs-lookup"><span data-stu-id="cee0e-129">To add references to the custom security trimmer project</span></span>


1. <span data-ttu-id="cee0e-130">Wählen Sie im **Projekt** auf **Verweis hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="cee0e-130">On the **Project** menu, choose **Add Reference**.</span></span>
    
  
2. <span data-ttu-id="cee0e-131">Klicken Sie auf der Registerkarte **.NET** Wählen Sie die Verweise mit den folgenden Komponentennamen aus, und wählen Sie dann auf die Schaltfläche **OK**:</span><span class="sxs-lookup"><span data-stu-id="cee0e-131">On the **.NET** tab, choose the references with the following component names, and then choose the **OK** button:</span></span>
    
  - <span data-ttu-id="cee0e-132">**Microsoft Search-Komponente**</span><span class="sxs-lookup"><span data-stu-id="cee0e-132">**Microsoft Search component**</span></span>
    
    <span data-ttu-id="cee0e-p105">Auf der Registerkarte **.NET** mit den Namen der Komponente **Microsoft Search-Komponente** sollte zwei Einträge angezeigt werden. Wählen Sie den Eintrag, in die Spalte Pfad \\ISAPI\\Microsoft.Office.Server.Search.dll ist. Wenn dieser Eintrag auf der Registerkarte **.NET** im Dialogfeld **Verweise hinzufügen** nicht vorhanden ist, müssen Sie den Verweis von der Registerkarte **Durchsuchen** mithilfe des Pfads zu der Microsoft.Office.Server.Search.dll hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="cee0e-p105">You should see two entries on the **.NET** tab with the component name **Microsoft Search component**. Select the entry where the Path column is \\ISAPI\\Microsoft.Office.Server.Search.dll. If this entry is missing from the **.NET** tab in the **Add References** dialog box, you must add the reference from the **Browse** tab by using the path to the Microsoft.Office.Server.Search.dll.</span></span>
    
  
  - <span data-ttu-id="cee0e-136">**Microsoft.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="cee0e-136">**Microsoft.IdentityModel**</span></span>
    
    <span data-ttu-id="cee0e-137">Wenn **Microsoft.IdentityModel** auf der Registerkarte **.NET** nicht aufgeführt ist, müssen Sie den Verweis auf die Microsoft.IdentityModel.dll über die Registerkarte **Durchsuchen** unter Verwendung des folgenden Pfads hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="cee0e-137">If **Microsoft.IdentityModel** is not listed on the **.NET** tab, you must add the reference to the Microsoft.IdentityModel.dll from the **Browse** tab, by using the following path:</span></span>
    
     `%ProgramFiles%\\Reference Assemblies\\Microsoft\\Windows Identity Foundation\\v4.0.`
    
  

## <a name="create-a-custom-security-pre-trimmer"></a><span data-ttu-id="cee0e-138">Erstellen eines vor dem benutzerdefinierten Security trimmers</span><span class="sxs-lookup"><span data-stu-id="cee0e-138">Create a custom security pre-trimmer</span></span>
<span data-ttu-id="cee0e-139"><a name="CreatePreTrimmer"> </a></span><span class="sxs-lookup"><span data-stu-id="cee0e-139"><a name="CreatePreTrimmer"> </a></span></span>


### <a name="to-create-the-class-file-for-the-security-pre-trimmer"></a><span data-ttu-id="cee0e-140">Die Klassendatei für den Security Trimmer vor dem Erstellen</span><span class="sxs-lookup"><span data-stu-id="cee0e-140">To create the class file for the security pre-trimmer</span></span>


1. <span data-ttu-id="cee0e-141">Wählen Sie im Menü **PROJEKT** die Option **Neues Element hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="cee0e-141">On the **Project** menu, choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="cee0e-142">Klicken Sie unter **Visual C#-Elemente** in **Installierte Vorlagen** Wählen Sie **Code** aus, und wählen Sie dann auf **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="cee0e-142">Under **Visual C# Items** in **Installed Templates**, choose **Code**, and then choose **Class**.</span></span>
    
  
3. <span data-ttu-id="cee0e-143">Geben Sie **CustomSecurityPreTrimmer.cs** ein, und wählen Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="cee0e-143">Type **CustomSecurityPreTrimmer.cs**, and then choose **Add**.</span></span>
    
  

### <a name="writing-the-custom-security-pre-trimmer-code"></a><span data-ttu-id="cee0e-144">Schreiben den benutzerdefinierten Security Trimmer Pre-code</span><span class="sxs-lookup"><span data-stu-id="cee0e-144">Writing the custom security pre-trimmer code</span></span>

<span data-ttu-id="cee0e-p106">Ihre benutzerdefinierten Security Trimmer muss die **ISecurityTrimmerPre** -Schnittstelle implementieren. Im folgenden Codebeispiel wird eine einfache Implementierung dieser Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="cee0e-p106">Your custom security trimmer must implement the **ISecurityTrimmerPre** interface. The following code example is a basic implementation of this interface.</span></span>
  
    
    

### <a name="to-modify-the-default-code-in-customsecuritypretrimmer"></a><span data-ttu-id="cee0e-147">So ändern Sie den Standardcode in CustomSecurityPreTrimmer</span><span class="sxs-lookup"><span data-stu-id="cee0e-147">To modify the default code in CustomSecurityPreTrimmer</span></span>


1. <span data-ttu-id="cee0e-148">Fügen Sie am Anfang der Klasse die folgenden **using**-Direktiven hinzu:</span><span class="sxs-lookup"><span data-stu-id="cee0e-148">Add the following **using** directives at the beginning of the class.</span></span>
    
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

2. <span data-ttu-id="cee0e-149">Geben Sie an, dass die **CustomSecurityPreTrimmer** -Klasse die [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) -Schnittstelle in der Klassendeklaration implementiert, wie im folgenden Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="cee0e-149">Specify that the **CustomSecurityPreTrimmer** class implements the [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) interface in the class declaration, as shown in the following code.</span></span>
    
```cs
  
public class CustomSecurityPreTrimmer : ISecurityTrimmerPre
```


### <a name="to-implement-the-isecuritytrimmerpre-interface-methods"></a><span data-ttu-id="cee0e-150">Implementieren die ISecurityTrimmerPre-Schnittstellenmethoden</span><span class="sxs-lookup"><span data-stu-id="cee0e-150">To implement the ISecurityTrimmerPre interface methods</span></span>


1. <span data-ttu-id="cee0e-151">Fügen Sie den folgenden Code hinzu, um die Methode [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) zu deklarieren:</span><span class="sxs-lookup"><span data-stu-id="cee0e-151">Add the following code for the  [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) method declaration.</span></span>
    
```cs
  public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{

}
```


    The basic version of this sample does not include any code in the **Initialize** method.
    
  
2. <span data-ttu-id="cee0e-152">Fügen Sie den folgenden Code hinzu, um die Methode [AddAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) zu deklarieren:</span><span class="sxs-lookup"><span data-stu-id="cee0e-152">Add the following code for the  [AddAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) method declaration.</span></span>
    
```cs
  
public IEnumerable<Tuple<Claim, bool>> AddAccess(
                IDictionary<string, object> sessionProperties, IIdentity passedUserIdentity)
{
//AddAccess method implementation, see steps 3-5.
}
```

3. <span data-ttu-id="cee0e-153">Im ersten Teil des Codes für die Methode **AddAccess** können wir dem Wert _passedUserIdentity_ die Identität des Benutzers entnehmen.</span><span class="sxs-lookup"><span data-stu-id="cee0e-153">For the first part of the **AddAccess** method implementation, we find out who the user is by looking at the _passedUserIdentity_.</span></span>
    
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

4. <span data-ttu-id="cee0e-154">Erstellen Sie eine Liste, befüllen Sie die Liste mit Ansprüchen, und geben Sie sie anschließend zurück, wie im folgenden Codebeispiel demonstriert:</span><span class="sxs-lookup"><span data-stu-id="cee0e-154">Create a list, populate the list with claims and return the list, as shown in the following code.</span></span>
    
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
    
  

## <a name="create-a-custom-security-post-trimmer"></a><span data-ttu-id="cee0e-155">Erstellen eines benutzerdefinierten Security Post-Trimmers</span><span class="sxs-lookup"><span data-stu-id="cee0e-155">Create a custom security post-trimmer</span></span>
<span data-ttu-id="cee0e-156"><a name="CreatePostTrimmer"> </a></span><span class="sxs-lookup"><span data-stu-id="cee0e-156"><a name="CreatePostTrimmer"> </a></span></span>


### <a name="to-create-the-class-file-for-the-security-post-trimmer"></a><span data-ttu-id="cee0e-157">Erstellen Sie die Klassendatei für den nach der Security trimmer</span><span class="sxs-lookup"><span data-stu-id="cee0e-157">To create the class file for the security post-trimmer</span></span>


1. <span data-ttu-id="cee0e-158">Wählen Sie im Menü **PROJEKT** die Option **Neues Element hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="cee0e-158">On the **Project** menu, choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="cee0e-159">Klicken Sie unter **Visual C#-Elemente** in **Installierte Vorlagen** Wählen Sie **Code** aus, und wählen Sie dann **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="cee0e-159">Under **Visual C# Items** in **Installed Templates**, choose **Code**, and then choose **Class**..</span></span>
    
  
3. <span data-ttu-id="cee0e-160">Geben Sie CustomSecurityPostTrimmer.csein, und wählen Sie dann auf **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="cee0e-160">Type CustomSecurityPostTrimmer.cs, and then choose **Add**.</span></span>
    
  

### <a name="writing-the-custom-security-post-trimmer-code"></a><span data-ttu-id="cee0e-161">Den benutzerdefinierten Security Trimmer nach der Code zu schreiben</span><span class="sxs-lookup"><span data-stu-id="cee0e-161">Writing the custom security post-trimmer code</span></span>

<span data-ttu-id="cee0e-p107">Ihre benutzerdefinierten Security Trimmer muss die **ISecurityTrimmerPost** -Schnittstelle implementieren. Das Codebeispiel in diesem Abschnitt wird eine einfache Implementierung dieser Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="cee0e-p107">Your custom security trimmer must implement the **ISecurityTrimmerPost** interface. The code example in this section is a basic implementation of this interface.</span></span>
  
    
    

### <a name="to-modify-the-default-code-in-customsecurityposttrimmer"></a><span data-ttu-id="cee0e-164">So ändern Sie den Standardcode in CustomSecurityPostTrimmer</span><span class="sxs-lookup"><span data-stu-id="cee0e-164">To modify the default code in CustomSecurityPostTrimmer</span></span>


1. <span data-ttu-id="cee0e-165">Fügen Sie am Anfang der Klasse die folgenden **using**-Direktiven hinzu:</span><span class="sxs-lookup"><span data-stu-id="cee0e-165">Add the following **using** directives at the beginning of the class:</span></span>
    
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

2. <span data-ttu-id="cee0e-166">Festlegen Sie, dass die **CustomSecurityPostTrimmer** -Klasse die [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) -Schnittstelle in der Klassendeklaration wie folgt implementiert:</span><span class="sxs-lookup"><span data-stu-id="cee0e-166">Specify that the **CustomSecurityPostTrimmer** class implements the [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) interface in the class declaration, as follows:</span></span>
    
```cs
  
public class CustomSecurityPostTrimmer : ISecurityTrimmerPost
```


### <a name="to-implement-the-isecuritytrimmerpost-interface-methods"></a><span data-ttu-id="cee0e-167">Implementieren die ISecurityTrimmerPost-Schnittstellenmethoden</span><span class="sxs-lookup"><span data-stu-id="cee0e-167">To implement the ISecurityTrimmerPost interface methods</span></span>


1. <span data-ttu-id="cee0e-168">Fügen Sie den folgenden Code hinzu, um die Methode [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) zu deklarieren:</span><span class="sxs-lookup"><span data-stu-id="cee0e-168">Add the following code for the  [Initialize()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) method declaration.</span></span>
    
```cs
  public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{

}
```


    The basic version of this sample does not include any code in the Initialize method.
    
  
2. <span data-ttu-id="cee0e-169">Fügen Sie den folgenden Code hinzu, um die Methode [CheckAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.CheckAccess.aspx) zu deklarieren:</span><span class="sxs-lookup"><span data-stu-id="cee0e-169">Add the following code for the  [CheckAccess()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.CheckAccess.aspx) method declaration.</span></span>
    
```cs
  
public BitArray CheckAccess(IList<string> documentCrawlUrls, IList<string> documentAcls, IDictionary<string, object> sessionProperties, IIdentity passedUserIdentity)
{
//CheckAccess method implementation, see steps 3-5.
}
```

3. <span data-ttu-id="cee0e-170">Für den ersten Teil der Implementierung der **CheckAccess** -Methode deklarieren und Initialisieren einer Variablen **BitArray** zum Speichern der Ergebnisse der Zugriffsüberprüfung für jede URL in der Auflistung **documentCrawlUrls** und Abrufen des Benutzers, der die Suchabfrage übermittelt hat, wie im folgenden Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="cee0e-170">For the first part of the **CheckAccess** method implementation, declare and initialize a **BitArray** variable to store the results of the access check for each URL in the **documentCrawlUrls** collection, and retrieve the user who submitted the query, as shown in the following code.</span></span>
    
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

4. <span data-ttu-id="cee0e-171">Durchlaufen Sie jede Durchforstungs-URL in der Auflistung, und führen Sie die Zugriffsüberprüfung, um festzustellen, ob der Benutzer, übermittelt hat, dass die Abfrage der Durchforstungs-URLs zugreifen kann, Inhaltselemente verknüpft ist, wie im folgenden Code dargestellt.</span><span class="sxs-lookup"><span data-stu-id="cee0e-171">Loop through each crawl URL in the collection, and perform the access check to determine if the user who submitted the query can access the crawl URL's associated content item, as shown in the following code.</span></span> 
    
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
    
  
5. <span data-ttu-id="cee0e-172">Setzen Sie den Rückgabewert der Methode **CheckAccess** auf **urlStatusArray**, wie im folgenden Codebeispiel demonstriert:</span><span class="sxs-lookup"><span data-stu-id="cee0e-172">Set the return value of the **CheckAccess** method to **urlStatusArray**, as shown in the following code.</span></span>
    
```cs
  
return urlStatusArray;
```


## <a name="register-the-custom-security-trimmer"></a><span data-ttu-id="cee0e-173">Registrieren des benutzerdefinierten Security Trimmers.</span><span class="sxs-lookup"><span data-stu-id="cee0e-173">Register the custom security trimmer</span></span>
<span data-ttu-id="cee0e-174"><a name="RegisterTrimmer"> </a></span><span class="sxs-lookup"><span data-stu-id="cee0e-174"><a name="RegisterTrimmer"> </a></span></span>

<span data-ttu-id="cee0e-175">Dieser Schritt beschreibt, wie Sie den benutzerdefinierten Security Trimmer konfigurieren und umfasst die folgenden Aufgaben:</span><span class="sxs-lookup"><span data-stu-id="cee0e-175">This step describes how to configure the custom security trimmer, and includes the following tasks:</span></span>
  
    
    

- <span data-ttu-id="cee0e-176">Registrieren des benutzerdefinierten Security trimmers für die Suchdienstanwendung mithilfe der Windows PowerShell-Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="cee0e-176">Registering the custom security trimmer for the Search service application by using the Windows PowerShell cmdlets.</span></span>
    
  
- <span data-ttu-id="cee0e-177">Neustarten des SharePoint Search Host Controllers (SPSearchHostController).</span><span class="sxs-lookup"><span data-stu-id="cee0e-177">Restarting the SharePoint search host controller (SPSearchHostController).</span></span>
    
  

### <a name="register-the-custom-security-trimmer"></a><span data-ttu-id="cee0e-178">Registrieren des benutzerdefinierten Security Trimmers</span><span class="sxs-lookup"><span data-stu-id="cee0e-178">Register the custom security trimmer</span></span>

<span data-ttu-id="cee0e-179">Benutzerdefinierte Security Trimmer werden mithilfe des Parameters _ClassName_ in der SharePoint-Verwaltungsshell registriert.</span><span class="sxs-lookup"><span data-stu-id="cee0e-179">You use the SharePoint Management Shell to register a custom security trimmer with  _ClassName_.</span></span> <span data-ttu-id="cee0e-180">In unserem Fall kann der Wert für _ClassName_ entweder **CustomSecurityPreTrimmer** oder **CustomSecurityPostTrimmer** sein.</span><span class="sxs-lookup"><span data-stu-id="cee0e-180">In our case,  _ClassName_ could be either **CustomSecurityPreTrimmer** or **CustomSecurityPostTrimmer**.</span></span> <span data-ttu-id="cee0e-181">Die nachfolgende Anleitung beschreibt, wie Sie einen benutzerdefinierten Security Trimmer registrieren. Als ID für die Suchdienstanwendung wird 1 gesetzt.</span><span class="sxs-lookup"><span data-stu-id="cee0e-181">The following procedure shows how to register a custom security trimmer, with the ID set to 1 for the Search service application.</span></span>
  
    
    

### <a name="to-register-the-custom-security-trimmer"></a><span data-ttu-id="cee0e-182">So registrieren Sie den benutzerdefinierten Security Trimmer</span><span class="sxs-lookup"><span data-stu-id="cee0e-182">To register the custom security trimmer</span></span>


1. <span data-ttu-id="cee0e-183">Navigieren Sie im Windows-Explorer zur Datei „CustomSecurityTrimmerSample.dll“ unter dem Pfad „_<Local_Drive>_:\\WINDOWS\\assembly“.</span><span class="sxs-lookup"><span data-stu-id="cee0e-183">In Windows Explorer, locate CustomSecurityTrimmerSample.dll in the path  _<Local_Drive>_:\\WINDOWS\\assembly.</span></span>
    
  
2. <span data-ttu-id="cee0e-184">Öffnen Sie das Kontextmenü für die Datei, und wählen Sie dann auf Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="cee0e-184">Open the shortcut menu for the file, and then choose Properties.</span></span>
    
  
3. <span data-ttu-id="cee0e-185">Wählen Sie im Dialogfeld **Eigenschaften** auf der Registerkarte **Allgemein** das Token aus, und kopieren Sie es.</span><span class="sxs-lookup"><span data-stu-id="cee0e-185">On the **General** tab in the **Properties** dialog box, select the token and copy it.</span></span>
    
  
4. <span data-ttu-id="cee0e-p109">Open the SharePoint-Verwaltungsshell. For information about using this tool, see  [Administering Service Applications Using the SharePoint 2010 Management Shell.](http://msdn.microsoft.com/library/aff64855-7377-4e4a-b3a9-b620c9047076%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="cee0e-p109">Open the SharePoint Management Shell. For information about using this tool, see  [Administering Service Applications Using the SharePoint 2010 Management Shell](http://msdn.microsoft.com/library/aff64855-7377-4e4a-b3a9-b620c9047076%28Office.15%29.aspx)</span></span>
    
  
5. <span data-ttu-id="cee0e-188">Geben Sie den folgenden Befehl in die Eingabeaufforderung ein:</span><span class="sxs-lookup"><span data-stu-id="cee0e-188">At the command prompt, type the following command.</span></span>
    
```
  New-SPEnterpriseSearchSecurityTrimmer -SearchApplication "Search Service Application"
-typeName "CustomSecurityTrimmerSample.ClassName, CustomSecurityTrimmerSample, 
Version=1.0.0.0, Culture=neutral, PublicKeyToken=token" -RulePath "xmldoc://*"
```


    In the command, replace  _ClassName_ either with **CustomSecurityPreTrimmer** or **CustomSecurityPostTrimmer** and _token_ with the Public Key Token for the CustomSecurityTrimmerSample.dll file. You must associate all post-trimmers with a crawl rule, _"xmldoc://*"_; but this is optional for pre-trimmers.
    
    > [!NOTE]
    > If you have multiple front-end web servers, you must deploy your security trimmer to the global assembly cache on all the front-end web servers in the farm. 

6. <span data-ttu-id="cee0e-189">Überprüfen Sie, ob der Security Trimmer in den folgenden PowerShell-Cmdlets registriert ist:</span><span class="sxs-lookup"><span data-stu-id="cee0e-189">Verify that your security trimmer is registered with the following PowerShell cmdlets.</span></span>
    
```
  
$searchApp = Get-SPEnterpriseSearchServiceApplication
$searchApp | Get-SPEnterpriseSearchSecurityTrimmer
```


    Your security trimmer must be visible in the results.
    
  

### <a name="to-restart-the-sharepoint-search-host-controller"></a><span data-ttu-id="cee0e-190">So starten Sie den Hostcontroller der SharePoint-Suche neu</span><span class="sxs-lookup"><span data-stu-id="cee0e-190">To restart the SharePoint search host controller</span></span>


- <span data-ttu-id="cee0e-191">Sie können den Suchdienst neu starten, durch Eingabe des folgenden PowerShell-Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="cee0e-191">You can restart the Search Service by typing the following PowerShell cmdlet.</span></span>
    
```
  
net restart sphostcontrollerservice

```


## <a name="see-also"></a><span data-ttu-id="cee0e-192">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="cee0e-192">See also</span></span>
<span data-ttu-id="cee0e-193"><a name="bk_sectrimmer_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="cee0e-193"><a name="bk_sectrimmer_addlresources"> </a></span></span>


-  [<span data-ttu-id="cee0e-194">Benutzerdefinierte Sicherheitskürzung für die Suche in SharePoint</span><span class="sxs-lookup"><span data-stu-id="cee0e-194">Custom security trimming for Search in SharePoint</span></span>](custom-security-trimming-for-search-in-sharepoint-server.md)
    
  
-  [<span data-ttu-id="cee0e-195">Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre</span><span class="sxs-lookup"><span data-stu-id="cee0e-195">Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx)
    
  
-  [<span data-ttu-id="cee0e-196">Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost</span><span class="sxs-lookup"><span data-stu-id="cee0e-196">Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx)
    
  
-  [<span data-ttu-id="cee0e-197">Microsoft.Office.Server.Search.Query.PluggableAccessCheckException</span><span class="sxs-lookup"><span data-stu-id="cee0e-197">Microsoft.Office.Server.Search.Query.PluggableAccessCheckException</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.PluggableAccessCheckException.aspx)
    
  

