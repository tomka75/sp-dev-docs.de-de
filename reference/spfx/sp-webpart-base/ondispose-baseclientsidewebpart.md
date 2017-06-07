# <a name="ondispose"></a>onDispose()




Diese API sollte zum Aktualisieren des Inhalts des PropertyPane verwendet werden. Diese API wird am Ende des Lebenszyklus des Webparts auf einer Seite aufgerufen. Sie sollte zum Entfernen lokaler Ressourcen (d. h. DOM-Elemente) verwendet werden, die das Webpart speichert. Diese API wird in Szenarien wie z. B. die Seitennavigation aufgerufen, der Host geht daher von einer Seite auf eine andere über und entfernt die Seite, die er verlässt.

**Signatur:** _@virtual protected onDispose(): void;_

**Gibt Folgendes zurück**: `void`





#### <a name="parameters"></a>Parameter
Keine


