---
title: .NET Performans İpuçları
ms.date: 03/30/2017
helpviewer_keywords:
- C# language, performance
- performance [C#]
- Visual Basic, performance
- performance [Visual Basic]
ms.assetid: ae275793-857d-4102-9095-b4c2a02d57f4
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 14ed06bbd09d7551707628060b460584816e4711
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046290"
---
# <a name="net-performance-tips"></a>.NET Performans İpuçları
*Performans* terimi genellikle programın yürütme hızına başvurur. Kaynak kodunuzda belirli temel kuralları izleyerek, bazen yürütme hızını artırabilirsiniz. Bazı programlarda, kodu yakından incelemek ve profil oluşturucular kullanarak olabildiğince hızlı çalıştığından emin olmak önemlidir. Diğer programlarda, bu tür iyileştirme gerçekleştirmek zorunda değilsiniz çünkü kod yazıldığı kadar hızlı şekilde çalışıyor. Bu makalede, performansın önyüklenebileceği bazı yaygın bölgeler ve ek performans konularına yönelik bağlantılar yer almaktadır. Performansı planlama ve ölçme hakkında daha fazla bilgi için bkz. [performans](index.md)  
  
## <a name="boxing-and-unboxing"></a>Kutulama ve Kutudan Çıkarma  
 Değer türlerinin, örneğin gibi <xref:System.Collections.ArrayList?displayProperty=nameWithType>genel olmayan koleksiyonlar sınıflarında çok sayıda kez paketlenmeleri gerektiği durumlarda kullanmaktan kaçınmak en iyisidir. Gibi genel Koleksiyonlar <xref:System.Collections.Generic.List%601?displayProperty=nameWithType>kullanarak değer türlerinin kutulamaktan kaçınabilirsiniz. Kutulama ve kutudan çıkarma, hesaplama açısından pahalı işlemlerdir. Bir değer türü paketlenme olduğunda, tamamen yeni bir nesne oluşturulması gerekir. Bu, basit bir başvuru atamasından 20 kat daha uzun sürebilir. Kutudan çıkarma sırasında, atama işlemi atamanın dört katı zaman alabilir. Daha fazla bilgi için bkz. [kutulama ve kutudan](../../csharp/programming-guide/types/boxing-and-unboxing.md)çıkarma.  
  
## <a name="strings"></a>Dizeler  
 Çok sayıda dize değişkenini birleştirme, örneğin sıkı bir döngüde, [+ işleci](../../csharp/language-reference/operators/addition-operator.md) veya Visual Basic [birleştirme işleçleri](../../visual-basic/language-reference/operators/concatenation-operators.md)yerine <xref:System.Text.StringBuilder?displayProperty=nameWithType> C# kullanın. Daha fazla bilgi için [nasıl yapılır: Visual Basic birden çok](../../csharp/how-to/concatenate-multiple-strings.md) dizeyi ve [birleştirme işleçlerini](../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)birleştirme.  
  
## <a name="destructors"></a>Yıkıcılar  
 Boş Yıkıcılar kullanılmamalıdır. Bir sınıf bir yıkıcı içerdiğinde, sonlandırma kuyruğunda bir giriş oluşturulur. Yıkıcı çağrıldığında, atık toplayıcı kuyruğu işlemek için çağrılır. Yok edicisi boşsa, bu yalnızca performans kaybı ile sonuçlanır. Daha fazla bilgi için bkz. [Yıkıcılar](../../csharp/programming-guide/classes-and-structs/destructors.md) ve [nesne ömrü: Nesneler nasıl oluşturulur ve yok edilir](../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md).  
  
## <a name="other-resources"></a>Diğer Kaynaklar  
  
- [Daha hızlı yönetilen kod yazma: Işlerin maliyetini öğrenin](https://go.microsoft.com/fwlink/?LinkId=99294)  
  
- [Yüksek performanslı yönetilen uygulamalar yazma: Bir öncü](https://go.microsoft.com/fwlink/?LinkId=99295)  
  
- [Çöp toplayıcı temelleri ve performans Ipuçları](https://go.microsoft.com/fwlink/?LinkId=99296)  
  
- [.NET uygulamalarındaki performans Ipuçları ve püf noktaları](https://go.microsoft.com/fwlink/?LinkId=99297)  

- [Riko Mariani performansı tidbits](https://go.microsoft.com/fwlink/?LinkId=115679)  

- [Vance Morrison blogu](https://blogs.msdn.microsoft.com/vancem/)
  
## <a name="see-also"></a>Ayrıca bkz.

- [Performans](index.md)
- [Visual Basic programlama kılavuzu](../../visual-basic/programming-guide/index.md)
- [C# Programlama Kılavuzu](../../csharp/programming-guide/index.md)
