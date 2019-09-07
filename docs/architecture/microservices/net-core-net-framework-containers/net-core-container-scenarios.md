---
title: Docker kapsayıcıları için ne zaman .NET Core seçilmelidir?
description: Kapsayıcılı .NET uygulamaları için .NET mikro hizmetleri mimarisi | Docker kapsayıcıları için ne zaman .NET Core seçme
ms.date: 09/11/2018
ms.openlocfilehash: 54ed1b4bbb16352b8c99204383f85ffb25d62be7
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/30/2019
ms.locfileid: "70296502"
---
# <a name="when-to-choose-net-core-for-docker-containers"></a><span data-ttu-id="e889b-103">Docker kapsayıcıları için ne zaman .NET Core seçilmelidir?</span><span class="sxs-lookup"><span data-stu-id="e889b-103">When to choose .NET Core for Docker containers</span></span>

<span data-ttu-id="e889b-104">.NET Core 'un modülerliği ve hafif doğası, kapsayıcılar için kusursuz hale getirir.</span><span class="sxs-lookup"><span data-stu-id="e889b-104">The modularity and lightweight nature of .NET Core makes it perfect for containers.</span></span> <span data-ttu-id="e889b-105">Bir kapsayıcı dağıtırken ve başlattığınızda, bu görüntü, .NET Framework .NET Core ile çok daha küçüktür.</span><span class="sxs-lookup"><span data-stu-id="e889b-105">When you deploy and start a container, its image is far smaller with .NET Core than with .NET Framework.</span></span> <span data-ttu-id="e889b-106">Buna karşılık, bir kapsayıcı için .NET Framework kullanmak için görüntünüzü, .NET Core için kullandığınız Windows nano Server veya Linux görüntülerinden çok daha ağır olan Windows Server Core görüntüsüne dayandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e889b-106">In contrast, to use .NET Framework for a container, you must base your image on the Windows Server Core image, which is a lot heavier than the Windows Nano Server or Linux images that you use for .NET Core.</span></span>

<span data-ttu-id="e889b-107">Ayrıca, .NET Core, Linux veya Windows kapsayıcı görüntüleriyle sunucu uygulamaları dağıtabilmeniz için platformlar arası bir platformdur.</span><span class="sxs-lookup"><span data-stu-id="e889b-107">Additionally, .NET Core is cross-platform, so you can deploy server apps with Linux or Windows container images.</span></span> <span data-ttu-id="e889b-108">Ancak geleneksel .NET Framework kullanıyorsanız, yalnızca Windows Server Core tabanlı görüntüleri dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e889b-108">However, if you are using the traditional .NET Framework, you can only deploy images based on Windows Server Core.</span></span>

<span data-ttu-id="e889b-109">Aşağıda .NET Core 'un neden seçmesinin daha ayrıntılı bir açıklaması verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e889b-109">The following is a more detailed explanation of why to choose .NET Core.</span></span>

## <a name="developing-and-deploying-cross-platform"></a><span data-ttu-id="e889b-110">Platformlar arası geliştirme ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="e889b-110">Developing and deploying cross platform</span></span>

<span data-ttu-id="e889b-111">Açık olarak, amacınız Docker (Linux ve Windows) tarafından desteklenen birden çok platformda çalışabilen bir uygulamaya (Web uygulaması veya hizmet) sahip olmak için, .NET Framework yalnızca Windows 'u desteklediğinden, sağ tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="e889b-111">Clearly, if your goal is to have an application (web app or service) that can run on multiple platforms supported by Docker (Linux and Windows), the right choice is .NET Core, because .NET Framework only supports Windows.</span></span>

<span data-ttu-id="e889b-112">.NET Core Ayrıca, macOS 'ı bir geliştirme platformu olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="e889b-112">.NET Core also supports macOS as a development platform.</span></span> <span data-ttu-id="e889b-113">Ancak, bir Docker konağına kapsayıcı dağıttığınızda, bu ana bilgisayar Linux veya Windows 'u temel almalıdır (Şu anda).</span><span class="sxs-lookup"><span data-stu-id="e889b-113">However, when you deploy containers to a Docker host, that host must (currently) be based on Linux or Windows.</span></span> <span data-ttu-id="e889b-114">Örneğin, bir geliştirme ortamında, Mac üzerinde çalışan bir Linux sanal makinesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e889b-114">For example, in a development environment, you could use a Linux VM running on a Mac.</span></span>

<span data-ttu-id="e889b-115">[Visual Studio](https://www.visualstudio.com/vs/) , Windows için tümleşik bir geliştirme ORTAMı (IDE) sağlar ve Docker geliştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="e889b-115">[Visual Studio](https://www.visualstudio.com/vs/) provides an integrated development environment (IDE) for Windows and supports Docker development.</span></span>

<span data-ttu-id="e889b-116">[Mac için Visual Studio](https://www.visualstudio.com/vs/visual-studio-mac/) , MacOS üzerinde çalışan ve Docker tabanlı uygulama geliştirmeyi destekleyen Xamarin Studio evrimi olan bir IDE 'dir.</span><span class="sxs-lookup"><span data-stu-id="e889b-116">[Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/) is an IDE, evolution of Xamarin Studio, that runs on macOS and supports Docker-based application development.</span></span> <span data-ttu-id="e889b-117">Bu, güçlü bir IDE kullanmak isteyen Mac makinelerde çalışan geliştiriciler için tercih edilen seçim olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e889b-117">This should be the preferred choice for developers working in Mac machines who also want to use a powerful IDE.</span></span>

<span data-ttu-id="e889b-118">MacOS, Linux ve Windows üzerinde [Visual Studio Code](https://code.visualstudio.com/) (vs Code) de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e889b-118">You can also use [Visual Studio Code](https://code.visualstudio.com/) (VS Code) on macOS, Linux, and Windows.</span></span> <span data-ttu-id="e889b-119">VS Code IntelliSense ve hata ayıklama dahil .NET Core 'u tam olarak destekler.</span><span class="sxs-lookup"><span data-stu-id="e889b-119">VS Code fully supports .NET Core, including IntelliSense and debugging.</span></span> <span data-ttu-id="e889b-120">VS Code basit bir düzenleyici olduğundan, Docker CLı ve [.NET Core komut satırı arabirimi (CLI)](../../../core/tools/index.md)Ile birlikte Mac üzerinde Kapsayıcılı uygulamalar geliştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e889b-120">Because VS Code is a lightweight editor, you can use it to develop containerized apps on the Mac in conjunction with the Docker CLI and the [.NET Core command-line interface (CLI)](../../../core/tools/index.md).</span></span> <span data-ttu-id="e889b-121">Ayrıca, IntelliSense desteği sağlayan alt Lime, Emacs, VI ve açık kaynaklı OmniSharp projesi gibi üçüncü taraf düzenleyicilerle de .NET Core 'u hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e889b-121">You can also target .NET Core with most third-party editors like Sublime, Emacs, vi, and the open-source OmniSharp project, which also provides IntelliSense support.</span></span>

<span data-ttu-id="e889b-122">Ides ve düzenleyicilere ek olarak, desteklenen tüm platformlar için [.NET Core CLI](../../../core/tools/index.md) araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e889b-122">In addition to the IDEs and editors, you can use the [.NET Core CLI](../../../core/tools/index.md) tools for all supported platforms.</span></span>

## <a name="using-containers-for-new-green-field-projects"></a><span data-ttu-id="e889b-123">Yeni ("yeşil-alan") projeler için kapsayıcıları kullanma</span><span class="sxs-lookup"><span data-stu-id="e889b-123">Using containers for new ("green-field") projects</span></span>

<span data-ttu-id="e889b-124">Kapsayıcılar genellikle bir mikro hizmet mimarisi ile birlikte kullanılır, ancak her türlü mimari kalıbı izleyen Web uygulamalarını veya hizmetlerini kapsayıtabilecek de kullanılabilirler.</span><span class="sxs-lookup"><span data-stu-id="e889b-124">Containers are commonly used in conjunction with a microservices architecture, although they can also be used to containerize web apps or services that follow any architectural pattern.</span></span> <span data-ttu-id="e889b-125">Windows kapsayıcılarında .NET Framework kullanabilirsiniz, ancak .NET Core 'un modülerliği ve hafif doğası, kapsayıcılar ve mikro hizmet mimarileri için mükemmel hale getirir.</span><span class="sxs-lookup"><span data-stu-id="e889b-125">You can use .NET Framework on Windows Containers, but the modularity and lightweight nature of .NET Core makes it perfect for containers and microservices architectures.</span></span> <span data-ttu-id="e889b-126">Bir kapsayıcı oluşturduğunuzda ve dağıttığınızda, bu görüntü .NET Core ile .NET Framework göre daha küçüktür.</span><span class="sxs-lookup"><span data-stu-id="e889b-126">When you create and deploy a container, its image is far smaller with .NET Core than with .NET Framework.</span></span>

## <a name="creating-and-deploying-microservices-on-containers"></a><span data-ttu-id="e889b-127">Kapsayıcılar üzerinde mikro hizmetler oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="e889b-127">Creating and deploying microservices on containers</span></span>

<span data-ttu-id="e889b-128">Düz süreçler kullanarak mikro hizmet tabanlı uygulamalar (kapsayıcılar olmadan) oluşturmak için geleneksel .NET Framework kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e889b-128">You could use the traditional .NET Framework for building microservices-based applications (without containers) by using plain processes.</span></span> <span data-ttu-id="e889b-129">Bu şekilde, .NET Framework zaten yüklenmiş ve süreçler genelinde paylaşıldığı için, süreçler hafif ve hızlı bir şekilde başlatılır.</span><span class="sxs-lookup"><span data-stu-id="e889b-129">That way, because the .NET Framework is already installed and shared across processes, processes are light and fast to start.</span></span> <span data-ttu-id="e889b-130">Ancak kapsayıcıları kullanıyorsanız, geleneksel .NET Framework görüntüsü de Windows Server Core ' a dayalıdır ve bu, mikro hizmetler arası bir yaklaşım için çok daha ağır hale gelir.</span><span class="sxs-lookup"><span data-stu-id="e889b-130">However, if you are using containers, the image for the traditional .NET Framework is also based on Windows Server Core and that makes it too heavy for a microservices-on-containers approach.</span></span>

<span data-ttu-id="e889b-131">Buna karşılık, .NET Core basit olduğundan, kapsayıcıları temel alan mikro hizmetlere dayalı bir sistemi benimseme konusunda .NET Core en iyi adaydır.</span><span class="sxs-lookup"><span data-stu-id="e889b-131">In contrast, .NET Core is the best candidate if you are embracing a microservices-oriented system that is based on containers, because .NET Core is lightweight.</span></span> <span data-ttu-id="e889b-132">Bunlara ek olarak, Linux görüntüsü veya Windows nano görüntüsü olan ilişkili kapsayıcı görüntüleri, her ikisi de açık ve hızlı bir şekilde kaplar ve hızla başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="e889b-132">In addition, its related container images, either the Linux image or the Windows Nano image, are lean and small making containers light and fast to start.</span></span>

<span data-ttu-id="e889b-133">Mikro hizmet mümkün olduğunca küçük olacak şekilde, küçük bir parmak izine sahip olmak, küçük bir [ilgi alanına sahip](https://en.wikipedia.org/wiki/Domain-driven_design)olmak, küçük bir sorun olduğunu göstermek ve hızlı bir şekilde başlayabilmek ve durdurmak için en az bir değer olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="e889b-133">A microservice is meant to be as small as possible: to be light when spinning up, to have a small footprint, to have a small Bounded Context (check DDD, [Domain-Driven Design](https://en.wikipedia.org/wiki/Domain-driven_design)), to represent a small area of concerns, and to be able to start and stop fast.</span></span> <span data-ttu-id="e889b-134">Bu gereksinimler için, .NET Core kapsayıcı görüntüsü gibi küçük ve hızlı-örnek oluşturma kapsayıcı görüntülerini kullanmak isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e889b-134">For those requirements, you will want to use small and fast-to-instantiate container images like the .NET Core container image.</span></span>

<span data-ttu-id="e889b-135">Mikro hizmetler mimarisi Ayrıca bir hizmet sınırı genelinde teknolojileri karıştırabilmeniz için de sağlar.</span><span class="sxs-lookup"><span data-stu-id="e889b-135">A microservices architecture also allows you to mix technologies across a service boundary.</span></span> <span data-ttu-id="e889b-136">Bu, diğer mikro hizmetlerle birlikte çalışan yeni mikro hizmetler veya Node. js, Python, Java, GoLang veya diğer teknolojiler ile geliştirilen hizmetler için aşamalı olarak .NET Core 'a geçiş sağlar.</span><span class="sxs-lookup"><span data-stu-id="e889b-136">This enables a gradual migration to .NET Core for new microservices that work in conjunction with other microservices or with services developed with Node.js, Python, Java, GoLang, or other technologies.</span></span>

## <a name="deploying-high-density-in-scalable-systems"></a><span data-ttu-id="e889b-137">Ölçeklenebilir sistemlerde yüksek yoğunluklu dağıtım</span><span class="sxs-lookup"><span data-stu-id="e889b-137">Deploying high density in scalable systems</span></span>

<span data-ttu-id="e889b-138">Kapsayıcı tabanlı sisteminizin en iyi yoğunluğu, ayrıntı düzeyi ve performansa ihtiyacı olduğunda, .NET Core ve ASP.NET Core en iyi seçenekleriniz vardır.</span><span class="sxs-lookup"><span data-stu-id="e889b-138">When your container-based system needs the best possible density, granularity, and performance, .NET Core and ASP.NET Core are your best options.</span></span> <span data-ttu-id="e889b-139">ASP.NET Core geleneksel .NET Framework en fazla on kat daha hızlıdır ve bu, bilinen mikro hizmetler için Java servinler, Go ve Node. js gibi diğer popüler sektör teknolojilerini de sağlar.</span><span class="sxs-lookup"><span data-stu-id="e889b-139">ASP.NET Core is up to ten times faster than ASP.NET in the traditional .NET Framework, and it leads other popular industry technologies for microservices, such as Java servlets, Go, and Node.js.</span></span>

<span data-ttu-id="e889b-140">Bu özellikle, yüzlerce mikro hizmet (kapsayıcı) çalıştırdığınız mikro hizmet mimarileri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e889b-140">This is especially relevant for microservices architectures, where you could have hundreds of microservices (containers) running.</span></span> <span data-ttu-id="e889b-141">Linux veya Windows nano 'daki ASP.NET Core görüntülerle (.NET Core çalışma zamanına bağlı olarak), sisteminizi çok daha az sayıda sunucu veya VM ile çalıştırarak, son olarak altyapı ve barındırma halinde maliyet tasarrufu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e889b-141">With ASP.NET Core images (based on the .NET Core runtime) on Linux or Windows Nano, you can run your system with a much lower number of servers or VMs, ultimately saving costs in infrastructure and hosting.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="e889b-142">[Önceki](general-guidance.md)İleri
>[](net-framework-container-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="e889b-142">[Previous](general-guidance.md)
[Next](net-framework-container-scenarios.md)</span></span>