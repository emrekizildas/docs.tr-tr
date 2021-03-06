---
title: İsteğe bağlı parametre türleri olarak kullanılan genel parametreler üzerinde sınıf kısıtlaması olmalıdır
ms.date: 07/20/2015
f1_keywords:
- vbc32124
- bc32124
helpviewer_keywords:
- BC32124
ms.assetid: 55aa8b2a-9ce3-4620-a710-2f9b0feb6143
ms.openlocfilehash: 11cf4f8d9457ebff385a601786dc97334f274324
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662069"
---
# <a name="generic-parameters-used-as-optional-parameter-types-must-be-class-constrained"></a>İsteğe bağlı parametre türleri olarak kullanılan genel parametreler üzerinde sınıf kısıtlaması olmalıdır
Bir yordam kullanan bir başvuru türü olması zorunlu değildir bir tür parametresi isteğe bağlı bir parametre ile bildirilir.  
  
 Her zaman isteğe bağlı her parametre için varsayılan bir değer sağlamanız gerekir. Parametre bir başvuru türü ise isteğe bağlı bir değer olmalıdır `Nothing`, herhangi bir başvuru türü için geçerli bir değer olduğu. Ancak, parametre bir değer türü ise, bu tür Visual Basic tarafından önceden tanımlanmış bir başlangıç veri türü olmalıdır. Kullanıcı tanımlı bir yapısı gibi bir bileşik değer türü, geçerli varsayılan değere sahip olmasıdır.  
  
 İsteğe bağlı bir parametre için bir tür parametresini kullandığınızda, geçerli varsayılan değer içermeyen bir değer türü olasılığını önlemek için başvuru türünde olduğunu garanti etmeniz gerekir. Yani, gerekir sınırlamak tür parametresi ile `Class` anahtar sözcüğü veya belirli bir sınıfın adı.  
  
 **Hata Kimliği:** BC32124  
  
## <a name="to-correct-this-error"></a>Bu hatayı düzeltmek için  
  
- Tür parametresi yalnızca bir başvuru türü kabul edecek şekilde sınırlamak veya isteğe bağlı parametresi için kullanmayın.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Visual Basic'de genel türler](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [Tür Listesi](../../../visual-basic/language-reference/statements/type-list.md)
- [Class Deyimi](../../../visual-basic/language-reference/statements/class-statement.md)
- [İsteğe Bağlı Parametreler](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)
- [Yapılar](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [Nothing](../../../visual-basic/language-reference/nothing.md)
