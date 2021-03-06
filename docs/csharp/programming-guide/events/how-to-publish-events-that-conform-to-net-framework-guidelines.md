---
title: "Vorgehensweise: Veröffentlichen von Ereignissen, die den .NET Framework-Richtlinien entsprechen (C#-Programmierhandbuch) | Microsoft-Dokumentation"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- events [C#], implementation guidelines
ms.assetid: 9310ae16-8627-44a2-b08c-05e5976202b1
caps.latest.revision: 31
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
ms.openlocfilehash: 78d069249c8131a091a206703c475faaf641d17b
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-publish-events-that-conform-to-net-framework-guidelines-c-programming-guide"></a>Gewusst wie: Veröffentlichen von Ereignissen, die den .NET Framework-Richtlinien entsprechen (C#-Programmierhandbuch)
Das folgende Verfahren veranschaulicht, wie Sie Ereignisse hinzufügen können, die dem [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]-Standardmuster ihrer Klassen und Strukturen folgen. Alle Ereignisse in der [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]-Klassenbibliothek basieren auf dem <xref:System.EventHandler>-Delegaten, der wie folgt definiert ist:  
  
```  
public delegate void EventHandler(object sender, EventArgs e);  
```  
  
> [!NOTE]
>  Das [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong_md.md)] führt eine generische Version dieses Delegaten ein: <xref:System.EventHandler%601>. Die folgenden Beispiele zeigen, wie Sie beide Versionen verwenden können.  
  
 Auch wenn Ereignisse in von Ihnen definierten Klassen auf jedem beliebigen Delegattyp basiert sein können – sogar Delegate, die einen Wert zurückgeben –, wird allgemein empfohlen, dass Sie Ihre Ereignisse mit <xref:System.EventHandler> auf dem [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]-Muster basieren, wie in folgendem Beispiel gezeigt.  
  
### <a name="to-publish-events-based-on-the-eventhandler-pattern"></a>So veröffentlichen Sie Ereignisse, die auf dem EventHandler-Muster basieren  
  
1.  (Überspringen Sie diesen Schritt, und gehen Sie direkt zu Schritt 3a, wenn Sie keine benutzerdefinierten Daten mit Ihrem Ereignis senden müssen.) Deklarieren Sie die Klasse Ihrer benutzerdefinierten Daten in einem für Ihre Herausgeber- und Ihre Abonnentenklasse sichtbaren Geltungsbereich. Fügen Sie dann die erforderlichen Member hinzu, die Ihre benutzerdefinierten Ereignisdaten enthalten sollen. In diesem Beispiel wird eine einzelne Zeichenfolge zurückgegeben.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
2.  (Überspringen Sie diesen Schritt, wenn Sie eine generische Version von <xref:System.EventHandler%601> verwenden.) Deklarieren Sie einen Delegaten in Ihrer Herausgeberklasse. Geben Sie ihm einen Namen, der auf *EventHandler* endet. Der zweite Parameter gibt Ihren benutzerdefinierten EventArgs-Typen an.  
  
    ```  
    public delegate void CustomEventHandler(object sender, CustomEventArgs a);  
    ```  
  
3.  Deklarieren Sie das Ereignis in Ihrer Herausgeberklasse, indem Sie einen der folgenden Schritte verwenden.  
  
    1.  Wenn Sie keine benutzerdefinierte EventArgs-Klasse haben, ist Ihr Ereignistyp der nicht generische EventHandler-Delegat. Sie müssen den Delegaten nicht deklarieren, da er schon im <xref:System>-Namespace deklariert wurde, der bei der Erstellung Ihres C#-Projekts erstellt wird. Fügen Sie den folgenden Code in Ihre Herausgeberklasse ein.  
  
        ```  
        public event EventHandler RaiseCustomEvent;  
        ```  
  
    2.  Wenn Sie die nicht generische Version von <xref:System.EventHandler> verwenden, und Sie eine benutzerdefinierte Klasse haben, die von <xref:System.EventArgs> abgeleitet ist, deklarieren Sie Ihr Ereignis innerhalb Ihrer Herausgeberklasse, und verwenden Sie Ihren Delegaten aus Schritt 2 als Typ.  
  
        ```  
        public event CustomEventHandler RaiseCustomEvent;  
  
        ```  
  
    3.  Wenn sie die generische Version verwenden, benötigen Sie keinen benutzerdefinierten Delegaten. Stattdessen geben Sie in Ihrer Herausgeberklasse Ihren Ereignistypen als `EventHandler<CustomEventArgs>` an und fügen den Namen Ihrer eigenen Klasse in die eckigen Klammern ein.  
  
        ```  
        public event EventHandler<CustomEventArgs> RaiseCustomEvent;  
        ```  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel veranschaulicht die oben genannten Schritte durch das Verwenden von einer benutzerdefinierten EventArgs-Klasse und von <xref:System.EventHandler%601> als Ereignistyp.  
  
 [!code-cs[csProgGuideEvents#2](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-publish-events-that-conform-to-net-framework-guidelines_1.cs)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Delegate>   
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)   
 [Ereignisse](../../../csharp/programming-guide/events/index.md)   
 [Delegaten](../../../csharp/programming-guide/delegates/index.md)
