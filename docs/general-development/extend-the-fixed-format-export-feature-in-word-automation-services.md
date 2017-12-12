---
title: Erweitern der Exportfunktion mit festgelegtem Format in Word Automation Services
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d8375505-432e-438e-971b-221a1d9bb601
ms.openlocfilehash: aad6cd52499a1599b15625d245e48eb46a7862be
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="extend-the-fixed-format-export-feature-in-word-automation-services"></a>Erweitern der Exportfunktion mit festgelegtem Format in Word Automation Services
Erweitern Sie Word Automation Services in Microsoft Office 2013 ersetzen Sie die Bibliothek, die von der Funktion zum Exportieren in feste Formate verwendet.
## <a name="introduction-to-the-word-file-conversion-service-fixed-format-export-feature"></a>Einführung in die Word-Datei Konvertierung Service mit festem Format export feature

In diesem Artikel wird beschrieben, wie so erweitern Sie das Feature exportieren in feste Formate von Word Automation Services zu verschiedenen exportieren in feste Formate-DLLs verwenden, sodass Drittanbieter-Entwickler von Microsoft bereitgestellte ersetzen können. Dieser Mechanismus ist erforderlich und des Office-Clients mit festem Format Erweiterbarkeit COM-Schnittstelle erweitert. Weitere Informationen finden Sie unter  [Extending the Office 2007 Fixed-Format Export Feature](http://msdn.microsoft.com/de-DE/library/aa338206.aspx).
  
    
    

## <a name="discovery"></a>Suche

Word Automation Services können Drittanbieter-Entwickler ersetzen Sie einen oder beide der Ausgaben mit festem Format unterstützt:
  
    
    

- PDF
    
  
- XPS
    
  
Wenn Sie die Formate ersetzen möchten, muss die jeweilige DLL in demselben Verzeichnis abgelegt werden wie die Kernbibliothek (Sword.dll) für Word Automation Services (Installationspfad: \<\<Installationsstammverzeichnis\>\>\\WebServices\\ConversionService\\Bin\\Converter\\) und den in Tabelle 1 angegebenen Dateinamen haben.
  
    
    

**Tabelle 1: Dateinamen der DLL-Dateien für Exporte mit festgelegtem Format**


|**Format**|**Dateiname**|
|:-----|:-----|
|PDF  <br/> |Renderpdf.dll  <br/> |
|XPS  <br/> |Renderxps.dll  <br/> |
   

## <a name="initialization"></a>Initialisierung

Eine Methode mit der folgenden Signatur muss die DLL-Datei exportiert werden.
  
    
    

```

HRESULT HrGetDocExporter (
IMsoDocExporter **ppimde,
IMsoServerFileManagerSite *psfms,
PFNKeepAlive pfnKeepAlive
)
```

Die Funktion erfordert die DLL zwei Schnittstellen und einer Methodenzeiger, die im folgenden Abschnitt beschrieben bereitgestellt.
  
    
    
Wenn die Funktion Fehler zurückgibt wird der Dienst nicht auf die Microsoft bereitgestellten Exporter (engl.) zurückgreifen. Stattdessen meldet der Dienst die Konvertierung als fehlgeschlagen ist.
  
    
    

## <a name="imsodocexporter"></a>IMsoDocExporter

Die **IMsoDocExporter** -Schnittstelle ist identisch mit der vorhandenen-Schnittstelle auf MSDN dokumentiert. Weitere Informationen finden Sie unter [Extending the Office 2007 Fixed-Format Export Feature](http://msdn.microsoft.com/de-DE/library/aa338206.aspx). Wenn die frühere Methode Erfolg zurückgegeben wird, werden diese Schnittstelle die Konvertierung durchgeführt.
  
    
    
Über die Anforderungen in der oben genannten Artikel beschrieben wird müssen Entwickler von DLLs exportieren in feste Formate Beachten Sie, dass der Dienst den bereitgestellten **IMsoDocExporter** in einem anderen Thread von der Anrufen kann, auf dem der Dienst **HrGetDocExporter**bezeichnet. Die DLL muss dies ohne den Anruf wieder an der Thread, **HrGetDocExporter**, aufgerufen, da der Dienst wird ein Nachrichtensystem nicht ausgeführt, und der gemarshallte Anruf nie erhalten über (was eine hängen und weitere Fehler) gemarshallt behandeln können.
  
    
    

## <a name="imsoserverfilemanagersite"></a>IMsoServerFileManagerSite

Die IMsoServerFileManagerSite-Schnittstelle wird wie folgt definiert.
  
    
    

```

#undef  INTERFACE
#define INTERFACE  IMsoServerFileManagerSite
DECLARE_INTERFACE(IMsoServerFileManagerSite)
{
STDMETHOD_(BOOL, FGetHandle) (const WCHAR *pwzFileName, HANDLE *phFile, BOOL fRead, BOOL fWrite) PURE;
STDMETHOD_(BOOL, FCloseHandle) (HANDLE hFile) PURE;
};
```

Diese Schnittstelle stellt die folgenden Methoden.
  
    
    

**In Tabelle 2. Methoden verfügbar gemacht werden, die von der IMsoServerFileManagerSite-Schnittstelle**

|||
|:-----|:-----|
|Methode  <br/> |Beschreibung  <br/> |
|**FGetHandle** <br/> |Ruft ein Dateihandle ab.  <br/> |
|**FCloseHandle** <br/> |Gibt ein Dateihandle frei.  <br/> |
   
Diese Schnittstelle erbt nicht von **IUnknown**. Die DLL-Datei exportieren in feste Formate darf entsprechend, einen Verweis auf dieses für die Lebensdauer bleiben.
  
    
    

### <a name="fgethandle"></a>FGetHandle

Das mit festem Format exportieren DLL-Aufrufe dieser Funktion zum Abrufen des Dateihandles zum Schreiben in. Es muss nicht versuchen Sie zum Öffnen von Dateien über einen anderen Mechanismus, da der Dienst in einer stark eingeschränkten Umgebung ohne Zugriff auf die meisten Stellen im Dateisystem ausgeführt wird.
  
    
    

```

BOOL FGetHandle (
const WCHAR *pwzFile,
HANDLE *phFile,
BOOL fRead,
BOOL fWrite
)
```


**Tabelle 3. FGetHandle-Parameter**

|||
|:-----|:-----|
|Parameter  <br/> |Beschreibung  <br/> |
|**pwzFile** <br/> |Gibt den Namen der Datei, das mit festem Format exportieren DLL öffnen möchte. Dies muss keinen vollständigen Dateipfad - müssen sie nur einen Dateinamen ein (beispielsweise Output.pdf) angeben.  <br/> |
|**phFile** <br/> |Gibt das Handle für die angegebene Datei an, ob die Datei erfolgreich geöffnet wird. Das Exportieren in feste Formate DLL können Sie dieses HANDLE in normalen Dateivorgänge, bis es geschlossen wird durch Aufrufen der **FCloseHandle** -Methode.<br/> |
|**fRead** <br/> |Gibt an, ob die Datei mit Lesezugriff geöffnet werden.  <br/> |
|**fWrite** <br/> |Gibt an, ob die Datei mit Schreibzugriff geöffnet werden. Diese Funktion gibt true, um Erfolg anzuzeigen und FALSE, um Fehler anzuzeigen.  <br/> |
   

### <a name="fclosehandle"></a>FCloseHandle

Das Exportieren in feste Formate DLL ruft diese Funktion um, die durch Aufrufen der Methode **FGetHandle** dateikennungen zu schließen.
  
    
    

```

BOOL FCloseHandle (
HANDLE phFile,
)
```

Der  *PhFile*  -Parameter gibt das Handle für die Datei geschlossen wird. Wenn der durch diese Methode zurückgegebene Wert 0 ist, einem fehlgeschlagenen Vorgang. Alle anderen Werte geben bei Erfolg.
  
    
    

## <a name="pfnkeepalive"></a>PFNKeepAlive

Wenn die DLL-Datei für Exporte mit festgelegtem Format aktiv ist, muss sie in regelmäßigen Abständen (konfigurierbar durch den Administrator) die Funktion **KeepAlive** aufrufen. Andernfalls geht der Dienst davon aus, dass die DLL-Datei für Exporte mit festgelegtem Format nicht mehr reagiert, und beendet den Prozess.
  
    
    
 `typedef void (*PFNKeepAlive)(void)`
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

Weitere Informationen finden Sie in den folgenden Ressourcen:
  
    
    

-  [Erweitern Sie das Office 2007-Format Export Feature](http://msdn.microsoft.com/de-DE/library/office/aa338206%28v=office.12%29.aspx)
    
  

