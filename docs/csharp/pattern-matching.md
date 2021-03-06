---
title: "Musterabgleich | Leitfaden für C#"
description: "Erfahren Sie mehr über Musterabgleichausdrücke in C#"
keywords: .NET, .NET Core, C#
ms.date: 01/24/2017
ms.author: wiwagn
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 1e575c32-2e2b-4425-9dca-7d118f3ed15b
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c5b1ef4b6de108e2ea3967630e9e37e52a97245c
ms.lasthandoff: 03/13/2017

---

# <a name="pattern-matching"></a>Musterabgleich #

Muster testen, ob ein Wert eine bestimmte *Form* hat, und können Informationen vom Wert *extrahieren*, wenn er die entsprechende Form hat. Der Musterabgleich stellt eine kürzere Syntax für Algorithmen bereit, die Sie bereits verwenden. Sie erstellen bereits mithilfe vorhandener Syntax Musterabgleichalgorithmen. Sie schreiben `if`- oder `switch`-Anweisungen, die Werte testen. Wenn diese Anweisungen anschließend übereinstimmen, extrahieren und verwenden Sie die Informationen von diesem Wert. Die neuen Syntaxelemente sind Erweiterungen für Anweisungen, mit denen Sie bereits vertraut sind: `is` und `switch`. Diese neuen Erweiterungen kombinieren das Testen von Werten mit dem Extrahieren dieser Information.

In diesem Thema wird die neue Syntax betrachtet, um Ihnen zu zeigen, wie dadurch ein lesbarer, kurzer Code ermöglicht wird. Ein Musterabgleich ermöglicht Idiome, bei denen Daten und der Code getrennt sind, im Gegensatz zu objektorientierten Entwürfen, bei denen Daten und die Methoden, die sie bearbeiten, eng gekoppelt sind.

Wir arbeiten mit Strukturen, die geometrische Formen mithilfe Musterabgleichanweisungen darstellen, um diese neuen Idiome zu veranschaulichen. Sie sind wahrscheinlich mit dem Erstellen von Klassenhierarchien und dem Erstellen [virtueller und überschriebener Methoden](methods.md#inherited) vertraut, um Objektverhalten anhand des Laufzeittyps des Objekts anzupassen.

Diese Techniken sind nicht für Daten geeignet, die nicht in einer Klassenhierarchie strukturiert sind. Wenn Daten und Methoden getrennt sind, benötigen Sie andere Tools. Die neuen *Musterabgleichkonstrukte* ermöglichen eine saubere Syntax, um Daten zu untersuchen und anhand jeder Bedingung dieser Daten Steuerungsflüsse zu bearbeiten. Sie schreiben bereits `if`-Anweisungen und `switch`, die den Wert einer Variable testen. Sie schreiben `is`-Anweisungen, die einen Typ einer Variable testen. *Musterabgleich* fügt neue Funktionen zu diesen Anweisungen hinzu.

In diesem Thema erstellen Sie eine Methode, die den Bereich der verschiedenen geometrischen Formen berechnet. Aber Sie tun dies, ohne auf objektorientierte Techniken zurückzugreifen und eine Klassenhierarchie für die verschiedenen Formen zu erstellen.
Sie verwenden stattdessen *Musterabgleich*. Sie machen jede Form zu einem `struct` anstatt zu einer Klasse, um weiter hervorzuheben, dass wir keine Vererbung verwenden. Beachten Sie, dass unterschiedliche `struct`-Typen keinen normalen benutzerdefinierten Basistyp angeben können, sodass Vererbung kein möglicher Entwurf ist.
Während Sie dieses Beispiel bearbeiten, vergleichen Sie diesen Code damit, wie er als Objekthierarchie strukturiert wäre. Wenn die Klasse, die Sie abfragen und bearbeiten müssen, keine Klassenhierarchie ist, ermöglicht Musterabgleich sehr elegante Entwürfe.

Anstatt mit einer Definition einer abstrakten Form zu starten und verschiedene bestimmte Formklassen hinzuzufügen, beginnen wir mit einfachen reinen Datendefinitionen für jede der geometrischen Formen:

[!code-csharp[ShapeDefinitions](../../samples/csharp/PatternMatching/Shapes.cs#01_ShapeDefinitions "Formdefinitionen")]

Wir schreiben von diesen Strukturen eine Methode, die den Bereich einiger Formen berechnet.

## <a name="the-is-type-pattern-expression"></a>Der Musterausdruck des `is`-Typs

Vor C# 7 mussten Sie jeden Typ in einer Reihe von `if`- und `is`-Anweisungen testen:

[!code-csharp[ClassicIsExpression](../../samples/csharp/PatternMatching/GeometricUtilities.cs#02_ClassicIsExpression "Klassisches Typmuster mit „is“")]

Der oben dargestellte Code ist ein klassischer Ausdruck des *Typmusters*: Sie testen eine Variable, um ihren Typ zu bestimmen, und handeln anhand dieses Typs unterschiedlich.

Dieser Code wird einfacher, indem Sie Erweiterungen für den `is`-Ausdruck verwenden, um eine Variable zuzuweisen, wenn der Test erfolgreich ausgeführt wird:

[!code-csharp[IsPatternExpression](../../samples/csharp/PatternMatching/GeometricUtilities.cs#03_IsPatternExpression "Musterausdruck „is“")]

In dieser aktualisierten Version testet der `is`-Ausdruck die Variable und weist sie einer neuen Variablen des richtigen Typs zu. Beachten Sie ebenfalls, dass die Version den `Rectangle`-Typ enthält, der ein `struct` ist. Der neue `is`-Ausdruck funktioniert mit Werttypen sowie mit Verweistypen.

Sprachregeln für Musterabgleichausdrücke helfen Ihnen, das Ergebnis eines Musterausdrucks nicht falsch zu verwenden. Im obigen Beispiel sind die Variablen `s`,  `c` und `r` nur im Geltungsbereich und werden definitiv zugewiesen, wenn die entsprechenden Musterabgleichausdrücke `true`-Ergebnisse haben. Wenn Sie versuchen, eine der Variablen an einem anderen Ort zu verwenden, erzeugt Ihr Code Compilerfehler.

Betrachten wir beide dieser Regeln im Detail, beginnend mit dem Geltungsbereich. Die Variable `c` ist im Geltungsbereich nur im `else`-Zweig der ersten `if`-Anweisung. Die Variable `s` liegt im Geltungsbereich in der Methode `ComputeArea`. Jeder Zweig einer `if`-Anweisung bildet nämlich einen separaten Geltungsbereich für Variablen. Die eigentliche `if`-Anweisung macht dies jedoch nicht. Das bedeutet, dass Variablen, die in der `if`-Anweisung deklariert wurden, im gleichen Geltungsbereich der `if`-Anweisung sind (in diesem Fall die Methode). Dieses Verhalten ist nicht spezifisch für den Musterabgleich, entspricht jedoch dem definierten Verhalten für variable Geltungsbereiche sowie für `if`- und `else`-Anweisungen.

Die Variablen `c` und `s` werden zugewiesen, wenn die jeweiligen `if`-Anweisungen aufgrund des definitiv zugewiesenen „when true“-Mechanismus „true“ sind.

> [!TIP]
> Die Beispiele in diesem Thema verwenden die empfohlenen Konstrukte, bei denen ein `is`-Ausdruck des Musterabgleichs definitiv die Mustervariable im `true`-Zweig der `if`-Anweisung zuweist.
> Sie können die Logik umdrehen, indem Sie sagen, dass `if (!(shape is Square s))` und die Variable `s` definitiv nur im `false`-Zweig zugewiesen seien. Obwohl das in C# gültig ist, wird es nicht empfohlen, da diese Logik komplizierter ist.

Diese Regeln bedeuten, dass Sie wahrscheinlich nicht versehentlich auf das Ergebnis eines Musterabgleichausdrucks zugreifen, wenn das Muster nicht erfüllt wurde.

## <a name="using-pattern-matching-switch-statements"></a>Musterabgleich mit `switch`-Anweisungen

Im Laufe der Zeit müssen Sie vielleicht andere Formtypen unterstützen. Mit der steigenden Anzahl von Bedingungen, die Sie testen, werden Sie feststellen, dass die Verwendung der `is`-Musterabgleichausdrücke sehr umständlich werden kann. Zusätzlich zum Bedarf an `if`-Ausdrücken für jeden Typ, den Sie testen möchten, schränken die `is`-Ausdrücke das Testen ein, wenn die Eingabe mit einem einzigen Typ übereinstimmt. In diesem Fall stellen Sie fest, dass die Musterabgleichausdrücke `switch` zu einer besseren Wahl werden. 

Die herkömmliche `switch`-Anweisung war ein Musterausdruck: Sie unterstützte das Konstantenmuster.
Sie können eine Variable mit einer beliebigen Konstante vergleichen, die in einer `case`-Anweisung verwendet wird:

[!code-csharp[ClassicSwitch](../../samples/csharp/PatternMatching/GeometricUtilities.cs#04_ClassicSwitch "Klassische switch-Anweisung")]

Das einzige Muster, das von der `switch`-Anweisung unterstützt wurde, war das Konstantenmuster. Sie war zudem auf numerische Typen und den `string`-Typ beschränkt.
Diese Einschränkungen wurden entfernt, und Sie können nun eine `switch`-Anweisung mit dem Typmuster schreiben:

[!code-csharp[Switch Type Pattern](../../samples/csharp/PatternMatching/GeometricUtilities.cs#05_SwitchTypePattern "Mit switch-Ausdruck berechnen")]

Die `switch`-Anweisung des Musterabgleichs verwendet ähnliche Syntax für Entwickler, die die `switch`-Anweisung im klassischen C-Stil verwendet haben. Jede `case` wird ausgewertet und der Code unterhalb der Bedingung, die mit der Eingabevariablen übereinstimmt, wird ausgeführt. Die Codeausführung kann nicht von einem case-Ausdruck in den nächsten „fortfahren“; die Syntax der `case`-Anweisung erfordert, dass jede `case` mit `break`, `return` oder `goto` endet.

> [!NOTE]
> Die `goto`-Anweisungen, die auf eine andere Bezeichnung springen, sind nur für das Konstantenmuster, die klassische switch-Anweisung, gültig.

Es gibt wichtige neue Regeln für die `switch`-Anweisung. Die Beschränkungen für den Typ der Variablen im `switch`-Ausdruck sind entfernt worden.
Jeder Typ wie `object` in diesem Beispiel kann verwendet werden. Die case-Ausdrücke sind nicht mehr auf konstante Werte beschränkt. Das Entfernen dieser Beschränkung bedeutet, dass das Neuanordnen von `switch`-Abschnitten das Verhalten eines Programms verändern kann.

Solange sie auf konstante Werte beschränkt waren, konnte nicht mehr als eine `case`-Bezeichnung mit dem Wert des `switch`-Ausdrucks übereinstimmen. Verbinden Sie das mit der Regel, das jeder `switch`-Abschnitt nicht im nächsten Abschnitt fortfahren darf, und daraus folgt, dass die `switch`-Abschnitte in jeder Reihenfolge neu angeordnet werden konnten, ohne das Verhalten zu beeinflussen.
Nun spielt die Reihenfolge von jedem Abschnitt mit verallgemeinerten `switch`-Ausdrücken eine Rolle. Die `switch`-Ausdrücke werden in der Reihenfolge ausgewertet, in der sie im Text auftreten. Die Ausführung wechselt zur ersten `switch`-Bezeichnung, die mit dem `switch`-Ausdruck übereinstimmt.  
Beachten Sie, dass der `default`-case nur ausgeführt wird, wenn keine andere case-Bezeichnung übereinstimmt. Der `default`-case wird zuletzt bewertet, unabhängig von der Reihenfolge im Text. Wenn kein `default`-case existiert und keine anderen `case`-Ausdrücke übereinstimmen, wird die Ausführung an der Anweisung nach der `switch`-Anweisung fortgesetzt. Kein Code der `case`-Bezeichnungen wird ausgeführt.

## <a name="when-clauses-in-case-expressions"></a>`when`-Klauseln in `case`-Ausdrücken

Sie können Sonderfälle für diese Formen erstellen, die einen 0-Bereich haben, indem Sie eine `when`-Klausel in der `case`-Bezeichnung verwenden. Ein Quadrat mit einer Seitenlänge von 0 oder ein Kreis mit einem Radius von 0 hat einen 0-Bereich. Sie geben diese Bedingung mithilfe einer `when`-Klausel für die `case`-Bezeichnung an:  

[!code-csharp[ComputeDegenerateShapes](../../samples/csharp/PatternMatching/GeometricUtilities.cs#07_ComputeDegenerateShapes "Formen mit 0-Bereich berechnen")]

Diese Änderung veranschaulicht einige wichtige Punkte hinsichtlich der neuen Syntax. Zuerst können mehrere `case`-Bezeichnungen auf den `switch`-Abschnitt angewendet werden. Der Anweisungsblock wird ausgeführt, wenn eine dieser Bezeichnungen `true` ist. Wenn in diesem Fall der `switch`-Ausdruck entweder ein Kreis oder ein Quadrat mit einem 0-Bereich ist, gibt die Methode die Konstante 0 zurück.

In diesem Beispiel werden zwei verschiedene Variablen in den zwei `case`-Bezeichnungen für den ersten `switch`-Block ausgeführt. Beachten Sie, dass die Anweisungen in diesem `switch`-Block weder die Variablen `c` (für den Kreis) noch `s` (für das Quadrat) verwenden.
Keine dieser Variablen wird definitiv in diesem `switch`-Block zugewiesen.
Wenn einer der Fälle übereinstimmt, wurde eindeutig eine der Variablen zugewiesen.
Allerdings ist es unmöglich zu sagen, *welche* während der Kompilierung zugewiesen wurde, da beide Fälle zur Laufzeit übereinstimmen könnten. Wenn Sie aus diesem Grund meistens mehrere `case`-Bezeichnungen für denselben Block verwenden, werden Sie keine neue Variable in die `case`-Anweisung einführen oder die Variable nur in der `when`-Klausel verwenden.

Nachdem diese Formen mit 0-Bereich hinzugefügt wurden, werden wir ein paar weitere Formtypen einfügen: ein Rechteck und ein Dreieck:

[!code-csharp[AddRectangleAndTriangle](../../samples/csharp/PatternMatching/GeometricUtilities.cs#09_AddRectangleAndTriangle "Rechteck und Dreieck hinzufügen")]

 Dieser Satz von Änderungen fügt `case`-Bezeichnungen für den degenerierten case und Bezeichnungen und Blöcke für jede der neuen Formen hinzu. 

Zuletzt können Sie einen `null`-case hinzufügen, um sicherzustellen, dass das Argument nicht `null` ist:

[!code-csharp[NullCase](../../samples/csharp/PatternMatching/GeometricUtilities.cs#10_NullCase "NULL-Case hinzufügen")]

Der Sonderfall für das `null`-Muster ist interessant, weil die Konstante `null` keinen Typ besitzt, aber in jeden Referenztyp oder Typ, der NULL-Werte zulässt, konvertiert werden kann. 

## <a name="conclusions"></a>Zusammenfassung

*Musterabgleichkonstrukte* helfen Ihnen, den Steuerungsfluss zwischen verschiedenen Variablen und Typen, die nicht durch eine Vererbungshierarchie verknüpft sind, einfach zu verwalten. Sie können auch die Logik steuern, um jede Bedingung, die Sie testen, in der Variable zu verwenden. Das ermöglicht Ihnen Muster und Idiome, die Sie häufiger brauchen werden, wenn Sie mehr verteilte Anwendungen entwickeln, bei denen Daten und die Methoden, die diese Daten bearbeiten, getrennt sind. Sie werden bemerken, dass die Formstrukturen, die in diesem Beispiel verwendet wurden, keine Methoden enthält, sondern nur schreibgeschützte Eigenschaften.
Musterabgleich funktioniert mit jedem Datentyp. Sie erstellen Ausdrücke, die das Objekt untersuchen und Steuerungsflussentscheidungen anhand dieser Bedingungen treffen.

Vergleichen Sie den Code in diesem Beispiel mit dem Entwurf, der aus dem Erstellen einer Klassenhierarchie für eine abstrakte `Shape` und spezifisch abgeleitete Formen folgen würde, von denen jede ihre eigene Implementierung einer virtuellen Methode hat, um den Bereich zu berechnen. Sie werden häufig feststellen, dass Musterabgleichausdrücke sehr nützlich sein können, wenn Sie mit Daten arbeiten und die Datenspeicherprobleme von den Verhaltensproblemen trennen möchten.


