---
title: openGenericCERCall MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), CER calls
- open generic CER calls
- constrained execution regions
- openGenericCERCall MDA
- CER calls
- managed debugging assistants (MDAs), CER calls
- generics [.NET Framework], open generic CER calls
ms.assetid: da3e4ff3-2e67-4668-9720-fa776c97407e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fa6ad656a5f762bf86d277d986bb087c97d7a78f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052410"
---
# <a name="opengenericcercall-mda"></a>openGenericCERCall MDA
Yönetilen `openGenericCERCall` hata ayıklama Yardımcısı, kök yöntemde genel tür değişkenleri olan kısıtlanmış bir yürütme bölgesi (cer) grafiğinin JIT derleme veya yerel görüntü oluşturma zamanında ve en az bir genel olarak işlenmekte olduğunu uyarmak için etkinleştirilir. tür değişkenleri bir nesne başvuru türüdür.  
  
## <a name="symptoms"></a>Belirtiler  
 Bir iş parçacığı iptal edildiğinde veya bir uygulama etki alanı kaldırıldığında CER kodu çalışmaz.  
  
## <a name="cause"></a>Sebep  
 JıT derleme zamanında, bir nesne başvuru türü içeren bir örnekleme yalnızca temsilcisidir çünkü sonuç kodu paylaşılır ve nesne başvuru türü değişkenlerinin her biri herhangi bir nesne başvuru türü olabilir. Bu, bazı çalışma zamanı kaynaklarının zamandan önce hazırlanmasını engelleyebilir.  
  
 Özellikle, genel tür değişkenlerine sahip Yöntemler geç kaynak ayırmayı arka planda alabilir. Bunlar genel sözlük girdileri olarak adlandırılır. Örneğin, `List<T> list = new List<T>();` `List<Object>, List<String>`bir genel tür değişkeni olan,çalışmazamanınınbakmalıolmasıvemuhtemelençalışmazamanında(örneğin,vb.)tamörneklemeyioluşturmasıgerekir.`T` Bu, geliştirici denetiminin ötesinde bellek tükenme gibi çeşitli nedenlerle başarısız olabilir.  
  
 Bu MDA, tam bir örnek oluşturma işlemi olmadığında değil, yalnızca JıT derleme sırasında etkinleştirilmelidir.  
  
 Bu MDA etkinleştirildiğinde, büyük ihtimalle CERs kötü örneklemelerde işlevsel değildir. Aslında, çalışma zamanı, MDA 'ın etkinleştirilmesini neden olan koşullarda bir CER uygulamayı denemedi. Böylece geliştirici, CER 'nin paylaşılan bir örneklemesini kullanıyorsa JıT derleme hataları, genel türler türü yükleme hataları veya hedeflenen CER bölgesi dahilinde iş parçacığı durdurulduğunda yakalanmaz.  
  
## <a name="resolution"></a>Çözüm  
 Bir CER içerebilen yöntemler için nesne başvuru türü olan genel tür değişkenlerini kullanmayın.  
  
## <a name="effect-on-the-runtime"></a>Çalışma zamanında etki  
 Bu MDA, CLR üzerinde hiçbir etkisi yoktur.  
  
## <a name="output"></a>Çıkış  
 Aşağıda bu MDA 'ın çıkış örneği verilmiştir.  
  
 `Method 'GenericMethodWithCer', which contains at least one constrained execution region, cannot be prepared automatically since it has one or more unbound generic type parameters.`  
  
 `The caller must ensure this method is prepared explicitly at run time prior to execution.`  
  
 `method name="GenericMethodWithCer"`  
  
 `declaringType name="OpenGenericCERCall"`  
  
## <a name="configuration"></a>Yapılandırma  
  
```xml  
<mdaConfig>  
  <assistants>  
    <openGenericCERCall/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>Örnek  
 CER kodu yürütülmedi.  
  
```csharp
using System;  
using System.Collections.Generic;  
using System.Runtime.CompilerServices;  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        CallGenericMethods();  
    }  
    static void CallGenericMethods()  
    {  
        // This call is correct. The instantiation of the method  
        // contains only nonreference types.  
        MyClass.GenericMethodWithCer<int>();  
  
        // This call is incorrect. A shared version of the method that  
        // cannot be completely analyzed will be JIT-compiled. The   
        // MDA will be activated at JIT-compile time, not at run time.  
        MyClass.GenericMethodWithCer<String>();  
    }  
}  
  
    class MyClass  
{  
    public static void GenericMethodWithCer<T>()  
    {  
        RuntimeHelpers.PrepareConstrainedRegions();  
        try  
        {  
  
        }  
        finally  
        {  
            // This is the start of the CER.  
            Console.WriteLine("In finally block.");  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>
- <xref:System.Runtime.ConstrainedExecution>
- [Yönetilen Hata Ayıklama Yardımcıları ile Hataları Tanılama](diagnosing-errors-with-managed-debugging-assistants.md)
