---
title: Uygulama Etki Alanlarını Kullanma
ms.date: 03/30/2017
helpviewer_keywords:
- application domains, about
- common language runtime, application domains
- runtime, application domains
ms.assetid: c6d99815-e022-4d2c-9420-1d7ab5b9d504
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ad05d005ece4a52e2df0dbb7e044522db58f1787
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971854"
---
# <a name="using-application-domains"></a><span data-ttu-id="9b486-102">Uygulama Etki Alanlarını Kullanma</span><span class="sxs-lookup"><span data-stu-id="9b486-102">Using Application Domains</span></span>
<span data-ttu-id="9b486-103">Uygulama etki alanları, ortak dil çalışma zamanı için bir yalıtım birimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b486-103">Application domains provide a unit of isolation for the common language runtime.</span></span> <span data-ttu-id="9b486-104">Bunlar bir işlem içinde oluşturulup çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="9b486-104">They are created and run inside a process.</span></span> <span data-ttu-id="9b486-105">Uygulama etki alanları genellikle çalışma zamanının bir işleme yüklenmesi ve bir uygulama etki alanı içinde Kullanıcı kodu yürütmesi ile ilgili bir uygulama olan bir çalışma zamanı ana bilgisayarı tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9b486-105">Application domains are usually created by a runtime host, which is an application responsible for loading the runtime into a process and executing user code within an application domain.</span></span> <span data-ttu-id="9b486-106">Çalışma zamanı ana bilgisayarı bir işlem ve varsayılan bir uygulama etki alanı oluşturur ve içinde yönetilen kodu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="9b486-106">The runtime host creates a process and a default application domain, and runs managed code inside it.</span></span> <span data-ttu-id="9b486-107">Çalışma zamanı Konakları ASP.NET, Microsoft Internet Explorer ve Windows kabuğu içerir.</span><span class="sxs-lookup"><span data-stu-id="9b486-107">Runtime hosts include ASP.NET, Microsoft Internet Explorer, and the Windows shell.</span></span>  
  
 <span data-ttu-id="9b486-108">Çoğu uygulama için kendi uygulama etki alanınızı oluşturmanız gerekmez; çalışma zamanı ana bilgisayarı sizin için gerekli uygulama etki alanlarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9b486-108">For most applications, you do not need to create your own application domain; the runtime host creates any necessary application domains for you.</span></span> <span data-ttu-id="9b486-109">Ancak, uygulamanızın kodu yalıtması veya dll 'Leri kullanması veya yüklemesi gerekiyorsa ek uygulama etki alanları oluşturabilir ve yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b486-109">However, you can create and configure additional application domains if your application needs to isolate code or to use and unload DLLs.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="9b486-110">Bu Bölümde</span><span class="sxs-lookup"><span data-stu-id="9b486-110">In This Section</span></span>  
 [<span data-ttu-id="9b486-111">Nasıl yapılır: Uygulama etki alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9b486-111">How to: Create an Application Domain</span></span>](../../../docs/framework/app-domains/how-to-create-an-application-domain.md)  
 <span data-ttu-id="9b486-112">Programlı olarak bir uygulama etki alanı oluşturma işlemini açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b486-112">Describes how to programmatically create an application domain.</span></span>  
  
 [<span data-ttu-id="9b486-113">Nasıl yapılır: Uygulama etki alanını kaldırma</span><span class="sxs-lookup"><span data-stu-id="9b486-113">How to: Unload an Application Domain</span></span>](../../../docs/framework/app-domains/how-to-unload-an-application-domain.md)  
 <span data-ttu-id="9b486-114">Bir uygulama etki alanını programlı olarak nasıl kaldırabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b486-114">Describes how to programmatically unload an application domain.</span></span>  
  
 [<span data-ttu-id="9b486-115">Nasıl yapılır: Uygulama etki alanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9b486-115">How to: Configure an Application Domain</span></span>](../../../docs/framework/app-domains/how-to-configure-an-application-domain.md)  
 <span data-ttu-id="9b486-116">Uygulama etki alanı yapılandırmaya bir giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b486-116">Provides an introduction to configuring an application domain.</span></span>  
  
 [<span data-ttu-id="9b486-117">Bir Uygulama Etki Alanından Kurulum Bilgilerini Alma</span><span class="sxs-lookup"><span data-stu-id="9b486-117">Retrieving Setup Information from an Application Domain</span></span>](../../../docs/framework/app-domains/retrieve-setup-information.md)  
 <span data-ttu-id="9b486-118">Bir uygulama etki alanından kurulum bilgilerinin nasıl alınacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b486-118">Describes how to retrieve setup information from an application domain.</span></span>  
  
 [<span data-ttu-id="9b486-119">Nasıl yapılır: Derlemeleri bir uygulama etki alanına yükleme</span><span class="sxs-lookup"><span data-stu-id="9b486-119">How to: Load Assemblies into an Application Domain</span></span>](../../../docs/framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)  
 <span data-ttu-id="9b486-120">Bir derlemenin uygulama etki alanına nasıl yükleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b486-120">Describes how to load an assembly into an application domain.</span></span>  
  
 [<span data-ttu-id="9b486-121">Nasıl yapılır: Bir derlemeden tür ve üye bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="9b486-121">How to: Obtain Type and Member Information from an Assembly</span></span>](../reflection-and-codedom/get-type-member-information.md)  
 <span data-ttu-id="9b486-122">Bir derleme hakkında bilgilerin nasıl alınacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b486-122">Describes how to retrieve information about an assembly.</span></span>  
  
 [<span data-ttu-id="9b486-123">Gölge Kopyalama Bütünleştirilmiş Kodları</span><span class="sxs-lookup"><span data-stu-id="9b486-123">Shadow Copying Assemblies</span></span>](../../../docs/framework/app-domains/shadow-copy-assemblies.md)  
 <span data-ttu-id="9b486-124">Gölge kopyalamanın, kullanıldıkları sırada derlemeler için güncelleştirmelerin nasıl izin verdiğini ve gölge kopyalamayı nasıl yapılandıracağınızı açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b486-124">Describes how shadow copying allows updates to assemblies while they are in use, and how to configure shadow copying.</span></span>  
  
 [<span data-ttu-id="9b486-125">Nasıl yapılır: Birinci şans özel durum bildirimlerini al</span><span class="sxs-lookup"><span data-stu-id="9b486-125">How to: Receive First-Chance Exception Notifications</span></span>](../../../docs/framework/app-domains/how-to-receive-first-chance-exception-notifications.md)  
 <span data-ttu-id="9b486-126">Ortak dil çalışma zamanı özel durum işleyicilerini aramaya başlamadan önce bir özel durumun oluşturulduğu bildirimini nasıl alacağınızı açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b486-126">Explains how you can receive a notification that an exception has been thrown, before the common language runtime has begun searching for exception handlers.</span></span>  
  
 [<span data-ttu-id="9b486-127">Bütünleştirilmiş Kod Yüklerini Çözme</span><span class="sxs-lookup"><span data-stu-id="9b486-127">Resolving Assembly Loads</span></span>](../../standard/assembly/resolve-loads.md)  
 <span data-ttu-id="9b486-128">Derleme yükleme başarısızlıklarını çözümlemek için <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> olayı kullanma hakkında rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b486-128">Provides guidance on using the <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> event to resolve assembly load failures.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="9b486-129">Başvuru</span><span class="sxs-lookup"><span data-stu-id="9b486-129">Reference</span></span>  
 <xref:System.AppDomain>  
 <span data-ttu-id="9b486-130">Bir uygulama etki alanını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9b486-130">Represents an application domain.</span></span> <span data-ttu-id="9b486-131">Uygulama etki alanları oluşturmak ve denetlemek için yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b486-131">Provides methods for creating and controlling application domains.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="9b486-132">İlgili Bölümler</span><span class="sxs-lookup"><span data-stu-id="9b486-132">Related Sections</span></span>  
 [<span data-ttu-id="9b486-133">.NET’te bütünleştirilmiş kodlar</span><span class="sxs-lookup"><span data-stu-id="9b486-133">Assemblies in .NET</span></span>](../../standard/assembly/index.md)  
 <span data-ttu-id="9b486-134">Derlemeler tarafından gerçekleştirilen işlevlere genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b486-134">Provides an overview of the functions performed by assemblies.</span></span>  
  
 [<span data-ttu-id="9b486-135">Bütünleştirilmiş Kodlarla Programlama</span><span class="sxs-lookup"><span data-stu-id="9b486-135">Programming with Assemblies</span></span>](../../standard/assembly/program.md)  
 <span data-ttu-id="9b486-136">Derlemelerde nasıl öznitelik oluşturacağınızı, işaretleyeceğinizi ve ayarlayacağınızı açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b486-136">Describes how to create, sign, and set attributes on assemblies.</span></span>  
  
 [<span data-ttu-id="9b486-137">Dinamik Yöntemleri ve Derlemeleri Yayma</span><span class="sxs-lookup"><span data-stu-id="9b486-137">Emitting Dynamic Methods and Assemblies</span></span>](../../../docs/framework/reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)  
 <span data-ttu-id="9b486-138">Dinamik derlemelerin nasıl oluşturulduğunu açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b486-138">Describes how to create dynamic assemblies.</span></span>  
  
 [<span data-ttu-id="9b486-139">Uygulama Etki Alanları</span><span class="sxs-lookup"><span data-stu-id="9b486-139">Application Domains</span></span>](../../../docs/framework/app-domains/application-domains.md)  
 <span data-ttu-id="9b486-140">Uygulama etki alanları üzerine kavramsal bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b486-140">Provides a conceptual overview of application domains.</span></span>  
  
 [<span data-ttu-id="9b486-141">Yansımaya genel bakış</span><span class="sxs-lookup"><span data-stu-id="9b486-141">Reflection Overview</span></span>](../../../docs/framework/reflection-and-codedom/reflection.md)  
 <span data-ttu-id="9b486-142">Bir derleme hakkında bilgi almak için **yansıma** sınıfının nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b486-142">Describes how to use the **Reflection** class to obtain information about an assembly.</span></span>
