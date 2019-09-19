---
title: Dizinler ve aralıklar kullanarak veri aralıklarını keşfet
description: Bu gelişmiş öğreticide, sıralı bir veri kümesinin dilimlerini incelemek üzere dizinler ve aralıklar kullanarak verileri araştırmanızı öğretilir.
ms.date: 04/19/2019
ms.custom: mvc
ms.openlocfilehash: d0eeadfff9732ced22e045536a88ed49cd98bbaa
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117839"
---
# <a name="indices-and-ranges"></a><span data-ttu-id="b3a4a-103">Dizinler ve aralıklar</span><span class="sxs-lookup"><span data-stu-id="b3a4a-103">Indices and ranges</span></span>

<span data-ttu-id="b3a4a-104">Aralıklar <xref:System.Array>ve dizinler <xref:System.String> <xref:System.ReadOnlySpan%601>, bir,, veya içinde tek öğe veya aralıklara erişmek için bir kısa sözdizimi sağlar. <xref:System.Span%601></span><span class="sxs-lookup"><span data-stu-id="b3a4a-104">Ranges and indices provide a succinct syntax for accessing single elements or ranges in an <xref:System.Array>, <xref:System.String>, <xref:System.Span%601>, or <xref:System.ReadOnlySpan%601>.</span></span> <span data-ttu-id="b3a4a-105">Bu özellikler, bir dizideki tek öğelere veya öğe aralıklarına erişmek için daha kısa, sözdizimini açık bir şekilde etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-105">These features enable more concise, clear syntax to access single elements or ranges of elements in a sequence.</span></span>

<span data-ttu-id="b3a4a-106">Bu öğreticide, aşağıdakileri nasıl yapacağınızı öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="b3a4a-106">In this tutorial, you'll learn how to:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="b3a4a-107">Bir dizideki aralıklar için söz dizimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-107">Use the syntax for ranges in a sequence.</span></span>
> - <span data-ttu-id="b3a4a-108">Her bir sıranın başlangıcı ve bitişi için tasarım kararlarını anlayın.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-108">Understand the design decisions for the start and end of each sequence.</span></span>
> - <span data-ttu-id="b3a4a-109"><xref:System.Index> Ve<xref:System.Range> türleri için senaryolar öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-109">Learn scenarios for the <xref:System.Index> and <xref:System.Range> types.</span></span>

## <a name="language-support-for-indices-and-ranges"></a><span data-ttu-id="b3a4a-110">Dizinler ve aralıklar için dil desteği</span><span class="sxs-lookup"><span data-stu-id="b3a4a-110">Language support for indices and ranges</span></span>

<span data-ttu-id="b3a4a-111">Bu dil desteği iki yeni türe ve iki yeni işleçlere dayanır:</span><span class="sxs-lookup"><span data-stu-id="b3a4a-111">This language support relies on two new types and two new operators:</span></span>

- <span data-ttu-id="b3a4a-112"><xref:System.Index?displayProperty=nameWithType>bir dizinin dizisini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-112"><xref:System.Index?displayProperty=nameWithType> represents an index into a sequence.</span></span>
- <span data-ttu-id="b3a4a-113">Bir dizinin bir sıranın sonuna `^`göreli olduğunu belirten bitiş işlecinden dizin.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-113">The index from end operator `^`, which specifies that an index is relative to the end of a sequence.</span></span>
- <span data-ttu-id="b3a4a-114"><xref:System.Range?displayProperty=nameWithType>bir dizinin alt aralığını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-114"><xref:System.Range?displayProperty=nameWithType> represents a sub range of a sequence.</span></span>
- <span data-ttu-id="b3a4a-115">Aralık işleci `..`, bir aralığın işlenenlerinin başlangıcını ve sonunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-115">The range operator `..`, which specifies the start and end of a range as its operands.</span></span>

<span data-ttu-id="b3a4a-116">Dizin kurallarıyla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-116">Let's start with the rules for indices.</span></span> <span data-ttu-id="b3a4a-117">Bir dizi `sequence`düşünün.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-117">Consider an array `sequence`.</span></span> <span data-ttu-id="b3a4a-118">Dizin, ile `sequence[0]`aynıdır. `0`</span><span class="sxs-lookup"><span data-stu-id="b3a4a-118">The `0` index is the same as `sequence[0]`.</span></span> <span data-ttu-id="b3a4a-119">Dizin, ile `sequence[sequence.Length]`aynıdır. `^0`</span><span class="sxs-lookup"><span data-stu-id="b3a4a-119">The `^0` index is the same as `sequence[sequence.Length]`.</span></span> <span data-ttu-id="b3a4a-120">`sequence[^0]` Bunun gibi`sequence[sequence.Length]` bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-120">Note that `sequence[^0]` does throw an exception, just as `sequence[sequence.Length]` does.</span></span> <span data-ttu-id="b3a4a-121">Herhangi bir sayı `n`için Dizin `^n` aynı `sequence[sequence.Length - n]`olur.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-121">For any number `n`, the index `^n` is the same as `sequence[sequence.Length - n]`.</span></span>

```csharp-interactive
string[] words = new string[]
{
                // index from start    index from end
    "The",      // 0                   ^9
    "quick",    // 1                   ^8
    "brown",    // 2                   ^7
    "fox",      // 3                   ^6
    "jumped",   // 4                   ^5
    "over",     // 5                   ^4
    "the",      // 6                   ^3
    "lazy",     // 7                   ^2
    "dog"       // 8                   ^1
};              // 9 (or words.Length) ^0
```

<span data-ttu-id="b3a4a-122">`^1` Dizinle son sözcüğü alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-122">You can retrieve the last word with the `^1` index.</span></span> <span data-ttu-id="b3a4a-123">Başlatmanın altına aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b3a4a-123">Add the following code below the initialization:</span></span>

[!code-csharp[LastIndex](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastIndex)]

<span data-ttu-id="b3a4a-124">Aralık, bir aralığın *başlangıcını* ve *sonunu* belirtir.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-124">A range specifies the *start* and *end* of a range.</span></span> <span data-ttu-id="b3a4a-125">Aralıklar dışlamalı, yani *bitiş* aralığa dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-125">Ranges are exclusive, meaning the *end* is not included in the range.</span></span> <span data-ttu-id="b3a4a-126">Aralık, tüm aralığı temsil eden tüm `[0..sequence.Length]` aralığı temsileder.`[0..^0]`</span><span class="sxs-lookup"><span data-stu-id="b3a4a-126">The range `[0..^0]` represents the entire range, just as `[0..sequence.Length]` represents the entire range.</span></span> 

<span data-ttu-id="b3a4a-127">Aşağıdaki kod, "hızlı", "kahverengi" ve "Fox" sözcüklerinin bulunduğu bir alt Aralık oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-127">The following code creates a subrange with the words "quick", "brown", and "fox".</span></span> <span data-ttu-id="b3a4a-128">`words[1]` İle`words[3]`içerir.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-128">It includes `words[1]` through `words[3]`.</span></span> <span data-ttu-id="b3a4a-129">Öğe `words[4]` Aralık içinde değil.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-129">The element `words[4]` isn't in the range.</span></span> <span data-ttu-id="b3a4a-130">Aşağıdaki kodu aynı yönteme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-130">Add the following code to the same method.</span></span> <span data-ttu-id="b3a4a-131">Etkileşimli pencerenin alt kısmına kopyalayıp yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-131">Copy and paste it at the bottom of the interactive window.</span></span>

[!code-csharp[Range](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Range)]

<span data-ttu-id="b3a4a-132">Aşağıdaki kod, "Lazy" ve "köpek" ile bir alt Aralık oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-132">The following code creates a subrange with "lazy" and "dog".</span></span> <span data-ttu-id="b3a4a-133">`words[^2]` Ve`words[^1]`içerir.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-133">It includes `words[^2]` and `words[^1]`.</span></span> <span data-ttu-id="b3a4a-134">Son dizin `words[^0]` dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-134">The end index `words[^0]` isn't included.</span></span> <span data-ttu-id="b3a4a-135">Aşağıdaki kodu da ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b3a4a-135">Add the following code as well:</span></span>

[!code-csharp[LastRange](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_LastRange)]

<span data-ttu-id="b3a4a-136">Aşağıdaki örnekler, başlangıç, bitiş veya her ikisi için açık olarak biten aralıklar oluşturur:</span><span class="sxs-lookup"><span data-stu-id="b3a4a-136">The following examples create ranges that are open ended for the start, end, or both:</span></span>

[!code-csharp[PartialRange](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_PartialRanges)]

<span data-ttu-id="b3a4a-137">Ayrıca, aralıkları veya dizinleri değişken olarak da bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-137">You can also declare ranges or indices as variables.</span></span> <span data-ttu-id="b3a4a-138">Değişken daha sonra `[` ve `]` karakterleri içinde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="b3a4a-138">The variable can then be used inside the `[` and `]` characters:</span></span>

[!code-csharp[IndexRangeTypes](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_RangeIndexTypes)]

<span data-ttu-id="b3a4a-139">Aşağıdaki örnekte, bu seçimlerin pek çok nedeni gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-139">The following sample shows many of the reasons for those choices.</span></span> <span data-ttu-id="b3a4a-140">Farklı birleşimler denemek için `z` , ve değiştirin `x`. `y`</span><span class="sxs-lookup"><span data-stu-id="b3a4a-140">Modify `x`, `y`, and `z` to try different combinations.</span></span> <span data-ttu-id="b3a4a-141">Denemeler `x` yaptığınızda, `y` 'den`y` küçük olan değerleri kullanın ve geçerli kombinasyonlardan daha küçüktür. `z`</span><span class="sxs-lookup"><span data-stu-id="b3a4a-141">When you experiment, use values where `x` is less than `y`, and `y` is less than `z` for valid combinations.</span></span> <span data-ttu-id="b3a4a-142">Aşağıdaki kodu yeni bir yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-142">Add the following code in a new method.</span></span> <span data-ttu-id="b3a4a-143">Farklı birleşimler deneyin:</span><span class="sxs-lookup"><span data-stu-id="b3a4a-143">Try different combinations:</span></span>

[!code-csharp[SemanticsExamples](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_Semantics)]

## <a name="scenarios-for-indices-and-ranges"></a><span data-ttu-id="b3a4a-144">Dizinler ve aralıklar için senaryolar</span><span class="sxs-lookup"><span data-stu-id="b3a4a-144">Scenarios for Indices and Ranges</span></span>

<span data-ttu-id="b3a4a-145">Genellikle tüm bir sıranın alt aralığında bazı analizler gerçekleştirmek istediğinizde aralıklar ve dizinler kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-145">You'll often use ranges and indices when you want to perform some analysis on subrange of an entire sequence.</span></span> <span data-ttu-id="b3a4a-146">Yeni söz dizimi, tam olarak hangi alt aralığın ilgili olduğunu okumaktan daha net.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-146">The new syntax is clearer in reading exactly what subrange is involved.</span></span> <span data-ttu-id="b3a4a-147">Yerel işlev `MovingAverage` , bağımsız değişkeni <xref:System.Range> olarak bir kullanır.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-147">The local function `MovingAverage` takes a <xref:System.Range> as its argument.</span></span> <span data-ttu-id="b3a4a-148">Bu yöntem daha sonra Min, Max ve Average hesaplama yaparken yalnızca o aralığı numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-148">The method then enumerates just that range when calculating the min, max, and average.</span></span> <span data-ttu-id="b3a4a-149">Projenizde aşağıdaki kodu deneyin:</span><span class="sxs-lookup"><span data-stu-id="b3a4a-149">Try the following code in your project:</span></span>

[!code-csharp[MovingAverages](~/samples/csharp/tutorials/RangesIndexes/IndicesAndRanges.cs#IndicesAndRanges_MovingAverage)]

<span data-ttu-id="b3a4a-150">Tamamlanan kodu [DotNet/Samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/RangesIndexes) deposundan indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3a4a-150">You can download the completed code from the [dotnet/samples](https://github.com/dotnet/samples/tree/master/csharp/tutorials/RangesIndexes) repository.</span></span>
