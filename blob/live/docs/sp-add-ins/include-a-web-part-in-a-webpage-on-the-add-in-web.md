---
title: "Einschließen eines Webparts auf einer Webseite im Add-In-Web"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 16a1d546cb1093be30012bc343f15b3a09ad23c5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="include-a-web-part-in-a-webpage-on-the-add-in-web"></a><span data-ttu-id="67f3f-102">Einschließen eines Webparts auf einer Webseite im Add-In-Web</span><span class="sxs-lookup"><span data-stu-id="67f3f-102">Include a Web Part in a webpage on the add-in web</span></span>
<span data-ttu-id="67f3f-103">Erfahren Sie, wie Sie ein Webpart auf einer Seite in einem SharePoint-Add-In einschließen.</span><span class="sxs-lookup"><span data-stu-id="67f3f-103">Learn how to include a Web Part on a page in a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="67f3f-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="67f3f-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="67f3f-107">Sie können ein standardmäßiges Webpart auf einer Seite im Add-In-Web eines SharePoint-Add-Ins einschließen, aber Sie müssen dies so tun, dass dadurch bei einer späteren Aktualisierung des Add-Ins keine Probleme verursacht werden.</span><span class="sxs-lookup"><span data-stu-id="67f3f-107">You can include an out-of-the-box Web Part in a page in the add-in web of a SharePoint Add-in, but it is important that you do this in a way that won't cause problems if you ever need to update the add-in.</span></span>
 

<span data-ttu-id="67f3f-108">Hier finden Sie ein Codebeispiel, in dem die Anweisungen aus diesem Thema veranschaulicht werden: [OfficeDev/Core.WebPartOnAppWebPage](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.WebPartOnAppWebPage)</span><span class="sxs-lookup"><span data-stu-id="67f3f-108">A code sample that illustrates the guidance of this topic is at:  [OfficeDev/Core.WebPartOnAppWebPage](https://github.com/OfficeDev/PnP/tree/master/Samples/Core.WebPartOnAppWebPage)</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="67f3f-109">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="67f3f-109">Prerequisites</span></span>

<span data-ttu-id="67f3f-110">Voraussetzungen finden Sie unter [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="67f3f-110">For the prerequisites, see  [Get started creating SharePoint-hosted SharePoint Add-ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span></span>
 

 

## <a name="add-a-web-part-to-a-page"></a><span data-ttu-id="67f3f-111">Hinzufügen eines Webparts zu einer Seite</span><span class="sxs-lookup"><span data-stu-id="67f3f-111">Add a Web Part to a page</span></span>


 

 

1. <span data-ttu-id="67f3f-p102">Erstellen Sie ein von SharePoint gehostetes SharePoint-Add-In in Visual Studio. Weitere Informationen finden Sie unter [Erste Schritte beim Erstellen von von SharePoint gehosteten SharePoint-Add-Ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="67f3f-p102">Create a SharePoint-hosted SharePoint Add-in project in Visual Studio. For details, see  [Get started creating SharePoint-hosted SharePoint Add-ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span></span>
    
 
2. <span data-ttu-id="67f3f-p103">Öffnen Sie die ASPX-Datei, der Sie ein Webpart hinzufügen möchten. In diesem Thema wird „Default.aspx“ als Beispiel verwendet.</span><span class="sxs-lookup"><span data-stu-id="67f3f-p103">Open the aspx file to which you want to add a Web Part. This topic uses Default.aspx as an example.</span></span> 
    
 
3. <span data-ttu-id="67f3f-p104">Fügen Sie dem **<asp:Content>**-Element, das das Webpart enthalten soll, mit Markup wie dem folgenden eine **WebPartZone** hinzu. Normalerweise fügen Sie sie dem **<asp:Content>**-Element hinzu, dessen **ContentPlaceHolderId** `PlaceHolderMain` ist. Im Folgenden finden Sie ein Beispiel.</span><span class="sxs-lookup"><span data-stu-id="67f3f-p104">Add a  **WebPartZone** to the **<asp:Content>** element where you want the Web Part with markup like the following. Typically, you want to add it to the **<asp:Content>** whose **ContentPlaceHolderId** is `PlaceHolderMain`. The following is an example.</span></span>
    
```XML
  <asp:Content ContentPlaceHolderId="PlaceHolderMain" runat="server">
  <WebPartPages:WebPartZone runat="server" FrameType="TitleBarOnly" 
      ID="HomePage1" Title="loc:full" />
</asp:Content>

```


     **Caution**  It is possible to add a Web Part element, such as  **<WebPartPages:XsltListViewWebPart>** as a child of the **WebPartZone**. But this is generally a bad practice in a SharePoint Add-in. If the add-in ever needs to be updated, a Web Part element inserted in the aspx file can cause the update to fail in some scenarios with the message "A web part with this ID has already been added to this page." We recommend that you add web parts to the elements manifest for the page as described later of this procedure.
4. <span data-ttu-id="67f3f-p105">Öffnen Sie die Elementmanifestdatei für die Seite. Sie heißt in der Regel „elements.xml" und befindet sich in demselben Projektordner wie die aspx-Datei.</span><span class="sxs-lookup"><span data-stu-id="67f3f-p105">Open the element manifest file for the page. This is usually called elements.xml and is located in the same project folder as the aspx file.</span></span>
    
 
5. <span data-ttu-id="67f3f-121">Fügen Sie im **File**-Element für die Seite ein untergeordnetes **AllUsersWebPart**-Element hinzu, und legen Sie seine **WebPartZoneID** auf den Wert der Webpartzone fest, die Sie auf der Seite erstellt haben, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="67f3f-121">In the  **File** element for the page, add a child **AllUsersWebPart** element and set its **WebPartZoneID** to the value of the Web Part zone that you created on the page as this example shows.</span></span>
    
```
  <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <Module Name="Pages">
    <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" >
      <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">

      </AllUsersWebPart>
    </File>
  </Module>
</Elements>

```

6. <span data-ttu-id="67f3f-122">Fügen Sie ein **CDATA**-Element als untergeordnetes Element von **AllUsersWebPart** hinzu, und fügen Sie dann ein **webParts**-Element als untergeordnetes Element von **CDATA** hinzu, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="67f3f-122">Add a  **CDATA** element as a child of the **AllUsersWebPart**, then add a  **webParts** element as a child of the **CDATA**, as shown in this example.</span></span> 
    
```
  <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">
  <![CDATA[
    <webParts>

    </webParts>
  ]]>
</AllUsersWebPart>
```

7. <span data-ttu-id="67f3f-p106">Fügen Sie **webPart**-Markup als untergeordnetes Element des **webParts**-Elements hinzu. Im folgenden Beispiel wird ein **XsltListViewWebPart** hinzugefügt. Es setzt voraus, dass eine benutzerdefinierte Liste „Test List“ Teil desselben Add-In-Projekts ist. Weitere Informationen zum Hinzufügen einer benutzerdefinierten Liste zu einem Add-In-Web finden Sie unter [Gewusst wie: Erstellen eines von einem Anbieter gehosteten Add-Ins, das eine benutzerdefinierte SharePoint-Liste und einen benutzerdefinierten Inhaltstyp enthält](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-conte.md).</span><span class="sxs-lookup"><span data-stu-id="67f3f-p106">Add  **webPart** markup as a child of the **webParts** element. The following is an example that adds an **XsltListViewWebPart**. It assumes that a custom list called "Test List" is part of the same add-in project. For information about how to add a custom list to an add-in web, see  [Create a provider-hosted add-in that includes a custom SharePoint list and content type](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-conte.md).</span></span> 
    
     <span data-ttu-id="67f3f-p107">**Hinweis** Beachten Sie, dass das Webpart keine ID-Eigenschaft hat. Es ist eine bewährte Methode, eine explizite ID für das Webpart nur in den zwei Fällen hinzufügen, in denen es unbedingt erforderlich ist: Das Webpart wird zu einer SharePoint-Wiki-Seite hinzugefügt. Das Webpart ist eins von zwei oder mehr Webparts, die verbunden werden.</span><span class="sxs-lookup"><span data-stu-id="67f3f-p107">**Note**   Note that the Web Part does not have an ID property. It is a best practice to include an explicit ID for the Web Part only in the two cases where it is really required: The Web Part is being added to a SharePoint wiki page. The Web Part is one of two or more Web Parts that will be connected.</span></span>

```
  <webParts>
  <webPart xmlns="http://schemas.microsoft.com/WebPart/v3">
    <metaData>
      <type name="Microsoft.SharePoint.WebPartPages.XsltListViewWebPart, 
                   Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, 
                   PublicKeyToken=71e9bce111e9429c" />
    </metaData>
    <data>
      <properties>
        <property name="ListUrl">Lists/{TestList}</property>
        <property name="IsIncluded">True</property>
        <property name="NoDefaultStyle">True</property>
        <property name="Title">{Test List}</property>
        <property name="PageType">PAGE_NORMALVIEW</property>
        <property name="Default">False</property>
        <property name="ViewContentTypeId">0x</property>
      </properties>
    </data>
  </webPart>
</webParts>
```

8. <span data-ttu-id="67f3f-p108">Drücken Sie F5, um das Add-In zu debuggen. Das Webpart sollte auf der Seite angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="67f3f-p108">Press F5 to debug the add-in. You should see the Web Part on the page.</span></span>
    
 

