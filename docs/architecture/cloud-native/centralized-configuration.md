---
title: Merkezi yapılandırma
description: Azure Key Vault kullanan merkezi yapılandırma, bulutta yerel uygulamaların yönetilmesini kolaylaştırabilir.
ms.date: 06/30/2019
ms.openlocfilehash: 4c516b6773d913acd71ff06742302e9766a141e2
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71214001"
---
# <a name="centralized-configuration"></a><span data-ttu-id="9228a-103">Merkezi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9228a-103">Centralized configuration</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="9228a-104">Bulutta yerel uygulamalar geleneksel tek örnekli tek parçalı uygulamalar 'dan daha fazla çalışan çok sayıda hizmet içerir.</span><span class="sxs-lookup"><span data-stu-id="9228a-104">Cloud-native applications involve many more running services than traditional single-instance monolithic apps.</span></span> <span data-ttu-id="9228a-105">Birbirine bağlı onlarca hizmet veren hizmetlerin yapılandırma ayarlarını yönetmek zor olabilir, bu nedenle merkezi yapılandırma depoları genellikle dağıtılmış uygulamalar için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="9228a-105">Managing configuration settings for dozens of interdependent services can be challenging, which is why centralized configuration stores are often implemented for distributed applications.</span></span>

<span data-ttu-id="9228a-106">[Bölüm 1](introduction.md)' de anlatıldığı gibi, on Iki öğeli uygulama önerileri, kod ve yapılandırma arasında katı ayrım gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9228a-106">As discussed in [Chapter 1](introduction.md), the Twelve-Factor App recommendations require strict separation between code and configuration.</span></span> <span data-ttu-id="9228a-107">Bu, yapılandırma ayarlarının sabitler olarak depolanması veya koddaki değişmez değerlerin bir ihlalin olması anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9228a-107">This means storing configuration settings as constants or literal values in code is a violation.</span></span> <span data-ttu-id="9228a-108">Geliştirme, test, hazırlama ve üretim dahil olmak üzere birden çok ortamda aynı kodun kullanılması gerektiğinden bu öneri vardır.</span><span class="sxs-lookup"><span data-stu-id="9228a-108">This recommendation exists because the same code should be used across multiple environments, including development, testing, staging, and production.</span></span> <span data-ttu-id="9228a-109">Ancak, yapılandırma değerleri bu ortamların her biri arasında farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="9228a-109">However, configuration values are likely to vary between each of these environments.</span></span> <span data-ttu-id="9228a-110">Bu nedenle, yapılandırma değerleri ortamın kendisinde depolanmalıdır veya ortamın kimlik bilgilerini merkezi bir yapılandırma deposuna depolaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9228a-110">So, configuration values should be stored in the environment itself, or the environment should store the credentials to a centralized configuration store.</span></span>

<span data-ttu-id="9228a-111">EShopOnContainers uygulaması, her mikro hizmetle yerel uygulama ayarları dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="9228a-111">The eShopOnContainers application includes local application settings files with each microservice.</span></span> <span data-ttu-id="9228a-112">Bu dosyalar kaynak denetimine iade edilir ancak bağlantı dizeleri veya API anahtarları gibi üretim sırları dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="9228a-112">These files are checked into source control but don't include production secrets such as connection strings or API keys.</span></span> <span data-ttu-id="9228a-113">Üretimde, hizmet başına ortam değişkenleriyle bireysel ayarların üzerine yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="9228a-113">In production, individual settings may be overwritten with per-service environment variables.</span></span> <span data-ttu-id="9228a-114">Bu, barındırılan uygulamalar için yaygın bir uygulamadır, ancak merkezi bir yapılandırma deposu sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="9228a-114">This is a common practice for hosted applications, but doesn't provide a central configuration store.</span></span> <span data-ttu-id="9228a-115">Yapılandırma ayarlarının merkezi yönetimini desteklemek için her mikro hizmet, yerel ayarları veya Azure Key Vault ayarları kullanımı arasında geçiş yapmak için bir ayar içerir.</span><span class="sxs-lookup"><span data-stu-id="9228a-115">To support centralized management of configuration settings, each microservice includes a setting to toggle between its use of local settings or Azure Key Vault settings.</span></span>

## <a name="azure-key-vault"></a><span data-ttu-id="9228a-116">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9228a-116">Azure Key Vault</span></span>

<span data-ttu-id="9228a-117">Azure Key Vault, belirteçlerin, parolaların, sertifikaların, API anahtarlarının ve diğer gizli parolaların güvenli bir şekilde depolanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9228a-117">Azure Key Vault provides secure storage of tokens, passwords, certificates, API keys, and other sensitive secrets.</span></span> <span data-ttu-id="9228a-118">Key Vault erişim, eShopOnContainers mikro hizmetleri için bir ClientID/ClientSecret bileşiminin kullanılması gereken, uygun bir arayan kimlik doğrulaması ve yetkilendirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9228a-118">Access to Key Vault requires proper caller authentication and authorization, which in the case of the eShopOnContainers microservices means the use of a ClientId/ClientSecret combination.</span></span> <span data-ttu-id="9228a-119">Bu kimlik bilgilerini kaynak denetimine iade etmeyin, ancak bunun yerine uygulamanın ortamında ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9228a-119">Don't check in these credentials into source control, but instead set in the application's environment.</span></span> <span data-ttu-id="9228a-120">AKS 'ten Key Vault doğrudan erişim, [Key Vault FlexVolume](https://github.com/Azure/kubernetes-keyvault-flexvol)kullanılarak elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="9228a-120">Direct access to Key Vault from AKS can be achieved using [Key Vault FlexVolume](https://github.com/Azure/kubernetes-keyvault-flexvol).</span></span>

<span data-ttu-id="9228a-121">Merkezi yapılandırma sayesinde, Merkezi günlük uç noktası gibi tüm uygulama için uygulanan ayarlar bir kez ayarlanabilir ve Dağıtılmış uygulamanın her bölümü tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9228a-121">With centralized configuration, settings that apply to the entire application, such as the centralized logging endpoint, can be set once and used by every part of the distributed application.</span></span> <span data-ttu-id="9228a-122">Mikro hizmetlerin bir diğerinden bağımsız olması gerekse de, yapılandırma ayrıntıları merkezi bir yapılandırma deposundan faydalanabilir bazı paylaşılan bağımlılıklar de vardır.</span><span class="sxs-lookup"><span data-stu-id="9228a-122">Although microservices should be independent of one another, there will typically still be some shared dependencies whose configuration details can benefit from a centralized configuration store.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="9228a-123">[Önceki](deploy-eshoponcontainers-azure.md)
>[İleri](scale-applications.md)</span><span class="sxs-lookup"><span data-stu-id="9228a-123">[Previous](deploy-eshoponcontainers-azure.md)
[Next](scale-applications.md)</span></span>