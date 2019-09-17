---
title: Mikro hizmetlerde esneklik ve yüksek kullanılabilirlik
description: Mikro hizmetlerin, geçici ağ ve bağımlılıklar hatalarıyla birlikte kullanılması için tasarlanmaları gerekir, bu da yüksek kullanılabilirlik elde etmek için dayanıklı olmalıdır.
ms.date: 09/20/2018
ms.openlocfilehash: bb1bef0c9cc08e43aed80a29effe89587fb296f6
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/30/2019
ms.locfileid: "70296256"
---
# <a name="resiliency-and-high-availability-in-microservices"></a><span data-ttu-id="40538-103">Mikro hizmetlerde esneklik ve yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="40538-103">Resiliency and high availability in microservices</span></span>

<span data-ttu-id="40538-104">Beklenmedik hatalarla ilgilenirken, özellikle dağıtılmış bir sistemde çözülecek en zor sorunlardan biridir.</span><span class="sxs-lookup"><span data-stu-id="40538-104">Dealing with unexpected failures is one of the hardest problems to solve, especially in a distributed system.</span></span> <span data-ttu-id="40538-105">Geliştiricilerin yazacağı kodun büyük bölümü özel durumları işlemeye ve bu da en fazla saatin test edilirken harcanmasını içerir.</span><span class="sxs-lookup"><span data-stu-id="40538-105">Much of the code that developers write involves handling exceptions, and this is also where the most time is spent in testing.</span></span> <span data-ttu-id="40538-106">Sorun, hataların işlenmesi için kodun yazılmasından daha karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="40538-106">The problem is more involved than writing code to handle failures.</span></span> <span data-ttu-id="40538-107">Mikro hizmetin çalıştığı makine başarısız olduğunda ne olur?</span><span class="sxs-lookup"><span data-stu-id="40538-107">What happens when the machine where the microservice is running fails?</span></span> <span data-ttu-id="40538-108">Bu mikro hizmet başarısızlığını (kendi kendine yönelik bir sorun) algılamanıza gerek kalmaz, ancak mikro hizmetinizi yeniden başlatmak için de bir işlem yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="40538-108">Not only do you need to detect this microservice failure (a hard problem on its own), but you also need something to restart your microservice.</span></span>

<span data-ttu-id="40538-109">Mikro bir hizmetin hatalara karşı dayanıklı olması ve başka bir makinede kullanılabilirlik için sık olarak yeniden başlatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="40538-109">A microservice needs to be resilient to failures and to be able to restart often on another machine for availability.</span></span> <span data-ttu-id="40538-110">Bu esneklik, mikro hizmetin bu durumu ' den kurtarabileceği ve mikro hizmetin başarıyla yeniden başlatılıp başlatılmayacağını belirten mikro hizmet adına kaydedilmiş duruma da gelir.</span><span class="sxs-lookup"><span data-stu-id="40538-110">This resiliency also comes down to the state that was saved on behalf of the microservice, where the microservice can recover this state from, and whether the microservice can restart successfully.</span></span> <span data-ttu-id="40538-111">Diğer bir deyişle, işlem yeteneğinin dayanıklılık olması gerekir (işlem herhangi bir zamanda yeniden başlatılabilir) ve durum veya verilerde esnekliği (veri kaybı yoktur ve veriler tutarlı kalır).</span><span class="sxs-lookup"><span data-stu-id="40538-111">In other words, there needs to be resiliency in the compute capability (the process can restart at any time) as well as resilience in the state or data (no data loss, and the data remains consistent).</span></span>

<span data-ttu-id="40538-112">Dayanıklılık sorunları, bir uygulama yükseltmesi sırasında hataların oluşma gibi başka senaryolar sırasında da bir bakış sürecinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="40538-112">The problems of resiliency are compounded during other scenarios, such as when failures occur during an application upgrade.</span></span> <span data-ttu-id="40538-113">Dağıtım sistemiyle çalışan mikro hizmetin, daha yeni bir sürüme ilerleyemeyeceğini veya daha önce tutarlı bir durumu korumak için önceki bir sürüme geri dönerek devam edip etmediğini belirlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="40538-113">The microservice, working with the deployment system, needs to determine whether it can continue to move forward to the newer version or instead roll back to a previous version to maintain a consistent state.</span></span> <span data-ttu-id="40538-114">Daha önce taşınabileceği ve mikro hizmetin önceki sürümlerinin nasıl kurtarılacağı hakkında daha fazla sayıda makinenin kabul edilip edilmeyeceği gibi sorular.</span><span class="sxs-lookup"><span data-stu-id="40538-114">Questions such as whether enough machines are available to keep moving forward and how to recover previous versions of the microservice need to be considered.</span></span> <span data-ttu-id="40538-115">Bu, tüm uygulama ve Orchestrator bu kararları verebilmeleri için mikro hizmetin sistem durumu bilgilerini yaymasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="40538-115">This requires the microservice to emit health information so that the overall application and orchestrator can make these decisions.</span></span>

<span data-ttu-id="40538-116">Ayrıca, dayanıklılık bulut tabanlı sistemlerin nasıl davranması ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="40538-116">In addition, resiliency is related to how cloud-based systems must behave.</span></span> <span data-ttu-id="40538-117">Belirtildiği gibi, bulut tabanlı bir sistem hatalara ve bunları otomatik olarak kurtarmayı denemelidir.</span><span class="sxs-lookup"><span data-stu-id="40538-117">As mentioned, a cloud-based system must embrace failures and must try to automatically recover from them.</span></span> <span data-ttu-id="40538-118">Örneğin, ağ veya kapsayıcı hatalarıyla ilgili durumlarda, istemci uygulamalarının veya istemci hizmetlerinin iletileri göndermeyi veya istekleri yeniden denemeyi yeniden denemek için bir stratejisine sahip olması gerekir, çünkü buluttaki hataların çoğu kısmen kısmi bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="40538-118">For instance, in case of network or container failures, client apps or client services must have a strategy to retry sending messages or to retry requests, since in many cases failures in the cloud are partial.</span></span> <span data-ttu-id="40538-119">Bu kılavuzdaki dayanıklı [uygulamalar uygulama](../implement-resilient-applications/index.md) bölümünde kısmi hatanın nasıl işleneceği ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="40538-119">The [Implementing Resilient Applications](../implement-resilient-applications/index.md) section in this guide addresses how to handle partial failure.</span></span> <span data-ttu-id="40538-120">Bu konuyu işlemek için çok çeşitli ilkeler sunan, üstel geri alma veya .NET Core 'daki devre kesici düzeniyle yeniden denemeler [gibi teknikleri](https://github.com/App-vNext/Polly)açıklar.</span><span class="sxs-lookup"><span data-stu-id="40538-120">It describes techniques like retries with exponential backoff or the Circuit Breaker pattern in .NET Core by using libraries like [Polly](https://github.com/App-vNext/Polly), which offers a large variety of policies to handle this subject.</span></span>

## <a name="health-management-and-diagnostics-in-microservices"></a><span data-ttu-id="40538-121">Mikro hizmetlerde sistem durumu yönetimi ve tanılama</span><span class="sxs-lookup"><span data-stu-id="40538-121">Health management and diagnostics in microservices</span></span>

<span data-ttu-id="40538-122">Açık görünebilir ve genellikle çok daha fazla görünür, ancak bir mikro hizmet, sistem durumunu ve tanılamayı raporlamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="40538-122">It may seem obvious, and it's often overlooked, but a microservice must report its health and diagnostics.</span></span> <span data-ttu-id="40538-123">Aksi takdirde, bir işlem perspektifinden çok daha fazla öngörü vardır.</span><span class="sxs-lookup"><span data-stu-id="40538-123">Otherwise, there's little insight from an operations perspective.</span></span> <span data-ttu-id="40538-124">Bir bağımsız hizmet kümesi genelinde tanılama olaylarının bağıntılandırın ve olay sırası 'nın mantıklı olması için makine saati eğimiyle ilgilenme.</span><span class="sxs-lookup"><span data-stu-id="40538-124">Correlating diagnostic events across a set of independent services and dealing with machine clock skews to make sense of the event order is challenging.</span></span> <span data-ttu-id="40538-125">Kabul edilen protokoller ve veri biçimleri üzerinde bir mikro hizmetle etkileşimde bulunmanızın yanı sıra, sorgulama ve görüntüleme amacıyla bir olay deposunda son görüntülenen sistem durumu ve tanılama olaylarının nasıl günlüğe alınacağını belirleme gereksinimi vardır.</span><span class="sxs-lookup"><span data-stu-id="40538-125">In the same way that you interact with a microservice over agreed-upon protocols and data formats, there's a need for standardization in how to log health and diagnostic events that ultimately end up in an event store for querying and viewing.</span></span> <span data-ttu-id="40538-126">Mikro hizmetler yaklaşımında, farklı takımların tek bir günlük biçiminde kabul ettığı anahtardır.</span><span class="sxs-lookup"><span data-stu-id="40538-126">In a microservices approach, it's key that different teams agree on a single logging format.</span></span> <span data-ttu-id="40538-127">Uygulamada Tanılama olaylarını görüntülemek için tutarlı bir yaklaşım olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="40538-127">There needs to be a consistent approach to viewing diagnostic events in the application.</span></span>

### <a name="health-checks"></a><span data-ttu-id="40538-128">Sistem durumu denetimleri</span><span class="sxs-lookup"><span data-stu-id="40538-128">Health checks</span></span>

<span data-ttu-id="40538-129">Sağlık, tanılamalardan farklıdır.</span><span class="sxs-lookup"><span data-stu-id="40538-129">Health is different from diagnostics.</span></span> <span data-ttu-id="40538-130">Sistem durumu, uygun işlemleri gerçekleştirmek için geçerli durumunu raporlayan mikro hizmet ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="40538-130">Health is about the microservice reporting its current state to take appropriate actions.</span></span> <span data-ttu-id="40538-131">İyi bir örnek, kullanılabilirliği sürdürmek için yükseltme ve dağıtım mekanizmalarıyla birlikte çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="40538-131">A good example is working with upgrade and deployment mechanisms to maintain availability.</span></span> <span data-ttu-id="40538-132">Bir hizmet, işlem kilitlenmesi veya makinenin yeniden başlatılması nedeniyle şu anda sağlıksız olabilir, ancak hizmet hala çalışıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="40538-132">Although a service might currently be unhealthy due to a process crash or machine reboot, the service might still be operational.</span></span> <span data-ttu-id="40538-133">İhtiyacınız olan son şey, bir yükseltme gerçekleştirerek bunu daha kötü hale getirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="40538-133">The last thing you need is to make this worse by performing an upgrade.</span></span> <span data-ttu-id="40538-134">En iyi yaklaşım, önce araştırılması veya mikro hizmetin kurtarılması için zaman vermaktır.</span><span class="sxs-lookup"><span data-stu-id="40538-134">The best approach is to do an investigation first or allow time for the microservice to recover.</span></span> <span data-ttu-id="40538-135">Mikro bir hizmetten gelen sistem durumu olayları bilinçli kararlar almanıza ve etkili bir şekilde kendi kendine düzeltme hizmetleri oluşturmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="40538-135">Health events from a microservice help us make informed decisions and, in effect, help create self-healing services.</span></span>

<span data-ttu-id="40538-136">Bu kılavuzun [ASP.NET Core Hizmetleri bölümünde sistem durumu denetimleri uygulama](../implement-resilient-applications/monitor-app-health.md#implement-health-checks-in-aspnet-core-services) bölümünde, mikro hizmetinizdeki yeni bir ASP.net healthdenetimleri kitaplığının nasıl kullanılacağını açıklayacağız. bu sayede, uygun işlemleri gerçekleştirmek için durumunu bir izleme hizmetine bildirebilirler.</span><span class="sxs-lookup"><span data-stu-id="40538-136">In the [Implementing health checks in ASP.NET Core services](../implement-resilient-applications/monitor-app-health.md#implement-health-checks-in-aspnet-core-services) section of this guide, we explain how to use a new ASP.NET HealthChecks library in your microservices so they can report their state to a monitoring service to take appropriate actions.</span></span>

<span data-ttu-id="40538-137">Ayrıca [GitHub](https://github.com/Xabaril/BeatPulse) 'da ve bir [NuGet paketi](https://www.nuget.org/packages/BeatPulse/)olarak kullanılabilir olan uygun olmayan bir açık kaynaklı kitaplık kullanma seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="40538-137">You also have the option of using an excellent open-source library called Beat Pulse, available on [GitHub](https://github.com/Xabaril/BeatPulse) and as a [NuGet package](https://www.nuget.org/packages/BeatPulse/).</span></span> <span data-ttu-id="40538-138">Bu kitaplık Ayrıca sistem durumu denetimleri de yapar ve bu da iki tür denetimi işler:</span><span class="sxs-lookup"><span data-stu-id="40538-138">This library also does health checks, with a twist, it handles two types of checks:</span></span>

- <span data-ttu-id="40538-139">**Lida**: Mikro hizmetin etkin olup olmadığını denetler, diğer bir deyişle, istekleri kabul edebilir ve yanıtlayabilir.</span><span class="sxs-lookup"><span data-stu-id="40538-139">**Liveness**: Checks if the microservice is alive, that is, if it’s able to accept requests and respond.</span></span> 
- <span data-ttu-id="40538-140">**Hazırlık**: Mikro hizmetin bağımlılıklarının (veritabanı, kuyruk hizmetleri vb.) kendi kendine hazırlanın olup olmadığını denetler, bu nedenle mikro hizmet bunun yapması gerekenleri gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="40538-140">**Readiness**: Checks if the microservice's dependencies (Database, queue services, etc.) are themselves ready, so the microservice can do what it’s supposed to do.</span></span> 

### <a name="using-diagnostics-and-logs-event-streams"></a><span data-ttu-id="40538-141">Tanılama ve günlük olay akışlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="40538-141">Using diagnostics and logs event streams</span></span>

<span data-ttu-id="40538-142">Günlükler, özel durumlar, uyarılar ve basit bilgilendirici iletiler de dahil olmak üzere bir uygulama veya hizmetin nasıl çalıştığı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="40538-142">Logs provide information about how an application or service is running, including exceptions, warnings, and simple informational messages.</span></span> <span data-ttu-id="40538-143">Genellikle, her günlük olay başına tek satırlık bir metin biçiminde bulunur, ancak özel durumlar genellikle birden çok satırda yığın izlemesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="40538-143">Usually, each log is in a text format with one line per event, although exceptions also often show the stack trace across multiple lines.</span></span>

<span data-ttu-id="40538-144">Tek parçalı sunucu tabanlı uygulamalarda, günlükleri disk üzerindeki bir dosyaya (günlük dosyası) yazabilir ve ardından herhangi bir araçla çözümleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40538-144">In monolithic server-based applications, you can simply write logs to a file on disk (a logfile) and then analyze it with any tool.</span></span> <span data-ttu-id="40538-145">Uygulama yürütmesi bir sabit sunucu veya VM ile sınırlı olduğundan, genellikle olay akışını çözümlemek için çok karmaşık değildir.</span><span class="sxs-lookup"><span data-stu-id="40538-145">Since application execution is limited to a fixed server or VM, it generally isn't too complex to analyze the flow of events.</span></span> <span data-ttu-id="40538-146">Ancak, bir Orchestrator kümesindeki çok sayıda düğümde birden fazla hizmetin yürütüldüğü dağıtılmış bir uygulamada, dağıtılmış olayları ilişkilendirebilmek zor olur.</span><span class="sxs-lookup"><span data-stu-id="40538-146">However, in a distributed application where multiple services are executed across many nodes in an orchestrator cluster, being able to correlate distributed events is a challenge.</span></span>

<span data-ttu-id="40538-147">Mikro hizmet tabanlı bir uygulama, olayların veya günlük dosyalarının çıkış akışını tek başına depolamayı denememelidir, hatta olayların yönlendirilmesini merkezi bir yere yönetmeyi denememelidir.</span><span class="sxs-lookup"><span data-stu-id="40538-147">A microservice-based application should not try to store the output stream of events or logfiles by itself, and not even try to manage the routing of the events to a central place.</span></span> <span data-ttu-id="40538-148">Saydam olmalıdır, yani her bir işlemin olay akışını, altında çalıştığı yürütme ortamı altyapısı tarafından toplanacak standart bir çıkışa yazması gerekir.</span><span class="sxs-lookup"><span data-stu-id="40538-148">It should be transparent, meaning that each process should just write its event stream to a standard output that underneath will be collected by the execution environment infrastructure where it's running.</span></span> <span data-ttu-id="40538-149">Bu olay akışı yönlendiricilerine bir örnek, birden fazla kaynaktan gelen olay akışlarını toplayan ve çıkış sistemlerine yayımlayan [Microsoft. Diagnostic. EventFlow](https://github.com/Azure/diagnostics-eventflow)' dır.</span><span class="sxs-lookup"><span data-stu-id="40538-149">An example of these event stream routers is [Microsoft.Diagnostic.EventFlow](https://github.com/Azure/diagnostics-eventflow), which collects event streams from multiple sources and publishes it to output systems.</span></span> <span data-ttu-id="40538-150">Bunlar, bir geliştirme ortamı için basit standart çıkış veya [Azure izleyici](https://azure.microsoft.com/services/monitor//) ve [Azure tanılama](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostics-extension-overview)gibi bulut sistemleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="40538-150">These can include simple standard output for a development environment or cloud systems like [Azure Monitor](https://azure.microsoft.com/services/monitor//) and [Azure Diagnostics](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostics-extension-overview).</span></span> <span data-ttu-id="40538-151">Ayrıca, ara, uyarı, rapor ve [izleme gibi çok](https://www.splunk.com/goto/Splunk_Log_Management?ac=ga_usa_log_analysis_phrase_Mar17&_kk=logs%20analysis&gclid=CNzkzIrex9MCFYGHfgodW5YOtA)farklı üçüncü taraf Günlük Analizi platformları ve araçları, gerçek zamanlı olarak da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40538-151">There are also good third-party log analysis platforms and tools that can search, alert, report, and monitor logs, even in real time, like [Splunk](https://www.splunk.com/goto/Splunk_Log_Management?ac=ga_usa_log_analysis_phrase_Mar17&_kk=logs%20analysis&gclid=CNzkzIrex9MCFYGHfgodW5YOtA).</span></span>

### <a name="orchestrators-managing-health-and-diagnostics-information"></a><span data-ttu-id="40538-152">Sistem durumu ve tanılama bilgilerini yöneten düzenleyiciler</span><span class="sxs-lookup"><span data-stu-id="40538-152">Orchestrators managing health and diagnostics information</span></span>

<span data-ttu-id="40538-153">Mikro hizmet tabanlı bir uygulama oluşturduğunuzda karmaşıklıkla uğraşmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="40538-153">When you create a microservice-based application, you need to deal with complexity.</span></span> <span data-ttu-id="40538-154">Tabii ki tek bir mikro hizmet, ile uğraşmak için basittir, ancak onlarca veya yüzlerce tür ve mikro hizmetlerin binlerce örneği karmaşık bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="40538-154">Of course, a single microservice is simple to deal with, but dozens or hundreds of types and thousands of instances of microservices is a complex problem.</span></span> <span data-ttu-id="40538-155">Yalnızca mikro hizmet mimarinizi oluşturma hakkında bilgi sahibi olmak için, kararlı ve birbirine bağlı bir sisteme sahip olmak istiyorsanız yüksek kullanılabilirlik, adreslenebilirlik, dayanıklılık, sağlık ve Tanılamalar da gereklidir.</span><span class="sxs-lookup"><span data-stu-id="40538-155">It isn't just about building your microservice architecture—you also need high availability, addressability, resiliency, health, and diagnostics if you intend to have a stable and cohesive system.</span></span>

![Düzenleyiciler, mikro hizmetlerinizi çalıştırmaya yönelik bir destek platformu sağlar.](./media/image22.png)

<span data-ttu-id="40538-157">**Şekil 4-22**.</span><span class="sxs-lookup"><span data-stu-id="40538-157">**Figure 4-22**.</span></span> <span data-ttu-id="40538-158">Mikro hizmet platformu, bir uygulamanın sistem durumu yönetimi için temel</span><span class="sxs-lookup"><span data-stu-id="40538-158">A Microservice Platform is fundamental for an application's health management</span></span>

<span data-ttu-id="40538-159">Şekil 4-22 ' de gösterilen karmaşık sorunlar kendi başınıza çözülememektedir.</span><span class="sxs-lookup"><span data-stu-id="40538-159">The complex problems shown in Figure 4-22 are very hard to solve by yourself.</span></span> <span data-ttu-id="40538-160">Geliştirme ekipleri, mikro hizmet tabanlı yaklaşımlar sayesinde iş sorunlarının çözümüne ve özel uygulamalar oluşturmaya odaklanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="40538-160">Development teams should focus on solving business problems and building custom applications with microservice-based approaches.</span></span> <span data-ttu-id="40538-161">Karmaşık altyapı sorunlarını çözmeye odaklanmamalıdır; Bu durumda, mikro hizmet tabanlı uygulamaların maliyeti çok büyük olur.</span><span class="sxs-lookup"><span data-stu-id="40538-161">They should not focus on solving complex infrastructure problems; if they did, the cost of any microservice-based application would be huge.</span></span> <span data-ttu-id="40538-162">Bu nedenle, bir hizmet oluşturma ve çalıştırma ve altyapı kaynaklarını verimli bir şekilde kullanma hakkında Sabit sorunları çözmeye çalışan, düzenleyiciler veya mikro hizmet kümeleri olarak adlandırılan mikro hizmet odaklı platformlar vardır.</span><span class="sxs-lookup"><span data-stu-id="40538-162">Therefore, there are microservice-oriented platforms, referred to as orchestrators or microservice clusters, that try to solve the hard problems of building and running a service and using infrastructure resources efficiently.</span></span> <span data-ttu-id="40538-163">Bu, mikro hizmetler yaklaşımını kullanan uygulamalar oluşturmanın karmaşıklıklarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="40538-163">This reduces the complexities of building applications that use a microservices approach.</span></span>

<span data-ttu-id="40538-164">Farklı düzenleyiciler benzer şekilde değişebilir, ancak her biri tarafından sunulan tanılama ve sistem durumu denetimleri, sonraki bölümde açıklandığı gibi, işletim sistemi platformuna bağlı olarak, bazen işletim sisteminde ve durum durumunda farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="40538-164">Different orchestrators might sound similar, but the diagnostics and health checks offered by each of them differ in features and state of maturity, sometimes depending on the OS platform, as explained in the next section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40538-165">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="40538-165">Additional resources</span></span>

- <span data-ttu-id="40538-166">**On Iki öğeli uygulama. XI. Açıldığında Günlükleri olay akışları olarak işle** </span><span class="sxs-lookup"><span data-stu-id="40538-166">**The Twelve-Factor App. XI. Logs: Treat logs as event streams** </span></span>\
  <https://12factor.net/logs>

- <span data-ttu-id="40538-167">**Microsoft tanılama EventFlow kitaplığı** GitHub deposu.</span><span class="sxs-lookup"><span data-stu-id="40538-167">**Microsoft Diagnostic EventFlow Library** GitHub repo.</span></span> \
  <https://github.com/Azure/diagnostics-eventflow>

- <span data-ttu-id="40538-168">**Azure Tanılama nedir?**  </span><span class="sxs-lookup"><span data-stu-id="40538-168">**What is Azure Diagnostics** </span></span>\
  <https://docs.microsoft.com/azure/azure-diagnostics>

- <span data-ttu-id="40538-169">**Windows bilgisayarlarını Azure Izleyici hizmetine bağlama** </span><span class="sxs-lookup"><span data-stu-id="40538-169">**Connect Windows computers to the Azure Monitor service** </span></span>\
  <https://docs.microsoft.com/azure/azure-monitor/platform/agent-windows>

- <span data-ttu-id="40538-170">**Ne demek Istediğinizi günlüğe kaydetme: Anlam günlüğü uygulama bloğunu kullanma** </span><span class="sxs-lookup"><span data-stu-id="40538-170">**Logging What You Mean: Using the Semantic Logging Application Block** </span></span>\
  <https://docs.microsoft.com/previous-versions/msp-n-p/dn440729(v=pandp.60)>

- <span data-ttu-id="40538-171">**Splunk** Resmi site.</span><span class="sxs-lookup"><span data-stu-id="40538-171">**Splunk** Official site.</span></span> \
  <https://www.splunk.com/>

- <span data-ttu-id="40538-172">**EventSource sınıfı** Windows için olay izleme için API (ETW) </span><span class="sxs-lookup"><span data-stu-id="40538-172">**EventSource Class** API for events tracing for Windows (ETW) </span></span>\
  [https://docs.microsoft.com/dotnet/api/system.diagnostics.tracing.eventsource](xref:System.Diagnostics.Tracing.EventSource)

>[!div class="step-by-step"]
><span data-ttu-id="40538-173">[Önceki](microservice-based-composite-ui-shape-layout.md)İleri
>[](scalable-available-multi-container-microservice-applications.md)</span><span class="sxs-lookup"><span data-stu-id="40538-173">[Previous](microservice-based-composite-ui-shape-layout.md)
[Next](scalable-available-multi-container-microservice-applications.md)</span></span>