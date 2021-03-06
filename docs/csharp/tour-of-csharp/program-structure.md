---
title: C#Program yapısı- C# dilin turu
description: Bir C# programın temel yapı taşlarını öğrenin
ms.date: 08/10/2016
ms.assetid: 984f0314-507f-47a0-af56-9011243f5e65
ms.openlocfilehash: 5102c72d68108f698a0456b9c14e6713778f4325
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834165"
---
# <a name="program-structure"></a>Program yapısı

' Deki C# temel kurumsal kavramlar, ***Programlar***, ***ad alanları***, ***türler***, ***Üyeler***ve ***derlemelerdir***. C#programlar bir veya daha fazla kaynak dosyadan oluşur. Programlar, üyeleri içeren ve ad alanları halinde düzenlenebilen türleri bildirir. Sınıflar ve arabirimler tür örnekleridir. Alanlar, Yöntemler, Özellikler ve olaylar üye örnekleridir. C# Programlar derlendiğinde, fiziksel olarak derlemeler halinde paketlenir. Derlemeler, sırasıyla ***uygulama*** veya ***kitaplık***uygulanıp uygulamadığına bağlı olarak `.exe` veya `.dll` dosya uzantısına sahiptir.

Örnek, `Acme.Collections` adlı bir ad alanında `Stack` adlı bir sınıf bildirir:

[!code-csharp[Stack](../../../samples/snippets/csharp/tour/program-structure/program.cs#L1-L34)]

Bu sınıfın tam adı `Acme.Collections.Stack` ' dır. Sınıf birçok üye içerir: `top` adlı bir alan, `Push` ve `Pop` adlı iki yöntem ve `Entry` adlı bir iç içe sınıf. @No__t-0 sınıfı üç üye içerir: `next` adlı bir alan, `data` adlı alan ve bir Oluşturucu. Örneğin kaynak kodunun dosyada depolandığını varsayarak `acme.cs`, komut satırı

```console
csc /t:library acme.cs
```

örneği bir kitaplık (`Main` giriş noktası olmadan) olarak derler ve `acme.dll` adlı bir derleme oluşturur.

> [!IMPORTANT]
> Yukarıdaki örnekler, komut satırı C# derleyicisi olarak `csc` kullanır. Bu derleyici bir Windows yürütülebiliridir. Diğer platformlarda C# kullanmak Için .NET Core araçlarını kullanmanız gerekir. .NET Core ekosistemi, komut satırı yapılarını yönetmek için `dotnet` CLı kullanır. Buna bağımlılıkları yönetme ve C# derleyicinin çağrılması dahildir. .NET Core tarafından desteklenen platformlarda bu araçların tam açıklaması için [Bu öğreticiye](../../core/tutorials/using-with-xplat-cli.md) bakın.

Derlemeler, ara dil (IL) yönergeleri biçiminde çalıştırılabilir kodu ve meta veri biçimindeki sembolik bilgileri içerir. Yürütülmeden önce, bir derlemedeki IL kodu, .NET ortak dil çalışma zamanının tam zamanında (JıT) derleyicisi tarafından otomatik olarak işlemciye özgü koda dönüştürülür.

Bir derleme, hem kodu hem de meta verileri içeren bir dizi işlevin kendine açıklayıcı bir birimi olduğundan, içinde C#`#include` yönergeleri ve üst bilgi dosyaları gerekmez. Belirli bir derlemede yer alan ortak türler ve Üyeler, yalnızca program derlenirken bu derlemeye C# başvurarak bir programda kullanılabilir hale getirilir. Örneğin, bu program `acme.dll` derlemesinden `Acme.Collections.Stack` sınıfını kullanır:

[!code-csharp[UsingStack](../../../samples/snippets/csharp/tour/program-structure/Program.cs#L38-L52)]

Program dosyada depolanıyorsa `example.cs` `example.cs` derlendiğinde, Acme. dll derlemesine derleyicinin/r seçeneği kullanılarak başvurulabilir:

```console
csc /r:acme.dll example.cs
```

Bu, çalıştırıldığında, çıktıyı üreten `example.exe` adlı bir çalıştırılabilir derleme oluşturur:

```console
100
10
1
```

C#bir programın kaynak metninin birkaç kaynak dosyada depolanmasına izin verir. Birden çok dosya C# programı derlendiğinde, tüm kaynak dosyalar birlikte işlenir ve kaynak dosyalar birbirini tamamen başvurabilir — kavramsal olarak, tüm kaynak dosyaları işlenmeden önce bir büyük dosyada birleştirilmiş olur. Bildirim sırası çok önemli olduğundan, C# bazı durumlarda ileri bildirimlere hiçbir şekilde gerek yoktur. C#kaynak dosyayı yalnızca bir ortak tür bildirmek üzere sınırlamaz veya kaynak dosyanın adının kaynak dosyada belirtilen bir türle eşleşmesi gerekir.

>[!div class="step-by-step"]
>[Önceki](index.md)
>[İleri](types-and-variables.md)
