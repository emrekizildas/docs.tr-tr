---
title: Bağımlılık yükleme-.NET Core
description: .NET Core 'da yönetilen ve yönetilmeyen bağımlılık yüklemeye genel bakış
ms.date: 08/09/2019
author: sdmaclea
ms.author: stmaclea
ms.topic: overview
ms.openlocfilehash: 69cca28606c64479d500e731ba95fe404bea38df
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70017334"
---
# <a name="dependency-loading-in-net-core"></a><span data-ttu-id="bad79-103">.NET Core 'da bağımlılık yükleme</span><span class="sxs-lookup"><span data-stu-id="bad79-103">Dependency loading in .NET Core</span></span>

<span data-ttu-id="bad79-104">Her .NET Core uygulamasının bağımlılıkları vardır.</span><span class="sxs-lookup"><span data-stu-id="bad79-104">Every .NET Core application has dependencies.</span></span> <span data-ttu-id="bad79-105">Basit `hello world` uygulamanın, .NET Core sınıf kitaplıklarının bölümlerine bağımlılıklar de vardır.</span><span class="sxs-lookup"><span data-stu-id="bad79-105">Even the simple `hello world` app has dependencies on portions of the .NET Core class libraries.</span></span>

<span data-ttu-id="bad79-106">.NET Core varsayılan derleme yükleme mantığını anlamak, tipik dağıtım sorunlarının anlaşılmasına ve hata ayıklamasına yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bad79-106">Understanding .NET Core default assembly loading logic can help understanding and debugging typical deployment issues.</span></span>

<span data-ttu-id="bad79-107">Bazı uygulamalarda bağımlılıklar, çalışma zamanında dinamik olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="bad79-107">In some applications, dependencies are dynamically determined at runtime.</span></span> <span data-ttu-id="bad79-108">Bu durumlarda, yönetilen derlemelerin ve yönetilmeyen bağımlılıkların nasıl yüklendiğini anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="bad79-108">In these situations, it's critical to understand how managed assemblies and unmanaged dependencies are loaded.</span></span>

## <a name="understanding-assemblyloadcontext"></a><span data-ttu-id="bad79-109">AssemblyLoadContext 'i anlama</span><span class="sxs-lookup"><span data-stu-id="bad79-109">Understanding AssemblyLoadContext</span></span>

<span data-ttu-id="bad79-110"><xref:System.Runtime.Loader.AssemblyLoadContext> API, .NET Core yükleme tasarımına yönelik olarak tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bad79-110">The <xref:System.Runtime.Loader.AssemblyLoadContext> API is central to the .NET Core loading design.</span></span> <span data-ttu-id="bad79-111">[AssemblyLoadContext 'ı anlama](understanding-assemblyloadcontext.md) makalesi, tasarıma kavramsal bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="bad79-111">The [Understanding AssemblyLoadContext](understanding-assemblyloadcontext.md) article provides a conceptual overview to the design.</span></span>

## <a name="loading-details"></a><span data-ttu-id="bad79-112">Ayrıntılar yükleniyor</span><span class="sxs-lookup"><span data-stu-id="bad79-112">Loading details</span></span>

<span data-ttu-id="bad79-113">Yükleme algoritması ayrıntıları birkaç makalede kısaca ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="bad79-113">The loading algorithm details are covered briefly in several articles:</span></span>
- [<span data-ttu-id="bad79-114">Yönetilen derleme yükleme algoritması</span><span class="sxs-lookup"><span data-stu-id="bad79-114">Managed assembly loading algorithm</span></span>](loading-managed.md)
- [<span data-ttu-id="bad79-115">Uydu derleme yükleme algoritması</span><span class="sxs-lookup"><span data-stu-id="bad79-115">Satellite assembly loading algorithm</span></span>](loading-resources.md)
- [<span data-ttu-id="bad79-116">Yönetilmeyen (yerel) kitaplık yükleme algoritması</span><span class="sxs-lookup"><span data-stu-id="bad79-116">Unmanaged (native) library loading algorithm</span></span>](loading-unmanaged.md)
- [<span data-ttu-id="bad79-117">Varsayılan yoklama</span><span class="sxs-lookup"><span data-stu-id="bad79-117">Default probing</span></span>](default-probing.md)

## <a name="create-a-net-core-application-with-plugins"></a><span data-ttu-id="bad79-118">Eklentilerle .NET Core uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="bad79-118">Create a .NET Core application with plugins</span></span>

<span data-ttu-id="bad79-119">[Eklentilerle bir .NET Core uygulaması oluşturma](../tutorials/creating-app-with-plugin-support.md) öğreticisi, özel bir AssemblyLoadContext oluşturmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="bad79-119">The tutorial [Create a .NET Core application with plugins](../tutorials/creating-app-with-plugin-support.md) describes how to create a custom AssemblyLoadContext.</span></span> <span data-ttu-id="bad79-120">Eklentinin bağımlılıklarını çözümlemek <xref:System.Runtime.Loader.AssemblyDependencyResolver> için bir kullanır.</span><span class="sxs-lookup"><span data-stu-id="bad79-120">It uses an <xref:System.Runtime.Loader.AssemblyDependencyResolver> to resolve the dependencies of the plugin.</span></span> <span data-ttu-id="bad79-121">Öğretici, eklentinin bağımlılıklarını barındırma uygulamasından doğru şekilde yalıtır.</span><span class="sxs-lookup"><span data-stu-id="bad79-121">The tutorial correctly isolates the plugin's dependencies from the hosting application.</span></span>

## <a name="how-to-use-and-debug-assembly-unloadability-in-net-core"></a><span data-ttu-id="bad79-122">.NET Core’da kaldırabilme özelliğini kullanma ve hatalarını ayıklama</span><span class="sxs-lookup"><span data-stu-id="bad79-122">How to use and debug assembly unloadability in .NET Core</span></span>

<span data-ttu-id="bad79-123">[.NET Core makalesindeki derleme ve hata ayıklama bütünleştirilmiş kodu kullanımı](../../standard/assembly/unloadability-howto.md) , adım adım öğreticidir.</span><span class="sxs-lookup"><span data-stu-id="bad79-123">The [How to use and debug assembly unloadability in .NET Core](../../standard/assembly/unloadability-howto.md) article is a step-by-step tutorial.</span></span> <span data-ttu-id="bad79-124">.NET Core uygulamasını yüklemeyi, çalıştırmayı ve sonra kaldırmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="bad79-124">It shows how to load a .NET Core application, execute, and then unload it.</span></span> <span data-ttu-id="bad79-125">Makalede ayrıca hata ayıklama ipuçları sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bad79-125">The article also provides debugging tips.</span></span>