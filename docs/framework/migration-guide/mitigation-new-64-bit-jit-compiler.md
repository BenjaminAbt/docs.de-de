---
title: "Entschärfung: Neuer 64-Bit-JIT-Compiler | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JIT compiler, 64-bit
- JIT compilation, 64-bit
- RyuJIT compiler
ms.assetid: 0332dabc-72c5-4bdc-8975-20d717802b17
caps.latest.revision: 6
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 994da1622246d09930fa9b74d6debac4f7a24b5b
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-new-64-bit-jit-compiler"></a>Entschärfung: Neuer 64-Bit-JIT-Compiler
Ab .NET Framework 4.6 enthält die Runtime einen neuen 64-Bit-JIT-Compiler für die Just-in-Time-Kompilierung. Diese Änderung wirkt sich nicht auf die Kompilierung mit dem 32-Bit-JIT-Compiler aus.  
  
## <a name="unexpected-behavior-or-exceptions"></a>Unerwartetes Verhalten oder Ausnahmen  
 In einigen Fällen führt die Kompilierung mit dem neuen 64-Bit-JIT-Compiler zu einer Laufzeitausnahme oder zu Verhalten, das beim Ausführen von mit dem älteren 64-Bit-JIT-Compiler kompiliertem Code nicht zu beobachten ist. Die bekannten Unterschiede umfassen folgende Punkte:  
  
> [!IMPORTANT]
>  Alle diese bekannten Probleme wurden im neuen 64-Bit-Compiler behoben, der mit .NET Framework 4.6.2 veröffentlicht wurde. Die meisten wurden auch in Service Releases von .NET Framework 4.6 und 4.6.1 behoben, die in Windows Update enthalten sind. Sie können diese Probleme vollständig beseitigen, indem Sie sicherstellen, dass Ihre Windows-Version auf dem aktuellen Stand ist oder ein Upgrade auf .NET Framework 4.6.2 ausführen.  
  
-   Unter bestimmten Umständen kann ein Unboxingvorgang in Releasebuilds mit aktivierter Optimierung eine <xref:System.NullReferenceException>-Ausnahme auslösen.  
  
-   In manchen Fällen kann bei der Ausführung von Produktionscode in einem großen Methodentext eine <xref:System.StackOverflowException>-Ausnahme ausgelöst werden.  
  
-   Unter bestimmtem Bedingungen werden in Releasebuilds an eine Methode übergebene Strukturen als Verweistypen statt als Werttypen behandelt. Eins der Anzeichen dieses Problems besteht darin, dass die einzelnen Elemente einer Sammlung in unerwarteter Reihenfolge angezeigt werden.  
  
-   Unter bestimmten Bedingungen ist der Vergleich von <xref:System.UInt16>-Werten mit festgelegtem hohem Bit fehlerhaft, wenn Optimierung aktiviert ist.  
  
-   Unter bestimmten Umständen, insbesondere beim Initialisieren von Arraywerten, kann die Speicherinitialisierung durch die <xref:System.Reflection.Emit.OpCodes.Initblk?displayProperty=fullName>-IL-Anweisung mit einem falschen Wert erfolgen. Dies kann entweder zu einem Ausnahmefehler oder zu einer falschen Ausgabe führen.  
  
-   Unter bestimmten seltenen Bedingungen kann ein bedingter Bittest den falschen <xref:System.Boolean>-Wert zurückgeben oder eine Ausnahme auslösen, wenn Compileroptimierungen aktiviert sind.  
  
-   Wenn unter bestimmten Umständen eine `if`-Anweisung für die Prüfung auf eine Bedingung vor dem Eintritt in einen `try`-Block oder beim Verlassen eines `try`-Blocks erfolgt und die gleiche Bedingung im `catch`- oder `finally`-Block ausgewertet wird, entfernt der neue 64-Bit-JIT-Compiler beim Optimieren von Code die `if`-Bedingung aus dem `catch`- oder `finally`-Block. Daher wird Code innerhalb der `if`-Anweisung im `catch`- oder `finally`-Block ohne Bedingung ausgeführt.  
  
<a name="General"></a>   
## <a name="mitigation-of-known-issues"></a>Entschärfung bekannter Probleme  
 Wenn bei Ihnen die oben aufgeführten Probleme auftreten, können Sie darauf mit einer der folgenden Maßnahmen reagieren:  
  
-   Ausführen eines Upgrades auf .NET Framework 4.6.2. Der neue 64-Bit-Compiler, der in .NET Framework 4.6.2 enthalten ist, behebt jedes dieser bekannten Probleme.  
  
-   Stellen Sie sicher, dass ihre Windows-Version auf dem aktuellen Stand ist, indem Sie Windows Update ausführen. Serviceupdates für .NET Framework 4.6 und 4.6.1 beheben jedes dieser Probleme, mit Ausnahme der <xref:System.NullReferenceException>-Ausnahme bei Unboxingvorgängen.  
  
-   Kompilieren Sie mit dem älteren 64-Bit-JIT-Compiler. Informationen zum Vorgehen dazu finden Sie unter [Entschärfung anderer Probleme](#Other).  
  
<a name="Other"></a>   
## <a name="mitigation-of-other-issues"></a>Entschärfung anderer Probleme  
 Wenn Sie andere Unterschiede im Verhalten zwischen Code, der mit dem älteren 64-Bit-Compiler kompiliert wurde, gegenüber mit dem neuen 64-Bit-JIT-Compiler kompiliertem Code oder zwischen den Debug- und Releaseversionen Ihrer App feststellen, die beide mit dem neuen 64-Bit-JIT-Compiler kompiliert wurden, können Sie folgendermaßen vorgehen, um Ihre App mit dem älteren 64-Bit-JIT-Compiler zu kompilieren:  
  
-   Sie können der Konfigurationsdatei Ihrer Anwendung auf Anwendungsbasis das [\<useLegacyJIT>](../../../docs/framework/configure-apps/file-schema/runtime/uselegacyjit-element.md)-Element hinzufügen. Die folgende Anweisung deaktiviert die Kompilierung mit dem neuen 64-Bit-JIT-Compiler und verwendet stattdessen den 64-Bit-Legacy-JIT-Compiler.  
  
    ```xml  
  
    <?xml version ="1.0"?>  
    <configuration>  
        <runtime>  
           <useLegacyJIT enabled="1" />  
        </runtime>  
    </configuration>  
  
    ```  
  
-   Auf Benutzerbasis können Sie dem `HKEY_CURRENT_USER\SOFTWARE\Microsoft\.NETFramework`-Wert der Registrierung einen `REG_DWORD`-Wert mit dem Namen `useLegacyJit` hinzufügen. Der Wert 1 aktiviert den 64-Bit-Legacy-JIT-Compiler, der Wert 0 deaktiviert ihn und aktiviert stattdessen den neuen 64-Bit-JIT-Compiler.  
  
-   Auf Computerbasis können Sie dem `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework`-Schlüssel der Registrierung einen `REG_DWORD`-Wert mit dem Namen `useLegacyJit` hinzufügen. Der Wert 1 aktiviert den 64-Bit-Legacy-JIT-Compiler, der Wert 0 deaktiviert ihn und aktiviert stattdessen den neuen 64-Bit-JIT-Compiler.  
  
 Ferner können Sie uns über das Problem informieren, indem Sie einen Bug auf [Microsoft Connect](https://connect.microsoft.com/VisualStudio) melden.  
  
## <a name="see-also"></a>Siehe auch  
 [Laufzeitänderungen](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-6.md)   
 [\<useLegacyJIT> Element](../../../docs/framework/configure-apps/file-schema/runtime/uselegacyjit-element.md)
