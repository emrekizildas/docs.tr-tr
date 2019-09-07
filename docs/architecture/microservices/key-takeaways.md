---
title: Anahtar paketleri
description: .NET mikro hizmetleri mimarisinden Kapsayıcılı .NET uygulamaları kılavuzu/e-kitabı için en önemli sorunları hızlı bir şekilde görmek için, bir mikro hizmet mimarisi kullanılırken, avantaj ve dezavantajları, örneğin tasarım için DDD desenlerine göz atın ve geliştirme, dayanıklılık, güvenlik ve düzenleyicilerinin kullanımı.
ms.date: 10/19/2018
ms.openlocfilehash: 3b8b7be9b3903c64221cba7c6abdb1e38f5d944f
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/30/2019
ms.locfileid: "70296027"
---
# <a name="key-takeaways"></a><span data-ttu-id="47eed-103">Anahtar koymalar</span><span class="sxs-lookup"><span data-stu-id="47eed-103">Key Takeaways</span></span>

<span data-ttu-id="47eed-104">Özet ve anahtar, en önemli ekibinizle bu kılavuzdan aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="47eed-104">As a summary and key takeaways, the following are the most important conclusions from this guide.</span></span>

<span data-ttu-id="47eed-105">**Kapsayıcıları kullanmanın avantajları.**</span><span class="sxs-lookup"><span data-stu-id="47eed-105">**Benefits of using containers.**</span></span> <span data-ttu-id="47eed-106">Kapsayıcı tabanlı çözümler, üretim ortamlarındaki başarısız bağımlılıklardan kaynaklanan dağıtım sorunlarını azaltmaya yardımcı olduklarından önemli maliyet tasarrufu sağlar.</span><span class="sxs-lookup"><span data-stu-id="47eed-106">Container-based solutions provide important cost savings because they help reduce deployment problems caused by failing dependencies in production environments.</span></span> <span data-ttu-id="47eed-107">Kapsayıcılar DevOps ve üretim işlemlerini önemli ölçüde geliştirir.</span><span class="sxs-lookup"><span data-stu-id="47eed-107">Containers significantly improve DevOps and production operations.</span></span>

<span data-ttu-id="47eed-108">**Kapsayıcılar ubititous olacaktır.**</span><span class="sxs-lookup"><span data-stu-id="47eed-108">**Containers will be ubiquitous.**</span></span> <span data-ttu-id="47eed-109">Docker tabanlı kapsayıcılar, Microsoft, Amazon AWS, Google ve IBM gibi Windows ve Linux ekosistemlerindeki temel satıcılar tarafından desteklenen sektördeki standart bir standart haline geliyor.</span><span class="sxs-lookup"><span data-stu-id="47eed-109">Docker-based containers are becoming the de facto standard in the industry, supported by key vendors in the Windows and Linux ecosystems, such as Microsoft, Amazon AWS, Google, and IBM.</span></span> <span data-ttu-id="47eed-110">Docker, büyük olasılıkla hem bulutta hem de şirket içi veri merkezlerinde bizde olacak.</span><span class="sxs-lookup"><span data-stu-id="47eed-110">Docker will probably soon be ubiquitous in both the cloud and on-premises datacenters.</span></span>

<span data-ttu-id="47eed-111">**Dağıtım birimi olarak kapsayıcılar.**</span><span class="sxs-lookup"><span data-stu-id="47eed-111">**Containers as a unit of deployment.**</span></span> <span data-ttu-id="47eed-112">Bir Docker kapsayıcısı, herhangi bir sunucu tabanlı uygulama veya hizmet için standart dağıtım birimidir.</span><span class="sxs-lookup"><span data-stu-id="47eed-112">A Docker container is becoming the standard unit of deployment for any server-based application or service.</span></span>

<span data-ttu-id="47eed-113">**Mikro hizmetler.**</span><span class="sxs-lookup"><span data-stu-id="47eed-113">**Microservices.**</span></span> <span data-ttu-id="47eed-114">Mikro hizmetler mimarisi, özerk hizmetler biçimindeki birçok bağımsız alt sistemi temel alan dağıtılmış ve büyük veya karmaşık görev açısından kritik uygulamalar için tercih edilen yaklaşım haline geliyor.</span><span class="sxs-lookup"><span data-stu-id="47eed-114">The microservices architecture is becoming the preferred approach for distributed and large or complex mission-critical applications based on many independent subsystems in the form of autonomous services.</span></span> <span data-ttu-id="47eed-115">Mikro hizmet tabanlı bir mimaride, uygulama geliştirilmiş, test edilmiş, sürümlü, dağıtılan ve bağımsız olarak ölçeklenen bir hizmetler koleksiyonu olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="47eed-115">In a microservice-based architecture, the application is built as a collection of services that are developed, tested, versioned, deployed, and scaled independently.</span></span> <span data-ttu-id="47eed-116">Her hizmet, ilgili tüm otonom veritabanlarını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="47eed-116">Each service can include any related autonomous database.</span></span>

<span data-ttu-id="47eed-117">**Etki alanı odaklı tasarım ve SOA.**</span><span class="sxs-lookup"><span data-stu-id="47eed-117">**Domain-driven design and SOA.**</span></span> <span data-ttu-id="47eed-118">Mikro hizmet mimarisi desenleri, hizmet odaklı mimari (SOA) ve etki alanı denetimli tasarımdan (DDD) türetilir.</span><span class="sxs-lookup"><span data-stu-id="47eed-118">The microservices architecture patterns derive from service-oriented architecture (SOA) and domain-driven design (DDD).</span></span> <span data-ttu-id="47eed-119">Gelişen iş ihtiyaçları ve kuralları olan ortamlar için mikro hizmetler tasarladığınızda ve geliştirirken, DDD yaklaşımlarının ve desenlerinin dikkate alınması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="47eed-119">When you design and develop microservices for environments with evolving business needs and rules, it's important to consider DDD approaches and patterns.</span></span>

<span data-ttu-id="47eed-120">**Mikro hizmet sorunları.**</span><span class="sxs-lookup"><span data-stu-id="47eed-120">**Microservices challenges.**</span></span> <span data-ttu-id="47eed-121">Mikro hizmetler bağımsız dağıtım, güçlü alt sistem sınırları ve teknoloji çeşitlemesi gibi birçok güçlü özellik sunar.</span><span class="sxs-lookup"><span data-stu-id="47eed-121">Microservices offer many powerful capabilities, like independent deployment, strong subsystem boundaries, and technology diversity.</span></span> <span data-ttu-id="47eed-122">Bununla birlikte, parçalanmış ve bağımsız veri modelleri, mikro hizmetler arasındaki dayanıklı iletişim, nihai tutarlılık ve bu işlemin sonucu olan işlemsel karmaşıklık gibi dağıtılmış uygulama geliştirmeyle ilgili birçok yeni zorluk da yükseltir. birden çok mikro hizmetten günlüğe kaydetme ve izleme bilgilerini toplama.</span><span class="sxs-lookup"><span data-stu-id="47eed-122">However, they also raise many new challenges related to distributed application development, such as fragmented and independent data models, resilient communication between microservices, eventual consistency, and operational complexity that results from aggregating logging and monitoring information from multiple microservices.</span></span> <span data-ttu-id="47eed-123">Bu yönleri geleneksel tek parçalı bir uygulamadan çok daha yüksek bir karmaşıklık düzeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="47eed-123">These aspects introduce a much higher complexity level than a traditional monolithic application.</span></span> <span data-ttu-id="47eed-124">Sonuç olarak, mikro hizmet tabanlı uygulamalar için yalnızca belirli senaryolar uygundur.</span><span class="sxs-lookup"><span data-stu-id="47eed-124">As a result, only specific scenarios are suitable for microservice-based applications.</span></span> <span data-ttu-id="47eed-125">Bunlar, birden fazla gelişen alt sistemi olan büyük ve karmaşık uygulamaları içerir.</span><span class="sxs-lookup"><span data-stu-id="47eed-125">These include large and complex applications with multiple evolving subsystems.</span></span> <span data-ttu-id="47eed-126">Bu durumlarda, daha uzun süreli çeviklik ve uygulama Bakımı sağlayacağından daha karmaşık bir yazılım mimarisine yatırım harcamıştır.</span><span class="sxs-lookup"><span data-stu-id="47eed-126">In these cases, it's worth investing in a more complex software architecture, because it will provide better long-term agility and application maintenance.</span></span>

<span data-ttu-id="47eed-127">**Tüm uygulamalar için kapsayıcılar.**</span><span class="sxs-lookup"><span data-stu-id="47eed-127">**Containers for any application.**</span></span> <span data-ttu-id="47eed-128">Kapsayıcılar, mikro hizmetler için uygundur, ancak Windows kapsayıcıları kullanılırken geleneksel .NET Framework temel alan tek parçalı uygulamalar için de kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="47eed-128">Containers are convenient for microservices, but can also be useful for monolithic applications based on the traditional .NET Framework, when using Windows Containers.</span></span> <span data-ttu-id="47eed-129">Birçok dağıtım-üretim sorununu çözme ve son teknoloji geliştirme ve test ortamları sağlama gibi Docker kullanmanın avantajları, birçok farklı uygulama türü için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="47eed-129">The benefits of using Docker, such as solving many deployment-to-production issues and providing state-of-the-art Dev and Test environments, apply to many different types of applications.</span></span>

<span data-ttu-id="47eed-130">**CLı ve IDE.**</span><span class="sxs-lookup"><span data-stu-id="47eed-130">**CLI versus IDE.**</span></span> <span data-ttu-id="47eed-131">Microsoft araçları ile, tercih ettiğiniz yaklaşımı kullanarak Kapsayıcılı .NET uygulamaları geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47eed-131">With Microsoft tools, you can develop containerized .NET applications using your preferred approach.</span></span> <span data-ttu-id="47eed-132">Docker CLı ve Visual Studio Code kullanarak bir CLı ve düzenleyici tabanlı ortamla geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47eed-132">You can develop with a CLI and an editor-based environment by using the Docker CLI and Visual Studio Code.</span></span> <span data-ttu-id="47eed-133">Ya da Visual Studio ile IDE odaklı bir yaklaşım ve çok Kapsayıcılı hata ayıklama gibi Docker için benzersiz özellikleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47eed-133">Or you can use an IDE-focused approach with Visual Studio and its unique features for Docker, such as multi-container debugging.</span></span>

<span data-ttu-id="47eed-134">**Dayanıklı bulut uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="47eed-134">**Resilient cloud applications.**</span></span> <span data-ttu-id="47eed-135">Bulut tabanlı sistemler ve dağıtılmış sistemlerde, genel olarak her zaman kısmi hata riski vardır.</span><span class="sxs-lookup"><span data-stu-id="47eed-135">In cloud-based systems and distributed systems in general, there is always the risk of partial failure.</span></span> <span data-ttu-id="47eed-136">İstemciler ve hizmetler ayrı süreçler (kapsayıcılar) olduğundan, bir hizmet istemcinin isteğine zamanında yanıt veremeyebilir.</span><span class="sxs-lookup"><span data-stu-id="47eed-136">Since clients and services are separate processes (containers), a service might not be able to respond in a timely way to a client’s request.</span></span> <span data-ttu-id="47eed-137">Örneğin, bir hizmet kısmi bir hata veya bakım için kapatılmış olabilir; hizmet aşırı yüklenmiş ve isteklere yavaş yanıt veriyor olabilir; ya da ağ sorunları nedeniyle kısa bir süredir erişilebilir olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="47eed-137">For example, a service might be down because of a partial failure or for maintenance; the service might be overloaded and responding slowly to requests; or it might not be accessible for a short time because of network issues.</span></span> <span data-ttu-id="47eed-138">Bu nedenle, bulut tabanlı bir uygulamanın bu hatalara yanıt vermesi ve bu hatalara yanıt vermek için bir strateji olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="47eed-138">Therefore, a cloud-based application must embrace those failures and have a strategy in place to respond to those failures.</span></span> <span data-ttu-id="47eed-139">Bu stratejiler, tekrarlanmış isteklerin üstel yükünün önüne geçmek için yeniden deneme ilkelerini (iletileri yeniden göndermeyi veya istekleri yeniden göndermeyi) ve devre kesici düzenlerini uygulamayı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="47eed-139">These strategies can include retry policies (resending messages or retrying requests) and implementing circuit-breaker patterns to avoid exponential load of repeated requests.</span></span> <span data-ttu-id="47eed-140">Temel olarak, bulut tabanlı uygulamaların, düzenleme yöneticileri veya hizmet veri yolları tarafından sağlananlara göre, bulut altyapısına veya özel tabanlı olarak dayanıklı mekanizmalarına sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="47eed-140">Basically, cloud-based applications must have resilient mechanisms—either based on cloud infrastructure or custom, as the high-level ones provided by  orchestrators or service buses.</span></span>

<span data-ttu-id="47eed-141">**Güven.**</span><span class="sxs-lookup"><span data-stu-id="47eed-141">**Security.**</span></span> <span data-ttu-id="47eed-142">Modern bir kapsayıcı dünyamız ve mikro hizmetler yeni güvenlik açıklarını açığa çıkarır.</span><span class="sxs-lookup"><span data-stu-id="47eed-142">Our modern world of containers and microservices can expose new vulnerabilities.</span></span> <span data-ttu-id="47eed-143">Kimlik doğrulama ve yetkilendirme temel alınarak temel uygulama güvenliği uygulamak için birkaç yol vardır.</span><span class="sxs-lookup"><span data-stu-id="47eed-143">There are several ways to implement basic application security, based on authentication and authorization.</span></span> <span data-ttu-id="47eed-144">Ancak, kapsayıcı güvenliği, doğal olarak daha güvenli uygulamalarla sonuçlanan ek anahtar bileşenleri dikkate almalıdır.</span><span class="sxs-lookup"><span data-stu-id="47eed-144">However, container security must consider additional key components that result in inherently safer applications.</span></span> <span data-ttu-id="47eed-145">Daha güvenli uygulamalar oluşturmaya yönelik kritik bir öğe, genellikle kimlik bilgileri, belirteçler, parolalar ve benzer şekilde uygulama gizli dizileri olarak adlandırılan gibi, diğer uygulama ve sistemlerle iletişim kurmak için güvenli bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="47eed-145">A critical element of building safer apps is having a secure way of communicating with other apps and systems, something that often requires credentials, tokens, passwords, and the like, commonly referred to as application secrets.</span></span> <span data-ttu-id="47eed-146">Her türlü güvenli çözüm, aktarım sırasında ve REST sırasında gizli dizileri şifrelemek ve parolaların son uygulama tarafından tüketilirken sızmasını önlemek gibi en iyi güvenlik uygulamalarını izlemelidir.</span><span class="sxs-lookup"><span data-stu-id="47eed-146">Any secure solution must follow security best practices, such as encrypting secrets while in transit and at rest, and preventing secrets from leaking when consumed by the final application.</span></span> <span data-ttu-id="47eed-147">Azure Key Vault kullanırken olduğu gibi, bu parolaların güvenli bir şekilde depolanması ve güvenli tutulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="47eed-147">Those secrets need to be stored and kept safely, as when using Azure Key Vault.</span></span>

<span data-ttu-id="47eed-148">**Düzenleyicileri.**</span><span class="sxs-lookup"><span data-stu-id="47eed-148">**Orchestrators.**</span></span> <span data-ttu-id="47eed-149">Azure Kubernetes hizmeti ve Azure Service Fabric gibi kapsayıcı tabanlı düzenleyiciler, önemli mikro hizmet ve kapsayıcı tabanlı uygulamaların önemli bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="47eed-149">Container-based orchestrators, such as Azure Kubernetes Service and Azure Service Fabric are key part of any significant microservice and container-based application.</span></span> <span data-ttu-id="47eed-150">Bu uygulamalar, yüksek karmaşıklığa, ölçeklenebilirlik ihtiyaçlarına sahip ve sabit bir evrimle gider.</span><span class="sxs-lookup"><span data-stu-id="47eed-150">These applications carry with them high complexity, scalability needs, and go through constant evolution.</span></span> <span data-ttu-id="47eed-151">Bu kılavuz, mikro hizmet tabanlı ve kapsayıcı tabanlı çözümlerde yöneticileri ve bunların rollerini sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="47eed-151">This guide has introduced orchestrators and their role in microservice-based and container-based solutions.</span></span> <span data-ttu-id="47eed-152">Uygulamanızın ihtiyacı olan karmaşık Kapsayıcılı uygulamalara yaklaşmayı düşünüyorsanız, düzenlemeler hakkında daha fazla bilgi edinmek için ek kaynaklar aramak yararlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="47eed-152">If your application needs are moving you toward complex containerized apps, you will find it useful to seek out additional resources for learning more about orchestrators.</span></span>

>[!div class="step-by-step"]
>[<span data-ttu-id="47eed-153">Önceki</span><span class="sxs-lookup"><span data-stu-id="47eed-153">Previous</span></span>](secure-net-microservices-web-applications/azure-key-vault-protects-secrets.md)