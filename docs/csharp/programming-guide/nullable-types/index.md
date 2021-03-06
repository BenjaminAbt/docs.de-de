---
title: Nullable-Typen (C#-Programmierhandbuch) | Microsoft-Dokumentation
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- nullable types [C#]
- C# language, nullable types
- types [C#], nullable
ms.assetid: e473cb01-28ca-42be-9cea-f717055d72c6
caps.latest.revision: 44
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 75726b9864abc0c9b556085e5215c6692d80fb12
ms.lasthandoff: 03/13/2017

---
# <a name="nullable-types-c-programming-guide"></a>Nullable-Typen (C#-Programmierhandbuch)
Nullable-Typen sind Instanzen der Struktur <xref:System.Nullable%601?displayProperty=fullName>. Ein Nullable-Typ kann den richtigen Bereich an Werten für den zugrunde liegenden Werttyp plus einen zusätzlichen `null`-Wert darstellen. Einem `Nullable<Int32>` (ausgesprochen „Nullable von Int32“) kann jeder Wert im Bereich von -2147483648 bis 2147483647 oder ein `null`-Wert zugewiesen werden. Einem `Nullable<bool>` können die Werte [true](../../../csharp/language-reference/keywords/true.md), [false](../../../csharp/language-reference/keywords/false.md) oder [null](../../../csharp/language-reference/keywords/null.md) zugewiesen werden. Die Möglichkeit, `null` zu numerischen und booleschen Typen zuzuweisen, ist besonders nützlich, wenn Sie mit Datenbanken und anderen Datentypen mit Elementen arbeiten, denen möglicherweise kein Wert zugewiesen wurde. Ein boolesches Feld in einer Datenbank kann beispielsweise die Werte `true` oder `false` speichern oder nicht definiert sein.  
  
 [!code-cs[csProgGuideTypes#3](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_1.cs)]  
  
 Das Beispiel zeigt die Ausgabe:  
  
 `num = Null`  
  
 `Nullable object must have a value.`  
  
 Weitere Beispiele finden Sie unter [Verwenden von Nullable-Typen](../../../csharp/programming-guide/nullable-types/using-nullable-types.md).  
  
## <a name="nullable-types-overview"></a>Übersicht über Nullable-Typen  
 Nullable-Typen weisen die folgenden Eigenschaften auf:  
  
-   Nullable-Typen stellen Werttypvariablen dar, denen der Wert `null` zugewiesen werden kann. Sie können keinen Nullable-Typ basierend auf einem Verweistyp erstellen. (Verweistypen unterstützen immer den `null`-Wert.)  
  
-   Die Syntax `T?` ist die Kurzform für <xref:System.Nullable%601>, wobei `T` ein Werttyp ist. Die beiden Formen sind austauschbar.  
  
-   Sie weisen einem Nullable-Typ einen Wert genauso zu, wie Sie es für einen regulären Werttyp tun würden, z.B. `int? x = 10;` oder `double? d = 4.108`. Einem Nullable-Typ kann auch der Wert `null`:`int? x = null.` zugewiesen werden.  
  
-   Verwenden Sie die <xref:System.Nullable%601.GetValueOrDefault%2A?displayProperty=fullName>-Methode, um entweder den zugewiesenen Wert oder den Standardwert für den zugrunde liegenden Typ zurückzugeben, wenn der Wert `null` ist, z.B. `int j = x.GetValueOrDefault();`  
  
-   Verwenden Sie die schreibgeschützten Eigenschaften <xref:System.Nullable%601.HasValue%2A> und <xref:System.Nullable%601.Value%2A>, um auf Null zu testen und den Wert abzurufen, wie in folgendem Beispiel gezeigt: `if(x.HasValue) j = x.Value;`  
  
    -   Die Eigenschaft `HasValue` gibt `true` zurück, wenn die Variable einen Wert enthält, oder sie gibt `false` zurück, wenn die Variable `null` ist.  
  
    -   Die Eigenschaft `Value` gibt einen Wert zurück, sofern einer zugewiesen ist. Andernfalls wird eine <xref:System.InvalidOperationException?displayProperty=fullName> ausgelöst.  
  
    -   Der Standardwert für `HasValue` lautet `false`. Die Eigenschaft `Value` hat keinen Standardwert.  
  
    -   Sie können auch die Operatoren `==` und `!=` mit einem Nullable-Typ verwenden, wie im folgenden Beispiel gezeigt: `if (x != null) y = x;`  
  
-   Verwenden Sie den Operator `??`, um einen Standardwert zuzuweisen, der angewendet wird, wenn ein Nullable-Typ, dessen aktueller Wert`null` lautet, einem Nicht-Nullable-Typ zugewiesen wird, z.B.: `int? x = null; int y = x ?? -1;`  
  
-   Geschachtelte Nullable-Typen sind nicht zulässig. Die folgende Zeile wird nicht kompiliert: `Nullable<Nullable<int>> n;`  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
 Weitere Informationen finden Sie unter:   
  
-   [Verwenden von Typen mit Nullwert](../../../csharp/programming-guide/nullable-types/using-nullable-types.md)  
  
-   [Boxing von Typen mit Nullwerten](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)  
  
-   [?? Operator](../../../csharp/language-reference/operators/null-conditional-operator.md)  
  
## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Nullable>   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [C#](../../../csharp/csharp.md)   
 [C#-Referenz](../../../csharp/language-reference/index.md)   
 [What exactly does 'lifted' mean?](http://go.microsoft.com/fwlink/?LinkId=112382) (Was bedeutet „Lifted“ genau?)

