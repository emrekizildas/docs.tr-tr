---
title: 'Nasıl yapılır: Çoklu dosya derlemesi oluşturma'
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- entry point for assembly
- compiling assemblies
- Al.exe
- command-line compilers
- assembly manifest, multifile assemblies
- assemblies [.NET Framework], compiling
- Assembly Linker
- code modules
- multifile assemblies
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 261c5583-8a76-412d-bda7-9b8ee3b131e5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9b95d686529da83a5a52edb80219874530212dcc
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991255"
---
# <a name="how-to-build-a-multifile-assembly"></a><span data-ttu-id="ba4dd-102">Nasıl yapılır: Çoklu dosya derlemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba4dd-102">How to: Build a multifile assembly</span></span>

<span data-ttu-id="ba4dd-103">Bu makalede, çok dosyalı bir derlemenin nasıl oluşturulacağı ve yordamdaki her adımın gösterildiği kod nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-103">This article explains how to create a multifile assembly and provides code that illustrates each step in the procedure.</span></span>

> [!NOTE]
> <span data-ttu-id="ba4dd-104">Ve Visual Basic için C# VISUAL Studio IDE yalnızca tek dosya derlemeler oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-104">The Visual Studio IDE for C# and Visual Basic can only be used to create single-file assemblies.</span></span> <span data-ttu-id="ba4dd-105">Çok dosyalı derlemeler oluşturmak istiyorsanız, komut satırı derleyicilerini veya Visual Studio 'Yu Visual C++Studio kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-105">If you want to create multifile assemblies, you must use the command-line compilers or Visual Studio with Visual C++.</span></span> <span data-ttu-id="ba4dd-106">Çok dosyalı derlemeler yalnızca .NET Framework tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-106">Multifile assemblies are supported by .NET Framework only.</span></span>

## <a name="create-a-multifile-assembly"></a><span data-ttu-id="ba4dd-107">Çoklu dosya derlemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba4dd-107">Create a multifile assembly</span></span>

1. <span data-ttu-id="ba4dd-108">Derlemedeki diğer modüller tarafından kod modüllerine başvuruda bulunulan ad alanlarını içeren tüm dosyaları derleyin.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-108">Compile all files that contain namespaces referenced by other modules in the assembly into code modules.</span></span> <span data-ttu-id="ba4dd-109">Kod modülleri için varsayılan uzantı *. netmodule*'dir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-109">The default extension for code modules is *.netmodule*.</span></span>

   <span data-ttu-id="ba4dd-110">Örneğin, `Stringer` dosyada adlı bir sınıf `Stringer`içeren bir `myStringer`ad alanı olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-110">For example, let's say the `Stringer` file has a namespace called `myStringer`, which includes a class called `Stringer`.</span></span> <span data-ttu-id="ba4dd-111">Sınıfı, konsola tek bir satır `StringerMethod` yazan adlı bir yöntemi içerir. `Stringer`</span><span class="sxs-lookup"><span data-stu-id="ba4dd-111">The `Stringer` class contains a method called `StringerMethod` that writes a single line to the console.</span></span>

   ```cpp
   // Assembly building example in the .NET Framework.
   using namespace System;

   namespace myStringer
   {
       public ref class Stringer
       {
       public:
           void StringerMethod()
           {
               System::Console::WriteLine("This is a line from StringerMethod.");
           }
       };
   }
   ```

   ```csharp
   // Assembly building example in the .NET Framework.
   using System;

   namespace myStringer
   {
       public class Stringer
       {
           public void StringerMethod()
           {
               System.Console.WriteLine("This is a line from StringerMethod.");
           }
       }
   }
   ```

   ```vb
   ' Assembly building example in the .NET Framework.
   Imports System

   Namespace myStringer
       Public Class Stringer
           Public Sub StringerMethod()
               System.Console.WriteLine("This is a line from StringerMethod.")
           End Sub
       End Class
   End Namespace
   ```

2. <span data-ttu-id="ba4dd-112">Bu kodu derlemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ba4dd-112">Use the following command to compile this code:</span></span>

   ```cpp
   cl /clr:pure /LN Stringer.cpp
   ```

   ```csharp
   csc /t:module Stringer.cs
   ```

   ```vb
   vbc /t:module Stringer.vb
   ```

   <span data-ttu-id="ba4dd-113">**/T:** derleyici seçeneğiyle *Modül* parametresini belirtme, dosyanın derleme yerine bir modül olarak derlenmesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-113">Specifying the *module* parameter with the **/t:** compiler option indicates that the file should be compiled as a module rather than as an assembly.</span></span> <span data-ttu-id="ba4dd-114">Derleyici, bir derlemeye eklenebilecek *strger. netmodule*adlı bir modül oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-114">The compiler produces a module called *Stringer.netmodule*, which can be added to an assembly.</span></span>

3. <span data-ttu-id="ba4dd-115">Kodda başvurulan diğer modülleri göstermek için gerekli derleyici seçeneklerini kullanarak diğer tüm modülleri derleyin.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-115">Compile all other modules, using the necessary compiler options to indicate the other modules that are referenced in the code.</span></span> <span data-ttu-id="ba4dd-116">Bu adım, **/addmodule** derleyici seçeneğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-116">This step uses the **/addmodule** compiler option.</span></span>

   <span data-ttu-id="ba4dd-117">Aşağıdaki örnekte, *istemci* adlı bir kod modülünün, 1. adımda oluşturulan `Main` *strger. dll* modülündeki bir yönteme başvuran bir giriş noktası yöntemi vardır.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-117">In the following example, a code module called *Client* has an entry point `Main` method that references a method in the *Stringer.dll* module created in step 1.</span></span>

   ```cpp
   #using "Stringer.netmodule"

   using namespace System;
   using namespace myStringer; //The namespace created in Stringer.netmodule.

   ref class MainClientApp
   {
       // Static method Main is the entry point method.
   public:
       static void Main()
       {
           Stringer^ myStringInstance = gcnew Stringer();
           Console::WriteLine("Client code executes");
           myStringInstance->StringerMethod();
       }
   };

   int main()
   {
       MainClientApp::Main();
   }
   ```

   ```csharp
   using System;
   using myStringer;

   class MainClientApp
   {
       // Static method Main is the entry point method.
       public static void Main()
       {
           Stringer myStringInstance = new Stringer();
           Console.WriteLine("Client code executes");
           myStringInstance.StringerMethod();
       }
   }
   ```

   ```vb
   Imports System
   Imports myStringer

   Class MainClientApp
       ' Static method Main is the entry point method.
       Public Shared Sub Main()
           Dim myStringInstance As New Stringer()
           Console.WriteLine("Client code executes")
           myStringInstance.StringerMethod()
       End Sub
   End Class
   ```

4. <span data-ttu-id="ba4dd-118">Bu kodu derlemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ba4dd-118">Use the following command to compile this code:</span></span>

   ```cpp
   cl /clr:pure /FUStringer.netmodule /LN Client.cpp
   ```

   ```csharp
   csc /addmodule:Stringer.netmodule /t:module Client.cs
   ```

   ```vb
   vbc /addmodule:Stringer.netmodule /t:module Client.vb
   ```

   <span data-ttu-id="ba4dd-119">Bu modül gelecekteki bir adımda bir derlemeye eklenecağından **/t: Module** seçeneğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-119">Specify the **/t:module** option because this module will be added to an assembly in a future step.</span></span> <span data-ttu-id="ba4dd-120">*İstemci* içindeki kod, *strger. netmodule*içindeki kodla oluşturulan bir ad alanına başvurduğundan **/addmodule** seçeneğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-120">Specify the **/addmodule** option because the code in *Client* references a namespace created by the code in *Stringer.netmodule*.</span></span> <span data-ttu-id="ba4dd-121">Derleyici, farklı bir modül olan *strger. netmodule*'e yönelik bir başvuru içeren *Client. netmodule* adlı bir modül üretir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-121">The compiler produces a module called *Client.netmodule* that contains a reference to another module, *Stringer.netmodule*.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ba4dd-122">C# Ve Visual Basic derleyicileri, aşağıdaki iki farklı sözdizimleri kullanılarak çok dosyalı derlemeler doğrudan oluşturulmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-122">The C# and Visual Basic compilers support directly creating multifile assemblies using the following two different syntaxes.</span></span>
   >
   > <span data-ttu-id="ba4dd-123">İki derleme iki dosya derleme oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ba4dd-123">Two compilations create a two-file assembly:</span></span>
   >
   >   ```cpp
   >   cl /clr:pure /LN Stringer.cpp
   >   cl /clr:pure Client.cpp /link /ASSEMBLYMODULE:Stringer.netmodule
   >   ```
   >
   >   ```csharp
   >   csc /t:module Stringer.cs
   >   csc Client.cs /addmodule:Stringer.netmodule
   >   ```
   >
   >   ```vb
   >   vbc /t:module Stringer.vb
   >   vbc Client.vb /addmodule:Stringer.netmodule
   >   ```
   >
   > <span data-ttu-id="ba4dd-124">Bir derleme iki dosya derleme oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ba4dd-124">One compilation creates a two-file assembly:</span></span>
   >
   >   ```cpp
   >   cl /clr:pure /LN Stringer.cpp
   >   cl /clr:pure Client.cpp /link /ASSEMBLYMODULE:Stringer.netmodule
   >   ```
   >
   >   ```csharp
   >   csc /out:Client.exe Client.cs /out:Stringer.netmodule Stringer.cs
   >   ```
   >
   >   ```vb
   >   vbc /out:Client.exe Client.vb /out:Stringer.netmodule Stringer.vb
   >   ```

5. <span data-ttu-id="ba4dd-125">Derleme bildirimini içeren çıktı dosyasını oluşturmak için [derleme Bağlayıcısı (al. exe)](../tools/al-exe-assembly-linker.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-125">Use the [Assembly Linker (Al.exe)](../tools/al-exe-assembly-linker.md) to create the output file that contains the assembly manifest.</span></span> <span data-ttu-id="ba4dd-126">Bu dosya, derlemenin parçası olan tüm modüller veya kaynaklar için başvuru bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-126">This file contains reference information for all modules or resources that are part of the assembly.</span></span>

    <span data-ttu-id="ba4dd-127">Komut satırında, aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="ba4dd-127">At the command prompt, type the following command:</span></span>

    <span data-ttu-id="ba4dd-128">**Al** \< *Modül*adımodül> adı>...\<</span><span class="sxs-lookup"><span data-stu-id="ba4dd-128">**al** \<*module name*> \<*module name*> …</span></span> <span data-ttu-id="ba4dd-129">**/Main:** \<*Yöntem adı*>  **/Out:** dosyaadı\< **/target:** *Assembly dosya* türü\<> ></span><span class="sxs-lookup"><span data-stu-id="ba4dd-129">**/main:**\<*method name*> **/out:**\<*file name*> **/target:**\<*assembly file type*></span></span>

    <span data-ttu-id="ba4dd-130">Bu komutta, *Modül adı* bağımsız değişkenleri derlemeye dahil edilecek her modülün adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-130">In this command, the *module name* arguments specify the name of each module to include in the assembly.</span></span> <span data-ttu-id="ba4dd-131">**/Main:** seçeneği derlemenin giriş noktası olan yöntem adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-131">The **/main:** option specifies the method name that is the assembly's entry point.</span></span> <span data-ttu-id="ba4dd-132">**/Out:** seçeneği, derleme meta verilerini içeren çıkış dosyasının adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-132">The **/out:** option specifies the name of the output file, which contains assembly metadata.</span></span> <span data-ttu-id="ba4dd-133">**/Target:** seçeneği, derlemenin bir konsol uygulaması yürütülebilir ( *. exe*) dosyası, bir Windows yürütülebilir ( *. Win*) dosyası veya bir kitaplık ( *. lib*) dosyası olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-133">The **/target:** option specifies that the assembly is a console application executable (*.exe*) file, a Windows executable (*.win*) file, or a library (*.lib*) file.</span></span>

    <span data-ttu-id="ba4dd-134">Aşağıdaki örnekte, *al. exe* , *MyAssembly. exe*adlı bir konsol uygulaması yürütülebilir dosyası olan bir derleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-134">In the following example, *Al.exe* creates an assembly that is a console application executable called *myAssembly.exe*.</span></span> <span data-ttu-id="ba4dd-135">Uygulama, *istemci. netmodule* ve *strger. netmodule*adlı iki modülden oluşur ve yalnızca derleme meta verilerini içeren *MyAssembly. exe*adlı yürütülebilir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-135">The application consists of two modules called *Client.netmodule* and *Stringer.netmodule*, and the executable file called *myAssembly.exe*, which contains only assembly metadata.</span></span> <span data-ttu-id="ba4dd-136">Derlemenin giriş noktası, sınıfının `Main` `MainClientApp` *Client. dll*dosyasında bulunan yöntemi olur.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-136">The entry point of the assembly is the `Main` method in the class `MainClientApp`, which is located in *Client.dll*.</span></span>

    ```cmd
    al Client.netmodule Stringer.netmodule /main:MainClientApp.Main /out:myAssembly.exe /target:exe
    ```

    <span data-ttu-id="ba4dd-137">Bir derlemenin içeriğini incelemek veya bir dosyanın derleme veya modülle olduğunu anlamak için [MSIL Disassembler (ıldadsm. exe)](../tools/ildasm-exe-il-disassembler.md) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-137">You can use the [MSIL Disassembler (Ildasm.exe)](../tools/ildasm-exe-il-disassembler.md) to examine the contents of an assembly, or determine whether a file is an assembly or a module.</span></span>

## <a name="see-also"></a><span data-ttu-id="ba4dd-138">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="ba4dd-138">See also</span></span>

- [<span data-ttu-id="ba4dd-139">Derlemeler oluştur</span><span class="sxs-lookup"><span data-stu-id="ba4dd-139">Create assemblies</span></span>](../../standard/assembly/create.md)
- [<span data-ttu-id="ba4dd-140">Nasıl yapılır: Derleme içeriğini görüntüle</span><span class="sxs-lookup"><span data-stu-id="ba4dd-140">How to: View assembly contents</span></span>](../../standard/assembly/view-contents.md)
- [<span data-ttu-id="ba4dd-141">Çalışma zamanının derlemeleri nasıl konumlandırır</span><span class="sxs-lookup"><span data-stu-id="ba4dd-141">How the runtime locates assemblies</span></span>](../deployment/how-the-runtime-locates-assemblies.md)
- [<span data-ttu-id="ba4dd-142">Çoklu dosya derlemeleri</span><span class="sxs-lookup"><span data-stu-id="ba4dd-142">Multifile assemblies</span></span>](multifile-assemblies.md)