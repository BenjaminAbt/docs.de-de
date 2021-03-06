---
title: "Gewusst wie: Schreiben eines Kopierkonstruktors (C#-Programmierhandbuch) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "Die Programmiersprache C#, Kopierkonstruktor"
  - "Kopierkonstruktor [C#]"
ms.assetid: fba899b5-fc41-428e-a745-3ebdbf37990a
caps.latest.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 20
---
# Gewusst wie: Schreiben eines Kopierkonstruktors (C#-Programmierhandbuch)
C\# stellt keinen Kopierkonstruktor für Objekte bereit. Sie können jedoch selbst einen schreiben.  
  
## Beispiel  
 Im folgenden Beispiel wird von der `Person`\-[Klasse](../../../csharp/language-reference/keywords/class.md) ein Kopierkonstruktor definiert, der eine Instanz von `Person` als sein Argument annimmt.  Die Werte der Eigenschaften des Arguments werden den Eigenschaften der neuen Instanz von `Person` zugewiesen.  Der Code enthält einen alternativen Kopierkonstruktor, der die `Name`\- und `Age`\-Eigenschaften der Instanz sendet, die Sie in den Instanzenkonstruktor der Klasse kopieren möchten.  
  
 [!code-cs[csProgGuideObjects#16](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-write-a-copy-constructor_1.cs)]  
  
## Siehe auch  
 <xref:System.ICloneable>   
 [C\#\-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [Klassen und Strukturen](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [Konstruktoren](../../../csharp/programming-guide/classes-and-structs/constructors.md)   
 [Destruktoren](../../../csharp/programming-guide/classes-and-structs/destructors.md)