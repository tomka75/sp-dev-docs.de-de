# <a name="rendercompleted"></a>renderCompleted()




Diese API sollte von Webparts aufgerufen werden, die ein asynchrones Rendering durchführen. Diese Webparts müssen die IsRenderAsync-API überschreiben und „true“ zurückgeben. Ein Beispiel hierfür sind Webparts, die Inhalte in einem IFrame rendern. Das Webpart initiiert die IFrame-Darstellung in der render()-API, aber das tatsächliche Rendern wird erst abgeschlossen, nachdem der Ladevorgang des IFrame abgeschlossen ist.

**Signatur:** _protected renderCompleted(): void;_

**Gibt Folgendes zurück**: `void`





#### <a name="parameters"></a>Parameter
Keine


