---
title: Using Deyimi (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.using
helpviewer_keywords:
- resource disposal
- Try...Catch...Finally statements, equivalent to Using statement
- resources [Visual Basic], disposing
- Using statement [Visual Basic]
ms.assetid: 665d1580-dd54-4e96-a9a9-6be2a68948f1
ms.openlocfilehash: 819af63acb6a1f038300bcb999dcfb904eb8a457
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71592085"
---
# <a name="using-statement-visual-basic"></a><span data-ttu-id="fd770-102">Using Deyimi (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="fd770-102">Using Statement (Visual Basic)</span></span>

<span data-ttu-id="fd770-103">@No__t-0 bloğunun başlangıcını bildirir ve isteğe bağlı olarak blok denetimlerinin bulunduğu sistem kaynaklarını alır.</span><span class="sxs-lookup"><span data-stu-id="fd770-103">Declares the beginning of a `Using` block and optionally acquires the system resources that the block controls.</span></span>

## <a name="syntax"></a><span data-ttu-id="fd770-104">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="fd770-104">Syntax</span></span>

```vb
Using { resourcelist | resourceexpression }
    [ statements ]
End Using
```

## <a name="parts"></a><span data-ttu-id="fd770-105">Bölümler</span><span class="sxs-lookup"><span data-stu-id="fd770-105">Parts</span></span>

|<span data-ttu-id="fd770-106">Terim</span><span class="sxs-lookup"><span data-stu-id="fd770-106">Term</span></span>|<span data-ttu-id="fd770-107">Tanım</span><span class="sxs-lookup"><span data-stu-id="fd770-107">Definition</span></span>|  
|---|---|  
|`resourcelist`|<span data-ttu-id="fd770-108">@No__t (0) belirtmezseniz gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fd770-108">Required if you do not supply `resourceexpression`.</span></span> <span data-ttu-id="fd770-109">Bu `Using` blok denetimlerinin denetimlerin virgülle ayrıldığı bir veya daha fazla sistem kaynağı listesi.</span><span class="sxs-lookup"><span data-stu-id="fd770-109">List of one or more system resources that this `Using` block controls, separated by commas.</span></span>|  
|`resourceexpression`|<span data-ttu-id="fd770-110">@No__t (0) belirtmezseniz gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fd770-110">Required if you do not supply `resourcelist`.</span></span> <span data-ttu-id="fd770-111">Bu `Using` bloğu tarafından denetlenerek bir sistem kaynağını işaret eden başvuru değişkeni veya ifadesi.</span><span class="sxs-lookup"><span data-stu-id="fd770-111">Reference variable or expression referring to a system resource to be controlled by this `Using` block.</span></span>|  
|`statements`|<span data-ttu-id="fd770-112">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="fd770-112">Optional.</span></span> <span data-ttu-id="fd770-113">@No__t-0 bloğunun çalıştığı deyimler bloğu.</span><span class="sxs-lookup"><span data-stu-id="fd770-113">Block of statements that the `Using` block runs.</span></span>|  
|`End Using`|<span data-ttu-id="fd770-114">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="fd770-114">Required.</span></span> <span data-ttu-id="fd770-115">@No__t-0 bloğunun tanımını ve denetlediği tüm kaynakların bir kısmını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="fd770-115">Terminates the definition of the `Using` block and disposes of all the resources that it controls.</span></span>|  

 <span data-ttu-id="fd770-116">@No__t-0 parçasındaki her kaynak aşağıdaki söz dizimi ve bölümlere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="fd770-116">Each resource in the `resourcelist` part has the following syntax and parts:</span></span>

 `resourcename As New resourcetype [ ( [ arglist ] ) ]`

 <span data-ttu-id="fd770-117">veya</span><span class="sxs-lookup"><span data-stu-id="fd770-117">-or-</span></span>

 `resourcename As resourcetype = resourceexpression`

## <a name="resourcelist-parts"></a><span data-ttu-id="fd770-118">resourceList bölümleri</span><span class="sxs-lookup"><span data-stu-id="fd770-118">resourcelist Parts</span></span>

|<span data-ttu-id="fd770-119">Terim</span><span class="sxs-lookup"><span data-stu-id="fd770-119">Term</span></span>|<span data-ttu-id="fd770-120">Tanım</span><span class="sxs-lookup"><span data-stu-id="fd770-120">Definition</span></span>|  
|---|---|  
|`resourcename`|<span data-ttu-id="fd770-121">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="fd770-121">Required.</span></span> <span data-ttu-id="fd770-122">@No__t-0 bloğunun denetlediği bir sistem kaynağına başvuran başvuru değişkeni.</span><span class="sxs-lookup"><span data-stu-id="fd770-122">Reference variable that refers to a system resource that the `Using` block controls.</span></span>|  
|`New`|<span data-ttu-id="fd770-123">@No__t-0 ifadesinde kaynak elde ederseniz gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fd770-123">Required if the `Using` statement acquires the resource.</span></span> <span data-ttu-id="fd770-124">Kaynağı zaten aldıysanız, ikinci söz dizimi alternatifini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fd770-124">If you have already acquired the resource, use the second syntax alternative.</span></span>|  
|`resourcetype`|<span data-ttu-id="fd770-125">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="fd770-125">Required.</span></span> <span data-ttu-id="fd770-126">Kaynağın sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fd770-126">The class of the resource.</span></span> <span data-ttu-id="fd770-127">Sınıfın <xref:System.IDisposable> arabirimini uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd770-127">The class must implement the <xref:System.IDisposable> interface.</span></span>|  
|`arglist`|<span data-ttu-id="fd770-128">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="fd770-128">Optional.</span></span> <span data-ttu-id="fd770-129">@No__t-0 örneğini oluşturmak için oluşturucuya geçirdiğiniz bağımsız değişkenlerin listesi.</span><span class="sxs-lookup"><span data-stu-id="fd770-129">List of arguments you are passing to the constructor to create an instance of `resourcetype`.</span></span> <span data-ttu-id="fd770-130">Bkz. [parametre listesi](parameter-list.md).</span><span class="sxs-lookup"><span data-stu-id="fd770-130">See [Parameter List](parameter-list.md).</span></span>|  
|`resourceexpression`|<span data-ttu-id="fd770-131">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="fd770-131">Required.</span></span> <span data-ttu-id="fd770-132">@No__t-0 gereksinimlerini karşılayan bir sistem kaynağına başvuran değişken veya ifade.</span><span class="sxs-lookup"><span data-stu-id="fd770-132">Variable or expression referring to a system resource satisfying the requirements of `resourcetype`.</span></span> <span data-ttu-id="fd770-133">İkinci sözdizimi alternatif kullanırsanız, denetimi `Using` ifadesine geçirmeden önce kaynağı edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd770-133">If you use the second syntax alternative, you must acquire the resource before passing control to the `Using` statement.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="fd770-134">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="fd770-134">Remarks</span></span>

 <span data-ttu-id="fd770-135">Bazen kodunuzun dosya tanıtıcısı, COM sarmalayıcısı veya SQL bağlantısı gibi yönetilmeyen bir kaynak olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd770-135">Sometimes your code requires an unmanaged resource, such as a file handle, a COM wrapper, or a SQL connection.</span></span> <span data-ttu-id="fd770-136">@No__t-0 bloğu, kodunuz ile işiniz bittiğinde bir veya daha fazla kaynağı elden çıkarma garantisi verir.</span><span class="sxs-lookup"><span data-stu-id="fd770-136">A `Using` block guarantees the disposal of one or more such resources when your code is finished with them.</span></span> <span data-ttu-id="fd770-137">Bu, diğer kodun kullanması için kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="fd770-137">This makes them available for other code to use.</span></span>

 <span data-ttu-id="fd770-138">Yönetilen kaynaklar, .NET Framework atık toplayıcı (GC) tarafından, sizin bölümlemeden herhangi bir ek kodlama yapılmadan elden alınır.</span><span class="sxs-lookup"><span data-stu-id="fd770-138">Managed resources are disposed of by the .NET Framework garbage collector (GC) without any extra coding on your part.</span></span> <span data-ttu-id="fd770-139">Yönetilen kaynaklar için `Using` bloğuna ihtiyacınız yoktur.</span><span class="sxs-lookup"><span data-stu-id="fd770-139">You do not need a `Using` block for managed resources.</span></span> <span data-ttu-id="fd770-140">Ancak, atık toplayıcıyı beklemek yerine, yönetilen bir kaynağın elden çıkarılmasını zorlamak için `Using` bloğu kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd770-140">However, you can still use a `Using` block to force the disposal of a managed resource instead of waiting for the garbage collector.</span></span>

 <span data-ttu-id="fd770-141">@No__t-0 bloğu üç bölümden oluşur: alma, kullanım ve çıkarma.</span><span class="sxs-lookup"><span data-stu-id="fd770-141">A `Using` block has three parts: acquisition, usage, and disposal.</span></span>

- <span data-ttu-id="fd770-142">*Alım* , bir değişken oluşturma ve sistem kaynağına başvuracak şekilde başlatma anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fd770-142">*Acquisition* means creating a variable and initializing it to refer to the system resource.</span></span> <span data-ttu-id="fd770-143">@No__t-0 ifadesinde bir veya daha fazla kaynak alabilir ya da bloğu girmeden önce tam olarak bir kaynak alabilir ve bunu `Using` ifadesine sağlayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="fd770-143">The `Using` statement can acquire one or more resources, or you can acquire exactly one resource before entering the block and supply it to the `Using` statement.</span></span> <span data-ttu-id="fd770-144">@No__t-0 sağlarsanız, denetimi `Using` ifadesine geçirmeden önce kaynağı edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fd770-144">If you supply `resourceexpression`, you must acquire the resource before passing control to the `Using` statement.</span></span>

- <span data-ttu-id="fd770-145">*Kullanım* , kaynaklara erişmek ve bunlarla eylemler gerçekleştirmek anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fd770-145">*Usage* means accessing the resources and performing actions with them.</span></span> <span data-ttu-id="fd770-146">@No__t-0 ve `End Using` arasındaki deyimler, kaynakların kullanımını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fd770-146">The statements between `Using` and `End Using` represent the usage of the resources.</span></span>

- <span data-ttu-id="fd770-147">*Aktiften çıkarma* , <xref:System.IDisposable.Dispose%2A> yönteminin `resourcename` içindeki nesne üzerinde çağrılması anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fd770-147">*Disposal* means calling the <xref:System.IDisposable.Dispose%2A> method on the object in `resourcename`.</span></span> <span data-ttu-id="fd770-148">Bu, nesnenin kaynaklarını düzgün bir şekilde sonlanmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="fd770-148">This allows the object to cleanly terminate its resources.</span></span> <span data-ttu-id="fd770-149">@No__t-0 deyimleri, `Using` bloğunun denetimindeki kaynakları ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="fd770-149">The `End Using` statement disposes of the resources under the `Using` block's control.</span></span>

## <a name="behavior"></a><span data-ttu-id="fd770-150">Davranış</span><span class="sxs-lookup"><span data-stu-id="fd770-150">Behavior</span></span>

 <span data-ttu-id="fd770-151">@No__t-0 bloğu, `Try` bloğunun kaynakları ve @no__t 4 blok tarafından kullanıldığı `Try`... `Finally` oluşturma gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="fd770-151">A `Using` block behaves like a `Try`...`Finally` construction in which the `Try` block uses the resources and the `Finally` block disposes of them.</span></span> <span data-ttu-id="fd770-152">Bu nedenle, `Using` bloğu, bloğundan çıktığınızda bağımsız olarak kaynakları elden çıkarma garantisi verir.</span><span class="sxs-lookup"><span data-stu-id="fd770-152">Because of this, the `Using` block guarantees disposal of the resources, no matter how you exit the block.</span></span> <span data-ttu-id="fd770-153">Bu, <xref:System.StackOverflowException> dışında işlenmeyen bir özel durum durumunda bile geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="fd770-153">This is true even in the case of an unhandled exception, except for a <xref:System.StackOverflowException>.</span></span>

 <span data-ttu-id="fd770-154">@No__t-0 ifadesiyle alınan her kaynak değişkeninin kapsamı `Using` bloğu ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fd770-154">The scope of every resource variable acquired by the `Using` statement is limited to the `Using` block.</span></span>

 <span data-ttu-id="fd770-155">@No__t-0 ifadesinde birden fazla sistem kaynağı belirtirseniz, efekt, `Using` blokları diğeri içinde iç içe yerleştirilmiş şekilde aynı olur.</span><span class="sxs-lookup"><span data-stu-id="fd770-155">If you specify more than one system resource in the `Using` statement, the effect is the same as if you nested `Using` blocks one within another.</span></span>

 <span data-ttu-id="fd770-156">@No__t-0 `Nothing` ise, <xref:System.IDisposable.Dispose%2A> çağrısı yapılmaz ve hiçbir özel durum oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="fd770-156">If `resourcename` is `Nothing`, no call to <xref:System.IDisposable.Dispose%2A> is made, and no exception is thrown.</span></span>

## <a name="structured-exception-handling-within-a-using-block"></a><span data-ttu-id="fd770-157">Bir using bloğu Içinde yapılandırılmış özel durum Işleme</span><span class="sxs-lookup"><span data-stu-id="fd770-157">Structured Exception Handling Within a Using Block</span></span>

 <span data-ttu-id="fd770-158">@No__t-0 bloğunda oluşabilecek bir özel durumu işlemeniz gerekiyorsa, buna tam bir `Try`... `Finally` yapımı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd770-158">If you need to handle an exception that might occur within the `Using` block, you can add a complete `Try`...`Finally` construction to it.</span></span> <span data-ttu-id="fd770-159">@No__t-0 ifadesinin bir kaynağı alırken başarılı olmadığı durumu işlemeniz gerekiyorsa, `resourcename` ' in `Nothing` olup olmadığını görmek için test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd770-159">If you need to handle the case where the `Using` statement is not successful in acquiring a resource, you can test to see if `resourcename` is `Nothing`.</span></span>

## <a name="structured-exception-handling-instead-of-a-using-block"></a><span data-ttu-id="fd770-160">Bir using bloğu yerine yapılandırılmış özel durum Işleme</span><span class="sxs-lookup"><span data-stu-id="fd770-160">Structured Exception Handling Instead of a Using Block</span></span>

 <span data-ttu-id="fd770-161">Kaynakların alımı üzerinde daha hassas denetime ihtiyacınız varsa veya `Finally` bloğunda ek koda ihtiyacınız varsa, `Using` bloğunu `Try`... `Finally` oluşturma olarak yeniden yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd770-161">If you need finer control over the acquisition of the resources, or you need additional code in the `Finally` block, you can rewrite the `Using` block as a `Try`...`Finally` construction.</span></span> <span data-ttu-id="fd770-162">Aşağıdaki örnekte, `resource` ' nin alımı ve aktiften çıkarılması ile eşdeğer olan iskelet `Try` ve `Using` kurulumlarını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fd770-162">The following example shows skeleton `Try` and `Using` constructions that are equivalent in the acquisition and disposal of `resource`.</span></span>

```vb
Using resource As New resourceType
    ' Insert code to work with resource.
End Using

' For the acquisition and disposal of resource, the following  
' Try construction is equivalent to the Using block.
Dim resource As New resourceType
Try
    ' Insert code to work with resource.
Finally
    If resource IsNot Nothing Then
        resource.Dispose()
    End If
End Try
```

> [!NOTE]
> <span data-ttu-id="fd770-163">@No__t-0 bloğunun içindeki kod, `resourcename` ' deki nesneyi başka bir değişkene atamamalıdır.</span><span class="sxs-lookup"><span data-stu-id="fd770-163">The code inside the `Using` block should not assign the object in `resourcename` to another variable.</span></span> <span data-ttu-id="fd770-164">@No__t-0 bloğundan çıktığınızda, kaynak atılmış olur ve diğer değişken işaret ettiği kaynağa erişemez.</span><span class="sxs-lookup"><span data-stu-id="fd770-164">When you exit the `Using` block, the resource is disposed, and the other variable cannot access the resource to which it points.</span></span>

## <a name="example"></a><span data-ttu-id="fd770-165">Örnek</span><span class="sxs-lookup"><span data-stu-id="fd770-165">Example</span></span>

 <span data-ttu-id="fd770-166">Aşağıdaki örnek, log. txt adlı bir dosya oluşturur ve dosyaya iki satırlık metin yazar.</span><span class="sxs-lookup"><span data-stu-id="fd770-166">The following example creates a file that is named log.txt and writes two lines of text to the file.</span></span> <span data-ttu-id="fd770-167">Örnek ayrıca aynı dosyayı okur ve metin satırlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="fd770-167">The example also reads that same file and displays the lines of text:</span></span>

 <span data-ttu-id="fd770-168">@No__t-0 ve <xref:System.IO.TextReader> sınıfları <xref:System.IDisposable> arabirimini uygulamadığından, kod, yazma ve okuma işlemlerinden sonra dosyanın doğru şekilde kapatılmasını sağlamak için `Using` deyimlerini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="fd770-168">Because the <xref:System.IO.TextWriter> and <xref:System.IO.TextReader> classes implement the <xref:System.IDisposable> interface, the code can use `Using` statements to ensure that the file is correctly closed after the write and read operations.</span></span>

 [!code-vb[VbVbalrStatements#50](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#50)]

## <a name="see-also"></a><span data-ttu-id="fd770-169">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="fd770-169">See also</span></span>

- <xref:System.IDisposable>
- [<span data-ttu-id="fd770-170">Try...Catch...Finally Deyimi</span><span class="sxs-lookup"><span data-stu-id="fd770-170">Try...Catch...Finally Statement</span></span>](try-catch-finally-statement.md)
- <span data-ttu-id="fd770-171">[Nasıl yapılır: Bir sistem kaynağını atma @ no__t-0</span><span class="sxs-lookup"><span data-stu-id="fd770-171">[How to: Dispose of a System Resource](../../programming-guide/language-features/control-flow/how-to-dispose-of-a-system-resource.md)</span></span>
