---
title: Desteklenen dağıtım senaryoları - WCF
ms.date: 03/30/2017
ms.assetid: 3399f208-3504-4c70-a22e-a7c02a8b94a6
ms.openlocfilehash: 2da55176cbfe618b332f2df210e3e1c0516b17ae
ms.sourcegitcommit: a8d3504f0eae1a40bda2b06bd441ba01f1631ef0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67170045"
---
# <a name="supported-deployment-scenarios"></a>Desteklenen dağıtım senaryoları

Kısmen güvenilir uygulamaların kullanım için desteklenen Windows Communication Foundation (WCF) özellikleri alt kümesi için WCF kullanan bazı, tümü değil, senaryolar gereksinimlerini karşılamak üzere tasarlanmıştır. Sunucuda, WCF Internet ölçeğinde ASP.NET 2.0 Medium Trust izin üçüncü taraf uygulamaları çalıştıran paylaşılan barındırma sağlayıcılarının güvenlik nedeniyle ayarlanmış gereksinimlerini karşılar. İstemcide, WCF kısmi güven desteği gibi dağıtım teknolojileri gereksinimlerini karşılamak için tasarlanan [ClickOnce dağıtımı](/visualstudio/deployment/clickonce-security-and-deployment) veya WPF'nin XAML tarayıcı uygulaması teknoloji, sorunsuz ve güvenli dağıtımına izin ver güvenilmeyen siteleri Masaüstü uygulamaları.

## <a name="minimum-permission-requirements"></a>En düşük izin gereksinimleri

WCF ya da aşağıdaki standart adlandırılmış izin kümelerinin altında çalışan uygulamalar, özelliklerin bir alt kümesini destekler:

- Orta güven izinleri

- Internet bölgesi izinleri

Kısmen güvenilir uygulamaların daha kısıtlayıcı izinlerle WCF kullanma girişimi çalışma zamanında güvenlik özel durumları neden olabilir.

Bu izin kümeleri, desteklenen özellikler hakkında daha fazla bilgi için bkz: [kısmi güven özelliği uyumluluğu](partial-trust-feature-compatibility.md).

## <a name="partial-trust-on-the-server"></a>Sunucu üzerinde kısmi güven

Birçok ticari sağlayıcılarının barındırma hizmetleri, ASP.NET Web uygulamasının kendi sunucuları üzerinde çalışan uygulamalar ASP.NET 2.0 Medium Trust izin kümesinde çalıştırma zorunlu kılabilir. WCF hizmetleri, bu ortamlarda çalıştırabilirsiniz, kullandıkları sağlanan <xref:System.ServiceModel.BasicHttpBinding>, <xref:System.ServiceModel.WebHttpBinding>, veya <xref:System.ServiceModel.WSHttpBinding> aktarım düzeyi güvenlik ile.

WCF hizmetlerini barındırma ortamları Medium Trust ile çalışan istemci isteklerine yanıt diğer sunuculara yönelik iletiler göndererek orta katman hizmet olarak da işlev görebilir. Uygulama barındırma ortamı uygun izni vermiştir, orta katman senaryoları sunucuda desteklenir <xref:System.Net.WebPermission> istedikleri sunucuya giden isteklerde.

Desteklenen SOAP bağlamaları birini kullanarak SOAP ileti ek olarak, WCF destekler <xref:System.ServiceModel.WebHttpBinding> kısmen güvenilir uygulamaların stili Web hizmetleri oluşturmak için. [WCF Web HTTP programlama modeli](wcf-web-http-programming-model.md), [WCF dağıtımı](wcf-syndication.md), ve [AJAX tümleştirme ve JSON desteği](ajax-integration-and-json-support.md) WCF özelliklerinin tümü desteklenir kısmi güven.

İş akışı Hizmetleri, tam güven izinleri gerektirir ve kısmen güvenilen uygulamalarda kullanılamaz.

Daha fazla bilgi için [nasıl yapılır: Orta güven ASP.NET 2.0 kullanan](https://go.microsoft.com/fwlink/?LinkId=84603).

## <a name="partial-trust-on-the-client"></a>İstemci üzerinde kısmi güven

Belirli güvenlik önlemleri indiriliyor ve güvenilmeyen Internet siteleriyle kod çalıştırırken alınması gerekir. Her ikisi de [ClickOnce dağıtımı](/visualstudio/deployment/clickonce-security-and-deployment) ve WPF'nin XAML tarayıcı uygulaması (XBAP) teknolojisi olun kısmi güven güvenilmeyen kod (Internet bölgesi) sınırlı izinler vermek için kullanın.

WCF tarafından dağıtılan kısmen güvenilir uygulamaların içinde uzak sunuculardan ile iletişim kurmak için kullanılabilir [ClickOnce dağıtımı](/visualstudio/deployment/clickonce-security-and-deployment) veya XBAP. Internet bölgesi izin kümesi içeren <xref:System.Net.WebPermission> kaynak konağını sağlayan açıklanan desteklenen WCF bağlamaları birini kullanarak, kaynak sunucu ile iletişim kurmak bu uygulamaları [kısmi güven özelliği uyumluluğu ](partial-trust-feature-compatibility.md).

## <a name="see-also"></a>Ayrıca bkz.

- [Kod erişimi güvenliği](../../misc/code-access-security.md)
- [Windows Presentation Foundation tarayıcıda tutulan uygulamalar genel bakış](../../wpf/app-development/wpf-xaml-browser-applications-overview.md)
- [Kısmi Güven](partial-trust.md)
- [ASP.NET güven düzeylerini ve ilke dosyaları](https://docs.microsoft.com/previous-versions/wyts434y(v=vs.140))
