---
title: ASP.NET Web Forms ve Blazor mimari karşılaştırması
description: ASP.NET Web Forms ve Blazor 'in mimarilerinin nasıl karşılaştırılacağını öğrenin.
author: danroth27
ms.author: daroth
ms.date: 09/11/2019
ms.openlocfilehash: 1137218e1cd99a39240592be415f734223e90b77
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71183961"
---
# <a name="architecture-comparison-of-aspnet-web-forms-and-blazor"></a><span data-ttu-id="e43fc-103">ASP.NET Web Forms ve Blazor mimari karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="e43fc-103">Architecture comparison of ASP.NET Web Forms and Blazor</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="e43fc-104">ASP.NET Web Forms ve Blazor birçok benzer kavramlara sahip olsa da, çalışma yöntemleri arasında farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-104">While ASP.NET Web Forms and Blazor have many similar concepts, there are differences in how they work.</span></span> <span data-ttu-id="e43fc-105">Bu bölümde ASP.NET Web Forms ve Blazor 'in iç işleyişi ve mimarileri incelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-105">This chapter examines the inner workings and architectures of ASP.NET Web Forms and Blazor.</span></span>

## <a name="aspnet-web-forms"></a><span data-ttu-id="e43fc-106">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="e43fc-106">ASP.NET Web Forms</span></span>

<span data-ttu-id="e43fc-107">ASP.NET Web Forms Framework, sayfa merkezli bir mimariyi temel alır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-107">The ASP.NET Web Forms framework is based on a page-centric architecture.</span></span> <span data-ttu-id="e43fc-108">Uygulamadaki bir konuma yönelik her HTTP isteği, ASP.NET yanıt veren ayrı bir sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-108">Each HTTP request for a location in the app is a separate page with which ASP.NET responds.</span></span> <span data-ttu-id="e43fc-109">Sayfalar istendiğinde, tarayıcının içeriği istenen sayfanın sonuçlarıyla birlikte değişir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-109">As pages are requested, the contents of the browser are replaced with the results of the page requested.</span></span>

<span data-ttu-id="e43fc-110">Sayfalar aşağıdaki bileşenlerden oluşur:</span><span class="sxs-lookup"><span data-stu-id="e43fc-110">Pages consist of the following components:</span></span>

* <span data-ttu-id="e43fc-111">HTML biçimlendirmesi</span><span class="sxs-lookup"><span data-stu-id="e43fc-111">HTML markup</span></span>
* <span data-ttu-id="e43fc-112">C#veya Visual Basic kodu</span><span class="sxs-lookup"><span data-stu-id="e43fc-112">C# or Visual Basic code</span></span>
* <span data-ttu-id="e43fc-113">Logic ve olay işleme özelliklerini içeren bir arka plan kod sınıfı</span><span class="sxs-lookup"><span data-stu-id="e43fc-113">A code-behind class containing logic and event-handling capabilities</span></span>
* <span data-ttu-id="e43fc-114">Denetimler</span><span class="sxs-lookup"><span data-stu-id="e43fc-114">Controls</span></span>

<span data-ttu-id="e43fc-115">Denetimler, bir sayfada program aracılığıyla yerleştirilebilen ve bunlarla etkileşim içinde yer alan yeniden kullanılabilir Web Kullanıcı arabirimi birimleridir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-115">Controls are reusable units of web UI that can be programmatically placed and interacted with on a page.</span></span> <span data-ttu-id="e43fc-116">Sayfalar, biçimlendirme, denetimler ve bazı kod içeren *. aspx* ile biten dosyalardan oluşur.</span><span class="sxs-lookup"><span data-stu-id="e43fc-116">Pages are composed of files that end with *.aspx* containing markup, controls, and some code.</span></span> <span data-ttu-id="e43fc-117">Arka plan kod sınıfları, kullanılan programlama diline bağlı olarak aynı temel ada ve bir *. aspx.cs* ya da *. aspx. vb* uzantısına sahip dosyalardır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-117">The code-behind classes are in files with the same base name and an *.aspx.cs* or *.aspx.vb* extension, depending on the programming language used.</span></span> <span data-ttu-id="e43fc-118">Her zaman, Web sunucusu *. aspx* dosyalarının içeriğini Yorumlar ve her değiştiğinde bunları derler.</span><span class="sxs-lookup"><span data-stu-id="e43fc-118">Interestingly, the web server interprets contents of the *.aspx* files and compiles them whenever they change.</span></span> <span data-ttu-id="e43fc-119">Web sunucusu zaten çalışıyor olsa bile bu yeniden derleme oluşur.</span><span class="sxs-lookup"><span data-stu-id="e43fc-119">This recompilation occurs even if the web server is already running.</span></span>

<span data-ttu-id="e43fc-120">Denetimler, biçimlendirme ile oluşturulup Kullanıcı denetimleri olarak teslim edilebilir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-120">Controls can be built with markup and delivered as user controls.</span></span> <span data-ttu-id="e43fc-121">Bir kullanıcı denetimi `UserControl` sınıftan türetilir ve sayfada benzer bir yapıya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-121">A user control derives from the `UserControl` class and has a similar structure to the Page.</span></span> <span data-ttu-id="e43fc-122">Kullanıcı denetimleri için biçimlendirme bir *. ascx* dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-122">Markup for user controls is stored in an *.ascx* file.</span></span> <span data-ttu-id="e43fc-123">Eşlik eden bir arka plan kod sınıfı, bir *. ascx.cs* veya *. ascx. vb* dosyasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="e43fc-123">An accompanying code-behind class resides in an *.ascx.cs* or *.ascx.vb* file.</span></span> <span data-ttu-id="e43fc-124">Denetimler, `WebControl` ya `CompositeControl` da temel sınıfından devralarak kodla tamamen oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-124">Controls can also be built completely with code, by inheriting from either the `WebControl` or `CompositeControl` base class.</span></span>

<span data-ttu-id="e43fc-125">Sayfaların Ayrıca kapsamlı bir olay yaşam döngüsü vardır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-125">Pages also have an extensive event lifecycle.</span></span> <span data-ttu-id="e43fc-126">Her sayfa, ASP.NET çalışma zamanı sayfanın kodunu her istek için yürütürken oluşan başlatma, yükleme, PreRender ve kaldırma olayları için olaylar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e43fc-126">Each page raises events for the initialization, load, prerender, and unload events that occur as the ASP.NET runtime executes the page's code for each request.</span></span>

<span data-ttu-id="e43fc-127">Bir sayfadaki denetimler genellikle denetimi sunan aynı sayfaya geri dönerek, bir gizli form alanından `ViewState`bir yük ile birlikte taşır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-127">Controls on a Page typically post-back to the same page that presented the control, and carry along with them a payload from a hidden form field called `ViewState`.</span></span> <span data-ttu-id="e43fc-128">`ViewState` Alan, oluşturuldukları sırada denetimlerin durumu hakkında bilgiler içerir ve ASP.NET çalışma zamanının sunucuya gönderilen içerikte yapılan değişiklikleri karşılaştırıp tanımlamasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-128">The `ViewState` field contains information about the state of the controls at the time they were rendered and presented on the page, allowing the ASP.NET runtime to compare and identify changes in the content submitted to the server.</span></span>

## <a name="blazor"></a><span data-ttu-id="e43fc-129">Blazor</span><span class="sxs-lookup"><span data-stu-id="e43fc-129">Blazor</span></span>

<span data-ttu-id="e43fc-130">Blazor, angular veya tepki verme gibi JavaScript ön uç çerçeveleri bakımından benzer bir istemci tarafı Web UI çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-130">Blazor is a client-side web UI framework similar in nature to JavaScript front-end frameworks like Angular or React.</span></span> <span data-ttu-id="e43fc-131">Blazor kullanıcı etkileşimlerini işler ve gerekli Kullanıcı arabirimi güncelleştirmelerini işler.</span><span class="sxs-lookup"><span data-stu-id="e43fc-131">Blazor handles user interactions and renders the necessary UI updates.</span></span> <span data-ttu-id="e43fc-132">Blazor *,* istek-yanıt modelini temel alır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-132">Blazor *isn't* based on a request-reply model.</span></span> <span data-ttu-id="e43fc-133">Kullanıcı etkileşimleri, belirli bir HTTP isteği bağlamında olmayan olaylar olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-133">User interactions are handled as events that aren't in the context of any particular HTTP request.</span></span>

<span data-ttu-id="e43fc-134">Blazor uygulamaları, HTML sayfasında işlenen bir veya daha fazla kök bileşenden oluşur.</span><span class="sxs-lookup"><span data-stu-id="e43fc-134">Blazor apps consist of one or more root components that are rendered on an HTML page.</span></span>

![HTML 'de Blazor bileşenleri](./media/architecture-comparison/blazor-components-in-html.png)

<span data-ttu-id="e43fc-136">Kullanıcı, bileşenlerin nerede işleneceğini ve bileşenlerin kullanıcı etkileşimleri için nasıl bağlanacağını, modele özgü bir [barındırma](hosting-models.md) .</span><span class="sxs-lookup"><span data-stu-id="e43fc-136">How the user specifies where components should render and how the components are then wired up for user interactions is [hosting model](hosting-models.md) specific.</span></span>

<span data-ttu-id="e43fc-137">Blazor [bileşenleri](components.md) , yeniden KULLANILABILIR bir UI parçasını temsil eden .net sınıflarıdır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-137">Blazor [components](components.md) are .NET classes that represent a reusable piece of UI.</span></span> <span data-ttu-id="e43fc-138">Her bileşen kendi durumunu korur ve diğer bileşenleri işlemeyi içerebilen kendi işleme mantığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-138">Each component maintains its own state and specifies its own rendering logic, which can include rendering other components.</span></span> <span data-ttu-id="e43fc-139">Bileşenler, bileşenin durumunu güncelleştirmek üzere belirli kullanıcı etkileşimleri için olay işleyicilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-139">Components specify event handlers for specific user interactions to update the component's state.</span></span>

<span data-ttu-id="e43fc-140">Bir bileşen bir olayı işlediğinde, Blazor bileşeni işler ve işlenmiş çıktıda nelerin değiştiğini izler.</span><span class="sxs-lookup"><span data-stu-id="e43fc-140">After a component handles an event, Blazor renders the component and keeps track of what changed in the rendered output.</span></span> <span data-ttu-id="e43fc-141">Bileşenler, Belge Nesne Modeli (DOM) doğrudan işlenmez.</span><span class="sxs-lookup"><span data-stu-id="e43fc-141">Components don't render directly to the Document Object Model (DOM).</span></span> <span data-ttu-id="e43fc-142">Bunun yerine, Blazor 'in değişiklikleri izleyebilmesi için, adlı `RenderTree` Dom 'ın bellek içi gösterimine işlenir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-142">They instead render to an in-memory representation of the DOM called a `RenderTree` so that Blazor can track the changes.</span></span> <span data-ttu-id="e43fc-143">Blazor, yeni işlenmiş çıktıyı daha sonra DOM 'a verimli bir şekilde uyguladığı bir UI farkını hesaplamak için önceki çıktıyla karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-143">Blazor compares the newly rendered output with the previous output to calculate a UI diff that it then applies efficiently to the DOM.</span></span>

![Blazor DOM etkileşimi](./media/architecture-comparison/blazor-dom-interaction.png)

<span data-ttu-id="e43fc-145">Bileşenler, olağan dışı bir kullanıcı arabirimi olayının dışına değiştiği takdirde, bunların işlenip işlenmeyeceğini el ile de belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="e43fc-145">Components can also manually indicate that they should be rendered if their state changes outside of a normal UI event.</span></span> <span data-ttu-id="e43fc-146">Blazor, yürütmenin `SynchronizationContext` tek bir mantıksal iş parçacığını zorlamak için bir kullanır.</span><span class="sxs-lookup"><span data-stu-id="e43fc-146">Blazor uses a `SynchronizationContext` to enforce a single logical thread of execution.</span></span> <span data-ttu-id="e43fc-147">Bir bileşenin yaşam döngüsü yöntemleri ve Blazor tarafından oluşturulan tüm olay geri çağırmaları bunun `SynchronizationContext`üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="e43fc-147">A component's lifecycle methods and any event callbacks that are raised by Blazor are executed on this `SynchronizationContext`.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="e43fc-148">[Önceki](introduction.md)
>[İleri](hosting-models.md)</span><span class="sxs-lookup"><span data-stu-id="e43fc-148">[Previous](introduction.md)
[Next](hosting-models.md)</span></span>