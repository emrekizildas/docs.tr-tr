---
title: Sürüm oluşturma ve .NET kitaplıkları
description: .NET kitaplıklarını sürüm oluşturma için en iyi yöntem önerileri.
author: jamesnk
ms.author: mairaw
ms.date: 12/10/2018
ms.openlocfilehash: 9250e48707c0ea72cdf8bef9663f5a3516309b86
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70969015"
---
# <a name="versioning"></a>Sürüm Oluşturma

Yazılım kitaplığı sürüm 1,0 ' de nadiren tamamlanmıştır. İyi kitaplıklar zaman içinde geliştikçe, özellikler ekleyerek, hataları düzelterek ve performansı artırdı. Mevcut kullanıcıları bozmadan, her bir sürümle ek değer sağlayan bir .NET kitaplığının yeni sürümlerini yayınlanbilmeniz önemlidir.

## <a name="breaking-changes"></a>Yeni değişiklikler

Sürümler arasındaki önemli değişiklikleri işleme hakkında daha fazla bilgi için bkz. [son değişiklikler](./breaking-changes.md).

## <a name="version-numbers"></a>Sürüm numaraları

.NET kitaplığı, bir sürümü belirtmek için birçok yol sunar. Bu sürümler en önemli öneme sahiptir:

### <a name="nuget-package-version"></a>NuGet paket sürümü

[NuGet paket sürümü](/nuget/reference/package-versioning) , NuGet.org, Visual Studio NuGet Paket Yöneticisi ve paket kullanıldığında kaynak koda eklenir. NuGet paket sürümü, kullanıcıların yaygın olarak görebilecekleri sürüm numarasıdır ve kullandıkları bir kitaplığın sürümü hakkında konuşduklarında bu bilgileri ifade eder. NuGet paket sürümü NuGet tarafından kullanılır ve çalışma zamanı davranışını etkilemez.

```xml
<PackageVersion>1.0.0-alpha1</PackageVersion>
```

NuGet paket sürümü ile birlikte bulunan NuGet paket tanımlayıcısı, NuGet içindeki bir paketi tanımlamak için kullanılır. Örneğin, `Newtonsoft.Json`.  +  `11.0.2` Soneki olan bir paket yayın öncesi paketidir ve test için ideal hale getiren özel davranışları vardır. Daha fazla bilgi için bkz. [yayın öncesi paketleri](./nuget.md#pre-release-packages).

NuGet paketi sürümü geliştiricilerin en çok görülebilen sürümü olduğu için, [anlamsal sürüm oluşturma (SemVer)](https://semver.org/)kullanılarak güncelleştirilmesi iyi bir fikirdir. SemVer, yayın arasındaki değişikliklerin önemini gösterir ve geliştiricilerin hangi sürümü kullanacağınızı seçerken bilinçli bir karar vermesini sağlar. Örneğin, ' dan `1.0` `2.0` ' a giderek, olası büyük değişiklikler olduğunu gösterir.

**✔️** NuGet paketinizi sürüm Için [Semver 2.0.0](https://semver.org/) kullanmayı düşünün.

**✔️** , kullanıcıların yaygın olarak göreceği sürüm numarası olduğundan, ortak belgelerde NuGet paketi sürümünü kullanın.

kararlı olmayan bir paket yayınlarken yayın öncesi son eki dahil **✔️** .

> Kullanıcılar, yayın öncesi paketleri almak için kabul etmelidir, dolayısıyla paketin tamamlanmamış olduğunu anlayacaktır.

### <a name="assembly-version"></a>Derleme sürümü

Derleme sürümü, CLR 'nin hangi derleme sürümünü yükleneceğini seçmek için çalışma zamanında kullandığı şeydir. Sürüm oluşturma kullanılarak bir derlemeyi seçmek, yalnızca güçlü bir ada sahip derlemeler için geçerlidir.

```xml
<AssemblyVersion>1.0.0.0</AssemblyVersion>
```

Windows .NET Framework CLR kesin bir adlandırılmış derlemeyi yüklemek için tam bir eşleşme talep ister. Örneğin, `Libary1, Version=1.0.0.0` bir `Newtonsoft.Json, Version=11.0.0.0`başvurusu ile derlendi. .NET Framework bu sürümü `11.0.0.0`yalnızca tam olarak yükler. Çalışma zamanında farklı bir sürüm yüklemek için .NET uygulamasının yapılandırma dosyasına bir bağlama yeniden yönlendirmesi eklenmelidir.

Bütünleştirilmiş kod sürümüyle birlikte tanımlayıcı adlandırma [katı derleme sürümü yüklemeye](../assembly/versioning.md)izin vermez. Bir kitaplıkta güçlü adlandırma bir dizi avantaja sahip olsa da, genellikle bir derlemenin bulunamaması ve içinde `app.config` / `web.config` [bağlama yeniden yönlendirmeleri](../../framework/configure-apps/redirect-assembly-versions.md) düzeltilmesi gereken çalışma zamanı özel durumları oluşur. .NET Core derleme yüklemesi gevşek bir şekilde geliştirilmiştir ve .NET Core CLR, derlemeleri daha yüksek bir sürüme sahip çalışma zamanında otomatik olarak yükler.

✔️ yalnızca AssemblyVersion içinde önemli bir sürüm dahil olmak üzere **göz önünde bulundurun** .

> Örneğin, Library 1,0 ve Library 1.0.1 'in `1.0.0.0`AssemblyVersion 'ı vardır, ancak kitaplığı 2,0 ' nin `2.0.0.0`AssemblyVersion 'ı vardır. Derleme sürümü genellikle daha az değiştiğinde bağlama yeniden yönlendirmelerini azaltır.

✔️ AssemblyVersion 'ın ana sürüm numarasını ve NuGet paket sürümünü eşitlenmiş halde tutmayı **göz önünde bulundurun** .

> AssemblyVersion, kullanıcıya görüntülenen bazı bilgilendirici iletilere, örneğin, özel durum iletilerinde derleme adı ve derleme nitelikli tür adlarına dahildir. Sürümler arasındaki ilişkinin saklanması, geliştiriciler tarafından hangi sürümü kullandıkları hakkında daha fazla bilgi sağlar.

**❌** Sabit bir AssemblyVersion yok.

> Bir AssemblyVersion, bağlama yeniden yönlendirmeleri gereksinimini ortadan kaldırdıkça, derlemenin yalnızca tek bir sürümünün genel derleme önbelleği 'ne (GAC) yüklenebileceği anlamına gelir. Ayrıca, GAC 'de derlemeye başvuruda bulunan uygulamalar, başka bir uygulama GAC derlemesini bozan değişikliklerle güncelleştirmiş olursa kesilir.

### <a name="assembly-file-version"></a>Bütünleştirilmiş kod dosyası sürümü

Derleme dosyası sürümü, Windows 'ta bir dosya sürümünü göstermek için kullanılır ve çalışma zamanı davranışına hiçbir etkiye sahip değildir. Bu sürümün ayarlanması isteğe bağlıdır. Windows Gezgini 'nde dosya özellikleri iletişim kutusunda görünür:

```xml
<FileVersion>11.0.2.21924</FileVersion>
```

![Windows Gezgini](./media/versioning/win-properties.png "Windows Gezgini")

✔️ AssemblyFileVersion düzeltmesi olarak bir sürekli tümleştirme yapı numarası dahil **etmeyi göz önünde bulundurun** .

> Örneğin, projenizin sürüm 1.0.0 derleniyor ve sürekli tümleştirme derleme numarası 99 ' dir; bu nedenle AssemblyFileVersion 1.0.0.99.

**✔️** dosya sürümü biçimini `Major.Minor.Build.Revision` kullanır.

> Dosya sürümü hiçbir şekilde .NET tarafından kullanılmadığından, [Windows dosya sürümünün](/windows/desktop/menurc/versioninfo-resource) `Major.Minor.Build.Revision` biçimde olmasını bekler. Sürüm bu biçimi izmezse bir uyarı tetiklenir.

### <a name="assembly-informational-version"></a>Derleme bilgilendirici sürümü

Derleme bilgilendirici sürümü, ek sürüm bilgilerini kaydetmek için kullanılır ve çalışma zamanı davranışına hiçbir etkiye sahip değildir. Bu sürümün ayarlanması isteğe bağlıdır. Kaynak bağlantısı kullanıyorsanız, bu sürüm NuGet paketi sürümü ve kaynak denetimi sürümü ile derleme üzerinde ayarlanır. Örneğin, `1.0.0-beta1+204ff0a` derlemenin oluşturulduğu kaynak kodun COMMIT karmasını içerir. Daha fazla bilgi için bkz. [kaynak bağlantısı](./sourcelink.md).

```xml
<AssemblyInformationalVersion>The quick brown fox jumped over the lazy dog.</AssemblyInformationalVersion>
```

> [!NOTE]
> Visual Studio 'nun eski sürümleri, bu sürüm biçimini `Major.Minor.Build.Revision`izmazsa derleme uyarısı oluşturur. Uyarı güvenle yoksayılabilir.

**❌** Derleme bilgilendirici sürümünü kendi kendinize ayarlamaktan kaçının.

> SourceLink 'in NuGet ve kaynak denetimi meta verilerini içeren sürümü otomatik olarak oluşturmasına izin verin.

>[!div class="step-by-step"]
>[Önceki](publish-nuget-package.md)İleri
>[](breaking-changes.md)
