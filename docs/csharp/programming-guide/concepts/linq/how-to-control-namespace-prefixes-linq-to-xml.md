---
title: "Vorgehensweise: Steuern von Namespacepräfixen (C#) (LINQ to XML) | Microsoft-Dokumentation"
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
ms.assetid: 64de5186-b81a-4ddd-8327-8693df59a01b
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 96bc6d1187aa72f8653cd01b2027306009634fd5
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-control-namespace-prefixes-c-linq-to-xml"></a>Gewusst wie: Steuern von Namespacepräfixen (C#) (LINQ to XML)
In diesem Thema wird beschrieben, wie Sie beim Serialisieren einer XML-Struktur Namespacepräfixe steuern können.  
  
 In vielen Situationen ist es nicht notwendig, die Namespacepräfixe zu steuern.  
  
 Bestimmte XML-Programmiertools erfordern jedoch eine spezifische Steuerung der Namespacepräfixe. Angenommen, Sie möchten z. B. ein XSLT-Stylesheet oder ein XAML-Dokument bearbeiten, das eingebettete XPath-Ausdrücke enthält, die auf bestimmte Namespacepräfixe verweisen. In diesem Fall ist es wichtig, dass das Dokument mit diesen konkreten Präfixen serialisiert wird.  
  
 Dies ist der häufigste Grund für die Steuerung von Namespacepräfixen.  
  
 Ein weiterer Grund für die Notwendigkeit, Namespacepräfixe zu steuern, liegt darin, dass die Benutzer das XML-Dokument manuell bearbeiten können sollen und dass Sie Namespacepräfixe erstellen möchten, die für den Benutzer einfach einzugeben sind. Nehmen wir z. B. an, Sie möchten ein XSD-Dokument generieren. Den Konventionen für Schemas zufolge verwenden Sie  als Präfix für den Schemanamespace entweder `xs` oder `xsd`.  
  
 Zum Steuern von Namespacepräfixen fügen Sie Attribute ein, die Namespaces deklarieren. Wenn Sie die Namespaces mit bestimmten Präfixen deklarieren, versucht [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)], die Namespacepräfixe beim Serialisieren zu beachten.  
  
 Beim Erstellen eines Attributs, das einen Namespace mit einem Präfix deklariert, erstellen Sie ein Attribut, bei dem der Namespace des Namens des Attributs <xref:System.Xml.Linq.XNamespace.Xmlns%2A> lautet und der Name des Attributs das Namespacepräfix ist. Der Wert des Attributs ist der URI des Namespace.  
  
## <a name="example"></a>Beispiel  
 Dieses Beispiel deklariert zwei Namespaces. Es gibt für den `http://www.adventure-works.com`-Namespace das Präfix `aw` und für den `www.fourthcoffee.com`-Namespace das Präfix `fc` an.  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XNamespace fc = "www.fourthcoffee.com";  
XElement root = new XElement(aw + "Root",  
    new XAttribute(XNamespace.Xmlns + "aw", "http://www.adventure-works.com"),  
    new XAttribute(XNamespace.Xmlns + "fc", "www.fourthcoffee.com"),  
    new XElement(fc + "Child",  
        new XElement(aw + "DifferentChild", "other content")  
    ),  
    new XElement(aw + "Child2", "c2 content"),  
    new XElement(fc + "Child3", "c3 content")  
);  
Console.WriteLine(root);  
```  
  
 Dieses Beispiel erzeugt die folgende Ausgabe:  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com" xmlns:fc="www.fourthcoffee.com">  
  <fc:Child>  
    <aw:DifferentChild>other content</aw:DifferentChild>  
  </fc:Child>  
  <aw:Child2>c2 content</aw:Child2>  
  <fc:Child3>c3 content</fc:Child3>  
</aw:Root>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Working with XML Namespaces (C#) (Arbeiten mit XML-Namespaces (C#))](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md)
