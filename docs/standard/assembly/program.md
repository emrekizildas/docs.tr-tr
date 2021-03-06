---
title: Bütünleştirilmiş kod içeren program
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework], programming
- programming assemblies
ms.assetid: 25918b15-701d-42c7-95fc-c290d08648d6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 03babe701b46eab54a76094c4728af80e6d9911e
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70973140"
---
# <a name="program-with-assemblies"></a>Bütünleştirilmiş kod içeren program
Derlemeler .NET Framework yapı taşlarıdır; temel dağıtım, sürüm denetimi, yeniden kullanım, etkinleştirme kapsamı ve güvenlik izinleri oluşturur. Bir derleme, ortak dil çalışma zamanına tür uygulamalarına dikkat etmesi için gerekli bilgileri sunar. Birlikte çalışacak ve mantıksal bir işlevsellik birimi oluşturacak bir tür ve kaynak koleksiyonudur. Çalışma zamanı için, bir derleme bağlamı dışında bir tür yoktur.  
  
 Bu bölümde modüller oluşturma, modüllerden derlemeler oluşturma, bir anahtar çifti oluşturma ve bir derlemeyi tanımlayıcı adla imzalama ve genel bütünleştirilmiş kod önbelleğine bir derleme yüklemesi açıklanmaktadır. Ayrıca, bu bölümde, derleme bildirimi bilgilerini görüntülemek için [MSIL Disassembler (ıldadsm. exe)](../../framework/tools/ildasm-exe-il-disassembler.md) ' nin nasıl kullanılacağı açıklanmaktadır.  
  
> [!NOTE]
> .NET Framework sürüm 2,0 ' den başlayarak, çalışma zamanı, yüklü olan çalışma zamanından daha yüksek bir sürüm numarasına sahip .NET Framework bir sürümle derlenen bir derlemeyi yüklemez. Bu, sürüm numarasının büyük ve küçük bileşenlerinin birleşimi için geçerlidir.  
  
## <a name="in-this-section"></a>Bu bölümde  
 [Derlemeler oluştur](create.md)  
 Tek dosyalı ve çoklu dosya Derlemeleriyle genel bir bakış sağlar.  
  
 [Derleme adları](names.md)  
 Derleme adlandırmasına genel bir bakış sağlar.  
  
 [Nasıl yapılır: Bir derlemenin tam nitelikli adını belirleme](find-fully-qualified-name.md)  
 Bir derlemenin tam nitelikli adının nasıl belirleneceğini açıklar.  
  
 [Intranet uygulamalarını tam güvende çalıştırma](../../framework/app-domains/running-intranet-applications-in-full-trust.md)  
 Bir intranet paylaşımında tam güvenle derlemeler için eski güvenlik ilkesinin nasıl belirtileceğini açıklar.  
  
 [Derleme konumu](location.md)  
 Derlemelerin nereye bulunacağı hakkında genel bakış sağlar.  
  
 [Nasıl yapılır: Tek dosya derlemesi oluşturma](../../framework/app-domains/build-single-file-assembly.md)  
 Tek dosya derlemesinin nasıl oluşturulacağını açıklar.  
  
 [Çoklu dosya derlemeleri](../../framework/app-domains/multifile-assemblies.md)  
 Çok dosyalı derlemeler oluşturma nedenlerini açıklar.  
  
 [Nasıl yapılır: Çoklu dosya derlemesi oluşturma](../../framework/app-domains/build-multifile-assembly.md)  
 Çoklu dosya derlemesinin nasıl oluşturulacağını açıklar.  
  
 [Derleme özniteliklerini ayarla](set-attributes.md)  
 Derleme özniteliklerini ve bunların nasıl ayarlanacağını açıklar.  
  
 [Tanımlayıcı adlı derlemeler oluşturma ve kullanma](create-use-strong-named.md)  
 Bir derlemeyi güçlü bir adla nasıl ve neden imzalayabileceğinizi açıklar ve nasıl yapılır konularını içerir.  
  
 [Bir derlemeyi gecikmeli imzala](delay-sign.md)  
 Bir derlemenin nasıl geciktirileneceğini açıklar.  
  
 [Derlemeler ve genel derleme önbelleği ile çalışma](../../framework/app-domains/working-with-assemblies-and-the-gac.md)  
 Derlemelerin nasıl ve neden genel derleme önbelleğine ekleneceğini ve nasıl yapılır konuları içerdiğini açıklar.  
  
 [Nasıl yapılır: Derleme içeriğini görüntüle](view-contents.md)  
 Derleme içeriğini görüntülemek için MSIL Disassembler (ıldadsm. exe) ' nin nasıl kullanılacağını açıklar.  
  
 [Ortak dil çalışma zamanında tür iletimi](type-forwarding.md)  
 Mevcut uygulamaları bozmadan bir türü farklı bir derlemeye taşımak için tür iletmenin nasıl kullanılacağını açıklar.  
  
## <a name="reference"></a>Başvuru  
 <xref:System.Reflection.Assembly>  
 Bir derlemeyi temsil eden .NET Framework sınıfı.  
  
## <a name="related-sections"></a>İlgili bölümler  
 [Nasıl yapılır: Bir derlemeden tür ve üye bilgilerini alma](../../framework/reflection-and-codedom/get-type-member-information.md)  
 Bir derlemeden program aracılığıyla tür ve diğer bilgilerin nasıl elde edileceğini açıklar.  
  
 [.NET’te bütünleştirilmiş kodlar](index.md)  
 Ortak dil çalışma zamanı derlemelerine kavramsal bir genel bakış sağlar.  
  
 [Derleme sürümü oluşturma](versioning.md)  
 Derleme bağlamaya ve <xref:System.Reflection.AssemblyVersionAttribute> ve <xref:System.Reflection.AssemblyInformationalVersionAttribute> özniteliklerine ilişkin bir genel bakış sağlar.  
  
 [Çalışma zamanının derlemeleri nasıl konumlandırır](../../framework/deployment/how-the-runtime-locates-assemblies.md)  
 Çalışma zamanının, bir bağlama isteğini yerine getirmek için hangi derlemeyi kullanacağınızı nasıl belirlediğini açıklar.  
  
 [Yansıması](../../framework/reflection-and-codedom/reflection.md)   
 Bir derleme hakkında bilgi almak için **yansıma** sınıfının nasıl kullanılacağını açıklar.
