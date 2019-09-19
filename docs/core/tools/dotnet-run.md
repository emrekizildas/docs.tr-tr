---
title: DotNet Run komutu
description: DotNet Run komutu, uygulamanızı kaynak koddan çalıştırmak için uygun bir seçenek sağlar.
ms.date: 05/29/2018
ms.openlocfilehash: ec2a24b78f435dd1905ec67b6f3f4a4ec3f7e7fa
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117486"
---
# <a name="dotnet-run"></a><span data-ttu-id="3ddd7-103">dotnet run</span><span class="sxs-lookup"><span data-stu-id="3ddd7-103">dotnet run</span></span>

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a><span data-ttu-id="3ddd7-104">Ad</span><span class="sxs-lookup"><span data-stu-id="3ddd7-104">Name</span></span>

<span data-ttu-id="3ddd7-105">`dotnet run`-Açık derleme veya başlatma komutları olmadan kaynak kodu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-105">`dotnet run` - Runs source code without any explicit compile or launch commands.</span></span>

## <a name="synopsis"></a><span data-ttu-id="3ddd7-106">Özeti</span><span class="sxs-lookup"><span data-stu-id="3ddd7-106">Synopsis</span></span>

<!-- markdownlint-disable MD025 -->

# <a name="net-core-21tabnetcore21"></a>[<span data-ttu-id="3ddd7-107">.NET Core 2,1</span><span class="sxs-lookup"><span data-stu-id="3ddd7-107">.NET Core 2.1</span></span>](#tab/netcore21)

```dotnetcli
dotnet run [-c|--configuration] [-f|--framework] [--force] [--launch-profile] [--no-build] [--no-dependencies]
    [--no-launch-profile] [--no-restore] [-p|--project] [--runtime] [-v|--verbosity] [[--] [application arguments]]
dotnet run [-h|--help]
```

# <a name="net-core-20tabnetcore20"></a>[<span data-ttu-id="3ddd7-108">.NET Core 2,0</span><span class="sxs-lookup"><span data-stu-id="3ddd7-108">.NET Core 2.0</span></span>](#tab/netcore20)

```dotnetcli
dotnet run [-c|--configuration] [-f|--framework] [--force] [--launch-profile] [--no-build] [--no-dependencies]
    [--no-launch-profile] [--no-restore] [-p|--project] [--runtime] [[--] [application arguments]]
dotnet run [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[<span data-ttu-id="3ddd7-109">.NET Core 1. x</span><span class="sxs-lookup"><span data-stu-id="3ddd7-109">.NET Core 1.x</span></span>](#tab/netcore1x)

```dotnetcli
dotnet run [-c|--configuration] [-f|--framework] [-p|--project] [[--] [application arguments]]
dotnet run [-h|--help]
```

---

## <a name="description"></a><span data-ttu-id="3ddd7-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3ddd7-110">Description</span></span>

<span data-ttu-id="3ddd7-111">Komut `dotnet run` , uygulamanızı kaynak koddan tek bir komutla çalıştırmak için uygun bir seçenek sunar.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-111">The `dotnet run` command provides a convenient option to run your application from the source code with one command.</span></span> <span data-ttu-id="3ddd7-112">Komut satırından hızlı yinelemeli geliştirme için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-112">It's useful for fast iterative development from the command line.</span></span> <span data-ttu-id="3ddd7-113">Komut, kodu oluşturmak için [`dotnet build`](dotnet-build.md) komutuna bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-113">The command depends on the [`dotnet build`](dotnet-build.md) command to build the code.</span></span> <span data-ttu-id="3ddd7-114">Projenin önce geri yüklenmesi gerektiği gibi, derleme için tüm gereksinimler, için `dotnet run` de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-114">Any requirements for the build, such as that the project must be restored first, apply to `dotnet run` as well.</span></span>

<span data-ttu-id="3ddd7-115">Çıktı dosyaları varsayılan konuma yazılır, `bin/<configuration>/<target>`yani.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-115">Output files are written into the default location, which is `bin/<configuration>/<target>`.</span></span> <span data-ttu-id="3ddd7-116">Örneğin, bir uygulamanız varsa ve `netcoreapp2.1` çalıştırırsanız `dotnet run`çıkış ' a yerleştirilir `bin/Debug/netcoreapp2.1`.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-116">For example if you have a `netcoreapp2.1` application and you run `dotnet run`, the output is placed in `bin/Debug/netcoreapp2.1`.</span></span> <span data-ttu-id="3ddd7-117">Dosyalar gerektiği gibi üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-117">Files are overwritten as needed.</span></span> <span data-ttu-id="3ddd7-118">Geçici dosyalar `obj` dizine yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-118">Temporary files are placed in the `obj` directory.</span></span>

<span data-ttu-id="3ddd7-119">Proje birden çok çerçeve belirtiyorsa, çerçeveyi belirtmek `dotnet run` için `-f|--framework <FRAMEWORK>` seçeneği kullanılmadığı müddetçe sonuçları bir hata halinde yürütüyordur.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-119">If the project specifies multiple frameworks, executing `dotnet run` results in an error unless the `-f|--framework <FRAMEWORK>` option is used to specify the framework.</span></span>

<span data-ttu-id="3ddd7-120">`dotnet run` Komut, oluşturulan derlemeler değil, proje bağlamında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-120">The `dotnet run` command is used in the context of projects, not built assemblies.</span></span> <span data-ttu-id="3ddd7-121">Bunun yerine Framework 'e bağımlı bir uygulama DLL 'sini çalıştırmaya çalışıyorsanız, bir komut olmadan [DotNet](dotnet.md) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-121">If you're trying to run a framework-dependent application DLL instead, you must use [dotnet](dotnet.md) without a command.</span></span> <span data-ttu-id="3ddd7-122">Örneğin, çalıştırmak `myapp.dll`için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3ddd7-122">For example, to run `myapp.dll`, use:</span></span>

```dotnetcli
dotnet myapp.dll
```

<span data-ttu-id="3ddd7-123">`dotnet` Sürücü hakkında daha fazla bilgi için bkz. [.NET Core komut satırı araçları (CLI)](index.md) konusu.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-123">For more information on the `dotnet` driver, see the [.NET Core Command Line Tools (CLI)](index.md) topic.</span></span>

<span data-ttu-id="3ddd7-124">Uygulamayı çalıştırmak için `dotnet run` komut, paylaşılan çalışma zamanının dışındaki uygulamanın tüm bağımlılıklarını NuGet önbelleğinden çözer.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-124">To run the application, the `dotnet run` command resolves the dependencies of the application that are outside of the shared runtime from the NuGet cache.</span></span> <span data-ttu-id="3ddd7-125">Önbelleğe alınmış bağımlılıkları kullandığından, üretim ortamında uygulamaları çalıştırmak için kullanılması `dotnet run` önerilmez.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-125">Because it uses cached dependencies, it's not recommended to use `dotnet run` to run applications in production.</span></span> <span data-ttu-id="3ddd7-126">Bunun yerine, [`dotnet publish`](dotnet-publish.md) komutunu kullanarak [bir dağıtım oluşturun](../deploying/index.md) ve yayımlanan çıktıyı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-126">Instead, [create a deployment](../deploying/index.md) using the [`dotnet publish`](dotnet-publish.md) command and deploy the published output.</span></span>

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="options"></a><span data-ttu-id="3ddd7-127">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="3ddd7-127">Options</span></span>

# <a name="net-core-21tabnetcore21"></a>[<span data-ttu-id="3ddd7-128">.NET Core 2,1</span><span class="sxs-lookup"><span data-stu-id="3ddd7-128">.NET Core 2.1</span></span>](#tab/netcore21)

`--`

<span data-ttu-id="3ddd7-129">Çalıştırılmakta olan uygulama `dotnet run` için bağımsız değişkenlerin bağımsız değişkenlerini sınırlandırın.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-129">Delimits arguments to `dotnet run` from arguments for the application being run.</span></span> <span data-ttu-id="3ddd7-130">Bu sınırlayıcıdan sonraki tüm bağımsız değişkenler uygulama çalıştırmasına geçirilir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-130">All arguments after this delimiter are passed to the application run.</span></span>

`-c|--configuration {Debug|Release}`

<span data-ttu-id="3ddd7-131">Yapı yapılandırmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-131">Defines the build configuration.</span></span> <span data-ttu-id="3ddd7-132">Varsayılan değer `Debug` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-132">The default value is `Debug`.</span></span>

`-f|--framework <FRAMEWORK>`

<span data-ttu-id="3ddd7-133">Belirtilen [Framework 'ü](../../standard/frameworks.md)kullanarak uygulamayı oluşturur ve çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-133">Builds and runs the app using the specified [framework](../../standard/frameworks.md).</span></span> <span data-ttu-id="3ddd7-134">Çerçeve proje dosyasında belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-134">The framework must be specified in the project file.</span></span>

`--force`

<span data-ttu-id="3ddd7-135">Son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-135">Forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="3ddd7-136">Bu bayrağın belirtilmesi, *Project. varlıklar. JSON* dosyasını silme ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-136">Specifying this flag is the same as deleting the *project.assets.json* file.</span></span>

`-h|--help`

<span data-ttu-id="3ddd7-137">Komut için kısa bir yardım yazdırır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-137">Prints out a short help for the command.</span></span>

`--launch-profile <NAME>`

<span data-ttu-id="3ddd7-138">Uygulamayı başlatırken kullanılacak başlatma profilinin adı (varsa).</span><span class="sxs-lookup"><span data-stu-id="3ddd7-138">The name of the launch profile (if any) to use when launching the application.</span></span> <span data-ttu-id="3ddd7-139">Başlatma profilleri, *launchsettings. JSON* dosyasında tanımlanır ve genellikle, `Development` `Staging`ve `Production`olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-139">Launch profiles are defined in the *launchSettings.json* file and are typically called `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="3ddd7-140">Daha fazla bilgi için bkz. [birden çok ortamla çalışma](/aspnet/core/fundamentals/environments).</span><span class="sxs-lookup"><span data-stu-id="3ddd7-140">For more information, see [Working with multiple environments](/aspnet/core/fundamentals/environments).</span></span>

`--no-build`

<span data-ttu-id="3ddd7-141">Çalıştırmadan önce projeyi oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-141">Doesn't build the project before running.</span></span> <span data-ttu-id="3ddd7-142">`--no-restore` Bayrak de örtülü olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-142">It also implicit sets the `--no-restore` flag.</span></span>

`--no-dependencies`

<span data-ttu-id="3ddd7-143">Projeden projeye (P2P) başvuruları olan bir projeyi geri yüklerken, başvuruları değil kök projeyi geri yükler.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-143">When restoring a project with project-to-project (P2P) references, restores the root project and not the references.</span></span>

`--no-launch-profile`

<span data-ttu-id="3ddd7-144">Uygulamayı yapılandırmak için *Launchsettings. JSON* kullanmaya çalışmayın.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-144">Doesn't try to use *launchSettings.json* to configure the application.</span></span>

`--no-restore`

<span data-ttu-id="3ddd7-145">Komutu çalıştırılırken örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-145">Doesn't execute an implicit restore when running the command.</span></span>

`-p|--project <PATH>`

<span data-ttu-id="3ddd7-146">Çalıştırılacak proje dosyasının yolunu belirtir (klasör adı veya tam yol).</span><span class="sxs-lookup"><span data-stu-id="3ddd7-146">Specifies the path of the project file to run (folder name or full path).</span></span> <span data-ttu-id="3ddd7-147">Belirtilmezse, varsayılan olarak geçerli dizini alır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-147">If not specified, it defaults to the current directory.</span></span>

`--runtime <RUNTIME_IDENTIFIER>`

<span data-ttu-id="3ddd7-148">Paketlerinin geri yükleneceği hedef çalışma zamanını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-148">Specifies the target runtime to restore packages for.</span></span> <span data-ttu-id="3ddd7-149">Çalışma zamanı tanımlayıcıları (RID 'Ler) listesi için bkz. [RID kataloğu](../rid-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="3ddd7-149">For a list of Runtime Identifiers (RIDs), see the [RID catalog](../rid-catalog.md).</span></span>

`-v|--verbosity <LEVEL>`

<span data-ttu-id="3ddd7-150">Komutun ayrıntı düzeyini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-150">Sets the verbosity level of the command.</span></span> <span data-ttu-id="3ddd7-151">İzin verilen değerler `q[uiet]` `m[inimal]` ,`n[ormal]`,, ve .`diag[nostic]` `d[etailed]`</span><span class="sxs-lookup"><span data-stu-id="3ddd7-151">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span>

# <a name="net-core-20tabnetcore20"></a>[<span data-ttu-id="3ddd7-152">.NET Core 2,0</span><span class="sxs-lookup"><span data-stu-id="3ddd7-152">.NET Core 2.0</span></span>](#tab/netcore20)

`--`

<span data-ttu-id="3ddd7-153">Çalıştırılmakta olan uygulama `dotnet run` için bağımsız değişkenlerin bağımsız değişkenlerini sınırlandırın.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-153">Delimits arguments to `dotnet run` from arguments for the application being run.</span></span> <span data-ttu-id="3ddd7-154">Bu sınırlayıcıdan sonraki tüm bağımsız değişkenler uygulama çalıştırmasına geçirilir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-154">All arguments after this delimiter are passed to the application run.</span></span>

`-c|--configuration {Debug|Release}`

<span data-ttu-id="3ddd7-155">Yapı yapılandırmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-155">Defines the build configuration.</span></span> <span data-ttu-id="3ddd7-156">Varsayılan değer `Debug` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-156">The default value is `Debug`.</span></span>

`-f|--framework <FRAMEWORK>`

<span data-ttu-id="3ddd7-157">Belirtilen [Framework 'ü](../../standard/frameworks.md)kullanarak uygulamayı oluşturur ve çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-157">Builds and runs the app using the specified [framework](../../standard/frameworks.md).</span></span> <span data-ttu-id="3ddd7-158">Çerçeve proje dosyasında belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-158">The framework must be specified in the project file.</span></span>

`--force`

<span data-ttu-id="3ddd7-159">Son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-159">Forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="3ddd7-160">Bu bayrağın belirtilmesi, *Project. varlıklar. JSON* dosyasını silme ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-160">Specifying this flag is the same as deleting the *project.assets.json* file.</span></span>

`-h|--help`

<span data-ttu-id="3ddd7-161">Komut için kısa bir yardım yazdırır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-161">Prints out a short help for the command.</span></span>

`--launch-profile <NAME>`

<span data-ttu-id="3ddd7-162">Uygulamayı başlatırken kullanılacak başlatma profilinin adı (varsa).</span><span class="sxs-lookup"><span data-stu-id="3ddd7-162">The name of the launch profile (if any) to use when launching the application.</span></span> <span data-ttu-id="3ddd7-163">Başlatma profilleri, *launchsettings. JSON* dosyasında tanımlanır ve genellikle, `Development` `Staging`ve `Production`olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-163">Launch profiles are defined in the *launchSettings.json* file and are typically called `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="3ddd7-164">Daha fazla bilgi için bkz. [birden çok ortamla çalışma](/aspnet/core/fundamentals/environments).</span><span class="sxs-lookup"><span data-stu-id="3ddd7-164">For more information, see [Working with multiple environments](/aspnet/core/fundamentals/environments).</span></span>

`--no-build`

<span data-ttu-id="3ddd7-165">Çalıştırmadan önce projeyi oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-165">Doesn't build the project before running.</span></span> <span data-ttu-id="3ddd7-166">`--no-restore` Bayrak de örtülü olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-166">It also implicit sets the `--no-restore` flag.</span></span>

`--no-dependencies`

<span data-ttu-id="3ddd7-167">Projeden projeye (P2P) başvuruları olan bir projeyi geri yüklerken, başvuruları değil kök projeyi geri yükler.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-167">When restoring a project with project-to-project (P2P) references, restores the root project and not the references.</span></span>

`--no-launch-profile`

<span data-ttu-id="3ddd7-168">Uygulamayı yapılandırmak için *Launchsettings. JSON* kullanmaya çalışmayın.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-168">Doesn't try to use *launchSettings.json* to configure the application.</span></span>

`--no-restore`

<span data-ttu-id="3ddd7-169">Komutu çalıştırılırken örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-169">Doesn't execute an implicit restore when running the command.</span></span>

`-p|--project <PATH>`

<span data-ttu-id="3ddd7-170">Çalıştırılacak proje dosyasının yolunu belirtir (klasör adı veya tam yol).</span><span class="sxs-lookup"><span data-stu-id="3ddd7-170">Specifies the path of the project file to run (folder name or full path).</span></span> <span data-ttu-id="3ddd7-171">Belirtilmezse, varsayılan olarak geçerli dizini alır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-171">If not specified, it defaults to the current directory.</span></span>

`--runtime <RUNTIME_IDENTIFIER>`

<span data-ttu-id="3ddd7-172">Paketlerinin geri yükleneceği hedef çalışma zamanını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-172">Specifies the target runtime to restore packages for.</span></span> <span data-ttu-id="3ddd7-173">Çalışma zamanı tanımlayıcıları (RID 'Ler) listesi için bkz. [RID kataloğu](../rid-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="3ddd7-173">For a list of Runtime Identifiers (RIDs), see the [RID catalog](../rid-catalog.md).</span></span>

# <a name="net-core-1xtabnetcore1x"></a>[<span data-ttu-id="3ddd7-174">.NET Core 1. x</span><span class="sxs-lookup"><span data-stu-id="3ddd7-174">.NET Core 1.x</span></span>](#tab/netcore1x)

`--`

<span data-ttu-id="3ddd7-175">Çalıştırılmakta olan uygulama `dotnet run` için bağımsız değişkenlerin bağımsız değişkenlerini sınırlandırın.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-175">Delimits arguments to `dotnet run` from arguments for the application being run.</span></span> <span data-ttu-id="3ddd7-176">Bu sınırlayıcıdan sonraki tüm bağımsız değişkenler uygulama çalıştırmasına geçirilir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-176">All arguments after this delimiter are passed to the application run.</span></span>

`-c|--configuration {Debug|Release}`

<span data-ttu-id="3ddd7-177">Yapı yapılandırmasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-177">Defines the build configuration.</span></span> <span data-ttu-id="3ddd7-178">Varsayılan değer `Debug` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-178">The default value is `Debug`.</span></span>

`-f|--framework <FRAMEWORK>`

<span data-ttu-id="3ddd7-179">Belirtilen [Framework 'ü](../../standard/frameworks.md)kullanarak uygulamayı oluşturur ve çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-179">Builds and runs the app using the specified [framework](../../standard/frameworks.md).</span></span> <span data-ttu-id="3ddd7-180">Çerçeve proje dosyasında belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-180">The framework must be specified in the project file.</span></span>

`-h|--help`

<span data-ttu-id="3ddd7-181">Komut için kısa bir yardım yazdırır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-181">Prints out a short help for the command.</span></span>

`-p|--project <PATH/PROJECT.csproj>`

<span data-ttu-id="3ddd7-182">Proje dosyasının yolunu ve adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-182">Specifies the path and name of the project file.</span></span> <span data-ttu-id="3ddd7-183">(Nota bakın.) Belirtilmezse, varsayılan olarak geçerli dizini alır.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-183">(See the NOTE.) If not specified, it defaults to the current directory.</span></span>

> [!NOTE]
> <span data-ttu-id="3ddd7-184">`-p|--project` Seçeneğiyle proje dosyasının yolunu ve adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-184">Use the path and name of the project file with the `-p|--project` option.</span></span> <span data-ttu-id="3ddd7-185">CLı 'deki bir gerileme, .NET Core SDK 1. x ile bir klasör yolu sağlamaya engel olur.</span><span class="sxs-lookup"><span data-stu-id="3ddd7-185">A regression in the CLI prevents providing a folder path with .NET Core SDK 1.x.</span></span> <span data-ttu-id="3ddd7-186">Bu sorun hakkında daha fazla bilgi için bkz. [DotNet Run-p, bir proje başlatılamadı (DotNet/clı #5992)](https://github.com/dotnet/cli/issues/5992).</span><span class="sxs-lookup"><span data-stu-id="3ddd7-186">For more information about this issue, see [dotnet run -p, can not start a project (dotnet/cli #5992)](https://github.com/dotnet/cli/issues/5992).</span></span>

---

## <a name="examples"></a><span data-ttu-id="3ddd7-187">Örnekler</span><span class="sxs-lookup"><span data-stu-id="3ddd7-187">Examples</span></span>

<span data-ttu-id="3ddd7-188">Projeyi geçerli dizinde Çalıştır:</span><span class="sxs-lookup"><span data-stu-id="3ddd7-188">Run the project in the current directory:</span></span>

`dotnet run`

<span data-ttu-id="3ddd7-189">Belirtilen projeyi Çalıştır:</span><span class="sxs-lookup"><span data-stu-id="3ddd7-189">Run the specified project:</span></span>

`dotnet run --project ./projects/proj1/proj1.csproj`

<span data-ttu-id="3ddd7-190">Projeyi geçerli dizinde çalıştırın ( `--help` boş `--` seçenek kullanıldığından bu örnekteki bağımsız değişken uygulamaya geçirilir):</span><span class="sxs-lookup"><span data-stu-id="3ddd7-190">Run the project in the current directory (the `--help` argument in this example is passed to the application, since the blank `--` option is used):</span></span>

`dotnet run --configuration Release -- --help`

<span data-ttu-id="3ddd7-191">Geçerli dizindeki proje için bağımlılıkları ve araçları geri yükleme yalnızca minimum çıktıyı gösterir ve ardından projeyi (.NET Core SDK 2,0 ve sonraki sürümleri) çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="3ddd7-191">Restore dependencies and tools for the project in the current directory only showing minimal output and then run the project: (.NET Core SDK 2.0 and later versions):</span></span>

`dotnet run --verbosity m`
