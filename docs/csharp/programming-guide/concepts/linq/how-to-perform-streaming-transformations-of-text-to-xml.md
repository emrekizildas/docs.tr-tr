---
title: "Nasıl yapılır: XML 'e (C#) metin akışı dönüşümleri gerçekleştirme"
ms.date: 07/20/2015
ms.assetid: 9b3bd941-d0ff-4f2d-ae41-7c3b81d8fae6
ms.openlocfilehash: 6dc48a7342bbeedb79e8e7f4a9270899be336f91
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70851029"
---
# <a name="how-to-perform-streaming-transformations-of-text-to-xml-c"></a>Nasıl yapılır: XML 'e (C#) metin akışı dönüşümleri gerçekleştirme

Bir metin dosyasını işlemeye yönelik bir yaklaşım, `yield return` yapıyı kullanarak metin dosyasını bir kerede bir satır akışı yapan bir genişletme yöntemi yazmaktır. Daha sonra, metin dosyasını yavaş ertelenmiş bir biçimde işleyen bir LINQ sorgusu yazabilirsiniz. Daha sonra çıktıyı akışa <xref:System.Xml.Linq.XStreamingElement> almak için öğesini kullanırsanız, kaynak metin dosyasının boyutundan bağımsız olarak en az miktarda bellek kullanan metin dosyasından XML 'e bir dönüşüm oluşturabilirsiniz.

 Akış dönüşümleriyle ilgili bazı uyarılar vardır. Bir akış dönüştürmesi en iyi şekilde, dosyanın tamamını bir kez işleyebileceğiniz ve satırları kaynak belgede gerçekleştikleri sırada işleyebileceğiniz durumlarda en iyi şekilde uygulanır. Dosyayı birden çok kez işlemek istiyorsanız veya satırları işleyebilmeniz için öncelikle sıralama yapmanız gerekiyorsa, bir akış tekniği kullanmanın avantajlarından çoğunu kaybedersiniz.

## <a name="example"></a>Örnek

 Aşağıdaki metin dosyası, kişiler. txt, bu örneğin kaynağıdır.

```text
#This is a comment
1,Tai,Yee,Writer
2,Nikolay,Grachev,Programmer
3,David,Wright,Inventor
```

 Aşağıdaki kod, metin dosyasının satırlarını ertelenmiş bir biçimde akıp bir genişletme yöntemi içerir.

```csharp
public static class StreamReaderSequence
{
    public static IEnumerable<string> Lines(this StreamReader source)
    {
        if (source == null)
            throw new ArgumentNullException(nameof(source));

        string line;
        while ((line = source.ReadLine()) != null)
        {
            yield return line;
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        var sr = new StreamReader("People.txt");
        var xmlTree = new XStreamingElement("Root",
            from line in sr.Lines()
            let items = line.Split(',')
            where !line.StartsWith("#")
            select new XElement("Person",
                       new XAttribute("ID", items[0]),
                       new XElement("First", items[1]),
                       new XElement("Last", items[2]),
                       new XElement("Occupation", items[3])
                   )
        );
        Console.WriteLine(xmlTree);
        sr.Close();
    }
}
```

 Bu örnek aşağıdaki çıktıyı üretir:

```xml
<Root>
  <Person ID="1">
    <First>Tai</First>
    <Last>Yee</Last>
    <Occupation>Writer</Occupation>
  </Person>
  <Person ID="2">
    <First>Nikolay</First>
    <Last>Grachev</Last>
    <Occupation>Programmer</Occupation>
  </Person>
  <Person ID="3">
    <First>David</First>
    <Last>Wright</Last>
    <Occupation>Inventor</Occupation>
  </Person>
</Root>
```

## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Xml.Linq.XStreamingElement>
