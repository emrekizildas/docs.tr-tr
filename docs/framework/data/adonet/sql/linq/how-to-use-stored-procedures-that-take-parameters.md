---
title: 'Nasıl yapılır: Parametre Alan Saklı Yordamlar Kullanma'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b935fd84-cb9c-4205-8c48-658d5db2ec93
ms.openlocfilehash: c2b657f704d072b987578be5520a58d007ecac37
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353012"
---
# <a name="how-to-use-stored-procedures-that-take-parameters"></a>Nasıl yapılır: Parametre Alan Saklı Yordamlar Kullanma
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], çıkış parametrelerini başvuru parametrelerine eşler ve değer türleri için parametreyi null yapılabilir olarak bildirir.  
  
 Bir satır kümesi döndüren sorguda bir giriş parametresinin nasıl kullanılacağına ilişkin bir örnek için bkz. [Nasıl yapılır: Satır kümelerini Döndür @ no__t-0.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki örnek tek bir giriş parametresi (müşteri KIMLIĞI) alır ve bir out parametresi (bu müşterinin toplam satışları) döndürür.  
  
```  
CREATE PROCEDURE [dbo].[CustOrderTotal]   
@CustomerID nchar(5),  
@TotalSales money OUTPUT  
AS  
SELECT @TotalSales = SUM(OD.UNITPRICE*(1-OD.DISCOUNT) * OD.QUANTITY)  
FROM ORDERS O, "ORDER DETAILS" OD  
where O.CUSTOMERID = @CustomerID AND O.ORDERID = OD.ORDERID  
```  
  
 [!code-csharp[DLinqSprox#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#2)]
 [!code-vb[DLinqSprox#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#2)]  
  
## <a name="example"></a>Örnek  
 Bu saklı yordamı aşağıdaki şekilde çağırabilirsiniz:  
  
 [!code-csharp[DLinqSprox#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/Program.cs#3)]
 [!code-vb[DLinqSprox#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/Module1.vb#3)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Saklı Yordamlar](stored-procedures.md)
- [Örnek Veritabanları İndirme](downloading-sample-databases.md)
- [Nullable değer türlerini kullanma](../../../../../csharp/programming-guide/nullable-types/using-nullable-types.md)
- [Boş Değer Atanabilen Değer Türleri](../../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
