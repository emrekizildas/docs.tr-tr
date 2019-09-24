---
title: WCF geliştiricileri için GRPC neden önerilir
description: GRPC 'nin neden modern mimarilere ve platformlara geçiş yapmak isteyen WCF geliştiricileri için iyi bir uyum olduğuna ilişkin bir tartışma.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 7e80936eb36bbba92958c349b5f1c0cb389d6b8d
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184038"
---
# <a name="why-grpc-is-recommended-for-wcf-developers"></a><span data-ttu-id="5dae5-103">WCF geliştiricileri için neden gRPC önerilir?</span><span class="sxs-lookup"><span data-stu-id="5dae5-103">Why gRPC is recommended for WCF developers</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="5dae5-104">GRPC 'nin diline ve tekniklerine ek olarak, gRPC 'nin .NET Core 'a geçiş yapmak isteyen WCF geliştiricilerine yönelik doğru çözüm olmasının yanı sıra, kullanılabilir alternatifler vardır.</span><span class="sxs-lookup"><span data-stu-id="5dae5-104">Before diving deeply into the language and techniques of gRPC, it's worth discussing why gRPC is the right solution for WCF developers who want to migrate to .NET Core, given there are alternatives available.</span></span>

## <a name="similarity-to-wcf"></a><span data-ttu-id="5dae5-105">WCF benzerliği</span><span class="sxs-lookup"><span data-stu-id="5dae5-105">Similarity to WCF</span></span>

<span data-ttu-id="5dae5-106">Uygulama ve yaklaşım farklı olsa da, gRPC ile hizmetleri geliştirme ve kullanma konusunda gerçek deneyim, WCF geliştiricileri için çok sezgisel olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5dae5-106">Although its implementation and approach is different, the actual experience of developing and consuming services with gRPC should be very intuitive for WCF developers.</span></span> <span data-ttu-id="5dae5-107">İstemci ve sunucu aynı platformda olsa da, ağ iletişimi konusunda endişelenmenize gerek kalmadan, kodunuzun temel amacı aynı.</span><span class="sxs-lookup"><span data-stu-id="5dae5-107">The underlying goal of making it possible to code as though the client and server were on the same platform, without needing to worry about networking, is the same.</span></span> <span data-ttu-id="5dae5-108">Her iki platform da, bu arabirimi bildirme işlemi farklı olsa da, bir arabirimi oluşturma ve uygulama ilkesini paylaşır.</span><span class="sxs-lookup"><span data-stu-id="5dae5-108">Both platforms share the principle of declaring and then implementing an interface, even though the process for declaring that interface is different.</span></span> <span data-ttu-id="5dae5-109">Ayrıca, Bölüm 5 ' te gösterildiği gibi, gRPC eşlemesi tarafından desteklenen farklı RPC çağrısı türleri, WCF Hizmetleri için kullanılabilen farklı bağlamalara çok uygundur.</span><span class="sxs-lookup"><span data-stu-id="5dae5-109">And as you'll see in chapter 5, the different types of RPC calls supported by gRPC map very well to the different bindings available to WCF services.</span></span>

## <a name="benefits-of-grpc"></a><span data-ttu-id="5dae5-110">GRPC 'nin avantajları</span><span class="sxs-lookup"><span data-stu-id="5dae5-110">Benefits of gRPC</span></span>

<span data-ttu-id="5dae5-111">Aşağıda, gRPC 'nin diğer çözümlerin üzerinde neden olduğu ek nedenler:</span><span class="sxs-lookup"><span data-stu-id="5dae5-111">Additional reasons why gRPC stands above other solutions are:</span></span>

### <a name="performance"></a><span data-ttu-id="5dae5-112">Performans</span><span class="sxs-lookup"><span data-stu-id="5dae5-112">Performance</span></span>

<span data-ttu-id="5dae5-113">Daha önce anlatıldığı gibi http/1.1 yerine HTTP/2 kullanılması, insan tarafından okunabilen iletiler gereksinimini ortadan kaldırır ve bunun yerine daha hızlı bir ikili protokolü kullanır.</span><span class="sxs-lookup"><span data-stu-id="5dae5-113">As already discussed, using HTTP/2 rather than HTTP/1.1 removes the requirement for human-readable messages and instead uses the smaller faster binary protocol.</span></span> <span data-ttu-id="5dae5-114">Bu, bilgisayarların ayrıştırılmasında daha etkilidir.</span><span class="sxs-lookup"><span data-stu-id="5dae5-114">This is more efficient for computers to parse.</span></span> <span data-ttu-id="5dae5-115">HTTP/2 Ayrıca, bir kuyrukta beklenmeden (HTTP/1.1 'de "satır başı (HOL) engelleme" olarak bilinen bir sorun olması gerekmeden), yanıtları tek bir bağlantı üzerinden aynı anda göndermek için de destekler.</span><span class="sxs-lookup"><span data-stu-id="5dae5-115">HTTP/2 also supports multiplexing requests over a single connection enabling responses to be sent as soon as they're ready without the need to wait in a queue (an issue in HTTP/1.1 known as "head-of-line (HOL) blocking").</span></span> <span data-ttu-id="5dae5-116">GRPC kullanılırken daha az kaynak olması gerekir ve bu, mobil cihazlarda ve yavaş ağlarda kullanılması iyi bir çözüm haline gelir.</span><span class="sxs-lookup"><span data-stu-id="5dae5-116">Fewer resources are needed when using gRPC, which makes it a good solution to use for mobile devices and over slower networks.</span></span>

### <a name="interoperability"></a><span data-ttu-id="5dae5-117">Birlikte Çalışabilirlik</span><span class="sxs-lookup"><span data-stu-id="5dae5-117">Interoperability</span></span>

<span data-ttu-id="5dae5-118">.NET, Java, Python, Go, C++, Node. js, Swift, Dart, Ruby ve php dahil tüm büyük programlama dilleri ve platformları Için GRPC araçları ve kitaplıkları vardır.</span><span class="sxs-lookup"><span data-stu-id="5dae5-118">There are gRPC tools and libraries for all major programming languages and platforms, including .NET, Java, Python, Go, C++, Node.js, Swift, Dart, Ruby, and PHP.</span></span> <span data-ttu-id="5dae5-119">Her platform için protokol arabelleklerinin ikili kablo biçimi ve verimli kod üretimi sayesinde, geliştiriciler, tam platformlar arası destekten hala keyif alırken performanslı uygulamalar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="5dae5-119">Thanks to the Protocol Buffers binary wire format and the efficient code generation for each platform, developers can build performant apps while still enjoying full cross-platform support.</span></span>

### <a name="usability-and-productivity"></a><span data-ttu-id="5dae5-120">Kullanılabilirlik ve üretkenlik</span><span class="sxs-lookup"><span data-stu-id="5dae5-120">Usability and productivity</span></span>

<span data-ttu-id="5dae5-121">gRPC, kapsamlı bir RPC çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="5dae5-121">gRPC is a comprehensive RPC solution.</span></span> <span data-ttu-id="5dae5-122">Düzenli olarak birden çok dilde ve platformda çalışır ve gerekli ortak kod kodu otomatik olarak üretilmeden harika araçlar sağlar, böylece iş mantığına odaklanmak için daha fazla geliştirici saati serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="5dae5-122">It works consistently across multiple languages and platforms, and provides excellent tooling, with much of the necessary boilerplate code auto-generated, so more developer time is freed up to focus on business logic.</span></span>

### <a name="streaming"></a><span data-ttu-id="5dae5-123">Akış</span><span class="sxs-lookup"><span data-stu-id="5dae5-123">Streaming</span></span>

<span data-ttu-id="5dae5-124">gRPC 'de, WCF 'nin tam çift yönlü hizmetlerine çok benzer işlevler sağlayan tam çift yönlü akış vardır.</span><span class="sxs-lookup"><span data-stu-id="5dae5-124">gRPC has full bidirectional streaming, which provides very similar functionality to WCF's full duplex services.</span></span> <span data-ttu-id="5dae5-125">gRPC akışı, normal internet bağlantıları, yük dengeleyiciler ve hizmet kafesleri üzerinden çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="5dae5-125">gRPC streaming can operate over regular internet connections, load balancers, and service meshes.</span></span>

### <a name="deadlinetimeouts-and-cancellation"></a><span data-ttu-id="5dae5-126">Son tarih/zaman aşımları ve iptal</span><span class="sxs-lookup"><span data-stu-id="5dae5-126">Deadline/timeouts and cancellation</span></span>

<span data-ttu-id="5dae5-127">gRPC, istemcilerin bir RPC 'nin tamamlaması için en uzun süreyi belirtmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="5dae5-127">gRPC allows clients to specify a maximum time for an RPC to complete.</span></span> <span data-ttu-id="5dae5-128">Belirtilen son tarih aşılırsa sunucu, işlemi istemciden bağımsız olarak iptal edebilir.</span><span class="sxs-lookup"><span data-stu-id="5dae5-128">If the specified deadline is exceeded the server can cancel the operation independently of the client.</span></span> <span data-ttu-id="5dae5-129">Son tarihler ve iptaller, kaynak kullanım sınırlarını zorlamaya yardımcı olmak için ek gRPC çağrıları aracılığıyla yayılamaz.</span><span class="sxs-lookup"><span data-stu-id="5dae5-129">Deadlines and cancellations can be propagated through further gRPC calls to help enforce resource usage limits.</span></span> <span data-ttu-id="5dae5-130">İstemciler, son tarih aşıldığında veya daha önce (örn. Kullanıcı etkileşimi nedeniyle) işlemleri iptal edebilir.</span><span class="sxs-lookup"><span data-stu-id="5dae5-130">Clients may also abort operations when a deadline is exceeded, or earlier if necessary (e.g. due to a user interaction).</span></span>

### <a name="security"></a><span data-ttu-id="5dae5-131">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="5dae5-131">Security</span></span>

<span data-ttu-id="5dae5-132">bir TLS uçtan uca şifreli bağlantı üzerinden HTTP/2 kullanılırken gRPC, örtülü olarak güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="5dae5-132">gRPC is implicitly secure when using HTTP/2 over an TLS end-to-end encrypted connection.</span></span> <span data-ttu-id="5dae5-133">Istemci sertifikası kimlik doğrulaması desteği (bkz. Bölüm 6) istemci ve sunucu arasındaki güvenliği ve güveni daha da artırır.</span><span class="sxs-lookup"><span data-stu-id="5dae5-133">Support for Client Certificate authentication (see chapter 6) further increases security and trust between client and server.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="5dae5-134">[Önceki](network-protocols.md)
>[İleri](protocol-buffers.md)</span><span class="sxs-lookup"><span data-stu-id="5dae5-134">[Previous](network-protocols.md)
[Next](protocol-buffers.md)</span></span>