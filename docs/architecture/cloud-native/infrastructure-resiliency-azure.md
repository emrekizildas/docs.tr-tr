---
title: Azure platformu dayanıklılığı
description: Azure için Cloud Native .NET uygulamaları tasarlama | Azure ile bulut altyapısı dayanıklılığı
ms.date: 06/30/2019
ms.openlocfilehash: 7f148588be97fa6bf8a055f5f5bed8e23908277f
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214202"
---
# <a name="azure-platform-resiliency"></a><span data-ttu-id="d4af4-103">Azure platformu dayanıklılığı</span><span class="sxs-lookup"><span data-stu-id="d4af4-103">Azure platform resiliency</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="d4af4-104">Bulutta güvenilir bir uygulama oluşturmak, geleneksel şirket içi uygulama geliştirmeden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-104">Building a reliable application in the cloud is different from traditional on-premises application development.</span></span> <span data-ttu-id="d4af4-105">Tarihsel olarak, ölçeğini ölçekleyerek bir bulut ortamında ölçeklendirmek için daha yüksek kaliteli donanımlar satın aldınız. Bu, hatalardan kaçınmak yerine, etkilerini en aza indirmek ve sistemi kararlı tutmaktır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-105">While historically you purchased higher-end hardware to scale up, in a cloud environment you scale out. Instead of trying to prevent failures, the goal is to minimize their effects and keep the system stable.</span></span>

<span data-ttu-id="d4af4-106">Bununla birlikte, güvenilir bulut uygulamaları farklı özellikleri görüntüler:</span><span class="sxs-lookup"><span data-stu-id="d4af4-106">That said, reliable cloud applications display distinct characteristics:</span></span>

- <span data-ttu-id="d4af4-107">Bunlar esnektir, sorunsuz bir şekilde kurtarılır ve çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="d4af4-107">They're resilient, recover gracefully from problems, and continue to function.</span></span>
- <span data-ttu-id="d4af4-108">Bunlar yüksek oranda kullanılabilir (HA) ve önemli bir kesinti olmadan sağlıklı bir durumda tasarlanan şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-108">They're highly available (HA) and run as designed in a healthy state with no significant downtime.</span></span>

<span data-ttu-id="d4af4-109">Bu özelliklerin birlikte nasıl çalıştığını ve güvenilir bir bulutta yerel uygulama oluşturmak için maliyeti nasıl etkileyeceğini anlama.</span><span class="sxs-lookup"><span data-stu-id="d4af4-109">Understanding how these characteristics work together - and how they affect cost - is essential to building a reliable cloud-native application.</span></span> <span data-ttu-id="d4af4-110">Azure bulutundaki özelliklerden yararlanarak, bulutta yerel uygulamalarınız için dayanıklılık ve kullanılabilirlik oluşturabileceğiniz yöntemlere bakacağız.</span><span class="sxs-lookup"><span data-stu-id="d4af4-110">We'll next look at ways that you can build resiliency and availability into your cloud-native applications leveraging features from the Azure cloud.</span></span>

## <a name="design-with-redundancy"></a><span data-ttu-id="d4af4-111">Yedeklilik ile tasarım</span><span class="sxs-lookup"><span data-stu-id="d4af4-111">Design with redundancy</span></span>

<span data-ttu-id="d4af4-112">Sorunlar, etki kapsamında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-112">Failures vary in scope of impact.</span></span> <span data-ttu-id="d4af4-113">Hatalı disk gibi bir donanım arızası, kümedeki tek bir düğümü etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-113">A hardware failure, such as a failed disk, can affect a single node in a cluster.</span></span> <span data-ttu-id="d4af4-114">Başarısız bir ağ anahtarı sunucu rafından tamamını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-114">A failed network switch could affect an entire server rack.</span></span> <span data-ttu-id="d4af4-115">Güç kaybı gibi yaygın olarak karşılaşılan sorunlar, tüm veri merkezini kesintiye uğratabilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-115">Less common failures, such as loss of power, could disrupt a whole datacenter.</span></span> <span data-ttu-id="d4af4-116">Nadiren, bir bölgenin tamamı kullanılamaz hale gelir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-116">Rarely, an entire region becomes unavailable.</span></span>

<span data-ttu-id="d4af4-117">[Artıklık](https://docs.microsoft.com/azure/architecture/guide/design-principles/redundancy) , uygulama esnekliği sağlamanın bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="d4af4-117">[Redundancy](https://docs.microsoft.com/azure/architecture/guide/design-principles/redundancy) is one way to provide application resilience.</span></span> <span data-ttu-id="d4af4-118">Gereken artıklık düzeyi, iş gereksinimlerinize bağlıdır ve sisteminizin maliyetini ve karmaşıklığını etkiler.</span><span class="sxs-lookup"><span data-stu-id="d4af4-118">The exact level of redundancy needed depends on your business requirements and will affect both cost and complexity of your system.</span></span> <span data-ttu-id="d4af4-119">Örneğin, çok bölgeli bir dağıtım, tek bölgeli bir dağıtıma göre yönetilmesi daha pahalıdır ve daha karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-119">For example, a multi-region deployment is more expensive and more complex to manage than a single-region deployment.</span></span> <span data-ttu-id="d4af4-120">Yük devretme ve yeniden çalışma işlemlerini yönetmek için işlemsel yordamlara ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="d4af4-120">You'll need operational procedures to manage failover and failback.</span></span> <span data-ttu-id="d4af4-121">Ek maliyet ve karmaşıklık, bazı iş senaryoları için başka bir şekilde hizalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-121">The additional cost and complexity might be justified for some business scenarios and not others.</span></span>

<span data-ttu-id="d4af4-122">Yedekliliği mimARDA uygulamak için uygulamanızdaki kritik yolları belirlemeniz ve sonra yoldaki her bir noktada artıklık olup olmadığını belirlemeniz gerekir mi?</span><span class="sxs-lookup"><span data-stu-id="d4af4-122">To architect redundancy, you need to identify the critical paths in your application, and then determine if there's redundancy at each point in the path?</span></span> <span data-ttu-id="d4af4-123">Bir alt sistem başarısız olursa, uygulama başka bir şeye devredilecek mi?</span><span class="sxs-lookup"><span data-stu-id="d4af4-123">If a subsystem should fail, will the application fail over to something else?</span></span> <span data-ttu-id="d4af4-124">Son olarak, Azure bulut platformunda yerleşik olarak bulunan ve artıklık gereksinimlerinizi karşılamak için kullanabileceğiniz özellikleri net bir şekilde kavramanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-124">Finally, you need a clear understanding of those features built into the Azure cloud platform that you can leverage to meet your redundancy requirements.</span></span> <span data-ttu-id="d4af4-125">Yedeklilik mimarisi için öneriler aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d4af4-125">Here are recommendations for architecting redundancy:</span></span>

- <span data-ttu-id="d4af4-126">*Birden çok hizmet örneğini dağıtın.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-126">*Deploy multiple instances of services.*</span></span> <span data-ttu-id="d4af4-127">Uygulamanız bir hizmetin tek bir örneğine bağımlıysa, tek bir hata noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4af4-127">If your application depends on a single instance of a service, it creates a single point of failure.</span></span> <span data-ttu-id="d4af4-128">Birden çok örnek sağlanması hem dayanıklılık hem de ölçeklenebilirliği geliştirir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-128">Provisioning multiple instances improves both resiliency and scalability.</span></span> <span data-ttu-id="d4af4-129">Azure Kubernetes hizmetinde barındırırken, Kubernetes bildirim dosyasında gereksiz örnekleri (çoğaltma kümeleri) bildirimli olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4af4-129">When hosting in Azure Kubernetes Service, you can declaratively configure redundant instances (replica sets) in the Kubernetes manifest file.</span></span> <span data-ttu-id="d4af4-130">Çoğaltma sayısı değeri, portalda veya daha sonra ele alınacaktır. otomatik ölçeklendirme özellikleri ile programlı bir şekilde yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-130">The replica count value can be managed programmatically, in the portal or through autoscaling features, which will be discussed later on.</span></span>

- <span data-ttu-id="d4af4-131">*Yük dengeleyiciyi kullanma.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-131">*Leveraging a load balancer.*</span></span> <span data-ttu-id="d4af4-132">Yük Dengeleme, uygulamanızın isteklerini sağlıklı hizmet örneklerine dağıtır ve sağlıksız örnekleri otomatik olarak dönüşten kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-132">Load-balancing distributes your application's requests to healthy service instances and automatically removes unhealthy instances from rotation.</span></span> <span data-ttu-id="d4af4-133">Kubernetes 'e dağıtım yaparken, hizmetler bölümündeki Kubernetes bildirim dosyasında Yük Dengeleme belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-133">When deploying to Kubernetes, load balancing can be specified in the Kubernetes manifest file in the Services section.</span></span>

- <span data-ttu-id="d4af4-134">*Çok bölgeli dağıtımını planlayın.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-134">*Plan for multiregion deployment.*</span></span> <span data-ttu-id="d4af4-135">Uygulamanız tek bir bölgeye dağıtılmışsa ve bölge kullanılamaz hale gelirse, uygulamanız da kullanılamaz hale gelir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-135">If your application is deployed to a single region, and the region becomes unavailable, your application will also become unavailable.</span></span> <span data-ttu-id="d4af4-136">Bu, uygulamanızın hizmet düzeyi sözleşmeleri koşullarında kabul edilebilir olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-136">This may be unacceptable under the terms of your application's service level agreements.</span></span> <span data-ttu-id="d4af4-137">Bunun yerine, uygulamanızı ve hizmetlerini birden çok bölgeye dağıtmaya dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d4af4-137">Instead, consider deploying your application and its services across multiple regions.</span></span> <span data-ttu-id="d4af4-138">Örneğin, bir Azure Kubernetes hizmeti (AKS) kümesi tek bir bölgeye dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-138">For example, an Azure Kubernetes Service (AKS) cluster is deployed to a single region.</span></span> <span data-ttu-id="d4af4-139">Sisteminizi bölgesel bir hatadan korumak için, uygulamanızı farklı bölgelerde birden çok AKS kümesine dağıtabilir ve [eşleştirilmiş bölgeler](https://buildazure.com/2017/01/06/azure-region-pairs-explained/) özelliğini kullanarak platform güncelleştirmelerini koordine edebilir ve kurtarma çalışmalarını önceliklendirin.</span><span class="sxs-lookup"><span data-stu-id="d4af4-139">To protect your system from a regional failure, you might deploy your application to multiple AKS clusters across different regions and use the [Paired Regions](https://buildazure.com/2017/01/06/azure-region-pairs-explained/) feature to coordinate platform updates and prioritize recovery efforts.</span></span>

- <span data-ttu-id="d4af4-140">*[Coğrafi çoğaltmayı](https://docs.microsoft.com/azure/sql-database/sql-database-active-geo-replication)etkinleştirin.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-140">*Enable [geo-replication](https://docs.microsoft.com/azure/sql-database/sql-database-active-geo-replication).*</span></span> <span data-ttu-id="d4af4-141">Azure SQL veritabanı ve Cosmos DB gibi hizmetler için coğrafi çoğaltma, verilerinizin birden çok bölgede ikincil çoğaltmalarını oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-141">Geo-replication for services such as Azure SQL Database and Cosmos DB will create secondary replicas of your data across multiple regions.</span></span> <span data-ttu-id="d4af4-142">Her iki hizmet de aynı bölgedeki verileri otomatik olarak çoğaltarak, coğrafi çoğaltma, bir ikincil bölgeye yük devretmek için bölgesel bir kesinti ile karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4af4-142">While both services will automatically replicate data within the same region, geo-replication protects you against a regional outage by enabling you to fail over to a secondary region.</span></span> <span data-ttu-id="d4af4-143">Kapsayıcı görüntülerinin depolandığı coğrafi çoğaltma merkezleri için bir en iyi yöntem.</span><span class="sxs-lookup"><span data-stu-id="d4af4-143">Another best practice for geo-replication centers around storing container images.</span></span> <span data-ttu-id="d4af4-144">AKS 'de bir hizmet dağıtmak için, görüntüyü depolamanız ve bir depodan çekmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-144">To deploy a service in AKS, you need to store and pull the image from a repository.</span></span> <span data-ttu-id="d4af4-145">Azure Container Registry, AKS ile tümleşir ve kapsayıcı görüntülerini güvenli bir şekilde saklayabilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-145">Azure Container Registry integrates with AKS and can securely store container images.</span></span> <span data-ttu-id="d4af4-146">Performansı ve kullanılabilirliği artırmak için, görüntülerinizi bir AKS kümeniz olan her bölgedeki bir kayıt defterine coğrafi olarak çoğaltmayı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d4af4-146">To improve performance and availability, consider geo-replicating your images to a registry in each region where you have an AKS cluster.</span></span> <span data-ttu-id="d4af4-147">Ardından, her bir AKS kümesi, Şekil 6-6 ' de gösterildiği gibi bölgesinde yerel kapsayıcı kayıt defterinden kapsayıcı görüntülerini çeker:</span><span class="sxs-lookup"><span data-stu-id="d4af4-147">Each AKS cluster then pulls container images from the local container registry in its region as shown in Figure 6-6:</span></span>

![Bölgeler arasında çoğaltılan kaynaklar](./media/replicated-resources.png)

<span data-ttu-id="d4af4-149">**Şekil 6-6**.</span><span class="sxs-lookup"><span data-stu-id="d4af4-149">**Figure 6-6**.</span></span> <span data-ttu-id="d4af4-150">Bölgeler arasında çoğaltılan kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d4af4-150">Replicated resources across regions</span></span>

- <span data-ttu-id="d4af4-151">*Bir DNS trafiği yük dengeleyici uygulayın.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-151">*Implement a DNS traffic load balancer.*</span></span> <span data-ttu-id="d4af4-152">[Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) , DNS düzeyinde yük dengelemeye göre kritik uygulamalar için yüksek kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4af4-152">[Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) provides high-availability for critical applications by load-balancing at the DNS level.</span></span> <span data-ttu-id="d4af4-153">Coğrafi konum, küme yanıt süresi ve hatta uygulama uç noktası sistem durumu temelinde trafiği farklı bölgelere yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-153">It can route traffic to different regions based on geography, cluster response time, and even application endpoint health.</span></span> <span data-ttu-id="d4af4-154">Örneğin, Azure Traffic Manager müşterileri en yakın AKS kümesine ve uygulama örneğine yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-154">For example, Azure Traffic Manager can direct customers to the closest AKS cluster and application instance.</span></span> <span data-ttu-id="d4af4-155">Farklı bölgelerde birden fazla AKS kümeniz varsa, trafiğin her kümede çalışan uygulamalara nasıl akacağını denetlemek için Traffic Manager kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4af4-155">If you have multiple AKS clusters in different regions, use Traffic Manager to control how traffic flows to the applications that run in each cluster.</span></span> <span data-ttu-id="d4af4-156">Şekil 6-7, bu senaryoyu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-156">Figure 6-7 shows this scenario.</span></span>

![AKS ve Azure Traffic Manager](./media/aks-traffic-manager.png)

<span data-ttu-id="d4af4-158">**Şekil 6-7**.</span><span class="sxs-lookup"><span data-stu-id="d4af4-158">**Figure 6-7**.</span></span> <span data-ttu-id="d4af4-159">AKS ve Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="d4af4-159">AKS and Azure Traffic Manager</span></span>

## <a name="design-for-scalability"></a><span data-ttu-id="d4af4-160">Ölçeklenebilirlik için tasarım</span><span class="sxs-lookup"><span data-stu-id="d4af4-160">Design for scalability</span></span>

<span data-ttu-id="d4af4-161">Bulut ölçeklendiriliyor.</span><span class="sxs-lookup"><span data-stu-id="d4af4-161">The cloud thrives on scaling.</span></span> <span data-ttu-id="d4af4-162">Sistem yükünü artırmak/azaltmak için sistem kaynaklarını artırma/azaltma yeteneği, Azure bulutunun önemli bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-162">The ability to increase/decrease system resources to address increasing/decreasing system load is a key tenet of the Azure cloud.</span></span> <span data-ttu-id="d4af4-163">Ancak, bir uygulamayı etkin bir şekilde ölçeklendirmek için uygulamanıza dahil ettiğiniz her bir Azure hizmetinin ölçekleme özelliklerinin anlaşılmasına gerek duyarsınız.</span><span class="sxs-lookup"><span data-stu-id="d4af4-163">But, to effectively scale an application, you need an understanding of the scaling features of each Azure service that you include in your application.</span></span>  <span data-ttu-id="d4af4-164">Sisteminizde ölçeklendirmeyi etkili bir şekilde uygulamaya yönelik öneriler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-164">Here are recommendations for effectively implementing scaling in your system.</span></span>

- <span data-ttu-id="d4af4-165">*Ölçeklendirme için tasarlayın.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-165">*Design for scaling.*</span></span> <span data-ttu-id="d4af4-166">Uygulamanın ölçeklendirilmesi için tasarlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-166">An application must be designed for scaling.</span></span> <span data-ttu-id="d4af4-167">Başlamak için hizmetlerin durum bilgisiz olması gerekir, bu nedenle istekler herhangi bir örneğe yönlendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-167">To start, services should be stateless so that requests can be routed to any instance.</span></span> <span data-ttu-id="d4af4-168">Durum bilgisi olmayan hizmetlerin olması, bir örneği eklemenin veya kaldırmanın geçerli kullanıcıları olumsuz yönde etkilemediği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-168">Having stateless services also means that adding or removing an instance doesn't adversely impact current users.</span></span>

- <span data-ttu-id="d4af4-169">*Bölüm iş yükleri*.</span><span class="sxs-lookup"><span data-stu-id="d4af4-169">*Partition workloads*.</span></span> <span data-ttu-id="d4af4-170">Etki alanlarının bağımsız bir şekilde çıkarılması, kendi kendine kapsanan mikro hizmetlere, her hizmetin diğerlerinden bağımsız olarak ölçeklendirilmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-170">Decomposing domains into independent, self-contained microservices enable each service to scale independently of others.</span></span> <span data-ttu-id="d4af4-171">Genellikle, hizmetler farklı ölçeklenebilirlik gereksinimlerine ve gereksinimlerine sahip olur.</span><span class="sxs-lookup"><span data-stu-id="d4af4-171">Typically, services will have different scalability needs and requirements.</span></span> <span data-ttu-id="d4af4-172">Bölümlendirme, bir uygulamanın tamamını ölçeklendirmeye yönelik gereksiz maliyet olmadan yalnızca ölçeklendirilmesi gerekenleri ölçeklendirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4af4-172">Partitioning enables you to scale only what needs to be scaled without the unnecessary cost of scaling an entire application.</span></span>

- <span data-ttu-id="d4af4-173">*Ölçeği genişletme tercih edin.* Bulut tabanlı uygulamalar, ölçeklendirmenin aksine kaynakları ölçeklendirmeye tercih ister.</span><span class="sxs-lookup"><span data-stu-id="d4af4-173">*Favor scale-out.* Cloud-based applications favor scaling out resources as opposed to scaling up.</span></span> <span data-ttu-id="d4af4-174">Ölçeği genişletme (yatay ölçeklendirme olarak da bilinir), istenen bir performans düzeyini karşılamak ve paylaşmak üzere mevcut bir sisteme daha fazla hizmet kaynağı eklenmesini içerir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-174">Scaling out (also known as horizontal scaling) involves adding more service resources to an existing system to meet and share a desired level of performance.</span></span> <span data-ttu-id="d4af4-175">Ölçeği artırma (dikey ölçeklendirme olarak da bilinir), var olan kaynakları daha güçlü donanımla (daha fazla disk, bellek ve işlem çekirdeği) değiştirmeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-175">Scaling up (also known as vertical scaling) involves replacing existing resources with more powerful hardware (more disk, memory, and processing cores).</span></span> <span data-ttu-id="d4af4-176">Ölçeği genişletme, bazı Azure bulut kaynaklarında bulunan otomatik ölçeklendirme özellikleriyle otomatik olarak çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-176">Scaling out can be invoked automatically with the autoscaling features available in some Azure cloud resources.</span></span> <span data-ttu-id="d4af4-177">Birden çok kaynak arasında ölçeklendirme yapmak, genel sisteme artıklık de ekler.</span><span class="sxs-lookup"><span data-stu-id="d4af4-177">Scaling out across multiple resources also adds redundancy to the overall system.</span></span> <span data-ttu-id="d4af4-178">Son olarak, tek bir kaynağın ölçeklendirilmesi genellikle pek çok daha küçük kaynak arasında ölçeklendirmeden daha pahalıdır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-178">Finally scaling up a single resource is typically more expensive than scaling out across many smaller resources.</span></span> <span data-ttu-id="d4af4-179">Şekil 6-8 iki yaklaşımı gösterir:</span><span class="sxs-lookup"><span data-stu-id="d4af4-179">Figure 6-8 shows the two approaches:</span></span>

![Ölçeği büyütme ve ölçeği genişletme](./media/scale-up-scale-out.png)

<span data-ttu-id="d4af4-181">**Şekil 6-8.**</span><span class="sxs-lookup"><span data-stu-id="d4af4-181">**Figure 6-8.**</span></span> <span data-ttu-id="d4af4-182">Ölçeği büyütme ve ölçeği genişletme</span><span class="sxs-lookup"><span data-stu-id="d4af4-182">Scale up versus scale out</span></span>

- <span data-ttu-id="d4af4-183">*Orantılı olarak ölçeklendirin.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-183">*Scale proportionally.*</span></span> <span data-ttu-id="d4af4-184">Bir hizmeti ölçeklendirirken, *kaynak kümeleri*açısından göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d4af4-184">When scaling a service, think in terms of *resource sets*.</span></span> <span data-ttu-id="d4af4-185">Belirli bir hizmeti önemli ölçüde ölçeklendirmeniz durumunda, arka uç veri depoları, önbellekler ve bağımlı hizmetler üzerinde hangi etkileri vardır?</span><span class="sxs-lookup"><span data-stu-id="d4af4-185">If you were to dramatically scale out a specific service, what impact would that have on back-end data stores, caches and dependent services?</span></span> <span data-ttu-id="d4af4-186">Cosmos DB gibi bazı kaynaklar orantılı bir şekilde ölçeklenebilir, ancak diğerleri pek çok olamaz.</span><span class="sxs-lookup"><span data-stu-id="d4af4-186">Some resources such as Cosmos DB can scale out proportionally, while many others can't.</span></span> <span data-ttu-id="d4af4-187">Kaynağı, diğer ilişkili kaynakları tüketdirecek bir noktaya ölçeklendirdiğinizden emin olmak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="d4af4-187">You want to ensure that you don't scale out a resource to a point where it will exhaust other associated resources.</span></span>

- <span data-ttu-id="d4af4-188">*Benzeşim kullanmaktan kaçının.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-188">*Avoid affinity.*</span></span> <span data-ttu-id="d4af4-189">Bir düğümün, genellikle bir *yapışkan oturum*olarak adlandırılan yerel benzeşim gerektirmemesini sağlamak en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-189">A best practice is to ensure a node doesn't require local affinity, often referred to as a *sticky session*.</span></span> <span data-ttu-id="d4af4-190">Bir istek herhangi bir örneğe yönlendiribilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-190">A request should be able to route to any instance.</span></span> <span data-ttu-id="d4af4-191">Durumu kalıcı hale getirmeniz gerekiyorsa, [Azure redsıs Cache](https://azure.microsoft.com/services/cache/)gibi dağıtılmış bir önbelleğe kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-191">If you need to persist state, it should be saved to a distributed cache, such as [Azure Redis cache](https://azure.microsoft.com/services/cache/).</span></span>

- <span data-ttu-id="d4af4-192">*Platform otomatik ölçeklendirme özelliklerinin avantajlarından yararlanın.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-192">*Take advantage of platform autoscaling features.*</span></span> <span data-ttu-id="d4af4-193">Özel veya üçüncü taraf mekanizmalarının yerine, mümkün olduğunda yerleşik otomatik ölçeklendirme özellikleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4af4-193">Use built-in autoscaling features whenever possible, rather than custom or third-party mechanisms.</span></span> <span data-ttu-id="d4af4-194">Mümkün olduğunda, kaynakların bir başlangıç gecikmesi olmadan kullanılabilir olduğundan emin olmak için zamanlanmış ölçekleme kurallarını kullanın, ancak kurallara uygun şekilde, isteğe bağlı olarak, talep halinde beklenmedik değişikliklerle ve bu kurallara otomatik ölçeklendirme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4af4-194">Where possible, use scheduled scaling rules to ensure that resources are available without a startup delay, but add reactive autoscaling to the rules as appropriate, to cope with unexpected changes in demand.</span></span> <span data-ttu-id="d4af4-195">Daha fazla bilgi için bkz. [Otomatik ölçeklendirme Kılavuzu](https://docs.microsoft.com/azure/architecture/best-practices/auto-scaling).</span><span class="sxs-lookup"><span data-stu-id="d4af4-195">For more information, see [Autoscaling guidance](https://docs.microsoft.com/azure/architecture/best-practices/auto-scaling).</span></span>

- <span data-ttu-id="d4af4-196">*Ölçeği artırma kararlılığı.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-196">*Scale-up aggressively.*</span></span> <span data-ttu-id="d4af4-197">Son bir uygulama, iş kaybı olmadan trafikte anında ani artışları hızlı bir şekilde karşılayabilmeniz için kararlılığı en iyi şekilde ölçeklendirmektir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-197">A final practice would be to scale up aggressively so that you can quickly meet immediate spikes in traffic without losing business.</span></span> <span data-ttu-id="d4af4-198">Daha sonra, sistem kararlı kalmasını sağlamak için ölçeği azaltın (yani gereksiz kaynakları kaldırın).</span><span class="sxs-lookup"><span data-stu-id="d4af4-198">And, then scale down (that is, remove unneeded resources) conservatively to keep the system stable.</span></span> <span data-ttu-id="d4af4-199">Bunu yapmanın basit bir yolu, ölçeklendirme işlemleri arasında bekleme süresi, kaynak eklemek için beş dakika, örnekleri kaldırmak için en fazla 15 dakika olan seyrek erişimli süreyi ayarlamanıza yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-199">A simple way to implement this is to set the cool down period, which is the time to wait between scaling operations, to five minutes for adding resources and up to 15 minutes for removing instances.</span></span>

## <a name="built-in-retry-in-services"></a><span data-ttu-id="d4af4-200">Hizmetlerde yerleşik yeniden deneme</span><span class="sxs-lookup"><span data-stu-id="d4af4-200">Built-in retry in services</span></span>

<span data-ttu-id="d4af4-201">Daha önceki bir bölümde programlı yeniden deneme işlemleri uygulamak için en iyi uygulama önerilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-201">We encouraged the best practice of implementing programmatic retry operations in an earlier section.</span></span> <span data-ttu-id="d4af4-202">Birçok Azure hizmeti ve bunlara karşılık gelen istemci SDK 'larının yeniden deneme mekanizmalarını de dahil olduğunu aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d4af4-202">Keep in mind that many Azure services and their corresponding client SDKs also include retry mechanisms.</span></span> <span data-ttu-id="d4af4-203">Aşağıdaki listede, bu kitapta tartışılan birçok Azure hizmeti için yeniden deneme özellikleri özetlenmektedir:</span><span class="sxs-lookup"><span data-stu-id="d4af4-203">The following list summarizes retry features in the many of the Azure services that are discussed in this book:</span></span>

- <span data-ttu-id="d4af4-204">*Azure Cosmos DB.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-204">*Azure Cosmos DB.*</span></span> <span data-ttu-id="d4af4-205">İstemci API 'sindeki sınıf başarısız denemeleri otomatik olarak yeniden oluşturur. <xref:Microsoft.Azure.Documents.Client.DocumentClient></span><span class="sxs-lookup"><span data-stu-id="d4af4-205">The <xref:Microsoft.Azure.Documents.Client.DocumentClient> class from the client API automatically retires failed attempts.</span></span> <span data-ttu-id="d4af4-206">Yeniden deneme sayısı ve en fazla bekleme süresi yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-206">The number of retries and maximum wait time are configurable.</span></span> <span data-ttu-id="d4af4-207">İstemci API 'SI tarafından oluşturulan özel durumlar, yeniden deneme ilkesini veya geçici olmayan hataları aşan isteklerdir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-207">Exceptions thrown by the client API are either requests that exceed the retry policy or non-transient errors.</span></span>

- <span data-ttu-id="d4af4-208">*Azure Redis Cache.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-208">*Azure Redis Cache.*</span></span> <span data-ttu-id="d4af4-209">Redsıs StackExchange istemcisi, başarısız denemelerde yeniden denemeler içeren bir bağlantı Yöneticisi sınıfı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-209">The Redis StackExchange client uses a connection manager class that includes retries on failed attempts.</span></span> <span data-ttu-id="d4af4-210">Yeniden deneme sayısı, belirli bir yeniden deneme ilkesi ve bekleme süresi yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-210">The number of retries, specific retry policy and wait time are all configurable.</span></span>

- <span data-ttu-id="d4af4-211">*Azure Service Bus.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-211">*Azure Service Bus.*</span></span> <span data-ttu-id="d4af4-212">Service Bus istemcisi bir geri alma aralığı, yeniden deneme sayısı ve <xref:Microsoft.ServiceBus.RetryExponential.TerminationTimeBuffer>bir işlemin ne zaman sürebileceği maksimum süreyi belirten bir [retrypolicy sınıfı](xref:Microsoft.ServiceBus.RetryPolicy) kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="d4af4-212">The Service Bus client exposes a [RetryPolicy class](xref:Microsoft.ServiceBus.RetryPolicy) that can be configured with a back-off interval, retry count, and <xref:Microsoft.ServiceBus.RetryExponential.TerminationTimeBuffer>, which specifies the maximum time an operation can take.</span></span> <span data-ttu-id="d4af4-213">Varsayılan ilke, denemeler arasında 30 saniyelik geri alma süresi olan dokuz en fazla yeniden deneme girişimdir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-213">The default policy is nine maximum retry attempts with a 30-second backoff period between attempts.</span></span>

- <span data-ttu-id="d4af4-214">*Azure SQL veritabanı.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-214">*Azure SQL Database.*</span></span> <span data-ttu-id="d4af4-215">[Entity Framework Core](https://docs.microsoft.com/ef/core/miscellaneous/connection-resiliency) kitaplığı kullanılırken yeniden deneme desteği sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d4af4-215">Retry support is provided when using the [Entity Framework Core](https://docs.microsoft.com/ef/core/miscellaneous/connection-resiliency) library.</span></span>

- <span data-ttu-id="d4af4-216">*Azure depolama.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-216">*Azure Storage.*</span></span> <span data-ttu-id="d4af4-217">Depolama istemci kitaplığı, yeniden deneme işlemlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="d4af4-217">The storage client library support retry operations.</span></span> <span data-ttu-id="d4af4-218">Stratejiler, Azure depolama tabloları, blob 'lar ve kuyruklar arasında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-218">The strategies vary across Azure storage tables, blobs, and queues.</span></span> <span data-ttu-id="d4af4-219">Ayrıca, coğrafi artıklık özelliği etkinken, alternatif yeniden denemeler birincil ve ikincil depolama hizmetleri konumları arasında geçiş yapar.</span><span class="sxs-lookup"><span data-stu-id="d4af4-219">As well, alternate retries switch between primary and secondary storage services locations when the geo-redundancy feature is enabled.</span></span>

- <span data-ttu-id="d4af4-220">*Azure Event Hubs.*</span><span class="sxs-lookup"><span data-stu-id="d4af4-220">*Azure Event Hubs.*</span></span> <span data-ttu-id="d4af4-221">Olay Hub 'ı istemci kitaplığı, yapılandırılabilir bir üstel geri alma özelliği içeren bir RetryPolicy özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d4af4-221">The Event Hub client library features a RetryPolicy property, which includes a configurable exponential backoff feature.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="d4af4-222">[Önceki](application-resiliency-patterns.md)
>[İleri](resilient-communications.md)</span><span class="sxs-lookup"><span data-stu-id="d4af4-222">[Previous](application-resiliency-patterns.md)
[Next](resilient-communications.md)</span></span>