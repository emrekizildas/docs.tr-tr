---
title: XslTransform Sınıfı XSLT İşlemcisini Uygular
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 88373fe2-4a6b-44f9-8a62-8a3e348e3a46
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8cc3eb3e3f147d8ed15587946af743c96739a9b1
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956859"
---
# <a name="xsltransform-class-implements-the-xslt-processor"></a>XslTransform Sınıfı XSLT İşlemcisini Uygular

> [!NOTE]
> @No__t-0 sınıfı, .NET Framework 2,0 ' de kullanılmıyor. @No__t-0 sınıfını kullanarak dönüşümler için Genişletilebilir Stil sayfası dili (XSLT) dönüşümleri gerçekleştirebilirsiniz. Daha fazla bilgi için, bkz. [XslCompiledTransform sınıfını kullanma](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) ve [XslTransform sınıfından geçiş](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md) .

@No__t-0 sınıfı, XSL dönüştürmeleri (XSLT) sürüm 1,0 önerisi uygulayan bir XSLT işlemcisidir. @No__t-0 yöntemi, stil sayfalarını bulur ve okur ve <xref:System.Xml.Xsl.XslTransform.Transform%2A> yöntemi verilen kaynak belgeyi dönüştürür. @No__t-0 arabirimini uygulayan tüm depolar, <xref:System.Xml.Xsl.XslTransform> için kaynak belge olarak kullanılabilir. .NET Framework şu anda <xref:System.Xml.XmlDocument>, <xref:System.Xml.XmlDataDocument> ve <xref:System.Xml.XPath.XPathDocument> <xref:System.Xml.XPath.IXPathNavigable> arabirimini uyguladığı için, bunların hepsi bir dönüşüme giriş kaynak belgesi olarak kullanılabilir.

.NET Framework <xref:System.Xml.Xsl.XslTransform> nesnesi yalnızca aşağıdaki ad alanıyla tanımlanan XSLT 1,0 belirtimini destekler:

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
```

Stil sayfası, aşağıdaki sınıflardan biri olan <xref:System.Xml.Xsl.XslTransform.Load%2A> yöntemi kullanılarak yüklenebilir:

- XPathNavigator

- Değerine

- URL 'YI temsil eden bir dize

Yukarıdaki giriş sınıflarının her biri için farklı bir <xref:System.Xml.Xsl.XslTransform.Load%2A> yöntemi vardır. Bazı yöntemler, bu sınıflardan birinin bir birleşimini ve <xref:System.Xml.XmlResolver> sınıfını bağımsız değişken olarak alır. @No__t-0, stil sayfasında `<xsl:import>` veya `<xsl:include>` tarafından başvurulan kaynakları bulur. Aşağıdaki yöntemler girdi olarak bir dize, <xref:System.Xml.XmlReader> veya <xref:System.Xml.XPath.XPathNavigator> alır.

```vb
Overloads Public Sub Load(String)
```

```csharp
public void Load(string);
```

```vb
Overloads Public Sub Load(String, XmlResolver)
```

```csharp
public void Load(string, XmlResolver);
```

```vb
Overloads Public Sub Load(XmlReader, XmlResolver, Evidence)
```

```csharp
public void Load(XmlReader, XmlResolver, Evidence);
```

```vb
Overloads Public Sub Load(XPathNavigator, XmlResolver, Evidence)
```

```csharp
public void Load(XPathNavigator, XmlResolver, Evidence);
```

Yukarıda gösterilen <xref:System.Xml.Xsl.XslTransform.Load%2A> yöntemlerinin çoğu parametre olarak bir <xref:System.Xml.XmlResolver> alır. @No__t-0, stil sayfasını ve xsl: import ve xsl: include öğelerinde başvurulan herhangi bir stil sayfasını yüklemek için kullanılır.

@No__t-0 yöntemlerinin çoğu ayrıca bir parametre olarak kanıt alır. Kanıt parametresi, stil sayfasıyla ilişkili <xref:System.Security.Policy.Evidence> ' dır. Stil sayfasının güvenlik düzeyi, başvurduğu komut dosyası, kullandığı @no__t 0 işlevleri ve <xref:System.Xml.Xsl.XsltArgumentList> tarafından kullanılan tüm uzantı nesneleri gibi referans yaptığı sonraki kaynakların güvenlik düzeyini etkiler.

Stil sayfası, URL parametresi içeren bir <xref:System.Xml.Xsl.XslTransform.Load%2A> yöntemi kullanılarak yüklenirse ve kanıt sağlanmazsa, stil sayfasının kanıtı, verilen URL 'nin sitesi ve bölgesi ile birleştirilerek hesaplanır.

URI veya kanıt sağlanmazsa, stil sayfası için kanıt kümesi tam olarak güvenilirdir. Güvenilmeyen kaynaklardan stil sayfaları yüklemeyin veya @no__t güvenilmeyen uzantı nesneleri ekleyin-0.

Güvenlik düzeyleri ve kanıt ve komut dosyalarını nasıl etkilediği hakkında daha fazla bilgi için, bkz. [\<msxsl: script > kullanarak XSLT stil sayfası betiği](../../../../docs/standard/data/xml/xslt-stylesheet-scripting-using-msxsl-script.md). Güvenlik düzeyleri ve kanıt ve uzantı nesnelerini nasıl etkilediği hakkında bilgi için bkz. [stil sayfası parametreleri ve uzantı nesneleri Için XsltArgumentList](../../../../docs/standard/data/xml/xsltargumentlist-for-style-sheet-parameters-and-extension-objects.md).

Güvenlik düzeyleri ve kanıtları ve `document()` işlevini nasıl etkilediği hakkında bilgi için bkz. [dış XSLT stil sayfalarını ve belgelerini çözümleme](../../../../docs/standard/data/xml/resolving-external-xslt-style-sheets-and-documents.md).

Bir stil sayfası, bir dizi giriş parametresiyle sağlanabilir. Stil sayfası, uzantı nesnelerindeki işlevleri de çağırabilir. Hem parametre hem de uzantı nesneleri <xref:System.Xml.Xsl.XsltArgumentList> sınıfı kullanılarak stil sayfasına sağlanır. @No__t-0 hakkında daha fazla bilgi için bkz. <xref:System.Xml.Xsl.XsltArgumentList>.

## <a name="recommended-secure-use-of-xsltransform-class"></a>XslTransform sınıfının önerilen güvenli kullanımı

Stil sayfasının güvenlik ayrıcalıkları, belirtilen kanıta bağımlıdır. Aşağıdaki tabloda stil sayfasının konumu özetlenmektedir ve ne tür bir kanıt verilecek olduğuna ilişkin bir açıklama verilir.

- XSLT stil sayfasının dış başvuruları yoktur veya stil sayfası güvendiğiniz bir kod tabanından gelir.

  - Derlemeinizden kanıt sağlayın:

    ```vb
    Dim xslt = New XslTransform() xslt.Load(stylesheet, resolver, Me.GetType().Assembly.Evidence)

    XsltTransform xslt = new XslTransform();  xslt.Load(stylesheet, resolver, this.GetType().Assembly.Evidence);
    ```

- XSLT stil sayfası bir dış kaynaktan gelir. Kaynağın kaynağı bilinirdi ve doğrulanabilir bir URI vardır.

  - URI kullanarak kanıt oluşturun.

    ```vb
    Dim xslt As New XslTransform() Dim ev As Evidence = XmlSecureResolver.CreateEvidenceForUrl(stylesheetUri) xslt.Load(stylesheet, resolver, evidence)

    XslTransform xslt = new XslTransform(); Evidence ev = XmlSecureResolver.CreateEvidenceForUrl(stylesheetUri); xslt.Load(stylesheet, resolver, evidence);
    ```

- XSLT stil sayfası bir dış kaynaktan gelir. Kaynağın kaynağı bilinmiyor.

  - Kanıtları `null` olarak ayarlayın. Betik blokları işlenmiyor, XSLT `document()` işlevi desteklenmiyor ve ayrıcalıklı uzantı nesnelerine izin verilmiyor.

    Ayrıca, `resolver` parametresini `null` olarak ayarlayabilirsiniz; bu, `xsl:import` ve `xsl:include` öğelerinin işlenmemesini sağlar.

- XSLT stil sayfası bir dış kaynaktan gelir. Kaynağın kaynağı bilinmiyor, ancak betik desteğine ihtiyacınız vardır.

  - Çağırandan kanıt iste.

## <a name="transformation-of-xml-data"></a>XML verilerinin dönüştürülmesi

Bir stil sayfası yüklendikten sonra, dönüştürme <xref:System.Xml.Xsl.XslTransform.Transform%2A> yöntemlerinden birini çağırarak ve bir giriş kaynak belgesi sağlayarak başlar. @No__t-0 yöntemi, farklı dönüştürme çıktıları sağlamak için aşırı yüklendi. Dönüştürme, aşağıdaki çıkış biçimlerine neden olabilir:

- <xref:System.Xml.XmlReader>

- <xref:System.Xml.XmlWriter>

- <xref:System.IO.TextWriter>

- <xref:System.IO.Stream>

- Dosyanın dize URL 'SI

Bu son biçim olan dize URL 'si, URL 'de bulunan bir giriş belgesini dönüştürme ve belgeyi çıkış URL 'sine yazma konusunda yaygın olarak kullanılan bir senaryo sağlar. Bu <xref:System.Xml.Xsl.XslTransform.Transform%2A> yöntemi bir dosyadan XML belgesi yüklemek, XSLT dönüşümünü gerçekleştirmek ve çıktıyı bir dosyaya yazmak için kullanışlı bir yöntemdir. Bu, giriş kaynak belgesi oluşturup yüklemeyi ve ardından bir dosya akışına yazmanızı önler. Aşağıdaki kod örneğinde, giriş ve çıkış olarak dize URL 'sini kullanarak <xref:System.Xml.Xsl.XslTransform.Transform%2A> yönteminin bu kullanımı gösterilmektedir:

```vb
Dim xsltransform As XslTransform = New XslTransform()
xsltransform.Load("favorite.xsl")
xsltransform.Transform("MyDocument.Xml", "TransformResult.xml", Nothing)
```

```csharp
XslTransform xsltransform = new XslTransform();
xsltransform.Load("favorite.xsl");
xsltransform.Transform("MyDocument.xml", "TransformResult.xml", null);
```

## <a name="transforming-a-section-of-an-xml-document"></a>XML belgesinin bir bölümünü dönüştürme

Dönüşümler belgeye bir bütün olarak uygulanır. Diğer bir deyişle, belge kök düğümü dışında bir düğüm geçirirseniz, bu, dönüşüm işleminin yüklenen belgedeki tüm düğümlere erişmesini engellemez. Bir sonuç ağacı parçasını dönüştürmek için, yalnızca sonuç ağacı parçasını içeren bir <xref:System.Xml.XmlDocument> oluşturmanız ve bu <xref:System.Xml.XmlDocument> ' i <xref:System.Xml.Xsl.XslTransform.Transform%2A> yöntemine iletmeniz gerekir. Aşağıdaki örnek, bir sonuç ağacı parçasında bir dönüştürme gerçekleştirir.

```vb
Dim xslt As New XslTransform()
xslt.Load("print_root.xsl")
Dim doc As New XmlDocument()
doc.Load("library.xml")
' Create a new document containing just the result tree fragment.
Dim testNode As XmlNode = doc.DocumentElement.FirstChild
Dim tmpDoc As New XmlDocument()
tmpDoc.LoadXml(testNode.OuterXml)
' Pass the document containing the result tree fragment
' to the Transform method.
Console.WriteLine(("Passing " + tmpDoc.OuterXml + " to print_root.xsl"))
xslt.Transform(tmpDoc, Nothing, Console.Out, Nothing)
```

```csharp
XslTransform xslt = new XslTransform();
xslt.Load("print_root.xsl");
XmlDocument doc = new XmlDocument();
doc.Load("library.xml");
// Create a new document containing just the result tree fragment.
XmlNode testNode = doc.DocumentElement.FirstChild;
XmlDocument tmpDoc = new XmlDocument();
tmpDoc.LoadXml(testNode.OuterXml);
// Pass the document containing the result tree fragment
// to the Transform method.
Console.WriteLine("Passing " + tmpDoc.OuterXml + " to print_root.xsl");
xslt.Transform(tmpDoc, null, Console.Out, null);
```

Örnek, input olarak Library. xml ve print_root. xsl dosyalarını kullanır ve aşağıdakileri konsola verir:

```console
Passing <book genre="novel" ISBN="1-861001-57-5"><title>Pride And Prejudice</title></book> to print_root.xsl
Root node is book.
```

Library. xml

```xml
<library>
  <book genre='novel' ISBN='1-861001-57-5'>
     <title>Pride And Prejudice</title>
  </book>
  <book genre='novel' ISBN='1-81920-21-2'>
     <title>Hook</title>
  </book>
</library>
```

print_root. Xsl

```xml
<stylesheet version="1.0" xmlns="http://www.w3.org/1999/XSL/Transform" >
  <output method="text" />
  <template match="/">
     Root node is  <value-of select="local-name(//*[position() = 1])" />
  </template>
</stylesheet>
```

## <a name="migration-of-xslt-from-net-framework-version-10-to-net-framework-version-11"></a>XSLT 'nin .NET Framework sürüm 1,0 ' den .NET Framework sürümüne geçişi 1,1

Aşağıdaki tabloda, <xref:System.Xml.Xsl.XslTransform.Load%2A> yöntemi için eski .NET Framework sürüm 1,0 yöntemleri ve yeni .NET Framework sürüm 1,1 yöntemleri gösterilmektedir. Yeni yöntemler, kanıt belirterek stil sayfasının izinlerini sınırlamanıza olanak tanır.

|Eski .NET Framework sürüm 1,0 yükleme yöntemleri|Değiştirme .NET Framework sürüm 1,1 yükleme yöntemleri|
|------------------------------------------------------|---------------------------------------------------------|
|Load (XPathNavigator girişi);<br /><br /> Load (XPathNavigator girişi, XmlResolver Çözümleyicisi);|Load (XPathNavigator stil sayfası, XmlResolver Çözümleyicisi, kanıt kanıtı);|
|Load (ıxpathgezinebilir stil sayfası);<br /><br /> Load (ıxpathgezinilebilir stil sayfası, XmlResolver Çözümleyicisi);|Load (ıxpathgezinilebilir stil sayfası, XmlResolver Çözümleyicisi, kanıt kanıtı);|
|Load (XmlReader stil sayfası);<br /><br /> Load (XmlReader stil sayfası, XmlResolver Çözümleyicisi);|Load (XmlReader stil sayfası, XmlResolver Çözümleyicisi, kanıt kanıtı);|

Aşağıdaki tabloda <xref:System.Xml.Xsl.XslTransform.Transform%2A> yöntemi için eski ve yeni yöntemler gösterilmektedir. Yeni yöntemler <xref:System.Xml.XmlResolver> nesnesi alır.

|Kullanımdan kalktı .NET Framework sürüm 1,0 dönüştürme yöntemleri|Değiştirme .NET Framework sürüm dönüştürme 1,1 yöntemleri|
|-----------------------------------------------------------|--------------------------------------------------------------|
|XmlReader dönüşümü (XPathNavigator girişi, XsltArgumentList bağımsız değişkenleri)|XmlReader Transform (XPathNavigator girişi, XsltArgumentList args, XmlResolver Çözümleyicisi)|
|XmlReader Transform (ıxpathgezinebilir girişi, XsltArgumentList args)|XmlReader Transform (ıxpathgezinebilir Input, XsltArgumentList args, XmlResolver Çözümleyicisi)|
|Void Transform (XPathNavigator girişi, XsltArgumentList args, XmlWriter çıktısı)|Void Transform (XPathNavigator girişi, XsltArgumentList args, XmlWriter çıktısı, XmlResolver Çözümleyicisi)|
|Void Transform (ıxpathgezinebilir Input, XsltArgumentList args, XmlWriter output)|Void Transform (ıxpathgezinebilir Input, XsltArgumentList args, XmlWriter Output, XmlResolver Çözümleyicisi)|
|Void Transform (XPathNavigator girişi, XsltArgumentList args, TextWriter çıkışı)|Void Transform (XPathNavigator girişi, XsltArgumentList args, TextWriter çıktısı, XmlResolver Çözümleyicisi)|
|Void Transform (ıxpathgezinebilir Input, XsltArgumentList args, TextWriter output)|Void Transform (ıxpathgezinebilir Input, XsltArgumentList args, TextWriter Output, XmlResolver Çözümleyicisi)|
|Void Transform (XPathNavigator girişi, XsltArgumentList args, akış çıkışı)|Void Transform (XPathNavigator girişi, XsltArgumentList args, Stream çıktısı, XmlResolver Çözümleyicisi)|
|Void Transform (ıxpathgezinebilir Input, XsltArgumentList args, stream output)|Void Transform (ıxpathgezinebilir Input, XsltArgumentList args, Stream Output, XmlResolver Çözümleyicisi)|
|Void Transform (dize girişi, dize çıktısı);|Void Transform (dize girişi, dize çıkışı, XmlResolver Çözümleyicisi);|

@No__t-0 özelliği .NET Framework sürüm 1,1 ' de kullanılmıyor. Bunun yerine, bir <xref:System.Xml.XmlResolver> nesnesi alacak yeni <xref:System.Xml.Xsl.XslTransform.Transform%2A> aşırı yüklemelerini kullanın.

## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Xml.Xsl.XslTransform>
- [XslTransform Sınıfı ile XSLT Dönüşümleri](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)
- [Dönüşümlerde XPathNavigator](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)
- [Dönüşümlerde XPathNodeIterator](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)
- [XslTransform’a XPathDocument Girişi](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)
- [XslTransform’a XmlDataDocument Girişi](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)
- [XslTransform’a XmlDocument Girişi](../../../../docs/standard/data/xml/xmldocument-input-to-xsltransform.md)
