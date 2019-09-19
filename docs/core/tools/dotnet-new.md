---
title: DotNet yeni komut
description: DotNet New komutu, belirtilen şablona göre yeni .NET Core projeleri oluşturur.
ms.date: 05/06/2019
ms.openlocfilehash: b61b5fd53f470c30b636026fa19ebfad834d6354
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117668"
---
# <a name="dotnet-new"></a><span data-ttu-id="1935b-103">dotnet new</span><span class="sxs-lookup"><span data-stu-id="1935b-103">dotnet new</span></span>

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a><span data-ttu-id="1935b-104">Ad</span><span class="sxs-lookup"><span data-stu-id="1935b-104">Name</span></span>

<span data-ttu-id="1935b-105">`dotnet new`-Belirtilen şablonu temel alan yeni bir proje, yapılandırma dosyası veya çözüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1935b-105">`dotnet new` - Creates a new project, configuration file, or solution based on the specified template.</span></span>

## <a name="synopsis"></a><span data-ttu-id="1935b-106">Özeti</span><span class="sxs-lookup"><span data-stu-id="1935b-106">Synopsis</span></span>

<!-- markdownlint-disable MD025 -->

# <a name="net-core-22tabnetcore22"></a>[<span data-ttu-id="1935b-107">.NET Core 2,2</span><span class="sxs-lookup"><span data-stu-id="1935b-107">.NET Core 2.2</span></span>](#tab/netcore22)

```dotnetcli
dotnet new <TEMPLATE> [--dry-run] [--force] [-i|--install] [-lang|--language] [-n|--name] [--nuget-source] [-o|--output] [-u|--uninstall] [Template options]
dotnet new <TEMPLATE> [-l|--list] [--type]
dotnet new [-h|--help]
```

# <a name="net-core-21tabnetcore21"></a>[<span data-ttu-id="1935b-108">.NET Core 2,1</span><span class="sxs-lookup"><span data-stu-id="1935b-108">.NET Core 2.1</span></span>](#tab/netcore21)

```dotnetcli
dotnet new <TEMPLATE> [--force] [-i|--install] [-lang|--language] [-n|--name] [--nuget-source] [-o|--output] [-u|--uninstall] [Template options]
dotnet new <TEMPLATE> [-l|--list] [--type]
dotnet new [-h|--help]
```

# <a name="net-core-20tabnetcore20"></a>[<span data-ttu-id="1935b-109">.NET Core 2,0</span><span class="sxs-lookup"><span data-stu-id="1935b-109">.NET Core 2.0</span></span>](#tab/netcore20)

```dotnetcli
dotnet new <TEMPLATE> [--force] [-i|--install] [-lang|--language] [-n|--name] [-o|--output] [-u|--uninstall] [Template options]
dotnet new <TEMPLATE> [-l|--list] [--type]
dotnet new [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[<span data-ttu-id="1935b-110">.NET Core 1. x</span><span class="sxs-lookup"><span data-stu-id="1935b-110">.NET Core 1.x</span></span>](#tab/netcore1x)

```dotnetcli
dotnet new <TEMPLATE> [-lang|--language] [-n|--name] [-o|--output] [-all|--show-all] [-h|--help] [Template options]
dotnet new <TEMPLATE> [-l|--list]
dotnet new [-all|--show-all]
dotnet new [-h|--help]
```

---

## <a name="description"></a><span data-ttu-id="1935b-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1935b-111">Description</span></span>

<span data-ttu-id="1935b-112">Komut `dotnet new` , geçerli bir .NET Core projesi başlatmak için kullanışlı bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-112">The `dotnet new` command provides a convenient way to initialize a valid .NET Core project.</span></span>

<span data-ttu-id="1935b-113">Komutu, belirtilen şablon ve seçeneklere göre diskteki yapıtları oluşturmak için [şablon altyapısını](https://github.com/dotnet/templating) çağırır.</span><span class="sxs-lookup"><span data-stu-id="1935b-113">The command calls the [template engine](https://github.com/dotnet/templating) to create the artifacts on disk based on the specified template and options.</span></span>

## <a name="arguments"></a><span data-ttu-id="1935b-114">Arguments</span><span class="sxs-lookup"><span data-stu-id="1935b-114">Arguments</span></span>

`TEMPLATE`

<span data-ttu-id="1935b-115">Komut çağrıldığında örnek oluşturulacak şablon.</span><span class="sxs-lookup"><span data-stu-id="1935b-115">The template to instantiate when the command is invoked.</span></span> <span data-ttu-id="1935b-116">Her şablonun geçirebilmeniz için özel seçenekleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-116">Each template might have specific options you can pass.</span></span> <span data-ttu-id="1935b-117">Daha fazla bilgi için bkz. [şablon seçenekleri](#template-options).</span><span class="sxs-lookup"><span data-stu-id="1935b-117">For more information, see [Template options](#template-options).</span></span>

<span data-ttu-id="1935b-118">Değer, şablonlar veya **kısa ad** sütunundaki metin üzerinde tam eşleşme değilse, bu iki sütunda bir alt dize eşleşmesi gerçekleştirilir. `TEMPLATE`</span><span class="sxs-lookup"><span data-stu-id="1935b-118">If the `TEMPLATE` value isn't an exact match on text in the **Templates** or **Short Name** column, a substring match is performed on those two columns.</span></span>

# <a name="net-core-22tabnetcore22"></a>[<span data-ttu-id="1935b-119">.NET Core 2,2</span><span class="sxs-lookup"><span data-stu-id="1935b-119">.NET Core 2.2</span></span>](#tab/netcore22)

<span data-ttu-id="1935b-120">Komut, şablonların varsayılan bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1935b-120">The command contains a default list of templates.</span></span> <span data-ttu-id="1935b-121">Kullanılabilir `dotnet new -l` şablonların bir listesini almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-121">Use `dotnet new -l` to obtain a list of the available templates.</span></span> <span data-ttu-id="1935b-122">Aşağıdaki tabloda, .NET Core SDK 2.2.100 ile önceden yüklenmiş olarak gelen şablonlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-122">The following table shows the templates that come pre-installed with the .NET Core SDK 2.2.100.</span></span> <span data-ttu-id="1935b-123">Şablon için varsayılan dil, köşeli ayraçlar içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-123">The default language for the template is shown inside the brackets.</span></span>

| <span data-ttu-id="1935b-124">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="1935b-124">Templates</span></span>                                    | <span data-ttu-id="1935b-125">Kısa Ad</span><span class="sxs-lookup"><span data-stu-id="1935b-125">Short Name</span></span>        | <span data-ttu-id="1935b-126">Dil</span><span class="sxs-lookup"><span data-stu-id="1935b-126">Language</span></span>     | <span data-ttu-id="1935b-127">Etiketler</span><span class="sxs-lookup"><span data-stu-id="1935b-127">Tags</span></span>                                  |
|----------------------------------------------|-------------------|--------------|---------------------------------------|
| <span data-ttu-id="1935b-128">Konsol Uygulaması</span><span class="sxs-lookup"><span data-stu-id="1935b-128">Console Application</span></span>                          | `console`         | <span data-ttu-id="1935b-129">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-129">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-130">Ortak/konsol</span><span class="sxs-lookup"><span data-stu-id="1935b-130">Common/Console</span></span>                        |
| <span data-ttu-id="1935b-131">Sınıf kitaplığı</span><span class="sxs-lookup"><span data-stu-id="1935b-131">Class library</span></span>                                | `classlib`        | <span data-ttu-id="1935b-132">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-132">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-133">Ortak/Kitaplık</span><span class="sxs-lookup"><span data-stu-id="1935b-133">Common/Library</span></span>                        |
| <span data-ttu-id="1935b-134">Birim testi projesi</span><span class="sxs-lookup"><span data-stu-id="1935b-134">Unit Test Project</span></span>                            | `mstest`          | <span data-ttu-id="1935b-135">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-135">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-136">Test/MSTest</span><span class="sxs-lookup"><span data-stu-id="1935b-136">Test/MSTest</span></span>                           |
| <span data-ttu-id="1935b-137">NUnit 3 test projesi</span><span class="sxs-lookup"><span data-stu-id="1935b-137">NUnit 3 Test Project</span></span>                         | `nunit`           | <span data-ttu-id="1935b-138">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-138">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-139">Test/NUnit</span><span class="sxs-lookup"><span data-stu-id="1935b-139">Test/NUnit</span></span>                            |
| <span data-ttu-id="1935b-140">NUnit 3 test öğesi</span><span class="sxs-lookup"><span data-stu-id="1935b-140">NUnit 3 Test Item</span></span>                            | `nunit-test`      | <span data-ttu-id="1935b-141">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-141">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-142">Test/NUnit</span><span class="sxs-lookup"><span data-stu-id="1935b-142">Test/NUnit</span></span>                            |
| <span data-ttu-id="1935b-143">xUnit test projesi</span><span class="sxs-lookup"><span data-stu-id="1935b-143">xUnit Test Project</span></span>                           | `xunit`           | <span data-ttu-id="1935b-144">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-144">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-145">Test/xUnit</span><span class="sxs-lookup"><span data-stu-id="1935b-145">Test/xUnit</span></span>                            |
| <span data-ttu-id="1935b-146">Razor sayfası</span><span class="sxs-lookup"><span data-stu-id="1935b-146">Razor Page</span></span>                                   | `page`            | <span data-ttu-id="1935b-147">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-147">[C#]</span></span>         | <span data-ttu-id="1935b-148">Web/ASP. NET</span><span class="sxs-lookup"><span data-stu-id="1935b-148">Web/ASP.NET</span></span>                           |
| <span data-ttu-id="1935b-149">MVC Viewıtemts</span><span class="sxs-lookup"><span data-stu-id="1935b-149">MVC ViewImports</span></span>                              | `viewimports`     | <span data-ttu-id="1935b-150">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-150">[C#]</span></span>         | <span data-ttu-id="1935b-151">Web/ASP. NET</span><span class="sxs-lookup"><span data-stu-id="1935b-151">Web/ASP.NET</span></span>                           |
| <span data-ttu-id="1935b-152">MVC ViewStart</span><span class="sxs-lookup"><span data-stu-id="1935b-152">MVC ViewStart</span></span>                                | `viewstart`       | <span data-ttu-id="1935b-153">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-153">[C#]</span></span>         | <span data-ttu-id="1935b-154">Web/ASP. NET</span><span class="sxs-lookup"><span data-stu-id="1935b-154">Web/ASP.NET</span></span>                           |
| <span data-ttu-id="1935b-155">ASP.NET Core boş</span><span class="sxs-lookup"><span data-stu-id="1935b-155">ASP.NET Core Empty</span></span>                           | `web`             | <span data-ttu-id="1935b-156">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-156">[C#], F#</span></span>     | <span data-ttu-id="1935b-157">Web/boş</span><span class="sxs-lookup"><span data-stu-id="1935b-157">Web/Empty</span></span>                             |
| <span data-ttu-id="1935b-158">ASP.NET Core Web uygulaması (Model-View-Controller)</span><span class="sxs-lookup"><span data-stu-id="1935b-158">ASP.NET Core Web App (Model-View-Controller)</span></span> | `mvc`             | <span data-ttu-id="1935b-159">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-159">[C#], F#</span></span>     | <span data-ttu-id="1935b-160">Web/MVC</span><span class="sxs-lookup"><span data-stu-id="1935b-160">Web/MVC</span></span>                               |
| <span data-ttu-id="1935b-161">ASP.NET Core Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="1935b-161">ASP.NET Core Web App</span></span>                         | <span data-ttu-id="1935b-162">`webapp`, `razor`</span><span class="sxs-lookup"><span data-stu-id="1935b-162">`webapp`, `razor`</span></span> | <span data-ttu-id="1935b-163">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-163">[C#]</span></span>         | <span data-ttu-id="1935b-164">Web/MVC/Razor Pages</span><span class="sxs-lookup"><span data-stu-id="1935b-164">Web/MVC/Razor Pages</span></span>                   |
| <span data-ttu-id="1935b-165">Angular ile ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1935b-165">ASP.NET Core with Angular</span></span>                    | `angular`         | <span data-ttu-id="1935b-166">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-166">[C#]</span></span>         | <span data-ttu-id="1935b-167">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="1935b-167">Web/MVC/SPA</span></span>                           |
| <span data-ttu-id="1935b-168">Tepki verme. js ile ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1935b-168">ASP.NET Core with React.js</span></span>                   | `react`           | <span data-ttu-id="1935b-169">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-169">[C#]</span></span>         | <span data-ttu-id="1935b-170">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="1935b-170">Web/MVC/SPA</span></span>                           |
| <span data-ttu-id="1935b-171">Yanıt verir. js ve Redux ile ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1935b-171">ASP.NET Core with React.js and Redux</span></span>         | `reactredux`      | <span data-ttu-id="1935b-172">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-172">[C#]</span></span>         | <span data-ttu-id="1935b-173">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="1935b-173">Web/MVC/SPA</span></span>                           |
| <span data-ttu-id="1935b-174">Razor sınıf kitaplığı</span><span class="sxs-lookup"><span data-stu-id="1935b-174">Razor Class Library</span></span>                          | `razorclasslib`   | <span data-ttu-id="1935b-175">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-175">[C#]</span></span>         | <span data-ttu-id="1935b-176">Web/Razor/kitaplık/Razor sınıfı kitaplığı</span><span class="sxs-lookup"><span data-stu-id="1935b-176">Web/Razor/Library/Razor Class Library</span></span> |
| <span data-ttu-id="1935b-177">ASP.NET Core Web API 'SI</span><span class="sxs-lookup"><span data-stu-id="1935b-177">ASP.NET Core Web API</span></span>                         | `webapi`          | <span data-ttu-id="1935b-178">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-178">[C#], F#</span></span>     | <span data-ttu-id="1935b-179">Web/WebAPI</span><span class="sxs-lookup"><span data-stu-id="1935b-179">Web/WebAPI</span></span>                            |
| <span data-ttu-id="1935b-180">Global. JSON dosyası</span><span class="sxs-lookup"><span data-stu-id="1935b-180">global.json file</span></span>                             | `globaljson`      |              | <span data-ttu-id="1935b-181">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-181">Config</span></span>                                |
| <span data-ttu-id="1935b-182">NuGet yapılandırması</span><span class="sxs-lookup"><span data-stu-id="1935b-182">NuGet Config</span></span>                                 | `nugetconfig`     |              | <span data-ttu-id="1935b-183">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-183">Config</span></span>                                |
| <span data-ttu-id="1935b-184">Web yapılandırması</span><span class="sxs-lookup"><span data-stu-id="1935b-184">Web Config</span></span>                                   | `webconfig`       |              | <span data-ttu-id="1935b-185">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-185">Config</span></span>                                |
| <span data-ttu-id="1935b-186">Çözüm dosyası</span><span class="sxs-lookup"><span data-stu-id="1935b-186">Solution File</span></span>                                | `sln`             |              | <span data-ttu-id="1935b-187">Çözüm</span><span class="sxs-lookup"><span data-stu-id="1935b-187">Solution</span></span>                              |

# <a name="net-core-21tabnetcore21"></a>[<span data-ttu-id="1935b-188">.NET Core 2,1</span><span class="sxs-lookup"><span data-stu-id="1935b-188">.NET Core 2.1</span></span>](#tab/netcore21)

<span data-ttu-id="1935b-189">Komut, şablonların varsayılan bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1935b-189">The command contains a default list of templates.</span></span> <span data-ttu-id="1935b-190">Kullanılabilir `dotnet new -l` şablonların bir listesini almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-190">Use `dotnet new -l` to obtain a list of the available templates.</span></span> <span data-ttu-id="1935b-191">Aşağıdaki tabloda, .NET Core SDK 2.1.300 ile önceden yüklenmiş olarak gelen şablonlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-191">The following table shows the templates that come pre-installed with the .NET Core SDK 2.1.300.</span></span> <span data-ttu-id="1935b-192">Şablon için varsayılan dil, köşeli ayraçlar içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-192">The default language for the template is shown inside the brackets.</span></span>

| <span data-ttu-id="1935b-193">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="1935b-193">Templates</span></span>                                    | <span data-ttu-id="1935b-194">Kısa Ad</span><span class="sxs-lookup"><span data-stu-id="1935b-194">Short Name</span></span>      | <span data-ttu-id="1935b-195">Dil</span><span class="sxs-lookup"><span data-stu-id="1935b-195">Language</span></span>     | <span data-ttu-id="1935b-196">Etiketler</span><span class="sxs-lookup"><span data-stu-id="1935b-196">Tags</span></span>                                  |
|----------------------------------------------|-----------------|--------------|---------------------------------------|
| <span data-ttu-id="1935b-197">Konsol Uygulaması</span><span class="sxs-lookup"><span data-stu-id="1935b-197">Console Application</span></span>                          | `console`       | <span data-ttu-id="1935b-198">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-198">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-199">Ortak/konsol</span><span class="sxs-lookup"><span data-stu-id="1935b-199">Common/Console</span></span>                        |
| <span data-ttu-id="1935b-200">Sınıf kitaplığı</span><span class="sxs-lookup"><span data-stu-id="1935b-200">Class library</span></span>                                | `classlib`      | <span data-ttu-id="1935b-201">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-201">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-202">Ortak/Kitaplık</span><span class="sxs-lookup"><span data-stu-id="1935b-202">Common/Library</span></span>                        |
| <span data-ttu-id="1935b-203">Birim testi projesi</span><span class="sxs-lookup"><span data-stu-id="1935b-203">Unit Test Project</span></span>                            | `mstest`        | <span data-ttu-id="1935b-204">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-204">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-205">Test/MSTest</span><span class="sxs-lookup"><span data-stu-id="1935b-205">Test/MSTest</span></span>                           |
| <span data-ttu-id="1935b-206">xUnit test projesi</span><span class="sxs-lookup"><span data-stu-id="1935b-206">xUnit Test Project</span></span>                           | `xunit`         | <span data-ttu-id="1935b-207">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-207">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-208">Test/xUnit</span><span class="sxs-lookup"><span data-stu-id="1935b-208">Test/xUnit</span></span>                            |
| <span data-ttu-id="1935b-209">Razor sayfası</span><span class="sxs-lookup"><span data-stu-id="1935b-209">Razor Page</span></span>                                   | `page`          | <span data-ttu-id="1935b-210">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-210">[C#]</span></span>         | <span data-ttu-id="1935b-211">Web/ASP. NET</span><span class="sxs-lookup"><span data-stu-id="1935b-211">Web/ASP.NET</span></span>                           |
| <span data-ttu-id="1935b-212">MVC Viewıtemts</span><span class="sxs-lookup"><span data-stu-id="1935b-212">MVC ViewImports</span></span>                              | `viewimports`   | <span data-ttu-id="1935b-213">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-213">[C#]</span></span>         | <span data-ttu-id="1935b-214">Web/ASP. NET</span><span class="sxs-lookup"><span data-stu-id="1935b-214">Web/ASP.NET</span></span>                           |
| <span data-ttu-id="1935b-215">MVC ViewStart</span><span class="sxs-lookup"><span data-stu-id="1935b-215">MVC ViewStart</span></span>                                | `viewstart`     | <span data-ttu-id="1935b-216">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-216">[C#]</span></span>         | <span data-ttu-id="1935b-217">Web/ASP. NET</span><span class="sxs-lookup"><span data-stu-id="1935b-217">Web/ASP.NET</span></span>                           |
| <span data-ttu-id="1935b-218">ASP.NET Core boş</span><span class="sxs-lookup"><span data-stu-id="1935b-218">ASP.NET Core Empty</span></span>                           | `web`           | <span data-ttu-id="1935b-219">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-219">[C#], F#</span></span>     | <span data-ttu-id="1935b-220">Web/boş</span><span class="sxs-lookup"><span data-stu-id="1935b-220">Web/Empty</span></span>                             |
| <span data-ttu-id="1935b-221">ASP.NET Core Web uygulaması (Model-View-Controller)</span><span class="sxs-lookup"><span data-stu-id="1935b-221">ASP.NET Core Web App (Model-View-Controller)</span></span> | `mvc`           | <span data-ttu-id="1935b-222">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-222">[C#], F#</span></span>     | <span data-ttu-id="1935b-223">Web/MVC</span><span class="sxs-lookup"><span data-stu-id="1935b-223">Web/MVC</span></span>                               |
| <span data-ttu-id="1935b-224">ASP.NET Core Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="1935b-224">ASP.NET Core Web App</span></span>                         | `razor`         | <span data-ttu-id="1935b-225">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-225">[C#]</span></span>         | <span data-ttu-id="1935b-226">Web/MVC/Razor Pages</span><span class="sxs-lookup"><span data-stu-id="1935b-226">Web/MVC/Razor Pages</span></span>                   |
| <span data-ttu-id="1935b-227">Angular ile ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1935b-227">ASP.NET Core with Angular</span></span>                    | `angular`       | <span data-ttu-id="1935b-228">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-228">[C#]</span></span>         | <span data-ttu-id="1935b-229">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="1935b-229">Web/MVC/SPA</span></span>                           |
| <span data-ttu-id="1935b-230">Tepki verme. js ile ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1935b-230">ASP.NET Core with React.js</span></span>                   | `react`         | <span data-ttu-id="1935b-231">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-231">[C#]</span></span>         | <span data-ttu-id="1935b-232">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="1935b-232">Web/MVC/SPA</span></span>                           |
| <span data-ttu-id="1935b-233">Yanıt verir. js ve Redux ile ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1935b-233">ASP.NET Core with React.js and Redux</span></span>         | `reactredux`    | <span data-ttu-id="1935b-234">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-234">[C#]</span></span>         | <span data-ttu-id="1935b-235">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="1935b-235">Web/MVC/SPA</span></span>                           | 
| <span data-ttu-id="1935b-236">Razor sınıf kitaplığı</span><span class="sxs-lookup"><span data-stu-id="1935b-236">Razor Class Library</span></span>                          | `razorclasslib` | <span data-ttu-id="1935b-237">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-237">[C#]</span></span>         | <span data-ttu-id="1935b-238">Web/Razor/kitaplık/Razor sınıfı kitaplığı</span><span class="sxs-lookup"><span data-stu-id="1935b-238">Web/Razor/Library/Razor Class Library</span></span> |
| <span data-ttu-id="1935b-239">ASP.NET Core Web API 'SI</span><span class="sxs-lookup"><span data-stu-id="1935b-239">ASP.NET Core Web API</span></span>                         | `webapi`        | <span data-ttu-id="1935b-240">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-240">[C#], F#</span></span>     | <span data-ttu-id="1935b-241">Web/WebAPI</span><span class="sxs-lookup"><span data-stu-id="1935b-241">Web/WebAPI</span></span>                            |
| <span data-ttu-id="1935b-242">Global. JSON dosyası</span><span class="sxs-lookup"><span data-stu-id="1935b-242">global.json file</span></span>                             | `globaljson`    |              | <span data-ttu-id="1935b-243">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-243">Config</span></span>                                |
| <span data-ttu-id="1935b-244">NuGet yapılandırması</span><span class="sxs-lookup"><span data-stu-id="1935b-244">NuGet Config</span></span>                                 | `nugetconfig`   |              | <span data-ttu-id="1935b-245">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-245">Config</span></span>                                |
| <span data-ttu-id="1935b-246">Web yapılandırması</span><span class="sxs-lookup"><span data-stu-id="1935b-246">Web Config</span></span>                                   | `webconfig`     |              | <span data-ttu-id="1935b-247">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-247">Config</span></span>                                |
| <span data-ttu-id="1935b-248">Çözüm dosyası</span><span class="sxs-lookup"><span data-stu-id="1935b-248">Solution File</span></span>                                | `sln`           |              | <span data-ttu-id="1935b-249">Çözüm</span><span class="sxs-lookup"><span data-stu-id="1935b-249">Solution</span></span>                              |

# <a name="net-core-20tabnetcore20"></a>[<span data-ttu-id="1935b-250">.NET Core 2,0</span><span class="sxs-lookup"><span data-stu-id="1935b-250">.NET Core 2.0</span></span>](#tab/netcore20)

<span data-ttu-id="1935b-251">Komut, şablonların varsayılan bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1935b-251">The command contains a default list of templates.</span></span> <span data-ttu-id="1935b-252">Kullanılabilir `dotnet new -l` şablonların bir listesini almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-252">Use `dotnet new -l` to obtain a list of the available templates.</span></span> <span data-ttu-id="1935b-253">Aşağıdaki tabloda, .NET Core SDK 2.0.0 ile önceden yüklenmiş olarak gelen şablonlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-253">The following table shows the templates that come pre-installed with the .NET Core SDK 2.0.0.</span></span> <span data-ttu-id="1935b-254">Şablon için varsayılan dil, köşeli ayraçlar içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-254">The default language for the template is shown inside the brackets.</span></span>

| <span data-ttu-id="1935b-255">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="1935b-255">Templates</span></span>                                    | <span data-ttu-id="1935b-256">Kısa Ad</span><span class="sxs-lookup"><span data-stu-id="1935b-256">Short Name</span></span>    | <span data-ttu-id="1935b-257">Dil</span><span class="sxs-lookup"><span data-stu-id="1935b-257">Language</span></span>     | <span data-ttu-id="1935b-258">Etiketler</span><span class="sxs-lookup"><span data-stu-id="1935b-258">Tags</span></span>                |
|----------------------------------------------|---------------|--------------|---------------------|
| <span data-ttu-id="1935b-259">Konsol Uygulaması</span><span class="sxs-lookup"><span data-stu-id="1935b-259">Console Application</span></span>                          | `console`     | <span data-ttu-id="1935b-260">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-260">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-261">Ortak/konsol</span><span class="sxs-lookup"><span data-stu-id="1935b-261">Common/Console</span></span>      |
| <span data-ttu-id="1935b-262">Sınıf kitaplığı</span><span class="sxs-lookup"><span data-stu-id="1935b-262">Class library</span></span>                                | `classlib`    | <span data-ttu-id="1935b-263">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-263">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-264">Ortak/Kitaplık</span><span class="sxs-lookup"><span data-stu-id="1935b-264">Common/Library</span></span>      |
| <span data-ttu-id="1935b-265">Birim testi projesi</span><span class="sxs-lookup"><span data-stu-id="1935b-265">Unit Test Project</span></span>                            | `mstest`      | <span data-ttu-id="1935b-266">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-266">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-267">Test/MSTest</span><span class="sxs-lookup"><span data-stu-id="1935b-267">Test/MSTest</span></span>         |
| <span data-ttu-id="1935b-268">xUnit test projesi</span><span class="sxs-lookup"><span data-stu-id="1935b-268">xUnit Test Project</span></span>                           | `xunit`       | <span data-ttu-id="1935b-269">[C#], F#, VB</span><span class="sxs-lookup"><span data-stu-id="1935b-269">[C#], F#, VB</span></span> | <span data-ttu-id="1935b-270">Test/xUnit</span><span class="sxs-lookup"><span data-stu-id="1935b-270">Test/xUnit</span></span>          |
| <span data-ttu-id="1935b-271">ASP.NET Core boş</span><span class="sxs-lookup"><span data-stu-id="1935b-271">ASP.NET Core Empty</span></span>                           | `web`         | <span data-ttu-id="1935b-272">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-272">[C#], F#</span></span>     | <span data-ttu-id="1935b-273">Web/boş</span><span class="sxs-lookup"><span data-stu-id="1935b-273">Web/Empty</span></span>           |
| <span data-ttu-id="1935b-274">ASP.NET Core Web uygulaması (Model-View-Controller)</span><span class="sxs-lookup"><span data-stu-id="1935b-274">ASP.NET Core Web App (Model-View-Controller)</span></span> | `mvc`         | <span data-ttu-id="1935b-275">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-275">[C#], F#</span></span>     | <span data-ttu-id="1935b-276">Web/MVC</span><span class="sxs-lookup"><span data-stu-id="1935b-276">Web/MVC</span></span>             |
| <span data-ttu-id="1935b-277">ASP.NET Core Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="1935b-277">ASP.NET Core Web App</span></span>                         | `razor`       | <span data-ttu-id="1935b-278">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-278">[C#]</span></span>         | <span data-ttu-id="1935b-279">Web/MVC/Razor Pages</span><span class="sxs-lookup"><span data-stu-id="1935b-279">Web/MVC/Razor Pages</span></span> |
| <span data-ttu-id="1935b-280">Angular ile ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1935b-280">ASP.NET Core with Angular</span></span>                    | `angular`     | <span data-ttu-id="1935b-281">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-281">[C#]</span></span>         | <span data-ttu-id="1935b-282">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="1935b-282">Web/MVC/SPA</span></span>         |
| <span data-ttu-id="1935b-283">Tepki verme. js ile ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1935b-283">ASP.NET Core with React.js</span></span>                   | `react`       | <span data-ttu-id="1935b-284">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-284">[C#]</span></span>         | <span data-ttu-id="1935b-285">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="1935b-285">Web/MVC/SPA</span></span>         |
| <span data-ttu-id="1935b-286">Yanıt verir. js ve Redux ile ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="1935b-286">ASP.NET Core with React.js and Redux</span></span>         | `reactredux`  | <span data-ttu-id="1935b-287">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-287">[C#]</span></span>         | <span data-ttu-id="1935b-288">MVC/Web/SPA</span><span class="sxs-lookup"><span data-stu-id="1935b-288">Web/MVC/SPA</span></span>         |
| <span data-ttu-id="1935b-289">ASP.NET Core Web API 'SI</span><span class="sxs-lookup"><span data-stu-id="1935b-289">ASP.NET Core Web API</span></span>                         | `webapi`      | <span data-ttu-id="1935b-290">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-290">[C#], F#</span></span>     | <span data-ttu-id="1935b-291">Web/WebAPI</span><span class="sxs-lookup"><span data-stu-id="1935b-291">Web/WebAPI</span></span>          |
| <span data-ttu-id="1935b-292">Global. JSON dosyası</span><span class="sxs-lookup"><span data-stu-id="1935b-292">global.json file</span></span>                             | `globaljson`  |              | <span data-ttu-id="1935b-293">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-293">Config</span></span>              |
| <span data-ttu-id="1935b-294">NuGet yapılandırması</span><span class="sxs-lookup"><span data-stu-id="1935b-294">Nuget Config</span></span>                                 | `nugetconfig` |              | <span data-ttu-id="1935b-295">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-295">Config</span></span>              |
| <span data-ttu-id="1935b-296">Web yapılandırması</span><span class="sxs-lookup"><span data-stu-id="1935b-296">Web Config</span></span>                                   | `webconfig`   |              | <span data-ttu-id="1935b-297">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-297">Config</span></span>              |
| <span data-ttu-id="1935b-298">Çözüm dosyası</span><span class="sxs-lookup"><span data-stu-id="1935b-298">Solution File</span></span>                                | `sln`         |              | <span data-ttu-id="1935b-299">Çözüm</span><span class="sxs-lookup"><span data-stu-id="1935b-299">Solution</span></span>            |
| <span data-ttu-id="1935b-300">Razor sayfası</span><span class="sxs-lookup"><span data-stu-id="1935b-300">Razor Page</span></span>                                   | `page`        |              | <span data-ttu-id="1935b-301">Web/ASP. NET</span><span class="sxs-lookup"><span data-stu-id="1935b-301">Web/ASP.NET</span></span>         |
| <span data-ttu-id="1935b-302">MVC Viewıtemts</span><span class="sxs-lookup"><span data-stu-id="1935b-302">MVC ViewImports</span></span>                              | `viewimports` |              | <span data-ttu-id="1935b-303">Web/ASP. NET</span><span class="sxs-lookup"><span data-stu-id="1935b-303">Web/ASP.NET</span></span>         |
| <span data-ttu-id="1935b-304">MVC ViewStart</span><span class="sxs-lookup"><span data-stu-id="1935b-304">MVC ViewStart</span></span>                                | `viewstart`   |              | <span data-ttu-id="1935b-305">Web/ASP. NET</span><span class="sxs-lookup"><span data-stu-id="1935b-305">Web/ASP.NET</span></span>         |

# <a name="net-core-1xtabnetcore1x"></a>[<span data-ttu-id="1935b-306">.NET Core 1. x</span><span class="sxs-lookup"><span data-stu-id="1935b-306">.NET Core 1.x</span></span>](#tab/netcore1x)

<span data-ttu-id="1935b-307">Komut, şablonların varsayılan bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1935b-307">The command contains a default list of templates.</span></span> <span data-ttu-id="1935b-308">Kullanılabilir `dotnet new -all` şablonların bir listesini almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-308">Use `dotnet new -all` to obtain a list of the available templates.</span></span> <span data-ttu-id="1935b-309">Aşağıdaki tabloda, .NET Core SDK 1.0.1 ile önceden yüklenmiş olarak gelen şablonlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-309">The following table shows the templates that come pre-installed with the .NET Core SDK 1.0.1.</span></span> <span data-ttu-id="1935b-310">Şablon için varsayılan dil, köşeli ayraçlar içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-310">The default language for the template is shown inside the brackets.</span></span>

| <span data-ttu-id="1935b-311">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="1935b-311">Templates</span></span>            | <span data-ttu-id="1935b-312">Kısa Ad</span><span class="sxs-lookup"><span data-stu-id="1935b-312">Short Name</span></span>    | <span data-ttu-id="1935b-313">Dil</span><span class="sxs-lookup"><span data-stu-id="1935b-313">Language</span></span> | <span data-ttu-id="1935b-314">Etiketler</span><span class="sxs-lookup"><span data-stu-id="1935b-314">Tags</span></span>           |
|----------------------|---------------|----------|----------------|
| <span data-ttu-id="1935b-315">Konsol Uygulaması</span><span class="sxs-lookup"><span data-stu-id="1935b-315">Console Application</span></span>  | `console`     | <span data-ttu-id="1935b-316">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-316">[C#], F#</span></span> | <span data-ttu-id="1935b-317">Ortak/konsol</span><span class="sxs-lookup"><span data-stu-id="1935b-317">Common/Console</span></span> |
| <span data-ttu-id="1935b-318">Sınıf kitaplığı</span><span class="sxs-lookup"><span data-stu-id="1935b-318">Class library</span></span>        | `classlib`    | <span data-ttu-id="1935b-319">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-319">[C#], F#</span></span> | <span data-ttu-id="1935b-320">Ortak/Kitaplık</span><span class="sxs-lookup"><span data-stu-id="1935b-320">Common/Library</span></span> |
| <span data-ttu-id="1935b-321">Birim testi projesi</span><span class="sxs-lookup"><span data-stu-id="1935b-321">Unit Test Project</span></span>    | `mstest`      | <span data-ttu-id="1935b-322">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-322">[C#], F#</span></span> | <span data-ttu-id="1935b-323">Test/MSTest</span><span class="sxs-lookup"><span data-stu-id="1935b-323">Test/MSTest</span></span>    |
| <span data-ttu-id="1935b-324">xUnit test projesi</span><span class="sxs-lookup"><span data-stu-id="1935b-324">xUnit Test Project</span></span>   | `xunit`       | <span data-ttu-id="1935b-325">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-325">[C#], F#</span></span> | <span data-ttu-id="1935b-326">Test/xUnit</span><span class="sxs-lookup"><span data-stu-id="1935b-326">Test/xUnit</span></span>     |
| <span data-ttu-id="1935b-327">ASP.NET Core boş</span><span class="sxs-lookup"><span data-stu-id="1935b-327">ASP.NET Core Empty</span></span>   | `web`         | <span data-ttu-id="1935b-328">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-328">[C#]</span></span>     | <span data-ttu-id="1935b-329">Web/boş</span><span class="sxs-lookup"><span data-stu-id="1935b-329">Web/Empty</span></span>      |
| <span data-ttu-id="1935b-330">ASP.NET Core Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="1935b-330">ASP.NET Core Web App</span></span> | `mvc`         | <span data-ttu-id="1935b-331">[C#],F#</span><span class="sxs-lookup"><span data-stu-id="1935b-331">[C#], F#</span></span> | <span data-ttu-id="1935b-332">Web/MVC</span><span class="sxs-lookup"><span data-stu-id="1935b-332">Web/MVC</span></span>        |
| <span data-ttu-id="1935b-333">ASP.NET Core Web API 'SI</span><span class="sxs-lookup"><span data-stu-id="1935b-333">ASP.NET Core Web API</span></span> | `webapi`      | <span data-ttu-id="1935b-334">[C#]</span><span class="sxs-lookup"><span data-stu-id="1935b-334">[C#]</span></span>     | <span data-ttu-id="1935b-335">Web/WebAPI</span><span class="sxs-lookup"><span data-stu-id="1935b-335">Web/WebAPI</span></span>     |
| <span data-ttu-id="1935b-336">NuGet yapılandırması</span><span class="sxs-lookup"><span data-stu-id="1935b-336">Nuget Config</span></span>         | `nugetconfig` |          | <span data-ttu-id="1935b-337">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-337">Config</span></span>         |
| <span data-ttu-id="1935b-338">Web yapılandırması</span><span class="sxs-lookup"><span data-stu-id="1935b-338">Web Config</span></span>           | `webconfig`   |          | <span data-ttu-id="1935b-339">Config</span><span class="sxs-lookup"><span data-stu-id="1935b-339">Config</span></span>         |
| <span data-ttu-id="1935b-340">Çözüm dosyası</span><span class="sxs-lookup"><span data-stu-id="1935b-340">Solution File</span></span>        | `sln`         |          | <span data-ttu-id="1935b-341">Çözüm</span><span class="sxs-lookup"><span data-stu-id="1935b-341">Solution</span></span>       |

---

## <a name="options"></a><span data-ttu-id="1935b-342">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="1935b-342">Options</span></span>

# <a name="net-core-22tabnetcore22"></a>[<span data-ttu-id="1935b-343">.NET Core 2,2</span><span class="sxs-lookup"><span data-stu-id="1935b-343">.NET Core 2.2</span></span>](#tab/netcore22)

`--dry-run`

<span data-ttu-id="1935b-344">Bir şablon oluşturulmasına neden olacaksa, verilen komutun çalıştırılması durumunda ne olacağını gösteren bir Özet görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1935b-344">Displays a summary of what would happen if the given command were run if it would result in a template creation.</span></span>

`--force`

<span data-ttu-id="1935b-345">Var olan dosyaları değiştirebilse bile içeriğin oluşturulmasını zorlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-345">Forces content to be generated even if it would change existing files.</span></span> <span data-ttu-id="1935b-346">Çıkış dizini zaten bir proje içerdiğinde bu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-346">This is required when the output directory already contains a project.</span></span>

`-h|--help`

<span data-ttu-id="1935b-347">Komut için yardım yazdırır.</span><span class="sxs-lookup"><span data-stu-id="1935b-347">Prints out help for the command.</span></span> <span data-ttu-id="1935b-348">`dotnet new` Komutun kendisi veya gibi herhangi bir şablon `dotnet new mvc --help`için çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-348">It can be invoked for the `dotnet new` command itself or for any template, such as `dotnet new mvc --help`.</span></span>

`-i|--install <PATH|NUGET_ID>`

<span data-ttu-id="1935b-349">`PATH` Veya`NUGET_ID` tarafından sağlanmış bir kaynak veya şablon paketi kurar.</span><span class="sxs-lookup"><span data-stu-id="1935b-349">Installs a source or template pack from the `PATH` or `NUGET_ID` provided.</span></span> <span data-ttu-id="1935b-350">Şablon paketinin bir ön sürümü sürümünü yüklemek istiyorsanız, sürümü biçiminde `<package-name>::<package-version>`belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1935b-350">If you want to install a prerelease version of a template package, you need to specify the version in the format of `<package-name>::<package-version>`.</span></span> <span data-ttu-id="1935b-351">Varsayılan olarak, `dotnet new` en \* son kararlı paket sürümünü temsil eden sürüm için geçirir.</span><span class="sxs-lookup"><span data-stu-id="1935b-351">By default, `dotnet new` passes \* for the version, which represents the last stable package version.</span></span> <span data-ttu-id="1935b-352">[Örnekler](#examples) bölümündeki bir örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="1935b-352">See an example at the [Examples](#examples) section.</span></span>

<span data-ttu-id="1935b-353">Özel şablonlar oluşturma hakkında daha fazla bilgi için bkz. [DotNet New Için özel şablonlar](custom-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1935b-353">For information on creating custom templates, see [Custom templates for dotnet new](custom-templates.md).</span></span>

`-l|--list`

<span data-ttu-id="1935b-354">Belirtilen adı içeren şablonları listeler.</span><span class="sxs-lookup"><span data-stu-id="1935b-354">Lists templates containing the specified name.</span></span> <span data-ttu-id="1935b-355">`dotnet new` Komut için çağrılırsa, belirtilen dizin için kullanılabilir olabilecek şablonları listeler.</span><span class="sxs-lookup"><span data-stu-id="1935b-355">If invoked for the `dotnet new` command, it lists the possible templates available for the given directory.</span></span> <span data-ttu-id="1935b-356">Örneğin, dizin zaten bir proje içeriyorsa, tüm proje şablonlarını listeetmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-356">For example if the directory already contains a project, it doesn't list all project templates.</span></span>

`-lang|--language {C#|F#|VB}`

<span data-ttu-id="1935b-357">Oluşturulacak şablonun dili.</span><span class="sxs-lookup"><span data-stu-id="1935b-357">The language of the template to create.</span></span> <span data-ttu-id="1935b-358">Kabul edilen dil şablona göre değişir (bkz. [arguments](#arguments) bölümünde Varsayılanlar).</span><span class="sxs-lookup"><span data-stu-id="1935b-358">The language accepted varies by the template (see defaults in the [arguments](#arguments) section).</span></span> <span data-ttu-id="1935b-359">Bazı şablonlar için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="1935b-359">Not valid for some templates.</span></span>

> [!NOTE]
> <span data-ttu-id="1935b-360">Bazı kabuklar `#` özel bir karakter olarak yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="1935b-360">Some shells interpret `#` as a special character.</span></span> <span data-ttu-id="1935b-361">Bu durumlarda, gibi dil parametre değerini `dotnet new console -lang "F#"`almalısınız.</span><span class="sxs-lookup"><span data-stu-id="1935b-361">In those cases, you need to enclose the language parameter value, such as `dotnet new console -lang "F#"`.</span></span>

`-n|--name <OUTPUT_NAME>`

<span data-ttu-id="1935b-362">Oluşturulan çıkışın adı.</span><span class="sxs-lookup"><span data-stu-id="1935b-362">The name for the created output.</span></span> <span data-ttu-id="1935b-363">Ad belirtilmemişse, geçerli dizinin adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1935b-363">If no name is specified, the name of the current directory is used.</span></span>

`--nuget-source`

<span data-ttu-id="1935b-364">Yüklemesi sırasında kullanılacak bir NuGet kaynağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-364">Specifies a NuGet source to use during install.</span></span>

`-o|--output <OUTPUT_DIRECTORY>`

<span data-ttu-id="1935b-365">Oluşturulan çıkışın yerleştirileceği konum.</span><span class="sxs-lookup"><span data-stu-id="1935b-365">Location to place the generated output.</span></span> <span data-ttu-id="1935b-366">Geçerli dizin varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="1935b-366">The default is the current directory.</span></span>

`--type`

<span data-ttu-id="1935b-367">Şablonları kullanılabilir türlerine göre filtreler.</span><span class="sxs-lookup"><span data-stu-id="1935b-367">Filters templates based on available types.</span></span> <span data-ttu-id="1935b-368">Önceden tanımlanmış değerler şunlardır "proje", "öğe" veya "diğer".</span><span class="sxs-lookup"><span data-stu-id="1935b-368">Predefined values are "project", "item", or "other".</span></span>

`-u|--uninstall <PATH|NUGET_ID>`

<span data-ttu-id="1935b-369">`PATH` Veya`NUGET_ID` belirtilen bir kaynak veya şablon paketini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1935b-369">Uninstalls a source or template pack at the `PATH` or `NUGET_ID` provided.</span></span> <span data-ttu-id="1935b-370">`<PATH|NUGET_ID>` Değer hariç tutularak, yüklü olan tüm şablon paketleri ve bunlarla ilişkili şablonlar görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1935b-370">When excluding the `<PATH|NUGET_ID>` value, all currently installed template packs and their associated templates are displayed.</span></span>

> [!NOTE]
> <span data-ttu-id="1935b-371">Bir `PATH`şablonu kullanarak kaldırmak için, yolu tam olarak nitelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1935b-371">To uninstall a template using a `PATH`, you need to fully qualify the path.</span></span> <span data-ttu-id="1935b-372">Örneğin, *C:/kullanıcıları/\<Kullanıcı >/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* çalışır, ancak içeren klasörden *./GarciaSoftware.ConsoleTemplate.CSharp* olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="1935b-372">For example, *C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* will work, but *./GarciaSoftware.ConsoleTemplate.CSharp* from the containing folder will not.</span></span>
> <span data-ttu-id="1935b-373">Ayrıca, şablon yolunuza son Sonlandırıcı Dizin eğik çizgi eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="1935b-373">Additionally, do not include a final terminating directory slash on your template path.</span></span>

# <a name="net-core-21tabnetcore21"></a>[<span data-ttu-id="1935b-374">.NET Core 2,1</span><span class="sxs-lookup"><span data-stu-id="1935b-374">.NET Core 2.1</span></span>](#tab/netcore21)

`--force`

<span data-ttu-id="1935b-375">Var olan dosyaları değiştirebilse bile içeriğin oluşturulmasını zorlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-375">Forces content to be generated even if it would change existing files.</span></span> <span data-ttu-id="1935b-376">Çıkış dizini zaten bir proje içerdiğinde bu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-376">This is required when the output directory already contains a project.</span></span>

`-h|--help`

<span data-ttu-id="1935b-377">Komut için yardım yazdırır.</span><span class="sxs-lookup"><span data-stu-id="1935b-377">Prints out help for the command.</span></span> <span data-ttu-id="1935b-378">`dotnet new` Komutun kendisi veya gibi herhangi bir şablon `dotnet new mvc --help`için çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-378">It can be invoked for the `dotnet new` command itself or for any template, such as `dotnet new mvc --help`.</span></span>

`-i|--install <PATH|NUGET_ID>`

<span data-ttu-id="1935b-379">`PATH` Veya`NUGET_ID` tarafından sağlanmış bir kaynak veya şablon paketi kurar.</span><span class="sxs-lookup"><span data-stu-id="1935b-379">Installs a source or template pack from the `PATH` or `NUGET_ID` provided.</span></span> <span data-ttu-id="1935b-380">Şablon paketinin bir ön sürümü sürümünü yüklemek istiyorsanız, sürümü biçiminde `<package-name>::<package-version>`belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1935b-380">If you want to install a prerelease version of a template package, you need to specify the version in the format of `<package-name>::<package-version>`.</span></span> <span data-ttu-id="1935b-381">Varsayılan olarak, `dotnet new` en \* son kararlı paket sürümünü temsil eden sürüm için geçirir.</span><span class="sxs-lookup"><span data-stu-id="1935b-381">By default, `dotnet new` passes \* for the version, which represents the last stable package version.</span></span> <span data-ttu-id="1935b-382">[Örnekler](#examples) bölümündeki bir örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="1935b-382">See an example at the [Examples](#examples) section.</span></span>

<span data-ttu-id="1935b-383">Özel şablonlar oluşturma hakkında daha fazla bilgi için bkz. [DotNet New Için özel şablonlar](custom-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1935b-383">For information on creating custom templates, see [Custom templates for dotnet new](custom-templates.md).</span></span>

`-l|--list`

<span data-ttu-id="1935b-384">Belirtilen adı içeren şablonları listeler.</span><span class="sxs-lookup"><span data-stu-id="1935b-384">Lists templates containing the specified name.</span></span> <span data-ttu-id="1935b-385">`dotnet new` Komut için çağrılırsa, belirtilen dizin için kullanılabilir olabilecek şablonları listeler.</span><span class="sxs-lookup"><span data-stu-id="1935b-385">If invoked for the `dotnet new` command, it lists the possible templates available for the given directory.</span></span> <span data-ttu-id="1935b-386">Örneğin, dizin zaten bir proje içeriyorsa, tüm proje şablonlarını listeetmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-386">For example if the directory already contains a project, it doesn't list all project templates.</span></span>

`-lang|--language {C#|F#|VB}`

<span data-ttu-id="1935b-387">Oluşturulacak şablonun dili.</span><span class="sxs-lookup"><span data-stu-id="1935b-387">The language of the template to create.</span></span> <span data-ttu-id="1935b-388">Kabul edilen dil şablona göre değişir (bkz. [arguments](#arguments) bölümünde Varsayılanlar).</span><span class="sxs-lookup"><span data-stu-id="1935b-388">The language accepted varies by the template (see defaults in the [arguments](#arguments) section).</span></span> <span data-ttu-id="1935b-389">Bazı şablonlar için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="1935b-389">Not valid for some templates.</span></span>

> [!NOTE]
> <span data-ttu-id="1935b-390">Bazı kabuklar `#` özel bir karakter olarak yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="1935b-390">Some shells interpret `#` as a special character.</span></span> <span data-ttu-id="1935b-391">Bu durumlarda, gibi dil parametre değerini `dotnet new console -lang "F#"`almalısınız.</span><span class="sxs-lookup"><span data-stu-id="1935b-391">In those cases, you need to enclose the language parameter value, such as `dotnet new console -lang "F#"`.</span></span>

`-n|--name <OUTPUT_NAME>`

<span data-ttu-id="1935b-392">Oluşturulan çıkışın adı.</span><span class="sxs-lookup"><span data-stu-id="1935b-392">The name for the created output.</span></span> <span data-ttu-id="1935b-393">Ad belirtilmemişse, geçerli dizinin adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1935b-393">If no name is specified, the name of the current directory is used.</span></span>

`--nuget-source`

<span data-ttu-id="1935b-394">Yüklemesi sırasında kullanılacak bir NuGet kaynağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-394">Specifies a NuGet source to use during install.</span></span>

`-o|--output <OUTPUT_DIRECTORY>`

<span data-ttu-id="1935b-395">Oluşturulan çıkışın yerleştirileceği konum.</span><span class="sxs-lookup"><span data-stu-id="1935b-395">Location to place the generated output.</span></span> <span data-ttu-id="1935b-396">Geçerli dizin varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="1935b-396">The default is the current directory.</span></span>

`--type`

<span data-ttu-id="1935b-397">Şablonları kullanılabilir türlerine göre filtreler.</span><span class="sxs-lookup"><span data-stu-id="1935b-397">Filters templates based on available types.</span></span> <span data-ttu-id="1935b-398">Önceden tanımlanmış değerler şunlardır "proje", "öğe" veya "diğer".</span><span class="sxs-lookup"><span data-stu-id="1935b-398">Predefined values are "project", "item" or "other".</span></span>

`-u|--uninstall <PATH|NUGET_ID>`

<span data-ttu-id="1935b-399">`PATH` Veya`NUGET_ID` belirtilen bir kaynak veya şablon paketini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1935b-399">Uninstalls a source or template pack at the `PATH` or `NUGET_ID` provided.</span></span>

> [!NOTE]
> <span data-ttu-id="1935b-400">Bir `PATH`şablonu kullanarak kaldırmak için, yolu tam olarak nitelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1935b-400">To uninstall a template using a `PATH`, you need to fully qualify the path.</span></span> <span data-ttu-id="1935b-401">Örneğin, *C:/kullanıcıları/\<Kullanıcı >/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* çalışır, ancak içeren klasörden *./GarciaSoftware.ConsoleTemplate.CSharp* olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="1935b-401">For example, *C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* will work, but *./GarciaSoftware.ConsoleTemplate.CSharp* from the containing folder will not.</span></span>
> <span data-ttu-id="1935b-402">Ayrıca, şablon yolunuza son Sonlandırıcı Dizin eğik çizgi eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="1935b-402">Additionally, do not include a final terminating directory slash on your template path.</span></span>

# <a name="net-core-20tabnetcore20"></a>[<span data-ttu-id="1935b-403">.NET Core 2,0</span><span class="sxs-lookup"><span data-stu-id="1935b-403">.NET Core 2.0</span></span>](#tab/netcore20)

`--force`

<span data-ttu-id="1935b-404">Var olan dosyaları değiştirebilse bile içeriğin oluşturulmasını zorlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-404">Forces content to be generated even if it would change existing files.</span></span> <span data-ttu-id="1935b-405">Çıkış dizini zaten bir proje içerdiğinde bu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-405">This is required when the output directory already contains a project.</span></span>

`-h|--help`

<span data-ttu-id="1935b-406">Komut için yardım yazdırır.</span><span class="sxs-lookup"><span data-stu-id="1935b-406">Prints out help for the command.</span></span> <span data-ttu-id="1935b-407">`dotnet new` Komutun kendisi veya gibi herhangi bir şablon `dotnet new mvc --help`için çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-407">It can be invoked for the `dotnet new` command itself or for any template, such as `dotnet new mvc --help`.</span></span>

`-i|--install <PATH|NUGET_ID>`

<span data-ttu-id="1935b-408">`PATH` Veya`NUGET_ID` tarafından sağlanmış bir kaynak veya şablon paketi kurar.</span><span class="sxs-lookup"><span data-stu-id="1935b-408">Installs a source or template pack from the `PATH` or `NUGET_ID` provided.</span></span> <span data-ttu-id="1935b-409">Şablon paketinin bir ön sürümü sürümünü yüklemek istiyorsanız, sürümü biçiminde `<package-name>::<package-version>`belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1935b-409">If you want to install a prerelease version of a template package, you need to specify the version in the format of `<package-name>::<package-version>`.</span></span> <span data-ttu-id="1935b-410">Varsayılan olarak, `dotnet new` en \* son kararlı paket sürümünü temsil eden sürüm için geçirir.</span><span class="sxs-lookup"><span data-stu-id="1935b-410">By default, `dotnet new` passes \* for the version, which represents the last stable package version.</span></span> <span data-ttu-id="1935b-411">[Örnekler](#examples) bölümündeki bir örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="1935b-411">See an example at the [Examples](#examples) section.</span></span>

<span data-ttu-id="1935b-412">Özel şablonlar oluşturma hakkında daha fazla bilgi için bkz. [DotNet New Için özel şablonlar](custom-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1935b-412">For information on creating custom templates, see [Custom templates for dotnet new](custom-templates.md).</span></span>

`-l|--list`

<span data-ttu-id="1935b-413">Belirtilen adı içeren şablonları listeler.</span><span class="sxs-lookup"><span data-stu-id="1935b-413">Lists templates containing the specified name.</span></span> <span data-ttu-id="1935b-414">`dotnet new` Komut için çağrılırsa, belirtilen dizin için kullanılabilir olabilecek şablonları listeler.</span><span class="sxs-lookup"><span data-stu-id="1935b-414">If invoked for the `dotnet new` command, it lists the possible templates available for the given directory.</span></span> <span data-ttu-id="1935b-415">Örneğin, dizin zaten bir proje içeriyorsa, tüm proje şablonlarını listeetmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-415">For example if the directory already contains a project, it doesn't list all project templates.</span></span>

`-lang|--language {C#|F#|VB}`

<span data-ttu-id="1935b-416">Oluşturulacak şablonun dili.</span><span class="sxs-lookup"><span data-stu-id="1935b-416">The language of the template to create.</span></span> <span data-ttu-id="1935b-417">Kabul edilen dil şablona göre değişir (bkz. [arguments](#arguments) bölümünde Varsayılanlar).</span><span class="sxs-lookup"><span data-stu-id="1935b-417">The language accepted varies by the template (see defaults in the [arguments](#arguments) section).</span></span> <span data-ttu-id="1935b-418">Bazı şablonlar için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="1935b-418">Not valid for some templates.</span></span>

> [!NOTE]
> <span data-ttu-id="1935b-419">Bazı kabuklar `#` özel bir karakter olarak yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="1935b-419">Some shells interpret `#` as a special character.</span></span> <span data-ttu-id="1935b-420">Bu durumlarda, gibi dil parametre değerini `dotnet new console -lang "F#"`almalısınız.</span><span class="sxs-lookup"><span data-stu-id="1935b-420">In those cases, you need to enclose the language parameter value, such as `dotnet new console -lang "F#"`.</span></span>

`-n|--name <OUTPUT_NAME>`

<span data-ttu-id="1935b-421">Oluşturulan çıkışın adı.</span><span class="sxs-lookup"><span data-stu-id="1935b-421">The name for the created output.</span></span> <span data-ttu-id="1935b-422">Ad belirtilmemişse, geçerli dizinin adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1935b-422">If no name is specified, the name of the current directory is used.</span></span>

`-o|--output <OUTPUT_DIRECTORY>`

<span data-ttu-id="1935b-423">Oluşturulan çıkışın yerleştirileceği konum.</span><span class="sxs-lookup"><span data-stu-id="1935b-423">Location to place the generated output.</span></span> <span data-ttu-id="1935b-424">Geçerli dizin varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="1935b-424">The default is the current directory.</span></span>

`--type`

<span data-ttu-id="1935b-425">Şablonları kullanılabilir türlerine göre filtreler.</span><span class="sxs-lookup"><span data-stu-id="1935b-425">Filters templates based on available types.</span></span> <span data-ttu-id="1935b-426">Önceden tanımlanmış değerler şunlardır "proje", "öğe" veya "diğer".</span><span class="sxs-lookup"><span data-stu-id="1935b-426">Predefined values are "project", "item" or "other".</span></span>

`-u|--uninstall <PATH|NUGET_ID>`

<span data-ttu-id="1935b-427">`PATH` Veya`NUGET_ID` belirtilen bir kaynak veya şablon paketini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1935b-427">Uninstalls a source or template pack at the `PATH` or `NUGET_ID` provided.</span></span>

> [!NOTE]
> <span data-ttu-id="1935b-428">Bir kaynağı `PATH`kullanarak bir şablonu kaldırmak için yolu tam olarak nitelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1935b-428">To uninstall a template using a source `PATH`, you need to fully qualify the path.</span></span> <span data-ttu-id="1935b-429">Örneğin, *C:/kullanıcıları/\<Kullanıcı >/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* çalışır, ancak içeren klasörden *./GarciaSoftware.ConsoleTemplate.CSharp* olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="1935b-429">For example, *C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* will work, but *./GarciaSoftware.ConsoleTemplate.CSharp* from the containing folder will not.</span></span> <span data-ttu-id="1935b-430">Ayrıca, şablon yolunuza son Sonlandırıcı Dizin eğik çizgi eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="1935b-430">Additionally, do not include a final terminating directory slash on your template path.</span></span>
> 
> <span data-ttu-id="1935b-431">Bir şablonu kaldırmak için gereken `PATH` veya `NUGET_ID` bağımsız değişkeni belirleyemıyorsanız, bağımsız değişken olmadan çalıştırıldığında `dotnet new --uninstall` , tüm yüklü şablonlar ve bunları kaldırmak için gereken bağımsız değişken listelenir.</span><span class="sxs-lookup"><span data-stu-id="1935b-431">If you are unable to determine the `PATH` or `NUGET_ID` argument needed to uninstall a template, running `dotnet new --uninstall` without an argument will list all installed templates and the argument required to uninstall them.</span></span>

# <a name="net-core-1xtabnetcore1x"></a>[<span data-ttu-id="1935b-432">.NET Core 1. x</span><span class="sxs-lookup"><span data-stu-id="1935b-432">.NET Core 1.x</span></span>](#tab/netcore1x)

`-all|--show-all`

<span data-ttu-id="1935b-433">Yalnızca `dotnet new` komutun bağlamında çalışırken belirli bir proje türü için tüm şablonları gösterir.</span><span class="sxs-lookup"><span data-stu-id="1935b-433">Shows all templates for a specific type of project when running in the context of the `dotnet new` command alone.</span></span> <span data-ttu-id="1935b-434">Gibi belirli bir şablon `dotnet new web -all`bağlamında çalıştırılırken, `-all` zorla oluşturma bayrağı olarak yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="1935b-434">When running in the context of a specific template, such as `dotnet new web -all`, `-all` is interpreted as a force creation flag.</span></span> <span data-ttu-id="1935b-435">Çıkış dizini zaten bir proje içerdiğinde bu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-435">This is required when the output directory already contains a project.</span></span>

`-h|--help`

<span data-ttu-id="1935b-436">Komut için yardım yazdırır.</span><span class="sxs-lookup"><span data-stu-id="1935b-436">Prints out help for the command.</span></span> <span data-ttu-id="1935b-437">`dotnet new` Komutun kendisi veya gibi herhangi bir şablon `dotnet new mvc --help`için çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-437">It can be invoked for the `dotnet new` command itself or for any template, such as `dotnet new mvc --help`.</span></span>

`-l|--list`

<span data-ttu-id="1935b-438">Belirtilen adı içeren şablonları listeler.</span><span class="sxs-lookup"><span data-stu-id="1935b-438">Lists templates containing the specified name.</span></span> <span data-ttu-id="1935b-439">`dotnet new` Komut için çağrılırsa, belirtilen dizin için kullanılabilir olabilecek şablonları listeler.</span><span class="sxs-lookup"><span data-stu-id="1935b-439">If invoked for the `dotnet new` command, it lists the possible templates available for the given directory.</span></span> <span data-ttu-id="1935b-440">Örneğin, dizin zaten bir proje içeriyorsa, tüm proje şablonlarını listeetmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-440">For example if the directory already contains a project, it doesn't list all project templates.</span></span>

`-lang|--language {C#|F#}`

<span data-ttu-id="1935b-441">Oluşturulacak şablonun dili.</span><span class="sxs-lookup"><span data-stu-id="1935b-441">The language of the template to create.</span></span> <span data-ttu-id="1935b-442">Kabul edilen dil şablona göre değişir (bkz. [arguments](#arguments) bölümünde Varsayılanlar).</span><span class="sxs-lookup"><span data-stu-id="1935b-442">The language accepted varies by the template (see defaults in the [arguments](#arguments) section).</span></span> <span data-ttu-id="1935b-443">Bazı şablonlar için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="1935b-443">Not valid for some templates.</span></span>

> [!NOTE]
> <span data-ttu-id="1935b-444">Bazı kabuklar `#` özel bir karakter olarak yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="1935b-444">Some shells interpret `#` as a special character.</span></span> <span data-ttu-id="1935b-445">Bu durumlarda, gibi dil parametre değerini `dotnet new console -lang "F#"`almalısınız.</span><span class="sxs-lookup"><span data-stu-id="1935b-445">In those cases, you need to enclose the language parameter value, such as `dotnet new console -lang "F#"`.</span></span>

`-n|--name <OUTPUT_NAME>`

<span data-ttu-id="1935b-446">Oluşturulan çıkışın adı.</span><span class="sxs-lookup"><span data-stu-id="1935b-446">The name for the created output.</span></span> <span data-ttu-id="1935b-447">Ad belirtilmemişse, geçerli dizinin adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1935b-447">If no name is specified, the name of the current directory is used.</span></span>

`-o|--output <OUTPUT_DIRECTORY>`

<span data-ttu-id="1935b-448">Oluşturulan çıkışın yerleştirileceği konum.</span><span class="sxs-lookup"><span data-stu-id="1935b-448">Location to place the generated output.</span></span> <span data-ttu-id="1935b-449">Geçerli dizin varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="1935b-449">The default is the current directory.</span></span>

---

## <a name="template-options"></a><span data-ttu-id="1935b-450">Şablon seçenekleri</span><span class="sxs-lookup"><span data-stu-id="1935b-450">Template options</span></span>

<span data-ttu-id="1935b-451">Her proje şablonunda ek seçenekler bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-451">Each project template may have additional options available.</span></span> <span data-ttu-id="1935b-452">Çekirdek şablonlar aşağıdaki ek seçeneklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="1935b-452">The core templates have the following additional options:</span></span>

# <a name="net-core-22tabnetcore22"></a>[<span data-ttu-id="1935b-453">.NET Core 2,2</span><span class="sxs-lookup"><span data-stu-id="1935b-453">.NET Core 2.2</span></span>](#tab/netcore22)

<span data-ttu-id="1935b-454">**konsola**</span><span class="sxs-lookup"><span data-stu-id="1935b-454">**console**</span></span>

<span data-ttu-id="1935b-455">`--langVersion <VERSION_NUMBER>`-Oluşturulan proje `LangVersion` dosyasındaki özelliği ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-455">`--langVersion <VERSION_NUMBER>` - Sets the `LangVersion` property in the created project file.</span></span> <span data-ttu-id="1935b-456">Örneğin, 7,3 kullanmak `--langVersion 7.3` C# için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-456">For example, use `--langVersion 7.3` to use C# 7.3.</span></span> <span data-ttu-id="1935b-457">İçin F#desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-457">Not supported for F#.</span></span>

<span data-ttu-id="1935b-458">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-458">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-459">**Angular, tepki, reactredux**</span><span class="sxs-lookup"><span data-stu-id="1935b-459">**angular, react, reactredux**</span></span>

<span data-ttu-id="1935b-460">`--exclude-launch-settings`- *Launchsettings. JSON* öğesini oluşturulan şablondan hariç tutun.</span><span class="sxs-lookup"><span data-stu-id="1935b-460">`--exclude-launch-settings` - Exclude *launchSettings.json* from the generated template.</span></span>

<span data-ttu-id="1935b-461">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-461">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-462">`--no-https`-Proje HTTPS gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-462">`--no-https` - Project doesn't require HTTPS.</span></span> <span data-ttu-id="1935b-463">Bu seçenek yalnızca `IndividualAuth` veya `OrganizationalAuth` kullanılmıyorsa geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-463">This option only applies if `IndividualAuth` or `OrganizationalAuth` are not being used.</span></span>

<span data-ttu-id="1935b-464">**razorclasslib**</span><span class="sxs-lookup"><span data-stu-id="1935b-464">**razorclasslib**</span></span>

<span data-ttu-id="1935b-465">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-465">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-466">**projesinin**</span><span class="sxs-lookup"><span data-stu-id="1935b-466">**classlib**</span></span>

<span data-ttu-id="1935b-467">`-f|--framework <FRAMEWORK>`-Hedeflenecek [çerçeveyi](../../standard/frameworks.md) belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-467">`-f|--framework <FRAMEWORK>` - Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1935b-468">Değerler: `netcoreapp2.2` bir .NET Core sınıf kitaplığı oluşturmak veya `netstandard2.0` bir .NET Standard sınıf kitaplığı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1935b-468">Values: `netcoreapp2.2` to create a .NET Core Class Library or `netstandard2.0` to create a .NET Standard Class Library.</span></span> <span data-ttu-id="1935b-469">Varsayılan değer `netstandard2.0` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-469">The default value is `netstandard2.0`.</span></span>

<span data-ttu-id="1935b-470">`--langVersion <VERSION_NUMBER>`-Oluşturulan proje `LangVersion` dosyasındaki özelliği ayarlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-470">`--langVersion <VERSION_NUMBER>` - Sets the `LangVersion` property in the created project file.</span></span> <span data-ttu-id="1935b-471">Örneğin, 7,3 kullanmak `--langVersion 7.3` C# için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-471">For example, use `--langVersion 7.3` to use C# 7.3.</span></span> <span data-ttu-id="1935b-472">İçin F#desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-472">Not supported for F#.</span></span>

<span data-ttu-id="1935b-473">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-473">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-474">**MSTest, xUnit**</span><span class="sxs-lookup"><span data-stu-id="1935b-474">**mstest, xunit**</span></span>

<span data-ttu-id="1935b-475">`-p|--enable-pack`- [DotNet Pack](dotnet-pack.md)kullanarak proje için paketlemeyi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-475">`-p|--enable-pack` - Enables packaging for the project using [dotnet pack](dotnet-pack.md).</span></span>

<span data-ttu-id="1935b-476">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-476">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-477">**NUnit**</span><span class="sxs-lookup"><span data-stu-id="1935b-477">**nunit**</span></span>

<span data-ttu-id="1935b-478">`-f|--framework <FRAMEWORK>`-Hedeflenecek [çerçeveyi](../../standard/frameworks.md) belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-478">`-f|--framework <FRAMEWORK>` - Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1935b-479">Varsayılan değer `netcoreapp2.1` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-479">The default value is `netcoreapp2.1`.</span></span>

<span data-ttu-id="1935b-480">`-p|--enable-pack`- [DotNet Pack](dotnet-pack.md)kullanarak proje için paketlemeyi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-480">`-p|--enable-pack` - Enables packaging for the project using [dotnet pack](dotnet-pack.md).</span></span>

<span data-ttu-id="1935b-481">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-481">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-482">**sayfasında**</span><span class="sxs-lookup"><span data-stu-id="1935b-482">**page**</span></span>

<span data-ttu-id="1935b-483">`-na|--namespace <NAMESPACE_NAME>`-Oluşturulan kod için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-483">`-na|--namespace <NAMESPACE_NAME>` - Namespace for the generated code.</span></span> <span data-ttu-id="1935b-484">Varsayılan değer `MyApp.Namespace` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-484">The default value is `MyApp.Namespace`.</span></span>

<span data-ttu-id="1935b-485">`-np|--no-pagemodel`-Sayfayı PageModel olmadan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1935b-485">`-np|--no-pagemodel` - Creates the page without a PageModel.</span></span>

<span data-ttu-id="1935b-486">**viewıtems 'lar**</span><span class="sxs-lookup"><span data-stu-id="1935b-486">**viewimports**</span></span>

<span data-ttu-id="1935b-487">`-na|--namespace <NAMESPACE_NAME>`-Oluşturulan kod için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-487">`-na|--namespace <NAMESPACE_NAME>` - Namespace for the generated code.</span></span> <span data-ttu-id="1935b-488">Varsayılan değer `MyApp.Namespace` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-488">The default value is `MyApp.Namespace`.</span></span>

<span data-ttu-id="1935b-489">**Web**</span><span class="sxs-lookup"><span data-stu-id="1935b-489">**web**</span></span>

<span data-ttu-id="1935b-490">`--exclude-launch-settings`- *Launchsettings. JSON* öğesini oluşturulan şablondan hariç tutun.</span><span class="sxs-lookup"><span data-stu-id="1935b-490">`--exclude-launch-settings` - Exclude *launchSettings.json* from the generated template.</span></span>

<span data-ttu-id="1935b-491">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-491">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-492">`--no-https`-Proje HTTPS gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-492">`--no-https` - Project doesn't require HTTPS.</span></span> <span data-ttu-id="1935b-493">Bu seçenek yalnızca `IndividualAuth` veya `OrganizationalAuth` kullanılmıyorsa geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-493">This option only applies if `IndividualAuth` or `OrganizationalAuth` are not being used.</span></span>

<span data-ttu-id="1935b-494">**MVC, WebApp**</span><span class="sxs-lookup"><span data-stu-id="1935b-494">**mvc, webapp**</span></span>

<span data-ttu-id="1935b-495">`-au|--auth <AUTHENTICATION_TYPE>`-Kullanılacak kimlik doğrulaması türü.</span><span class="sxs-lookup"><span data-stu-id="1935b-495">`-au|--auth <AUTHENTICATION_TYPE>` - The type of authentication to use.</span></span> <span data-ttu-id="1935b-496">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1935b-496">The possible values are:</span></span>

- <span data-ttu-id="1935b-497">`None`-Kimlik doğrulaması yok (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="1935b-497">`None` - No authentication (Default).</span></span>
- <span data-ttu-id="1935b-498">`Individual`-Bireysel kimlik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="1935b-498">`Individual` - Individual authentication.</span></span>
- <span data-ttu-id="1935b-499">`IndividualB2C`-Azure AD B2C ile bireysel kimlik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="1935b-499">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
- <span data-ttu-id="1935b-500">`SingleOrg`-Tek bir kiracı için kuruluş kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-500">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
- <span data-ttu-id="1935b-501">`MultiOrg`-Birden çok kiracı için kuruluş kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-501">`MultiOrg` - Organizational authentication for multiple tenants.</span></span>
- <span data-ttu-id="1935b-502">`Windows`-Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-502">`Windows` - Windows authentication.</span></span>

<span data-ttu-id="1935b-503">`--aad-b2c-instance <INSTANCE>`-Bağlanılacak Azure Active Directory B2C örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-503">`--aad-b2c-instance <INSTANCE>` - The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="1935b-504">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-504">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-505">Varsayılan değer `https://login.microsoftonline.com/tfp/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-505">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

<span data-ttu-id="1935b-506">`-ssp|--susi-policy-id <ID>`-Bu proje için oturum açma ve kaydolma ilkesi KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-506">`-ssp|--susi-policy-id <ID>` - The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="1935b-507">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-507">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-508">`-rp|--reset-password-policy-id <ID>`-Bu proje için parola sıfırlama ilkesi KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-508">`-rp|--reset-password-policy-id <ID>` - The reset password policy ID for this project.</span></span> <span data-ttu-id="1935b-509">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-509">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-510">`-ep|--edit-profile-policy-id <ID>`-Bu proje için profil ilkesi KIMLIĞINI Düzenle.</span><span class="sxs-lookup"><span data-stu-id="1935b-510">`-ep|--edit-profile-policy-id <ID>` - The edit profile policy ID for this project.</span></span> <span data-ttu-id="1935b-511">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-511">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-512">`--aad-instance <INSTANCE>`-Bağlanılacak Azure Active Directory örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-512">`--aad-instance <INSTANCE>` - The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="1935b-513">`SingleOrg` Veya`MultiOrg` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-513">Use with `SingleOrg` or `MultiOrg` authentication.</span></span> <span data-ttu-id="1935b-514">Varsayılan değer `https://login.microsoftonline.com/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-514">The default value is `https://login.microsoftonline.com/`.</span></span>

<span data-ttu-id="1935b-515">`--client-id <ID>`-Bu projenin Istemci KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-515">`--client-id <ID>` - The Client ID for this project.</span></span> <span data-ttu-id="1935b-516">`IndividualB2C`, Veyakimlik`MultiOrg`doğrulamasıylakullanın. `SingleOrg`</span><span class="sxs-lookup"><span data-stu-id="1935b-516">Use with `IndividualB2C`, `SingleOrg`, or `MultiOrg` authentication.</span></span> <span data-ttu-id="1935b-517">Varsayılan değer `11111111-1111-1111-11111111111111111` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-517">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

<span data-ttu-id="1935b-518">`--domain <DOMAIN>`-Dizin kiracının etki alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-518">`--domain <DOMAIN>` - The domain for the directory tenant.</span></span> <span data-ttu-id="1935b-519">`SingleOrg` Veya`IndividualB2C` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-519">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-520">Varsayılan değer `qualified.domain.name` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-520">The default value is `qualified.domain.name`.</span></span>

<span data-ttu-id="1935b-521">`--tenant-id <ID>`-Bağlanılacak dizinin Tenantıd KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-521">`--tenant-id <ID>` - The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="1935b-522">`SingleOrg` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-522">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-523">Varsayılan değer `22222222-2222-2222-2222-222222222222` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-523">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

<span data-ttu-id="1935b-524">`--callback-path <PATH>`-Uygulamanın yeniden yönlendirme URI 'sinin temel yolu içindeki istek yolu.</span><span class="sxs-lookup"><span data-stu-id="1935b-524">`--callback-path <PATH>` - The request path within the application's base path of the redirect URI.</span></span> <span data-ttu-id="1935b-525">`SingleOrg` Veya`IndividualB2C` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-525">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-526">Varsayılan değer `/signin-oidc` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-526">The default value is `/signin-oidc`.</span></span>

<span data-ttu-id="1935b-527">`-r|--org-read-access`-Bu uygulamanın dizine okuma erişimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-527">`-r|--org-read-access` - Allows this application read-access to the directory.</span></span> <span data-ttu-id="1935b-528">Yalnızca veya `SingleOrg` `MultiOrg` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-528">Only applies to `SingleOrg` or `MultiOrg` authentication.</span></span>

<span data-ttu-id="1935b-529">`--exclude-launch-settings`- *Launchsettings. JSON* öğesini oluşturulan şablondan hariç tutun.</span><span class="sxs-lookup"><span data-stu-id="1935b-529">`--exclude-launch-settings` - Exclude *launchSettings.json* from the generated template.</span></span>

<span data-ttu-id="1935b-530">`--no-https`-Proje HTTPS gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-530">`--no-https` - Project doesn't require HTTPS.</span></span> <span data-ttu-id="1935b-531">`app.UseHsts`ve `app.UseHttpsRedirection` öğesine`Startup.Configure`eklenmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-531">`app.UseHsts` and `app.UseHttpsRedirection` aren't added to `Startup.Configure`.</span></span> <span data-ttu-id="1935b-532">Bu `Individual`seçenek yalnızca `IndividualB2C` `MultiOrg` , ,,veyakullanılmıyorsageçerlidir.`SingleOrg`</span><span class="sxs-lookup"><span data-stu-id="1935b-532">This option only applies if `Individual`, `IndividualB2C`, `SingleOrg`, or `MultiOrg` aren't being used.</span></span>

<span data-ttu-id="1935b-533">`-uld|--use-local-db`-SQLite yerine LocalDB kullanılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-533">`-uld|--use-local-db` - Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="1935b-534">Yalnızca veya `Individual` `IndividualB2C` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-534">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-535">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-535">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-536">**WebApi**</span><span class="sxs-lookup"><span data-stu-id="1935b-536">**webapi**</span></span>

<span data-ttu-id="1935b-537">`-au|--auth <AUTHENTICATION_TYPE>`-Kullanılacak kimlik doğrulaması türü.</span><span class="sxs-lookup"><span data-stu-id="1935b-537">`-au|--auth <AUTHENTICATION_TYPE>` - The type of authentication to use.</span></span> <span data-ttu-id="1935b-538">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1935b-538">The possible values are:</span></span>

- <span data-ttu-id="1935b-539">`None`-Kimlik doğrulaması yok (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="1935b-539">`None` - No authentication (Default).</span></span>
- <span data-ttu-id="1935b-540">`IndividualB2C`-Azure AD B2C ile bireysel kimlik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="1935b-540">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
- <span data-ttu-id="1935b-541">`SingleOrg`-Tek bir kiracı için kuruluş kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-541">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
- <span data-ttu-id="1935b-542">`Windows`-Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-542">`Windows` - Windows authentication.</span></span>

<span data-ttu-id="1935b-543">`--aad-b2c-instance <INSTANCE>`-Bağlanılacak Azure Active Directory B2C örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-543">`--aad-b2c-instance <INSTANCE>` - The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="1935b-544">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-544">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-545">Varsayılan değer `https://login.microsoftonline.com/tfp/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-545">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

<span data-ttu-id="1935b-546">`-ssp|--susi-policy-id <ID>`-Bu proje için oturum açma ve kaydolma ilkesi KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-546">`-ssp|--susi-policy-id <ID>` - The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="1935b-547">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-547">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-548">`--aad-instance <INSTANCE>`-Bağlanılacak Azure Active Directory örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-548">`--aad-instance <INSTANCE>` - The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="1935b-549">`SingleOrg` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-549">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-550">Varsayılan değer `https://login.microsoftonline.com/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-550">The default value is `https://login.microsoftonline.com/`.</span></span>

<span data-ttu-id="1935b-551">`--client-id <ID>`-Bu projenin Istemci KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-551">`--client-id <ID>` - The Client ID for this project.</span></span> <span data-ttu-id="1935b-552">`IndividualB2C` Veya`SingleOrg` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-552">Use with `IndividualB2C` or `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-553">Varsayılan değer `11111111-1111-1111-11111111111111111` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-553">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

<span data-ttu-id="1935b-554">`--domain <DOMAIN>`-Dizin kiracının etki alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-554">`--domain <DOMAIN>` - The domain for the directory tenant.</span></span> <span data-ttu-id="1935b-555">`SingleOrg` Veya`IndividualB2C` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-555">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-556">Varsayılan değer `qualified.domain.name` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-556">The default value is `qualified.domain.name`.</span></span>

<span data-ttu-id="1935b-557">`--tenant-id <ID>`-Bağlanılacak dizinin Tenantıd KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-557">`--tenant-id <ID>` - The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="1935b-558">`SingleOrg` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-558">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-559">Varsayılan değer `22222222-2222-2222-2222-222222222222` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-559">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

<span data-ttu-id="1935b-560">`-r|--org-read-access`-Bu uygulamanın dizine okuma erişimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-560">`-r|--org-read-access` - Allows this application read-access to the directory.</span></span> <span data-ttu-id="1935b-561">Yalnızca veya `SingleOrg` `MultiOrg` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-561">Only applies to `SingleOrg` or `MultiOrg` authentication.</span></span>

<span data-ttu-id="1935b-562">`--exclude-launch-settings`- *Launchsettings. JSON* öğesini oluşturulan şablondan hariç tutun.</span><span class="sxs-lookup"><span data-stu-id="1935b-562">`--exclude-launch-settings` - Exclude *launchSettings.json* from the generated template.</span></span>

<span data-ttu-id="1935b-563">`--no-https`-Proje HTTPS gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-563">`--no-https` - Project doesn't require HTTPS.</span></span> <span data-ttu-id="1935b-564">`app.UseHsts`ve `app.UseHttpsRedirection` öğesine`Startup.Configure`eklenmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-564">`app.UseHsts` and `app.UseHttpsRedirection` aren't added to `Startup.Configure`.</span></span> <span data-ttu-id="1935b-565">Bu `Individual`seçenek yalnızca `IndividualB2C` `MultiOrg` , ,,veyakullanılmıyorsageçerlidir.`SingleOrg`</span><span class="sxs-lookup"><span data-stu-id="1935b-565">This option only applies if `Individual`, `IndividualB2C`, `SingleOrg`, or `MultiOrg` aren't being used.</span></span>

<span data-ttu-id="1935b-566">`-uld|--use-local-db`-SQLite yerine LocalDB kullanılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-566">`-uld|--use-local-db` - Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="1935b-567">Yalnızca veya `Individual` `IndividualB2C` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-567">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-568">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-568">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-569">**globaljson**</span><span class="sxs-lookup"><span data-stu-id="1935b-569">**globaljson**</span></span>

<span data-ttu-id="1935b-570">`--sdk-version <VERSION_NUMBER>`- *Global. JSON* dosyasında kullanılacak .NET Core SDK sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-570">`--sdk-version <VERSION_NUMBER>` - Specifies the version of the .NET Core SDK to use in the *global.json* file.</span></span>

# <a name="net-core-21tabnetcore21"></a>[<span data-ttu-id="1935b-571">.NET Core 2,1</span><span class="sxs-lookup"><span data-stu-id="1935b-571">.NET Core 2.1</span></span>](#tab/netcore21)

<span data-ttu-id="1935b-572">**konsol, angular, tepki, reactredux, razorclasslib**</span><span class="sxs-lookup"><span data-stu-id="1935b-572">**console, angular, react, reactredux, razorclasslib**</span></span>

<span data-ttu-id="1935b-573">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-573">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-574">**projesinin**</span><span class="sxs-lookup"><span data-stu-id="1935b-574">**classlib**</span></span>

<span data-ttu-id="1935b-575">`-f|--framework <FRAMEWORK>`-Hedeflenecek [çerçeveyi](../../standard/frameworks.md) belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-575">`-f|--framework <FRAMEWORK>` - Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1935b-576">Değerler: `netcoreapp2.1` bir .NET Core sınıf kitaplığı oluşturmak veya `netstandard2.0` bir .NET Standard sınıf kitaplığı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1935b-576">Values: `netcoreapp2.1` to create a .NET Core Class Library or `netstandard2.0` to create a .NET Standard Class Library.</span></span> <span data-ttu-id="1935b-577">Varsayılan değer `netstandard2.0` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-577">The default value is `netstandard2.0`.</span></span>

<span data-ttu-id="1935b-578">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-578">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-579">**MSTest, xUnit**</span><span class="sxs-lookup"><span data-stu-id="1935b-579">**mstest, xunit**</span></span>

<span data-ttu-id="1935b-580">`-p|--enable-pack`- [DotNet Pack](dotnet-pack.md)kullanarak proje için paketlemeyi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-580">`-p|--enable-pack` - Enables packaging for the project using [dotnet pack](dotnet-pack.md).</span></span>

<span data-ttu-id="1935b-581">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-581">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-582">**globaljson**</span><span class="sxs-lookup"><span data-stu-id="1935b-582">**globaljson**</span></span>

<span data-ttu-id="1935b-583">`--sdk-version <VERSION_NUMBER>`- *Global. JSON* dosyasında kullanılacak .NET Core SDK sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-583">`--sdk-version <VERSION_NUMBER>` - Specifies the version of the .NET Core SDK to use in the *global.json* file.</span></span>

<span data-ttu-id="1935b-584">**Web**</span><span class="sxs-lookup"><span data-stu-id="1935b-584">**web**</span></span>

<span data-ttu-id="1935b-585">`--exclude-launch-settings`- *Launchsettings. JSON* öğesini oluşturulan şablondan hariç tutun.</span><span class="sxs-lookup"><span data-stu-id="1935b-585">`--exclude-launch-settings` - Exclude *launchSettings.json* from the generated template.</span></span>

<span data-ttu-id="1935b-586">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-586">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-587">`--no-https`-Proje HTTPS gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-587">`--no-https` - Project doesn't require HTTPS.</span></span> <span data-ttu-id="1935b-588">Bu seçenek yalnızca `IndividualAuth` veya `OrganizationalAuth` kullanılmıyorsa geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-588">This option only applies if `IndividualAuth` or `OrganizationalAuth` are not being used.</span></span>

<span data-ttu-id="1935b-589">**WebApi**</span><span class="sxs-lookup"><span data-stu-id="1935b-589">**webapi**</span></span>

<span data-ttu-id="1935b-590">`-au|--auth <AUTHENTICATION_TYPE>`-Kullanılacak kimlik doğrulaması türü.</span><span class="sxs-lookup"><span data-stu-id="1935b-590">`-au|--auth <AUTHENTICATION_TYPE>` - The type of authentication to use.</span></span> <span data-ttu-id="1935b-591">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1935b-591">The possible values are:</span></span>

- <span data-ttu-id="1935b-592">`None`-Kimlik doğrulaması yok (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="1935b-592">`None` - No authentication (Default).</span></span>
- <span data-ttu-id="1935b-593">`IndividualB2C`-Azure AD B2C ile bireysel kimlik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="1935b-593">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
- <span data-ttu-id="1935b-594">`SingleOrg`-Tek bir kiracı için kuruluş kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-594">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
- <span data-ttu-id="1935b-595">`Windows`-Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-595">`Windows` - Windows authentication.</span></span>

<span data-ttu-id="1935b-596">`--aad-b2c-instance <INSTANCE>`-Bağlanılacak Azure Active Directory B2C örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-596">`--aad-b2c-instance <INSTANCE>` - The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="1935b-597">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-597">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-598">Varsayılan değer `https://login.microsoftonline.com/tfp/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-598">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

<span data-ttu-id="1935b-599">`-ssp|--susi-policy-id <ID>`-Bu proje için oturum açma ve kaydolma ilkesi KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-599">`-ssp|--susi-policy-id <ID>` - The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="1935b-600">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-600">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-601">`--aad-instance <INSTANCE>`-Bağlanılacak Azure Active Directory örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-601">`--aad-instance <INSTANCE>` - The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="1935b-602">`SingleOrg` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-602">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-603">Varsayılan değer `https://login.microsoftonline.com/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-603">The default value is `https://login.microsoftonline.com/`.</span></span>

<span data-ttu-id="1935b-604">`--client-id <ID>`-Bu projenin Istemci KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-604">`--client-id <ID>` - The Client ID for this project.</span></span> <span data-ttu-id="1935b-605">`IndividualB2C` Veya`SingleOrg` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-605">Use with `IndividualB2C` or `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-606">Varsayılan değer `11111111-1111-1111-11111111111111111` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-606">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

<span data-ttu-id="1935b-607">`--domain <DOMAIN>`-Dizin kiracının etki alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-607">`--domain <DOMAIN>` - The domain for the directory tenant.</span></span> <span data-ttu-id="1935b-608">`SingleOrg` Veya`IndividualB2C` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-608">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-609">Varsayılan değer `qualified.domain.name` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-609">The default value is `qualified.domain.name`.</span></span>

<span data-ttu-id="1935b-610">`--tenant-id <ID>`-Bağlanılacak dizinin Tenantıd KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-610">`--tenant-id <ID>` - The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="1935b-611">`SingleOrg` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-611">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-612">Varsayılan değer `22222222-2222-2222-2222-222222222222` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-612">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

<span data-ttu-id="1935b-613">`-r|--org-read-access`-Bu uygulamanın dizine okuma erişimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-613">`-r|--org-read-access` - Allows this application read-access to the directory.</span></span> <span data-ttu-id="1935b-614">Yalnızca veya `SingleOrg` `MultiOrg` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-614">Only applies to `SingleOrg` or `MultiOrg` authentication.</span></span>

<span data-ttu-id="1935b-615">`--exclude-launch-settings`- *Launchsettings. JSON* öğesini oluşturulan şablondan hariç tutun.</span><span class="sxs-lookup"><span data-stu-id="1935b-615">`--exclude-launch-settings` - Exclude *launchSettings.json* from the generated template.</span></span>

<span data-ttu-id="1935b-616">`-uld|--use-local-db`-SQLite yerine LocalDB kullanılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-616">`-uld|--use-local-db` - Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="1935b-617">Yalnızca veya `Individual` `IndividualB2C` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-617">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-618">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-618">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-619">`--no-https`-Proje HTTPS gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-619">`--no-https` - Project doesn't require HTTPS.</span></span> <span data-ttu-id="1935b-620">`app.UseHsts`ve `app.UseHttpsRedirection` öğesine`Startup.Configure`eklenmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-620">`app.UseHsts` and `app.UseHttpsRedirection` aren't added to `Startup.Configure`.</span></span> <span data-ttu-id="1935b-621">Bu `Individual`seçenek yalnızca `IndividualB2C` `MultiOrg` , ,,veyakullanılmıyorsageçerlidir.`SingleOrg`</span><span class="sxs-lookup"><span data-stu-id="1935b-621">This option only applies if `Individual`, `IndividualB2C`, `SingleOrg`, or `MultiOrg` aren't being used.</span></span>

<span data-ttu-id="1935b-622">**MVC, Razor**</span><span class="sxs-lookup"><span data-stu-id="1935b-622">**mvc, razor**</span></span>

<span data-ttu-id="1935b-623">`-au|--auth <AUTHENTICATION_TYPE>`-Kullanılacak kimlik doğrulaması türü.</span><span class="sxs-lookup"><span data-stu-id="1935b-623">`-au|--auth <AUTHENTICATION_TYPE>` - The type of authentication to use.</span></span> <span data-ttu-id="1935b-624">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1935b-624">The possible values are:</span></span>

- <span data-ttu-id="1935b-625">`None`-Kimlik doğrulaması yok (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="1935b-625">`None` - No authentication (Default).</span></span>
- <span data-ttu-id="1935b-626">`Individual`-Bireysel kimlik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="1935b-626">`Individual` - Individual authentication.</span></span>
- <span data-ttu-id="1935b-627">`IndividualB2C`-Azure AD B2C ile bireysel kimlik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="1935b-627">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
- <span data-ttu-id="1935b-628">`SingleOrg`-Tek bir kiracı için kuruluş kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-628">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
- <span data-ttu-id="1935b-629">`MultiOrg`-Birden çok kiracı için kuruluş kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-629">`MultiOrg` - Organizational authentication for multiple tenants.</span></span>
- <span data-ttu-id="1935b-630">`Windows`-Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-630">`Windows` - Windows authentication.</span></span>

<span data-ttu-id="1935b-631">`--aad-b2c-instance <INSTANCE>`-Bağlanılacak Azure Active Directory B2C örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-631">`--aad-b2c-instance <INSTANCE>` - The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="1935b-632">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-632">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-633">Varsayılan değer `https://login.microsoftonline.com/tfp/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-633">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

<span data-ttu-id="1935b-634">`-ssp|--susi-policy-id <ID>`-Bu proje için oturum açma ve kaydolma ilkesi KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-634">`-ssp|--susi-policy-id <ID>` - The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="1935b-635">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-635">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-636">`-rp|--reset-password-policy-id <ID>`-Bu proje için parola sıfırlama ilkesi KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-636">`-rp|--reset-password-policy-id <ID>` - The reset password policy ID for this project.</span></span> <span data-ttu-id="1935b-637">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-637">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-638">`-ep|--edit-profile-policy-id <ID>`-Bu proje için profil ilkesi KIMLIĞINI Düzenle.</span><span class="sxs-lookup"><span data-stu-id="1935b-638">`-ep|--edit-profile-policy-id <ID>` - The edit profile policy ID for this project.</span></span> <span data-ttu-id="1935b-639">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-639">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-640">`--aad-instance <INSTANCE>`-Bağlanılacak Azure Active Directory örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-640">`--aad-instance <INSTANCE>` - The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="1935b-641">`SingleOrg` Veya`MultiOrg` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-641">Use with `SingleOrg` or `MultiOrg` authentication.</span></span> <span data-ttu-id="1935b-642">Varsayılan değer `https://login.microsoftonline.com/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-642">The default value is `https://login.microsoftonline.com/`.</span></span>

<span data-ttu-id="1935b-643">`--client-id <ID>`-Bu projenin Istemci KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-643">`--client-id <ID>` - The Client ID for this project.</span></span> <span data-ttu-id="1935b-644">`IndividualB2C`, Veyakimlik`MultiOrg`doğrulamasıylakullanın. `SingleOrg`</span><span class="sxs-lookup"><span data-stu-id="1935b-644">Use with `IndividualB2C`, `SingleOrg`, or `MultiOrg` authentication.</span></span> <span data-ttu-id="1935b-645">Varsayılan değer `11111111-1111-1111-11111111111111111` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-645">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

<span data-ttu-id="1935b-646">`--domain <DOMAIN>`-Dizin kiracının etki alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-646">`--domain <DOMAIN>` - The domain for the directory tenant.</span></span> <span data-ttu-id="1935b-647">`SingleOrg` Veya`IndividualB2C` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-647">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-648">Varsayılan değer `qualified.domain.name` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-648">The default value is `qualified.domain.name`.</span></span>

<span data-ttu-id="1935b-649">`--tenant-id <ID>`-Bağlanılacak dizinin Tenantıd KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-649">`--tenant-id <ID>` - The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="1935b-650">`SingleOrg` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-650">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-651">Varsayılan değer `22222222-2222-2222-2222-222222222222` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-651">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

<span data-ttu-id="1935b-652">`--callback-path <PATH>`-Uygulamanın yeniden yönlendirme URI 'sinin temel yolu içindeki istek yolu.</span><span class="sxs-lookup"><span data-stu-id="1935b-652">`--callback-path <PATH>` - The request path within the application's base path of the redirect URI.</span></span> <span data-ttu-id="1935b-653">`SingleOrg` Veya`IndividualB2C` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-653">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-654">Varsayılan değer `/signin-oidc` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-654">The default value is `/signin-oidc`.</span></span>

<span data-ttu-id="1935b-655">`-r|--org-read-access`-Bu uygulamanın dizine okuma erişimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-655">`-r|--org-read-access` - Allows this application read-access to the directory.</span></span> <span data-ttu-id="1935b-656">Yalnızca veya `SingleOrg` `MultiOrg` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-656">Only applies to `SingleOrg` or `MultiOrg` authentication.</span></span>

<span data-ttu-id="1935b-657">`--exclude-launch-settings`- *Launchsettings. JSON* öğesini oluşturulan şablondan hariç tutun.</span><span class="sxs-lookup"><span data-stu-id="1935b-657">`--exclude-launch-settings` - Exclude *launchSettings.json* from the generated template.</span></span>

<span data-ttu-id="1935b-658">`--use-browserlink`-Projedeki BrowserLink öğesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1935b-658">`--use-browserlink` - Includes BrowserLink in the project.</span></span>

<span data-ttu-id="1935b-659">`-uld|--use-local-db`-SQLite yerine LocalDB kullanılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-659">`-uld|--use-local-db` - Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="1935b-660">Yalnızca veya `Individual` `IndividualB2C` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-660">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-661">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-661">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-662">`--no-https`-Proje HTTPS gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-662">`--no-https` - Project doesn't require HTTPS.</span></span> <span data-ttu-id="1935b-663">`app.UseHsts`ve `app.UseHttpsRedirection` öğesine`Startup.Configure`eklenmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-663">`app.UseHsts` and `app.UseHttpsRedirection` aren't added to `Startup.Configure`.</span></span> <span data-ttu-id="1935b-664">Bu `Individual`seçenek yalnızca `IndividualB2C` `MultiOrg` , ,,veyakullanılmıyorsageçerlidir.`SingleOrg`</span><span class="sxs-lookup"><span data-stu-id="1935b-664">This option only applies if `Individual`, `IndividualB2C`, `SingleOrg`, or `MultiOrg` aren't being used.</span></span>

<span data-ttu-id="1935b-665">**sayfasında**</span><span class="sxs-lookup"><span data-stu-id="1935b-665">**page**</span></span>

<span data-ttu-id="1935b-666">`-na|--namespace <NAMESPACE_NAME>`-Oluşturulan kod için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-666">`-na|--namespace <NAMESPACE_NAME>` - Namespace for the generated code.</span></span> <span data-ttu-id="1935b-667">Varsayılan değer `MyApp.Namespace` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-667">The default value is `MyApp.Namespace`.</span></span>

<span data-ttu-id="1935b-668">`-np|--no-pagemodel`-Sayfayı PageModel olmadan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1935b-668">`-np|--no-pagemodel` - Creates the page without a PageModel.</span></span>

<span data-ttu-id="1935b-669">**viewıtems 'lar**</span><span class="sxs-lookup"><span data-stu-id="1935b-669">**viewimports**</span></span>

<span data-ttu-id="1935b-670">`-na|--namespace <NAMESPACE_NAME>`-Oluşturulan kod için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-670">`-na|--namespace <NAMESPACE_NAME>` - Namespace for the generated code.</span></span> <span data-ttu-id="1935b-671">Varsayılan değer `MyApp.Namespace` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-671">The default value is `MyApp.Namespace`.</span></span>

# <a name="net-core-20tabnetcore20"></a>[<span data-ttu-id="1935b-672">.NET Core 2,0</span><span class="sxs-lookup"><span data-stu-id="1935b-672">.NET Core 2.0</span></span>](#tab/netcore20)

<span data-ttu-id="1935b-673">**konsol, angular, tepki, reactredux**</span><span class="sxs-lookup"><span data-stu-id="1935b-673">**console, angular, react, reactredux**</span></span>

<span data-ttu-id="1935b-674">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-674">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-675">**projesinin**</span><span class="sxs-lookup"><span data-stu-id="1935b-675">**classlib**</span></span>

<span data-ttu-id="1935b-676">`-f|--framework <FRAMEWORK>`-Hedeflenecek [çerçeveyi](../../standard/frameworks.md) belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-676">`-f|--framework <FRAMEWORK>` - Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1935b-677">Değerler: `netcoreapp2.0` bir .NET Core sınıf kitaplığı oluşturmak veya `netstandard2.0` bir .NET Standard sınıf kitaplığı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1935b-677">Values: `netcoreapp2.0` to create a .NET Core Class Library or `netstandard2.0` to create a .NET Standard Class Library.</span></span> <span data-ttu-id="1935b-678">Varsayılan değer `netstandard2.0` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-678">The default value is `netstandard2.0`.</span></span>

<span data-ttu-id="1935b-679">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-679">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-680">**MSTest, xUnit**</span><span class="sxs-lookup"><span data-stu-id="1935b-680">**mstest, xunit**</span></span>

<span data-ttu-id="1935b-681">`-p|--enable-pack`- [DotNet Pack](dotnet-pack.md)kullanarak proje için paketlemeyi etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1935b-681">`-p|--enable-pack` - Enables packaging for the project using [dotnet pack](dotnet-pack.md).</span></span>

<span data-ttu-id="1935b-682">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-682">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-683">**globaljson**</span><span class="sxs-lookup"><span data-stu-id="1935b-683">**globaljson**</span></span>

<span data-ttu-id="1935b-684">`--sdk-version <VERSION_NUMBER>`- *Global. JSON* dosyasında kullanılacak .NET Core SDK sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-684">`--sdk-version <VERSION_NUMBER>` - Specifies the version of the .NET Core SDK to use in the *global.json* file.</span></span>

<span data-ttu-id="1935b-685">**Web**</span><span class="sxs-lookup"><span data-stu-id="1935b-685">**web**</span></span>

<span data-ttu-id="1935b-686">`--use-launch-settings`-Oluşturulan şablon çıkışında *Launchsettings. JSON* öğesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1935b-686">`--use-launch-settings` - Includes *launchSettings.json* in the generated template output.</span></span>

<span data-ttu-id="1935b-687">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-687">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-688">**WebApi**</span><span class="sxs-lookup"><span data-stu-id="1935b-688">**webapi**</span></span>

<span data-ttu-id="1935b-689">`-au|--auth <AUTHENTICATION_TYPE>`-Kullanılacak kimlik doğrulaması türü.</span><span class="sxs-lookup"><span data-stu-id="1935b-689">`-au|--auth <AUTHENTICATION_TYPE>` - The type of authentication to use.</span></span> <span data-ttu-id="1935b-690">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1935b-690">The possible values are:</span></span>

- <span data-ttu-id="1935b-691">`None`-Kimlik doğrulaması yok (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="1935b-691">`None` - No authentication (Default).</span></span>
- <span data-ttu-id="1935b-692">`IndividualB2C`-Azure AD B2C ile bireysel kimlik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="1935b-692">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
- <span data-ttu-id="1935b-693">`SingleOrg`-Tek bir kiracı için kuruluş kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-693">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
- <span data-ttu-id="1935b-694">`Windows`-Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-694">`Windows` - Windows authentication.</span></span>

<span data-ttu-id="1935b-695">`--aad-b2c-instance <INSTANCE>`-Bağlanılacak Azure Active Directory B2C örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-695">`--aad-b2c-instance <INSTANCE>` - The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="1935b-696">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-696">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-697">Varsayılan değer `https://login.microsoftonline.com/tfp/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-697">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

<span data-ttu-id="1935b-698">`-ssp|--susi-policy-id <ID>`-Bu proje için oturum açma ve kaydolma ilkesi KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-698">`-ssp|--susi-policy-id <ID>` - The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="1935b-699">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-699">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-700">`--aad-instance <INSTANCE>`-Bağlanılacak Azure Active Directory örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-700">`--aad-instance <INSTANCE>` - The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="1935b-701">`SingleOrg` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-701">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-702">Varsayılan değer `https://login.microsoftonline.com/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-702">The default value is `https://login.microsoftonline.com/`.</span></span>

<span data-ttu-id="1935b-703">`--client-id <ID>`-Bu projenin Istemci KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-703">`--client-id <ID>` - The Client ID for this project.</span></span> <span data-ttu-id="1935b-704">`IndividualB2C` Veya`SingleOrg` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-704">Use with `IndividualB2C` or `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-705">Varsayılan değer `11111111-1111-1111-11111111111111111` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-705">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

<span data-ttu-id="1935b-706">`--domain <DOMAIN>`-Dizin kiracının etki alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-706">`--domain <DOMAIN>` - The domain for the directory tenant.</span></span> <span data-ttu-id="1935b-707">`SingleOrg` Veya`IndividualB2C` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-707">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-708">Varsayılan değer `qualified.domain.name` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-708">The default value is `qualified.domain.name`.</span></span>

<span data-ttu-id="1935b-709">`--tenant-id <ID>`-Bağlanılacak dizinin Tenantıd KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-709">`--tenant-id <ID>` - The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="1935b-710">`SingleOrg` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-710">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-711">Varsayılan değer `22222222-2222-2222-2222-222222222222` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-711">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

<span data-ttu-id="1935b-712">`-r|--org-read-access`-Bu uygulamanın dizine okuma erişimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-712">`-r|--org-read-access` - Allows this application read-access to the directory.</span></span> <span data-ttu-id="1935b-713">Yalnızca veya `SingleOrg` `MultiOrg` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-713">Only applies to `SingleOrg` or `MultiOrg` authentication.</span></span>

<span data-ttu-id="1935b-714">`--use-launch-settings`-Oluşturulan şablon çıkışında *Launchsettings. JSON* öğesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1935b-714">`--use-launch-settings` - Includes *launchSettings.json* in the generated template output.</span></span>

<span data-ttu-id="1935b-715">`-uld|--use-local-db`-SQLite yerine LocalDB kullanılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-715">`-uld|--use-local-db` - Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="1935b-716">Yalnızca veya `Individual` `IndividualB2C` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-716">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-717">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-717">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-718">**MVC, Razor**</span><span class="sxs-lookup"><span data-stu-id="1935b-718">**mvc, razor**</span></span>

<span data-ttu-id="1935b-719">`-au|--auth <AUTHENTICATION_TYPE>`-Kullanılacak kimlik doğrulaması türü.</span><span class="sxs-lookup"><span data-stu-id="1935b-719">`-au|--auth <AUTHENTICATION_TYPE>` - The type of authentication to use.</span></span> <span data-ttu-id="1935b-720">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1935b-720">The possible values are:</span></span>

- <span data-ttu-id="1935b-721">`None`-Kimlik doğrulaması yok (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="1935b-721">`None` - No authentication (Default).</span></span>
- <span data-ttu-id="1935b-722">`Individual`-Bireysel kimlik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="1935b-722">`Individual` - Individual authentication.</span></span>
- <span data-ttu-id="1935b-723">`IndividualB2C`-Azure AD B2C ile bireysel kimlik doğrulama.</span><span class="sxs-lookup"><span data-stu-id="1935b-723">`IndividualB2C` - Individual authentication with Azure AD B2C.</span></span>
- <span data-ttu-id="1935b-724">`SingleOrg`-Tek bir kiracı için kuruluş kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-724">`SingleOrg` - Organizational authentication for a single tenant.</span></span>
- <span data-ttu-id="1935b-725">`MultiOrg`-Birden çok kiracı için kuruluş kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-725">`MultiOrg` - Organizational authentication for multiple tenants.</span></span>
- <span data-ttu-id="1935b-726">`Windows`-Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1935b-726">`Windows` - Windows authentication.</span></span>

<span data-ttu-id="1935b-727">`--aad-b2c-instance <INSTANCE>`-Bağlanılacak Azure Active Directory B2C örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-727">`--aad-b2c-instance <INSTANCE>` - The Azure Active Directory B2C instance to connect to.</span></span> <span data-ttu-id="1935b-728">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-728">Use with `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-729">Varsayılan değer `https://login.microsoftonline.com/tfp/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-729">The default value is `https://login.microsoftonline.com/tfp/`.</span></span>

<span data-ttu-id="1935b-730">`-ssp|--susi-policy-id <ID>`-Bu proje için oturum açma ve kaydolma ilkesi KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-730">`-ssp|--susi-policy-id <ID>` - The sign-in and sign-up policy ID for this project.</span></span> <span data-ttu-id="1935b-731">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-731">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-732">`-rp|--reset-password-policy-id <ID>`-Bu proje için parola sıfırlama ilkesi KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-732">`-rp|--reset-password-policy-id <ID>` - The reset password policy ID for this project.</span></span> <span data-ttu-id="1935b-733">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-733">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-734">`-ep|--edit-profile-policy-id <ID>`-Bu proje için profil ilkesi KIMLIĞINI Düzenle.</span><span class="sxs-lookup"><span data-stu-id="1935b-734">`-ep|--edit-profile-policy-id <ID>` - The edit profile policy ID for this project.</span></span> <span data-ttu-id="1935b-735">`IndividualB2C` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-735">Use with `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-736">`--aad-instance <INSTANCE>`-Bağlanılacak Azure Active Directory örneği.</span><span class="sxs-lookup"><span data-stu-id="1935b-736">`--aad-instance <INSTANCE>` - The Azure Active Directory instance to connect to.</span></span> <span data-ttu-id="1935b-737">`SingleOrg` Veya`MultiOrg` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-737">Use with `SingleOrg` or `MultiOrg` authentication.</span></span> <span data-ttu-id="1935b-738">Varsayılan değer `https://login.microsoftonline.com/` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-738">The default value is `https://login.microsoftonline.com/`.</span></span>

<span data-ttu-id="1935b-739">`--client-id <ID>`-Bu projenin Istemci KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-739">`--client-id <ID>` - The Client ID for this project.</span></span> <span data-ttu-id="1935b-740">`IndividualB2C`, Veyakimlik`MultiOrg`doğrulamasıylakullanın. `SingleOrg`</span><span class="sxs-lookup"><span data-stu-id="1935b-740">Use with `IndividualB2C`, `SingleOrg`, or `MultiOrg` authentication.</span></span> <span data-ttu-id="1935b-741">Varsayılan değer `11111111-1111-1111-11111111111111111` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-741">The default value is `11111111-1111-1111-11111111111111111`.</span></span>

<span data-ttu-id="1935b-742">`--domain <DOMAIN>`-Dizin kiracının etki alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-742">`--domain <DOMAIN>` - The domain for the directory tenant.</span></span> <span data-ttu-id="1935b-743">`SingleOrg` Veya`IndividualB2C` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-743">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-744">Varsayılan değer `qualified.domain.name` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-744">The default value is `qualified.domain.name`.</span></span>

<span data-ttu-id="1935b-745">`--tenant-id <ID>`-Bağlanılacak dizinin Tenantıd KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1935b-745">`--tenant-id <ID>` - The TenantId ID of the directory to connect to.</span></span> <span data-ttu-id="1935b-746">`SingleOrg` Kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-746">Use with `SingleOrg` authentication.</span></span> <span data-ttu-id="1935b-747">Varsayılan değer `22222222-2222-2222-2222-222222222222` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-747">The default value is `22222222-2222-2222-2222-222222222222`.</span></span>

<span data-ttu-id="1935b-748">`--callback-path <PATH>`-Uygulamanın yeniden yönlendirme URI 'sinin temel yolu içindeki istek yolu.</span><span class="sxs-lookup"><span data-stu-id="1935b-748">`--callback-path <PATH>` - The request path within the application's base path of the redirect URI.</span></span> <span data-ttu-id="1935b-749">`SingleOrg` Veya`IndividualB2C` kimlik doğrulamasıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="1935b-749">Use with `SingleOrg` or `IndividualB2C` authentication.</span></span> <span data-ttu-id="1935b-750">Varsayılan değer `/signin-oidc` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-750">The default value is `/signin-oidc`.</span></span>

<span data-ttu-id="1935b-751">`-r|--org-read-access`-Bu uygulamanın dizine okuma erişimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1935b-751">`-r|--org-read-access` - Allows this application read-access to the directory.</span></span> <span data-ttu-id="1935b-752">Yalnızca veya `SingleOrg` `MultiOrg` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-752">Only applies to `SingleOrg` or `MultiOrg` authentication.</span></span>

<span data-ttu-id="1935b-753">`--use-launch-settings`-Oluşturulan şablon çıkışında *Launchsettings. JSON* öğesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1935b-753">`--use-launch-settings` - Includes *launchSettings.json* in the generated template output.</span></span>

<span data-ttu-id="1935b-754">`--use-browserlink`-Projedeki BrowserLink öğesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1935b-754">`--use-browserlink` - Includes BrowserLink in the project.</span></span>

<span data-ttu-id="1935b-755">`-uld|--use-local-db`-SQLite yerine LocalDB kullanılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-755">`-uld|--use-local-db` - Specifies LocalDB should be used instead of SQLite.</span></span> <span data-ttu-id="1935b-756">Yalnızca veya `Individual` `IndividualB2C` kimlik doğrulaması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1935b-756">Only applies to `Individual` or `IndividualB2C` authentication.</span></span>

<span data-ttu-id="1935b-757">`--no-restore`-Proje oluşturma sırasında örtük geri yükleme yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="1935b-757">`--no-restore` - Doesn't execute an implicit restore during project creation.</span></span>

<span data-ttu-id="1935b-758">**sayfasında**</span><span class="sxs-lookup"><span data-stu-id="1935b-758">**page**</span></span>

<span data-ttu-id="1935b-759">`-na|--namespace <NAMESPACE_NAME>`-Oluşturulan kod için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-759">`-na|--namespace <NAMESPACE_NAME>`- Namespace for the generated code.</span></span> <span data-ttu-id="1935b-760">Varsayılan değer `MyApp.Namespace` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-760">The default value is `MyApp.Namespace`.</span></span>

<span data-ttu-id="1935b-761">`-np|--no-pagemodel`-Sayfayı PageModel olmadan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1935b-761">`-np|--no-pagemodel` - Creates the page without a PageModel.</span></span>

<span data-ttu-id="1935b-762">**viewıtems 'lar**</span><span class="sxs-lookup"><span data-stu-id="1935b-762">**viewimports**</span></span>

<span data-ttu-id="1935b-763">`-na|--namespace <NAMESPACE_NAME>`-Oluşturulan kod için ad alanı.</span><span class="sxs-lookup"><span data-stu-id="1935b-763">`-na|--namespace <NAMESPACE_NAME>`- Namespace for the generated code.</span></span> <span data-ttu-id="1935b-764">Varsayılan değer `MyApp.Namespace` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-764">The default value is `MyApp.Namespace`.</span></span>

# <a name="net-core-1xtabnetcore1x"></a>[<span data-ttu-id="1935b-765">.NET Core 1. x</span><span class="sxs-lookup"><span data-stu-id="1935b-765">.NET Core 1.x</span></span>](#tab/netcore1x)

<span data-ttu-id="1935b-766">**konsol, xUnit, MSTest, Web, WebApi**</span><span class="sxs-lookup"><span data-stu-id="1935b-766">**console, xunit, mstest, web, webapi**</span></span>

<span data-ttu-id="1935b-767">`-f|--framework <FRAMEWORK>`-Hedeflenecek [çerçeveyi](../../standard/frameworks.md) belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-767">`-f|--framework <FRAMEWORK>` - Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1935b-768">Değerler: `netcoreapp1.0` veya `netcoreapp1.1`.</span><span class="sxs-lookup"><span data-stu-id="1935b-768">Values: `netcoreapp1.0` or `netcoreapp1.1`.</span></span> <span data-ttu-id="1935b-769">Varsayılan değer `netcoreapp1.0` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-769">The default value is `netcoreapp1.0`.</span></span>

<span data-ttu-id="1935b-770">**projesinin**</span><span class="sxs-lookup"><span data-stu-id="1935b-770">**classlib**</span></span>

<span data-ttu-id="1935b-771">`-f|--framework <FRAMEWORK>`-Hedeflenecek [çerçeveyi](../../standard/frameworks.md) belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-771">`-f|--framework <FRAMEWORK>` - Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1935b-772">Değerler: `netcoreapp1.0`, `netcoreapp1.1`, veya `netstandard1.0` .`netstandard1.6`</span><span class="sxs-lookup"><span data-stu-id="1935b-772">Values: `netcoreapp1.0`, `netcoreapp1.1`, or `netstandard1.0` to `netstandard1.6`.</span></span> <span data-ttu-id="1935b-773">Varsayılan değer `netstandard1.4` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-773">The default value is `netstandard1.4`.</span></span>

<span data-ttu-id="1935b-774">**mvc**</span><span class="sxs-lookup"><span data-stu-id="1935b-774">**mvc**</span></span>

<span data-ttu-id="1935b-775">`-f|--framework <FRAMEWORK>`-Hedeflenecek [çerçeveyi](../../standard/frameworks.md) belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-775">`-f|--framework <FRAMEWORK>` - Specifies the [framework](../../standard/frameworks.md) to target.</span></span> <span data-ttu-id="1935b-776">Değerler: `netcoreapp1.0` veya `netcoreapp1.1`.</span><span class="sxs-lookup"><span data-stu-id="1935b-776">Values: `netcoreapp1.0` or `netcoreapp1.1`.</span></span> <span data-ttu-id="1935b-777">Varsayılan değer `netcoreapp1.0` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-777">The default value is `netcoreapp1.0`.</span></span>

<span data-ttu-id="1935b-778">`-au|--auth <AUTHENTICATION_TYPE>`-Kullanılacak kimlik doğrulaması türü.</span><span class="sxs-lookup"><span data-stu-id="1935b-778">`-au|--auth <AUTHENTICATION_TYPE>` - The type of authentication to use.</span></span> <span data-ttu-id="1935b-779">Değerler: `None` veya `Individual`.</span><span class="sxs-lookup"><span data-stu-id="1935b-779">Values: `None` or `Individual`.</span></span> <span data-ttu-id="1935b-780">Varsayılan değer `None` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-780">The default value is `None`.</span></span>

<span data-ttu-id="1935b-781">`-uld|--use-local-db`-SQLite yerine LocalDB kullanılıp kullanılmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1935b-781">`-uld|--use-local-db` - Specifies whether or not to use LocalDB instead of SQLite.</span></span> <span data-ttu-id="1935b-782">Değerler: `true` veya `false`.</span><span class="sxs-lookup"><span data-stu-id="1935b-782">Values: `true` or `false`.</span></span> <span data-ttu-id="1935b-783">Varsayılan değer `false` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="1935b-783">The default value is `false`.</span></span>

---

## <a name="examples"></a><span data-ttu-id="1935b-784">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1935b-784">Examples</span></span>

<span data-ttu-id="1935b-785">Şablon adını C# belirterek bir konsol uygulaması projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1935b-785">Create a C# console application project by specifying the template name:</span></span>

`dotnet new "Console Application"`

<span data-ttu-id="1935b-786">Geçerli dizinde F# bir konsol uygulaması projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1935b-786">Create an F# console application project in the current directory:</span></span>

`dotnet new console -lang F#`

<span data-ttu-id="1935b-787">Belirtilen dizinde bir .NET Standard sınıf kitaplığı projesi oluşturun (yalnızca .NET Core SDK 2,0 veya sonraki sürümlerle kullanılabilir):</span><span class="sxs-lookup"><span data-stu-id="1935b-787">Create a .NET Standard class library project in the specified directory (available only with .NET Core SDK 2.0 or later versions):</span></span>

`dotnet new classlib -lang VB -o MyLibrary`

<span data-ttu-id="1935b-788">Geçerli dizinde kimlik doğrulaması C# olmadan yeni bir ASP.NET Core MVC projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1935b-788">Create a new ASP.NET Core C# MVC project in the current directory with no authentication:</span></span>

`dotnet new mvc -au None`

<span data-ttu-id="1935b-789">Yeni bir xUnit projesi oluştur:</span><span class="sxs-lookup"><span data-stu-id="1935b-789">Create a new xUnit project:</span></span>

`dotnet new xunit`

<span data-ttu-id="1935b-790">MVC için kullanılabilen tüm şablonları listeleyin:</span><span class="sxs-lookup"><span data-stu-id="1935b-790">List all templates available for MVC:</span></span>

`dotnet new mvc -l`

<span data-ttu-id="1935b-791">*We* alt dizeniz ile eşleşen tüm şablonları listeleyin.</span><span class="sxs-lookup"><span data-stu-id="1935b-791">List all templates matching the *we* substring.</span></span> <span data-ttu-id="1935b-792">Tam eşleşme bulunamadı, bu nedenle alt dize eşleştirmesi hem kısa ad hem de ad sütunlarında çalışır.</span><span class="sxs-lookup"><span data-stu-id="1935b-792">No exact match is found, so substring matching runs against both the short name and name columns.</span></span>

`dotnet new we -l`

<span data-ttu-id="1935b-793">Şablonla *eşleşen şablonu*çağırma girişimi.</span><span class="sxs-lookup"><span data-stu-id="1935b-793">Attempt to invoke the template matching *ng*.</span></span> <span data-ttu-id="1935b-794">Tek bir eşleşme belirlenemiyorsa kısmi eşleşen şablonları listeleyin.</span><span class="sxs-lookup"><span data-stu-id="1935b-794">If a single match can't be determined, list the templates that are partial matches.</span></span>

`dotnet new ng`

<span data-ttu-id="1935b-795">ASP.NET Core için tek sayfalı uygulama şablonlarının 2,0 sürümünü (yalnızca .NET Core SDK 1,1 ve sonraki sürümler için kullanılabilir) (komut seçeneği) yükler:</span><span class="sxs-lookup"><span data-stu-id="1935b-795">Install version 2.0 of the Single Page Application templates for ASP.NET Core (command option available for .NET Core SDK 1.1 and later versions only):</span></span>

`dotnet new -i Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0`

<span data-ttu-id="1935b-796">SDK sürümü 2.0.0 (yalnızca .NET Core SDK 2,0 veya üzeri sürümlerle kullanılabilir) ayarı geçerli dizinde *Global. JSON* oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1935b-796">Create a *global.json* in the current directory setting the SDK version to 2.0.0 (available only with .NET Core SDK 2.0 or later versions):</span></span>

`dotnet new globaljson --sdk-version 2.0.0`

## <a name="see-also"></a><span data-ttu-id="1935b-797">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="1935b-797">See also</span></span>

- [<span data-ttu-id="1935b-798">DotNet New için özel şablonlar</span><span class="sxs-lookup"><span data-stu-id="1935b-798">Custom templates for dotnet new</span></span>](custom-templates.md)
- [<span data-ttu-id="1935b-799">Dotnet new için özel şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="1935b-799">Create a custom template for dotnet new</span></span>](../tutorials/create-custom-template.md)
- [<span data-ttu-id="1935b-800">DotNet/DotNet-şablon-örnek GitHub deposu</span><span class="sxs-lookup"><span data-stu-id="1935b-800">dotnet/dotnet-template-samples GitHub repo</span></span>](https://github.com/dotnet/dotnet-template-samples)
- [<span data-ttu-id="1935b-801">DotNet New için kullanılabilir şablonlar</span><span class="sxs-lookup"><span data-stu-id="1935b-801">Available templates for dotnet new</span></span>](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)
