---
title: "Angeben einer Vorlage für eine Dokumentbibliothek in einem Cloud-Business-Add-In"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: b9505ee15250d4a69a3a79b8d3a4e4893ff5e298
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="provide-a-template-for-a-document-library-in-a-cloud-business-add-in"></a>Angeben einer Vorlage für eine Dokumentbibliothek in einem Cloud-Business-Add-In
Zusätzlich zu den Office-Vorlagen, die beim Hinzufügen eines Dokuments zu einer SharePoint-Dokumentbibliothek verfügbar sind, können Sie auch Ihre eigenen Vorlagen verwenden. Sie haben möglicherweise Ihre eigene Verkaufsangebotsvorlage, die Sie verwenden möchten, wenn neue Aufträge hinzugefügt werden.
 

 **Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).
 


## 

Wenn Sie dies noch nicht getan haben, ordnen Sie Ihrem Cloud-Business-Add-In eine Dokumentbibliothek hinzu. Weitere Informationen finden Sie unter [Zuordnen einer Dokumentbibliothek zu einer Entität](associate-a-document-library-with-an-entity.md).
 

 

### <a name="to-add-a-template"></a>So fügen Sie eine Vorlage hinzu


1. Wechseln Sie zu Ihrer SharePoint-Entwicklerwebsite, und klicken Sie anschließend auf der Seite **Entwickler** auf **Websiteinhalte**.
    
 
2. Klicken Sie auf der Seite **Websiteinhalte** auf **Einstellungen**, wie in Abbildung 1 dargestellt.
    
    **Abbildung 1. Der Link „Einstellungen“**

 

  ![Link zu Websiteeinstellungen](../images/CBA_IM_8b.PNG)
 

 

 
3. Klicken Sie auf der Seite **Websiteeinstellungen** in der Liste **Web-Designer-Kataloge** auf **Websiteinhaltstypen**, wie in Abbildung 2 dargestellt.
    
    **Abbildung 2. Der Link „Websiteinhaltstypen“**

 

  ![Link „Websiteinhaltstypen“](../images/CBA_IM_26.PNG)
 

 

 
4. Klicken Sie auf der Seite **Websiteinhaltstypen** auf **Erstellen**, wie in Abbildung 3 dargestellt.
    
    **Abbildung 3. Der Link „Erstellen“**

 

  ![Link „Erstellen“](../images/CBA_IM_27.PNG)
 

 

 
5. Geben Sie auf der Seite **Neuer Websiteinhaltstyp** einen Namen und eine Beschreibung für Ihre Vorlage ein. Wählen Sie bei **Übergeordneter Inhaltstyp** **Dokumentinhaltstyp** und **Dokument** aus, wie in Abbildung 4 dargestellt.
    
    **Abbilgung 4. Auswahloptionen für „Übergeordneter Inhaltstyp“**

 

  ![Auswahloptionen für „Übergeordneter Inhaltstyp“](../images/CBA_IM_28.PNG)
 

 

 
6. Klicken Sie im Abschnitt **Gruppe** in der Liste **Vorhandene Gruppe** auf **Dokumentinhaltstypen**, wie in Abbildung 5 dargestellt, und anschließend auf **OK**.
    
    **Abbildung 5. Gruppeneinstellung**

 

  ![Gruppeneinstellung](../images/CBA_IM_28a.PNG)
 

 

 
7. Klicken Sie auf der Seite **Websiteinhaltstyp** auf **Erweiterte Einstellungen**.
    
 
8. Geben Sie auf der Seite **Erweiterte Einstellungen** entweder die URL einer vorhandenen Dokumentvorlage ein oder laden Sie eine neue Dokumentvorlage hoch, wie in Abbildung 6 dargestellt, und klicken Sie anschließend auf **OK**.
    
    **Abbildung 6. Angeben der Dokumentvorlage**

 

  ![Angeben der Dokumentvorlage](../images/CBA_IM_29.PNG)
 

 

 
9. Wechseln Sie zur Seite **Websiteinhalte**, klicken Sie auf Ihre Dokumentbibliothek, und wechseln Sie dann auf die Seite **Einstellungen**.
    
 
10. Klicken Sie auf der Seite **Einstellungen** auf **Aus vorhandenen Websiteinhaltstypen hinzufügen**.
    
 
11. Fügen Sie Ihre Vorlage auf der Seite **Inhaltstypen hinzufügen** wie in Abbildung 7 dargestellt hinzu, und klicken Sie anschließend auf **OK**.
    
    **Abbildung 7. Hinzufügen der Vorlage**

 

  ![Hinzufügen der Vorlage](../images/CBA_IM_29a.PNG)
 

 

 
12. Führen Sie Ihr Add-In aus, und fügen Sie ein Dokument hinzu. Ihre Vorlage sollte im Dialogfeld **Neue Datei erstellen** angezeigt werden, wie in Abbildung 8 dargestellt.
    
    **Abbildung 8. Das Dialogfeld „Neue Datei erstellen“ mit der neuen Vorlage**

 

  ![Das Dialogfeld „Neue Datei erstellen“ mit der neuen Vorlage](../images/CBA_IM_30.PNG)
 

 

 

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Entwickeln von Cloud-Business-Add-Ins](develop-cloud-business-add-ins.md)
    
 
-  [Zuordnen einer Dokumentbibliothek zu einer Entität](associate-a-document-library-with-an-entity.md)
    
 

