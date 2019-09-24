---
title: Blazor ile yeniden kullanılabilir kullanıcı arabirimi bileşenleri oluşturun
description: Blazor ile yeniden kullanılabilir kullanıcı arabirimi bileşenleri oluşturmayı ve bunların ASP.NET Web Forms denetimleriyle nasıl karşılaştırılacağını öğrenin.
author: danroth27
ms.author: daroth
ms.date: 09/18/2019
ms.openlocfilehash: b461cf1b572de389c746b894d79d157bf2791e48
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71183954"
---
# <a name="build-reusable-ui-components-with-blazor"></a><span data-ttu-id="2a2cc-103">Blazor ile yeniden kullanılabilir kullanıcı arabirimi bileşenleri oluşturun</span><span class="sxs-lookup"><span data-stu-id="2a2cc-103">Build reusable UI components with Blazor</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="2a2cc-104">ASP.NET Web Forms hakkındaki harika şeyler, yeniden kullanılabilir kullanıcı arabirimi (UI) kodunun yeniden kullanılabilir kullanıcı arabirimi denetimlerine kapsüllemesini mümkün kılar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-104">One of the beautiful things about ASP.NET Web Forms is how it enables encapsulation of reusable pieces of user interface (UI) code into reusable UI controls.</span></span> <span data-ttu-id="2a2cc-105">Özel Kullanıcı denetimleri, *. ascx* dosyalarını kullanarak biçimlendirme içinde tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-105">Custom user controls can be defined in markup using *.ascx* files.</span></span> <span data-ttu-id="2a2cc-106">Ayrıca, tam tasarımcı desteğiyle kodda ayrıntılı sunucu denetimleri de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-106">You can also build elaborate server controls in code with full designer support.</span></span>

<span data-ttu-id="2a2cc-107">Blazor, *Bileşenler*aracılığıyla UI kapsüllemeyi de destekler.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-107">Blazor also supports UI encapsulation through *components*.</span></span> <span data-ttu-id="2a2cc-108">Bileşen:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-108">A component:</span></span>

* <span data-ttu-id="2a2cc-109">, Kendinden bağımsız bir kullanıcı arabirimi öbektir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-109">Is a self-contained chunk of UI.</span></span>
* <span data-ttu-id="2a2cc-110">Kendi durumunu ve işleme mantığını korur.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-110">Maintains its own state and rendering logic.</span></span>
* <span data-ttu-id="2a2cc-111">UI olay işleyicilerini tanımlayabilir, giriş verilerine bağlanabilir ve kendi yaşam döngüsünü yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-111">Can define UI event handlers, bind to input data, and manage its own lifecycle.</span></span>
* <span data-ttu-id="2a2cc-112">Genellikle Razor söz dizimi kullanarak bir *. Razor* dosyasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-112">Is typically defined in a *.razor* file using Razor syntax.</span></span>

## <a name="an-introduction-to-razor"></a><span data-ttu-id="2a2cc-113">Razor 'e giriş</span><span class="sxs-lookup"><span data-stu-id="2a2cc-113">An introduction to Razor</span></span>

<span data-ttu-id="2a2cc-114">Razor, HTML ve C#temel alan hafif bir işaretleme şablon dilidir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-114">Razor is a light-weight markup templating language based on HTML and C#.</span></span> <span data-ttu-id="2a2cc-115">Razor sayesinde, bileşen işleme mantığınızı tanımlamak için biçimlendirme C# ve kod arasında sorunsuzca geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-115">With Razor, you can seamlessly transition between markup and C# code to define your component rendering logic.</span></span> <span data-ttu-id="2a2cc-116">*. Razor* dosyası derlendiğinde, işleme mantığı .net sınıfında yapılandırılmış bir şekilde yakalanır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-116">When the *.razor* file is compiled, the rendering logic is captured in a structured way in a .NET class.</span></span> <span data-ttu-id="2a2cc-117">Derlenen sınıfın adı *. Razor* dosya adından alınır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-117">The name of the compiled class is taken from the *.razor* file name.</span></span> <span data-ttu-id="2a2cc-118">Ad alanı, proje ve klasör yolu için varsayılan ad alanından alınır veya `@namespace` yönergesini kullanarak ad alanını açıkça belirtebilirsiniz (aşağıdaki Razor yönergelerinden daha fazlası).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-118">The namespace is taken from the default namespace for the project and the folder path, or you can explicitly specify the namespace using the `@namespace` directive (more on Razor directives below).</span></span>

<span data-ttu-id="2a2cc-119">Bir bileşenin işleme mantığı, kullanılarak C#dinamik mantık eklenen normal HTML işaretlemesi kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-119">A component's rendering logic is authored using normal HTML markup with dynamic logic added using C#.</span></span> <span data-ttu-id="2a2cc-120">' A geçiş yapmak için C# karakter`@` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-120">The `@` character is used to transition to C#.</span></span> <span data-ttu-id="2a2cc-121">Razor genellikle HTML 'ye geri döndüğünüzde gelime konusunda akıllı bir değer sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-121">Razor is typically smart about figuring out when you've switched back to HTML.</span></span> <span data-ttu-id="2a2cc-122">Örneğin, aşağıdaki bileşen geçerli saat ile bir `<p>` etiket oluşturur:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-122">For example, the following component renders a `<p>` tag with the current time:</span></span>

```razor
<p>@DateTime.Now</p>
```

<span data-ttu-id="2a2cc-123">Bir C# ifadenin başlangıcını ve bitiyi açıkça belirtmek için parantez kullanın:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-123">To explicitly specify the beginning and ending of a C# expression, use parentheses:</span></span>

```razor
<p>@(DateTime.Now)</p>
```

<span data-ttu-id="2a2cc-124">Razor Ayrıca, işleme mantığınızdaki denetim C# akışını kullanmayı da kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-124">Razor also makes it easy to use C# control flow in your rendering logic.</span></span> <span data-ttu-id="2a2cc-125">Örneğin, koşullu olarak bazı HTML 'yi şöyle işleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-125">For example, you can conditionally render some HTML like this:</span></span>

```razor
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
```

<span data-ttu-id="2a2cc-126">Ya da aşağıdaki gibi normal C# `foreach` bir döngü kullanarak öğelerin bir listesini oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-126">Or you can generate a list of items using a normal C# `foreach` loop like this:</span></span>

```razor
<ul>
@foreach (var item in items)
{
    <li>item.Text</li>
}
</ul>
```

<span data-ttu-id="2a2cc-127">ASP.NET Web Forms içindeki yönergeler gibi Razor yönergeleri, Razor bileşeninin nasıl derlendiğine ilişkin birçok yönü denetler.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-127">Razor directives, like directives in ASP.NET Web Forms, control many aspects of how a Razor component is compiled.</span></span> <span data-ttu-id="2a2cc-128">Örneğin, bileşen şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-128">Examples include the component's:</span></span>

* <span data-ttu-id="2a2cc-129">Ad Alanı</span><span class="sxs-lookup"><span data-stu-id="2a2cc-129">Namespace</span></span>
* <span data-ttu-id="2a2cc-130">Temel sınıf</span><span class="sxs-lookup"><span data-stu-id="2a2cc-130">Base class</span></span>
* <span data-ttu-id="2a2cc-131">Uygulanan arabirimler</span><span class="sxs-lookup"><span data-stu-id="2a2cc-131">Implemented interfaces</span></span>
* <span data-ttu-id="2a2cc-132">Genel parametreler</span><span class="sxs-lookup"><span data-stu-id="2a2cc-132">Generic parameters</span></span>
* <span data-ttu-id="2a2cc-133">İçeri aktarılan ad alanları</span><span class="sxs-lookup"><span data-stu-id="2a2cc-133">Imported namespaces</span></span>
* <span data-ttu-id="2a2cc-134">Yolların</span><span class="sxs-lookup"><span data-stu-id="2a2cc-134">Routes</span></span>

<span data-ttu-id="2a2cc-135">Razor yönergeleri `@` karakteriyle başlar ve genellikle dosyanın başlangıcında yeni bir satırın başlangıcında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-135">Razor directives start with the `@` character and are typically used at the start of a new line at the start of the file.</span></span> <span data-ttu-id="2a2cc-136">Örneğin, `@namespace` yönerge bileşenin ad alanını tanımlar:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-136">For example, the `@namespace` directive defines the component's namespace:</span></span>

```razor
@namespace MyComponentNamespace
```

<span data-ttu-id="2a2cc-137">Aşağıdaki tabloda, Blazor içinde kullanılan çeşitli Razor yönergeleri ve varsa ASP.NET Web Forms eşdeğerleri özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-137">The following table summarizes the various Razor directives used in Blazor and their ASP.NET Web Forms equivalents, if they exist.</span></span>

|<span data-ttu-id="2a2cc-138">Yönergesi</span><span class="sxs-lookup"><span data-stu-id="2a2cc-138">Directive</span></span>    |<span data-ttu-id="2a2cc-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2a2cc-139">Description</span></span>|<span data-ttu-id="2a2cc-140">Örnek</span><span class="sxs-lookup"><span data-stu-id="2a2cc-140">Example</span></span>|<span data-ttu-id="2a2cc-141">Web Forms eşdeğeri</span><span class="sxs-lookup"><span data-stu-id="2a2cc-141">Web Forms equivalent</span></span>|
|-------------|-----------|-------|--------------------|
|`@attribute` |<span data-ttu-id="2a2cc-142">Bileşene bir sınıf düzeyi özniteliği ekler</span><span class="sxs-lookup"><span data-stu-id="2a2cc-142">Adds a class-level attribute to the component</span></span>|`@attribute [Authorize]`|<span data-ttu-id="2a2cc-143">Yok.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-143">None</span></span>|
|`@code`      |<span data-ttu-id="2a2cc-144">Bileşene sınıf üyeleri ekler</span><span class="sxs-lookup"><span data-stu-id="2a2cc-144">Adds class members to the component</span></span>|`@code { ... }`|`<script runat="server">...</script>`|
|`@implements`|<span data-ttu-id="2a2cc-145">Belirtilen arabirimi uygular</span><span class="sxs-lookup"><span data-stu-id="2a2cc-145">Implements the specified interface</span></span>|`@implements IDisposable`|<span data-ttu-id="2a2cc-146">Arka plan kodu kullan</span><span class="sxs-lookup"><span data-stu-id="2a2cc-146">Use code-behind</span></span>|
|`@inherits`  |<span data-ttu-id="2a2cc-147">Belirtilen taban sınıftan devralır</span><span class="sxs-lookup"><span data-stu-id="2a2cc-147">Inherits from the specified base class</span></span>|`@inherits MyComponentBase`|`<%@ Control Inherits="MyUserControlBase" %>`|
|`@inject`    |<span data-ttu-id="2a2cc-148">Bileşene bir hizmet çıkarır</span><span class="sxs-lookup"><span data-stu-id="2a2cc-148">Injects a service into the component</span></span>|`@inject IJSRuntime JS`|<span data-ttu-id="2a2cc-149">Yok.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-149">None</span></span>|
|`@layout`    |<span data-ttu-id="2a2cc-150">Bileşen için bir düzen bileşeni belirtir</span><span class="sxs-lookup"><span data-stu-id="2a2cc-150">Specifies a layout component for the component</span></span>|`@layout MainLayout`|`<%@ Page MasterPageFile="~/Site.Master" %>`|
|`@namespace` |<span data-ttu-id="2a2cc-151">Bileşen için ad alanını ayarlar</span><span class="sxs-lookup"><span data-stu-id="2a2cc-151">Sets the namespace for the component</span></span>|`@namespace MyNamespace`|<span data-ttu-id="2a2cc-152">Yok.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-152">None</span></span>|
|`@page`      |<span data-ttu-id="2a2cc-153">Bileşen için yolu belirtir</span><span class="sxs-lookup"><span data-stu-id="2a2cc-153">Specifies the route for the component</span></span>|`@page "/product/{id}"`|`<%@ Page %>`|
|`@typeparam` |<span data-ttu-id="2a2cc-154">Bileşen için genel bir tür parametresi belirtir</span><span class="sxs-lookup"><span data-stu-id="2a2cc-154">Specifies a generic type parameter for the component</span></span>|`@typeparam TItem`|<span data-ttu-id="2a2cc-155">Arka plan kodu kullan</span><span class="sxs-lookup"><span data-stu-id="2a2cc-155">Use code-behind</span></span>|
|`@using`     |<span data-ttu-id="2a2cc-156">Kapsama getirmek için bir ad alanı belirtir</span><span class="sxs-lookup"><span data-stu-id="2a2cc-156">Specifies a namespace to bring into scope</span></span>|`@using MyComponentNamespace`|<span data-ttu-id="2a2cc-157">*Web. config* 'de ad alanı Ekle</span><span class="sxs-lookup"><span data-stu-id="2a2cc-157">Add namespace in *web.config*</span></span>|

<span data-ttu-id="2a2cc-158">Razor bileşenleri Ayrıca, bileşenlerin nasıl derlendiğine (olay işleme, veri bağlama, bileşen & öğe başvuruları vb.) ilişkin çeşitli yönlerini denetlemek için öğeler üzerinde *yönerge özniteliklerinin* kapsamlı bir şekilde kullanılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-158">Razor components also make extensive use of *directive attributes* on elements to control various aspects of how components get compiled (event handling, data binding, component & element references, and so on).</span></span> <span data-ttu-id="2a2cc-159">Yönerge öznitelikleri All, parantez içindeki değerlerin isteğe bağlı olduğu ortak bir genel söz dizimini izler:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-159">Directive attributes all follow a common generic syntax where the values in parenthesis are optional:</span></span>

```razor
@directive(-suffix(:name))(="value")
```

<span data-ttu-id="2a2cc-160">Aşağıdaki tabloda, Blazor ' de kullanılan Razor yönergelerinin çeşitli öznitelikleri özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-160">The following table summarizes the various attributes for Razor directives used in Blazor.</span></span>

|<span data-ttu-id="2a2cc-161">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="2a2cc-161">Attribute</span></span>    |<span data-ttu-id="2a2cc-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2a2cc-162">Description</span></span>|<span data-ttu-id="2a2cc-163">Örnek</span><span class="sxs-lookup"><span data-stu-id="2a2cc-163">Example</span></span>|
|-------------|-----------|-------|
|`@attributes`|<span data-ttu-id="2a2cc-164">Özniteliklerin sözlüğünü işler</span><span class="sxs-lookup"><span data-stu-id="2a2cc-164">Renders a dictionary of attributes</span></span>|`<input @attributes="ExtraAttributes" />`|
|`@bind`      |<span data-ttu-id="2a2cc-165">İki yönlü veri bağlama oluşturur</span><span class="sxs-lookup"><span data-stu-id="2a2cc-165">Creates a two-way data binding</span></span>    |`<input @bind="username" @bind:event="oninput" />`|
|`@on{event}` |<span data-ttu-id="2a2cc-166">Belirtilen olay için bir olay işleyicisi ekler</span><span class="sxs-lookup"><span data-stu-id="2a2cc-166">Adds an event handler for the specified event</span></span>|`<button @onclick="IncrementCount">Click me!</button>`|
|`@key`       |<span data-ttu-id="2a2cc-167">Bir koleksiyondaki öğeleri korumak için dağıtılmış algoritma tarafından kullanılacak bir anahtar belirtir</span><span class="sxs-lookup"><span data-stu-id="2a2cc-167">Specifies a key to be used by the diffing algorithm for preserving elements in a collection</span></span>|`<DetailsEditor @key="person" Details="person.Details" />`|
|`@ref`       |<span data-ttu-id="2a2cc-168">Bileşene veya HTML öğesine bir başvuru yakalar</span><span class="sxs-lookup"><span data-stu-id="2a2cc-168">Captures a reference to the component or HTML element</span></span>|`<MyDialog @ref="myDialog" />`|

<span data-ttu-id="2a2cc-169">Blazor (`@onclick`, `@bind`, `@ref`vb.) tarafından kullanılan çeşitli yönerge öznitelikleri aşağıdaki bölümlerde ve sonraki bölümlerde ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-169">The various directive attributes used by Blazor (`@onclick`, `@bind`, `@ref`, and so on) are covered in the sections below and later chapters.</span></span>

<span data-ttu-id="2a2cc-170">*. Aspx* ve *. ascx* dosyalarında kullanılan sözdizimlerinin birçoğu Razor 'de paralel sözdizimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-170">Many of the syntaxes used in *.aspx* and *.ascx* files have parallel syntaxes in Razor.</span></span> <span data-ttu-id="2a2cc-171">ASP.NET Web Forms ve Razor için sözdizimlerinin basit bir karşılaştırması aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-171">Below is a simple comparison of the syntaxes for ASP.NET Web Forms and Razor.</span></span>

|<span data-ttu-id="2a2cc-172">Özellik</span><span class="sxs-lookup"><span data-stu-id="2a2cc-172">Feature</span></span>                      |<span data-ttu-id="2a2cc-173">Web Forms</span><span class="sxs-lookup"><span data-stu-id="2a2cc-173">Web Forms</span></span>           |<span data-ttu-id="2a2cc-174">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2a2cc-174">Syntax</span></span>               |<span data-ttu-id="2a2cc-175">Razor</span><span class="sxs-lookup"><span data-stu-id="2a2cc-175">Razor</span></span>         |<span data-ttu-id="2a2cc-176">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2a2cc-176">Syntax</span></span> |
|-----------------------------|--------------------|---------------------|--------------|-------|
|<span data-ttu-id="2a2cc-177">Yönergeler</span><span class="sxs-lookup"><span data-stu-id="2a2cc-177">Directives</span></span>                   |`<%@ [directive] %>`|`<%@ Page %>`        |`@[directive]`|`@page`|
|<span data-ttu-id="2a2cc-178">Kod blokları</span><span class="sxs-lookup"><span data-stu-id="2a2cc-178">Code blocks</span></span>                  |`<% %>`             |`<% int x = 123; %>` |`@{ }`        |`@{ int x = 123; }`|
|<span data-ttu-id="2a2cc-179">İfadeler</span><span class="sxs-lookup"><span data-stu-id="2a2cc-179">Expressions</span></span><br><span data-ttu-id="2a2cc-180">(HTML kodlu)</span><span class="sxs-lookup"><span data-stu-id="2a2cc-180">(HTML-encoded)</span></span>|`<%: %>`            |`<%:DateTime.Now %>` |<span data-ttu-id="2a2cc-181">İndirgen`@`</span><span class="sxs-lookup"><span data-stu-id="2a2cc-181">Implicit: `@`</span></span><br><span data-ttu-id="2a2cc-182">Anlaşılır`@()`</span><span class="sxs-lookup"><span data-stu-id="2a2cc-182">Explicit: `@()`</span></span>|`@DateTime.Now`<br>`@(DateTime.Now)`|
|<span data-ttu-id="2a2cc-183">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="2a2cc-183">Comments</span></span>                     |`<%-- --%>`         |`<%-- Commented --%>`|`@* *@`       |`@* Commented *@`|
|<span data-ttu-id="2a2cc-184">Veri bağlama</span><span class="sxs-lookup"><span data-stu-id="2a2cc-184">Data binding</span></span>                 |`<%# %>`            |`<%# Bind("Name") %>`|`@bind`       |`<input @bind="username" />`|

<span data-ttu-id="2a2cc-185">Razor bileşen sınıfına üye eklemek için `@code` yönergesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-185">To add members to the Razor component class, use the `@code` directive.</span></span> <span data-ttu-id="2a2cc-186">Bu teknik, bir `<script runat="server">...</script>` ASP.NET Web Forms Kullanıcı denetiminde veya sayfasında blok kullanmaya benzer.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-186">This technique is similar to using a `<script runat="server">...</script>` block in an ASP.NET Web Forms user control or page.</span></span>

```razor
@code {
    int count = 0;

    void IncrementCount()
    {
        count++;
    }
}
```

<span data-ttu-id="2a2cc-187">Razor temel aldığı için C#, bir C# proje ( *. csproj*) içinden derlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-187">Because Razor is based on C#, it must be compiled from within a C# project (*.csproj*).</span></span> <span data-ttu-id="2a2cc-188">VB projesinden *. Razor* dosyalarını derlenemez ( *. vbproj*).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-188">You can't compile *.razor* files from a VB project (*.vbproj*).</span></span> <span data-ttu-id="2a2cc-189">Blazor projenizden VB projelerine yine de başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-189">You can still reference VB projects from your Blazor project.</span></span> <span data-ttu-id="2a2cc-190">Tersi de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-190">The opposite is true too.</span></span>

<span data-ttu-id="2a2cc-191">Tam Razor söz dizimi başvuru için bkz. [ASP.NET Core için Razor söz dizimi başvurusu](/aspnet/core/mvc/views/razor).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-191">For a full Razor syntax reference, see [Razor syntax reference for ASP.NET Core](/aspnet/core/mvc/views/razor).</span></span>

## <a name="use-components"></a><span data-ttu-id="2a2cc-192">Bileşenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="2a2cc-192">Use components</span></span>

<span data-ttu-id="2a2cc-193">Normal HTML 'den başlayarak, bileşenler kendi işleme mantığının bir parçası olarak diğer bileşenleri de kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-193">Aside from normal HTML, components can also use other components as part of their rendering logic.</span></span> <span data-ttu-id="2a2cc-194">Razor 'de bir bileşen kullanmanın sözdizimi, bir ASP.NET Web Forms uygulamasında kullanıcı denetimi kullanmaya benzerdir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-194">The syntax for using a component in Razor is similar to using a user control in an ASP.NET Web Forms app.</span></span> <span data-ttu-id="2a2cc-195">Bileşenler, bileşenin tür adıyla eşleşen bir öğe etiketi kullanılarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-195">Components are specified using an element tag that matches the type name of the component.</span></span> <span data-ttu-id="2a2cc-196">Örneğin, aşağıdaki gibi bir `Counter` bileşen ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-196">For example, you can add a `Counter` component like this:</span></span>

```razor
<Counter />
```

<span data-ttu-id="2a2cc-197">ASP.NET Web Forms aksine, Blazor içindeki bileşenler:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-197">Unlike ASP.NET Web Forms, components in Blazor:</span></span>

* <span data-ttu-id="2a2cc-198">Öğe öneki kullanmayın (örneğin, `asp:`).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-198">Don't use an element prefix (for example, `asp:`).</span></span>
* <span data-ttu-id="2a2cc-199">Sayfada veya *Web. config*dosyasında kayıt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-199">Don't require registration on the page or in the *web.config*.</span></span>

<span data-ttu-id="2a2cc-200">.NET türlerine benzer Razor bileşenleri düşünün çünkü bu, tam olarak bir şeydir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-200">Think of Razor components like you would .NET types, because that's exactly what they are.</span></span> <span data-ttu-id="2a2cc-201">Bileşeni içeren derlemeye başvuruluyorsa, bileşen kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-201">If the assembly containing the component is referenced, then the component is available for use.</span></span> <span data-ttu-id="2a2cc-202">Bileşenin ad alanını kapsama getirmek için `@using` yönergesini uygulayın:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-202">To bring the component's namespace into scope, apply the `@using` directive:</span></span>

```razor
@using MyComponentLib

<Counter />
```

<span data-ttu-id="2a2cc-203">Varsayılan Blazor projelerinde görüldüğü gibi, yönergeleri bir *_ımports. Razor* dosyasına `@using` koymak ve bu sayede, aynı dizinde ve alt dizinlerde bulunan tüm *. Razor* dosyalarına aktarılmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-203">As seen in the default Blazor projects, it's common to put `@using` directives into a *_Imports.razor* file so that they're imported into all *.razor* files in the same directory and in child directories.</span></span>

<span data-ttu-id="2a2cc-204">Bir bileşenin ad alanı kapsamda değilse, içinde C#olduğu gibi tam tür adını kullanarak bir bileşen belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-204">If the namespace for a component isn't in scope, you can specify a component using its full type name, as you can in C#:</span></span>

```razor
<MyComponentLib.Counter />
```

## <a name="component-parameters"></a><span data-ttu-id="2a2cc-205">Bileşen parametreleri</span><span class="sxs-lookup"><span data-stu-id="2a2cc-205">Component parameters</span></span>

<span data-ttu-id="2a2cc-206">ASP.NET Web Forms ' de, genel özellikleri kullanarak parametreleri ve verileri denetimlere akışı sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-206">In ASP.NET Web Forms, you can flow parameters and data to controls using public properties.</span></span> <span data-ttu-id="2a2cc-207">Bu özellikler, öznitelikler kullanılarak biçimlendirme içinde ayarlanabilir veya doğrudan kodda ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-207">These properties can be set in markup using attributes or set directly in code.</span></span> <span data-ttu-id="2a2cc-208">Blazor bileşenleri benzer bir şekilde çalışır, ancak bileşen özellikleri de bileşen parametreleri olarak kabul edilecek `[Parameter]` özniteliğiyle işaretlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-208">Blazor components work in a similar fashion, although the component properties must also be marked with the `[Parameter]` attribute to be considered component parameters.</span></span>

<span data-ttu-id="2a2cc-209">Aşağıdaki `Counter` bileşen, düğmenin tıklandığı her seferinde `IncrementAmount` artırılması `Counter` gereken miktarı belirtmek için kullanılan adlı bir bileşen parametresini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-209">The following `Counter` component defines a component parameter called `IncrementAmount` that can be used to specify the amount that the `Counter` should be incremented each time the button is clicked.</span></span>

```razor
<h1>Counter</h1>

<p>Current count: @currentCount</p>

<button class="btn btn-primary" @onclick="IncrementCount">Click me</button>

@code {
    int currentCount = 0;

    [Parameter]
    public int IncrementAmount { get; set; } = 1;

    void IncrementCount()
    {
        currentCount+=IncrementAmount;
    }
}
```

<span data-ttu-id="2a2cc-210">Blazor içinde bir bileşen parametresi belirtmek için, ASP.NET Web Forms içinde olduğu gibi bir özniteliği kullanın:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-210">To specify a component parameter in Blazor, use an attribute as you would in ASP.NET Web Forms:</span></span>

```razor
<Counter IncrementAmount="10" />
```

## <a name="event-handlers"></a><span data-ttu-id="2a2cc-211">Olay işleyicileri</span><span class="sxs-lookup"><span data-stu-id="2a2cc-211">Event handlers</span></span>

<span data-ttu-id="2a2cc-212">Hem ASP.NET Web Forms hem de Blazor Kullanıcı arabirimi olaylarını işlemek için bir olay tabanlı programlama modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-212">Both ASP.NET Web Forms and Blazor provide an event-based programming model for handling UI events.</span></span> <span data-ttu-id="2a2cc-213">Bu tür olaylara örnek olarak düğme tıklamaları ve metin girişi dahildir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-213">Examples of such events include button clicks and text input.</span></span> <span data-ttu-id="2a2cc-214">ASP.NET Web Forms ' de, DOM tarafından sunulan UI olaylarını işlemek için HTML sunucu denetimlerini kullanırsınız veya Web sunucusu denetimleri tarafından sunulan olayları işleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-214">In ASP.NET Web Forms, you use HTML server controls to handle UI events exposed by the DOM, or you can handle events exposed by web server controls.</span></span> <span data-ttu-id="2a2cc-215">Olaylar, arka arkaya geri dönüş istekleri aracılığıyla sunucuda ortaya çıkmış.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-215">The events are surfaced on the server through form post-back requests.</span></span> <span data-ttu-id="2a2cc-216">Aşağıdaki Web Forms düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-216">Consider the following Web Forms button click example:</span></span>

<span data-ttu-id="2a2cc-217">*Counter. ascx*</span><span class="sxs-lookup"><span data-stu-id="2a2cc-217">*Counter.ascx*</span></span>

```aspx-csharp
<asp:Button ID="ClickMeButton" runat="server" Text="Click me!" OnClick="ClickMeButton_Click" />
```

<span data-ttu-id="2a2cc-218">*Counter.ascx.cs*</span><span class="sxs-lookup"><span data-stu-id="2a2cc-218">*Counter.ascx.cs*</span></span>

```csharp
public partial class Counter : System.Web.UI.UserControl
{
    protected void ClickMeButton_Click(object sender, EventArgs e)
    {
        Console.WriteLine("The button was clicked!");
    }
}
```

<span data-ttu-id="2a2cc-219">Blazor ' de, DOM UI olayları için işleyicileri doğrudan formun `@on{event}`yönerge özniteliklerini kullanarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-219">In Blazor, you can register handlers for DOM UI events directly using directive attributes of the form `@on{event}`.</span></span> <span data-ttu-id="2a2cc-220">`{event}` Yer tutucu, olayın adını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-220">The `{event}` placeholder represents the name of the event.</span></span> <span data-ttu-id="2a2cc-221">Örneğin, aşağıdaki gibi düğme tıklamalarını dinleyeseçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-221">For example, you can listen for button clicks like this:</span></span>

```razor
<button @onclick="OnClick">Click me!</button>

@code {
    void OnClick()
    {
        Console.WriteLine("The button was clicked!);
    }
}
```

<span data-ttu-id="2a2cc-222">Olay işleyicileri, olay hakkında daha fazla bilgi sağlamak için isteğe bağlı, olaya özgü bir bağımsız değişkeni kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-222">Event handlers can accept an optional, event-specific argument to provide more information about the event.</span></span> <span data-ttu-id="2a2cc-223">Örneğin, fare olayları bir `MouseEventArgs` bağımsız değişken alabilir, ancak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-223">For example, mouse events can take a `MouseEventArgs` argument, but it isn't required.</span></span>

```razor
<button @onclick="OnClick">Click me!</button>

@code {
    void OnClick(MouseEventArgs e) 
    {
        Console.WriteLine($"Mouse clicked at {e.ScreenX}, {e.ScreenY}.");
    }
}
```

<span data-ttu-id="2a2cc-224">Bir olay işleyicisi için bir yöntem grubuna başvurmak yerine bir lambda ifadesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-224">Instead of referring to a method group for an event handler, you can use a lambda expression.</span></span> <span data-ttu-id="2a2cc-225">Lambda ifadesi, diğer kapsam içi değerleri kapatmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-225">A lambda expression allows you to close over other in-scope values.</span></span>

```razor
@foreach (var buttonLabel in buttonLabels)
{
    <button @onclick="() => Console.WriteLine($"The {buttonLabel} button was clicked!")">@buttonLabel</button>
}
```

<span data-ttu-id="2a2cc-226">Olay işleyicileri, zaman uyumlu veya zaman uyumsuz olarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-226">Event handlers can execute synchronously or asynchronously.</span></span> <span data-ttu-id="2a2cc-227">Örneğin, aşağıdaki `OnClick` olay işleyicisi zaman uyumsuz olarak yürütülür:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-227">For example, the following `OnClick` event handler executes asynchronously:</span></span>

```razor
<button @onclick="OnClick">Click me!</button>

@code {
    async Task OnClick() 
    {
        var result = await Http.GetAsync("api/values");
    }
}
```

<span data-ttu-id="2a2cc-228">Bir olay işlendikten sonra bileşen, bileşen durumu değişikliklerini hesaba göre işlenir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-228">After an event is handled, the component is rendered to account for any component state changes.</span></span> <span data-ttu-id="2a2cc-229">Zaman uyumsuz olay işleyicileriyle, bileşen işleyici yürütme tamamlandıktan hemen sonra işlenir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-229">With asynchronous event handlers, the component is rendered immediately after the handler execution completes.</span></span> <span data-ttu-id="2a2cc-230">Bileşen, zaman uyumsuz `Task` tamamlandıktan sonra yeniden işlenir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-230">The component is rendered *again* after the asynchronous `Task` completes.</span></span> <span data-ttu-id="2a2cc-231">Bu zaman uyumsuz yürütme modu, zaman uyumsuz `Task` olarak devam ederken, bazı uygun Kullanıcı arabirimini işleme fırsatı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-231">This asynchronous execution mode provides an opportunity to render some appropriate UI while the asynchronous `Task` is still in progress.</span></span>

```razor
<button @onclick="Get message">Get message</button>

@if (showMessage)
{
    @if (message == null)
    {
        <p><em>Loading...</em></p>
    }
    else
    {
        <p>The message is: @message</p>
    }
}

@code 
{
    bool showMessage = false;
    string message;

    public async Task ShowMessage()
    {
        showMessage = true;
        message = await MessageService.GetMessageAsync();
    }
}
```

<span data-ttu-id="2a2cc-232">Bileşenler, türünde `EventCallback<TValue>`bir bileşen parametresi tanımlayarak kendi olaylarını da tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-232">Components can also define their own events by defining a component parameter of type `EventCallback<TValue>`.</span></span> <span data-ttu-id="2a2cc-233">Olay geri çağırmaları, DOM UI olay işleyicilerinin tüm çeşitlemelerini destekler: isteğe bağlı bağımsız değişkenler, zaman uyumlu veya zaman uyumsuz, yöntem grupları veya lambda ifadeleri.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-233">Event callbacks support all the variations of DOM UI event handlers: optional arguments, synchronous or asynchronous, method groups, or lambda expressions.</span></span>

```razor
<button class="btn btn-primary" @onclick="OnClick">Click me!</button>

@code {
    [Parameter]
    public EventCallback<MouseEventArgs> OnClick { get; set; }
}
```

## <a name="data-binding"></a><span data-ttu-id="2a2cc-234">Veri bağlama</span><span class="sxs-lookup"><span data-stu-id="2a2cc-234">Data binding</span></span>

<span data-ttu-id="2a2cc-235">Blazor, bir UI bileşeninden bileşen durumuna veri bağlamak için basit bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-235">Blazor provides a simple mechanism to bind data from a UI component to the component's state.</span></span> <span data-ttu-id="2a2cc-236">Bu yaklaşım, veri kaynaklarından kullanıcı arabirimi denetimlerine veri bağlamak için ASP.NET Web Forms özelliklerinden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-236">This approach differs from the features in ASP.NET Web Forms for binding data from data sources to UI controls.</span></span> <span data-ttu-id="2a2cc-237">[Verilerle ilgilenme](data.md) bölümünde farklı veri kaynaklarından veri işlemeyi ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-237">We'll cover handling data from different data sources in the [Dealing with data](data.md) section.</span></span>

<span data-ttu-id="2a2cc-238">Bir UI bileşeninden bileşen durumuna iki yönlü bir veri bağlama oluşturmak için, `@bind` Directive özniteliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-238">To create a two-way data binding from a UI component to the component's state, use the `@bind` directive attribute.</span></span> <span data-ttu-id="2a2cc-239">Aşağıdaki örnekte, onay kutusunun değeri `isChecked` alana bağlanır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-239">In the following example, the value of the check box is bound to the `isChecked` field.</span></span>

```razor
<input type="checkbox" @bind="isChecked" />

@code {
    bool isChecked;
}
```

<span data-ttu-id="2a2cc-240">Bileşen işlendiğinde onay kutusunun değeri `isChecked` alanın değerine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-240">When the component is rendered, the value of the checkbox is set to the value of the `isChecked` field.</span></span> <span data-ttu-id="2a2cc-241">Kullanıcı onay kutusuna geçiş yaparken, `onchange` olay tetiklenir `isChecked` ve alan yeni değere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-241">When the user toggles the checkbox, the `onchange` event is fired and the `isChecked` field is set to the new value.</span></span> <span data-ttu-id="2a2cc-242">Bu `@bind` örnekte sözdizimi aşağıdaki biçimlendirmeye eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-242">The `@bind` syntax in this case is equivalent to the following markup:</span></span>

```razor
<input value="@isChecked" @onchange="(UIChangeEventArgs e) => isChecked = e.Value" />
```

<span data-ttu-id="2a2cc-243">Bağlama için kullanılan olayı değiştirmek için `@bind:event` özniteliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-243">To change the event used for the bind, use the `@bind:event` attribute.</span></span>

```razor
<input @bind="text" @bind:event="oninput" />
<p>@text</p>

@code {
    string text;
}
```

<span data-ttu-id="2a2cc-244">Bileşenler, parametrelerine veri bağlamayı da destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-244">Components can also support data binding to their parameters.</span></span> <span data-ttu-id="2a2cc-245">Veri bağlama için, bağlanabilir parametreyle aynı ada sahip bir olay geri çağırma parametresi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-245">To data bind, define an event callback parameter with the same name as the bindable parameter.</span></span> <span data-ttu-id="2a2cc-246">"Değiştirilen" sonek ada eklenir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-246">The "Changed" suffix is added to the name.</span></span>

<span data-ttu-id="2a2cc-247">*PasswordBox. Razor*</span><span class="sxs-lookup"><span data-stu-id="2a2cc-247">*PasswordBox.razor*</span></span>

```razor
Password: <input 
    value="@Password" 
    @oninput="OnPasswordChanged" 
    type="@(showPassword ? "text" : "password")" />

<label><input type="checkbox" @bind="showPassword" />Show password</label>

@code {
    private bool showPassword;

    [Parameter]
    public string Password { get; set; }

    [Parameter]
    public EventCallback<string> PasswordChanged { get; set; }

    private Task OnPasswordChanged(ChangeEventArgs e)
    {
        Password = e.Value.ToString();
        return PasswordChanged.InvokeAsync(Password);
    }
}
```

<span data-ttu-id="2a2cc-248">Bir veri bağlamasını temel bir kullanıcı arabirimi öğesine zincirlemek için değeri ayarlayın ve olayı, `@bind` özniteliğini kullanmak yerine doğrudan UI öğesi üzerinde işleyin.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-248">To chain a data binding to an underlying UI element, set the value and handle the event directly on the UI element instead of using the `@bind` attribute.</span></span>

<span data-ttu-id="2a2cc-249">Bir bileşen parametresine bağlamak için, bağlamak istediğiniz parametreyi `@bind-{Parameter}` belirtmek üzere bir özniteliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-249">To bind to a component parameter, use a `@bind-{Parameter}` attribute to specify the parameter to which you want to bind.</span></span>

```razor
<PasswordBox @bind-Password="password" />

@code {
    string password;
}
```

## <a name="state-changes"></a><span data-ttu-id="2a2cc-250">Durum değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="2a2cc-250">State changes</span></span>

<span data-ttu-id="2a2cc-251">Bileşenin durumu normal bir kullanıcı arabirimi olayının veya olay geri çağrısının dışında değiştiyse, bileşen yeniden oluşturulması gerektiğini el ile işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-251">If the component's state has changed outside of a normal UI event or event callback, then the component must manually signal that it needs to be rendered again.</span></span> <span data-ttu-id="2a2cc-252">Bir bileşenin durumunun değiştiğini bildirmek için, bileşeninde `StateHasChanged` yöntemi çağırın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-252">To signal that a component's state has changed, call the `StateHasChanged` method on the component.</span></span>

<span data-ttu-id="2a2cc-253">Aşağıdaki örnekte, bir bileşeni, uygulamanın diğer bölümleri tarafından güncelleştirilebilen bir `AppState` hizmetten bir ileti görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-253">In the example below, a component displays a message from an `AppState` service that can be updated by other parts of the app.</span></span> <span data-ttu-id="2a2cc-254">Bileşen, ileti her `StateHasChanged` güncelleştirildiğinde bileşenin işlenmesi `AppState.OnChange` için yöntemini olaya kaydeder.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-254">The component registers its `StateHasChanged` method with the `AppState.OnChange` event so that the component is rendered whenever the message gets updated.</span></span>

```csharp
public class AppState
{
    public string Message { get; }

    // Lets components receive change notifications
    public event Action OnChange;

    public void UpdateMessage(string message)
    {
        shortlist.Add(itinerary);
        NotifyStateChanged();
    }

    private void NotifyStateChanged() => OnChange?.Invoke();
}
```

```razor
@inject AppState AppState

<p>App message: @AppState.Message</p>

@code {
    protected override void OnInitialized()
    {
        AppState.OnChange += StateHasChanged
    }
}
```

## <a name="component-lifecycle"></a><span data-ttu-id="2a2cc-255">Bileşen yaşam döngüsü</span><span class="sxs-lookup"><span data-stu-id="2a2cc-255">Component lifecycle</span></span>

<span data-ttu-id="2a2cc-256">ASP.NET Web Forms Framework, modüller, sayfalar ve denetimler için iyi tanımlanmış yaşam döngüsü yöntemlerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-256">The ASP.NET Web Forms framework has well-defined lifecycle methods for modules, pages, and controls.</span></span> <span data-ttu-id="2a2cc-257">Örneğin, aşağıdaki denetim `Init`, `Load`, ve `UnLoad` yaşam döngüsü olayları için olay işleyicilerini uygular:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-257">For example, the following control implements event handlers for the `Init`, `Load`, and `UnLoad` lifecycle events:</span></span>

<span data-ttu-id="2a2cc-258">*Counter.ascx.cs*</span><span class="sxs-lookup"><span data-stu-id="2a2cc-258">*Counter.ascx.cs*</span></span>

```csharp
public partial class Counter : System.Web.UI.UserControl
{
    protected void Page_Init(object sender, EventArgs e) { ... }
    protected void Page_Load(object sender, EventArgs e) { ... }
    protected void Page_UnLoad(object sender, EventArgs e) { ... }
}
```

<span data-ttu-id="2a2cc-259">Blazor bileşenlerinde de iyi tanımlanmış bir yaşam döngüsü vardır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-259">Blazor components also have a well-defined lifecycle.</span></span> <span data-ttu-id="2a2cc-260">Bileşenin yaşam döngüsü, bileşen durumunu başlatmak ve Gelişmiş bileşen davranışları uygulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-260">A component's lifecycle can be used to initialize component state and implement advanced component behaviors.</span></span> 

<span data-ttu-id="2a2cc-261">Tüm Blazor bileşen yaşam döngüsü yöntemlerinin hem zaman uyumlu hem de zaman uyumsuz sürümleri vardır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-261">All of Blazor's component lifecycle methods have both synchronous and asynchronous versions.</span></span> <span data-ttu-id="2a2cc-262">Bileşen işleme zaman uyumludur.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-262">Component rendering is synchronous.</span></span> <span data-ttu-id="2a2cc-263">Zaman uyumsuz mantığı bileşen işlemenin bir parçası olarak çalıştıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-263">You can't run asynchronous logic as part of the component rendering.</span></span> <span data-ttu-id="2a2cc-264">Tüm zaman uyumsuz mantığın bir `async` yaşam döngüsü yönteminin parçası olarak yürütülmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-264">All asynchronous logic must execute as part of an `async` lifecycle method.</span></span>

### <a name="oninitialized"></a><span data-ttu-id="2a2cc-265">OnInitialized</span><span class="sxs-lookup"><span data-stu-id="2a2cc-265">OnInitialized</span></span>

<span data-ttu-id="2a2cc-266">`OnInitialized` Ve`OnInitializedAsync` yöntemleri, bileşeni başlatmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-266">The `OnInitialized` and `OnInitializedAsync` methods are used to initialize the component.</span></span> <span data-ttu-id="2a2cc-267">Bir bileşen genellikle ilk işlendikten sonra başlatılır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-267">A component is typically initialized after it's first rendered.</span></span> <span data-ttu-id="2a2cc-268">Bir bileşen başlatıldıktan sonra, en sonunda atılmadan önce birden çok kez oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-268">After a component is initialized, it may be rendered multiple times before it's eventually disposed.</span></span> <span data-ttu-id="2a2cc-269">Yöntemi, ASP.NET Web Forms sayfalarındaki ve `Page_Load` denetimlerindeki olaya benzerdir. `OnInitialized`</span><span class="sxs-lookup"><span data-stu-id="2a2cc-269">The `OnInitialized` method is similar to the `Page_Load` event in ASP.NET Web Forms pages and controls.</span></span>

```csharp
protected override void OnInitialized() { ... }
protected override async Task OnInitializedAsync() { await ... }
```

### <a name="onparametersset"></a><span data-ttu-id="2a2cc-270">OnParametersSet</span><span class="sxs-lookup"><span data-stu-id="2a2cc-270">OnParametersSet</span></span>

<span data-ttu-id="2a2cc-271">`OnParametersSet` Ve`OnParametersSetAsync` yöntemleri bir bileşen üst öğeden parametreleri aldığında ve değer özelliklerine atandığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-271">The `OnParametersSet` and `OnParametersSetAsync` methods are called when a component has received parameters from its parent and the value are assigned to properties.</span></span> <span data-ttu-id="2a2cc-272">Bu yöntemler bileşen başlatıldıktan sonra ve *bileşen her işlendiğinde*yürütülür.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-272">These methods are executed after component initialization and *each time the component is rendered*.</span></span>

```csharp
protected override void OnParametersSet() { ... }
protected override async Task OnParametersSetAsync() { await ... }
```

### <a name="onafterrender"></a><span data-ttu-id="2a2cc-273">OnAfterRender</span><span class="sxs-lookup"><span data-stu-id="2a2cc-273">OnAfterRender</span></span>

<span data-ttu-id="2a2cc-274">`OnAfterRender` Ve`OnAfterRenderAsync` yöntemleri bir bileşen işlemeyi tamamladıktan sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-274">The `OnAfterRender` and `OnAfterRenderAsync` methods are called after a component has finished rendering.</span></span> <span data-ttu-id="2a2cc-275">Öğe ve bileşen başvuruları bu noktada doldurulur (aşağıdaki kavramlarda daha fazla).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-275">Element and component references are populated at this point (more on these concepts below).</span></span> <span data-ttu-id="2a2cc-276">Bu noktada tarayıcıyla etkileşim etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-276">Interactivity with the browser is enabled at this point.</span></span> <span data-ttu-id="2a2cc-277">DOM ve JavaScript yürütme etkileşimleri güvenle yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-277">Interactions with the DOM and JavaScript execution can safely take place.</span></span> 

```csharp
protected override void OnAfterRender(bool firstRender)
{
    if (firstRender)
    {
        ...
    }
}
protected override async Task OnAfterRenderAsync(bool firstRender)
{
    if (firstRender)
    {
        await ...
    }
}
```

<span data-ttu-id="2a2cc-278">`OnAfterRender`ve `OnAfterRenderAsync` *sunucuda prerendering çağrıldığında çağrılmaz*.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-278">`OnAfterRender` and `OnAfterRenderAsync` *aren't called when prerendering on the server*.</span></span>

<span data-ttu-id="2a2cc-279">Parametre, bileşen ilk kez işlendiğinde, aksi durumda değeri ' dir `false`. `firstRender` `true`</span><span class="sxs-lookup"><span data-stu-id="2a2cc-279">The `firstRender` parameter is `true` the first time the component is rendered; otherwise, its value is `false`.</span></span>

### <a name="idisposable"></a><span data-ttu-id="2a2cc-280">IDisposable</span><span class="sxs-lookup"><span data-stu-id="2a2cc-280">IDisposable</span></span>

<span data-ttu-id="2a2cc-281">Blazor bileşenleri `IDisposable` , bileşen kullanıcı arabiriminden kaldırıldığında kaynakların atılmaya uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-281">Blazor components can implement `IDisposable` to dispose of resources when the component is removed from the UI.</span></span> <span data-ttu-id="2a2cc-282">Bir Razor bileşeni `@implements` yönergesini kullanarak `IDispose` uygulayabilir:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-282">A Razor component can implement `IDispose` by using the `@implements` directive:</span></span>

```razor
@using System
@implements IDisposable

...

@code {
    public void Dispose()
    {
        ...
    }
}
```

## <a name="capture-component-references"></a><span data-ttu-id="2a2cc-283">Bileşen başvurularını yakala</span><span class="sxs-lookup"><span data-stu-id="2a2cc-283">Capture component references</span></span>

<span data-ttu-id="2a2cc-284">ASP.NET Web Forms ' de, bir denetim örneğini kendi KIMLIĞINE başvurarak doğrudan kodda işlemek yaygındır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-284">In ASP.NET Web Forms, it's common to manipulate a control instance directly in code by referring to its ID.</span></span> <span data-ttu-id="2a2cc-285">Blazor ' de, çok daha az yaygın olsa da bir bileşeni bir başvuruyu yakalamak ve işlemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-285">In Blazor, it's also possible to capture and manipulate a reference to a component, although it's much less common.</span></span>

<span data-ttu-id="2a2cc-286">Blazor içinde bir bileşen başvurusu yakalamak için `@ref` Directive özniteliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-286">To capture a component reference in Blazor, use the `@ref` directive attribute.</span></span> <span data-ttu-id="2a2cc-287">Özniteliğin değeri, başvurulan bileşenle aynı türde ayarlanabilir bir alanın adıyla eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-287">The value of the attribute should match the name of a settable field with the same type as the referenced component.</span></span>

```razor
<MyLoginDialog @ref="loginDialog" ... />

@code {
    MyLoginDialog loginDialog;

    void OnSomething()
    {
        loginDialog.Show();
    }
}
```

<span data-ttu-id="2a2cc-288">Üst bileşen işlendiğinde, alanı alt bileşen örneğiyle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-288">When the parent component is rendered, the field is populated with the child component instance.</span></span> <span data-ttu-id="2a2cc-289">Daha sonra bileşen örneği üzerinde yöntemleri çağırabilir veya başka şekilde düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-289">You can then call methods on, or otherwise manipulate, the component instance.</span></span>

<span data-ttu-id="2a2cc-290">Bileşen başvurularını kullanarak bileşen durumunu doğrudan işlemek önerilmez.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-290">Manipulating component state directly using component references isn't recommended.</span></span> <span data-ttu-id="2a2cc-291">Bunun yapılması bileşenin doğru saatlerde otomatik olarak işlenmesini önler.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-291">Doing so prevents the component from being rendered automatically at the correct times.</span></span>

## <a name="capture-element-references"></a><span data-ttu-id="2a2cc-292">Öğe başvurularını yakala</span><span class="sxs-lookup"><span data-stu-id="2a2cc-292">Capture element references</span></span>

<span data-ttu-id="2a2cc-293">Blazor bileşenleri, bir öğeye başvuruları yakalayabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-293">Blazor components can capture references to an element.</span></span> <span data-ttu-id="2a2cc-294">ASP.NET Web Forms içindeki HTML sunucu denetimlerinden farklı olarak, Blazor içindeki bir öğe başvurusunu kullanarak DOM 'ı doğrudan düzenleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-294">Unlike HTML server controls in ASP.NET Web Forms, you can't manipulate the DOM directly using an element reference in Blazor.</span></span> <span data-ttu-id="2a2cc-295">Blazor, DOM dağıtma algoritmasını kullanarak sizin için çoğu DOM etkileşimini işler.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-295">Blazor handles most DOM interactions for you using its DOM diffing algorithm.</span></span> <span data-ttu-id="2a2cc-296">Blazor içindeki yakalanan öğe başvuruları donuk.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-296">Captured element references in Blazor are opaque.</span></span> <span data-ttu-id="2a2cc-297">Ancak, JavaScript birlikte çalışma çağrısında belirli bir öğe başvurusunu geçirmek için kullanılırlar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-297">However, they're used to pass a specific element reference in a JavaScript interop call.</span></span> <span data-ttu-id="2a2cc-298">JavaScript birlikte çalışma hakkında daha fazla bilgi için bkz. [ASP.NET Core Blazor JavaScript Interop](/aspnet/core/blazor/javascript-interop).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-298">For more information about JavaScript interop, see [ASP.NET Core Blazor JavaScript interop](/aspnet/core/blazor/javascript-interop).</span></span>

## <a name="templated-components"></a><span data-ttu-id="2a2cc-299">Şablonlu bileşenler</span><span class="sxs-lookup"><span data-stu-id="2a2cc-299">Templated components</span></span>

<span data-ttu-id="2a2cc-300">ASP.NET Web Forms içinde *şablonlu denetimler*oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-300">In ASP.NET Web Forms, you can create *templated controls*.</span></span> <span data-ttu-id="2a2cc-301">Şablonlu denetimler, geliştiricinin bir kapsayıcı denetimini işlemek için kullanılan HTML 'nin bir bölümünü belirtmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-301">Templated controls enable the developer to specify a portion of the HTML used to render a container control.</span></span> <span data-ttu-id="2a2cc-302">Şablonlu sunucu denetimleri oluşturma mekanizması karmaşıktır, ancak kullanıcı tarafından özelleştirilebilir bir şekilde veri işlemeye yönelik güçlü senaryolar sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-302">The mechanics of building templated server controls are complex, but they enable powerful scenarios for rendering data in a user customizable way.</span></span> <span data-ttu-id="2a2cc-303">Şablonlu denetimlerin örnekleri ve `Repeater` `DataList`içerir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-303">Examples of templated controls include `Repeater` and `DataList`.</span></span> 

<span data-ttu-id="2a2cc-304">Blazor bileşenleri, veya `RenderFragment` `RenderFragment<T>`türündeki bileşen parametreleri tanımlayarak şablonlu da oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-304">Blazor components can also be templated by defining component parameters of type `RenderFragment` or `RenderFragment<T>`.</span></span> <span data-ttu-id="2a2cc-305">Bir `RenderFragment` , daha sonra bileşen tarafından işlenebilen bir Razor biçimlendirme öbeğini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-305">A `RenderFragment` represents a chunk of Razor markup that can then be rendered by the component.</span></span> <span data-ttu-id="2a2cc-306">, İşleme parçası işlendiğinde belirtilebilen bir parametre alan Razor biçimlendirme öbektir.`RenderFragment<T>`</span><span class="sxs-lookup"><span data-stu-id="2a2cc-306">A `RenderFragment<T>` is a chunk of Razor markup that takes a parameter that can be specified when the render fragment is rendered.</span></span>

### <a name="child-content"></a><span data-ttu-id="2a2cc-307">Alt içerik</span><span class="sxs-lookup"><span data-stu-id="2a2cc-307">Child content</span></span>

<span data-ttu-id="2a2cc-308">Blazor bileşenleri alt içeriğini bir olarak yakalayabilir ve bu `RenderFragment` içeriği bileşen işlemenin bir parçası olarak işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-308">Blazor components can capture their child content as a `RenderFragment` and render that content as part of the component rendering.</span></span> <span data-ttu-id="2a2cc-309">Alt içeriği yakalamak için, türü `RenderFragment` bir bileşen parametresi tanımlayın ve bu `ChildContent`parametreyi adlandırın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-309">To capture child content, define a component parameter of type `RenderFragment` and name it `ChildContent`.</span></span>

<span data-ttu-id="2a2cc-310">*ChildContentComponent. Razor*</span><span class="sxs-lookup"><span data-stu-id="2a2cc-310">*ChildContentComponent.razor*</span></span>

```razor
<h1>Component with child content</h1>

<div>@ChildContent</div>

@code {
    [Parameter]
    public RenderFragment ChildContent { get; set; }
}
```

<span data-ttu-id="2a2cc-311">Bir üst bileşen daha sonra normal Razor söz dizimi kullanarak alt içerik sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-311">A parent component can then supply child content using normal Razor syntax.</span></span>

```razor
<ChildContentComponent>
    <p>The time is @DateTime.Now</p>
</ChildContentComponent>
```

### <a name="template-parameters"></a><span data-ttu-id="2a2cc-312">Şablon parametreleri</span><span class="sxs-lookup"><span data-stu-id="2a2cc-312">Template parameters</span></span>

<span data-ttu-id="2a2cc-313">Şablonlu bir Blazor bileşeni, veya `RenderFragment` `RenderFragment<T>`türünde birden çok bileşen parametresi de tanımlayabilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-313">A templated Blazor component can also define multiple component parameters of type `RenderFragment` or `RenderFragment<T>`.</span></span> <span data-ttu-id="2a2cc-314">İçin `RenderFragment<T>` parametresi çağrıldığında belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-314">The parameter for a `RenderFragment<T>` can be specified when it's invoked.</span></span> <span data-ttu-id="2a2cc-315">Bir bileşen için genel bir tür parametresi belirtmek için `@typeparam` Razor yönergesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-315">To specify a generic type parameter for a component, use the `@typeparam` Razor directive.</span></span>

<span data-ttu-id="2a2cc-316">*SimpleListView. Razor*</span><span class="sxs-lookup"><span data-stu-id="2a2cc-316">*SimpleListView.razor*</span></span>

```razor
@typeparam TItem

@Heading

<ul>
@foreach (var item in items)
{
    <li>@ItemTemplate(item)</li>
}
</ul>

@code {
    [Parameter]
    public RenderFragment Heading { get; set; }

    [Parameter]
    public RenderFragment<TItem> ItemTemplate { get; set; }

    [Parameter]
    public IEnumerable<TItem> Items { get; set; }
}
```

<span data-ttu-id="2a2cc-317">Şablonlu bir bileşen kullanırken, şablon parametreleri parametrelerin adlarıyla eşleşen alt öğeler kullanılarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-317">When using a templated component, the template parameters can be specified using child elements that match the names of the parameters.</span></span> <span data-ttu-id="2a2cc-318">Öğe olarak geçirilmiş türdeki `RenderFragment<T>` bileşen bağımsız değişkenlerinin adlı `context`örtülü bir parametresi vardır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-318">Component arguments of type `RenderFragment<T>` passed as elements have an implicit parameter named `context`.</span></span> <span data-ttu-id="2a2cc-319">Bu uygulama parametresinin adını alt öğe üzerindeki `Context` özniteliğini kullanarak değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-319">You can change the name of this implement parameter using the `Context` attribute on the child element.</span></span> <span data-ttu-id="2a2cc-320">Herhangi bir genel tür parametresi, tür parametresinin adıyla eşleşen bir öznitelik kullanılarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-320">Any generic type parameters can be specified using an attribute that matches the name of the type parameter.</span></span> <span data-ttu-id="2a2cc-321">Mümkünse tür parametresi çıkarsanacaktır:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-321">The type parameter will be inferred if possible:</span></span>

```razor
<SimpleListView Items="messages" TItem="string">
    <Heading>
        <h1>My list</h1>
    </Heading>
    <ItemTemplate Content="message">
        <p>The message is: @message</p>
    </ItemTemplate>
</SimpleListView>
```

<span data-ttu-id="2a2cc-322">Bu bileşenin çıktısı şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="2a2cc-322">The output of this component looks like this:</span></span>

```html
<h1>My list</h1>
<ul>
    <li>The message is: message1</li>
    <li>The message is: message2</li>
<ul>
```

## <a name="code-behind"></a><span data-ttu-id="2a2cc-323">Arka plan kodu</span><span class="sxs-lookup"><span data-stu-id="2a2cc-323">Code-behind</span></span>

<span data-ttu-id="2a2cc-324">Bir Blazor bileşeni genellikle tek bir *. Razor* dosyasında yazılır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-324">A Blazor component is typically authored in a single *.razor* file.</span></span> <span data-ttu-id="2a2cc-325">Ancak, arka plan kod dosyası kullanarak kodu ve biçimlendirmeyi ayırmak de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-325">However, it's also possible to separate the code and markup using a code-behind file.</span></span> <span data-ttu-id="2a2cc-326">Bir bileşen dosyası kullanmak için, bileşen dosyasının C# dosya adıyla eşleşen bir dosya ekleyin *. cs* uzantısı eklenmiştir (*Counter.Razor.cs*).</span><span class="sxs-lookup"><span data-stu-id="2a2cc-326">To use a component file, add a C# file that matches the file name of the component file but with a *.cs* extension added (*Counter.razor.cs*).</span></span> <span data-ttu-id="2a2cc-327">Bileşen için C# bir temel sınıf tanımlamak üzere dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-327">Use the C# file to define a base class for the component.</span></span> <span data-ttu-id="2a2cc-328">Temel sınıfı istediğiniz şekilde adlandırın, ancak sınıfı bileşen sınıfıyla aynı ada, ancak `Base` uzantısı eklenmiş (`CounterBase`) olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-328">You can name the base class anything you'd like, but it's common to name the class the same as the component class, but with a `Base` extension added (`CounterBase`).</span></span> <span data-ttu-id="2a2cc-329">Bileşen tabanlı sınıf de türevi `ComponentBase`olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-329">The component-based class must also derive from `ComponentBase`.</span></span> <span data-ttu-id="2a2cc-330">Ardından, Razor bileşen dosyasında, bileşen ( `@inherits` `@inherits CounterBase`) için temel sınıfı belirtmek üzere yönergesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-330">Then, in the Razor component file, add the `@inherits` directive to specify the base class for the component (`@inherits CounterBase`).</span></span>

<span data-ttu-id="2a2cc-331">*Counter. Razor*</span><span class="sxs-lookup"><span data-stu-id="2a2cc-331">*Counter.razor*</span></span>

```razor
@inherits CounterBase

<h1>Counter</h1>

<p>Current count: @currentCount</p>

<button @onclick="IncrementCount">Click me</button>
```

<span data-ttu-id="2a2cc-332">*Counter.razor.cs*</span><span class="sxs-lookup"><span data-stu-id="2a2cc-332">*Counter.razor.cs*</span></span>

```csharp
public class CounterBase : ComponentBase 
{
    protected int currentCount = 0;

    protected void IncrementCount()
    {
        currentCount++;
    }
}
```

<span data-ttu-id="2a2cc-333">Temel sınıftaki `protected` `public` bileşen üyelerinin görünürlüğü, bileşen sınıfına görünür olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-333">The visibility of the component's members in the base class must be `protected` or `public` to be visible to the component class.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2a2cc-334">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2a2cc-334">Additional resources</span></span>

<span data-ttu-id="2a2cc-335">Yukarıdaki, Blazor bileşenlerinin tüm yönlerinin kapsamlı bir şekilde ele alınması değildir.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-335">The preceding isn't an exhaustive treatment of all aspects of Blazor components.</span></span> <span data-ttu-id="2a2cc-336">[ASP.NET Core Razor bileşenleri oluşturma ve kullanma](/aspnet/core/blazor/components)hakkında daha fazla bilgi için Blazor belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="2a2cc-336">For more information on how to [Create and use ASP.NET Core Razor components](/aspnet/core/blazor/components), see the Blazor documentation.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="2a2cc-337">[Önceki](app-startup.md)
>[İleri](pages-routing-layouts.md)</span><span class="sxs-lookup"><span data-stu-id="2a2cc-337">[Previous](app-startup.md)
[Next](pages-routing-layouts.md)</span></span>