# Import Declarations: The open Keyword (F#)

An *import declaration* specifies a module or namespace whose elements you can reference without using a fully qualified name.


## CAPS_SYNTAX_MD

```
open module-or-namespace-name
```

## CAPS_REMARKS_MD
Referencing code by using the fully qualified namespace or module path every time can create code that is hard to write, read, and maintain. Instead, you can use the **open** keyword for frequently used modules and namespaces so that when you reference a member of that module or namespace, you can use the short form of the name instead of the fully qualified name. This keyword is similar to the **using** keyword in C#, **using****namespace** in C#, and **Imports** in Visual Basic.

The module or namespace provided must be in the same project or in a referenced project or assembly. If it is not, you can add a reference to the project, or use the **-reference** command**-**line option (or its abbreviation, **-r**). For more information, see [Compiler Options &#40;F&#35;&#41;](Compiler+Options+%28F%23%29.md).

The import declaration makes the names available in the code that follows the declaration, up to the end of the enclosing namespace, module, or file.

When you use multiple import declarations, they should appear on separate lines.

The following code shows the use of the **open** keyword to simplify code.

```

// Without the import declaration, you must include the full
// path to .NET Framework namespaces such as System.IO.
let writeToFile1 filename (text: string) =
  let stream1 = new System.IO.FileStream(filename, System.IO.FileMode.Create)
  let writer = new System.IO.StreamWriter(stream1)
  writer.WriteLine(text)

// Open a .NET Framework namespace.
open System.IO

// Now you do not have to include the full paths.
let writeToFile2 filename (text: string) =
  let stream1 = new FileStream(filename, FileMode.Create)
  let writer = new StreamWriter(stream1)
  writer.WriteLine(text)

writeToFile2 "file1.txt" "Testing..."
```

    The F# compiler does not emit an error or warning when ambiguities occur when the same name occurs in more than one open module or namespace. When ambiguities occur, F# gives preference to the more recently opened module or namespace. For example, in the following code, **empty** means **Seq.empty**, even though **empty** is located in both the **List** and **Seq** modules.


```
open List
open Seq
printfn "%A" empty
```
Therefore, be careful when you open modules or namespaces such as **List** or **Seq** that contain members that have identical names; instead, consider using the qualified names. You should avoid any situation in which the code is dependent upon the order of the import declarations.


## Namespaces That Are Open by Default
Some namespaces are so frequently used in F# code that they are opened implicitly without the need of an explicit import declaration. The following table shows the namespaces that are open by default.



|Namespace|Description|
|---------|-----------|
|**Microsoft.FSharp.Core**|Contains basic F# type definitions for built-in types such as **int** and **float**.|
|**Microsoft.FSharp.Core.Operators**|Contains basic arithmetic operations such as **+** and **&#42;**.|
|**Microsoft.FSharp.Collections**|Contains immutable collection classes such as **List** and **Array**.|
|**Microsoft.FSharp.Control**|Contains types for control constructs such as lazy evaluation and asynchronous workflows.|
|**Microsoft.FSharp.Text**|Contains functions for formatted IO, such as the **printf** function.|

## AutoOpen Attribute
You can apply the **AutoOpen** attribute to an assembly if you want to automatically open a namespace or module when the assembly is referenced. You can also apply the **AutoOpen** attribute to a module to automatically open that module when the parent module or namespace is opened. For more information, see [Core.AutoOpenAttribute Class &#40;F&#35;&#41;](Core.AutoOpenAttribute+Class+%28F%23%29.md).


## RequireQualifiedAccess Attribute
Some modules, records, or union types may specify the RequireQualifiedAccess attribute. When you reference elements of those modules, records, or unions, you must use a qualified name regardless of whether you include an import declaration. If you use this attribute strategically on types that define commonly used names, you help avoid name collisions and thereby make code more resilient to changes in libraries. For more information, see [Core.RequireQualifiedAccessAttribute Class &#40;F&#35;&#41;](Core.RequireQualifiedAccessAttribute+Class+%28F%23%29.md).


## See Also
[F&#35; Language Reference](F%23+Language+Reference.md)

[Namespaces &#40;F&#35;&#41;](Namespaces+%28F%23%29.md)

[Modules &#40;F&#35;&#41;](Modules+%28F%23%29.md)
