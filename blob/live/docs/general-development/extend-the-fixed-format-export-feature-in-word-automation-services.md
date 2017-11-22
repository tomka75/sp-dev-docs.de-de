---
title: Erweitern der Exportfunktion mit festgelegtem Format in Word Automation Services
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d8375505-432e-438e-971b-221a1d9bb601
ms.openlocfilehash: de50843d70b07089a27ac8601fc76377717fd135
ms.sourcegitcommit: 61f26b4fe41d3cd80622d9950d8f6599df48f26f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/26/2017
---
# <a name="extend-the-fixed-format-export-feature-in-word-automation-services"></a><span data-ttu-id="a3268-102">Erweitern der Exportfunktion mit festgelegtem Format in Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="a3268-102">Extend the fixed-format export feature in Word Automation Services</span></span>
<span data-ttu-id="a3268-103">Erweitern Sie Word Automation Services in Microsoft Office 2013 ersetzen Sie die Bibliothek, die von der Funktion zum Exportieren in feste Formate verwendet.</span><span class="sxs-lookup"><span data-stu-id="a3268-103">Extend Word Automation Services in Microsoft Office 2013 to replace the library used by the fixed-format export feature.</span></span>
## <a name="introduction-to-the-word-file-conversion-service-fixed-format-export-feature"></a><span data-ttu-id="a3268-104">Einführung in die Word-Datei Konvertierung Service mit festem Format export feature</span><span class="sxs-lookup"><span data-stu-id="a3268-104">Introduction to the Word file conversion service fixed-format export feature</span></span>

<span data-ttu-id="a3268-p101">In diesem Artikel wird beschrieben, wie so erweitern Sie das Feature exportieren in feste Formate von Word Automation Services zu verschiedenen exportieren in feste Formate-DLLs verwenden, sodass Drittanbieter-Entwickler von Microsoft bereitgestellte ersetzen können. Dieser Mechanismus ist erforderlich und des Office-Clients mit festem Format Erweiterbarkeit COM-Schnittstelle erweitert. Weitere Informationen finden Sie unter  [Extending the Office 2007 Fixed-Format Export Feature](http://msdn.microsoft.com/de-DE/library/aa338206.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3268-p101">This article describes how to extend the fixed-format export feature of Word Automation Services to use different fixed-format export DLLs, so third-party developers can replace those provided by Microsoft. This mechanism requires and extends the Office client fixed-format extensibility COM interface. For more information, see  [Extending the Office 2007 Fixed-Format Export Feature](http://msdn.microsoft.com/de-DE/library/aa338206.aspx).</span></span>
  
    
    

## <a name="discovery"></a><span data-ttu-id="a3268-108">Suche</span><span class="sxs-lookup"><span data-stu-id="a3268-108">Discovery</span></span>

<span data-ttu-id="a3268-109">Word Automation Services können Drittanbieter-Entwickler ersetzen Sie einen oder beide der Ausgaben mit festem Format unterstützt:</span><span class="sxs-lookup"><span data-stu-id="a3268-109">Word Automation Services allows third-party developers to replace either or both of the fixed format outputs supported:</span></span>
  
    
    

- <span data-ttu-id="a3268-110">PDF</span><span class="sxs-lookup"><span data-stu-id="a3268-110">PDF</span></span>
    
  
- <span data-ttu-id="a3268-111">XPS</span><span class="sxs-lookup"><span data-stu-id="a3268-111">XPS</span></span>
    
  
<span data-ttu-id="a3268-112">Wenn Sie die Formate ersetzen möchten, muss die jeweilige DLL in demselben Verzeichnis abgelegt werden wie die Kernbibliothek (Sword.dll) für Word Automation Services (Installationspfad: \<\<Installationsstammverzeichnis\>\>\\WebServices\\ConversionService\\Bin\\Converter\\) und den in Tabelle 1 angegebenen Dateinamen haben.</span><span class="sxs-lookup"><span data-stu-id="a3268-112">To replace each format, the DLL must be located in the same directory as the core library (Sword.dll) for Word Automation Services (install path: \<\<install root\>\>\\WebServices\\ConversionService\\Bin\\Converter\\), and must have the specific file name specified in table 1.</span></span>
  
    
    

<span data-ttu-id="a3268-113">**Tabelle 1: Dateinamen der DLL-Dateien für Exporte mit festgelegtem Format**</span><span class="sxs-lookup"><span data-stu-id="a3268-113">**Table 1. File names for fixed-format export DLLs**</span></span>


|<span data-ttu-id="a3268-114">**Format**</span><span class="sxs-lookup"><span data-stu-id="a3268-114">**Format**</span></span>|<span data-ttu-id="a3268-115">**Dateiname**</span><span class="sxs-lookup"><span data-stu-id="a3268-115">**File Name**</span></span>|
|:-----|:-----|
|<span data-ttu-id="a3268-116">PDF</span><span class="sxs-lookup"><span data-stu-id="a3268-116">PDF</span></span>  <br/> |<span data-ttu-id="a3268-117">Renderpdf.dll</span><span class="sxs-lookup"><span data-stu-id="a3268-117">Renderpdf.dll</span></span>  <br/> |
|<span data-ttu-id="a3268-118">XPS</span><span class="sxs-lookup"><span data-stu-id="a3268-118">XPS</span></span>  <br/> |<span data-ttu-id="a3268-119">Renderxps.dll</span><span class="sxs-lookup"><span data-stu-id="a3268-119">Renderxps.dll</span></span>  <br/> |
   

## <a name="initialization"></a><span data-ttu-id="a3268-120">Initialisierung</span><span class="sxs-lookup"><span data-stu-id="a3268-120">Initialization</span></span>

<span data-ttu-id="a3268-121">Eine Methode mit der folgenden Signatur muss die DLL-Datei exportiert werden.</span><span class="sxs-lookup"><span data-stu-id="a3268-121">The DLL must export a method with the following signature.</span></span>
  
    
    

```

HRESULT HrGetDocExporter (
IMsoDocExporter **ppimde,
IMsoServerFileManagerSite *psfms,
PFNKeepAlive pfnKeepAlive
)
```

<span data-ttu-id="a3268-122">Die Funktion erfordert die DLL zwei Schnittstellen und einer Methodenzeiger, die im folgenden Abschnitt beschrieben bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="a3268-122">The function requires the DLL to supply two interfaces and a method pointer, described in the following section.</span></span>
  
    
    
<span data-ttu-id="a3268-p102">Wenn die Funktion Fehler zurückgibt wird der Dienst nicht auf die Microsoft bereitgestellten Exporter (engl.) zurückgreifen. Stattdessen meldet der Dienst die Konvertierung als fehlgeschlagen ist.</span><span class="sxs-lookup"><span data-stu-id="a3268-p102">If the function returns failure the service will not fall back to the Microsoft-provided exporter. Instead, the service will report the conversion as having failed.</span></span>
  
    
    

## <a name="imsodocexporter"></a><span data-ttu-id="a3268-125">IMsoDocExporter</span><span class="sxs-lookup"><span data-stu-id="a3268-125">IMsoDocExporter</span></span>

<span data-ttu-id="a3268-p103">Die **IMsoDocExporter** -Schnittstelle ist identisch mit der vorhandenen-Schnittstelle auf MSDN dokumentiert. Weitere Informationen finden Sie unter [Extending the Office 2007 Fixed-Format Export Feature](http://msdn.microsoft.com/de-DE/library/aa338206.aspx). Wenn die frühere Methode Erfolg zurückgegeben wird, werden diese Schnittstelle die Konvertierung durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="a3268-p103">The **IMsoDocExporter** interface is identical to the existing interface documented on MSDN. For more information, see [Extending the Office 2007 Fixed-Format Export Feature](http://msdn.microsoft.com/de-DE/library/aa338206.aspx). When the previous method returns success, this interface performs the conversion.</span></span>
  
    
    
<span data-ttu-id="a3268-p104">Über die Anforderungen in der oben genannten Artikel beschrieben wird müssen Entwickler von DLLs exportieren in feste Formate Beachten Sie, dass der Dienst den bereitgestellten **IMsoDocExporter** in einem anderen Thread von der Anrufen kann, auf dem der Dienst **HrGetDocExporter**bezeichnet. Die DLL muss dies ohne den Anruf wieder an der Thread, **HrGetDocExporter**, aufgerufen, da der Dienst wird ein Nachrichtensystem nicht ausgeführt, und der gemarshallte Anruf nie erhalten über (was eine hängen und weitere Fehler) gemarshallt behandeln können.</span><span class="sxs-lookup"><span data-stu-id="a3268-p104">Beyond the requirements described in the aforementioned article, developers of fixed-format export DLLs must be aware that the service can call the provided **IMsoDocExporter** on a different thread from the one on which the service called **HrGetDocExporter**. The DLL must be able to handle this without marshalling the call back to the thread that called **HrGetDocExporter**, because the service does not run a message pump and the marshaled call will never get through (resulting in a hang and subsequent failure).</span></span>
  
    
    

## <a name="imsoserverfilemanagersite"></a><span data-ttu-id="a3268-131">IMsoServerFileManagerSite</span><span class="sxs-lookup"><span data-stu-id="a3268-131">IMsoServerFileManagerSite</span></span>

<span data-ttu-id="a3268-132">Die IMsoServerFileManagerSite-Schnittstelle wird wie folgt definiert.</span><span class="sxs-lookup"><span data-stu-id="a3268-132">The IMsoServerFileManagerSite interface is defined as follows.</span></span>
  
    
    

```

#undef  INTERFACE
#define INTERFACE  IMsoServerFileManagerSite
DECLARE_INTERFACE(IMsoServerFileManagerSite)
{
STDMETHOD_(BOOL, FGetHandle) (const WCHAR *pwzFileName, HANDLE *phFile, BOOL fRead, BOOL fWrite) PURE;
STDMETHOD_(BOOL, FCloseHandle) (HANDLE hFile) PURE;
};
```

<span data-ttu-id="a3268-133">Diese Schnittstelle stellt die folgenden Methoden.</span><span class="sxs-lookup"><span data-stu-id="a3268-133">This interface exposes the following methods.</span></span>
  
    
    

<span data-ttu-id="a3268-134">**In Tabelle 2. Methoden verfügbar gemacht werden, die von der IMsoServerFileManagerSite-Schnittstelle**</span><span class="sxs-lookup"><span data-stu-id="a3268-134">**Table 2. Methods exposed by the IMsoServerFileManagerSite interface**</span></span>

|||
|:-----|:-----|
|<span data-ttu-id="a3268-135">Methode</span><span class="sxs-lookup"><span data-stu-id="a3268-135">Method</span></span>  <br/> |<span data-ttu-id="a3268-136">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="a3268-136">Description</span></span>  <br/> |
|<span data-ttu-id="a3268-137">**FGetHandle**</span><span class="sxs-lookup"><span data-stu-id="a3268-137">**FGetHandle**</span></span> <br/> |<span data-ttu-id="a3268-138">Ruft ein Dateihandle ab.</span><span class="sxs-lookup"><span data-stu-id="a3268-138">Gets a file handle.</span></span>  <br/> |
|<span data-ttu-id="a3268-139">**FCloseHandle**</span><span class="sxs-lookup"><span data-stu-id="a3268-139">**FCloseHandle**</span></span> <br/> |<span data-ttu-id="a3268-140">Gibt ein Dateihandle frei.</span><span class="sxs-lookup"><span data-stu-id="a3268-140">Releases a file handle.</span></span>  <br/> |
   
<span data-ttu-id="a3268-p105">Diese Schnittstelle erbt nicht von **IUnknown**. Die DLL-Datei exportieren in feste Formate darf entsprechend, einen Verweis auf dieses für die Lebensdauer bleiben.</span><span class="sxs-lookup"><span data-stu-id="a3268-p105">This interface does not inherit from **IUnknown**. Accordingly, the fixed-format export DLL is allowed to keep a reference to it for its lifetime.</span></span>
  
    
    

### <a name="fgethandle"></a><span data-ttu-id="a3268-143">FGetHandle</span><span class="sxs-lookup"><span data-stu-id="a3268-143">FGetHandle</span></span>

<span data-ttu-id="a3268-p106">Das mit festem Format exportieren DLL-Aufrufe dieser Funktion zum Abrufen des Dateihandles zum Schreiben in. Es muss nicht versuchen Sie zum Öffnen von Dateien über einen anderen Mechanismus, da der Dienst in einer stark eingeschränkten Umgebung ohne Zugriff auf die meisten Stellen im Dateisystem ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="a3268-p106">The fixed-format export DLL calls this function to get file handles to write to. It must not try to open files through any other mechanism because the service runs in a highly restricted environment without access to most places in the file system.</span></span>
  
    
    

```

BOOL FGetHandle (
const WCHAR *pwzFile,
HANDLE *phFile,
BOOL fRead,
BOOL fWrite
)
```


<span data-ttu-id="a3268-146">**Tabelle 3. FGetHandle-Parameter**</span><span class="sxs-lookup"><span data-stu-id="a3268-146">**Table 3. FGetHandle parameters**</span></span>

|||
|:-----|:-----|
|<span data-ttu-id="a3268-147">Parameter</span><span class="sxs-lookup"><span data-stu-id="a3268-147">Parameter</span></span>  <br/> |<span data-ttu-id="a3268-148">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="a3268-148">Description</span></span>  <br/> |
|<span data-ttu-id="a3268-149">**pwzFile**</span><span class="sxs-lookup"><span data-stu-id="a3268-149">**pwzFile**</span></span> <br/> |<span data-ttu-id="a3268-p107">Gibt den Namen der Datei, das mit festem Format exportieren DLL öffnen möchte. Dies muss keinen vollständigen Dateipfad - müssen sie nur einen Dateinamen ein (beispielsweise Output.pdf) angeben.</span><span class="sxs-lookup"><span data-stu-id="a3268-p107">Specifies the name of the file the fixed-format export DLL wants to open. This must not be a full file path—it must specify only a file name (for example, Output.pdf).</span></span>  <br/> |
|<span data-ttu-id="a3268-152">**phFile**</span><span class="sxs-lookup"><span data-stu-id="a3268-152">**phFile**</span></span> <br/> |<span data-ttu-id="a3268-p108">Gibt das Handle für die angegebene Datei an, ob die Datei erfolgreich geöffnet wird. Das Exportieren in feste Formate DLL können Sie dieses HANDLE in normalen Dateivorgänge, bis es geschlossen wird durch Aufrufen der **FCloseHandle** -Methode.</span><span class="sxs-lookup"><span data-stu-id="a3268-p108">Specifies the handle to the specified file, if the file is opened successfully. The fixed-format export DLL can then use this HANDLE in normal file operations until it closes it by calling the **FCloseHandle** method. </span></span><br/> |
|<span data-ttu-id="a3268-155">**fRead**</span><span class="sxs-lookup"><span data-stu-id="a3268-155">**fRead**</span></span> <br/> |<span data-ttu-id="a3268-156">Gibt an, ob die Datei mit Lesezugriff geöffnet werden.</span><span class="sxs-lookup"><span data-stu-id="a3268-156">Specifies whether the file is to be opened with read access.</span></span>  <br/> |
|<span data-ttu-id="a3268-157">**fWrite**</span><span class="sxs-lookup"><span data-stu-id="a3268-157">**fWrite**</span></span> <br/> |<span data-ttu-id="a3268-p109">Gibt an, ob die Datei mit Schreibzugriff geöffnet werden. Diese Funktion gibt true, um Erfolg anzuzeigen und FALSE, um Fehler anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="a3268-p109">Specifies whether the file is to be opened with write access. This function returns TRUE to indicate success and FALSE to indicate failure.</span></span>  <br/> |
   

### <a name="fclosehandle"></a><span data-ttu-id="a3268-160">FCloseHandle</span><span class="sxs-lookup"><span data-stu-id="a3268-160">FCloseHandle</span></span>

<span data-ttu-id="a3268-161">Das Exportieren in feste Formate DLL ruft diese Funktion um, die durch Aufrufen der Methode **FGetHandle** dateikennungen zu schließen.</span><span class="sxs-lookup"><span data-stu-id="a3268-161">The fixed-format export DLL calls this function to close file handles obtained through calls to the **FGetHandle** method.</span></span>
  
    
    

```

BOOL FCloseHandle (
HANDLE phFile,
)
```

<span data-ttu-id="a3268-p110">Der  *PhFile*  -Parameter gibt das Handle für die Datei geschlossen wird. Wenn der durch diese Methode zurückgegebene Wert 0 ist, einem fehlgeschlagenen Vorgang. Alle anderen Werte geben bei Erfolg.</span><span class="sxs-lookup"><span data-stu-id="a3268-p110">The  *phFile*  parameter specifies the handle to the file to be closed. If the value returned by this method is 0, the operation failed. All other values indicate success.</span></span>
  
    
    

## <a name="pfnkeepalive"></a><span data-ttu-id="a3268-165">PFNKeepAlive</span><span class="sxs-lookup"><span data-stu-id="a3268-165">PFNKeepAlive</span></span>

<span data-ttu-id="a3268-166">Wenn die DLL-Datei für Exporte mit festgelegtem Format aktiv ist, muss sie in regelmäßigen Abständen (konfigurierbar durch den Administrator) die Funktion **KeepAlive** aufrufen. Andernfalls geht der Dienst davon aus, dass die DLL-Datei für Exporte mit festgelegtem Format nicht mehr reagiert, und beendet den Prozess.</span><span class="sxs-lookup"><span data-stu-id="a3268-166">When the fixed-format export DLL is active, it must call the **KeepAlive** function at regular intervals (configurable by the administrator) to prevent the service from assuming that the fixed-format export DLL is hung and terminating the process.</span></span>
  
    
    
 `typedef void (*PFNKeepAlive)(void)`
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="a3268-167">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="a3268-167">Additional resources</span></span>
<span data-ttu-id="a3268-168"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a3268-168"></span></span>

<span data-ttu-id="a3268-169">Weitere Informationen finden Sie in den folgenden Ressourcen:</span><span class="sxs-lookup"><span data-stu-id="a3268-169">For more information, see the following resources:</span></span>
  
    
    

-  [<span data-ttu-id="a3268-170">Erweitern Sie das Office 2007-Format Export Feature</span><span class="sxs-lookup"><span data-stu-id="a3268-170">Extending the Office 2007 Fixed-Format Export Feature</span></span>](http://msdn.microsoft.com/de-DE/library/office/aa338206%28v=office.12%29.aspx)
    
  

