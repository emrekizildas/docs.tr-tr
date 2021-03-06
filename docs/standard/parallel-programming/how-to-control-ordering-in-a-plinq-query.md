---
title: 'Nasıl yapılır: PLINQ Sorgusunda Sıralama Denetimi'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to control ordering
ms.assetid: c67eccc7-004d-4b2f-987e-919cbbd62ef7
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7416f2f9c200d687d3f2c1f14b01cafdb48f85b1
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988190"
---
# <a name="how-to-control-ordering-in-a-plinq-query"></a>Nasıl yapılır: PLINQ Sorgusunda Sıralama Denetimi
Bu örneklerde, <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> genişletme yöntemi kullanılarak bir PLINQ sorgusunda sıralamayı denetleme gösterilmektedir.  
  
> [!WARNING]
> Bu örnekler öncelikle kullanımı göstermeye yöneliktir ve eşdeğer sıralı LINQ to Objects sorgularından daha hızlı çalışmayabilir.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki örnek, kaynak sırasının sıralamasını korur. Bu bazen gereklidir; Örneğin, bazı sorgu işleçleri doğru sonuçlar üretmek için sıralı bir kaynak sırası gerektirir.  
  
 [!code-csharp[PLINQ#12](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#12)]
 [!code-vb[PLINQ#12](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#12)]  
  
## <a name="example"></a>Örnek  
 Aşağıdaki örnek, kaynak sırası büyük olasılıkla sıralanmalıdır beklenen bazı sorgu işleçlerini gösterir. Bu işleçler sıralanmamış diziler üzerinde çalışır, ancak bunlar beklenmedik sonuçlara neden olabilirler.  
  
 [!code-csharp[PLINQ#14](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#14)]
 [!code-vb[PLINQ#14](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#14)]  
  
 Bu yöntemi çalıştırmak için, [PLINQ veri örneği](../../../docs/standard/parallel-programming/plinq-data-sample.md) projesindeki PLINQDataSample sınıfına yapıştırın ve F5 tuşuna basın.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki örnek, bir sorgunun ilk bölümü için sıralamayı nasıl koruyabileceğiniz gösterir, sonra bir JOIN yan tümcesinin performansını artırmak için sıralamayı kaldırır ve sonra sıralamayı son sonuç dizisine yeniden uygular.  
  
 [!code-csharp[PLINQ#15](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#15)]
 [!code-vb[PLINQ#15](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#15)]  
  
 Bu yöntemi çalıştırmak için, [PLINQ veri örneği](../../../docs/standard/parallel-programming/plinq-data-sample.md) projesindeki PLINQDataSample sınıfına yapıştırın ve F5 tuşuna basın.  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Linq.ParallelEnumerable>
- [Paralel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)
