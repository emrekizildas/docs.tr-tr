---
title: 'Nasıl yapılır: dize içinde arama-Visual Basic'
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], finding
- strings [Visual Basic], searching
- examples [Visual Basic], strings
ms.assetid: ae4c79e0-08ea-489f-bdb2-5eb6d355f284
ms.openlocfilehash: fe9e50dc5458fdf8546094e5f41c2f001f1d2791
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700068"
---
# <a name="how-to-search-within-a-string-visual-basic"></a><span data-ttu-id="41204-102">Nasıl yapılır: dize içinde arama (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="41204-102">How to: search within a string (Visual Basic)</span></span>

<span data-ttu-id="41204-103">Bu makalede, Visual Basic bir dize içinde aramanın nasıl yapılacağı hakkında bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="41204-103">This article shows an example of how to search within a string in Visual Basic.</span></span>

## <a name="example"></a><span data-ttu-id="41204-104">Örnek</span><span class="sxs-lookup"><span data-stu-id="41204-104">Example</span></span>

<span data-ttu-id="41204-105">Bu örnek, bir alt dizenin ilk geçtiği dizini raporlamak için bir <xref:System.String> nesnesi üzerinde <xref:System.String.IndexOf%2A> yöntemini çağırır:</span><span class="sxs-lookup"><span data-stu-id="41204-105">This example calls the <xref:System.String.IndexOf%2A> method on a <xref:System.String> object to report the index of the first occurrence of a substring:</span></span>

 [!code-vb[VbVbalrStrings#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#71)]

## <a name="robust-programming"></a><span data-ttu-id="41204-106">Güçlü programlama</span><span class="sxs-lookup"><span data-stu-id="41204-106">Robust programming</span></span>

<span data-ttu-id="41204-107">@No__t-0 yöntemi, alt dizenin ilk oluşumunun ilk karakterinin konumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="41204-107">The <xref:System.String.IndexOf%2A> method returns the location of the first character of the first occurrence of the substring.</span></span> <span data-ttu-id="41204-108">Dizin 0 tabanlıdır, yani bir dizenin ilk karakterinin 0 dizinine sahip olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="41204-108">The index is 0-based, which means the first character of a string has an index of 0.</span></span>

<span data-ttu-id="41204-109">@No__t-0 alt dizeyi bulamazsa,-1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="41204-109">If <xref:System.String.IndexOf%2A> does not find the substring, it returns -1.</span></span>

<span data-ttu-id="41204-110">@No__t-0 yöntemi, büyük/küçük harfe duyarlıdır ve geçerli kültürü kullanır.</span><span class="sxs-lookup"><span data-stu-id="41204-110">The <xref:System.String.IndexOf%2A> method is case-sensitive and uses the current culture.</span></span>

<span data-ttu-id="41204-111">En iyi hata denetimi için, bir TRY `Try` bloğunda dize aramasını kapsamak isteyebilirsiniz [... Yakala... Finally deyiminin](../../../language-reference/statements/try-catch-finally-statement.md) oluşturulması.</span><span class="sxs-lookup"><span data-stu-id="41204-111">For optimal error control, you might want to enclose the string search in the `Try` block of a [Try...Catch...Finally Statement](../../../language-reference/statements/try-catch-finally-statement.md) construction.</span></span>

## <a name="see-also"></a><span data-ttu-id="41204-112">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="41204-112">See also</span></span>

- <xref:System.String.IndexOf%2A>
- [<span data-ttu-id="41204-113">Try...Catch...Finally Deyimi</span><span class="sxs-lookup"><span data-stu-id="41204-113">Try...Catch...Finally Statement</span></span>](../../../language-reference/statements/try-catch-finally-statement.md)
- [<span data-ttu-id="41204-114">Visual Basic dizelere giriş</span><span class="sxs-lookup"><span data-stu-id="41204-114">Introduction to Strings in Visual Basic</span></span>](introduction-to-strings.md)
- [<span data-ttu-id="41204-115">Dizeler</span><span class="sxs-lookup"><span data-stu-id="41204-115">Strings</span></span>](index.md)
