# <a name="isphttpclientcommonconfiguration-interface"></a>ISPHttpClientCommonConfiguration-Schnittstelle







Flags-Schnittstelle für SPHttpClientConfiguration.




## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Typ   | Beschreibung|
|:-------------|:-------|:-----------|
|`jsonRequest`      | `boolean` | Wenn dieser Schalter zutrifft: Wenn die „Content-Type“-Kopfzeile nicht explizit für die Anforderung hinzugefügt wurde, so wird diese von SPHttpClient hinzugefügt, wenn die Anforderung ein Schreibvorgang ist (d. h. eine andere HTTP-Methode als „GET“, „HEAD“ oder „OPTIONS“) ist. Für OData 3.0 ist der Wert „application/json;odata=verbose;charset=utf-8'“. Für OData 4.0 ist der Wert „application/json;charset=utf-8“. |
|`jsonResponse`      | `boolean` | Wenn dieser Schalter zutrifft: Wenn die Kopfzeile „Accept“ nicht explizit für die Anforderung hinzugefügt wurde, wird sie von SPHttpClient hinzugefügt. Für OData 3.0 ist der Wert „application/json“. Für OData 4.0 ist der Wert „application/json;odata.metadata=minimal“. |






