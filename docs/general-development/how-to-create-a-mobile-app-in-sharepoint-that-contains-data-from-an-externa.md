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
# <a name="how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-external-data-source"></a>Vorgehensweise: Erstellen eine mobile app in SharePoint, die Daten aus einer externen Datenquelle enthält.
Hier erfahren Sie, wie Sie eine einfache mobile app in SharePoint erstellen, die Daten aus externen Datenquelle enthält, indem Sie mithilfe von Business Connectivity Services und Herstellen einer Verbindung mit einer externen Liste. SharePoint ermöglicht Ihnen, mobile Anwendungen zu erstellen, mit die externe Daten in Datenbanken, Unternehmensanwendungen und Web 2.0-Diensten mithilfe von Business Connectivity Services zugreifen können. Sie können auch vollständigen Interaktion mit den externen Daten einschließlich rückschreibfunktionen aus dem mobilen Gerät bereitstellen. Zu diesem Zweck erstellen von apps, die mit externen Listen, die einen besonderen Typ von Listen in SharePoint sind herzustellen, die basieren auf externe Inhaltstypen und Daten aus externen Systemen enthalten. Die neue SharePoint-Liste für Windows Phone-Vorlage in Visual Studio 2010 Express können Sie schnell und problemlos Erstellen von apps für Windows Phone, die mit externen Listen eine Verbindung herstellt. Beispielsweise können Sie eine Windows Phone-app erstellen, die den Produktkatalog für eine Inventarliste in SharePoint auf das Telefon für die Vertriebsmitarbeiter bereitstellt. In diesem Thema wird das Erstellen einer Windows Phone-app, die externe Daten aus der Northwind-Beispieldatenbank anzeigt, indem es eine Verbindung mit einer externen Liste in SharePoint. Beachten Sie, dass in diesem Beispiel wird die externe Liste zu Northwind-Datenbank mit einer benutzerdefinierten OData-Dienst herstellt. Es ist jedoch möglich, Verbinden mit Datenbanken direkt als auch für alle externen Systeme, die von Business Connectivity Services, mithilfe von externen Listen unterstützt wird. Mit der neuen SharePoint-Liste Vorlage in Visual Studio erstellen Sie eine mobile app, die auf eine externe Liste auf einer SharePoint-Website zugreifen können. Dieser Artikel enthält eine schrittweise Anleitung, die mit einer externen Business Data Connectivity (BDC)-Dienst Modell hochladen beginnt und endet mit der neuen mobilen Anwendung zu testen.
  
    
    


> **Wichtig:** Wenn Sie eine App für Windows Phone 8 entwickeln, müssen Sie Visual Studio Express 2012 anstelle von Visual Studio 2010 Express verwenden. Mit Ausnahme der Entwicklungsumgebung gelten alle Informationen in diesem Artikel für das Erstellen von Apps sowohl auf Windows Phone 8 als auch auf Windows Phone 7. Weitere Informationen finden Sie unter [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung mobiler Apps für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md). 
  
    
    


## <a name="prerequisites-for-creating-a-mobile-app-that-contains-external-data"></a>Voraussetzungen für die Erstellung einer mobilen App, die externe Daten enthält
<a name="SP15Createmobileapp_prereq"> </a>


- Eine SharePoint Installation mit Administratorrechten zum Hochladen des BDC-Modells für die Northwind-Datenbank und einer SharePoint-Website, in dem Sie die externe Liste erstellen
    
  
- Microsoft Visual Studio Express mit den neuen SharePoint phonevorlagen aus  [Microsoft SharePoint SDK for Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  
- Das BDC-Modell für unsere exampleNorthwind_oData.bdmc (Laden von  [SharePoint: erstellen eine einfachen externen listenbasierten Phone-app](http://code.msdn.microsoft.com/sharepoint/SharePoint-Create-a-88800202))
    
  
- Eine SharePoint Installation mit Administratorrechten zum Hochladen des BDC-Modells für die Northwind-Datenbank und einer SharePoint-Website, in dem Sie die externe Liste erstellen
    
  

## <a name="step-1-upload-a-bdc-metadata-model"></a>Schritt 1: Hochladen einer BDC-Metadatenmodell
<a name="HowToCreateSimpleExternalListBasedPhoneApp_Step1"> </a>

Ein BDC-Modell ist das Herzstück von Business Connectivity Services. Es ist eine XML-Datei, die Datenstrukturen wie **Entity** (externer Inhaltstyp) und **-Methode** wird verwendet, um die abstrakten komplexen Details über das externe System. Es wird automatisch generierten beim Erstellen eines externen Inhaltstyps mit SharePoint Designer und für einige Datenquellentypen solche .NET und OData-Quellen, Sie das BDC-Modell manuell oder mithilfe von Visual Studio erstellen müssen. Wenn Sie ein BDC-Modell für den BDC-Metadatenspeicher mithilfe der SharePoint-Zentraladministration hochladen, können die externen Inhaltstypen im Modell definierten verwendet werden, zum Erstellen von externer Listen in SharePoint Listen darstellen, die Daten aus dem zugrunde liegenden externen System anzeigen. In diesem Schritt werden das Northwind-Beispiel BDC-Modell für den Metadatenspeicher hochladen mithilfe der SharePoint-Zentraladministration.
  
    
    

1. Navigieren Sie zur Zentraladministration.
    
  
2. Wählen Sie **Anwendungsverwaltung**, und wählen Sie dann auf **Dienstanwendungen verwalten**.
    
  
3. Wählen Sie auf der Seite „Dienstanwendung“ **Business Data Connectivity-Dienst** aus.
    
  
4. Wählen Sie im Menüband in der BDC-Dienstanwendung **Importieren**.
    
  
5. Wählen Sie auf der Seite BDC-Modell importieren **Business Data Connectivity-Dienst**.
    
  
6. Wählen Sie auf dem Menüband in der BDC-Dienstanwendung **Importieren**.
    
  
7. Wählen Sie **Durchsuchen** aus, auf der Seite BDC-Modell importieren.
    
  
8. Klicken Sie im Dialogfeld **Datei zum Hochladen auswählen** suchen Sie die Datei Northwind_oData.bdcm, und wählen Sie dann auf **Öffnen**.
    
  
9. Nachdem die Datei importiert wurde, wählen Sie die Schaltfläche **OK**.
    
  

## <a name="step-2-grant-permissions"></a>Schritt 2: Gewähren von Berechtigungen
<a name="HowToCreateSimpleExternalListBasedPhoneApp_Step2"> </a>

Als Nächstes müssen Sie zum Festlegen von Berechtigungen für das BDC-Modell, um anzugeben, die im Modell beschriebenen Methoden ausgeführt werden kann. Dies ist ein erforderlicher Schritt. Es wird empfohlen, dass Sie bestimmte Berechtigungen, jedem Benutzer oder Gruppe, die sie so benötigt erteilen, dass die Anmeldeinformationen der geringsten Rechte zum Ausführen der erforderlichen Aufgaben erforderlich. Weitere Informationen zum Festlegen von Berechtigungen finden Sie unter Übersicht über Business Connectivity Service-Berechtigungen in  [Business Connectivity Services-Sicherheit (Übersicht) (SharePoint Server 2010)](http://technet.microsoft.com/en-us/library/ee661740.aspx). In diesem Schritt erteilen Sie die Berechtigung an sich selbst zum Ausführen der Methods beschrieben, die in der Northwind-Beispiel BDC-Modell.
  
    
    

1. Navigieren Sie zur Zentraladministration.
    
  
2. Wählen Sie **Anwendungsverwaltung**, und wählen Sie dann auf **Dienstanwendungen verwalten**.
    
  
3. Wählen Sie auf der Seite Dienstanwendungen die **Business Data Connectivity-Dienst**.
    
  
4. Wählen Sie im Menüband der Dropdown Liste in der Gruppe **Ansicht** **BDC-Modelle**.
    
  
5. In der Liste der BDC-Modelle mit dem Mauszeiger Northwind_oData.bdcm, und wählen Sie **Berechtigungen festlegen**, wie in Abbildung 1 dargestellt.
    
   **Abbildung 1. Auswahl von Berechtigungen für BDC-Modell**

  

  ![Auswählen von Berechtigungen für BDC-Modell](../images/SPCon15_BDC_SetPermissions_ODataWebNorthWind.png)
  

  

  
6. Wählen Sie die Schaltfläche **Durchsuchen**, klicken Sie im Dialogfeld **Objektberechtigungen festlegen**.
    
  
7. Klicken Sie im Dialogfeld **Personen und Gruppen auswählen** für Ihr Konto zu suchen Sie, und wählen Sie die Schaltfläche **OK**.
    
  
8. Wählen Sie die Berechtigungen für das **Bearbeiten**, **Ausführen**, **Auswählbar In Clients** und **Berechtigungen festlegen**, wie in Abbildung 2 dargestellt.
    
   **Abbildung 2. Festlegen von Berechtigungen für Gruppenrichtlinienobjekte**

  

  ![Festlegen von BDC-Objektberechtigungen](../images/SPCon15_Setting_BDCObjectPermission_DialogueBox.png)
  

  

  
9. Klicken Sie auf **OK**.
    
  
10. Wählen Sie im Menüband **Externe Inhaltstypen** aus der Dropdown Liste in der Gruppe **Ansicht**.
    
  
11. In der Liste der externen Inhaltstypen mit dem Mauszeiger **Kunden**, und wählen Sie dann auf **Berechtigungen festlegen**.
    
  
12. Wählen Sie die Schaltfläche **Durchsuchen**, und suchen Sie nach Ihrem Konto, klicken Sie im Dialogfeld **Objektberechtigungen festlegen**.
    
  
13. Klicken Sie im Dialogfeld **Objektberechtigungen festlegen** auf **Hinzufügen**, und wählen Sie die Berechtigungen für das **Bearbeiten**, **Ausführen**, **Auswählbar In Clients** und **Berechtigungen festlegen**.
    
  
14. Stellen Sie sicher, dass das Kontrollkästchen **Berechtigungen weitergeben** aktiviert ist.
    
  
15. Klicken Sie auf **OK**.
    
  

## <a name="step-3-create-an-external-list"></a>Schritt 3: Erstellen einer externen Liste
<a name="HowToCreateSimpleExternalListBasedPhoneApp_Step3"> </a>

Nun, dass Sie das BDC-Modell hochgeladen und Festlegen von Berechtigungen haben, können Sie eine externe Liste basierend auf den externen Inhaltstyp definiert im BDC-Modell erstellen. In diesem Schritt erstellen Sie eine externe Liste basierend auf den externen Inhaltstyp Customer definiert, in der Northwind-BDC-Modell, die, das Sie in  [Schritt 1: Hochladen einer BDC-Metadatenmodell](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md#HowToCreateSimpleExternalListBasedPhoneApp_Step1)hochgeladen.
  
    
    

1. Navigieren Sie zu der SharePoint-Website, in dem die neue Liste angezeigt werden soll.
    
  
2. Wählen Sie auf der Homepage der Website **Weitere**.
    
  
3. Wählen Sie auf der Seite Apps **Hinzufügen einer App**.
    
  
4. Klicken Sie auf der appseite hinzufügen bewegen Sie den Mauszeiger über die **Externe Liste**, und wählen Sie **Hinzufügen**.
    
  
5. Geben Sie im Dialogfeld **Hinzufügen einer externen Liste** einen Namen wie „Customers“ in das Feld **Name** ein.
    
  
6. Geben Sie im Feld **Externer Inhaltstyp** die externe Datenquelle an, die Sie in Schritt 1 hochgeladen haben.
    
  
7. Klicken Sie auf **OK**.
    
  
8. Wählen Sie auf der Seite Apps **Kundenliste** zum Anzeigen der Liste aus.
    
  

## <a name="step-4-create-a-mobile-app-using-the-windows-phone-sharepoint-list-application-template"></a>Schritt 4: Erstellen einer mobilen app mithilfe der Windows Phone SharePoint List Application-Vorlage
<a name="HowToCreateSimpleExternalListBasedPhoneApp_Step4"> </a>

Die externe Liste bereit ist, und Sie können nun eine Windows Phone 7-app, die für die externe Liste verbindet Sie erstellt, in das  [Schritt 3: Erstellen einer externen Liste](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md#HowToCreateSimpleExternalListBasedPhoneApp_Step3) erstellen und Anzeigen von Kundendaten aus der Northwind-Datenbank.
  
    
    

1. Starten Sie Visual Studio 2010 Express.
    
  
2. Wählen Sie auf der Menüleiste **Datei**, **Neues Projekt** aus. Das Dialogfeld **Neues Projekt** wird geöffnet.
    
  
3. Klicken Sie im Dialogfeld **Neues Projekt** Wählen Sie **Visual c#**, wählen Sie **Silverlight für Windows Phone**, und wählen Sie dann auf **Windows Phone SharePoint List Application**.
    
  
4. Geben Sie einen Namen für das Projekt. Wir verwenden in diesem Beispiel CustomerApp , wie in Abbildung 3 dargestellt.
    
   **Abbildung 3. Auswählen der Windows Phone SharePoint List Application-Vorlage in Visual Studio**

  

  ![Vorlage für mobile SharePoint-Listen-App](../images/SP15Con_VisualStudioMobileSPListTemplate.png)
  

  

  
5. Klicken Sie auf **OK**.
    
  
6. Geben Sie in der **SharePoint-Phone-Anwendungs-Assistent** die URL der SharePoint-Website, in der Sie die externe Liste erstellt haben.
    
  
7. Wählen Sie die Liste der **Kunden** aus, und wählen Sie **Weiter**.
    
  
8. Auf dem Bildschirm **Wählen Sie Ansichten** **Kundenliste Lese-** und wählen Sie **Weiter**.
    
  
9. **Wählen Sie** auf dem Bildschirm **Wählen Sie Vorgänge**, und wählen Sie dann auf **Weiter**.
    
  
10. Klicken Sie auf dem Bildschirm **Wählen Sie Felder** Wählen Sie die Felder, die Sie verwenden oder in Ihre mobile app anzeigen möchten, und wählen Sie dann auf **Weiter**.
    
  
11. Ordnen Sie auf dem Bildschirm **Reihenfolge Felder** die Felder bei Bedarf neu an, und wählen Sie dann auf **Fertig stellen**.
    
  
12. Sie haben nun erfolgreich die app erstellt, die für die externe Liste verbindet.
    
  

## <a name="run-and-test-your-app"></a>Führen Sie aus und Testen Sie Ihrer app
<a name="HowToCreateSimpleExternalListBasedPhoneApp_RunAndTest"> </a>

Nun, dass die app ausgeführt werden kann, können Sie ihn mit Phone-Emulator testen.
  
    
    

1. Wählen Sie in Visual Studio **Debuggen**, und klicken Sie dann Debuggen Sie **Starten**, oder drücken Sie F5.
    
  
2. Wenn Sie aufgefordert werden, melden Sie sich mit den gleichen Benutzernamen und das Kennwort, das Sie zur Anmeldung bei der SharePoint-Website verwendet. Stellen Sie sicher, dass Sie über Administratorrechte verfügen.
    
  
3. Navigieren Sie in der Ergebnisliste Kunden wie in Abbildung 4 dargestellt.
    
   **Abbildung 4. Mobile app Anzeigen von externen SharePoint-Liste**

  

  ![Demo für mobile BDC-App](../images/SPCon15_BDCMobileAppDemo.png)
  

  

  

> **Hinweis:** Bei Verwendung des Assistenten für SharePoint-Listenvorlagen zum Erstellen einer mobilen App für eine externe Liste, die schreibgeschützte Felder enthält, lässt der vom Assistenten generierte Code nicht zu, dass Benutzer Elemente erstellen oder bearbeiten. 
  
    
    


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="SP15createmobileapp_addlresources"> </a>


  
    
    

-  [Erstellen von Windows Phone-Apps, die auf SharePoint zugreifen](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Überblick über Anwendungsvorlagen für Windows Phone SharePoint in Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md)
    
  
-  
  [Vorgehensweise: Erstellen externer Listen in SharePoint](http://msdn.microsoft.com/en-us/library/ee558778.aspx)
    
  
-  [Vorgehensweise: Erstellen eine Windows Phone SharePoint Liste app](how-to-create-a-windows-phone-sharepoint-list-app.md)
    
  
-  [Vorgehensweise: Einrichten einer Umgebung für die Entwicklung von mobilen Anwendungen für SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Windows Phone SDK 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Microsoft SharePoint SDK für Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

