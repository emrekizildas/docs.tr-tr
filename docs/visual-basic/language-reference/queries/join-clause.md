---
title: JOIN tümcesi (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QueryJoinIn
- vb.QueryJoin
- vb.QueryJoinOn
helpviewer_keywords:
- queries [Visual Basic], Join
- Join statement [Visual Basic]
- Join clause [Visual Basic]
ms.assetid: 6dd37936-b27c-4e00-98ad-154b23f4de64
ms.openlocfilehash: 8eab7db00515f55b086b5e1beddd149f966cb27a
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72001930"
---
# <a name="join-clause-visual-basic"></a>JOIN tümcesi (Visual Basic)
İki koleksiyonu tek bir koleksiyon halinde birleştirir. JOIN işlemi, eşleşen anahtarlara dayalıdır ve `Equals` işlecini kullanır.  
  
## <a name="syntax"></a>Sözdizimi  
  
```vb  
Join element In collection _  
  [ joinClause _ ]   
  [ groupJoinClause ... _ ]   
On key1 Equals key2 [ And key3 Equals key4 [... ]  
```  
  
## <a name="parts"></a>Parçaya  
 `element`  
 Gereklidir. Birleştirilen koleksiyonun denetim değişkeni.  
  
 `collection`  
 Gereklidir. @No__t-0 işlecinin sol tarafında tanımlanan koleksiyonla birleştirilecek koleksiyon. @No__t-0 yan tümcesi, başka bir `Join` yan tümcesinde veya `Group Join` yan tümcesinde iç içe olabilir.  
  
 `joinClause`  
 İsteğe bağlı. Sorguyu daha da daraltmak için bir veya daha fazla ek `Join` yan tümcesi.  
  
 `groupJoinClause`  
 İsteğe bağlı. Sorguyu daha da daraltmak için bir veya daha fazla ek `Group Join` yan tümcesi.  
  
 `key1` `Equals` `key2`  
 Gereklidir. Katılmakta olan koleksiyonlar için anahtarları tanımlar. Birleştirilecek koleksiyonlardan anahtarları karşılaştırmak için `Equals` işlecini kullanmanız gerekir. Birden çok anahtarı belirlemek için `And` işlecini kullanarak Birleştirme koşullarını birleştirebilirsiniz. `key1` `Join` işlecinin sol tarafındaki koleksiyonda olmalıdır. `key2`, `Join` işlecinin sağ tarafındaki koleksiyondan olmalıdır.  
  
 JOIN koşulunda kullanılan anahtarlar, koleksiyondan birden fazla öğe içeren ifadeler olabilir. Ancak, her anahtar ifadesi yalnızca ilgili koleksiyonundan öğe içerebilir.  
  
## <a name="remarks"></a>Açıklamalar  
 @No__t-0 yan tümcesi, katılmakta olan koleksiyonlardan eşleşen anahtar değerlerini temel alarak iki koleksiyonu birleştirir. Elde edilen koleksiyon, `Join` işlecinin sol tarafında tanımlanan koleksiyondaki herhangi bir değer birleşimini ve `Join` yan tümcesinde tanımlanan koleksiyonu içerebilir. Sorgu yalnızca `Equals` işleci tarafından belirtilen koşulun karşılandığı sonuçları döndürür. Bu, SQL 'de `INNER JOIN` ile eşdeğerdir.  
  
 İki veya daha fazla koleksiyonu tek bir koleksiyonda birleştirmek için bir sorguda birden çok `Join` yan tümcesini kullanabilirsiniz.  
  
 @No__t-0 yan tümcesi olmadan koleksiyonları birleştirmek için örtük bir birleştirme gerçekleştirebilirsiniz. Bunu yapmak için, `From` yan tümcesine birden çok `In` yan tümce ekleyin ve JOIN için kullanmak istediğiniz anahtarları tanımlayan bir `Where` yan tümcesi belirtin.  
  
 Koleksiyonları tek bir hiyerarşik koleksiyonda birleştirmek için `Group Join` yan tümcesini kullanabilirsiniz. Bu, SQL 'de `LEFT OUTER JOIN` gibidir.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki kod örneği, bir müşteri listesini siparişleriyle birlikte birleştirmek için örtük bir birleştirme gerçekleştirir.  
  
 [!code-vb[VbSimpleQuerySamples#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#13)]  
  
## <a name="example"></a>Örnek  
 Aşağıdaki kod örneği, `Join` yan tümcesini kullanarak iki koleksiyonu birleştirir.  
  
 [!code-vb[VbSimpleQuerySamples#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples2.vb#12)]  
  
 Bu örnek aşağıdakine benzer bir çıktı oluşturacaktır:  
  
 `winlogon (968), Windows Logon`  
  
 `explorer (2424), File Explorer`  
  
 `cmd (5136), Command Window`  
  
## <a name="example"></a>Örnek  
 Aşağıdaki kod örneği iki koleksiyon birleştirir `Join` yan tümcesini iki anahtar sütunla birlikte kullanarak.  
  
 [!code-vb[VbSimpleQuerySamples#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples3.vb#17)]  
  
 Örnek aşağıdakine benzer bir çıktı oluşturacaktır:  
  
 `winlogon (968), Windows Logon, Priority = 13`  
  
 `cmd (700), Command Window, Priority = 8`  
  
 `explorer (2424), File Explorer, Priority = 8`  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Visual Basic LINQ 'e giriş](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [Sorgular](../../../visual-basic/language-reference/queries/index.md)
- [Select yan tümcesi](../../../visual-basic/language-reference/queries/select-clause.md)
- [From yan tümcesi](../../../visual-basic/language-reference/queries/from-clause.md)
- [Group JOIN yan tümcesi](../../../visual-basic/language-reference/queries/group-join-clause.md)
- [WHERE yan tümcesi](../../../visual-basic/language-reference/queries/where-clause.md)
