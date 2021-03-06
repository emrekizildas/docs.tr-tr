---
title: x:Member Yönergesi
ms.date: 03/30/2017
ms.assetid: 4d8394ef-644c-4331-b6c5-be855d392980
ms.openlocfilehash: d3d023873aab2039913a78108440a2e2d4ea77fb
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053738"
---
# <a name="xmember-directive"></a>x:Member Yönergesi
İşaretlemede bir XAML üyesi bildirir.  
  
## <a name="xaml-object-element-usage"></a>XAML Nesne Öğesi Kullanımı  
  
```xaml  
<object x:Class="className">  
  <x:Members>  
    <x:Member Name="propertyName"/>  
    additionalMembers  
  </x:Members>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML Değerleri  
  
|||  
|-|-|  
|`className`|XAML üretimi için yedekleme sınıfının veya kısmi sınıfın adı.|  
|`memberName`|Tanımlanan özelliğin üye adı.|  
  
## <a name="remarks"></a>Açıklamalar  
 .NET Framework XAML Hizmetleri uygulamasında,. `x:Member`doğrudan bir tür yedeklemesi yoktur, ancak <xref:System.Windows.Markup.MemberDefinition> sınıfı tarafından desteklenir. Xaml düğüm akışında `x:Member` , bir öğesi xaml Language xaml ad alanından adlı `Member`bir üye olarak temsil edilir. Üye `Member` , biçimlendirme tarafından belirtilen öznitelikleri barındırır.  
  
 Ve ' `Name` `Type` nin anlamı .NET Framework xaml Hizmetleri düzeyinde atanmaz. Bunlar, daha sonra belirli çerçeveler tarafından uygulanabilir kuralların altında yorumlanmak üzere, ilk XAML düğüm akışında dize değerleri olarak depolanır. Anlamı bir XAML adı ve XAML türü anlamını gösterebilir veya uygulamaya bağlı olarak yalnızca bir yedekleme türü sisteminde geçerli olabilir.  
  
 ' Nin pratik kullanımını, `x:Members` İşaretlemede üye tanımlarının belirtilmesi için bir yol olarak desteklemek amacıyla, üyelerin değiştirilebilen bir sınıfla ilişkilendirilmesi gerekir. Hedeflenen model `x:Members` , bir `x:Class`türü belirten bir üye olarak mevcuttur. Ancak, türleri ve üyeleri ilişkilendirme mekanizması veya dinamik üye tanımlarının üretilmesinin .NET Framework XAML Hizmetleri düzeyinde desteklenmez. Bu, XAML 'den üye tanımlarını destekleyen uygulama modelleri olan tek tek çerçeveler için bırakılır. Genellikle, XAML 'yi biçimlendirme-derleme ve bu özelliği desteklemeye yönelik saf from-XAML derlemeleri ile tümleştirme sağlayan MSBUILD derleme eylemleri.  
  
## <a name="xproperty-for-windows-workflow-foundation"></a>Windows Workflow Foundation için x:Property  
 Windows Workflow Foundation için, `x:Property` tamamen XAML 'de oluşturulan özel bir etkinliğin üyelerini ya da arka plan kod içeren bir etkinlik tasarımcısının xaml tanımlı dinamik üyelerini tanımlar. `x:Class`Ayrıca XAML üretiminin kök öğesinde de belirtilmelidir. Bu, .NET Framework XAML Hizmetleri düzeyinde bir gereklilik değildir, ancak XAML üretimi özel etkinlikleri destekleyen MSBUILD derleme eylemleri tarafından yüklendiğinde ve genel olarak XAML Windows Workflow Foundation bir gereksinim haline gelir. Windows Workflow Foundation, saf xaml tür adını `x:Property` `Type` özniteliği için amaçlanan değeri olarak kullanmaz ve bunun yerine burada belgelenmeyen bir kural kullanır. Daha fazla bilgi için bkz. [DynamicActivity oluşturma](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd807392(v=vs.100)).
