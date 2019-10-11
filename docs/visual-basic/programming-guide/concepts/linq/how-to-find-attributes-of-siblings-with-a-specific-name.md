---
title: 'Nasıl yapılır: belirli bir ada sahip eşdüzey öğelerinin özniteliklerini bulma (XPath-LINQ to XML) (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 83b3ddca-830a-4b71-9756-9e4bdf907302
ms.openlocfilehash: 709c21cee37c42f7633b2b108b8846ddd8e3b4e7
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72249895"
---
# <a name="how-to-find-attributes-of-siblings-with-a-specific-name-xpath-linq-to-xml-visual-basic"></a><span data-ttu-id="d13e2-102">Nasıl yapılır: belirli bir ada sahip eşdüzey öğelerinin özniteliklerini bulma (XPath-LINQ to XML) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d13e2-102">How to: Find Attributes of Siblings with a Specific Name (XPath-LINQ to XML) (Visual Basic)</span></span>
<span data-ttu-id="d13e2-103">Bu konu, bağlam düğümünün eşdüzey öğelerinin tüm özniteliklerinin nasıl bulunacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d13e2-103">This topic shows how to find all attributes of the siblings of the context node.</span></span> <span data-ttu-id="d13e2-104">Koleksiyonda yalnızca belirli bir ada sahip öznitelikler döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d13e2-104">Only attributes with a specific name are returned in the collection.</span></span>  
  
 <span data-ttu-id="d13e2-105">XPath ifadesi:</span><span class="sxs-lookup"><span data-stu-id="d13e2-105">The XPath expression is:</span></span>  
  
 `../Book/@id`  
  
## <a name="example"></a><span data-ttu-id="d13e2-106">Örnek</span><span class="sxs-lookup"><span data-stu-id="d13e2-106">Example</span></span>  
 <span data-ttu-id="d13e2-107">Bu örnek önce bir `Book` öğesi bulur ve sonra `Book` adlı tüm eşdüzey öğeleri bulur ve sonra `id` adlı tüm öznitelikleri bulur.</span><span class="sxs-lookup"><span data-stu-id="d13e2-107">This example first finds a `Book` element, and then finds all sibling elements named `Book`, and then finds all attributes named `id`.</span></span> <span data-ttu-id="d13e2-108">Sonuç, özniteliklerin koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="d13e2-108">The result is a collection of attributes.</span></span>  
  
 <span data-ttu-id="d13e2-109">Bu örnek, şu XML belgesini kullanır: [örnek xml dosyası: kitaplar (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-books-linq-to-xml.md).</span><span class="sxs-lookup"><span data-stu-id="d13e2-109">This example uses the following XML document: [Sample XML File: Books (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-books-linq-to-xml.md).</span></span>  
  
```vb  
Dim books as XDocument = XDocument.Load("Books.xml")  
Dim book As XElement = books.Root.<Book>(0)  
  
' LINQ to XML query  
Dim list1 As IEnumerable(Of XAttribute) = _  
    From el In book.Parent.<Book> _  
    Select el.Attribute("id")  
  
' XPath expression  
Dim list2 As IEnumerable(Of XAttribute) = DirectCast(book. _  
    XPathEvaluate("../Book/@id"), IEnumerable).Cast(Of XAttribute)()  
  
If list1.Count() = list2.Count() And _  
        (list1.Intersect(list2)).Count() = list1.Count() Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
  
For Each el As XAttribute In list1  
    Console.WriteLine(el)  
Next  
```  
  
 <span data-ttu-id="d13e2-110">Bu örnek aşağıdaki çıktıyı üretir:</span><span class="sxs-lookup"><span data-stu-id="d13e2-110">This example produces the following output:</span></span>  
  
```console  
Results are identical  
id="bk101"  
id="bk102"  
```  
  
## <a name="see-also"></a><span data-ttu-id="d13e2-111">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d13e2-111">See also</span></span>

- [<span data-ttu-id="d13e2-112">XPath kullanıcıları için LINQ to XML (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d13e2-112">LINQ to XML for XPath Users (Visual Basic)</span></span>](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
