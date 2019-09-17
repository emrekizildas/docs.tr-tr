---
title: Bütünleştirilmiş kod içeren program
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework], programming
- programming assemblies
ms.assetid: 25918b15-701d-42c7-95fc-c290d08648d6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 03babe701b46eab54a76094c4728af80e6d9911e
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70973140"
---
# <a name="program-with-assemblies"></a><span data-ttu-id="2fa7c-102">Bütünleştirilmiş kod içeren program</span><span class="sxs-lookup"><span data-stu-id="2fa7c-102">Program with assemblies</span></span>
<span data-ttu-id="2fa7c-103">Derlemeler .NET Framework yapı taşlarıdır; temel dağıtım, sürüm denetimi, yeniden kullanım, etkinleştirme kapsamı ve güvenlik izinleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-103">Assemblies are the building blocks of the .NET Framework; they form the fundamental unit of deployment, version control, reuse, activation scoping, and security permissions.</span></span> <span data-ttu-id="2fa7c-104">Bir derleme, ortak dil çalışma zamanına tür uygulamalarına dikkat etmesi için gerekli bilgileri sunar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-104">An assembly provides the common language runtime with the information it needs to be aware of type implementations.</span></span> <span data-ttu-id="2fa7c-105">Birlikte çalışacak ve mantıksal bir işlevsellik birimi oluşturacak bir tür ve kaynak koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-105">It is a collection of types and resources that are built to work together and form a logical unit of functionality.</span></span> <span data-ttu-id="2fa7c-106">Çalışma zamanı için, bir derleme bağlamı dışında bir tür yoktur.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-106">To the runtime, a type does not exist outside the context of an assembly.</span></span>  
  
 <span data-ttu-id="2fa7c-107">Bu bölümde modüller oluşturma, modüllerden derlemeler oluşturma, bir anahtar çifti oluşturma ve bir derlemeyi tanımlayıcı adla imzalama ve genel bütünleştirilmiş kod önbelleğine bir derleme yüklemesi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-107">This section describes how to create modules, create assemblies from modules, create a key pair and sign an assembly with a strong name, and install an assembly into the global assembly cache.</span></span> <span data-ttu-id="2fa7c-108">Ayrıca, bu bölümde, derleme bildirimi bilgilerini görüntülemek için [MSIL Disassembler (ıldadsm. exe)](../../framework/tools/ildasm-exe-il-disassembler.md) ' nin nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-108">In addition, this section describes how to use the [MSIL Disassembler (Ildasm.exe)](../../framework/tools/ildasm-exe-il-disassembler.md) to view assembly manifest information.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="2fa7c-109">.NET Framework sürüm 2,0 ' den başlayarak, çalışma zamanı, yüklü olan çalışma zamanından daha yüksek bir sürüm numarasına sahip .NET Framework bir sürümle derlenen bir derlemeyi yüklemez.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-109">Starting with the .NET Framework version 2.0, the runtime will not load an assembly that was compiled with a version of the .NET Framework that has a higher version number than the currently loaded runtime.</span></span> <span data-ttu-id="2fa7c-110">Bu, sürüm numarasının büyük ve küçük bileşenlerinin birleşimi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-110">This applies to the combination of the major and minor components of the version number.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="2fa7c-111">Bu bölümde</span><span class="sxs-lookup"><span data-stu-id="2fa7c-111">In this section</span></span>  
 [<span data-ttu-id="2fa7c-112">Derlemeler oluştur</span><span class="sxs-lookup"><span data-stu-id="2fa7c-112">Create assemblies</span></span>](create.md)  
 <span data-ttu-id="2fa7c-113">Tek dosyalı ve çoklu dosya Derlemeleriyle genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-113">Provides an overview of single-file and multifile assemblies.</span></span>  
  
 [<span data-ttu-id="2fa7c-114">Derleme adları</span><span class="sxs-lookup"><span data-stu-id="2fa7c-114">Assembly names</span></span>](names.md)  
 <span data-ttu-id="2fa7c-115">Derleme adlandırmasına genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-115">Provides an overview of assembly naming.</span></span>  
  
 [<span data-ttu-id="2fa7c-116">Nasıl yapılır: Bir derlemenin tam nitelikli adını belirleme</span><span class="sxs-lookup"><span data-stu-id="2fa7c-116">How to: Determine an assembly's fully qualified name</span></span>](find-fully-qualified-name.md)  
 <span data-ttu-id="2fa7c-117">Bir derlemenin tam nitelikli adının nasıl belirleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-117">Describes how to determine the fully qualified name of an assembly.</span></span>  
  
 [<span data-ttu-id="2fa7c-118">Intranet uygulamalarını tam güvende çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2fa7c-118">Run intranet applications in full trust</span></span>](../../framework/app-domains/running-intranet-applications-in-full-trust.md)  
 <span data-ttu-id="2fa7c-119">Bir intranet paylaşımında tam güvenle derlemeler için eski güvenlik ilkesinin nasıl belirtileceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-119">Describes how to specify legacy security policy for full-trust assemblies on an intranet share.</span></span>  
  
 [<span data-ttu-id="2fa7c-120">Derleme konumu</span><span class="sxs-lookup"><span data-stu-id="2fa7c-120">Assembly location</span></span>](location.md)  
 <span data-ttu-id="2fa7c-121">Derlemelerin nereye bulunacağı hakkında genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-121">Provides an overview of where to locate assemblies.</span></span>  
  
 [<span data-ttu-id="2fa7c-122">Nasıl yapılır: Tek dosya derlemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2fa7c-122">How to: Build a single-file assembly</span></span>](../../framework/app-domains/build-single-file-assembly.md)  
 <span data-ttu-id="2fa7c-123">Tek dosya derlemesinin nasıl oluşturulacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-123">Describes how to create a single-file assembly.</span></span>  
  
 [<span data-ttu-id="2fa7c-124">Çoklu dosya derlemeleri</span><span class="sxs-lookup"><span data-stu-id="2fa7c-124">Multifile assemblies</span></span>](../../framework/app-domains/multifile-assemblies.md)  
 <span data-ttu-id="2fa7c-125">Çok dosyalı derlemeler oluşturma nedenlerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-125">Describes reasons for creating multifile assemblies.</span></span>  
  
 [<span data-ttu-id="2fa7c-126">Nasıl yapılır: Çoklu dosya derlemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2fa7c-126">How to: Build a multifile assembly</span></span>](../../framework/app-domains/build-multifile-assembly.md)  
 <span data-ttu-id="2fa7c-127">Çoklu dosya derlemesinin nasıl oluşturulacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-127">Describes how to create a multifile assembly.</span></span>  
  
 [<span data-ttu-id="2fa7c-128">Derleme özniteliklerini ayarla</span><span class="sxs-lookup"><span data-stu-id="2fa7c-128">Set assembly attributes</span></span>](set-attributes.md)  
 <span data-ttu-id="2fa7c-129">Derleme özniteliklerini ve bunların nasıl ayarlanacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-129">Describes assembly attributes and how to set them.</span></span>  
  
 [<span data-ttu-id="2fa7c-130">Tanımlayıcı adlı derlemeler oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="2fa7c-130">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)  
 <span data-ttu-id="2fa7c-131">Bir derlemeyi güçlü bir adla nasıl ve neden imzalayabileceğinizi açıklar ve nasıl yapılır konularını içerir.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-131">Describes how and why you sign an assembly with a strong name, and includes how-to topics.</span></span>  
  
 [<span data-ttu-id="2fa7c-132">Bir derlemeyi gecikmeli imzala</span><span class="sxs-lookup"><span data-stu-id="2fa7c-132">Delay-sign an assembly</span></span>](delay-sign.md)  
 <span data-ttu-id="2fa7c-133">Bir derlemenin nasıl geciktirileneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-133">Describes how to delay-sign an assembly.</span></span>  
  
 [<span data-ttu-id="2fa7c-134">Derlemeler ve genel derleme önbelleği ile çalışma</span><span class="sxs-lookup"><span data-stu-id="2fa7c-134">Work with assemblies and the global assembly cache</span></span>](../../framework/app-domains/working-with-assemblies-and-the-gac.md)  
 <span data-ttu-id="2fa7c-135">Derlemelerin nasıl ve neden genel derleme önbelleğine ekleneceğini ve nasıl yapılır konuları içerdiğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-135">Describes how and why you add assemblies to the global assembly cache, and includes how-to topics.</span></span>  
  
 [<span data-ttu-id="2fa7c-136">Nasıl yapılır: Derleme içeriğini görüntüle</span><span class="sxs-lookup"><span data-stu-id="2fa7c-136">How to: View assembly contents</span></span>](view-contents.md)  
 <span data-ttu-id="2fa7c-137">Derleme içeriğini görüntülemek için MSIL Disassembler (ıldadsm. exe) ' nin nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-137">Describes how to use the MSIL Disassembler (Ildasm.exe) to view assembly contents.</span></span>  
  
 [<span data-ttu-id="2fa7c-138">Ortak dil çalışma zamanında tür iletimi</span><span class="sxs-lookup"><span data-stu-id="2fa7c-138">Type forwarding in the common language runtime</span></span>](type-forwarding.md)  
 <span data-ttu-id="2fa7c-139">Mevcut uygulamaları bozmadan bir türü farklı bir derlemeye taşımak için tür iletmenin nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-139">Describes how to use type forwarding to move a type into a different assembly without breaking existing applications.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="2fa7c-140">Başvuru</span><span class="sxs-lookup"><span data-stu-id="2fa7c-140">Reference</span></span>  
 <xref:System.Reflection.Assembly>  
 <span data-ttu-id="2fa7c-141">Bir derlemeyi temsil eden .NET Framework sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-141">The .NET Framework class that represents an assembly.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="2fa7c-142">İlgili bölümler</span><span class="sxs-lookup"><span data-stu-id="2fa7c-142">Related sections</span></span>  
 [<span data-ttu-id="2fa7c-143">Nasıl yapılır: Bir derlemeden tür ve üye bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="2fa7c-143">How to: Obtain type and member information from an assembly</span></span>](../../framework/reflection-and-codedom/get-type-member-information.md)  
 <span data-ttu-id="2fa7c-144">Bir derlemeden program aracılığıyla tür ve diğer bilgilerin nasıl elde edileceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-144">Describes how to programmatically obtain type and other information from an assembly.</span></span>  
  
 [<span data-ttu-id="2fa7c-145">.NET’te bütünleştirilmiş kodlar</span><span class="sxs-lookup"><span data-stu-id="2fa7c-145">Assemblies in .NET</span></span>](index.md)  
 <span data-ttu-id="2fa7c-146">Ortak dil çalışma zamanı derlemelerine kavramsal bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-146">Provides a conceptual overview of common language runtime assemblies.</span></span>  
  
 [<span data-ttu-id="2fa7c-147">Derleme sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="2fa7c-147">Assembly versioning</span></span>](versioning.md)  
 <span data-ttu-id="2fa7c-148">Derleme bağlamaya ve <xref:System.Reflection.AssemblyVersionAttribute> ve <xref:System.Reflection.AssemblyInformationalVersionAttribute> özniteliklerine ilişkin bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-148">Provides an overview of assembly binding and of the <xref:System.Reflection.AssemblyVersionAttribute> and <xref:System.Reflection.AssemblyInformationalVersionAttribute> attributes.</span></span>  
  
 [<span data-ttu-id="2fa7c-149">Çalışma zamanının derlemeleri nasıl konumlandırır</span><span class="sxs-lookup"><span data-stu-id="2fa7c-149">How the runtime locates assemblies</span></span>](../../framework/deployment/how-the-runtime-locates-assemblies.md)  
 <span data-ttu-id="2fa7c-150">Çalışma zamanının, bir bağlama isteğini yerine getirmek için hangi derlemeyi kullanacağınızı nasıl belirlediğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-150">Describes how the runtime determines which assembly to use to fulfill a binding request.</span></span>  
  
 <span data-ttu-id="2fa7c-151">[Yansıması](../../framework/reflection-and-codedom/reflection.md) </span><span class="sxs-lookup"><span data-stu-id="2fa7c-151">[Reflection](../../framework/reflection-and-codedom/reflection.md) </span></span>  
 <span data-ttu-id="2fa7c-152">Bir derleme hakkında bilgi almak için **yansıma** sınıfının nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="2fa7c-152">Describes how to use the **Reflection** class to obtain information about an assembly.</span></span>