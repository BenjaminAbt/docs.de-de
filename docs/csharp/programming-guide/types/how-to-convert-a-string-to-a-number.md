---
title: "Gewusst wie: Konvertieren einer Zeichenfolge in eine Zahl (C#-Programmierhandbuch) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "Konvertierungen [C#]"
  - "Konvertierungen [C#], Zeichenfolge in ganzzahligen Typ"
  - "Konvertieren von Zeichenfolgen in ganzzahligen Typ [C#]"
  - "Zeichenfolgen [C#], Konvertieren in ganzzahligen Typ"
ms.assetid: 467b9979-86ee-4afd-b734-30299cda91e3
caps.latest.revision: 34
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 34
---
# Gewusst wie: Konvertieren einer Zeichenfolge in eine Zahl (C#-Programmierhandbuch)
Sie können eine [Zeichenfolge](../../../csharp/language-reference/keywords/string.md) mithilfe von Methoden in der <xref:System.Convert>\-Klasse oder durch die Verwendung der `TryParse`\-Methode, die in verschiedenen numerischen Typen \(int, long, float usw.\) Anwendung findet, in eine Zahl umwandeln.  
  
 Wenn Sie über eine Zeichenfolge verfügen, ist es etwas effizienter und einfacher, eine `TryParse`\-Methode \(beispielsweise `int.TryParse(“11”)`\) aufzurufen.  Die Verwendung einer `Convert`\-Methode eignet sich eher für allgemeine Objekte, die <xref:System.IConvertible> implementieren.  
  
 Sie können die Methode `Parse` oder `TryParse` für den numerischen Typ verwenden, den Sie in der Zeichenfolge erwarten, beispielsweise den <xref:System.Int32?displayProperty=fullName>\-Typ.  Die <xref:System.Convert.ToUInt32%2A?displayProperty=fullName>\-Methode verwendet <xref:System.Int32.Parse%2A> intern.  Wenn die Zeichenfolge in keinem gültigen Format vorliegt, löst `Parse` eine Ausnahme aus, während `TryParse` [false](../../../csharp/language-reference/keywords/false.md) zurückgibt.  
  
## Beispiel  
 Die Methoden `Parse` und `TryParse` ignorieren Leerzeichen am Anfang und Ende der Zeichenfolge. Alle anderen Zeichen müssen jedoch Zeichen sein, die den entsprechenden numerischen Typ bilden \(int, long, ulong, float, decimal usw.\).  Leerzeichen in den die Zahl bildenden Zeichen führen zu einem Fehler.  Beispielsweise können Sie `decimal.TryParse` verwenden, um „10“, „10.3“, „  10  „ zu analysieren. Sie können diese Methode jedoch nicht verwenden, um 10 aus „10X“, „1 0“ \(beachten Sie das Leerzeichen\), „10 .3“ \(beachten Sie das Leerzeichen\), „10e1“ \(`float.TryParse` funktioniert in diesem Fall\) usw. zu analysieren.  
  
 Die unten stehenden Beispiele zeigen erfolgreiche sowie nicht erfolgreiche Aufrufe von `Parse` und `TryParse`.  
  
 [!code-cs[csProgGuideTypes#5555](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_1.cs)]  
[!code-cs[csProgGuideTypes#25](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_2.cs)]  
[!code-cs[csProgGuideTypes#26](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_3.cs)]  
[!code-cs[csProgGuideTypes#27](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_4.cs)]  
[!code-cs[csProgGuideTypes#28](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_5.cs)]  
[!code-cs[csProgGuideTypes#100](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_6.cs)]  
  
## Beispiel  
 In der folgenden Tabelle werden einige der Methoden aus der <xref:System.Convert>\-Klasse aufgelistet, die Sie verwenden können.  
  
|Numerischer Typ|Methode|  
|---------------------|-------------|  
|`decimal`|<xref:System.Convert.ToDecimal%28System.String%29>|  
|`float`|<xref:System.Convert.ToSingle%28System.String%29>|  
|`double`|<xref:System.Convert.ToDouble%28System.String%29>|  
|`short`|<xref:System.Convert.ToInt16%28System.String%29>|  
|`int`|<xref:System.Convert.ToInt32%28System.String%29>|  
|`long`|<xref:System.Convert.ToInt64%28System.String%29>|  
|`ushort`|<xref:System.Convert.ToUInt16%28System.String%29>|  
|`uint`|<xref:System.Convert.ToUInt32%28System.String%29>|  
|`ulong`|<xref:System.Convert.ToUInt64%28System.String%29>|  
  
 In diesem Beispiel wird die <xref:System.Convert.ToInt32%28System.String%29?displayProperty=fullName>\-Methode aufgerufen, um einen Eingabe\-[string](../../../csharp/language-reference/keywords/string.md) in einen [int](../../../csharp/language-reference/keywords/int.md)\-Datentyp zu konvertieren.  Der Code fängt die zwei häufigsten Ausnahmen ab, die von dieser Methode ausgelöst werden können: <xref:System.FormatException> und <xref:System.OverflowException>.  Wenn die Zahl inkrementiert werden kann, ohne dass der integer\-Speicherbereich überläuft, fügt das Programm dem Ergebnis 1 hinzu und druckt die Ausgabe.  
  
 [!code-cs[csProgGuideTypes#5555](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_1.cs)]  
[!code-cs[csProgGuideTypes#24](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_7.cs)]  
  
## Siehe auch  
 [Typen](../../../csharp/programming-guide/types/index.md)   
 [Gewusst wie: Bestimmen, ob eine Zeichenfolge einen numerischen Wert darstellt](../../../csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)   
 [.NET Framework 4\-Hilfsprogramm zur Formatierung](http://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d)