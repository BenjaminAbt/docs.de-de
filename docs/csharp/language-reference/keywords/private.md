---
title: private (C#-Referenz) | Microsoft-Dokumentation
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- private_CSharpKeyword
- private
dev_langs:
- CSharp
helpviewer_keywords:
- private keyword [C#]
ms.assetid: 654c0bb8-e6ac-4086-bf96-7474fa6aa1c8
caps.latest.revision: 17
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
ms.openlocfilehash: 6af1e4d3cc97b2a43a912c8e0b59ac9f9e192a62
ms.lasthandoff: 03/13/2017

---
# <a name="private-c-reference"></a>private (C#-Referenz)
Das `private`-Schlüsselwort ist ein Zugriffsmodifizierer für Member. Privater-Zugriff ist die am wenigsten eingeschränkte Zugriffsebene. Private Member sind nur innerhalb der Klasse oder Struktur, in der sie, wie im folgenden Beispiel, deklariert werden:  
  
```  
class Employee  
{  
    private int i;  
    double d;   // private access by default  
}  
```  
  
 Geschachtelte Typen im gleichen Text können auch auf diese privaten Member zugreifen.  
  
 Es ist ein Kompilierzeitfehler auf einen privaten Member außerhalb der Klasse oder Struktur, in der sie deklariert ist, zu verweisen.  
  
 Einen Vergleich von `private` mit den anderen Zugriffsmodifizierern finden Sie unter [Zugriffsebenen](../../../csharp/language-reference/keywords/accessibility-levels.md) und [Zugriffsmodifizierer](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel enthält die `Employee`-Klasse zwei private Datenmember, `name` und `salary`. Als private Member können nur Membermethoden auf sie zugreifen. Die öffentlichen Methoden `GetName` und `Salary` werden hinzugefügt, um gesteuerten Zugriff auf die privaten Member zu ermöglichen. Auf den `name`-Member wird über eine öffentliche Methode zugegriffen, und auf den `salary`-Member wird über eine öffentliche schreibgeschützte Eigenschaft zugegriffen. (Weitere Informationen finden Sie unter [Eigenschaften](../../../csharp/programming-guide/classes-and-structs/properties.md).)  
  
 [!code-cs[csrefKeywordsModifiers#10](../../../csharp/language-reference/keywords/codesnippet/CSharp/private_1.cs)]  
  
## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Referenz](../../../csharp/language-reference/index.md)   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [C#-Schlüsselwörter](../../../csharp/language-reference/keywords/index.md)   
 [Zugriffsmodifizierer](../../../csharp/language-reference/keywords/access-modifiers.md)   
 [Zugriffsebenen](../../../csharp/language-reference/keywords/accessibility-levels.md)   
 [Modifizierer](../../../csharp/language-reference/keywords/modifiers.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)   
 [internal](../../../csharp/language-reference/keywords/internal.md)
