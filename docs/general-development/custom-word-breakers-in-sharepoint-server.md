---
title: "Benutzerdefinierte Wörtertrennungen in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d18b48d4-987c-4228-9932-30d5b30f86a2
ms.openlocfilehash: 52ee69b816c55f49334d3309e10b331551284770
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="custom-word-breakers-in-sharepoint"></a>Benutzerdefinierte Wörtertrennungen in SharePoint
In diesem Artikel finden Sie Informationen zu Wörtertrennungen in SharePoint. Die Wörtertrennung ist eines der wichtigsten Features bei der Verarbeitung natürlicher Sprache (Natural Language Processing, NLP), die Suchläufe ermöglichen und Suchergebnisse (oder Abrufe) verbessern. Durch Wörtertrennungen wird ein Textfluss in einzelne Wörter oder Token aufgeteilt, die Sie als Basis für die weitere Sprachverarbeitung verwenden können. Wörtertrennungen sind sprachspezifisch. Zusätzlich zu integrierten Wörtertrennungen ermöglicht die Suche in SharePoint die Verwendung von benutzerdefinierten Wörtertrennungen, sodass Benutzer das Wörtertrennungsverhalten entsprechend ihren Anforderungen anpassen können. Eine Liste der Sprachen, die die Anpassung der Wörtertrennung unterstützt, finden Sie unter [Unterstützte Sprachen für die Anpassung der Wörtertrennung in SharePoint](#SP15_SupportedLanguages).
  
    
    

Informationen zum Schreiben einer Wörtertrennung finden Sie in den folgenden Artikeln: 
-  [Implementieren von einem Worttrennmodul](http://msdn.microsoft.com/de-DE/library/ms693186%28v=vs.85%29.aspx)
    
  
-  [IWordBreaker-Schnittstelle](http://msdn.microsoft.com/de-DE/library/ms691079%28v=vs.85%29.aspx)
    
  

## <a name="how-to-switch-to-a-custom-word-breaker-in-sharepoint"></a>Wechseln zu einer benutzerdefinierten Wörtertrennung in SharePoint
<a name="SP15wordbreaker_howto"> </a>


> **Vorsicht:** Beim Ersetzen vorhandener Wörtertrennungen ändern Sie die Registrierung auf eigene Verantwortung. Es können schwerwiegende Probleme auftreten, wenn Sie die Registrierung nicht ordnungsgemäß mithilfe des Registrierungs-Editors oder einer anderen Methode ändern. Diese Probleme erfordern möglicherweise eine Neuinstallation des Betriebssystems. Microsoft kann nicht sicherstellen, dass diese Probleme behoben werden können. Der Wechsel zu einer anderen Wörtertrennung kann auch schwerwiegende Probleme beim Indizieren und Abfragen verursachen. Bevor Sie die Registrierung ändern, sichern Sie die Registrierung, und stellen Sie sicher, dass Sie wissen, wie Sie die Registrierung im Falle ein Problems wiederherstellen. 
  
    
    

Führen Sie die folgenden Schritte aus, ersetzen Sie das vorhandene Worttrennmodul mit einem benutzerdefinierten Worttrennmodul oder ersetzen das vorhandene Worttrennmodul mit einem Worttrennmodul in einer anderen Sprache.
  
    
    

1. Öffnen Sie den Registrierungs-Editor wie folgt:
    
1. Wählen Sie **Start**, und wählen Sie dann **Run**.
    
  
2. Klicken Sie im Dialogfeld **Open** Geben Sie **Regedit**, und wählen Sie dann **OK**.
    
  
2. Wählen Sie im Registrierungs-Editor den folgenden Registrierungsunterschlüssel:
    
    **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Office Server\\15.0\\Search\\Setup\\ContentIndexCommon\\LanguageResources\\Default\\** _language from the list below_
    
  
3. Klicken Sie im rechten Bereich öffnen Sie das Kontextmenü für den Registrierungswert **WBDLLPathOverride**, und wählen Sie **Modify**.
    
  
4. Klicken Sie im Dialogfeld **Edit String** **Value data** Sie im Feld Geben Sie den Pfad zu Ihrer benutzerdefinierten Worttrennmodul DLL-Datei, und wählen Sie dann **OK**. Die neue DLL sollte sich in demselben Pfad wie die vorhandene DLL befinden, die ersetzt wird.
    
  
5. Klicken Sie im rechten Bereich öffnen Sie das Kontextmenü für den Registrierungswert **WBreakerClass**, und wählen Sie **Modify**.
    
  
6. Klicken Sie im Dialogfeld **Edit String** **Value data** Sie im Feld Geben Sie die Klassen-ID der benutzerdefinierten Worttrennmodul, und wählen Sie dann **OK**.
    
  
7. Starten Sie den SharePoint-Suchhostcontroller und SharePoint neu.
    
  
8. Führen Sie eine vollständige erneute Durchforstung durch.
    
  

## <a name="supported-languages-for-word-breaker-customizations-in-sharepoint"></a>Unterstützte Sprachen für die Anpassung der Wörtertrennung in SharePoint
<a name="SP15_SupportedLanguages"> </a>

Die folgenden Sprachen werden für die Anpassung von Word wörtertrennung unterstützt:
  
    
    
Arabisch
  
    
    
Bengali
  
    
    
Bulgarisch
  
    
    
Katalanisch
  
    
    
Chinesisch (Volksrepublik China)
  
    
    
Chinesisch (Taiwan)
  
    
    
Kroatisch
  
    
    
Tschechisch
  
    
    
Dänisch
  
    
    
Niederländisch (Niederländisch)
  
    
    
Deutsch (Deutschland)
  
    
    
Estnisch
  
    
    
Finnisch
  
    
    
Französisch (Standard)
  
    
    
Deutsch (Standard)
  
    
    
Griechisch
  
    
    
Gudscharati
  
    
    
Hebräisch
  
    
    
Hindi
  
    
    
Ungarisch
  
    
    
Isländisch
  
    
    
Indonesisch
  
    
    
Italienisch (Standard)
  
    
    
Japanisch
  
    
    
Kannada
  
    
    
Kasachisch
  
    
    
Koreanisch
  
    
    
Lettisch
  
    
    
Litauisch
  
    
    
Malaiisch
  
    
    
Malayalam
  
    
    
Marathi
  
    
    
Norwegisch
  
    
    
Polnisch
  
    
    
Portugiesisch (Portugiesisch)
  
    
    
Punjabi
  
    
    
Rumänisch
  
    
    
Russisch
  
    
    
Serbisch (Kyrillisch)
  
    
    
Slowakisch
  
    
    
Slowenisch
  
    
    
Spanisch (Moderne Sortierung)
  
    
    
Schwedisch
  
    
    
Tamil
  
    
    
Telugu
  
    
    
Thailändisch
  
    
    
Türkisch
  
    
    
Ukrainisch
  
    
    
Urdu
  
    
    
Vietnamesisch
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="SP15wordbreakers_addresources"> </a>


-  [Konfigurieren der Suche in SharePoint](configure-search-in-sharepoint.md)
    
  
-  [Implementieren von einem Worttrennmodul](http://msdn.microsoft.com/de-DE/library/ms693186%28v=vs.85%29.aspx)
    
  
-  [IWordBreaker-Schnittstelle](http://msdn.microsoft.com/de-DE/library/ms691079%28v=vs.85%29.aspx)
    
  

