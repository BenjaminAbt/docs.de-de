---
title: /target:exe (C#-Compileroption) | Microsoft-Dokumentation
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /exe
dev_langs:
- CSharp
helpviewer_keywords:
- target compiler options [C#], /target:exe
- /target compiler options [C#], /target:exe
- -target compiler options [C#], /target:exe
ms.assetid: bda5717d-1b91-4848-956b-fcf85c30e432
caps.latest.revision: 12
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
ms.openlocfilehash: 9d5784186f564241c896333d518e297c3c094f28
ms.lasthandoff: 03/13/2017

---
# <a name="targetexe-c-compiler-options"></a>/target:exe (C#-Compileroptionen)
Die Option **/target:exe** bewirkt, dass der Compiler eine ausführbare Konsolenanwendung (EXE) erstellt.  
  
## <a name="syntax"></a>Syntax  
  
```  
/target:exe  
```  
  
## <a name="remarks"></a>Hinweise  
 Die Option **/target:exe** ist standardmäßig aktiviert. Die ausführbare Datei wird mit der Dateiendung „.exe“ erstellt.  
  
 Verwenden Sie [/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md), um ein ausführbares Windows-Programm zu erstellen.  
  
 Sofern Sie nicht die Option [/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md) verwenden, erhält die Ausgabedatei den Namen der Eingabedatei, die die [Main](../../../csharp/programming-guide/main-and-command-args/index.md)-Methode enthält.  
  
 Wenn es in der Befehlszeile angegeben wurde, werden alle Dateien bis zur nächsten Option **/out** oder **/target:module** verwendet, um die EXE-Datei zu erstellen  
  
 Nur eine **Main**-Methode wird in den Quellcodedateien benötigt, die in eine EXE-Datei kompiliert werden. Sollte Ihr Code mehr als eine Klasse mit einer **Main**-Methode haben, können Sie mit der Compileroption [/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md) angeben, welche Klasse die Methode **Main** enthält.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>So legen Sie diese Compileroption in der Visual Studio-Entwicklungsumgebung fest  
  
1.  Öffnen Sie die Seite **Eigenschaften** des Projekts.  
  
2.  Klicken Sie auf die Eigenschaftenseite **Anwendung**.  
  
3.  Ändern Sie die Eigenschaft **Ausgabetyp**.  
  
 Informationen zum programmatischen Festlegen dieser Compileroption finden Sie unter <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## <a name="example"></a>Beispiel  
 Jede der folgenden Befehlszeilen wird `in.cs` kompilieren, wodurch `in.exe` erstellt wird:  
  
```  
csc /target:exe in.cs  
csc in.cs  
```  
  
## <a name="see-also"></a>Siehe auch  
 [/target (C#-Compileroptionen)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C#-Compileroptionen](../../../csharp/language-reference/compiler-options/index.md)
