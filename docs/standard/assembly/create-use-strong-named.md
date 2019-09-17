---
title: Tanımlayıcı adlı ssemblies oluşturma ve kullanma
ms.date: 08/19/2019
helpviewer_keywords:
- strong-name bypass feature
- strong-named assemblies, about strong-named assemblies
- strong-named assemblies
- signing assemblies
- assemblies [.NET Framework], signing
- strong-named assemblies, scenarios
- assemblies [.NET Framework], strong-named
- strong-named assemblies, loading into trusted application domains
- assembly binding, strong-named
ms.assetid: ffbf6d9e-4a88-4a8a-9645-4ce0ee1ee5f9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 55869c107d245738df3af5ca9bb1b22195e90024
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70973322"
---
# <a name="create-and-use-strong-named-assemblies"></a><span data-ttu-id="26222-102">Tanımlayıcı adlı derlemeler oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="26222-102">Create and use strong-named assemblies</span></span>

<span data-ttu-id="26222-103">Tanımlayıcı ad, derleme kimliğinden (basit metin adı, sürüm numarası ve kültür bilgileri (sağlanmışsa) ve bir ortak anahtar ve dijital imza ile oluşur.</span><span class="sxs-lookup"><span data-stu-id="26222-103">A strong name consists of the assembly's identity—its simple text name, version number, and culture information (if provided)—plus a public key and a digital signature.</span></span> <span data-ttu-id="26222-104">Karşılık gelen özel anahtar kullanılarak derleme dosyasından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="26222-104">It is generated from an assembly file using the corresponding private key.</span></span> <span data-ttu-id="26222-105">(Derleme dosyası, derlemeyi oluşturan tüm dosyaların adlarını ve karmalarını içeren derleme bildirimini içerir.)</span><span class="sxs-lookup"><span data-stu-id="26222-105">(The assembly file contains the assembly manifest, which contains the names and hashes of all the files that make up the assembly.)</span></span>

> [!WARNING]
> <span data-ttu-id="26222-106">Güvenlik için tanımlayıcı adlara güvenmeyin.</span><span class="sxs-lookup"><span data-stu-id="26222-106">Do not rely on strong names for security.</span></span> <span data-ttu-id="26222-107">Yalnızca benzersiz bir kimlik sağlarlar.</span><span class="sxs-lookup"><span data-stu-id="26222-107">They provide a unique identity only.</span></span>

<span data-ttu-id="26222-108">Tanımlayıcı adlı bir derleme, yalnızca diğer tanımlayıcı adlı derlemelerden türleri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="26222-108">A strong-named assembly can only use types from other strong-named assemblies.</span></span> <span data-ttu-id="26222-109">Aksi takdirde, tanımlayıcı adlı derlemenin bütünlüğü tehlikeye girebilir.</span><span class="sxs-lookup"><span data-stu-id="26222-109">Otherwise, the integrity of the strong-named assembly would be compromised.</span></span>

> [!NOTE]
> <span data-ttu-id="26222-110">.NET Core, tanımlayıcı adlı derlemeleri desteklese de, .NET Core kitaplığındaki tüm derlemeler imzalansa da, üçüncü taraf derlemelerin çoğunluğunun tanımlayıcı adlara ihtiyacı yoktur.</span><span class="sxs-lookup"><span data-stu-id="26222-110">Although .NET Core supports strong-named assemblies, and all assemblies in the .NET Core library are signed, the majority of third-party assemblies do not need strong names.</span></span> <span data-ttu-id="26222-111">Daha fazla bilgi için bkz. GitHub 'da [tanımlayıcı ad imzalama](https://github.com/dotnet/corefx/blob/master/Documentation/project-docs/strong-name-signing.md) .</span><span class="sxs-lookup"><span data-stu-id="26222-111">For more information, see [Strong Name Signing](https://github.com/dotnet/corefx/blob/master/Documentation/project-docs/strong-name-signing.md) on GitHub.</span></span>

## <a name="strong-name-scenario"></a><span data-ttu-id="26222-112">Tanımlayıcı ad senaryosu</span><span class="sxs-lookup"><span data-stu-id="26222-112">Strong name scenario</span></span>

<span data-ttu-id="26222-113">Aşağıdaki senaryo, bir derlemeyi güçlü bir adla imzalama ve daha sonra bu ada göre başvuruda bulunma sürecini özetler.</span><span class="sxs-lookup"><span data-stu-id="26222-113">The following scenario outlines the process of signing an assembly with a strong name and later referencing it by that name.</span></span>

1. <span data-ttu-id="26222-114">Derleme A, aşağıdaki yöntemlerden biri kullanılarak bir tanımlayıcı ad ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="26222-114">Assembly A is created with a strong name using one of the following methods:</span></span>

    - <span data-ttu-id="26222-115">Visual Studio gibi güçlü adlar oluşturmayı destekleyen bir geliştirme ortamı kullanma.</span><span class="sxs-lookup"><span data-stu-id="26222-115">Using a development environment that supports creating strong names, such as Visual Studio.</span></span>

    - <span data-ttu-id="26222-116">Bir komut satırı derleyicisi veya [derleme Bağlayıcısı (al. exe)](../../framework/tools/al-exe-assembly-linker.md)kullanarak, [tanımlayıcı ad Aracı (sn. exe)](../../framework/tools/sn-exe-strong-name-tool.md) kullanarak bir şifreleme anahtarı çifti oluşturma ve bu anahtar çiftini derlemeye atama.</span><span class="sxs-lookup"><span data-stu-id="26222-116">Creating a cryptographic key pair using the [Strong Name tool (Sn.exe)](../../framework/tools/sn-exe-strong-name-tool.md) and assigning that key pair to the assembly using either a command-line compiler or the [Assembly Linker (Al.exe)](../../framework/tools/al-exe-assembly-linker.md).</span></span> <span data-ttu-id="26222-117">Windows SDK hem sn. exe hem de al. exe sağlar.</span><span class="sxs-lookup"><span data-stu-id="26222-117">The Windows SDK provides both Sn.exe and Al.exe.</span></span>

2. <span data-ttu-id="26222-118">Geliştirme ortamı veya aracı, geliştiricinin özel anahtarıyla derlemenin bildirimini içeren dosyanın karmasını imzalar.</span><span class="sxs-lookup"><span data-stu-id="26222-118">The development environment or tool signs the hash of the file containing the assembly's manifest with the developer's private key.</span></span> <span data-ttu-id="26222-119">Bu dijital imza, derleme A 'nın bildirimini içeren taşınabilir çalıştırılabilir (PE) dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="26222-119">This digital signature is stored in the portable executable (PE) file that contains Assembly A's manifest.</span></span>

3. <span data-ttu-id="26222-120">Derleme B, A derlemesi tüketicisidir. Derleme B 'nin bildiriminin başvuru bölümü, derleme A 'nın ortak anahtarını temsil eden bir belirteç içerir.</span><span class="sxs-lookup"><span data-stu-id="26222-120">Assembly B is a consumer of Assembly A. The reference section of Assembly B's manifest includes a token that represents Assembly A's public key.</span></span> <span data-ttu-id="26222-121">Belirteç, tam ortak anahtarın bir bölümüdür ve alan kazanmak için anahtarın kendisi yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="26222-121">A token is a portion of the full public key and is used rather than the key itself to save space.</span></span>

4. <span data-ttu-id="26222-122">Ortak dil çalışma zamanı, derleme genel derleme önbelleğine yerleştirildiğinde tanımlayıcı ad imzasını doğrular.</span><span class="sxs-lookup"><span data-stu-id="26222-122">The common language runtime verifies the strong name signature when the assembly is placed in the global assembly cache.</span></span> <span data-ttu-id="26222-123">Çalışma zamanında tanımlayıcı ada göre bağlamada ortak dil çalışma zamanı, derleme B 'nin bildiriminde depolanan anahtarı, derleme A için tanımlayıcı ad oluşturmak için kullanılan anahtarla karşılaştırır. .NET Framework güvenlik denetimi başarılı olursa ve bağlama başarılı olursa, derleme B, derleme A 'nın bitleri kurcalanmayan ve bu bitlerin aslında A derlemesi geliştiricilerinden geldiği garantisi vardır.</span><span class="sxs-lookup"><span data-stu-id="26222-123">When binding by strong name at run time, the common language runtime compares the key stored in Assembly B's manifest with the key used to generate the strong name for Assembly A. If the .NET Framework security checks pass and the bind succeeds, Assembly B has a guarantee that Assembly A's bits have not been tampered with and that these bits actually come from the developers of Assembly A.</span></span>

> [!NOTE]
> <span data-ttu-id="26222-124">Bu senaryo güven sorunlarına yönelik değildir.</span><span class="sxs-lookup"><span data-stu-id="26222-124">This scenario doesn't address trust issues.</span></span> <span data-ttu-id="26222-125">Derlemeler, güçlü bir ada ek olarak tam Microsoft Authenticode imzalarını taşıyabilir.</span><span class="sxs-lookup"><span data-stu-id="26222-125">Assemblies can carry full Microsoft Authenticode signatures in addition to a strong name.</span></span> <span data-ttu-id="26222-126">Authenticode imzaları, güven kuran bir sertifika içerir.</span><span class="sxs-lookup"><span data-stu-id="26222-126">Authenticode signatures include a certificate that establishes trust.</span></span> <span data-ttu-id="26222-127">Tanımlayıcı adların kodun bu şekilde imzalanmasını gerektirmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="26222-127">It's important to note that strong names don't require code to be signed in this way.</span></span> <span data-ttu-id="26222-128">Tanımlayıcı adlar yalnızca benzersiz bir kimlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="26222-128">Strong names only provide a unique identity.</span></span>

## <a name="bypass-signature-verification-of-trusted-assemblies"></a><span data-ttu-id="26222-129">Güvenilen derlemelerin imza doğrulamasını atla</span><span class="sxs-lookup"><span data-stu-id="26222-129">Bypass signature verification of trusted assemblies</span></span>

<span data-ttu-id="26222-130">.NET Framework 3,5 Service Pack 1 ' den itibaren, bir derleme bir tam güvenli uygulama etki alanına yüklendiğinde, `MyComputer` bölgenin varsayılan uygulama etki alanı gibi tanımlayıcı ad imzaları doğrulanmaz.</span><span class="sxs-lookup"><span data-stu-id="26222-130">Starting with the .NET Framework 3.5 Service Pack 1, strong-name signatures are not validated when an assembly is loaded into a full-trust application domain, such as the default application domain for the `MyComputer` zone.</span></span> <span data-ttu-id="26222-131">Bu, tanımlayıcı ad atlama özelliği olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="26222-131">This is referred to as the strong-name bypass feature.</span></span> <span data-ttu-id="26222-132">Tam güven ortamında, <xref:System.Security.Permissions.StrongNameIdentityPermission> imzalarından bağımsız olarak imzalı, tam güvenle derlemeler için her zaman başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="26222-132">In a full-trust environment, demands for <xref:System.Security.Permissions.StrongNameIdentityPermission> always succeed for signed, full-trust assemblies, regardless of their signature.</span></span> <span data-ttu-id="26222-133">Güçlü ad atlama özelliği, bu durumda derlemelerin daha hızlı yüklenmesine izin vermek için tam güven derlemelerinin tanımlayıcı ad imzası doğrulamasının gereksiz ek yükünü önler.</span><span class="sxs-lookup"><span data-stu-id="26222-133">The strong-name bypass feature avoids the unnecessary overhead of strong-name signature verification of full-trust assemblies in this situation, allowing the assemblies to load faster.</span></span>

<span data-ttu-id="26222-134">Atlama özelliği, bir tanımlayıcı ad ile imzalanmış ve aşağıdaki özelliklere sahip olan her derleme için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="26222-134">The bypass feature applies to any assembly that is signed with a strong name and that has the following characteristics:</span></span>

- <span data-ttu-id="26222-135">Kanıt olmadan <xref:System.Security.Policy.StrongName> tamamen güvenilir (örneğin, bölge kanıtları vardır `MyComputer` ).</span><span class="sxs-lookup"><span data-stu-id="26222-135">Fully trusted without <xref:System.Security.Policy.StrongName> evidence (for example, has `MyComputer` zone evidence).</span></span>

- <span data-ttu-id="26222-136">Tam güvenilir <xref:System.AppDomain>bir şekilde yüklendi.</span><span class="sxs-lookup"><span data-stu-id="26222-136">Loaded into a fully trusted <xref:System.AppDomain>.</span></span>

- <span data-ttu-id="26222-137"><xref:System.AppDomainSetup.ApplicationBase%2A> Özelliği altında<xref:System.AppDomain>bir konumdan yüklendi.</span><span class="sxs-lookup"><span data-stu-id="26222-137">Loaded from a location under the <xref:System.AppDomainSetup.ApplicationBase%2A> property of that <xref:System.AppDomain>.</span></span>

- <span data-ttu-id="26222-138">Gecikmeli imza değildir.</span><span class="sxs-lookup"><span data-stu-id="26222-138">Not delay-signed.</span></span>

<span data-ttu-id="26222-139">Bu özellik ayrı uygulamalar veya bir bilgisayar için devre dışı bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="26222-139">This feature can be disabled for individual applications or for a computer.</span></span> <span data-ttu-id="26222-140">Bkz [. nasıl yapılır: Tanımlayıcı adı atlama özelliğini](disable-strong-name-bypass-feature.md)devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="26222-140">See [How to: Disable the strong-name bypass feature](disable-strong-name-bypass-feature.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="26222-141">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="26222-141">Related topics</span></span>

|<span data-ttu-id="26222-142">Başlık</span><span class="sxs-lookup"><span data-stu-id="26222-142">Title</span></span>|<span data-ttu-id="26222-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="26222-143">Description</span></span>|
|-----------|-----------------|
|[<span data-ttu-id="26222-144">Nasıl yapılır: Ortak özel anahtar çifti oluşturma</span><span class="sxs-lookup"><span data-stu-id="26222-144">How to: Create a public-private key pair</span></span>](create-public-private-key-pair.md)|<span data-ttu-id="26222-145">Bir derlemeyi imzalamak için bir şifreleme anahtarı çiftinin nasıl oluşturulacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="26222-145">Describes how to create a cryptographic key pair for signing an assembly.</span></span>|
|[<span data-ttu-id="26222-146">Nasıl yapılır: Bir derlemeyi güçlü bir adla imzala</span><span class="sxs-lookup"><span data-stu-id="26222-146">How to: Sign an assembly with a strong name</span></span>](sign-strong-name.md)|<span data-ttu-id="26222-147">Tanımlayıcı adlı derlemenin nasıl oluşturulacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="26222-147">Describes how to create a strong-named assembly.</span></span>|
|[<span data-ttu-id="26222-148">Gelişmiş tanımlayıcı adlandırma</span><span class="sxs-lookup"><span data-stu-id="26222-148">Enhanced strong naming</span></span>](enhanced-strong-naming.md)|<span data-ttu-id="26222-149">4,5 .NET Framework güçlü adlarla ilgili geliştirmeleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="26222-149">Describes enhancements to strong-names in the .NET Framework 4.5.</span></span>|
|[<span data-ttu-id="26222-150">Nasıl yapılır: Tanımlayıcı adlı bir derlemeye başvuru</span><span class="sxs-lookup"><span data-stu-id="26222-150">How to: Reference a strong-named assembly</span></span>](reference-strong-named.md)|<span data-ttu-id="26222-151">Derleme zamanında veya çalışma zamanında tanımlayıcı adlı bir derlemede türlerin veya kaynakların nasıl başvurululacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="26222-151">Describes how to reference types or resources in a strong-named assembly at compile time or run time.</span></span>|
|[<span data-ttu-id="26222-152">Nasıl yapılır: Tanımlayıcı adı atlama özelliğini devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="26222-152">How to: Disable the strong-name bypass feature</span></span>](disable-strong-name-bypass-feature.md)|<span data-ttu-id="26222-153">Tanımlayıcı ad imzalarının doğrulanmasını atlayan özelliğin nasıl devre dışı bırakılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="26222-153">Describes how to disable the feature that bypasses the validation of strong-name signatures.</span></span> <span data-ttu-id="26222-154">Bu özellik tüm veya belirli uygulamalar için devre dışı bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="26222-154">This feature can be disabled for all or for specific applications.</span></span>|
|[<span data-ttu-id="26222-155">Derlemeler oluştur</span><span class="sxs-lookup"><span data-stu-id="26222-155">Create assemblies</span></span>](create.md)|<span data-ttu-id="26222-156">Tek dosyalı ve çoklu dosya Derlemeleriyle genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="26222-156">Provides an overview of single-file and multifile assemblies.</span></span>|
|[<span data-ttu-id="26222-157">Visual Studio 'da bir derlemeyi imzalamayı geciktirme</span><span class="sxs-lookup"><span data-stu-id="26222-157">How to delay sign an assembly in Visual Studio</span></span>](/visualstudio/ide/managing-assembly-and-manifest-signing#how-to-sign-an-assembly-in-visual-studio)|<span data-ttu-id="26222-158">Derleme oluşturulduktan sonra bir derlemeyi güçlü bir adla nasıl imzalayabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="26222-158">Explains how to sign an assembly with a strong name after the assembly has been created.</span></span>|
|[<span data-ttu-id="26222-159">Sn. exe (tanımlayıcı ad aracı)</span><span class="sxs-lookup"><span data-stu-id="26222-159">Sn.exe (Strong Name tool)</span></span>](../../framework/tools/sn-exe-strong-name-tool.md)|<span data-ttu-id="26222-160">Güçlü adlara sahip derlemeler oluşturulmasına yardımcı olan .NET Framework dahil olan aracı açıklar.</span><span class="sxs-lookup"><span data-stu-id="26222-160">Describes the tool included in the .NET Framework that helps create assemblies with strong names.</span></span> <span data-ttu-id="26222-161">Bu araç, temel yönetim, imza oluşturma ve imza doğrulaması için seçenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="26222-161">This tool provides options for key management, signature generation, and signature verification.</span></span>|
|[<span data-ttu-id="26222-162">Al. exe (bütünleştirilmiş kod bağlayıcı)</span><span class="sxs-lookup"><span data-stu-id="26222-162">Al.exe (Assembly linker)</span></span>](../../framework/tools/al-exe-assembly-linker.md)|<span data-ttu-id="26222-163">Modüller veya kaynak dosyalarından derleme bildirimine sahip bir dosya üreten .NET Framework dahil olan aracı açıklar.</span><span class="sxs-lookup"><span data-stu-id="26222-163">Describes the tool included in the .NET Framework that generates a file that has an assembly manifest from modules or resource files.</span></span>|