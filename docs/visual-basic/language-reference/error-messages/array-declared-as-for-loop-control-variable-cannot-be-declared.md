---
title: For döngüsü denetim değişkeni olarak bildirilen dizi başlangıç boyutuyla bildirilemez
ms.date: 07/20/2015
f1_keywords:
- vbc32039
- bc32039
helpviewer_keywords:
- BC32039
ms.assetid: 1d8b6560-c9eb-4b71-a038-24c6f5a5ce46
ms.openlocfilehash: 9e8bb7b79b5a770c3c92e47d8e7c01c5b83d6061
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701203"
---
# <a name="array-declared-as-for-loop-control-variable-cannot-be-declared-with-an-initial-size"></a>For döngüsü denetim değişkeni olarak bildirilen dizi başlangıç boyutuyla bildirilemez
@No__t-0 döngüsü *öğesi* yineleme değişkeni olarak bir diziyi kullanır, ancak bu diziyi başlatır.  
  
 Aşağıdaki deyimler bu hatanın nasıl üretime olduğunu gösterir.  
  
```vb  
Dim arrayList As New List(Of Integer())  
For Each listElement() As Integer In arrayList  
For Each listElement(1) As Integer In arrayList  
```  
  
 İlk `For Each` deyimleri `arrayList` ' in öğelerine erişmenin doğru yoludur. İkinci `For Each` ifadesinde bu hata oluşturulur.  
  
 **Hata kimliği:** BC32039  
  
## <a name="to-correct-this-error"></a>Bu hatayı düzeltmek için  
  
- Başlatma *öğesini öğe* yineleme değişkeni bildiriminden kaldırın.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [For...Next Deyimi](../../../visual-basic/language-reference/statements/for-next-statement.md)
- [Diziler](../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [Koleksiyonlar](../../../standard/collections/index.md)
