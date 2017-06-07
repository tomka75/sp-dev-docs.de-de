# <a name="httpclientresponse-class"></a>HttpClientResponse-Klasse

_Implementiert: `Response`_





Die Response-Unterklasse, die von Methoden wie HttpClient.fetch() zurückgegeben wird.



## <a name="properties"></a>Eigenschaften

| Eigenschaft     | Zugriffsmodifizierer | Typ | Beschreibung|
|:-------------|:----|:-------|:-----------|
|`bodyUsed`     | `public` | `boolean` | _Schreibgeschützt._ {@inheritdoc Body.bodyUsed} |
|`headers`     | `public` | `Headers` | _Schreibgeschützt._ {@inheritdoc Response.headers} |
|`nativeResponse`     | `public` | `Response` |  |
|`ok`     | `public` | `boolean` | _Schreibgeschützt._ {@inheritdoc Response.ok} |
|`status`     | `public` | `number` | _Schreibgeschützt._ {@inheritdoc Response.status} |
|`statusText`     | `public` | `string` | _Schreibgeschützt._ {@inheritdoc Response.statusText} |
|`type`     | `public` | `ResponseType` | _Schreibgeschützt._ {@inheritdoc Response.type} |
|`url`     | `public` | `string` | _Schreibgeschützt._ {@inheritdoc Response.url} |




## <a name="methods"></a>Methoden

| Methode       | Zugriffsmodifizierer | Rückgabewerte  | Beschreibung|
|:-------------|:----|:-------|:-----------|
|[`arrayBuffer()`](arraybuffer-httpclientresponse.md)     | `public` | `Promise<ArrayBuffer>` | {@inheritdoc Body.arrayBuffer} |
|[`blob()`](blob-httpclientresponse.md)     | `public` | `Promise<Blob>` | {@inheritdoc Body.blob} |
|[`clone()`](clone-httpclientresponse.md)     | `public` | [`HttpClientResponse`](../sp-http/httpclientresponse.md) |  |
|[`error()`](error-httpclientresponse.md)     | `public, static` | `Response` | {@inheritdoc Response.error} |
|[`formData()`](formdata-httpclientresponse.md)     | `public` | `Promise<FormData>` | {@inheritdoc Body.formData} |
|[`json()`](json-httpclientresponse.md)     | `public` | `Promise<any>` | {@inheritdoc Body.json} |
|[`redirect()`](redirect-httpclientresponse.md)     | `public, static` | `Response` | {@inheritdoc Response.redirect} |
|[`text()`](text-httpclientresponse.md)     | `public` | `Promise<string>` | {@inheritdoc Body.text} |





### <a name="remarks"></a>HinwBemerkungeneise

Dies ist ein Platzhalter. Künftig werden möglicherweise zusätzliche HttpClient-spezifische Funktionen zu dieser Klasse hinzugefügt.

