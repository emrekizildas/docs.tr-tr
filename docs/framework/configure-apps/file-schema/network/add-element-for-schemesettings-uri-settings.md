---
title: schemeSettings için <add> Öğesi (Uri Ayarları)
ms.date: 03/30/2017
ms.assetid: 594a7b3b-af23-4cfa-b616-0b2dddb1a705
ms.openlocfilehash: efd52557ea8b617a39e685ff8ad69bab01322a7a
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699602"
---
# <a name="add-element-for-schemesettings-uri-settings"></a>\<mesettings için > öğesi ekleme (URI ayarları)
Düzen adı için bir düzen ayarı ekler.  
  
[ **\<Yapılandırma >** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **\<urı >** ](uri-element-uri-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3[ **\<bir mesettings >** ](schemesettings-element-uri-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5 **\<add >**  
  
## <a name="syntax"></a>Sözdizimi  
  
```xml  
<add
  name="http|https"
  genericUriParserOptions="DontUnescapePathDotsAndSlashes"
/>  
```  
  
## <a name="attributes-and-elements"></a>Öznitelikler ve Öğeler  
 Aşağıdaki bölümlerde öznitelikler, alt öğeler ve üst öğeler açıklanır  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|  
|---------------|-----------------|  
|name|Bu ayarın geçerli olduğu Düzen adı. Yalnızca Name = "http" ve Name = "https" değerleri desteklenir.|  
  
## <a name="attribute-name-attribute"></a>{Öznitelik adı} Özniteliğe  
  
|Değer|Açıklama|  
|-----------|-----------------|  
|genericUriParserOptions|Bu şema için ayrıştırıcı seçenekleri. Yalnızca genericUriParserOptions = "DontUnescapePathDotsAndSlashes" değeri desteklenir.|  
  
### <a name="child-elements"></a>Alt Öğeler  
 Yok.  
  
### <a name="parent-elements"></a>Üst Öğeler  
  
|Öğe|Açıklama|  
|-------------|-----------------|  
|[\<Ramesettings > öğesi (Uri Ayarları)](schemesettings-element-uri-settings.md)|Belirli düzenler için <xref:System.Uri> ' ın nasıl ayrıştıralınacağını belirtir.|  
  
## <a name="remarks"></a>Açıklamalar  
 Varsayılan olarak, <xref:System.Uri?displayProperty=nameWithType> sınıfı, yol sıkıştırmayı yürütmeden önce yüzde kodlamalı yol sınırlayıcılarını kaldırır. Bu, aşağıdaki gibi saldırılara karşı bir güvenlik mekanizması olarak uygulanmıştır:  
  
 `http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 Bu URI, yüzde kodlamalı karakterleri doğru şekilde işlemeyen modüllere geçiriliyorsa, aşağıdaki komut sunucu tarafından yürütülebilmesiyle sonuçlanabilir:  
  
 `c:\Windows\System32\cmd.exe /c dir c:\`  
  
 Bu nedenle, <xref:System.Uri?displayProperty=nameWithType> sınıfı ilk olarak yol sınırlayıcılarını yok eder ve ardından yol sıkıştırması uygular. Yukarıdaki kötü amaçlı URL 'YI <xref:System.Uri?displayProperty=nameWithType> sınıf oluşturucusuna geçirmenin sonucu aşağıdaki URI ile sonuçlanır:  
  
 `http://www.microsoft.com/Windows/System32/cmd.exe?/c+dir+c:\`  
  
 Bu varsayılan davranış, belirli bir düzen için ıgmesettings yapılandırma seçeneği kullanılarak yüzde olmayan kodlanmış yol sınırlayıcılarını kaçırılmamış şekilde değiştirilebilir.  
  
## <a name="configuration-files"></a>Yapılandırma Dosyaları  
 Bu öğe, uygulama yapılandırma dosyasında veya makine yapılandırma dosyasında (Machine. config) kullanılabilir.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki örnek, http şeması için yüzde kodlamalı bir yol sınırlayıcılarını yok etmek üzere <xref:System.Uri> sınıfı tarafından kullanılan bir yapılandırmayı gösterir.  
  
```xml  
<configuration>  
  <uri>  
    <schemeSettings>  
      <add name="http" genericUriParserOptions="DontUnescapePathDotsAndSlashes"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Configuration.SchemeSettingElement?displayProperty=nameWithType>
- <xref:System.Configuration.SchemeSettingElementCollection?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection.SchemeSettings%2A?displayProperty=nameWithType>
- <xref:System.GenericUriParserOptions?displayProperty=nameWithType>
- <xref:System.Uri?displayProperty=nameWithType>
- [Ağ Ayarları Şeması](index.md)
