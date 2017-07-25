<span data-ttu-id="91fd9-p123">Fügen Sie Eingaben für Ihre Zeichenfolgen hinzu. In diesem Fall haben Sie die Datei **MyStrings.d.ts**:</span><span class="sxs-lookup"><span data-stu-id="91fd9-p123">Add typings for your strings. In this case, you have a file **MyStrings.d.ts**:</span></span>

```json
{
"strings": "strings/{locale}.js"
}
```
    
Fügen Sie Eingaben für Ihre Zeichenfolgen hinzu. In diesem Fall haben Sie die Datei **MyStrings.d.ts**:

```typescript
declare interface IStrings {
webpartTitle: string;
initialPrompt: string;
exitPrompt: string;
}

declare module 'mystrings' {
const strings: IStrings;
export = strings;
}
```
    
<span data-ttu-id="91fd9-201">Hinzufügen von Importen für die Zeichenfolgen in Ihrem Projekt:</span><span class="sxs-lookup"><span data-stu-id="91fd9-201">Add imports for the strings in your project:</span></span>
    
```typescript
import * as strings from 'strings';
```
    
<span data-ttu-id="91fd9-202">Verwenden der Zeichenfolgen in Ihrem Projekt:</span><span class="sxs-lookup"><span data-stu-id="91fd9-202">Use the strings in your project:</span></span>

```typescript
alert(strings.initialPrompt);
```
