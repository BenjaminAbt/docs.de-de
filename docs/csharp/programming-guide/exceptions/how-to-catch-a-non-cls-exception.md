---
title: 'Vorgehensweise: Abfangen einer Nicht-CLS-Ausnahme | Microsoft-Dokumentation'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exceptions [C#], non-CLS
ms.assetid: db4630b3-5240-471a-b3a7-c7ff6ab31e8d
caps.latest.revision: 8
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
ms.openlocfilehash: 3515ecab379a0e910cdd5ba82a4a39b085cc816f
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-catch-a-non-cls-exception"></a>Gewusst wie: Abfangen einer Nicht-CLS-Ausnahme
Einige .NET-Sprachen, einschließlich C++/CLI, erlauben Objekten, Ausnahmen auszulösen, die nicht aus <xref:System.Exception> stammen. Diese Ausnahmen werden als *Nicht-CLS-Ausnahmen* oder *Nicht-Ausnahmen* bezeichnet. In [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] können Sie keine Nicht-CLS-Ausnahmen auslösen. Sie können sie jedoch auf zwei Arten abfangen:  
  
-   Innerhalb eines `catch (Exception e)`-Blocks als eine <xref:System.Runtime.CompilerServices.RuntimeWrappedException>.  
  
     In der Standardeinstellung fängt eine [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)]-Assembly Nicht-CLS-Ausnahmen als umschlossene Ausnahmen ab. Verwenden Sie diese Methode, wenn Sie Zugriff auf die ursprüngliche Ausnahme benötigen, auf die über die <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A>-Eigenschaft zugegriffen werden kann. Weiter unten in diesem Thema wird erläutert, wie Abfragen auf diese Art und Weise abgefangen werden können.  
  
-   Innerhalb eines allgemeinen Catch-Blocks (ein Catch-Block ohne angegebenen Ausnahmetyp), der nach einem `catch (Exception)`- oder `catch (Exception e)`-Block eingefügt wird.  
  
     Verwenden Sie diese Methode, wenn Sie eine Aktion (z.B. das Schreiben in eine Protokolldatei) als Reaktion auf Nicht-CLS-Ausnahmen ausführen möchten und Sie keinen Zugriff auf die Ausnahmeinformationen benötigen. Standardmäßig umschließt die Common Language Runtime alle Ausnahmen. Um dieses Verhalten zu deaktivieren, fügen Sie dieses Attribut auf Assemblyebene Ihrem Code hinzu, in der Regel in die Datei „AssemblyInfo.cs“: `[assembly: RuntimeCompatibilityAttribute(WrapNonExceptionThrows = false)]`.  
  
### <a name="to-catch-a-non-cls-exception"></a>So fangen Sie eine Nicht-CLS-Ausnahme ab  
  
1.  Verwenden Sie innerhalb von `catch(Exception e) block` das Schlüsselwort `as`, um zu testen, ob `e` in eine <xref:System.Runtime.CompilerServices.RuntimeWrappedException> umgewandelt werden kann.  
  
2.  Greifen Sie über die <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A>-Eigenschaft auf die ursprüngliche Ausnahme zu.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel zeigt, wie Sie eine Nicht-CLS-Ausnahme abfangen, die von einer in C++/CRL geschriebenen Klassenbibliothek ausgelöst wurde. Beachten Sie, dass in diesem Beispiel der [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)]-Clientcode im Voraus weiß, dass der Ausnahmetyp, der ausgelöst wird, eine <xref:System.String?displayProperty=fullName> darstellt. Wandeln Sie die <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A>-Eigenschaft in den ursprünglichen Typ um, solange dieser Typ über Ihren Code erreicht werden kann.  
  
```  
// Class library written in C++/CLR.  
   ThrowNonCLS.Class1 myClass = new ThrowNonCLS.Class1();  
  
   try  
   {  
    // throws gcnew System::String(  
    // "I do not derive from System.Exception!");  
    myClass.TestThrow();   
   }  
  
   catch (Exception e)  
   {  
    RuntimeWrappedException rwe = e as RuntimeWrappedException;  
    if (rwe != null)      
    {  
      String s = rwe.WrappedException as String;  
      if (s != null)  
      {  
        Console.WriteLine(s);  
      }  
    }  
    else  
    {  
       // Handle other System.Exception types.  
    }  
   }             
```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Runtime.CompilerServices.RuntimeWrappedException>   
 [Ausnahmen und Ausnahmebehandlung](../../../csharp/programming-guide/exceptions/index.md)
