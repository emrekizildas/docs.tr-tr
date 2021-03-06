---
title: .NET Core ve Açık Kaynak
ms.date: 03/30/2017
ms.assetid: e6bd4655-ce37-4003-8462-468a6fe2c40f
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2ad74a70fff9916dc66bb4d2eacbdaf40cb241c3
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70853955"
---
# <a name="net-core-and-open-source"></a>.NET Core ve Açık Kaynak
Bu konuda .NET Core 'un ne olduğuna ilişkin kısa bir genel bakış sağlanır ve nasıl daha fazla bilgi bulabileceğiniz gösterilmektedir. .NET Core için konuların tüm listesini bulmak için [.NET Core Kılavuzu](../../core/index.md)' nu ziyaret edin.
  
<a name="BKMK_WhatisNETCore"></a>   
## <a name="what-is-net-core"></a>.NET Core nedir?  
 .NET Core, .NET Standard genel amaçlı, modüler, platformlar arası ve açık kaynaklı bir uygulamadır. .NET Framework ile aynı API 'lerin birçoğunu içerir (ancak .NET Core daha küçük bir küme) ve çeşitli işletim sistemlerini ve yonga hedeflerini destekleyen çalışma zamanı, çerçeve, derleyici ve araç bileşenlerini içerir. .NET Core uygulamasının öncelikli olarak ASP.NET Core iş yükleri tarafından ve ayrıca ihtiyacın yanı sıra daha modern bir uygulamaya sahip olması gerekir. Cihaz, bulut ve katıştırılmış/IoT senaryolarında kullanılabilir.  
  
 .NET Core 'u kullanmaya başlamak için [10 dakikalık](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro).net öğreticisini ziyaret edin Merhaba dünya.  
  
 .NET Core 'un ana özellikleri şunlardır:  
  
- **Platformlar arası:** .NET Core, ihtiyacınız olan uygulama özelliklerini uygulamak ve platform hedefinizden bağımsız olarak bu kodu yeniden kullanmak için temel işlevsellik sağlar. Şu anda üç ana işletim sistemini (OS) desteklemektedir: Windows, Linux ve macOS. Desteklenen işletim sistemleri arasında değiştirilmemiş olarak çalışan uygulamalar ve kitaplıklar yazabilirsiniz. Desteklenen işletim sistemlerinin listesini görmek için [.NET Core yol haritası](https://github.com/dotnet/core/blob/master/roadmap.md)' nı ziyaret edin.
  
- **Açık Kaynak:** .NET Core, [.net Foundation](https://www.dotnetfoundation.org/) 'ın Stewardship altındaki birçok projeden biridir ve [GitHub](https://github.com/)' da kullanılabilir.  Açık kaynaklı bir proje olarak .NET Core 'un olması, daha saydam bir geliştirme sürecini yükseltir ve etkin ve bağlı bir topluluk yükseltir.  
  
- **Esnek dağıtım:** uygulamanızı dağıtmanın iki ana yolu vardır: çerçeveye bağımlı dağıtım veya kendi kendine kapsanan dağıtım. Çerçeveye bağımlı dağıtım ile, yalnızca uygulamanız ve üçüncü taraf bağımlılıkları yüklenir ve uygulamanız, .NET Core 'un sistem genelindeki bir sürümüne bağlıdır.  Kendi kendine içerilen dağıtım ile uygulamanızı oluşturmak için kullanılan .NET Core sürümü, uygulamanız ve üçüncü taraf bağımlılıklarınızla birlikte da dağıtılır ve diğer sürümlerle yan yana çalıştırılabilir.    Daha fazla bilgi için bkz. [.NET Core uygulama dağıtımı](../../core/deploying/index.md).

- **Modüler:** .NET Core, daha küçük derleme paketlerinde NuGet aracılığıyla yayınlandığı için modüler hale gelir. Çekirdek işlevlerin çoğunu içeren bir büyük derleme yerine, .NET Core daha küçük Özellik merkezli paketler olarak sunulmaktadır. Bu, bizim için daha çevik bir geliştirme modeli sağlar ve uygulamanızı yalnızca ihtiyacınız olan NuGet paketlerini içerecek şekilde iyileştirmenize olanak tanır. Daha küçük bir uygulama yüzeyi alanının avantajları, daha sıkı güvenlik, azaltılmış bakım, iyileştirilmiş performans ve bir Kullandıkça öde modelinde daha düşük maliyetlere sahiptir.  
  
## <a name="the-net-core-platform"></a>.NET Core platformu  
 .NET Core platformu, yönetilen derleyiciler, çalışma zamanı, temel sınıf kitaplıkları ve ASP.NET Core gibi çok sayıda uygulama modeli içeren birkaç bileşenden oluşur. Aşağıdaki [GitHub](https://github.com/) depolarını ziyaret ederek, farklı bileşenler hakkında daha fazla bilgi alabilir ve bağlı olabilirsiniz:  
  
- [.NET Core](https://github.com/dotnet/core)  
  
- [CoreFX-.NET Core temel kitaplıkları](https://github.com/dotnet/corefx)  
  
- [CoreCLR-.NET Core çalışma zamanı](https://github.com/dotnet/coreclr)  
  
- [CLı-.NET Core komut satırı araçları](https://github.com/dotnet/cli)  
  
- [Roslyn-.NET Compiler Platform](https://github.com/dotnet/roslyn)  
  
- [ASP.NET Core](https://github.com/aspnet/home)  
  
## <a name="see-also"></a>Ayrıca bkz.

- [.NET öğreticisi-10 dakika içinde Merhaba Dünya](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro)
- [.NET Core Kılavuzu](../../core/index.md)
- [ASP.NET Core belgeleri](/aspnet/core/)
