---
title: "Vorgehensweise Erstellen eine mobile app in SharePoint, die Daten aus einer externen Datenquelle enthält."
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f1d62256-aca0-4a59-8145-0add9e68a449
ms.openlocfilehash: cd5c036ac63df1a11f6812bd44af407ad56cb27a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-external-data-source"></a><span data-ttu-id="dac0d-102">Vorgehensweise: Erstellen eine mobile app in SharePoint, die Daten aus einer externen Datenquelle enthält.</span><span class="sxs-lookup"><span data-stu-id="dac0d-102">How to: Create a mobile app in SharePoint that contains data from an external data source</span></span>
<span data-ttu-id="dac0d-p101">Hier erfahren Sie, wie Sie eine einfache mobile app in SharePoint erstellen, die Daten aus externen Datenquelle enthält, indem Sie mithilfe von Business Connectivity Services und Herstellen einer Verbindung mit einer externen Liste. SharePoint ermöglicht Ihnen, mobile Anwendungen zu erstellen, mit die externe Daten in Datenbanken, Unternehmensanwendungen und Web 2.0-Diensten mithilfe von Business Connectivity Services zugreifen können. Sie können auch vollständigen Interaktion mit den externen Daten einschließlich rückschreibfunktionen aus dem mobilen Gerät bereitstellen. Zu diesem Zweck erstellen von apps, die mit externen Listen, die einen besonderen Typ von Listen in SharePoint sind herzustellen, die basieren auf externe Inhaltstypen und Daten aus externen Systemen enthalten. Die neue SharePoint-Liste für Windows Phone-Vorlage in Visual Studio 2010 Express können Sie schnell und problemlos Erstellen von apps für Windows Phone, die mit externen Listen eine Verbindung herstellt. Beispielsweise können Sie eine Windows Phone-app erstellen, die den Produktkatalog für eine Inventarliste in SharePoint auf das Telefon für die Vertriebsmitarbeiter bereitstellt. In diesem Thema wird das Erstellen einer Windows Phone-app, die externe Daten aus der Northwind-Beispieldatenbank anzeigt, indem es eine Verbindung mit einer externen Liste in SharePoint. Beachten Sie, dass in diesem Beispiel wird die externe Liste zu Northwind-Datenbank mit einer benutzerdefinierten OData-Dienst herstellt. Es ist jedoch möglich, Verbinden mit Datenbanken direkt als auch für alle externen Systeme, die von Business Connectivity Services, mithilfe von externen Listen unterstützt wird. Mit der neuen SharePoint-Liste Vorlage in Visual Studio erstellen Sie eine mobile app, die auf eine externe Liste auf einer SharePoint-Website zugreifen können. Dieser Artikel enthält eine schrittweise Anleitung, die mit einer externen Business Data Connectivity (BDC)-Dienst Modell hochladen beginnt und endet mit der neuen mobilen Anwendung zu testen.</span><span class="sxs-lookup"><span data-stu-id="dac0d-p101">Learn how to create a simple mobile app in SharePoint that contains data from external data source by using Business Connectivity Services and connecting to an external list. SharePoint enables you to build mobile applications that can access external data from databases, enterprise applications, and Web 2.0 services using Business Connectivity Services. You can also provide complete interaction with the external data including write-back capabilities from your mobile device. You do this by creating apps that connect to external lists, which are a special type of lists in SharePoint that are based on external content types and contain data from an external system. The new Windows Phone SharePoint List template in Visual Studio 2010 Express enables you to quickly and easily create apps for the Windows Phone that connects to external lists. For example, you can build a Windows phone app that brings the product catalog for an inventory list in SharePoint to the phone for the sales people. This topic shows how to create a Windows Phone app that displays external data from the Northwind sample database by connecting to an external list in SharePoint. Notice that in this example, the external list connects to the Northwind database using a custom OData service; however, it's possible to connect to databases directly as well as any external system that is supported by Business Connectivity Services, using external lists. With the new SharePoint List template in Visual Studio, you can create a mobile app that can access an external list on a SharePoint site. This article provides a step-by-step procedure that begins with uploading an external Business Data Connectivity (BDC) service model and ends with testing your new mobile app.</span></span>
  
    
    


> <span data-ttu-id="dac0d-113">**Wichtig:** Wenn Sie eine App für Windows Phone 8 entwickeln, müssen Sie Visual Studio Express 2012 anstelle von Visual Studio 2010 Express verwenden.</span><span class="sxs-lookup"><span data-stu-id="dac0d-113">**Important** If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express. Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="dac0d-114">Mit Ausnahme der Entwicklungsumgebung gelten alle Informationen in diesem Artikel für das Erstellen von Apps sowohl auf Windows Phone 8 als auch auf Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="dac0d-114">Important If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express. Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="dac0d-115">Weitere Informationen finden Sie unter [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung mobiler Apps für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="dac0d-115">For more information, see  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span></span> 
  
    
    


## <a name="prerequisites-for-creating-a-mobile-app-that-contains-external-data"></a><span data-ttu-id="dac0d-116">Voraussetzungen für die Erstellung einer mobilen App, die externe Daten enthält</span><span class="sxs-lookup"><span data-stu-id="dac0d-116">Prerequisites for creating a mobile app that contains external data</span></span>
<span data-ttu-id="dac0d-117"><a name="SP15Createmobileapp_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="dac0d-117"></span></span>


- <span data-ttu-id="dac0d-118">Eine SharePoint Installation mit Administratorrechten zum Hochladen des BDC-Modells für die Northwind-Datenbank und einer SharePoint-Website, in dem Sie die externe Liste erstellen</span><span class="sxs-lookup"><span data-stu-id="dac0d-118">A SharePoint installation with administrative privileges to upload the BDC model for the Northwind database and a SharePoint site where you create the external list</span></span>
    
  
- <span data-ttu-id="dac0d-119">Microsoft Visual Studio Express mit den neuen SharePoint phonevorlagen aus  [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)</span><span class="sxs-lookup"><span data-stu-id="dac0d-119">Microsoft Visual Studio Express with the new SharePoint phone templates from  [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)</span></span>
    
  
- <span data-ttu-id="dac0d-120">Das BDC-Modell für unsere exampleNorthwind_oData.bdmc (Laden von  [SharePoint: erstellen eine einfachen externen listenbasierten Phone-app](http://code.msdn.microsoft.com/sharepoint/SharePoint-Create-a-88800202))</span><span class="sxs-lookup"><span data-stu-id="dac0d-120">The BDC model for our exampleNorthwind_oData.bdmc (download from  [SharePoint: Create a simple external list-based phone app](http://code.msdn.microsoft.com/sharepoint/SharePoint-Create-a-88800202))</span></span>
    
  
- <span data-ttu-id="dac0d-121">Eine SharePoint Installation mit Administratorrechten zum Hochladen des BDC-Modells für die Northwind-Datenbank und einer SharePoint-Website, in dem Sie die externe Liste erstellen</span><span class="sxs-lookup"><span data-stu-id="dac0d-121">A SharePoint installation with administrative privileges to upload the BDC model for the Northwind database and a SharePoint site where you create the external list</span></span>
    
  

## <a name="step-1-upload-a-bdc-metadata-model"></a><span data-ttu-id="dac0d-122">Schritt 1: Hochladen einer BDC-Metadatenmodell</span><span class="sxs-lookup"><span data-stu-id="dac0d-122">Step 1: Upload a BDC metadata model</span></span>
<span data-ttu-id="dac0d-123"><a name="HowToCreateSimpleExternalListBasedPhoneApp_Step1"> </a></span><span class="sxs-lookup"><span data-stu-id="dac0d-123"></span></span>

<span data-ttu-id="dac0d-p103">Ein BDC-Modell ist das Herzstück von Business Connectivity Services. Es ist eine XML-Datei, die Datenstrukturen wie **Entity** (externer Inhaltstyp) und **-Methode** wird verwendet, um die abstrakten komplexen Details über das externe System. Es wird automatisch generierten beim Erstellen eines externen Inhaltstyps mit SharePoint Designer und für einige Datenquellentypen solche .NET und OData-Quellen, Sie das BDC-Modell manuell oder mithilfe von Visual Studio erstellen müssen. Wenn Sie ein BDC-Modell für den BDC-Metadatenspeicher mithilfe der SharePoint-Zentraladministration hochladen, können die externen Inhaltstypen im Modell definierten verwendet werden, zum Erstellen von externer Listen in SharePoint Listen darstellen, die Daten aus dem zugrunde liegenden externen System anzeigen. In diesem Schritt werden das Northwind-Beispiel BDC-Modell für den Metadatenspeicher hochladen mithilfe der SharePoint-Zentraladministration.</span><span class="sxs-lookup"><span data-stu-id="dac0d-p103">A BDC model is the core of Business Connectivity Services. It's an XML file that uses data structures such as **Entity** (external content type) and **Method** to abstract out complex details about the external system. It's auto-generated when you create an external content type using SharePoint Designer and for some data source types such .NET and OData sources, you need to create the BDC model manually or by using Visual Studio. When you upload a BDC model to the BDC metadata store using SharePoint Central Administration, the external content types defined in the model can be used to create external lists in SharePoint which are lists that display data from the underlying external system. In this step, you'll upload the Northwind sample BDC model to the Metadata Store using SharePoint Central Administration.</span></span>
  
    
    

1. <span data-ttu-id="dac0d-129">Navigieren Sie zur Zentraladministration.</span><span class="sxs-lookup"><span data-stu-id="dac0d-129">Navigate to Central Administration.</span></span>
    
  
2. <span data-ttu-id="dac0d-130">Wählen Sie **Anwendungsverwaltung**, und wählen Sie dann auf **Dienstanwendungen verwalten**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-130">Choose **Application Management**, and then choose **Manage Service Applications**.</span></span>
    
  
3. <span data-ttu-id="dac0d-131">Wählen Sie auf der Seite „Dienstanwendung“ **Business Data Connectivity-Dienst** aus.</span><span class="sxs-lookup"><span data-stu-id="dac0d-131">On the Service Application page, choose **Business Data Connectivity Service**.</span></span>
    
  
4. <span data-ttu-id="dac0d-132">Wählen Sie im Menüband in der BDC-Dienstanwendung **Importieren**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-132">On the ribbon in the BDC Service application, choose **Import**.</span></span>
    
  
5. <span data-ttu-id="dac0d-133">Wählen Sie auf der Seite BDC-Modell importieren **Business Data Connectivity-Dienst**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-133">On the Import BDC Model page, choose **Business Data Connectivity Service**.</span></span>
    
  
6. <span data-ttu-id="dac0d-134">Wählen Sie auf dem Menüband in der BDC-Dienstanwendung **Importieren**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-134">On the ribbon in the BDC Service application, choose **Import**.</span></span>
    
  
7. <span data-ttu-id="dac0d-135">Wählen Sie **Durchsuchen** aus, auf der Seite BDC-Modell importieren.</span><span class="sxs-lookup"><span data-stu-id="dac0d-135">On the Import BDC Model page, choose **Browse**.</span></span>
    
  
8. <span data-ttu-id="dac0d-136">Klicken Sie im Dialogfeld **Datei zum Hochladen auswählen** suchen Sie die Datei Northwind_oData.bdcm, und wählen Sie dann auf **Öffnen**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-136">In the **Choose a File to upload** dialog box, browse to the Northwind_oData.bdcm file, and then choose **Open**.</span></span>
    
  
9. <span data-ttu-id="dac0d-137">Nachdem die Datei importiert wurde, wählen Sie die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-137">After the file is imported, choose the **OK** button.</span></span>
    
  

## <a name="step-2-grant-permissions"></a><span data-ttu-id="dac0d-138">Schritt 2: Gewähren von Berechtigungen</span><span class="sxs-lookup"><span data-stu-id="dac0d-138">Step 2: Grant permissions</span></span>
<span data-ttu-id="dac0d-139"><a name="HowToCreateSimpleExternalListBasedPhoneApp_Step2"> </a></span><span class="sxs-lookup"><span data-stu-id="dac0d-139"></span></span>

<span data-ttu-id="dac0d-p104">Als Nächstes müssen Sie zum Festlegen von Berechtigungen für das BDC-Modell, um anzugeben, die im Modell beschriebenen Methoden ausgeführt werden kann. Dies ist ein erforderlicher Schritt. Es wird empfohlen, dass Sie bestimmte Berechtigungen, jedem Benutzer oder Gruppe, die sie so benötigt erteilen, dass die Anmeldeinformationen der geringsten Rechte zum Ausführen der erforderlichen Aufgaben erforderlich. Weitere Informationen zum Festlegen von Berechtigungen finden Sie unter Übersicht über Business Connectivity Service-Berechtigungen in  [Business Connectivity Services-Sicherheit (Übersicht) (SharePoint Server 2010)](http://technet.microsoft.com/de-de/library/ee661740.aspx). In diesem Schritt erteilen Sie die Berechtigung an sich selbst zum Ausführen der Methods beschrieben, die in der Northwind-Beispiel BDC-Modell.</span><span class="sxs-lookup"><span data-stu-id="dac0d-p104">Next you need to set permissions on the BDC model to specify who can execute the methods described in the model. This is a required step. We recommend that you give specific permissions to each user or group that needs them, in such a way that the credentials provide the least privilege necessary to perform the needed tasks. For more information about setting permissions, see Business Connectivity Service permissions overview in  [Business Connectivity Services security overview (SharePoint Server 2010)](http://technet.microsoft.com/de-de/library/ee661740.aspx). In this step, you give permission to yourself to execute the methods described in the Northwind sample BDC model.</span></span>
  
    
    

1. <span data-ttu-id="dac0d-145">Navigieren Sie zur Zentraladministration.</span><span class="sxs-lookup"><span data-stu-id="dac0d-145">Navigate to Central Administration.</span></span>
    
  
2. <span data-ttu-id="dac0d-146">Wählen Sie **Anwendungsverwaltung**, und wählen Sie dann auf **Dienstanwendungen verwalten**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-146">Choose **Application Management**, and then choose **Manage Service Applications**.</span></span>
    
  
3. <span data-ttu-id="dac0d-147">Wählen Sie auf der Seite Dienstanwendungen die **Business Data Connectivity-Dienst**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-147">On the Service Application page, choose **Business Data Connectivity Service**.</span></span>
    
  
4. <span data-ttu-id="dac0d-148">Wählen Sie im Menüband der Dropdown Liste in der Gruppe **Ansicht** **BDC-Modelle**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-148">In the ribbon, choose **BDC Models** from the drop-down list in the **View** group.</span></span>
    
  
5. <span data-ttu-id="dac0d-149">In der Liste der BDC-Modelle mit dem Mauszeiger Northwind_oData.bdcm, und wählen Sie **Berechtigungen festlegen**, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="dac0d-149">In the list of BDC models, hover over Northwind_oData.bdcm and choose **Set Permissions**, as shown in Figure 1.</span></span>
    
   <span data-ttu-id="dac0d-150">**Abbildung 1. Auswahl von Berechtigungen für BDC-Modell**</span><span class="sxs-lookup"><span data-stu-id="dac0d-150">**Figure 1. Choosing permissions for BDC model**</span></span>

  

  ![Auswählen von Berechtigungen für BDC-Modell](../images/SPCon15_BDC_SetPermissions_ODataWebNorthWind.png)
  

  

  
6. <span data-ttu-id="dac0d-152">Wählen Sie die Schaltfläche **Durchsuchen**, klicken Sie im Dialogfeld **Objektberechtigungen festlegen**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-152">In the **Set Object Permissions** dialog box, choose the **Browse** button.</span></span>
    
  
7. <span data-ttu-id="dac0d-153">Klicken Sie im Dialogfeld **Personen und Gruppen auswählen** für Ihr Konto zu suchen Sie, und wählen Sie die Schaltfläche **OK**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-153">In the **Select People and Groups** dialog box, search for your account and choose the **OK** button.</span></span>
    
  
8. <span data-ttu-id="dac0d-154">Wählen Sie die Berechtigungen für das **Bearbeiten**, **Ausführen**, **Auswählbar In Clients** und **Berechtigungen festlegen**, wie in Abbildung 2 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="dac0d-154">Select the permissions for **Edit**, **Execute**, **Selectable In Clients**, and **Set Permissions**, as shown in Figure 2.</span></span>
    
   <span data-ttu-id="dac0d-155">**Abbildung 2. Festlegen von Berechtigungen für Gruppenrichtlinienobjekte**</span><span class="sxs-lookup"><span data-stu-id="dac0d-155">**Figure 2. Setting object permissions**</span></span>

  

  ![Festlegen von BDC-Objektberechtigungen](../images/SPCon15_Setting_BDCObjectPermission_DialogueBox.png)
  

  

  
9. <span data-ttu-id="dac0d-157">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-157">Choose the **OK** button.</span></span>
    
  
10. <span data-ttu-id="dac0d-158">Wählen Sie im Menüband **Externe Inhaltstypen** aus der Dropdown Liste in der Gruppe **Ansicht**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-158">In the ribbon, select **External Content Types** from the drop-down list in the **View** group.</span></span>
    
  
11. <span data-ttu-id="dac0d-159">In der Liste der externen Inhaltstypen mit dem Mauszeiger **Kunden**, und wählen Sie dann auf **Berechtigungen festlegen**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-159">In the list of external content types, hover over **Customer**, and then choose **Set Permissions**.</span></span>
    
  
12. <span data-ttu-id="dac0d-160">Wählen Sie die Schaltfläche **Durchsuchen**, und suchen Sie nach Ihrem Konto, klicken Sie im Dialogfeld **Objektberechtigungen festlegen**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-160">In the **Set Object Permissions** dialog box, choose the **Browse** button and search for your account.</span></span>
    
  
13. <span data-ttu-id="dac0d-161">Klicken Sie im Dialogfeld **Objektberechtigungen festlegen** auf **Hinzufügen**, und wählen Sie die Berechtigungen für das **Bearbeiten**, **Ausführen**, **Auswählbar In Clients** und **Berechtigungen festlegen**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-161">In the **Set Object Permissions** dialog box, choose **Add** and select the permissions for **Edit**, **Execute**, **Selectable In Clients**, and **Set Permissions**.</span></span>
    
  
14. <span data-ttu-id="dac0d-162">Stellen Sie sicher, dass das Kontrollkästchen **Berechtigungen weitergeben** aktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="dac0d-162">Ensure that the **Propagate Permissions** box is selected.</span></span>
    
  
15. <span data-ttu-id="dac0d-163">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-163">Choose the **OK** button.</span></span>
    
  

## <a name="step-3-create-an-external-list"></a><span data-ttu-id="dac0d-164">Schritt 3: Erstellen einer externen Liste</span><span class="sxs-lookup"><span data-stu-id="dac0d-164">Step 3: Create an external list</span></span>
<span data-ttu-id="dac0d-165"><a name="HowToCreateSimpleExternalListBasedPhoneApp_Step3"> </a></span><span class="sxs-lookup"><span data-stu-id="dac0d-165"></span></span>

<span data-ttu-id="dac0d-p105">Nun, dass Sie das BDC-Modell hochgeladen und Festlegen von Berechtigungen haben, können Sie eine externe Liste basierend auf den externen Inhaltstyp definiert im BDC-Modell erstellen. In diesem Schritt erstellen Sie eine externe Liste basierend auf den externen Inhaltstyp Customer definiert, in der Northwind-BDC-Modell, die, das Sie in  [Schritt 1: Hochladen einer BDC-Metadatenmodell](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md#HowToCreateSimpleExternalListBasedPhoneApp_Step1)hochgeladen.</span><span class="sxs-lookup"><span data-stu-id="dac0d-p105">Now that you've uploaded the BDC model and set permissions, you can create an external list based on the external content type defined in the BDC model. In this step, you will create an external list based on the Customer external content type defined in the Northwind BDC model you uploaded in  [Step 1: Upload a BDC metadata model](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md#HowToCreateSimpleExternalListBasedPhoneApp_Step1).</span></span>
  
    
    

1. <span data-ttu-id="dac0d-168">Navigieren Sie zu der SharePoint-Website, in dem die neue Liste angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="dac0d-168">Navigate to the SharePoint site where you want the new list.</span></span>
    
  
2. <span data-ttu-id="dac0d-169">Wählen Sie auf der Homepage der Website **Weitere**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-169">On the home page of the site, choose **More**.</span></span>
    
  
3. <span data-ttu-id="dac0d-170">Wählen Sie auf der Seite Apps **Hinzufügen einer App**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-170">On the Apps page, choose **Add an App**.</span></span>
    
  
4. <span data-ttu-id="dac0d-171">Klicken Sie auf der appseite hinzufügen bewegen Sie den Mauszeiger über die **Externe Liste**, und wählen Sie **Hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-171">On the Add an App page, hover over **External List** and choose **Add it**.</span></span>
    
  
5. <span data-ttu-id="dac0d-172">Geben Sie im Dialogfeld **Hinzufügen einer externen Liste** einen Namen wie „Customers“ in das Feld **Name** ein.</span><span class="sxs-lookup"><span data-stu-id="dac0d-172">In the **Adding an External List** dialog box, enter a name such asCustomers in the **Name** field.</span></span>
    
  
6. <span data-ttu-id="dac0d-173">Geben Sie im Feld **Externer Inhaltstyp** die externe Datenquelle an, die Sie in Schritt 1 hochgeladen haben.</span><span class="sxs-lookup"><span data-stu-id="dac0d-173">In the **External Content Type** box, specify the external data source that you uploaded in step 1.</span></span>
    
  
7. <span data-ttu-id="dac0d-174">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-174">Choose the **OK** button.</span></span>
    
  
8. <span data-ttu-id="dac0d-175">Wählen Sie auf der Seite Apps **Kundenliste** zum Anzeigen der Liste aus.</span><span class="sxs-lookup"><span data-stu-id="dac0d-175">On the Apps page, choose **Customers List** to view the list.</span></span>
    
  

## <a name="step-4-create-a-mobile-app-using-the-windows-phone-sharepoint-list-application-template"></a><span data-ttu-id="dac0d-176">Schritt 4: Erstellen einer mobilen app mithilfe der Windows Phone SharePoint List Application-Vorlage</span><span class="sxs-lookup"><span data-stu-id="dac0d-176">Step 4: Create a mobile app using the Windows Phone SharePoint List Application template</span></span>
<span data-ttu-id="dac0d-177"><a name="HowToCreateSimpleExternalListBasedPhoneApp_Step4"> </a></span><span class="sxs-lookup"><span data-stu-id="dac0d-177"></span></span>

<span data-ttu-id="dac0d-178">Die externe Liste bereit ist, und Sie können nun eine Windows Phone 7-app, die für die externe Liste verbindet Sie erstellt, in das  [Schritt 3: Erstellen einer externen Liste](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md#HowToCreateSimpleExternalListBasedPhoneApp_Step3) erstellen und Anzeigen von Kundendaten aus der Northwind-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="dac0d-178">Your external list is ready and you can now create a Windows Phone 7 app that connects to the external list you created in  [Step 3: Create an external list](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md#HowToCreateSimpleExternalListBasedPhoneApp_Step3) and display Customer data from the Northwind database.</span></span>
  
    
    

1. <span data-ttu-id="dac0d-179">Starten Sie Visual Studio 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="dac0d-179">Start Visual Studio 2010 Express.</span></span>
    
  
2. <span data-ttu-id="dac0d-p106">Wählen Sie auf der Menüleiste **Datei**, **Neues Projekt** aus. Das Dialogfeld **Neues Projekt** wird geöffnet.</span><span class="sxs-lookup"><span data-stu-id="dac0d-p106">On the menu bar, choose **File**, **New Project**. The **New Project** dialog box opens.</span></span>
    
  
3. <span data-ttu-id="dac0d-182">Klicken Sie im Dialogfeld **Neues Projekt** Wählen Sie **Visual c#**, wählen Sie **Silverlight für Windows Phone**, und wählen Sie dann auf **Windows Phone SharePoint List Application**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-182">In the **New Project** dialog box, choose **Visual C#**, choose **Silverlight for Windows Phone**, and then choose **Windows Phone SharePoint List Application**.</span></span>
    
  
4. <span data-ttu-id="dac0d-p107">Geben Sie einen Namen für das Projekt. Wir verwenden in diesem Beispiel CustomerApp , wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="dac0d-p107">Specify a name for the project. We use CustomerApp in this example, as shown in Figure 3.</span></span>
    
   <span data-ttu-id="dac0d-185">**Abbildung 3. Auswählen der Windows Phone SharePoint List Application-Vorlage in Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="dac0d-185">**Figure 3. Selecting the Windows Phone SharePoint List Application template in Visual Studio**</span></span>

  

  ![Vorlage für mobile SharePoint-Listen-App](../images/SP15Con_VisualStudioMobileSPListTemplate.png)
  

  

  
5. <span data-ttu-id="dac0d-187">Klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-187">Choose the **OK** button.</span></span>
    
  
6. <span data-ttu-id="dac0d-188">Geben Sie in der **SharePoint-Phone-Anwendungs-Assistent** die URL der SharePoint-Website, in der Sie die externe Liste erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="dac0d-188">In the **SharePoint Phone Application Wizard**, enter the URL of the SharePoint site in which you created the external list.</span></span>
    
  
7. <span data-ttu-id="dac0d-189">Wählen Sie die Liste der **Kunden** aus, und wählen Sie **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-189">Choose the **Customers** list, and choose **Next**.</span></span>
    
  
8. <span data-ttu-id="dac0d-190">Auf dem Bildschirm **Wählen Sie Ansichten** **Kundenliste Lese-** und wählen Sie **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-190">On the **Choose Views** screen, select **Customer Read List** and choose **Next**.</span></span>
    
  
9. <span data-ttu-id="dac0d-191">**Wählen Sie** auf dem Bildschirm **Wählen Sie Vorgänge**, und wählen Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-191">On the **Choose Operations** screen, choose **Display**, and then choose **Next**.</span></span>
    
  
10. <span data-ttu-id="dac0d-192">Klicken Sie auf dem Bildschirm **Wählen Sie Felder** Wählen Sie die Felder, die Sie verwenden oder in Ihre mobile app anzeigen möchten, und wählen Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-192">On the **Choose Fields** screen, select the fields you want to use or display in your mobile app, and then choose **Next**.</span></span>
    
  
11. <span data-ttu-id="dac0d-193">Ordnen Sie auf dem Bildschirm **Reihenfolge Felder** die Felder bei Bedarf neu an, und wählen Sie dann auf **Fertig stellen**.</span><span class="sxs-lookup"><span data-stu-id="dac0d-193">On the **Order Fields** screen, reorder the fields if needed, and then choose **Finish**.</span></span>
    
  
12. <span data-ttu-id="dac0d-194">Sie haben nun erfolgreich die app erstellt, die für die externe Liste verbindet.</span><span class="sxs-lookup"><span data-stu-id="dac0d-194">You've now successfully created the app that connects to the external list.</span></span>
    
  

## <a name="run-and-test-your-app"></a><span data-ttu-id="dac0d-195">Führen Sie aus und Testen Sie Ihrer app</span><span class="sxs-lookup"><span data-stu-id="dac0d-195">Run and test your app</span></span>
<span data-ttu-id="dac0d-196"><a name="HowToCreateSimpleExternalListBasedPhoneApp_RunAndTest"> </a></span><span class="sxs-lookup"><span data-stu-id="dac0d-196"></span></span>

<span data-ttu-id="dac0d-197">Nun, dass die app ausgeführt werden kann, können Sie ihn mit Phone-Emulator testen.</span><span class="sxs-lookup"><span data-stu-id="dac0d-197">Now that the app is ready to run, you can test it using phone emulator.</span></span>
  
    
    

1. <span data-ttu-id="dac0d-198">Wählen Sie in Visual Studio **Debuggen**, und klicken Sie dann Debuggen Sie **Starten**, oder drücken Sie F5.</span><span class="sxs-lookup"><span data-stu-id="dac0d-198">In Visual Studio, choose **Debug**, and then choose **Start Debugging**, or press F5.</span></span>
    
  
2. <span data-ttu-id="dac0d-p108">Wenn Sie aufgefordert werden, melden Sie sich mit den gleichen Benutzernamen und das Kennwort, das Sie zur Anmeldung bei der SharePoint-Website verwendet. Stellen Sie sicher, dass Sie über Administratorrechte verfügen.</span><span class="sxs-lookup"><span data-stu-id="dac0d-p108">When prompted, log in by using the same username and password that you used to log in to the SharePoint site. Ensure that you have admin rights.</span></span>
    
  
3. <span data-ttu-id="dac0d-201">Navigieren Sie in der Ergebnisliste Kunden wie in Abbildung 4 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="dac0d-201">Scroll through the resulting Customers list, as shown in Figure 4.</span></span>
    
   <span data-ttu-id="dac0d-202">**Abbildung 4. Mobile app Anzeigen von externen SharePoint-Liste**</span><span class="sxs-lookup"><span data-stu-id="dac0d-202">**Figure 4. Mobile app displaying SharePoint external list**</span></span>

  

  ![Demo für mobile BDC-App](../images/SPCon15_BDCMobileAppDemo.png)
  

  

  

> <span data-ttu-id="dac0d-204">**Hinweis:** Bei Verwendung des Assistenten für SharePoint-Listenvorlagen zum Erstellen einer mobilen App für eine externe Liste, die schreibgeschützte Felder enthält, lässt der vom Assistenten generierte Code nicht zu, dass Benutzer Elemente erstellen oder bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="dac0d-204">**Note** When you use the SharePoint List Template wizard to create a mobile app for an external list that has read-only fields, the code that is generated by the wizard does not allow users to create or edit items.</span></span> 
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="dac0d-205">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="dac0d-205">Additional resources</span></span>
<span data-ttu-id="dac0d-206"><a name="SP15createmobileapp_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="dac0d-206"></span></span>


  
    
    

-  [<span data-ttu-id="dac0d-207">Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen</span><span class="sxs-lookup"><span data-stu-id="dac0d-207">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="dac0d-208">Überblick über Anwendungsvorlagen für Windows Phone SharePoint in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dac0d-208">Overview of Windows Phone SharePoint application templates in Visual Studio</span></span>](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md)
    
  
-  <span data-ttu-id="dac0d-209">
  [Vorgehensweise: Erstellen externer Listen in SharePoint](http://msdn.microsoft.com/de-de/library/ee558778.aspx)</span><span class="sxs-lookup"><span data-stu-id="dac0d-209">[How to: Create External Lists in SharePoint](http://msdn.microsoft.com/de-de/library/ee558778.aspx)</span></span>
    
  
-  [<span data-ttu-id="dac0d-210">Vorgehensweise: Erstellen eine Windows Phone SharePoint Liste app</span><span class="sxs-lookup"><span data-stu-id="dac0d-210">How to: Create a Windows Phone SharePoint list app</span></span>](how-to-create-a-windows-phone-sharepoint-list-app.md)
    
  
-  [<span data-ttu-id="dac0d-211">Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint</span><span class="sxs-lookup"><span data-stu-id="dac0d-211">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="dac0d-212">Windows Phone SDK 7.1</span><span class="sxs-lookup"><span data-stu-id="dac0d-212">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="dac0d-213">Microsoft SharePoint SDK für Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="dac0d-213">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

