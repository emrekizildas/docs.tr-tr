---
title: Uygulama Etki Alanları ve Derlemelerle Programlama
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], programming
- programming assemblies
- application domains, programming
- programming application domains
ms.assetid: 96d3b8e3-bef8-4da0-9a81-9841e23a94e9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 84d674f7ae8e80d7a5e6a40539e3330fcfa9b563
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053110"
---
# <a name="programming-with-application-domains-and-assemblies"></a><span data-ttu-id="41acf-102">Uygulama Etki Alanları ve Derlemelerle Programlama</span><span class="sxs-lookup"><span data-stu-id="41acf-102">Programming with Application Domains and Assemblies</span></span>

<span data-ttu-id="41acf-103">Microsoft Internet Explorer, ASP.NET ve Windows kabuğu gibi konaklar, ortak dil çalışma zamanını bir işleme yükler, bu işlemde bir [uygulama etki alanı](application-domains.md) oluşturur ve ardından bir .net çalıştırırken bu uygulama etki alanında Kullanıcı kodunu yükler ve yürütür Framework uygulaması.</span><span class="sxs-lookup"><span data-stu-id="41acf-103">Hosts such as Microsoft Internet Explorer, ASP.NET, and the Windows shell load the common language runtime into a process, create an [application domain](application-domains.md) in that process, and then load and execute user code in that application domain when running a .NET Framework application.</span></span> <span data-ttu-id="41acf-104">Çoğu durumda, çalışma zamanı ana bilgisayarı bu görevleri gerçekleştirdiğinden, uygulama etki alanları oluşturma ve bunlara derleme yükleme konusunda endişelenmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="41acf-104">In most cases, you do not have to worry about creating application domains and loading assemblies into them because the runtime host performs those tasks.</span></span>  
  
<span data-ttu-id="41acf-105">Bununla birlikte, ortak dil çalışma zamanını barındıracak bir uygulama oluşturuyorsanız, programlı olarak kaldırmak istediğiniz araçları veya kodu oluşturun ya da bir yandan kaldırılabildiği ve yeniden yüklenebilir olan eklenebilir bileşenler oluşturun uygulama etki alanları.</span><span class="sxs-lookup"><span data-stu-id="41acf-105">However, if you are creating an application that will host the common language runtime, creating tools or code you want to unload programmatically, or creating pluggable components that can be unloaded and reloaded on the fly, you will be creating your own application domains.</span></span> <span data-ttu-id="41acf-106">Çalışma zamanı ana bilgisayarı oluşturmasanız bile, bu bölümde bu uygulama etki alanlarında yüklü uygulama etki alanları ve Derlemeleriyle çalışma hakkında önemli bilgiler verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="41acf-106">Even if you are not creating a runtime host, this section provides important information on how to work with application domains and assemblies loaded in these application domains.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="41acf-107">Bu Bölümde</span><span class="sxs-lookup"><span data-stu-id="41acf-107">In This Section</span></span>  

[<span data-ttu-id="41acf-108">Uygulama Etki Alanları ve Bütünleştirilmiş Kodlar için Nasıl Yapılır Konuları</span><span class="sxs-lookup"><span data-stu-id="41acf-108">Application Domains and Assemblies How-to Topics</span></span>](application-domains-and-assemblies-how-to-topics.md)  
<span data-ttu-id="41acf-109">Uygulama etki alanları ve Derlemeleriyle programlama için kavramsal belgelerde bulunan tüm nasıl yapılır konularına bağlantılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="41acf-109">Provides links to all How-to topics found in the conceptual documentation for programming with application domains and assemblies.</span></span>  
  
[<span data-ttu-id="41acf-110">Uygulama Etki Alanlarını Kullanma</span><span class="sxs-lookup"><span data-stu-id="41acf-110">Using Application Domains</span></span>](use.md)  
<span data-ttu-id="41acf-111">Uygulama etki alanları oluşturma, yapılandırma ve kullanma örnekleri sunar.</span><span class="sxs-lookup"><span data-stu-id="41acf-111">Provides examples of creating, configuring, and using application domains.</span></span>  
  
[<span data-ttu-id="41acf-112">Bütünleştirilmiş Kodlarla Programlama</span><span class="sxs-lookup"><span data-stu-id="41acf-112">Programming with Assemblies</span></span>](../../standard/assembly/program.md)  
<span data-ttu-id="41acf-113">Derlemelerde nasıl öznitelik oluşturacağınızı, işaretleyeceğinizi ve ayarlayacağınızı açıklar.</span><span class="sxs-lookup"><span data-stu-id="41acf-113">Describes how to create, sign, and set attributes on assemblies.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="41acf-114">İlgili Bölümler</span><span class="sxs-lookup"><span data-stu-id="41acf-114">Related Sections</span></span>  

[<span data-ttu-id="41acf-115">Dinamik Yöntemleri ve Derlemeleri Yayma</span><span class="sxs-lookup"><span data-stu-id="41acf-115">Emitting Dynamic Methods and Assemblies</span></span>](../reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)  
<span data-ttu-id="41acf-116">Dinamik derlemelerin nasıl oluşturulduğunu açıklar.</span><span class="sxs-lookup"><span data-stu-id="41acf-116">Describes how to create dynamic assemblies.</span></span>  
  
[<span data-ttu-id="41acf-117">.NET’te bütünleştirilmiş kodlar</span><span class="sxs-lookup"><span data-stu-id="41acf-117">Assemblies in .NET</span></span>](../../standard/assembly/index.md)  
<span data-ttu-id="41acf-118">Derlemeler üzerine kavramsal bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="41acf-118">Provides a conceptual overview of assemblies.</span></span>  
  
[<span data-ttu-id="41acf-119">Uygulama Etki Alanları</span><span class="sxs-lookup"><span data-stu-id="41acf-119">Application Domains</span></span>](application-domains.md)  
<span data-ttu-id="41acf-120">Uygulama etki alanları üzerine kavramsal bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="41acf-120">Provides a conceptual overview of application domains.</span></span>  
  
[<span data-ttu-id="41acf-121">Yansımaya genel bakış</span><span class="sxs-lookup"><span data-stu-id="41acf-121">Reflection Overview</span></span>](../reflection-and-codedom/reflection.md)  
<span data-ttu-id="41acf-122">Bir derleme hakkında bilgi almak için **yansıma** sınıfının nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="41acf-122">Describes how to use the **Reflection** class to obtain information about an assembly.</span></span>
