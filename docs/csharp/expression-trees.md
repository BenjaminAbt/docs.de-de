---
title: Expression Trees
description: Expression Trees
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: aceb4719-0d5a-4b19-b01f-b51063bcc54f
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e6ec60b6cdbe29def719f7970dad15fad65902e7
ms.lasthandoff: 03/13/2017

---

# <a name="expression-trees"></a>Expression Trees

Wenn Sie LINQ verwendet haben, verfügen Sie über Erfahrung mit einer umfangreichen Bibliothek, in der die `Func`-Typen Teil des API-Satzes sind. (Wenn Sie nicht mit LINQ vertraut sind, möchten Sie möglicherweise vorher [das LINQ-Tutorial](linq/index.md) und das Tutorial zu [lambda expressions (Lambdaausdrücke)](lambda-expressions.md) lesen.) *Ausdrucksbaumstrukturen* bieten eine umfangreichere Interaktion mit den Argumenten, die Funktionen sind.

Sie schreiben die Argumente der Funktion in der Regel mithilfe von Lambdaausdrücken, wenn Sie LINQ-Abfragen erstellen. In einer normalen LINQ-Abfrage werden die Funktionsargumente in einen Delegaten transformiert, den der Compiler erstellt. 

Wenn Sie eine umfangreichere Interaktion haben möchten, müssen Sie *Ausdrucksbaumstrukturen* verwenden.
Ausdrucksbaumstrukturen stellen Code wie eine Struktur dar, die Sie untersuchen, ändern oder ausführen können. Diese Tools bieten Ihnen die Möglichkeit, Code während der Laufzeit zu ändern. Sie können Code schreiben, der ausgeführte Algorithmen untersucht oder neue Funktionen einfügt. In erweiterten Szenarios können Sie ausgeführte Algorithmen ändern und sogar C#-Ausdrücke für die Ausführung in einer anderen Umgebung in eine andere Form übersetzen.

Sie haben wahrscheinlich bereits Code geschrieben, der Ausdrucksbaumstrukturen verwendet. LINQ-APIs von Entity Framework akzeptieren Ausdrucksbaumstrukturen als Argumente für das LINQ-Abfrageausdrucksmuster.
So kann [Entity Framework](http://docs.efproject.net/en/latest/) die Abfrage übersetzen, die Sie in C# in SQL geschrieben haben, die im Datenbankmodul ausgeführt wird. Ein weiteres Beispiel ist [Moq](https://github.com/Moq/moq), was ein beliebtes Mockingframework für .NET ist.

In den verbleibenden Abschnitten dieses Tutorials wird untersucht, was Ausdrucksbaumstrukturen sind, es werden die Framework-Klassen untersucht, die Ausdrucksbaumstrukturen unterstützen, und es wird gezeigt, wie Sie mit Ausdrucksbaumstrukturen arbeiten. Sie erfahren, wie Sie Ausdrucksbaumstrukturen lesen und diese erstellen, wie Sie geänderte Ausdrucksbaumstrukturen erstellen und wie Sie Code von dargestellten Ausdrucksbaumstrukturen ausführen. Nach dem Lesen können Sie mit diesen Strukturen umfangreiche adaptive Algorithmen erstellen.
<style type="text/css"> ol { list-style-type: upper-roman; } </style>
1. [Expression Trees Explained (Ausdrucksbaumstrukturen erklärt)](expression-trees-explained.md)

    Understand the structure and concepts behind *Expression Trees*.
    
2. [Framework-Typen, die Ausdrucksbaumstrukturen unterstützen](expression-classes.md)
    
    Erfahren Sie mehr über die Strukturen und Klassen, die Ausdrucksbaumstrukturen definieren und bearbeiten.
    
3. [Ausführen von Ausdrücken](expression-trees-execution.md)

    Erfahren Sie, wie Sie eine Ausdrucksbaumstruktur, die als Lambdaausdruck dargestellt wird, in einen Delegaten konvertieren, und wie Sie den resultierenden Delegaten ausführen.

4. [Interpretieren von Ausdrücken](expression-trees-interpreting.md)

    Erfahren Sie, wie Sie *Ausdrucksbaumstrukturen* durchlaufen und untersuchen, um zu verstehen, welchen Code die Ausdrucksbaumstruktur darstellt.

5. [Erstellen von Ausdrücken](expression-trees-building.md)

    Erfahren Sie, wie Sie die Knoten für eine Ausdrucksbaumstruktur erstellen, und wie Sie Ausdrucksbaumstrukturen erstellen.

6. [Übersetzen von Ausdrücken](expression-trees-translating.md)

    Erfahren Sie, wie Sie eine geänderte Kopie einer Ausdrucksbaumstruktur erstellen oder wie Sie eine Ausdrucksbaumstruktur in ein anderes Format übersetzen.

7. [Schlussbemerkung](expression-trees-summary.md)

    Überprüfen Sie die Informationen zu Ausdrucksbaumstrukturen.
    

