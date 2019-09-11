---
title: Eklentilerle .NET Core uygulaması oluşturma
description: Eklentileri destekleyen bir .NET Core uygulaması oluşturmayı öğrenin.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/28/2019
ms.openlocfilehash: 54a4459619ee69fc74a14da7ff7fe10a472a4433
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70849439"
---
# <a name="create-a-net-core-application-with-plugins"></a><span data-ttu-id="0e791-103">Eklentilerle .NET Core uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e791-103">Create a .NET Core application with plugins</span></span>

<span data-ttu-id="0e791-104">Bu öğreticide nasıl yapılacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="0e791-104">This tutorial shows you how to:</span></span>

- <span data-ttu-id="0e791-105">Eklentileri desteklemek için bir proje yapısı yapın.</span><span class="sxs-lookup"><span data-stu-id="0e791-105">Structure a project to support plugins.</span></span>
- <span data-ttu-id="0e791-106">Her bir eklentiyi <xref:System.Runtime.Loader.AssemblyLoadContext> yüklemek için özel oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e791-106">Create a custom <xref:System.Runtime.Loader.AssemblyLoadContext> to load each plugin.</span></span>
- <span data-ttu-id="0e791-107">Eklentilerin bağımlılıklara sahip olmasını sağlamak için türükullanın.`System.Runtime.Loader.AssemblyDependencyResolver`</span><span class="sxs-lookup"><span data-stu-id="0e791-107">Use the `System.Runtime.Loader.AssemblyDependencyResolver` type to allow plugins to have dependencies.</span></span>
- <span data-ttu-id="0e791-108">Yalnızca derleme yapıtları kopyalanarak kolayca dağıtılabilecek olan eklentileri yazar.</span><span class="sxs-lookup"><span data-stu-id="0e791-108">Author plugins that can be easily deployed by just copying the build artifacts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e791-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0e791-109">Prerequisites</span></span>

- <span data-ttu-id="0e791-110">[.NET Core 3,0 Preview 2 SDK](https://dotnet.microsoft.com/download) veya daha yeni bir sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="0e791-110">Install the [.NET Core 3.0 Preview 2 SDK](https://dotnet.microsoft.com/download) or a newer version.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="0e791-111">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e791-111">Create the application</span></span>

<span data-ttu-id="0e791-112">İlk adım, uygulamayı oluşturmaktır:</span><span class="sxs-lookup"><span data-stu-id="0e791-112">The first step is to create the application:</span></span>

1. <span data-ttu-id="0e791-113">Yeni bir klasör oluşturun ve bu klasörde ' i çalıştırın `dotnet new console -o AppWithPlugin`.</span><span class="sxs-lookup"><span data-stu-id="0e791-113">Create a new folder, and in that folder run `dotnet new console -o AppWithPlugin`.</span></span> 
2. <span data-ttu-id="0e791-114">Projeyi daha kolay hale getirmek için bir Visual Studio çözüm dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0e791-114">To make building the project easier, create a Visual Studio solution file.</span></span> <span data-ttu-id="0e791-115">Aynı `dotnet new sln` klasörde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e791-115">Run `dotnet new sln` in the same folder.</span></span> 
3. <span data-ttu-id="0e791-116">Uygulama `dotnet sln add AppWithPlugin/AppWithPlugin.csproj` projesini çözüme eklemek için ' i çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e791-116">Run `dotnet sln add AppWithPlugin/AppWithPlugin.csproj` to add the app project to the solution.</span></span>

<span data-ttu-id="0e791-117">Şimdi uygulamamızın iskektlerini dolduracağız.</span><span class="sxs-lookup"><span data-stu-id="0e791-117">Now we can fill in the skeleton of our application.</span></span> <span data-ttu-id="0e791-118">*Appwithplugin/program. cs* dosyasındaki kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0e791-118">Replace the code in the *AppWithPlugin/Program.cs* file with the following code:</span></span>

```csharp
using PluginBase;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Reflection;

namespace AppWithPlugin
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                if (args.Length == 1 && args[0] == "/d")
                {
                    Console.WriteLine("Waiting for any key...");
                    Console.ReadLine();
                }

                // Load commands from plugins.

                if (args.Length == 0)
                {
                    Console.WriteLine("Commands: ");
                    // Output the loaded commands.
                }
                else
                {
                    foreach (string commandName in args)
                    {
                        Console.WriteLine($"-- {commandName} --");

                        // Execute the command with the name passed as an argument.

                        Console.WriteLine();
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex);
            }
        }
    }
}

```

## <a name="create-the-plugin-interfaces"></a><span data-ttu-id="0e791-119">Eklenti arabirimlerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e791-119">Create the plugin interfaces</span></span>

<span data-ttu-id="0e791-120">Eklentilerle uygulama oluşturmanın bir sonraki adımı, eklentilerin uygulanması gereken arabirimi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0e791-120">The next step in building an app with plugins is defining the interface the plugins need to implement.</span></span> <span data-ttu-id="0e791-121">Uygulamanız ve eklentiler arasında iletişim kurmak için kullanmayı planladığınız türleri içeren bir sınıf kitaplığı almanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="0e791-121">We suggest that you make a class library that contains any types that you plan to use for communicating between your app and plugins.</span></span> <span data-ttu-id="0e791-122">Bu bölüm, tam uygulamanızı teslim etmek zorunda kalmadan eklenti arabiriminizi bir paket olarak yayımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e791-122">This division allows you to publish your plugin interface as a package without having to ship your full application.</span></span>

<span data-ttu-id="0e791-123">Projenin kök klasöründe, öğesini çalıştırın `dotnet new classlib -o PluginBase`.</span><span class="sxs-lookup"><span data-stu-id="0e791-123">In the root folder of the project, run `dotnet new classlib -o PluginBase`.</span></span> <span data-ttu-id="0e791-124">Ayrıca, projeyi `dotnet sln add PluginBase/PluginBase.csproj` çözüm dosyasına eklemek için öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e791-124">Also, run `dotnet sln add PluginBase/PluginBase.csproj` to add the project to the solution file.</span></span> <span data-ttu-id="0e791-125">Dosyayı silin ve aşağıdaki arabirim tanımıyla adlı `PluginBase` `ICommand.cs` klasörde yeni bir dosya oluşturun: `PluginBase/Class1.cs`</span><span class="sxs-lookup"><span data-stu-id="0e791-125">Delete the `PluginBase/Class1.cs` file, and create a new file in the `PluginBase` folder named `ICommand.cs` with the following interface definition:</span></span>

[!code-csharp[the-plugin-interface](~/samples/core/extensions/AppWithPlugin/PluginBase/ICommand.cs)]

<span data-ttu-id="0e791-126">Bu `ICommand` arabirim, tüm eklentilerin uygulayamayacağı arabirimdir.</span><span class="sxs-lookup"><span data-stu-id="0e791-126">This `ICommand` interface is the interface that all of the plugins will implement.</span></span>

<span data-ttu-id="0e791-127">`ICommand` Arabirim tanımlandığına göre, uygulama projesi biraz daha fazla doldurulabilir.</span><span class="sxs-lookup"><span data-stu-id="0e791-127">Now that the `ICommand` interface is defined, the application project can be filled in a little more.</span></span> <span data-ttu-id="0e791-128">Kök klasördeki `dotnet add AppWithPlugin\AppWithPlugin.csproj reference PluginBase\PluginBase.csproj` komutla projeye bir `AppWithPlugin` başvuru `PluginBase` ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0e791-128">Add a reference from the `AppWithPlugin` project to the `PluginBase` project with the `dotnet add AppWithPlugin\AppWithPlugin.csproj reference PluginBase\PluginBase.csproj`  command from the root folder.</span></span>

<span data-ttu-id="0e791-129">Verilen dosya yollarından eklentileri yüklemesini etkinleştirmek için yorumuaşağıdakikodparçacığıiledeğiştirin:`// Load commands from plugins`</span><span class="sxs-lookup"><span data-stu-id="0e791-129">Replace the `// Load commands from plugins` comment with the following code snippet to enable it to load plugins from given file paths:</span></span>

```csharp
string[] pluginPaths = new string[]
{
    // Paths to plugins to load.
};

IEnumerable<ICommand> commands = pluginPaths.SelectMany(pluginPath =>
{
    Assembly pluginAssembly = LoadPlugin(pluginPath);
    return CreateCommands(pluginAssembly);
}).ToList();
```

<span data-ttu-id="0e791-130">Sonra `// Output the loaded commands` yorumu aşağıdaki kod parçacığı ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0e791-130">Then replace the `// Output the loaded commands` comment with the following code snippet:</span></span>

```csharp
foreach (ICommand command in commands)
{
    Console.WriteLine($"{command.Name}\t - {command.Description}");
}
```

<span data-ttu-id="0e791-131">`// Execute the command with the name passed as an argument` Yorumu aşağıdaki kod parçacığıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0e791-131">Replace the `// Execute the command with the name passed as an argument` comment with the following snippet:</span></span>

```csharp
ICommand command = commands.FirstOrDefault(c => c.Name == commandName);
if (command == null)
{
    Console.WriteLine("No such command is known.");
    return;
}

command.Execute();
```

<span data-ttu-id="0e791-132">Son olarak, burada gösterildiği gibi, ve `Program` `CreateCommands`adlı `LoadPlugin` sınıfa statik yöntemler ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0e791-132">And finally, add static methods to the `Program` class named `LoadPlugin` and `CreateCommands`, as shown here:</span></span>

```csharp
static Assembly LoadPlugin(string relativePath)
{
    throw new NotImplementedException();
}

static IEnumerable<ICommand> CreateCommands(Assembly assembly)
{
    int count = 0;

    foreach (Type type in assembly.GetTypes())
    {
        if (typeof(ICommand).IsAssignableFrom(type))
        {
            ICommand result = Activator.CreateInstance(type) as ICommand;
            if (result != null)
            {
                count++;
                yield return result;
            }
        }
    }

    if (count == 0)
    {
        string availableTypes = string.Join(",", assembly.GetTypes().Select(t => t.FullName));
        throw new ApplicationException(
            $"Can't find any type which implements ICommand in {assembly} from {assembly.Location}.\n" +
            $"Available types: {availableTypes}");
    }
}
```

## <a name="load-plugins"></a><span data-ttu-id="0e791-133">Eklentileri yükle</span><span class="sxs-lookup"><span data-stu-id="0e791-133">Load plugins</span></span>

<span data-ttu-id="0e791-134">Artık uygulama, yüklenen eklenti derlemelerinden komutları doğru bir şekilde yükleyebilir ve örneklendirilecek, ancak hala eklenti derlemelerini yükleyemeyebilir.</span><span class="sxs-lookup"><span data-stu-id="0e791-134">Now the application can correctly load and instantiate commands from loaded plugin assemblies, but it is still unable to load the plugin assemblies.</span></span> <span data-ttu-id="0e791-135">*Appwithplugin* klasöründe aşağıdaki içeriğe sahip *PluginLoadContext.cs* adlı bir dosya oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0e791-135">Create a file named *PluginLoadContext.cs* in the *AppWithPlugin* folder with the following contents:</span></span>

[!code-csharp[loading-plugins](~/samples/core/extensions/AppWithPlugin/AppWithPlugin/PluginLoadContext.cs)]

<span data-ttu-id="0e791-136">`PluginLoadContext` Tür öğesinden<xref:System.Runtime.Loader.AssemblyLoadContext>türetilir.</span><span class="sxs-lookup"><span data-stu-id="0e791-136">The `PluginLoadContext` type derives from <xref:System.Runtime.Loader.AssemblyLoadContext>.</span></span> <span data-ttu-id="0e791-137">Bu `AssemblyLoadContext` tür çalışma zamanında, geliştiricilerin, derleme sürümlerinin çakışmadığından emin olmak için yüklü derlemeleri farklı gruplara yalıtmalarına olanak tanıyan özel bir türdür.</span><span class="sxs-lookup"><span data-stu-id="0e791-137">The `AssemblyLoadContext` type is a special type in the runtime that allows developers to isolate loaded assemblies into different groups to ensure that assembly versions do not conflict.</span></span> <span data-ttu-id="0e791-138">Ayrıca, özel `AssemblyLoadContext` , derlemeleri yüklemek için farklı yollar seçebilir ve varsayılan davranışı geçersiz kılabilir.</span><span class="sxs-lookup"><span data-stu-id="0e791-138">Additionally, a custom `AssemblyLoadContext` can choose different paths to load assemblies from and override the default behavior.</span></span> <span data-ttu-id="0e791-139">, `PluginLoadContext` Derleme adlarını yollara çözümlemek için `AssemblyDependencyResolver` .NET Core 3,0 ' de tanıtılan türün bir örneğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0e791-139">The `PluginLoadContext` uses an instance of the `AssemblyDependencyResolver` type introduced in .NET Core 3.0 to resolve assembly names to paths.</span></span> <span data-ttu-id="0e791-140">`AssemblyDependencyResolver` Nesnesi, .NET sınıf kitaplığı yoluyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0e791-140">The `AssemblyDependencyResolver` object is constructed with the path to a .NET class library.</span></span> <span data-ttu-id="0e791-141">Derlemeleri ve yerel kitaplıkları, yolu `AssemblyDependencyResolver` oluşturucuya geçilen sınıf kitaplığı için *. Deps. JSON* dosyasını temel alarak göreli yollarına çözümler.</span><span class="sxs-lookup"><span data-stu-id="0e791-141">It resolves assemblies and native libraries to their relative paths based on the *.deps.json* file for the class library whose path was passed to the `AssemblyDependencyResolver` constructor.</span></span> <span data-ttu-id="0e791-142">Özel `AssemblyLoadContext` , eklentilerin kendi bağımlılıklarına sahip olmasını sağlar `AssemblyDependencyResolver` ve bağımlılıkları doğru şekilde yüklemeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="0e791-142">The custom `AssemblyLoadContext` enables plugins to have their own dependencies, and the `AssemblyDependencyResolver` makes it easy to correctly load the dependencies.</span></span>

<span data-ttu-id="0e791-143">`AppWithPlugin` `Program.LoadPlugin` Projenin türüolduğunagöre,yöntemiaşağıdakigövdelegüncelleştirin`PluginLoadContext` :</span><span class="sxs-lookup"><span data-stu-id="0e791-143">Now that the `AppWithPlugin` project has the `PluginLoadContext` type, update the `Program.LoadPlugin` method with the following body:</span></span>

```csharp
static Assembly LoadPlugin(string relativePath)
{
    // Navigate up to the solution root
    string root = Path.GetFullPath(Path.Combine(
        Path.GetDirectoryName(
            Path.GetDirectoryName(
                Path.GetDirectoryName(
                    Path.GetDirectoryName(
                        Path.GetDirectoryName(typeof(Program).Assembly.Location)))))));

    string pluginLocation = Path.GetFullPath(Path.Combine(root, relativePath.Replace('\\', Path.DirectorySeparatorChar)));
    Console.WriteLine($"Loading commands from: {pluginLocation}");
    PluginLoadContext loadContext = new PluginLoadContext(pluginLocation);
    return loadContext.LoadFromAssemblyName(new AssemblyName(Path.GetFileNameWithoutExtension(pluginLocation)));
}
```

<span data-ttu-id="0e791-144">Her eklenti için farklı `PluginLoadContext` bir örnek kullanarak, Eklentiler, sorun olmadan farklı veya hatta çakışan bağımlılıklara sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="0e791-144">By using a different `PluginLoadContext` instance for each plugin, the plugins can have different or even conflicting dependencies without issue.</span></span>

## <a name="create-a-simple-plugin-with-no-dependencies"></a><span data-ttu-id="0e791-145">Bağımlılıkları olmayan basit bir eklenti oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e791-145">Create a simple plugin with no dependencies</span></span>

<span data-ttu-id="0e791-146">Kök klasöre geri döndüğünüzde şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="0e791-146">Back in the root folder, do the following:</span></span>

1. <span data-ttu-id="0e791-147">`dotnet new classlib -o HelloPlugin` Adlı`HelloPlugin`yeni bir sınıf kitaplığı projesi oluşturmak için öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e791-147">Run `dotnet new classlib -o HelloPlugin` to create a new class library project named `HelloPlugin`.</span></span>
2. <span data-ttu-id="0e791-148">`dotnet sln add HelloPlugin/HelloPlugin.csproj` Projeyi`AppWithPlugin` çözüme eklemek için ' i çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e791-148">Run `dotnet sln add HelloPlugin/HelloPlugin.csproj` to add the project to the `AppWithPlugin` solution.</span></span> 
3. <span data-ttu-id="0e791-149">*Merhaba Plugin/Class1. cs* dosyasını aşağıdaki içeriklerle *HelloCommand.cs* adlı bir dosyayla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0e791-149">Replace the *HelloPlugin/Class1.cs* file with a file named *HelloCommand.cs* with the following contents:</span></span>

[!code-csharp[the-hello-plugin](~/samples/core/extensions/AppWithPlugin/HelloPlugin/HelloCommand.cs)]

<span data-ttu-id="0e791-150">Şimdi, *Helloplugin. csproj* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="0e791-150">Now, open the *HelloPlugin.csproj* file.</span></span> <span data-ttu-id="0e791-151">Şuna benzer olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="0e791-151">It should look similar to the following:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netcoreapp3.0</TargetFramework>
  </PropertyGroup>

</Project>

```

<span data-ttu-id="0e791-152">`<Project>` Etiketler arasında, aşağıdaki öğeleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0e791-152">In between the `<Project>` tags, add the following elements:</span></span>

```xml
<ItemGroup>
<ProjectReference Include="..\PluginBase\PluginBase.csproj">
    <Private>false</Private>
</ProjectReference>
</ItemGroup>
```

<span data-ttu-id="0e791-153">`<Private>false</Private>` Öğesi çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0e791-153">The `<Private>false</Private>` element is very important.</span></span> <span data-ttu-id="0e791-154">Bu, MSBuild 'in *Pluginbase. dll dosyasını* helloplugin çıkış dizinine kopyalamamasını söyler.</span><span class="sxs-lookup"><span data-stu-id="0e791-154">This tells MSBuild to not copy *PluginBase.dll* to the output directory for HelloPlugin.</span></span> <span data-ttu-id="0e791-155">' Nin çıkış dizininde *pluginbase. dll* derlemesi varsa, `PluginLoadContext` derlemeyi bulur ve *Merhaba Plugin. dll* derlemesini yüklediğinde yükler.</span><span class="sxs-lookup"><span data-stu-id="0e791-155">If the *PluginBase.dll* assembly is present in the output directory, `PluginLoadContext` will find the assembly there and load it when it loads the *HelloPlugin.dll* assembly.</span></span> <span data-ttu-id="0e791-156">Bu noktada, `HelloPlugin.HelloCommand` türü, varsayılan yükleme bağlamına `ICommand` yüklenen `ICommand` arabirimi değil,, `HelloPlugin` projenin çıkış dizinindeki *pluginbase. dll* ' den arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="0e791-156">At this point, the `HelloPlugin.HelloCommand` type will implement the `ICommand` interface from the *PluginBase.dll* in the output directory of the `HelloPlugin` project, not the `ICommand` interface that is loaded into the default load context.</span></span> <span data-ttu-id="0e791-157">Çalışma zamanı, bu iki türü farklı derlemelerden farklı türler olarak gördüğünden, `AppWithPlugin.Program.CreateCommands` bu yöntem komutları bulamaz.</span><span class="sxs-lookup"><span data-stu-id="0e791-157">Since the runtime sees these two types as different types from different assemblies, the `AppWithPlugin.Program.CreateCommands` method will not find the commands.</span></span> <span data-ttu-id="0e791-158">Sonuç olarak, `<Private>false</Private>` eklenti arabirimlerini içeren derlemeye başvuru için meta veriler gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e791-158">As a result, the `<Private>false</Private>` metadata is required for the reference to the assembly containing the plugin interfaces.</span></span>

<span data-ttu-id="0e791-159">Proje tamamlandığına göre, `HelloPlugin` eklentinin nerede bulunabileceğinizi bilmesi için `AppWithPlugin` projeyi güncelleştirmemiz gerekir. `HelloPlugin`</span><span class="sxs-lookup"><span data-stu-id="0e791-159">Now that the `HelloPlugin` project is complete, we should update the `AppWithPlugin` project to know where the `HelloPlugin` plugin can be found.</span></span> <span data-ttu-id="0e791-160">Açıklamadan sonra, `pluginPaths` dizinin bir öğesi olarak ekleyin. `@"HelloPlugin\bin\Debug\netcoreapp3.0\HelloPlugin.dll"` `// Paths to plugins to load`</span><span class="sxs-lookup"><span data-stu-id="0e791-160">After the `// Paths to plugins to load` comment, add `@"HelloPlugin\bin\Debug\netcoreapp3.0\HelloPlugin.dll"` as an element of the `pluginPaths` array.</span></span>

## <a name="create-a-plugin-with-library-dependencies"></a><span data-ttu-id="0e791-161">Kitaplık bağımlılıklarıyla eklenti oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e791-161">Create a plugin with library dependencies</span></span>

<span data-ttu-id="0e791-162">Neredeyse tüm eklentiler basit bir "Merhaba Dünya" öğesinden daha karmaşıktır ve birçok eklenti diğer kitaplıklara bağımlılıkları vardır.</span><span class="sxs-lookup"><span data-stu-id="0e791-162">Almost all plugins are more complex than a simple "Hello World", and many plugins have dependencies on other libraries.</span></span> <span data-ttu-id="0e791-163">Örnekteki `JsonPlugin` `Newtonsoft.Json`ve `OldJson` eklenti projeleri üzerinde NuGet paketi bağımlılıklarını içeren iki eklenti örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e791-163">The `JsonPlugin` and `OldJson` plugin projects in the sample show two examples of plugins with NuGet package dependencies on `Newtonsoft.Json`.</span></span> <span data-ttu-id="0e791-164">Proje dosyaları, proje başvuruları için özel bilgilere sahip değildir ve (eklenti yolları `pluginPaths` diziye eklendikten sonra) Eklentiler, appwithplugin uygulamasının yürütülmesi halinde çalıştırılsa bile kusursuz bir şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="0e791-164">The project files themselves do not have any special information for the project references, and (after adding the plugin paths to the `pluginPaths` array) the plugins run perfectly, even if run in the same execution of the AppWithPlugin app.</span></span> <span data-ttu-id="0e791-165">Ancak, bu projeler başvurulan derlemeleri çıkış dizinine kopyalamadıkları için, eklentilerin çalışması için kullanıcının makinesinde derlemelerin mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e791-165">However, these projects do not copy the referenced assemblies to their output directory, so the assemblies need to be present on the user's machine for the plugins to work.</span></span> <span data-ttu-id="0e791-166">Bu sorunu geçici olarak çözmek için iki yol vardır.</span><span class="sxs-lookup"><span data-stu-id="0e791-166">There are two ways to work around this problem.</span></span> <span data-ttu-id="0e791-167">İlk seçenek, sınıf kitaplığını yayımlamak için `dotnet publish` komutunu kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="0e791-167">The first option is to use the `dotnet publish` command to publish the class library.</span></span> <span data-ttu-id="0e791-168">Alternatif olarak, eklenti `dotnet build` için çıkışını kullanmak istiyorsanız, eklentinin proje dosyasındaki `<PropertyGroup>` Etiketler arasına `<CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>` özelliği ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e791-168">Alternatively, if you want to be able to use the output of `dotnet build` for your plugin, you can add the `<CopyLocalLockFileAssemblies>true</CopyLocalLockFileAssemblies>` property between the `<PropertyGroup>` tags in the plugin's project file.</span></span> <span data-ttu-id="0e791-169">Örnek için bkz. eklentiprojesi.`XcopyablePlugin`</span><span class="sxs-lookup"><span data-stu-id="0e791-169">See the `XcopyablePlugin` plugin project for an example.</span></span>

## <a name="other-plugin-examples-in-the-sample"></a><span data-ttu-id="0e791-170">Örnekteki diğer eklenti örnekleri</span><span class="sxs-lookup"><span data-stu-id="0e791-170">Other plugin examples in the sample</span></span>

<span data-ttu-id="0e791-171">Bu öğreticinin tüm kaynak kodu [DotNet/Samples deposunda](https://github.com/dotnet/samples/tree/master/core/extensions/AppWithPlugin)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="0e791-171">The complete source code for this tutorial can be found in [the dotnet/samples repository](https://github.com/dotnet/samples/tree/master/core/extensions/AppWithPlugin).</span></span> <span data-ttu-id="0e791-172">Tamamlanan örnek, bazı `AssemblyDependencyResolver` davranış örneklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="0e791-172">The completed sample includes a few other examples of `AssemblyDependencyResolver` behavior.</span></span> <span data-ttu-id="0e791-173">Örneğin, `AssemblyDependencyResolver` nesne yerel kitaplıkları ve NuGet paketlerine dahil edilen yerelleştirilmiş uydu derlemelerini de çözümleyebilir.</span><span class="sxs-lookup"><span data-stu-id="0e791-173">For example, the `AssemblyDependencyResolver` object can also resolve native libraries as well as localized satellite assemblies included in NuGet packages.</span></span> <span data-ttu-id="0e791-174">Örnekler deposunda `FrenchPlugin` ve bu senaryolar gösterilmektedir. `UVPlugin`</span><span class="sxs-lookup"><span data-stu-id="0e791-174">The `UVPlugin` and `FrenchPlugin` in the samples repository demonstrate these scenarios.</span></span>

## <a name="how-to-reference-a-plugin-interface-assembly-defined-in-a-nuget-package"></a><span data-ttu-id="0e791-175">NuGet paketinde tanımlanan eklenti arabirimi derlemesine başvurma</span><span class="sxs-lookup"><span data-stu-id="0e791-175">How to reference a plugin interface assembly defined in a NuGet package</span></span>

<span data-ttu-id="0e791-176">Adlı bir uygulama olan, adlı `A.PluginBase`NuGet paketinde tanımlanmış bir eklenti arabirimi olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="0e791-176">Let's say that there is an app A that has a plugin interface defined in the NuGet package named `A.PluginBase`.</span></span> <span data-ttu-id="0e791-177">Eklenti projenizde pakete doğru şekilde nasıl başvurdunuz?</span><span class="sxs-lookup"><span data-stu-id="0e791-177">How do you reference the package correctly in your plugin project?</span></span> <span data-ttu-id="0e791-178">Proje başvuruları için, proje dosyasındaki `<Private>false</Private>` `ProjectReference` öğesindeki meta verilerin kullanılması dll 'nin çıkışa kopyalanmasını engelledi.</span><span class="sxs-lookup"><span data-stu-id="0e791-178">For project references, using the `<Private>false</Private>` metadata on the `ProjectReference` element in the project file prevented the dll from being copied to the output.</span></span>

<span data-ttu-id="0e791-179">`A.PluginBase` Pakete doğru bir şekilde başvurmak için proje dosyasındaki `<PackageReference>` öğeyi şu şekilde değiştirmek istersiniz:</span><span class="sxs-lookup"><span data-stu-id="0e791-179">To correctly reference the `A.PluginBase` package, you want to change the `<PackageReference>` element in the project file to the following:</span></span>

```xml
<PackageReference Include="A.PluginBase" Version="1.0.0">
    <ExcludeAssets>runtime</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="0e791-180">Bu, `A.PluginBase` derlemelerin eklentinin çıkış dizinine kopyalanmasını engeller ve eklenti 'un `A.PluginBase`bir sürümünü kullanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e791-180">This prevents the `A.PluginBase` assemblies from being copied to the output directory of your plugin and ensures that your plugin will use A's version of `A.PluginBase`.</span></span>

## <a name="plugin-target-framework-recommendations"></a><span data-ttu-id="0e791-181">Eklenti hedef Framework önerileri</span><span class="sxs-lookup"><span data-stu-id="0e791-181">Plugin target framework recommendations</span></span>

<span data-ttu-id="0e791-182">Eklenti bağımlılık yüklemesi *. Deps. JSON* dosyasını kullandığından, eklentinin hedef çerçevesiyle ilgili bir Gotcha vardır.</span><span class="sxs-lookup"><span data-stu-id="0e791-182">Because plugin dependency loading uses the *.deps.json* file, there is a gotcha related to the plugin's target framework.</span></span> <span data-ttu-id="0e791-183">Özellikle, eklentilerinizin bir .NET Standard sürümü yerine .NET Core 3,0 gibi bir çalışma zamanını hedeflemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0e791-183">Specifically, your plugins should target a runtime, such as .NET Core 3.0, instead of a version of .NET Standard.</span></span> <span data-ttu-id="0e791-184">*. Deps. JSON* dosyası, projenin hedeflediği çerçeveye göre oluşturulur ve birçok .NET Standard uyumlu paket, belirli çalışma zamanları için .NET Standard ve uygulama derlemelerinin oluşturulmasına yönelik başvuru derlemeleri sunduğundan, *. Deps. JSON* uygulama derlemelerini doğru görmeyebilir veya Istediğiniz .NET Core sürümü yerine bir derlemenin .NET Standard sürümünü alabilir.</span><span class="sxs-lookup"><span data-stu-id="0e791-184">The *.deps.json* file is generated based on which framework the project targets, and since many .NET Standard-compatible packages ship reference assemblies for building against .NET Standard and implementation assemblies for specific runtimes, the *.deps.json* may not correctly see implementation assemblies, or it may grab the .NET Standard version of an assembly instead of the .NET Core version you expect.</span></span>
