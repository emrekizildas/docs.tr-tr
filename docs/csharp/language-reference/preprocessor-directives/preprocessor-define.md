---
title: '#C# başvuru tanımla'
ms.custom: seodec18
ms.date: 06/30/2018
f1_keywords:
- '#define'
helpviewer_keywords:
- '#define directive [C#]'
ms.assetid: 23638b8f-779c-450e-b600-d55682de7d01
ms.openlocfilehash: d207c96621564acd8070c9d5f618f43a6d8f15a4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924597"
---
# <a name="define-c-reference"></a>#define (C# Başvurusu)
Bir sembol `#define` tanımlamak için kullanırsınız. [#İf](./preprocessor-if.md) yönergesine geçirilen ifade olarak sembolünü kullandığınızda, aşağıdaki örnekte gösterildiği gibi ifade olarak değerlendirilir `true`.  
 
 ```csharp
 #define DEBUG
 ```
  
## <a name="remarks"></a>Açıklamalar  
  
> [!NOTE]
> Yönerge `#define` , genellikle C ve C++' de yapıldığı gibi sabit değerleri bildirmek için kullanılamaz. İçindeki C# sabitler, bir sınıfın veya yapının statik üyeleri olarak en iyi şekilde tanımlanır. Bu tür sabitlere sahipseniz, bunları tutmak için ayrı bir "sabitler" sınıfı oluşturmayı düşünün.  
  
 Simgeler, derleme koşullarını belirtmek için kullanılabilir. Sembol için [#if](./preprocessor-if.md) ya da [#elif](./preprocessor-elif.md)ile test edebilirsiniz. Koşullu derleme gerçekleştirmek <xref:System.Diagnostics.ConditionalAttribute> için öğesini de kullanabilirsiniz.  
  
 Bir sembol tanımlayabilirsiniz, ancak bir simgeye değer atayamazsınız. Ayrıca Önişlemci yönergeleri olmayan herhangi bir yönergeyi kullanmadan önce yönergedosyadagörünmelidir.`#define`  
  
 Ayrıca, [-define](../compiler-options/define-compiler-option.md) derleyici seçeneğiyle bir simge tanımlayabilirsiniz. [#Undef](./preprocessor-undef.md)bir simge tanımlayabilirsiniz.  
  
 `-define` Veya ile`#define` tanımladığınız bir sembol aynı ada sahip bir değişkenle çakışmaz. Diğer bir deyişle, bir değişken adı bir Önişlemci yönergesine geçirilmemelidir ve bir sembol yalnızca bir Önişlemci yönergesi tarafından değerlendirilebilmelidir.  
  
 Kullanılarak `#define` oluşturulan bir simgenin kapsamı, sembolün tanımlandığı dosyadır.  
  
 Aşağıdaki örnekte gösterildiği gibi yönergeleri dosyanın en üstüne koymanız `#define` gerekir.  
  
```csharp  
#define DEBUG  
//#define TRACE  
#undef TRACE  
  
using System;  
  
public class TestDefine  
{  
    static void Main()  
    {  
#if (DEBUG)  
        Console.WriteLine("Debugging is enabled.");  
#endif  
  
#if (TRACE)  
     Console.WriteLine("Tracing is enabled.");  
#endif  
    }  
}  
// Output:  
// Debugging is enabled.  
```  
  
 Bir simgenin nasıl tanımlanacağını gösteren bir örnek için bkz. [#undef](./preprocessor-undef.md).  
  
## <a name="see-also"></a>Ayrıca bkz.

- [C#Başvurunun](../index.md)
- [C# Programlama Kılavuzu](../../programming-guide/index.md)
- [C# Ön İşlemci Yönergeleri](./index.md)
- [const](../keywords/const.md)
- [Nasıl yapılır: Izleme ve hata ayıklama ile koşullu derleme](../../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)
- [#undef](./preprocessor-undef.md)
- [#if](./preprocessor-if.md)
