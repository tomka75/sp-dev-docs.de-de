# <a name="loadscripturloptions"></a>loadScript(url,options)




Wenn eine URL vorhanden ist, wird ein Skript geladen.

**Signatur:** _loadScript < TModule >(url: string, options?: [ILoadScriptOptions](../sp-loader/iloadscriptoptions.md)): Zusage<TModule>;_

**Gibt Folgendes zurück**: `Promise<TModule>`



Eine Zusage, die das geladene Modul enthält.

#### <a name="parameters"></a>Parameter


| Parameter    | Typ    | Beschreibung |
|:-------------|:---------------|:------------|
| `url`    | `string` | Die Skript-URL. |
| `options`    | [`ILoadScriptOptions`](../sp-loader/iloadscriptoptions.md) | __Optional.__ globalExportsName: Wenn es sich bei dem Skript nicht um ein AMD-Modul handelt, das ein globales Element auf der Seite lädt, geben Sie den Namen des globalen Elements an. |


