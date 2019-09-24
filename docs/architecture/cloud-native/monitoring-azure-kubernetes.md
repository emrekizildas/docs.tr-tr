---
title: Azure Kubernetes hizmetlerinde izleme
description: Azure Kubernetes hizmetlerinde izleme
ms.date: 09/23/2019
ms.openlocfilehash: 71192601eac2169db188b25da3dc91b71b860903
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184990"
---
# <a name="monitoring-in-azure-kubernetes-services"></a><span data-ttu-id="0b397-103">Azure Kubernetes hizmetlerinde izleme</span><span class="sxs-lookup"><span data-stu-id="0b397-103">Monitoring in Azure Kubernetes Services</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="0b397-104">Kubernetes 'te yerleşik günlük oluşturma basit bir.</span><span class="sxs-lookup"><span data-stu-id="0b397-104">The built-in logging in Kubernetes is primitive.</span></span> <span data-ttu-id="0b397-105">Ancak, günlükleri Kubernetes dışında ve düzgün çözümlenebilecekleri bir yere almak için bazı harika seçenekler vardır.</span><span class="sxs-lookup"><span data-stu-id="0b397-105">However, there are some great options for getting the logs out of Kubernetes and into a place where they can be properly analyzed.</span></span> <span data-ttu-id="0b397-106">AKS kümelerinizi izlemeniz gerekiyorsa, Kubernetes için elastik yığının yapılandırılması harika bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="0b397-106">If you need to monitor your AKS clusters, configuring Elastic Stack for Kubernetes is a great solution.</span></span>

## <a name="elastic-stack"></a><span data-ttu-id="0b397-107">Elastik yığın</span><span class="sxs-lookup"><span data-stu-id="0b397-107">Elastic Stack</span></span>

<span data-ttu-id="0b397-108">Elastik yığın, bir Kubernetes kümesinden bilgi toplamak için güçlü bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="0b397-108">The Elastic Stack is a powerful option for gathering information from a Kubernetes cluster.</span></span> <span data-ttu-id="0b397-109">Kubernetes, bir Elakes arama uç noktasına günlük göndermeyi destekler ve [çoğu bölüm](https://kubernetes.io/docs/tasks/debug-application-cluster/logging-elasticsearch-kibana/)Için, Şekil 7-5 ' de gösterildiği gibi, ortam değişkenlerini ayarlamak gerekir:</span><span class="sxs-lookup"><span data-stu-id="0b397-109">Kubernetes supports sending logs to an Elasticsearch endpoint, and for the [most part](https://kubernetes.io/docs/tasks/debug-application-cluster/logging-elasticsearch-kibana/), all you need to get started is to set the environment variables as shown in Figure 7-5:</span></span>

```kubernetes
KUBE_LOGGING_DESTINATION=elasticsearch
KUBE_ENABLE_NODE_LOGGING=true
```

<span data-ttu-id="0b397-110">**Şekil 7-5** -Kubernetes için yapılandırma değişkenleri</span><span class="sxs-lookup"><span data-stu-id="0b397-110">**Figure 7-5** - Configuration variables for Kubernetes</span></span>

<span data-ttu-id="0b397-111">Bu, küme üzerinde elaa araması yükleyecek ve tüm küme günlüklerini buna gönderen hedeflenecek.</span><span class="sxs-lookup"><span data-stu-id="0b397-111">This will install Elasticsearch on the cluster and target sending all the cluster logs to it.</span></span>

<span data-ttu-id="0b397-112">![Kubernetes](./media/kibana-dashboard.png)
**Şekil 7-6**' den alınan günlüklere yönelik bir sorgunun sonuçlarını gösteren bir kibana panosu örneği.</span><span class="sxs-lookup"><span data-stu-id="0b397-112">![An example of a Kibana dashboard showing the results of a query against logs ingested from Kubernetes](./media/kibana-dashboard.png)
**Figure 7-6**.</span></span> <span data-ttu-id="0b397-113">Kubernetes 'ten alınan günlüklere yönelik bir sorgunun sonuçlarını gösteren bir kibana panosu örneği</span><span class="sxs-lookup"><span data-stu-id="0b397-113">An example of a Kibana dashboard showing the results of a query against logs that are ingested from Kubernetes</span></span>

## <a name="azure-container-monitoring"></a><span data-ttu-id="0b397-114">Azure Kapsayıcı Izleme</span><span class="sxs-lookup"><span data-stu-id="0b397-114">Azure Container Monitoring</span></span>

<span data-ttu-id="0b397-115">Azure Container Monitoring yalnızca Kubernetes değil, DC/OS, Docker Sısınma ve Red Hat OpenShift gibi diğer düzenleme altyapılarından günlük kullanmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="0b397-115">Azure Container Monitoring supports consuming logs from not just Kubernetes but also from other orchestration engines such as DC/OS, Docker Swarm, and Red Hat OpenShift.</span></span>

<span data-ttu-id="0b397-116">![Çeşitli kapsayıcılardan](./media/containers-diagram.png)
günlükleri kullanma**Şekil 7-7**.</span><span class="sxs-lookup"><span data-stu-id="0b397-116">![Consuming logs from various containers](./media/containers-diagram.png)
**Figure 7-7**.</span></span>  <span data-ttu-id="0b397-117">Çeşitli kapsayıcılardan günlükleri kullanma</span><span class="sxs-lookup"><span data-stu-id="0b397-117">Consuming logs from various containers</span></span>

<span data-ttu-id="0b397-118">Günlük ve ölçüm bilgileri yalnızca kümede çalışan kapsayıcılardan değil, küme konaklarından da toplanır.</span><span class="sxs-lookup"><span data-stu-id="0b397-118">Log and metric information is gathered not just from the containers running in the cluster but also from the cluster hosts themselves.</span></span> <span data-ttu-id="0b397-119">Bu, bir hatayı daha kolay bir şekilde izlemek için, günlük bilgilerinin iki ' dan daha kolay olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b397-119">It allows correlating log information from the two making it much easier to track down an error.</span></span>

<span data-ttu-id="0b397-120">Günlük toplayıcıların yüklenmesi [Windows](https://docs.microsoft.com/azure/azure-monitor/insights/containers#configure-a-log-analytics-windows-agent-for-kubernetes) ve [Linux](https://docs.microsoft.com/azure/azure-monitor/insights/containers#configure-a-log-analytics-linux-agent-for-kubernetes) kümelerine göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="0b397-120">Installing the log collectors differs on [Windows](https://docs.microsoft.com/azure/azure-monitor/insights/containers#configure-a-log-analytics-windows-agent-for-kubernetes) and [Linux](https://docs.microsoft.com/azure/azure-monitor/insights/containers#configure-a-log-analytics-linux-agent-for-kubernetes) clusters.</span></span> <span data-ttu-id="0b397-121">Ancak her iki durumda da günlük koleksiyonu bir Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)olarak uygulanır. Bu, günlük toplayıcının düğümlerin her birinde bir kapsayıcı olarak çalıştırıldığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0b397-121">But in both cases the log collection is implemented as a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), meaning that the log collector is run as a container on each of the nodes.</span></span>

<span data-ttu-id="0b397-122">Hangi Orchestrator veya işletim sisteminin Azure Izleyici arka plan programını çalıştırıyor olduğuna bakılmaksızın, günlük bilgileri kullanıcıların tanıdık olduğu Azure Izleyici araçlarına iletilir.</span><span class="sxs-lookup"><span data-stu-id="0b397-122">No matter which orchestrator or operating system is running the Azure Monitor daemon, the log information is forwarded to the same Azure Monitor tools with which users are familiar.</span></span> <span data-ttu-id="0b397-123">Bu, karma bir Kubernetes/Azure Işlevleri ortamı gibi farklı günlük kaynaklarını karıştırarak oluşan ortamlarda paralel bir deneyim sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b397-123">This ensures a parallel experience in environments that mix different log sources such as a hybrid Kubernetes/Azure Functions environment.</span></span>

<span data-ttu-id="0b397-124">![Bir dizi çalışan kapsayıcıyı günlüğe kaydetme ve ölçüm bilgilerini gösteren örnek bir Pano. **Şekil 7-8**. ](./media/containers-dashboard.png)
</span><span class="sxs-lookup"><span data-stu-id="0b397-124">![A sample dashboard showing logging and metric information from a number of running containers.](./media/containers-dashboard.png)
**Figure 7-8**.</span></span> <span data-ttu-id="0b397-125">Bir dizi çalışan kapsayıcıyı günlüğe kaydetme ve ölçüm bilgilerini gösteren örnek bir Pano.</span><span class="sxs-lookup"><span data-stu-id="0b397-125">A sample dashboard showing logging and metric information from a number of running containers.</span></span>

## <a name="logfinalize"></a><span data-ttu-id="0b397-126">Log. Finalize ()</span><span class="sxs-lookup"><span data-stu-id="0b397-126">Log.Finalize()</span></span>

<span data-ttu-id="0b397-127">Günlüğe kaydetme, her türlü uygulamayı ölçeklendirmenin en fazla ve en önemli bölümlerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="0b397-127">Logging is one of the most overlooked and yet most important parts of deploying any application at scale.</span></span> <span data-ttu-id="0b397-128">Uygulamaların boyutu ve karmaşıklığı artdıkça, bunları hata ayıklamanın zorluğunu ortadan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="0b397-128">As the size and complexity of applications increase, then so does the difficulty of debugging them.</span></span> <span data-ttu-id="0b397-129">Kullanılabilir en yüksek kaliteli günlüklere sahip olmak, hata ayıklamayı çok daha kolay hale getirir ve "neredeyse olanaksız" olarak "bir Pleasant deneyimi" bölgesine taşımaktır.</span><span class="sxs-lookup"><span data-stu-id="0b397-129">Having top quality logs available makes debugging much easier and moves it from the realm of "nearly impossible" to "a pleasant experience".</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="0b397-130">[Önceki](logging-with-elastic-stack.md)
>[İleri](azure-monitor.md)</span><span class="sxs-lookup"><span data-stu-id="0b397-130">[Previous](logging-with-elastic-stack.md)
[Next](azure-monitor.md)</span></span>