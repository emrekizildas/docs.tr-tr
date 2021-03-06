---
title: <supportedRuntime> yapılandırma öğesi-.NET
ms.date: 04/02/2019
ms.custom: updateeachrelease
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#supportedRuntime
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/supportedRuntime
helpviewer_keywords:
- supportedRuntime element
- <supportedRuntime> element
ms.assetid: 1ae16e23-afbe-4de4-b413-bc457f37b69f
ms.openlocfilehash: 5e7fc5f81468ff7c4eba8145ee42a4c7cf8bc0b8
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697514"
---
# <a name="supportedruntime-element"></a>\<supportedRuntime > öğesi

Uygulamanın desteklediği ortak dil çalışma zamanı sürümünü ve isteğe bağlı olarak .NET Framework sürümünü belirtir.  

[\<yapılandırma >](../configuration-element.md)  
&nbsp; @ no__t-1[\<startup >](startup-element.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 **\<supportedRuntime >**  

## <a name="syntax"></a>Sözdizimi

```xml
<supportedRuntime version="runtime version" sku="sku id"/>
```

## <a name="attributes"></a>Öznitelikler

|Öznitelik|Açıklama|
|---------------|-----------------|
|**version**|İsteğe bağlı öznitelik.<br /><br /> Bu uygulamanın desteklediği ortak dil çalışma zamanı (CLR) sürümünü belirten bir dize değeri. @No__t-0 özniteliğinin geçerli değerleri için, ["çalışma zamanı sürümü" değerleri](#version) bölümüne bakın. **Note:**  .NET Framework 3,5 ' de, "*çalışma zamanı sürümü*" değeri formu *önemli*olarak alır. *küçük*. *oluşturun*. .NET Framework 4 ' ten itibaren, yalnızca büyük ve küçük sürüm numaraları gereklidir (yani "v 4.0.30319" yerine "v 4.0"). Kısa dize önerilir.|
|**isteyin**|İsteğe bağlı öznitelik.<br /><br /> Bu uygulamanın hangi .NET Framework sürümünü desteklediğini belirten stok tutma birimini (SKU) belirten bir dize değeri.<br /><br /> .NET Framework 4,0 ' den başlayarak `sku` özniteliğinin kullanılması önerilir.  Mevcut olduğunda, uygulamanın hedeflediği .NET Framework sürümünü belirtir.<br /><br /> SKU özniteliğinin geçerli değerleri için, ["SKU kimliği" değerleri](#sku) bölümüne bakın.|

## <a name="remarks"></a>Açıklamalar

**@No__t-1supportedRuntime >** öğesi uygulama yapılandırma dosyasında yoksa, uygulamayı oluşturmak için kullanılan çalışma zamanının sürümü kullanılır.

**@No__t-1supportedRuntime >** öğesi, çalışma zamanının 1,1 veya sonraki bir sürümü kullanılarak oluşturulan tüm uygulamalar tarafından kullanılmalıdır. Yalnızca çalışma zamanının 1,0 sürümünü desteklemek üzere oluşturulan uygulamalar [\<requiredRuntime >](../startup/requiredruntime-element.md) öğesini kullanmalıdır.

> [!NOTE]
> Yapılandırma dosyasını belirtmek için [CorBindToRuntimeByCfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md) işlevini kullanırsanız, çalışma zamanının tüm sürümleri için `<requiredRuntime>` öğesini kullanmanız gerekir. [CorBindToRuntimeByCfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md)kullandığınızda `<supportedRuntime>` öğesi yok sayılır.  
  
1,1 ile 3,5 arasında .NET Framework çalışma zamanının sürümlerini destekleyen uygulamalar için, çalışma zamanının birden çok sürümü desteklenbir şekilde ilk öğe, çalışma zamanının en çok tercih edilen sürümünü belirtmeli ve son öğe en az tercih edilen sürüm. .NET Framework 4,0 veya sonraki sürümleri destekleyen uygulamalar için `version` özniteliği, .NET Framework 4 ve sonraki sürümlerde ortak olan CLR sürümünü gösterir ve `sku` özniteliği, uygulamanın hedeflediği tek bir .NET Framework sürümünü gösterir. 

Yapılandırma dosyasında `sku` özniteliğine sahip **\<supportedRuntime >** öğesi varsa ve yüklü .NET Framework sürümü belirtilen desteklenen sürümden düşükse, uygulama çalıştırılamaz ve bunun yerine bir desteklenen sürümü yüklemek isteyen ileti. Aksi takdirde, uygulama yüklü herhangi bir sürümde çalışmaya çalışır, ancak bu sürümle tam olarak uyumlu değilse beklenmedik şekilde davranabilir. (.NET Framework sürümleri arasındaki uyumluluk farklılıkları için, .NET Framework bkz. [uygulama uyumluluğu](https://docs.microsoft.com/dotnet/framework/migration-guide/application-compatibility).) Bu nedenle, daha kolay hata tanılama için bu öğeyi uygulama yapılandırma dosyasına eklemeniz önerilir. (Yeni bir proje oluştururken, Visual Studio tarafından otomatik olarak oluşturulan yapılandırma dosyası zaten içerir.)
  
> [!NOTE]
> Uygulamanız [CorBindToRuntimeEx işlevi](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)gibi eski etkinleştirme yollarını kullanıyorsa ve bu yolların daha önceki bir sürüm yerine CLR sürüm 4 ' ü etkinleştirmesini istiyorsanız veya uygulamanız .NET Framework 4 ile oluşturulup bir bağımlılığı varsa .NET Framework önceki bir sürümüyle oluşturulmuş karma modda bir derlemede, desteklenen çalışma zamanları listesinde .NET Framework 4 ' ü belirtmek yeterli değildir. Ayrıca, yapılandırma dosyanızdaki [\<startup > öğesinde](../startup/startup-element.md) , `useLegacyV2RuntimeActivationPolicy` özniteliğini `true` olarak ayarlamanız gerekir. Ancak, bu özniteliğin `true` olarak ayarlanması, .NET Framework önceki sürümleriyle oluşturulan tüm bileşenlerin, yerleşik oldukları çalışma zamanları yerine .NET Framework 4 kullanılarak çalıştırıldığı anlamına gelir.

Uygulamaları üzerinde çalıştırabilecekleri tüm .NET Framework sürümleri ile sınamanızı öneririz.

<a name="version"></a> 
## <a name="runtime-version-values"></a>"çalışma zamanı sürümü" değerleri
@No__t-0 özniteliği, belirli bir uygulama için gerekli olan ortak dil çalışma zamanı (CLR) sürümünü belirtir. Tüm .NET Framework v4. x sürümlerinin `v4.0` CLR belirttiğine unutmayın. Aşağıdaki tabloda `version` özniteliğinin *çalışma zamanı sürüm* değeri için geçerli değerler listelenmektedir.

|.NET Framework sürümü|`version` özniteliği|
|----------------------------|-------------------------|
|1.0|"v 1.0.3705"|
|1.1|"v 1.1.4322"|
|2,0|"v 2.0.50727"|
|3.0|"v 2.0.50727"|
|3.5|"v 2.0.50727"|
|4.0-4.8|"v 4.0"|

## <a name="sku"></a>"SKU kimliği" değerleri

@No__t-0 özniteliği, uygulamanın hedeflediği ve çalışması gereken .NET Framework sürümünü göstermek için bir hedef çerçeve bilinen adı (tfd) kullanır. Aşağıdaki tabloda, .NET Framework 4 ' ten başlayarak `sku` özniteliği tarafından desteklenen geçerli değerler listelenmiştir.

|.NET Framework sürümü|`sku` özniteliği|
|----------------------------|---------------------|
|4.0|". NETFramework, sürüm = v 4.0 "|
|4,0, istemci profili|". NETFramework, sürüm = v 4.0, profil = Istemci "|
|4,0, Platform Güncelleştirme 1|". NETFramework, sürüm = v 4.0.1 "|
|4,0, istemci profili, güncelleştirme 1|". NETFramework, Version = v 4.0.1, profile = Client "|
|4,0, Platform Güncelleştirme 2|". NETFramework, sürüm = v 4.0.2 "|
|4,0, istemci profili, güncelleştirme 2|". NETFramework, Version = v 4.0.2, profile = Client "|
|4,0, Platform Güncelleştirme 3|". NETFramework, sürüm = v 4.0.3 "|
|4,0, istemci profili, güncelleştirme 3|". NETFramework, Version = v 4.0.3, profile = Client "|
|4,5|". NETFramework, sürüm = v 4.5 "|
|4.5.1|". NETFramework, sürüm = v 4.5.1 "|
|4.5.2|". NETFramework, sürüm = v 4.5.2 "|
|4.6|". NETFramework, sürüm = v 4.6 "|
|4.6.1|". NETFramework, sürüm = v 4.6.1 "|
|4.6.2|". NETFramework, sürüm = v 4.6.2 "|
|4,7|". NETFramework, sürüm = v 4.7 "|
|4.7.1|". NETFramework, sürüm = v 4.7.1 "|
|4.7.2|". NETFramework, sürüm = v 4.7.2 "|
|4,8|". NETFramework, sürüm = v 4.8 "|

## <a name="example"></a>Örnek

Aşağıdaki örnek, bir yapılandırma dosyasında desteklenen çalışma zamanı sürümünün nasıl ekleneceğini gösterir. Yapılandırma dosyası, uygulamanın 4,7 .NET Framework hedeflediği anlamına gelir.

```xml
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7" />
   </startup>
</configuration>
```

## <a name="configuration-file"></a>Yapılandırma dosyası

Bu öğe, uygulama yapılandırma dosyasında kullanılabilir.

## <a name="see-also"></a>Ayrıca bkz.

- [Başlangıç Ayarları Şeması](../startup/index.md)
- [Yapılandırma Dosyası Şeması](../index.md)
- [İşlem İçi Yan Yana Yürütme](../../../deployment/in-process-side-by-side-execution.md)
