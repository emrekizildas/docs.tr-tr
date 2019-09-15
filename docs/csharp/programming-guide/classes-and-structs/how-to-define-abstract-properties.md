---
title: 'Nasıl yapılır: Soyut özellikleri tanımlama- C# Programlama Kılavuzu'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- properties [C#], abstract
- abstract properties [C#]
ms.assetid: 672a90eb-47b9-4ae0-9914-af53852fddcb
ms.openlocfilehash: 57fd2ed3a26bf5986f9c8a1a6cae6b041811e84c
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70970895"
---
# <a name="how-to-define-abstract-properties-c-programming-guide"></a><span data-ttu-id="8b517-102">Nasıl yapılır: Soyut özellikleri tanımlama (C# Programlama Kılavuzu)</span><span class="sxs-lookup"><span data-stu-id="8b517-102">How to: Define Abstract Properties (C# Programming Guide)</span></span>
<span data-ttu-id="8b517-103">Aşağıdaki örnek, [soyut](../../language-reference/keywords/abstract.md) özelliklerin nasıl tanımlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b517-103">The following example shows how to define [abstract](../../language-reference/keywords/abstract.md) properties.</span></span> <span data-ttu-id="8b517-104">Soyut özellik bildirimi, özellik erişimcilerinin bir uygulamasını sağlamaz--sınıfın özellikleri desteklediğini bildirir, ancak erişimci uygulamasını türetilmiş sınıflara bırakır.</span><span class="sxs-lookup"><span data-stu-id="8b517-104">An abstract property declaration does not provide an implementation of the property accessors -- it declares that the class supports properties, but leaves the accessor implementation to derived classes.</span></span> <span data-ttu-id="8b517-105">Aşağıdaki örnek, temel bir sınıftan devralınan soyut özelliklerin nasıl uygulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b517-105">The following example demonstrates how to implement the abstract properties inherited from a base class.</span></span>  
  
 <span data-ttu-id="8b517-106">Bu örnek, her biri ayrı ayrı derlenen üç dosyadan oluşur ve sonuçta elde edilen derlemeye sonraki derleme tarafından başvurulur:</span><span class="sxs-lookup"><span data-stu-id="8b517-106">This sample consists of three files, each of which is compiled individually and its resulting assembly is referenced by the next compilation:</span></span>  
  
- <span data-ttu-id="8b517-107">abstractshape.CS: `Shape` bir soyut `Area` özellik içeren sınıf.</span><span class="sxs-lookup"><span data-stu-id="8b517-107">abstractshape.cs: the `Shape` class that contains an abstract `Area` property.</span></span>  
  
- <span data-ttu-id="8b517-108">shapes.cs: `Shape` Sınıfının alt sınıfları.</span><span class="sxs-lookup"><span data-stu-id="8b517-108">shapes.cs: The subclasses of the `Shape` class.</span></span>  
  
- <span data-ttu-id="8b517-109">shapetest.cs: Bazı `Shape`türetilmiş nesnelerin bölümlerini görüntüleyen bir test programı.</span><span class="sxs-lookup"><span data-stu-id="8b517-109">shapetest.cs: A test program to display the areas of some `Shape`-derived objects.</span></span>  
  
 <span data-ttu-id="8b517-110">Örneği derlemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8b517-110">To compile the example, use the following command:</span></span>  
  
 `csc abstractshape.cs shapes.cs shapetest.cs`  
  
 <span data-ttu-id="8b517-111">Bu, shapetest. exe yürütülebilir dosyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8b517-111">This will create the executable file shapetest.exe.</span></span>  
  
## <a name="example"></a><span data-ttu-id="8b517-112">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b517-112">Example</span></span>  
 <span data-ttu-id="8b517-113">Bu dosya, türünün `Shape` `Area` `double`özelliğini içeren sınıfını bildirir.</span><span class="sxs-lookup"><span data-stu-id="8b517-113">This file declares the `Shape` class that contains the `Area` property of the type `double`.</span></span>  
  
 [!code-csharp[csProgGuideInheritance#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#1)]  
  
- <span data-ttu-id="8b517-114">Özelliğindeki değiştiriciler Özellik bildiriminin kendine yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8b517-114">Modifiers on the property are placed on the property declaration itself.</span></span> <span data-ttu-id="8b517-115">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8b517-115">For example:</span></span>  
  
    ```csharp  
    public abstract double Area  
    ```  
  
- <span data-ttu-id="8b517-116">Soyut bir özellik bildirirken (Bu örnekte olduğu `Area` gibi), yalnızca hangi özellik erişimcilerinin kullanılabilir olduğunu, ancak uygulamadıklarını belirtmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="8b517-116">When declaring an abstract property (such as `Area` in this example), you simply indicate what property accessors are available, but do not implement them.</span></span> <span data-ttu-id="8b517-117">Bu örnekte, yalnızca bir [Get](../../language-reference/keywords/get.md) erişimcisi bulunur, bu nedenle özellik salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="8b517-117">In this example, only a [get](../../language-reference/keywords/get.md) accessor is available, so the property is read-only.</span></span>  
  
## <a name="example"></a><span data-ttu-id="8b517-118">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b517-118">Example</span></span>  
 <span data-ttu-id="8b517-119">Aşağıdaki kod, öğesinin üç alt kümesini `Shape` ve kendi uygulamasını sağlamak için `Area` özelliği nasıl geçersiz kıladığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b517-119">The following code shows three subclasses of `Shape` and how they override the `Area` property to provide their own implementation.</span></span>  
  
 [!code-csharp[csProgGuideInheritance#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#2)]  
  
## <a name="example"></a><span data-ttu-id="8b517-120">Örnek</span><span class="sxs-lookup"><span data-stu-id="8b517-120">Example</span></span>  
 <span data-ttu-id="8b517-121">Aşağıdaki kod, bir dizi `Shape`türetilmiş nesne oluşturan ve alanlarının baskılarını yazdıran bir test programı gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b517-121">The following code shows a test program that creates a number of `Shape`-derived objects and prints out their areas.</span></span>  
  
 [!code-csharp[csProgGuideInheritance#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#3)]  
  
## <a name="see-also"></a><span data-ttu-id="8b517-122">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8b517-122">See also</span></span>

- [<span data-ttu-id="8b517-123">C# Programlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="8b517-123">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="8b517-124">Sınıflar ve Yapılar</span><span class="sxs-lookup"><span data-stu-id="8b517-124">Classes and Structs</span></span>](./index.md)
- [<span data-ttu-id="8b517-125">Soyut ve Korumalı Sınıflar ve Sınıf Üyeleri</span><span class="sxs-lookup"><span data-stu-id="8b517-125">Abstract and Sealed Classes and Class Members</span></span>](./abstract-and-sealed-classes-and-class-members.md)
- [<span data-ttu-id="8b517-126">Özellikler</span><span class="sxs-lookup"><span data-stu-id="8b517-126">Properties</span></span>](./properties.md)
