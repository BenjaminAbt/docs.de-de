---
title: Ausdrucksbaumstrukturen (C#) | Microsoft-Dokumentation
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 7d0ac21a-6d90-4e2e-8903-528cb78615b7
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: 87195c8936aba485919d6c717fcbfaa1b282bddc
ms.lasthandoff: 03/31/2017

---
# <a name="expression-trees-c"></a>Ausdrucksbaumstrukturen (C#)
Ausdrucksbaumstrukturen stellen Code in einer baumähnlichen Datenstruktur dar, in denen jeder Knoten ein Ausdruck ist, z. B. ein Methodenaufruf oder eine binäre Operation wie `x < y`.  
  
 Sie können Code kompilieren und ausführen, der von Ausdrucksbaumstrukturen dargestellt wird. Dies ermöglicht dynamische Änderungen des ausführbaren Codes, die Ausführung von LINQ-Abfragen in verschiedenen Datenbanken und die Erstellung von dynamischen Abfragen. Weitere Informationen zu Ausdrucksbaumstrukturen in LINQ finden Sie unter [How to: Use Expression Trees to Build Dynamic Queries (C#) (Vorgehensweise: Verwenden von Ausdrucksbaumstrukturen zum Erstellen von dynamischen Abfragen (C#))](../../../../csharp/programming-guide/concepts/expression-trees/how-to-use-expression-trees-to-build-dynamic-queries.md).  
  
 Ausdrucksbaumstrukturen werden auch in der Dynamic Language Runtime (DLR) verwendet, um Interoperabilität zwischen dynamischen Sprachen und dem .NET-Framework zu gewährleisten und ermöglicht Entwicklern von Compilern, Ausdrucksbaumstrukturen anstelle der Microsoft Intermediate Language (MSIL) auszugeben. Weitere Informationen zur DLR finden Sie unter [Übersicht über die Dynamic Language Runtime](https://msdn.microsoft.com/library/dd233052).  
  
 Sie können den C#- oder Visual Basic-Compiler zur Erstellung einer Ausdrucksbaumstruktur veranlassen, basierend auf einem anonymen Lambdaausdruck, oder Sie können Ausdrucksbaumstrukturen durch Verwendung des Namespace <xref:System.Linq.Expressions> manuell erstellen.  
  
## <a name="creating-expression-trees-from-lambda-expressions"></a>Erstellen von Ausdrucksbaumstrukturen aus Lambda-Ausdrücken  
 Wenn ein Lambdaausdruck einer Variablen vom Typ <xref:System.Linq.Expressions.Expression%601> zugewiesen ist, gibt der Compiler Code aus, um eine Ausdrucksbaumstruktur zu erstellen, die den Lambdaausdruck verkörpert.  
  
 Der C#-Compiler kann Ausdrucksbaumstrukturen nur aus Ausdrucklambdas (oder einzeiligen Lambdas) erstellen. Es kann keine Anweisungslambdas (oder mehrzeiligen Lambdas) analysieren. Weitere Informationen zu Lambdaausdrücken in C# finden Sie unter [Lambdaausdrücke](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 In den folgenden Codebeispielen wird veranschaulicht, wie Sie C#-Compiler dazu veranlassen, eine Ausdrucksbaumstruktur zu erstellen, die den Lambdaausdruck `num => num < 5` verkörpert.  
  
```csharp  
Expression<Func<int, bool>> lambda = num => num < 5;  
```  
  
## <a name="creating-expression-trees-by-using-the-api"></a>Erstellen von Ausdrucksbaumstrukturen mit der API  
 Um Ausdrucksbaumstrukturen mit der API zu erstellen, verwenden Sie die Klasse <xref:System.Linq.Expressions.Expression>. Diese Klasse enthält statische Factorymethoden, die bestimmte Ausdrucksbaumstruktur-Knotentypen erstellen können, z.B. <xref:System.Linq.Expressions.ParameterExpression>, der eine Variable oder einen Parameter darstellt oder <xref:System.Linq.Expressions.MethodCallExpression>, der einen Methodenaufruf darstellt. <xref:System.Linq.Expressions.ParameterExpression>, <xref:System.Linq.Expressions.MethodCallExpression> und andere ausdrucksspezifische Typen sind ebenso im Namespace <xref:System.Linq.Expressions> definiert. Diese Typen stammen vom abstrakten Typ <xref:System.Linq.Expressions.Expression> ab.  
  
 Im folgenden Codebeispiel wird veranschaulicht, wie eine Ausdrucksbaumstruktur erstellt wird, die den Lambdaausdruck `num => num < 5` mithilfe der API verkörpert.  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Manually build the expression tree for   
// the lambda expression num => num < 5.  
ParameterExpression numParam = Expression.Parameter(typeof(int), "num");  
ConstantExpression five = Expression.Constant(5, typeof(int));  
BinaryExpression numLessThanFive = Expression.LessThan(numParam, five);  
Expression<Func<int, bool>> lambda1 =  
    Expression.Lambda<Func<int, bool>>(  
        numLessThanFive,  
        new ParameterExpression[] { numParam });  
```  
  
 In .NET Framework 4 oder höher unterstützt die Ausdrucksbaumstruktur-API auch Zuweisungen und Ablaufsteuerungsausdrücke wie Schleifen, bedingte Blöcke und `try-catch`-Blöcke. Mithilfe der API können Sie Ausdrucksbaumstrukturen erstellen, die komplexer sind als diejenigen, die von Lambda-Ausdrücken vom C#-Compiler erstellt werden. Im folgenden Beispiel wird veranschaulicht, wie eine Ausdrucksbaumstruktur erstellt wird, welche die Fakultät einer Zahl berechnet.  
  
```csharp  
// Creating a parameter expression.  
ParameterExpression value = Expression.Parameter(typeof(int), "value");  
  
// Creating an expression to hold a local variable.   
ParameterExpression result = Expression.Parameter(typeof(int), "result");  
  
// Creating a label to jump to from a loop.  
LabelTarget label = Expression.Label(typeof(int));  
  
// Creating a method body.  
BlockExpression block = Expression.Block(  
    // Adding a local variable.  
    new[] { result },  
    // Assigning a constant to a local variable: result = 1  
    Expression.Assign(result, Expression.Constant(1)),  
    // Adding a loop.  
        Expression.Loop(  
    // Adding a conditional block into the loop.  
           Expression.IfThenElse(  
    // Condition: value > 1  
               Expression.GreaterThan(value, Expression.Constant(1)),  
    // If true: result *= value --  
               Expression.MultiplyAssign(result,  
                   Expression.PostDecrementAssign(value)),  
    // If false, exit the loop and go to the label.  
               Expression.Break(label, result)  
           ),  
    // Label to jump to.  
       label  
    )  
);  
  
// Compile and execute an expression tree.  
int factorial = Expression.Lambda<Func<int, int>>(block, value).Compile()(5);  
  
Console.WriteLine(factorial);  
// Prints 120.  
```

Weitere Informationen finden Sie unter [Generating Dynamic Methods with Expression Trees in Visual Studio 2010 (Generieren dynamischer Methoden mit Ausdrucksbaumstrukturen in Visual Studio 2010)](http://go.microsoft.com/fwlink/p/?LinkId=169513). Dieser Artikel gilt auch für höhere Versionen von Visual Studio.
  
## <a name="parsing-expression-trees"></a>Analysieren von Ausdrucksbaumstrukturen  
 Im folgenden Codebeispiel wird veranschaulicht, wie die Ausdrucksbaumstruktur, die den Lambdaausdruck `num => num < 5` darstellt, in seine Bestandteile zerlegt werden kann.  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Create an expression tree.  
Expression<Func<int, bool>> exprTree = num => num < 5;  
  
// Decompose the expression tree.  
ParameterExpression param = (ParameterExpression)exprTree.Parameters[0];  
BinaryExpression operation = (BinaryExpression)exprTree.Body;  
ParameterExpression left = (ParameterExpression)operation.Left;  
ConstantExpression right = (ConstantExpression)operation.Right;  
  
Console.WriteLine("Decomposed expression: {0} => {1} {2} {3}",  
                  param.Name, left.Name, operation.NodeType, right.Value);  
  
// This code produces the following output:  
  
// Decomposed expression: num => num LessThan 5  
```  
  
## <a name="immutability-of-expression-trees"></a>Unveränderlichkeit von Ausdrucksbaumstrukturen  
 Ausdrucksbaumstrukturen sollten unveränderlich sein. Das heißt, wenn Sie eine Ausdrucksbaumstruktur ändern möchten, müssen Sie einen neuen Knoten konstruieren, indem Sie einen vorhandenen Knoten kopieren und die enthaltenen Knoten ersetzen. Sie können einen Ausdrucksbaumstruktur-Besucher verwenden, um die vorhandene Ausdrucksbaumstruktur zu durchlaufen. Weitere Informationen finden Sie unter [How to: Modify Expression Trees (C#) (Vorgehensweise: Bearbeiten von Ausdrucksbaumstrukturen (C#))](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md).  
  
## <a name="compiling-expression-trees"></a>Kompilieren von Ausdrucksbaumstrukturen  
 Der Typ <xref:System.Linq.Expressions.Expression%601> stellt die Methode <xref:System.Linq.Expressions.Expression%601.Compile%2A> bereit, die den durch eine Ausdrucksbaumstruktur dargestellten Code in einen ausführbaren Delegaten kompiliert.  
  
 Im folgenden Codebeispiel wird veranschaulicht, wie eine Ausdrucksbaumstruktur kompiliert und der daraus resultierende Code ausgeführt wird.  
  
```csharp  
// Creating an expression tree.  
Expression<Func<int, bool>> expr = num => num < 5;  
  
// Compiling the expression tree into a delegate.  
Func<int, bool> result = expr.Compile();  
  
// Invoking the delegate and writing the result to the console.  
Console.WriteLine(result(4));  
  
// Prints True.  
  
// You can also use simplified syntax  
// to compile and run an expression tree.  
// The following line can replace two previous statements.  
Console.WriteLine(expr.Compile()(4));  
  
// Also prints True.  
```  
  
 Weitere Informationen finden Sie unter [How to: Execute Expression Trees (C#) (Vorgehensweise: Ausführen von Ausdrucksbaumstrukturen (C#))](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Linq.Expressions>   
 [How to: Execute Expression Trees (C#) (Vorgehensweise: Ausführen von Ausdrucksbaumstrukturen (C#))](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)   
 [How to: Modify Expression Trees (C#) (Vorgehensweise: Bearbeiten von Ausdrucksbaumstrukturen (C#))](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md)   
 [Lambda-Ausdrücke](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Übersicht über die Dynamic Language Runtime](https://msdn.microsoft.com/library/dd233052)   
 [Programming Concepts (C#) (Programmierkonzepte (C#))](../../../../csharp/programming-guide/concepts/index.md)
