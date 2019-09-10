---
title: LINQ to Entities Hakkında Bilinen Sorunlar ve Dikkat Edilmesi Gerekenler
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: acd71129-5ff0-4b4e-b266-c72cc0c53601
ms.openlocfilehash: 4fb7d574fdb9bd6bd9465cffaf0fda5069b2c0ee
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854377"
---
# <a name="known-issues-and-considerations-in-linq-to-entities"></a>LINQ to Entities Hakkında Bilinen Sorunlar ve Dikkat Edilmesi Gerekenler
Bu bölüm LINQ to Entities sorgularıyla ilgili bilinen sorunlar hakkında bilgi sağlar.  
  
- [Önbelleğe alınabilecek LINQ sorguları](#LINQQueriesThatAreNotCached)  
  
- [Sipariş bilgileri kayıp](#OrderingInfoLost)  
  
- [İşaretsiz tamsayılar desteklenmiyor](#UnsignedIntsUnsupported)  
  
- [Tür dönüştürme hataları](#TypeConversionErrors)  
  
- [Skalar olmayan değişkenlere başvurma desteklenmiyor](#RefNonScalarClosures)  
  
- [İç içe geçmiş sorgular SQL Server 2000 ile başarısız olabilir](#NestedQueriesSQL2000)  
  
- [Anonim bir türe yansıtma](#ProjectToAnonymousType)  
  
<a name="LINQQueriesThatAreNotCached"></a>   
## <a name="linq-queries-that-cannot-be-cached"></a>Önbelleğe alınabilecek LINQ sorguları  
 .NET Framework 4,5 ' den başlayarak LINQ to Entities sorguları otomatik olarak önbelleğe alınır. Ancak, bu işleci, `Enumerable.Contains` bellek içi koleksiyonlara uygulayan LINQ to Entities sorguları otomatik olarak önbelleğe alınmaz. Ayrıca, derlenen LINQ sorgularında bellek içi koleksiyonlara parametreleştirmeye izin verilmez.  
  
<a name="OrderingInfoLost"></a>   
## <a name="ordering-information-lost"></a>Sipariş bilgileri kayıp  
 Sütunları anonim bir türde yansıtma, bir SQL Server 2005 veritabanına karşı yürütülen bazı sorgularda sıralama bilgilerinin "80" uyumluluk düzeyine ayarlanmış olarak kaybolmasına neden olur.  Bu durum, aşağıdaki örnekte gösterildiği gibi, order by listesindeki bir sütun adı seçicideki bir sütun adıyla eşleştiğinde meydana gelir:  
  
 [!code-csharp[DP L2E Conceptual Examples#SBUDT543840](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#sbudt543840)]
 [!code-vb[DP L2E Conceptual Examples#SBUDT543840](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#sbudt543840)]  
  
<a name="UnsignedIntsUnsupported"></a>   
## <a name="unsigned-integers-not-supported"></a>İşaretsiz tamsayılar desteklenmiyor  
 Entity Framework işaretsiz tamsayılar desteklemediğinden LINQ to Entities sorgusunda işaretsiz bir tamsayı türü belirtilmesi desteklenmez. İşaretsiz bir tamsayı belirtirseniz, aşağıdaki örnekte gösterildiği <xref:System.ArgumentException> gibi sorgu ifadesi çevirisi sırasında bir özel durum atılır. Bu örnek 48000 KIMLIKLI bir sipariş için sorgular.  
  
 [!code-csharp[DP L2E Conceptual Examples#UIntAsQueryParam](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#uintasqueryparam)]
 [!code-vb[DP L2E Conceptual Examples#UIntAsQueryParam](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#uintasqueryparam)]  
  
<a name="TypeConversionErrors"></a>   
## <a name="type-conversion-errors"></a>Tür dönüştürme hataları  
 Visual Basic, bir özellik `CByte` işlevi kullanılarak 1 değeri olan SQL Server bit türünde bir sütunla eşlendiğinde, bir <xref:System.Data.SqlClient.SqlException> "aritmetik taşma hatası" iletisiyle oluşturulur. Aşağıdaki örnek, AdventureWorks örnek `Product.MakeFlag` veritabanındaki sütununu sorgular ve sorgu sonuçları üzerinden yineedildiğinde bir özel durum oluşturulur.  
  
 [!code-vb[DP L2E Conceptual Examples#SBUDT544355](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#sbudt544355)]  
  
<a name="RefNonScalarClosures"></a>   
## <a name="referencing-non-scalar-variables-not-supported"></a>Skalar olmayan değişkenlere başvurma desteklenmiyor  
 Bir sorgu içindeki bir varlık gibi skaler olmayan değişkenlere başvurma desteklenmez. Böyle bir sorgu yürütüldüğünde, <xref:System.NotSupportedException> "türün `EntityType`sabit değeri oluşturulamıyor" iletisini içeren bir özel durum oluşturulur. Bu bağlamda yalnızca ilkel türler (Int32, String ve Guid gibi) destekleniyor. "  
  
> [!NOTE]
> Skaler değişkenler koleksiyonuna başvurmak desteklenir.  
  
 [!code-csharp[DP L2E Conceptual Examples#SBUDT555877](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#sbudt555877)]
 [!code-vb[DP L2E Conceptual Examples#SBUDT555877](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#sbudt555877)]  
  
<a name="NestedQueriesSQL2000"></a>   
## <a name="nested-queries-may-fail-with-sql-server-2000"></a>İç içe geçmiş sorgular SQL Server 2000 ile başarısız olabilir  
 SQL Server 2000 ile, üç veya daha fazla düzey derinlikli iç içe Transact-SQL sorguları oluşturduklarında LINQ to Entities sorguları başarısız olabilir.  
  
<a name="ProjectToAnonymousType"></a>   
## <a name="projecting-to-an-anonymous-type"></a>Anonim bir türe yansıtma  
 Üzerinde yöntemi<xref:System.Data.Objects.ObjectQuery%601.Include%2A> kullanarak ilgili nesneleri dahil etmek için ilk sorgu yolunu tanımlayabilir veardındandöndürülennesnelerianonimbirtüreeklemekiçinLINQkullanıyorsanız,Includeyöntemindebelirtilennesnelersorguyaeklenmez<xref:System.Data.Objects.ObjectQuery%601> sonucunun.  
  
 [!code-csharp[DP L2E Conceptual Examples#ProjToAnonType1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#projtoanontype1)]
 [!code-vb[DP L2E Conceptual Examples#ProjToAnonType1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#projtoanontype1)]  
  
 İlgili nesneleri almak için, döndürülen türleri bir anonim türe proje olarak değiştirmeyin.  
  
 [!code-csharp[DP L2E Conceptual Examples#ProjToAnonType2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#projtoanontype2)]
 [!code-vb[DP L2E Conceptual Examples#ProjToAnonType2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#projtoanontype2)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [LINQ to Entities](linq-to-entities.md)
