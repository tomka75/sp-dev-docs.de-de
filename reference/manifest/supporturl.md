
# <a name="supporturl-element"></a>SupportUrl-Element

Gibt die URL einer Seite an, die Supportinformationen für Ihr Add-In enthält.

## <a name="example"></a>Beispiel

```XML
<OfficeApp>
...
  <IconUrl DefaultValue="https://contoso.com/assets/icon-32.png" />
  <HighResolutionIconUrl DefaultValue="https://contoso.com/assets/hi-res-icon.png"/>
  
  
  <SupportUrl DefaultValue="https://contoso.com/support " />
  
  
  <AppDomains>
  ...
  </AppDomains>
...
</OfficeApp>

```


## <a name="attributes"></a>Attribute

|**Attribut**|**Typ**|**Erforderlich**|**Beschreibung**|
|:-----|:-----|:-----|:-----|
|DefaultValue|URL|erforderlich|Gibt den Standardwert für diese Einstellung an, der für das im [DefaultLocale](../../reference/manifest/defaultlocale.md)-Element angegebene Gebietsschema ausgedrückt wird.|

## <a name="child-elements"></a>Untergeordnete Elemente

|  Element | Erforderlich | Beschreibung  |
|:-----|:-----|:-----|
|  [Override](../../reference/manifest/override.md)   | Nein | Gibt die Einstellung für zusätzliche Gebietsschema-URLS an. |

## <a name="parent-element"></a>Übergeordnetes Element
[OfficeApp](../../reference/manifest/officeapp.md)

