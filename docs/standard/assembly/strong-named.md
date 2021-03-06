---
title: Tanımlayıcı adlı derlemeler
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies, about strong-named assemblies
- assemblies [.NET Framework], strong-named
ms.assetid: d4a80263-f3e0-4d81-9b61-f0cbeae3797b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 67beeba6ce33fb1a8c3d02337d98282ccf30341a
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991302"
---
# <a name="strong-named-assemblies"></a>Tanımlayıcı adlı derlemeler

Derlemeyi güçlü adlandırma derleme için benzersiz bir kimlik oluşturur ve derleme çakışmalarını önleyebilir.

## <a name="what-makes-a-strong-named-assembly"></a>Tanımlayıcı adlı bütünleştirilmiş kod ne olur?

Tanımlayıcı adlı bütünleştirilmiş kod, derleme ile dağıtılan ortak anahtara karşılık gelen özel anahtar kullanılarak oluşturulur ve derlemenin kendisi olur. Bütünleştirilmiş kod, derlemeyi oluşturan tüm dosyaların adlarını ve karmalarını içeren derleme bildirimini içerir. Aynı tanımlayıcı ada sahip derlemeler özdeş olmalıdır.

Visual Studio 'Yu veya bir komut satırı aracını kullanarak derlemeleri kesin olarak ad olarak belirleyebilirsiniz. Daha fazla bilgi için [nasıl yapılır: Bir derlemeyi tanımlayıcı ad](sign-strong-name.md) veya [sn. exe (tanımlayıcı ad aracı)](../../framework/tools/sn-exe-strong-name-tool.md)ile imzalayın.

Tanımlayıcı adlı bir derleme oluşturulduğunda, derleme basit metin adını, sürüm numarasını, isteğe bağlı kültür bilgilerini, dijital imzayı ve imza için kullanılan özel anahtara karşılık gelen ortak anahtarı içerir.

> [!WARNING]
> Güvenlik için tanımlayıcı adlara güvenmeyin. Yalnızca benzersiz bir kimlik sağlarlar.

## <a name="why-strong-name-your-assemblies"></a>Derlemelerinize neden güçlü ad adı veriyor?

Tanımlayıcı adlı bir derlemeye başvuru yaptığınızda, sürüm oluşturma ve adlandırma koruması gibi belirli avantajları de bekleyebilir. .NET Framework, tanımlayıcı adlı derlemeler genel derleme önbelleğinde yüklenebilir ve bu da bazı senaryoları etkinleştirmek için gereklidir.

Tanımlayıcı adlı derlemeler aşağıdaki senaryolarda faydalıdır:

- Derlemelerinize tanımlayıcı adlı derlemeler tarafından başvurulmak üzere veya tanımlayıcı adlı diğer derlemelerden derlemelerinize erişim vermek `friend` isteyebilirsiniz.

- Uygulamanın aynı derlemenin farklı sürümlerine erişmesi gerekir. Bu, çakışma olmadan aynı uygulama etki alanında yan yana yüklemek üzere bir derlemenin farklı sürümlerinin olması gerektiği anlamına gelir. Örneğin, aynı basit ada sahip derlemelerde bir API 'nin farklı uzantıları varsa, güçlü adlandırma derlemenin her sürümü için benzersiz bir kimlik sağlar.

- Derlemenizi kullanarak uygulamaların performansını olumsuz şekilde etkilememesini istemezsiniz, bu nedenle derlemenin etki alanı nötr olmasını isteyebilirsiniz. Bu, genel derleme önbelleğine bir etki alanı nötr derleme yüklenmesi gerektiğinden, güçlü adlandırma gerektirir.

- Yayımcı ilkesi uygulayarak uygulamanızın bakımını merkezileştirmek istiyorsunuz, bu, derlemenin genel derleme önbelleğinde yüklü olması gerektiği anlamına gelir.

Açık kaynaklı bir geliştiricisiyseniz ve tanımlayıcı adlı bir derlemenin kimlik avantajlarından yararlanmak istiyorsanız, kaynak denetim sisteminize bir derlemeyle ilişkili özel anahtarı iade etmeyi düşünün.

## <a name="see-also"></a>Ayrıca bkz.

- [Genel derleme önbelleği](../../framework/app-domains/gac.md)
- [Nasıl yapılır: Bir derlemeyi güçlü bir adla imzala](sign-strong-name.md)
- [Sn. exe (tanımlayıcı ad aracı)](../../framework/tools/sn-exe-strong-name-tool.md)
- [Tanımlayıcı adlı derlemeler oluşturma ve kullanma](create-use-strong-named.md)
