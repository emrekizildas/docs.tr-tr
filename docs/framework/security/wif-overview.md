---
title: Windows Identity Foundation 4.5’e Genel Bakış
ms.date: 03/30/2017
ms.assetid: 5f723345-7270-49e2-b638-b3a34bd40517
author: BrucePerlerMS
ms.openlocfilehash: c9420ce641da32edc6196be0743d967446a14947
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045000"
---
# <a name="windows-identity-foundation-45-overview"></a>Windows Identity Foundation 4.5’e Genel Bakış
Windows Identity Foundation 4.5, uygulamalarınızda beyana dayalı kimlik uygulamak için kullanılan bir .NET Framework sınıf kümesidir. Bunu kullanarak, talep kullanan uygulama ve hizmetlerin avantajlarından daha kolay bir şekilde yararlanabilirsiniz. WIF 4.5, .NET Framework 4.5 veya sonraki sürümlerini kullanan herhangi bir Web uygulamasında veya Web hizmetinde kullanılabilir. WIF, Microsoft'un açık standartları temel alan ortak sektör vizyonunu uygulayan Federal Kimlik yazılım ailesinin bir parçasıdır. Federal Kimlik üç bileşenden oluşur: [Active Directory® Federasyon Hizmetleri](https://go.microsoft.com/fwlink/?LinkID=247516) (AD FS) 2,0, [Windows Azure Access Control Hizmetleri](https://go.microsoft.com/fwlink/?LinkID=247517) (ACS) ve WIF. Bu üç bileşen birlikte Microsoft'un yeni beyana dayalı bulut kimliği ve erişim platformunun merkezini oluşturur.  
  
 WıF hakkında daha fazla bilgi için MSDN 'deki güvenlik Geliştirici Merkezi ' nde [Windows Identity Foundation Web sitesine](https://go.microsoft.com/fwlink/?LinkId=149009) bakın. WıF kullanarak uygulamalar oluşturmaya giriş için, bkz. Vittorio Bertoccı ile [programlama Windows Identity Foundation](https://www.microsoftpressstore.com/store/programming-windows-identity-foundation-9780735627185) (Microsoft Press tarafından yayımlandı).  
  
## <a name="wif-45-features"></a>WIF 4.5 Özellikleri  
 WIF 4.5, kimlik kullanan uygulamalar oluşturmak için kullanılan bir çerçevedir. Çerçeve, WS-Güven ve WS-Federasyon protokollerini özetler ve geliştiricilere talep kullanan uygulamalar ve gerekirse güvenlik belirteci hizmetleri (STS) oluşturmak için API'ler sunar. Uygulamalar AD FS ve ACS gibi STS'lerden verilen belirteçleri işlemek için WIF'yi kullanabilir ve web uygulamasında veya web hizmetinde kimlik tabanlı kararlar verebilir.  
  
 WIF 4.5 aşağıdaki önemli özelliklere sahiptir:  
  
- Talep kullanan uygulamalar oluşturma (bağlı taraf uygulamaları). WIF geliştiricilerin talep kullanan uygulamalar oluşturmasına yardımcı olur. Uygulama geliştiricilerine talep modelinin yanı sıra, talepleri temel alan kullanıcı erişimi kararlarının verilmesine yardımcı olan zengin bir API'ler kümesi de sağlar.  WIF geliştiricilere, uygulamalarını ister ASP.NET ister WCF ortamlarında oluşturmayı seçmiş olsunlar, sürekli bir programlama deneyimi de sağlar.  
  
- Talep kullanan uygulamalarda kimlik temsili desteği oluşturma.  WIF, orijinal istek sahiplerinin kimliklerini birden fazla hizmet sınırı arasında koruma özelliği sağlar. Bu özellik, çerçevede "ActAs" ya da "OnBehalfOf" işlevi kullanılarak gerçekleştirilebilir ve geliştiricilere talep kullanan uygulamalarına kimlik temsili desteği ekleme imkanı tanır.  
  
- Özel STS'ler oluşturma.  WIF, WS-Güven protokolünü destekleyen özel STS oluşturulmasını önemli ölçüde daha kolay hale getirir. Böyle bir STS'ye Etkin STS de denir.  
  
     Ayrıca, çerçeve Web tarayıcısı istemcileri sağlamak için WS-Federasyonu destekleyen STS oluşturma desteği de sağlar. Böyle bir STS'ye Edilgen STS de denir.  
  
- Visual Studio 11 için uygulamanızı beyana dayalı kimlik ile güvenli hale getirmenizi ve birden fazla kimlik sağlayıcısından gelen kullanıcıları kabul etmenizi sağlayan yeni kimlik ve erişim aracı. Bu wif aracını şu URL 'den indirebilirsiniz: <https://go.microsoft.com/fwlink/?LinkID=245849> veya doğrudan Extensions Manager 'da "kimlik" araması yaparak doğrudan Visual Studio 11 içinden. Daha fazla bilgi için bkz. [Visual Studio Için kimlik ve erişim aracı 2012](identity-and-access-tool-for-vs.md).  
  
 WIF aşağıdaki ana senaryoları destekler:  
  
- Federasyon.  WIF iki veya daha fazla iş ortağı arasında federasyon oluşturulmasını mümkün kılar. Talep kullanan uygulamalar (RP'ler) ve özel STS'ler oluşturma desteği, geliştiricilerin bu senaryoyu gerçekleştirmelerine yardımcı olur.  
  
- Kimlik Temsili.  WIF, geliştiricilerin kimlik temsili senaryosu geliştirebilmesi için kimliklerin hizmet sınırları arasında korunmasını kolaylaştırır.  
  
- Kimlik Doğrulamayı Yükseltme. Uygulama içindeki farklı kaynaklar için kimlik doğrulama gereksinimleri değişiklik gösterebilir. WIF, geliştiricilere artımlı kimlik doğrulama gereksinimleri gerektiren uygulamalar oluşturma imkanı tanır (örneğin: Kullanıcı Adı/Parola kimlik doğrulaması ile ilk oturum ve ardından Akıllı Kart kimlik doğrulamasına yükseltme).  
  
 WIF kullanarak, beyana dayalı kimlik modelinin avantajlarından daha kolay bir şekilde yararlanabileceksiniz. Daha fazla bilgi için bkz. [geliştiriciler Için Windows Identity Foundation teknik incelemesi](https://download.microsoft.com/download/7/d/0/7d0b5166-6a8a-418a-addd-95ee9b046994/windowsidentityfoundationwhitepaperfordevelopers-rtw.pdf).
