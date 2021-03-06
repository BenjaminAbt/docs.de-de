---
title: base (C#-Referenz) | Microsoft-Dokumentation
description: base (C#-Referenz)
keywords: "base (C#), base-Schlüsselwort (C#), base-Schlüsselwort (C#-Referenz), base-Schlüsselwort (C#-Sprachreferenz)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- base
- BaseClass.BaseClass
- base_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- base keyword [C#]
ms.assetid: 8b645dbe-1a33-49b8-8716-1c401f9a5ea5
caps.latest.revision: 14
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
ms.openlocfilehash: adebe9f77cf1fe40a4aa8b00a2ef65c499d27ad3
ms.lasthandoff: 03/13/2017

---
# <a name="base-c-reference"></a>base (C#-Referenz)
Das `base`-Schlüsselwort wird verwendet, um aus einer abgeleiteten Klasse auf die Member der Basisklasse zuzugreifen:  
  
-   Rufen Sie eine Methode der Basisklasse auf, die durch eine andere Methode überschrieben wurde.  
  
-   Geben Sie an, welcher Konstruktor der Basisklasse beim Erstellen von Instanzen der abgeleiteten Klasse aufgerufen werden soll.  
  
 Zugriff auf eine Basisklasse ist nur in einem Konstruktor, einer Instanzenmethode oder einem Instanzeneigenschaften-Accessor zulässig.  
  
 Die Nutzung eines `base`-Schlüsselworts innerhalb einer statischen Methode ist ein Fehler.  
  
 Die Basisklasse, auf die zugegriffen wird, ist die Basisklasse, die in der Klassendeklaration angegeben ist. Wenn Sie z.B. `class ClassB : ClassA` angeben, wird von ClassB auf die Member von ClassA unabhängig von der Basisklasse von ClassA zugegriffen.  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel verfügen sowohl die Basisklasse `Person` als auch die abgeleitete Klasse `Employee` über eine Methode mit dem Namen `Getinfo`. Mithilfe des `base`-Schlüsselworts ist es möglich, die `Getinfo`-Methode der Basisklasse aus der abgeleiteten Klasse abzurufen.  
  
 [!code-cs[csrefKeywordsAccess#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/base_1.cs)]  
  
 Weitere Beispiele finden Sie unter [new](../../../csharp/language-reference/keywords/new.md), [virtual](../../../csharp/language-reference/keywords/virtual.md) und [override](../../../csharp/language-reference/keywords/override.md).  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird veranschaulicht, wie der aufgerufene Konstruktor der Basisklasse beim Erstellen von Instanzen einer abgeleiteten Klasse angegeben wird.  
  
 [!code-cs[csrefKeywordsAccess#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/base_2.cs)]  
  
## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Referenz](../../../csharp/language-reference/index.md)   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [C#-Schlüsselwörter](../../../csharp/language-reference/keywords/index.md)   
 [this](../../../csharp/language-reference/keywords/this.md)
