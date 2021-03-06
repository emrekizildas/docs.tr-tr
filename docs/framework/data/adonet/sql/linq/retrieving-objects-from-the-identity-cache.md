---
title: Kimlik Önbelleğinden Nesne Alma
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 96c13903-ccb6-4a0e-ab6a-8ca955ca314d
ms.openlocfilehash: d14b15f72bd196d8b3a61f22c614516e17d2e95b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781235"
---
# <a name="retrieving-objects-from-the-identity-cache"></a>Kimlik Önbelleğinden Nesne Alma
Bu konu, <xref:System.Data.Linq.DataContext>tarafından yönetilen kimlik önbelleğinden bir nesne döndüren LINQ to SQL sorgularının türlerini açıklar.  
  
 LINQ to SQL, nesneleri <xref:System.Data.Linq.DataContext> yönetme yöntemlerinden biri, sorgular yürütüldüğü zaman bir kimlik önbelleğindeki nesne kimliklerini günlüğe kaydetmeye göre yapılır. Bazı durumlarda LINQ to SQL veritabanında bir sorgu yürütmeden önce kimlik önbelleğinden bir nesne almaya çalışacaktır.  
  
 Genellikle, bir LINQ to SQL sorgusunun kimlik önbelleğinden bir nesne döndürmesi için, sorgunun bir nesnenin birincil anahtarını temel almalıdır ve tek bir nesne döndürmesi gerekir. Özellikle, sorgu aşağıda gösterilen genel formlardan birinde olmalıdır.  
  
> [!NOTE]
> Önceden derlenen sorgular, kimlik önbelleğinden nesne döndürmez. Önceden derlenen sorgular hakkında daha fazla bilgi için bkz <xref:System.Data.Linq.CompiledQuery> . ve [nasıl yapılır: Sorguları](how-to-store-and-reuse-queries.md)depolayın ve yeniden kullanın.  
  
 Bir sorgu, kimlik önbelleğinden bir nesne almak için aşağıdaki genel formlardan birinde olmalıdır:  
  
- <xref:System.Data.Linq.Table%601>`.Function1(` `predicate``)`  
  
- <xref:System.Data.Linq.Table%601>`.Function1(` `predicate``).Function2()`  
  
 Bu genel formlarda `Function1` `Function2`,, ve `predicate` aşağıdaki gibi tanımlanmıştır.  
  
 `Function1`aşağıdakilerden herhangi biri olabilir:  
  
- <xref:System.Linq.Queryable.Where%2A>  
  
- <xref:System.Linq.Queryable.First%2A>  
  
- <xref:System.Linq.Queryable.FirstOrDefault%2A>  
  
- <xref:System.Linq.Queryable.Single%2A>  
  
- <xref:System.Linq.Queryable.SingleOrDefault%2A>  
  
 `Function2`aşağıdakilerden herhangi biri olabilir:  
  
- <xref:System.Linq.Queryable.First%2A>  
  
- <xref:System.Linq.Queryable.FirstOrDefault%2A>  
  
- <xref:System.Linq.Queryable.Single%2A>  
  
- <xref:System.Linq.Queryable.SingleOrDefault%2A>  
  
 `predicate`nesnenin birincil anahtar özelliğinin sabit bir değere ayarlandığı bir ifade olmalıdır. Bir nesnenin birden fazla özellik tarafından tanımlanmış bir birincil anahtarı varsa, her birincil anahtar özelliği sabit bir değere ayarlanmalıdır. Aşağıda, form `predicate` örnekleri gelmelidir:  
  
- `c => c.PK == constant_value`  
  
- `c => c.PK1 == constant_value1 && c=> c.PK2 == constant_value2`  
  
## <a name="example"></a>Örnek  
 Aşağıdaki kod, kimlik önbelleğinden bir nesne alan LINQ to SQL sorgularının türlerine örnekler sağlar.  
  
 [!code-csharp[L2S_QueryCache#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/l2s_querycache/cs/program.cs#1)]
 [!code-vb[L2S_QueryCache#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/l2s_querycache/vb/module1.vb#1)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Sorgu Kavramları](query-concepts.md)
- [Nesne Kimliği](object-identity.md)
- [Arka Plan Bilgileri](background-information.md)
- [Nesne Kimliği](object-identity.md)
