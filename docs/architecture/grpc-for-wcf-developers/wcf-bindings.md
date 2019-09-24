---
title: WCF bağlamaları ve aktarımları-WCF geliştiricileri için gRPC
description: Farklı WCF bağlamalarının ve aktarımların gRPC ile nasıl karşılaştırılacağını öğrenin.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 50bac73ee68d7156fc5fed55dfffb3ba7f2de924
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184059"
---
# <a name="wcf-bindings-and-transports"></a><span data-ttu-id="5c894-103">WCF bağlamaları ve aktarımları</span><span class="sxs-lookup"><span data-stu-id="5c894-103">WCF bindings and transports</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="5c894-104">WCF, farklı ağ protokolleri, hat biçimleri ve diğer uygulama ayrıntılarını belirten birçok farklı yerleşik *bağlamaları* vardır.</span><span class="sxs-lookup"><span data-stu-id="5c894-104">WCF has lots of different built-in *bindings* that specify different network protocols, wire formats, and other implementation details.</span></span> <span data-ttu-id="5c894-105">gRPC, tek bir ağ protokolüne ve tek bir hat biçimine sahiptir (Teknik olarak Tel biçimlendirme özelleştirilebilir ancak bu kitabın kapsamına göre daha fazla *olabilir* ).</span><span class="sxs-lookup"><span data-stu-id="5c894-105">gRPC effectively has just one network protocol and one wire format (technically the wire format *may* be customized, but that is beyond the scope of this book).</span></span> <span data-ttu-id="5c894-106">GRPC 'nin çoğu durumda en iyi çözümü sunduğunu keşfedersiniz.</span><span class="sxs-lookup"><span data-stu-id="5c894-106">You are likely to discover that gRPC offers the best solution in most cases.</span></span> <span data-ttu-id="5c894-107">Aşağıda, en ilgili WCF bağlamaları ve gRPC 'deki eşdeğer değerleriyle nasıl Karşılaştırıldığı hakkında kısa bir tartışma verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5c894-107">What follows is a short discussion about the most relevant WCF bindings and how they compare to their equivalent in gRPC.</span></span>

## <a name="nettcp"></a><span data-ttu-id="5c894-108">NetTCP</span><span class="sxs-lookup"><span data-stu-id="5c894-108">NetTCP</span></span>

<span data-ttu-id="5c894-109">WCF 'nin NetTCP bağlaması kalıcı bağlantılar, küçük mesajlar ve iki yönlü mesajlaşma sağlar ancak yalnızca .NET istemcileri ve sunucuları arasında çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5c894-109">WCF's NetTCP binding allows for persistent connections, small messages, and two-way messaging but only works between .NET clients and servers.</span></span> <span data-ttu-id="5c894-110">gRPC aynı işlevselliğe izin verir ancak birden çok programlama dilinde ve platformunda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="5c894-110">gRPC allows the same functionality but is supported across multiple programming languages and platforms.</span></span> <span data-ttu-id="5c894-111">gRPC, her zaman aynı şekilde uygulanmasa da, WCF NetTCP bağlamasının birçok özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5c894-111">gRPC has many of the features of WCF NetTCP binding, although not always implemented in the same way.</span></span> <span data-ttu-id="5c894-112">Örneğin, WCF 'de şifreleme yapılandırma ile denetlenir ve çerçevede işlenir.</span><span class="sxs-lookup"><span data-stu-id="5c894-112">For example, in WCF, encryption is controlled through configuration and handled in the framework.</span></span> <span data-ttu-id="5c894-113">GRPC 'de şifreleme, TLS üzerinden HTTP/2 kullanılarak bağlantı düzeyinde elde edilir.</span><span class="sxs-lookup"><span data-stu-id="5c894-113">In gRPC, encryption is achieved at the connection level using HTTP/2 over TLS.</span></span>

## <a name="http"></a><span data-ttu-id="5c894-114">HTTP</span><span class="sxs-lookup"><span data-stu-id="5c894-114">HTTP</span></span>

<span data-ttu-id="5c894-115">WCF BasicHttpBinding genellikle metin tabanlıdır, hatta SOAP biçimi olarak SOAP kullanarak ve modern ağa bağlı uygulamaların standartları tarafından çok yavaştır.</span><span class="sxs-lookup"><span data-stu-id="5c894-115">WCF's BasicHttpBinding is generally text based, using SOAP as the wire format, and is very slow by the standards of modern networked applications.</span></span> <span data-ttu-id="5c894-116">Yalnızca, platformlar arası birlikte çalışabilirlik veya internet altyapısı üzerinden bağlantı sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5c894-116">It's only really used to provide cross-platform interoperability, or connection over internet infrastructure.</span></span> <span data-ttu-id="5c894-117">GRPC 'nin eşdeğeri; HTTP/2 ' de iletiler için ikili Protohat Tel biçimi ile temel alınan aktarım katmanı olarak HTTP/2 kullandığından, tüm modern programlama dilleri ile tam platformlar arası birlikte çalışabilirlik olanağı sunabilir ve çerçeveleri.</span><span class="sxs-lookup"><span data-stu-id="5c894-117">The equivalent in gRPC—because it uses HTTP/2 as the underlying transport layer with the binary Protobuf wire format for messages—can offer NetTCP service level performance but with full cross-platform interoperability with all modern programming languages and frameworks.</span></span>

## <a name="named-pipes"></a><span data-ttu-id="5c894-118">Adlandırılmış Kanallar</span><span class="sxs-lookup"><span data-stu-id="5c894-118">Named Pipes</span></span>

<span data-ttu-id="5c894-119">WCF, aynı fiziksel makinedeki süreçler arasındaki iletişim için adlandırılmış bir kanallar bağlaması sağladı.</span><span class="sxs-lookup"><span data-stu-id="5c894-119">WCF provided a Named Pipes binding for communication between processes on the same physical machine.</span></span> <span data-ttu-id="5c894-120">Adlandırılmış kanallar ASP.NET Core gRPC 'nin ilk sürümü tarafından desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="5c894-120">Named Pipes are not supported by the first release of ASP.NET Core gRPC.</span></span>

<span data-ttu-id="5c894-121">Windows dışında, adlandırılmış kanallar tarafından sunulan işlevsellik bunun yerine genellikle UNIX etki alanı yuvaları tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="5c894-121">Outside Windows, the functionality provided by Named Pipes is instead generally provided by Unix Domain Sockets.</span></span> <span data-ttu-id="5c894-122">Bu yuvalar `/var/run/docker.sock`, sistem ve sunucu olarak hangi GRPC ile çalışabileceği gibi, dosya sistemi adresleriyle temsil edilen normal TCP benzeri yuvalardır.</span><span class="sxs-lookup"><span data-stu-id="5c894-122">These sockets are regular TCP-like sockets represented with file-system addresses, such as `/var/run/docker.sock`, which gRPC can work with as both client and server.</span></span> <span data-ttu-id="5c894-123">Windows üzerinde adlandırılmış kanallar stili işlevini kullanmanız gerekiyorsa, Windows 10 ve Windows Server 'da bir sonraki güncelleştirme olan 2019 S4 içinde, etki alanı yuvalarını Windows içinde tam olarak desteklenen bir yerel özellik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="5c894-123">If you need to use Named Pipes style functionality on Windows, the next update to Windows 10 and Windows Server, in 2019 Q4, adds Domain Sockets as a fully supported native feature within Windows.</span></span> <span data-ttu-id="5c894-124">Bu nedenle, Windows 'un bu ve sonraki sürümlerinde (veya Linux 'ta) çalışan gRPC Hizmetleri, adlandırılmış kanallar yerine etki alanı yuvaları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="5c894-124">So, gRPC services running on these and later versions of Windows (or on Linux) can use Domain Sockets instead of Named Pipes.</span></span> <span data-ttu-id="5c894-125">Ancak ekibiniz en son Windows sürümüne güncelleştiregerekmiyorsa, localhost TCP yuvalarını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c894-125">However, if your team is unable to update to the latest version of Windows, then you'll need to use localhost TCP sockets.</span></span> <span data-ttu-id="5c894-126">Yerel TCP yuvalarını kullanmayla ilgili güvenlik sorunları, istemci ve sunucu arasında sertifika kimlik doğrulamasının kullanılmasıyla ele alınabilir.</span><span class="sxs-lookup"><span data-stu-id="5c894-126">Security concerns about using local TCP sockets can be addressed with the use of certificate authentication between client and server.</span></span>

## <a name="msmq"></a><span data-ttu-id="5c894-127">MSMQ</span><span class="sxs-lookup"><span data-stu-id="5c894-127">MSMQ</span></span>

<span data-ttu-id="5c894-128">MSMQ, özel bir Windows ileti kuyruğu.</span><span class="sxs-lookup"><span data-stu-id="5c894-128">MSMQ is a proprietary Windows message queue.</span></span> <span data-ttu-id="5c894-129">WCF 'nin MSMQ 'ya bağlanması, gelecekte herhangi bir zamanda işlenebilecek istemcilerden gelen istekleri "yangın ve unutmaları" sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c894-129">WCF's binding to MSMQ enables "fire and forget" requests from clients that may be processed at any time in the future.</span></span> <span data-ttu-id="5c894-130">gRPC hiçbir ileti kuyruğu işlevini yerel olarak sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="5c894-130">gRPC doesn't natively provide any message queue functionality.</span></span> <span data-ttu-id="5c894-131">En iyi alternatif, Azure Service Bus, ırbbitmq veya Kafka gibi bir mesajlaşma sistemini doğrudan kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="5c894-131">The best alternative would be to directly use a messaging system like Azure Service Bus, RabbitMQ, or Kafka.</span></span> <span data-ttu-id="5c894-132">Bu, istemci tarafından doğrudan sıraya ileti yerleştirilerek veya iletileri sıraya alan bir gRPC istemci akış hizmeti ile uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="5c894-132">This could be implemented with the client placing messages directly onto the queue, or a gRPC client streaming service that enqueues the messages.</span></span>

## <a name="webhttpbinding"></a><span data-ttu-id="5c894-133">WebHttpBinding</span><span class="sxs-lookup"><span data-stu-id="5c894-133">WebHttpBinding</span></span>

<span data-ttu-id="5c894-134">`WebGet` Ve`WebInvoke` öznitelikleri ile WebHttpBinding (WCF REST olarak da bilinir), bu, bundan daha az ortak olduğu zaman JSON 'ı tek seferde konuşabilme API 'leri geliştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c894-134">The WebHttpBinding (also known as WCF ReST), with the `WebGet` and `WebInvoke` attributes, enabled you to develop ReSTful APIs that could speak JSON at a time when this was less common than now.</span></span> <span data-ttu-id="5c894-135">Bu nedenle, WCF REST ile oluşturulmuş bir yenilenmiş API 'niz varsa, gRPC 'ye dönüştürmek yerine eşdeğer işlevselliği sağlayacak şekilde onu düzenli bir ASP.NET Core MVC web API uygulamasına geçirmeyi düşünün.</span><span class="sxs-lookup"><span data-stu-id="5c894-135">Therefore, if you have a RESTful API built with WCF REST, consider migrating it to a regular ASP.NET Core MVC Web API application, which would provide equivalent functionality, rather than converting to gRPC.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="5c894-136">[Önceki](wcf-endpoints-grpc-methods.md)
>[İleri](rpc-types.md)</span><span class="sxs-lookup"><span data-stu-id="5c894-136">[Previous](wcf-endpoints-grpc-methods.md)
[Next](rpc-types.md)</span></span>