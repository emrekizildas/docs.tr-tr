---
title: WS-* Protocols-WCF geliştiricileri için gRPC
description: WCF tarafından desteklenen WS-* protokollerini ve gRPC ile kullanılabilen alternatifleri gözden geçirme
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: cd9af401fc46297fc0c67f5b3e5d6b34177d6a87
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184031"
---
# <a name="ws--protocols"></a>WS-\* protokoller

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Windows Communication Foundation (WCF) ile çalışmanın gerçek avantajlarından biri, var olan _WS-\*_  standart protokollerin çoğunu destekliyordu. Bu bölüm, GRPC 'nin aynı WS-\* Protocols ' i nasıl yönettiğini kısaca kapsar ve alternatif olmadığında hangi seçeneklerin kullanılabildiğini tartışır.

## <a name="metadata-exchange---ws-policy-ws-discovery-and-so-on"></a>Meta veri değişimi-WS-Policy, WS-Discovery, vb.

SOAP Hizmetleri, veri biçimleri, işlemler veya iletişim seçenekleri gibi bilgilerle Web Hizmetleri Açıklama Dili (WSDL) şema belgelerini kullanıma sunar. Bu şema, istemci kodunu oluşturmak için kullanılabilir.

GRPC, sunucular ve istemciler aynı `.proto` dosyalardan oluşturulduğunda en iyi şekilde çalışır, ancak sunucu yansıması isteğe bağlı uzantısı, çalışan bir sunucudan dinamik bilgileri açığa çıkarmak için bir yol sağlar. Daha fazla bilgi için bkz. [GRPC. Reflection](https://nuget.org/packages/Grpc.Reflection) NuGet paketi ve [GRPC C# sunucusu yansıma](https://github.com/grpc/grpc/blob/master/doc/csharp/server_reflection.md) makalesi.

WS-Discovery protokolü, yerel bir ağdaki hizmetleri bulmak için kullanılır. gRPC Hizmetleri genellikle DNS veya Tüketil veya ZooKeeper gibi bir hizmet kayıt defteri kullanılarak bulunur.

## <a name="security--ws-security-ws-federation-xml-encryption-and-so-on"></a>Güvenlik – WS-Security, WS-Federation, XML şifrelemesi, vb.

Güvenlik, kimlik doğrulaması ve yetkilendirme, [Bölüm 6](security.md)' da çok daha ayrıntılı olarak ele alınmıştır. Ancak, WCF 'nin aksine gRPC WS-Security, WS Federasyonu veya XML şifrelemesini desteklemediğinden buraya dikkat edin. Bu nedenle, gRPC harika güvenlik sağlar; TLS üzerinden HTTP/2 kullanılırken tüm gRPC ağ trafiği otomatik olarak şifrelenir ve karşılıklı istemci/sunucu kimlik doğrulaması için x509 sertifikaları kullanılabilir.

## <a name="ws-reliablemessaging"></a>WS-ReliableMessaging

gRPC, WS-ReliableMessaging ' e eşdeğer değildir. Yeniden deneme semantiği, muhtemelen [Polly](https://github.com/App-vNext/Polly)gibi bir kitaplıkla birlikte kodda işlenmelidir. Kubernetes veya benzer düzenleme ortamlarında çalışırken [hizmet kafesleri](service-mesh.md) , hizmetler arasında güvenilir mesajlaşma sağlamaya da yardımcı olabilir.

## <a name="ws-transaction-ws-coordination"></a>WS-Işlem, WS koordinasyonu

WCF 'nin dağıtılmış işlem uygulamaları Windows ' Microsoft Dağıtılmış İşlem Düzenleyicisi veya MSDTC kullanır. Bu, SQL Server, MSMQ veya Windows dosya sistemleri gibi, özellikle destekleyen kaynak yöneticileriyle birlikte kullanılabilir. Modern mikro hizmetler dünyasında, kullanımda olan daha geniş teknoloji yelpazesi nedeniyle, henüz eşdeğer değildir. İşlem tartışması için bkz. [ek a](appendix.md).

>[!div class="step-by-step"]
>[Önceki](error-handling.md)
>[İleri](migrate-wcf-to-grpc.md)
