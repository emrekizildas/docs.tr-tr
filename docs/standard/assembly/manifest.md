---
title: Derleme bildirimi
ms.date: 08/20/2019
helpviewer_keywords:
- assembly manifest
- dynamic assemblies, assembly manifest
- metadata, assembly manifest
- culture, assembly manifest
- assemblies [.NET Framework], metadata
ms.assetid: 8e40fab9-549d-4731-aec2-ffa47a382de0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 053726b200b73956099ff9274cc8f63f21d8fc64
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70973175"
---
# <a name="assembly-manifest"></a>Derleme bildirimi
Statik veya dinamik tüm derlemeler, derleme içindeki öğelerin birbirleriyle nasıl ilişkili olduğunu açıklayan bir veri koleksiyonu içerir. Derleme bildirimi, bu derleme metaverilerini içerir. Bir derleme bildirimi, derlemenin sürüm gereksinimlerini ve güvenlik kimliğini belirtmek, derlemenin kapsamını tanımlamak ve kaynaklara, sınıflara yapılan atıfları çözmek için gereken tüm metaverileri içerir. Derleme bildirimi, Microsoft ara dili (MSIL) koduna sahip bir PE dosyasında ( *. exe* veya *. dll*) ya da yalnızca derleme bildirimi bilgilerini IÇEREN tek başına bir pe dosyasında depolanabilir.  
  
 Aşağıdaki görselde, bildirimin saklanabileceği farklı şekilleri gösterilmektedir.  
  
 ![Tek dosyalı derleme ve çok dosyalı derleme yapılandırmasındaki bildirimi gösteren diyagram.](./media/manifest/assembly-types-diagram.gif)  
  
 İlişkili tek bir dosyaya sahip bir derlemede, tek dosyalı derleme oluşturmak amacıyla bildirim PE dosyasına eklenir. Bağımsız bir bildirim dosyasına veya bildirim derlemesindeki PE dosyalarından birine ekli şekilde bir çoklu dosya derlemesi oluşturabilirsiniz.  
  
 Her derlemenin bildirimi, aşağıdaki işlevleri gerçekleştirir:  
  
- Derlemeyi oluşturan dosyaları listeler.  
  
- Derlemenin türlerine ve kaynaklarına yapılan atıfların, tanımlarını ve uygulamalarını içeren dosyalarla nasıl eşleştirildiğini yönetir.  
  
- Derlemenin bağımlı olduğu diğer derlemeleri listeler.  
  
- Derlemenin tüketicileri ve derlemenin uygulama ayrıntıları arasında bir yöneltme düzeyi sağlar.  
  
- Derlemeyi kendini açıklayan hale getirir.  
  
## <a name="assembly-manifest-contents"></a>Bütünleştirilmiş kod bildirim içerikleri  
 Aşağıdaki tabloda, derleme bildiriminde bulunan bilgiler gösterilmektedir. İlk dört öğe: derleme adı, sürüm numarası, kültür ve tanımlayıcı ad bilgileri derlemenin kimliğini yapar.  
  
|Bilgiler|Açıklama|  
|-----------------|-----------------|  
|Bütünleştirilmiş kod adı|Derlemenin adını belirten bir metin dizesi.|  
|Sürüm numarası|Bir ana ve alt sürüm numarası ve bir düzeltme ve yapı numarası. Ortak dil çalışma zamanı sürüm ilkesini uygulamak için bu numaraları kullanır.|  
|Kültür|Derlemenin desteklediği kültür veya dil hakkında bilgi. Bu bilgiler, yalnızca bir derlemeyi kültüre veya dile özel bilgi içeren bir uydu derleme olarak tanımlamak için kullanılmalıdır. (Kültür bilgisine sahip bir derleme, otomatik olarak bir uydu derleme kabul edilir.)|  
|Tanımlayıcı ad bilgisi|Derlemeye tanımlayıcı ad verilmişse yayımcıdan gelen ortak anahtar.|  
|Derlemedeki tüm dosyaların listesi|Derlemede bulunan her dosyayla bir dosya adının karması. Derlemeyi oluşturan tüm dosyaların, derleme bildirimini içeren dosyayla aynı dizinde olması gerektiğine dikkat edin.|  
|Tür başvuru bilgisi|Çalışma zamanı tarafından bir tür başvurusu ile bildirimini ve uygulamasını içeren dosyanın eşleştirilmesi için kullanılan bilgiler. Bu, derlemeden dışarı aktarılan türler için kullanılır.|  
|Atıfta bulunulan derlemeler hakkında bilgi|Derleme tarafından statik olarak atıfta bulunulan diğer derlemelerin listesi. Her başvuru, bağımlı derlemenin adını, derleme metaverilerini (sürüm, kültür, işletim sistemi vb.) ve, derleme tanımlayıcı ada sahipse, ortak anahtarı içerir.|  
  
 Kodunuzda derleme öznitelikleri kullanarak derleme bildirimine bazı bilgiler ekleyebilir veya bazı bilgileri değiştirebilirsiniz. Ticari Marka, Telif Hakkı, Ürün, Şirket ve Bilgilendirme Sürümü dahil olmak üzere sürüm bilgilerini ve bilgilendirme özniteliklerini değiştirebilirsiniz. Derleme özniteliklerinin tüm listesi için bkz. [derleme özniteliklerini ayarlama](set-attributes.md).  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Bütünleştirilmiş kod içeriği](contents.md)
- [Derleme sürümü oluşturma](versioning.md)
- [Uydu derlemeleri oluşturma](../../framework/resources/creating-satellite-assemblies-for-desktop-apps.md)
- [Tanımlayıcı adlı derlemeler](strong-named.md)
