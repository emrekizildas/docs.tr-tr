---
title: 'Nasıl yapılır: Yansıma Kullanarak Temsilci Bağlama'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- events [.NET Framework], adding event handlers with reflection
- reflection, adding event-handler delegates
- delegates [.NET Framework], adding event handlers with reflection
ms.assetid: 076ee62d-a964-449e-a447-c31b33518b81
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 937dca59be8b83526ebf6cd4c369532b1a8b9afe
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045975"
---
# <a name="how-to-hook-up-a-delegate-using-reflection"></a><span data-ttu-id="4a86a-102">Nasıl yapılır: Yansıma Kullanarak Temsilci Bağlama</span><span class="sxs-lookup"><span data-stu-id="4a86a-102">How to: Hook Up a Delegate Using Reflection</span></span>
<span data-ttu-id="4a86a-103">Derlemeleri yüklemek ve çalıştırmak için yansıma kullandığınızda, olayları bağlamak için C# `+=` işleç veya Visual Basic [AddHandler ifadesiyle](../../visual-basic/language-reference/statements/addhandler-statement.md) gibi dil özelliklerini kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="4a86a-103">When you use reflection to load and run assemblies, you cannot use language features like the C# `+=` operator or the Visual Basic [AddHandler statement](../../visual-basic/language-reference/statements/addhandler-statement.md) to hook up events.</span></span> <span data-ttu-id="4a86a-104">Aşağıdaki yordamlarda, tüm gerekli türleri yansıma aracılığıyla alarak bir olaya mevcut bir yöntemi nasıl yedekleyerek, yansıma yayma kullanarak dinamik bir yöntem oluşturma ve bir olaya bağlama işlemleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-104">The following procedures show how to hook up an existing method to an event by getting all the necessary types through reflection, and how to create a dynamic method using reflection emit and hook it up to an event.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="4a86a-105">Bir olay işleme temsilcisini bağlamak için başka bir yöntem için, <xref:System.Reflection.EventInfo.AddEventHandler%2A> <xref:System.Reflection.EventInfo> sınıfının yöntemi için kod örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="4a86a-105">For another way to hook up an event-handling delegate, see the code example for the <xref:System.Reflection.EventInfo.AddEventHandler%2A> method of the <xref:System.Reflection.EventInfo> class.</span></span>  
  
### <a name="to-hook-up-a-delegate-using-reflection"></a><span data-ttu-id="4a86a-106">Yansımayı kullanarak bir temsilciyi bağlama</span><span class="sxs-lookup"><span data-stu-id="4a86a-106">To hook up a delegate using reflection</span></span>  
  
1. <span data-ttu-id="4a86a-107">Olayları başlatan bir tür içeren bir derleme yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4a86a-107">Load an assembly that contains a type that raises events.</span></span> <span data-ttu-id="4a86a-108">Derlemeler genellikle <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> yöntemiyle yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-108">Assemblies are usually loaded with the <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="4a86a-109">Bu örneği basit tutmak için geçerli derlemede bulunan türetilmiş bir form kullanılır, bu nedenle <xref:System.Reflection.Assembly.GetExecutingAssembly%2A> yöntem geçerli derlemeyi yüklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-109">To keep this example simple, a derived form in the current assembly is used, so the <xref:System.Reflection.Assembly.GetExecutingAssembly%2A> method is used to load the current assembly.</span></span>  
  
     [!code-cpp[HookUpDelegate#3](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#3)]
     [!code-csharp[HookUpDelegate#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#3)]
     [!code-vb[HookUpDelegate#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#3)]  
  
2. <span data-ttu-id="4a86a-110">Türü temsil <xref:System.Type> eden bir nesne alın ve türün bir örneğini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4a86a-110">Get a <xref:System.Type> object representing the type, and create an instance of the type.</span></span> <span data-ttu-id="4a86a-111">Yöntemi <xref:System.Activator.CreateInstance%28System.Type%29> , parametresiz bir oluşturucuya sahip olduğu için aşağıdaki kodda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-111">The <xref:System.Activator.CreateInstance%28System.Type%29> method is used in the following code because the form has a parameterless constructor.</span></span> <span data-ttu-id="4a86a-112">Oluşturmakta olduğunuz türün parametresiz bir Oluşturucusu yoksa <xref:System.Activator.CreateInstance%2A> kullanabileceğiniz daha fazla başka aşırı yükleme yöntemi vardır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-112">There are several other overloads of the <xref:System.Activator.CreateInstance%2A> method that you can use if the type you are creating does not have a parameterless constructor.</span></span> <span data-ttu-id="4a86a-113">Yeni örnek, derleme hakkında hiçbir şeyin <xref:System.Object> bilinmediğini belirten derlemeyi sürdürmek için tür olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-113">The new instance is stored as type <xref:System.Object> to maintain the fiction that nothing is known about the assembly.</span></span> <span data-ttu-id="4a86a-114">(Yansıma, adlarını önceden bilmeden bir derlemede almanızı sağlar.)</span><span class="sxs-lookup"><span data-stu-id="4a86a-114">(Reflection allows you to get the types in an assembly without knowing their names in advance.)</span></span>  
  
     [!code-cpp[HookUpDelegate#4](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#4)]
     [!code-csharp[HookUpDelegate#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#4)]
     [!code-vb[HookUpDelegate#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#4)]  
  
3. <span data-ttu-id="4a86a-115">Olayı temsil <xref:System.Reflection.EventInfo> eden bir nesne alın ve olayı işlemek için <xref:System.Reflection.EventInfo.EventHandlerType%2A> kullanılan temsilcinin türünü almak için özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4a86a-115">Get an <xref:System.Reflection.EventInfo> object representing the event, and use the <xref:System.Reflection.EventInfo.EventHandlerType%2A> property to get the type of delegate used to handle the event.</span></span> <span data-ttu-id="4a86a-116">Aşağıdaki kodda, <xref:System.Windows.Forms.Control.Click> olay için bir <xref:System.Reflection.EventInfo> elde edilir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-116">In the following code, an <xref:System.Reflection.EventInfo> for the <xref:System.Windows.Forms.Control.Click> event is obtained.</span></span>  
  
     [!code-cpp[HookUpDelegate#5](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#5)]
     [!code-csharp[HookUpDelegate#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#5)]
     [!code-vb[HookUpDelegate#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#5)]  
  
4. <span data-ttu-id="4a86a-117">Olayı işleyen <xref:System.Reflection.MethodInfo> yöntemi temsil eden bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-117">Get a <xref:System.Reflection.MethodInfo> object representing the method that handles the event.</span></span> <span data-ttu-id="4a86a-118">Bu konunun ilerleyen kısımlarında örnek bölümünde yer alan tüm program kodu, <xref:System.EventHandler> <xref:System.Windows.Forms.Control.Click> olayı işleyen temsilcinin imzasıyla eşleşen bir yöntemi içerir, ancak çalışma zamanında dinamik yöntemler de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a86a-118">The complete program code in the Example section later in this topic contains a method that matches the signature of the <xref:System.EventHandler> delegate, which handles the <xref:System.Windows.Forms.Control.Click> event, but you can also generate dynamic methods at run time.</span></span> <span data-ttu-id="4a86a-119">Ayrıntılar için, dinamik bir yöntem kullanarak çalışma zamanında olay işleyicisi oluşturmak için eşlik eden yordama bakın.</span><span class="sxs-lookup"><span data-stu-id="4a86a-119">For details, see the accompanying procedure, for generating an event handler at run time by using a dynamic method.</span></span>  
  
     [!code-cpp[HookUpDelegate#6](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#6)]
     [!code-csharp[HookUpDelegate#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#6)]
     [!code-vb[HookUpDelegate#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#6)]  
  
5. <span data-ttu-id="4a86a-120"><xref:System.Delegate.CreateDelegate%2A> Yöntemini kullanarak temsilcinin bir örneğini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4a86a-120">Create an instance of the delegate, using the <xref:System.Delegate.CreateDelegate%2A> method.</span></span> <span data-ttu-id="4a86a-121">Bu Yöntem statiktir (`Shared` Visual Basic), bu nedenle temsilci türü sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-121">This method is static (`Shared` in Visual Basic), so the delegate type must be supplied.</span></span> <span data-ttu-id="4a86a-122">' A <xref:System.Delegate.CreateDelegate%2A> <xref:System.Reflection.MethodInfo> sahip olan aşırı yüklemelerin kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-122">Using the overloads of <xref:System.Delegate.CreateDelegate%2A> that take a <xref:System.Reflection.MethodInfo> is recommended.</span></span>  
  
     [!code-cpp[HookUpDelegate#7](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#7)]
     [!code-csharp[HookUpDelegate#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#7)]
     [!code-vb[HookUpDelegate#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#7)]  
  
6. <span data-ttu-id="4a86a-123">`add` Erişimci yöntemini alın ve olayı bağlamak için çağırın.</span><span class="sxs-lookup"><span data-stu-id="4a86a-123">Get the `add` accessor method and invoke it to hook up the event.</span></span> <span data-ttu-id="4a86a-124">Tüm olayların, üst `add` düzey dillerin sözdizimi `remove` tarafından gizlenen bir erişimcisi ve erişimcisi vardır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-124">All events have an `add` accessor and a `remove` accessor, which are hidden by the syntax of high-level languages.</span></span> <span data-ttu-id="4a86a-125">Örneğin, C# olayları bağlamak için `+=` işlecini kullanır ve Visual Basic [AddHandler ifadesini](../../visual-basic/language-reference/statements/addhandler-statement.md)kullanır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-125">For example, C# uses the `+=` operator to hook up events, and Visual Basic uses the [AddHandler statement](../../visual-basic/language-reference/statements/addhandler-statement.md).</span></span> <span data-ttu-id="4a86a-126">Aşağıdaki kod, `add` <xref:System.Windows.Forms.Control.Click> olayın erişimcisini alır ve temsilci örneğini geçirerek geç sınırı çağırır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-126">The following code gets the `add` accessor of the <xref:System.Windows.Forms.Control.Click> event and invokes it late-bound, passing in the delegate instance.</span></span> <span data-ttu-id="4a86a-127">Bağımsız değişkenlerin bir dizi olarak geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-127">The arguments must be passed as an array.</span></span>  
  
     [!code-cpp[HookUpDelegate#8](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#8)]
     [!code-csharp[HookUpDelegate#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#8)]
     [!code-vb[HookUpDelegate#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#8)]  
  
7. <span data-ttu-id="4a86a-128">Olayı test edin.</span><span class="sxs-lookup"><span data-stu-id="4a86a-128">Test the event.</span></span> <span data-ttu-id="4a86a-129">Aşağıdaki kod, kod örneğinde tanımlanan formu gösterir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-129">The following code shows the form defined in the code example.</span></span> <span data-ttu-id="4a86a-130">Forma tıklanması olay işleyicisini çağırır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-130">Clicking the form invokes the event handler.</span></span>  
  
     [!code-cpp[HookUpDelegate#12](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#12)]
     [!code-csharp[HookUpDelegate#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#12)]
     [!code-vb[HookUpDelegate#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#12)]  
  
<a name="procedureSection1"></a>   
### <a name="to-generate-an-event-handler-at-run-time-by-using-a-dynamic-method"></a><span data-ttu-id="4a86a-131">Çalışma zamanında dinamik bir yöntem kullanarak olay işleyicisi oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="4a86a-131">To generate an event handler at run time by using a dynamic method</span></span>  
  
1. <span data-ttu-id="4a86a-132">Olay işleyici yöntemleri, basit dinamik yöntemler ve yansıma yayma kullanılarak çalışma zamanında oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-132">Event-handler methods can be generated at run time, using lightweight dynamic methods and reflection emit.</span></span> <span data-ttu-id="4a86a-133">Bir olay işleyicisi oluşturmak için temsilcinin dönüş türü ve parametre türlerine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-133">To construct an event handler, you need the return type and parameter types of the delegate.</span></span> <span data-ttu-id="4a86a-134">Bu, temsilcinin `Invoke` yöntemi incelenerek elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-134">These can be obtained by examining the delegate's `Invoke` method.</span></span> <span data-ttu-id="4a86a-135">Aşağıdaki kod, `GetDelegateReturnType` bu bilgileri elde `GetDelegateParameterTypes` etmek için ve yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-135">The following code uses the `GetDelegateReturnType` and `GetDelegateParameterTypes` methods to obtain this information.</span></span> <span data-ttu-id="4a86a-136">Bu yöntemlerin kodu, bu konunun ilerleyen kısımlarında örnek bölümünde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-136">The code for these methods can be found in the Example section later in this topic.</span></span>  
  
     <span data-ttu-id="4a86a-137">Bir <xref:System.Reflection.Emit.DynamicMethod>adı vermek gerekli değildir, bu nedenle boş dize kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-137">It is not necessary to name a <xref:System.Reflection.Emit.DynamicMethod>, so the empty string can be used.</span></span> <span data-ttu-id="4a86a-138">Aşağıdaki kodda, son bağımsız değişken dinamik yöntemi geçerli türle ilişkilendirir ve bu temsilci, `Example` sınıfın tüm ortak ve özel üyelerine erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a86a-138">In the following code, the last argument associates the dynamic method with the current type, giving the delegate access to all the public and private members of the `Example` class.</span></span>  
  
     [!code-cpp[HookUpDelegate#9](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#9)]
     [!code-csharp[HookUpDelegate#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#9)]
     [!code-vb[HookUpDelegate#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#9)]  
  
2. <span data-ttu-id="4a86a-139">Bir yöntem gövdesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4a86a-139">Generate a method body.</span></span> <span data-ttu-id="4a86a-140">Bu yöntem bir dize yükler, bir dizeyi alan <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=nameWithType> metodun aşırı yüklemesini çağırır, dönüş değerini yığından kapatır (işleyicinin dönüş türü olmadığından) ve döndürür.</span><span class="sxs-lookup"><span data-stu-id="4a86a-140">This method loads a string, calls the overload of the <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=nameWithType> method that takes a string, pops the return value off the stack (because the handler has no return type), and returns.</span></span> <span data-ttu-id="4a86a-141">Dinamik yöntemleri yayma hakkında daha fazla bilgi edinmek için [bkz. nasıl yapılır: Dinamik yöntemleri](how-to-define-and-execute-dynamic-methods.md)tanımlayın ve yürütün.</span><span class="sxs-lookup"><span data-stu-id="4a86a-141">To learn more about emitting dynamic methods, see [How to: Define and Execute Dynamic Methods](how-to-define-and-execute-dynamic-methods.md).</span></span>  
  
     [!code-cpp[HookUpDelegate#10](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#10)]
     [!code-csharp[HookUpDelegate#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#10)]
     [!code-vb[HookUpDelegate#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#10)]  
  
3. <span data-ttu-id="4a86a-142"><xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> Yöntemini çağırarak dinamik metodu doldurun.</span><span class="sxs-lookup"><span data-stu-id="4a86a-142">Complete the dynamic method by calling its <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> method.</span></span> <span data-ttu-id="4a86a-143">Olayın çağırma listesine temsilciyi eklemek için erişimcisinikullanın.`add`</span><span class="sxs-lookup"><span data-stu-id="4a86a-143">Use the `add` accessor to add the delegate to the invocation list for the event.</span></span>  
  
     [!code-cpp[HookUpDelegate#11](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#11)]
     [!code-csharp[HookUpDelegate#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#11)]
     [!code-vb[HookUpDelegate#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#11)]  
  
4. <span data-ttu-id="4a86a-144">Olayı test edin.</span><span class="sxs-lookup"><span data-stu-id="4a86a-144">Test the event.</span></span> <span data-ttu-id="4a86a-145">Aşağıdaki kod, kod örneğinde tanımlanan formu yükler.</span><span class="sxs-lookup"><span data-stu-id="4a86a-145">The following code loads the form defined in the code example.</span></span> <span data-ttu-id="4a86a-146">Formu tıklatmak, hem önceden tanımlanmış olay işleyicisini hem de yayınlanan olay işleyicisini çağırır.</span><span class="sxs-lookup"><span data-stu-id="4a86a-146">Clicking the form invokes both the predefined event handler and the emitted event handler.</span></span>  
  
     [!code-cpp[HookUpDelegate#12](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#12)]
     [!code-csharp[HookUpDelegate#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#12)]
     [!code-vb[HookUpDelegate#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#12)]  
  
## <a name="example"></a><span data-ttu-id="4a86a-147">Örnek</span><span class="sxs-lookup"><span data-stu-id="4a86a-147">Example</span></span>  
 <span data-ttu-id="4a86a-148">Aşağıdaki kod örneği, var olan bir yöntemin yansıma kullanarak bir olaya nasıl bağlanacağını ve ayrıca, <xref:System.Reflection.Emit.DynamicMethod> çalışma zamanında bir yöntemi göstermek ve bir olaya bağlamak için sınıfını nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="4a86a-148">The following code example shows how to hook up an existing method to an event using reflection, and also how to use the <xref:System.Reflection.Emit.DynamicMethod> class to emit a method at run time and hook it up to an event.</span></span>  
  
 [!code-cpp[HookUpDelegate#1](../../../samples/snippets/cpp/VS_Snippets_CLR/HookUpDelegate/cpp/source.cpp#1)]
 [!code-csharp[HookUpDelegate#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HookUpDelegate/cs/source.cs#1)]
 [!code-vb[HookUpDelegate#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HookUpDelegate/vb/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="4a86a-149">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="4a86a-149">See also</span></span>

- <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>
- <xref:System.Reflection.Emit.DynamicMethod>
- <xref:System.Activator.CreateInstance%2A>
- <xref:System.Delegate.CreateDelegate%2A>
- [<span data-ttu-id="4a86a-150">Nasıl yapılır: Dinamik yöntemleri tanımlama ve yürütme</span><span class="sxs-lookup"><span data-stu-id="4a86a-150">How to: Define and Execute Dynamic Methods</span></span>](how-to-define-and-execute-dynamic-methods.md)
- [<span data-ttu-id="4a86a-151">Yansıma</span><span class="sxs-lookup"><span data-stu-id="4a86a-151">Reflection</span></span>](reflection.md)
