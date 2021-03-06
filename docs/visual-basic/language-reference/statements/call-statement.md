---
title: Call Deyimi (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Call
helpviewer_keywords:
- procedures [Visual Basic], Call statement
- Call statement [Visual Basic]
- procedures [Visual Basic], calling
ms.assetid: e5b31571-6867-406f-b8e7-a3f9aae4723a
ms.openlocfilehash: a04ebddc7db176188876da1082e1e6946e1e8eec
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005172"
---
# <a name="call-statement-visual-basic"></a>Call Deyimi (Visual Basic)

Denetimi bir `Function`, `Sub` veya dinamik bağlantı kitaplığı (DLL) yordamına aktarır.  
  
## <a name="syntax"></a>Sözdizimi  
  
```vb  
[ Call ] procedureName [ (argumentList) ]  
```  
  
## <a name="parts"></a>Bölümler  

|||
|---|---|
|`procedureName`|Gerekli. Çağrılacak yordamın adı.|
|`argumentList`|İsteğe bağlı. Çağrıldığında yordama geçirilen bağımsız değişkenleri temsil eden değişkenlerin veya ifadelerin listesi. Birden çok bağımsız değişken virgülle ayrılır. @No__t-0 eklerseniz, parantez içine almanız gerekir.|
|||
  
## <a name="remarks"></a>Açıklamalar

 Bir yordamı çağırdığınızda `Call` anahtar sözcüğünü kullanabilirsiniz. Çoğu yordam çağrısı için bu anahtar sözcüğünü kullanmanız gerekmez.

 Çağrılan ifade bir tanımlayıcı ile başlamadığınızda genellikle `Call` anahtar sözcüğünü kullanırsınız. Diğer kullanımlar için `Call` anahtar sözcüğünün kullanılması önerilmez.

 Yordam bir değer döndürürse `Call` deyimleri onu atar.

## <a name="example"></a>Örnek

 Aşağıdaki kodda, bir yordamı çağırmak için `Call` anahtar sözcüğünün gerekli olduğu iki örnek gösterilmektedir. Her iki örnekte de çağrılan ifade bir tanımlayıcı ile başlamaz.

 [!code-vb[VbVbalrStatements#97](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#97)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Function Deyimi](function-statement.md)
- [Sub Deyimi](sub-statement.md)
- [Declare Deyimi](declare-statement.md)
- [Lambda İfadeleri](../../programming-guide/language-features/procedures/lambda-expressions.md)
