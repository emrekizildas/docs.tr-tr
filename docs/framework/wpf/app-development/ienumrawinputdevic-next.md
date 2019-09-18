---
title: IEnumRAWINPUTDEVIC:Next
ms.date: 03/30/2017
helpviewer_keywords:
- Next method [WPF]
ms.assetid: 3698b44d-510e-4d18-b32b-85f17188ee26
ms.openlocfilehash: c7450a9ababa9cf3cb02d572f5ed84f0791d74e4
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053405"
---
# <a name="ienumrawinputdevicnext"></a><span data-ttu-id="96973-102">IEnumRAWINPUTDEVIC:Next</span><span class="sxs-lookup"><span data-stu-id="96973-102">IEnumRAWINPUTDEVIC:Next</span></span>
<span data-ttu-id="96973-103">Numaralandırıcının listesindeki `celt` bir sonraki [çwınputdevice](/windows/desktop/api/winuser/ns-winuser-rawinputdevice) yapılarını sıralar `rgelt` ve bunları içinde numaralandırılmış öğelerin `pceltFetched`gerçek sayısıyla birlikte döndürür.</span><span class="sxs-lookup"><span data-stu-id="96973-103">Enumerates the next `celt` [RAWINPUTDEVICE](/windows/desktop/api/winuser/ns-winuser-rawinputdevice) structures in the enumerator's list, returning them in `rgelt` along with the actual number of enumerated elements in `pceltFetched`.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="96973-104">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="96973-104">Syntax</span></span>  
  
```cpp  
HRESULT Next(  
      [in] ULONG celt,  
      [out, size_is(celt), length_is(*pceltFetched)] RAWINPUTDEVICE *rgelt,  
      [out] ULONG *pceltFetched);  
```  
  
## <a name="parameters"></a><span data-ttu-id="96973-105">Parametreler</span><span class="sxs-lookup"><span data-stu-id="96973-105">Parameters</span></span>  
 `celt`  
  
 <span data-ttu-id="96973-106">'ndaki ' De `rgelt`döndürülen [ıwınputdevice](/windows/desktop/api/winuser/ns-winuser-rawinputdevice) yapılarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="96973-106">[in] Number of [RAWINPUTDEVICE](/windows/desktop/api/winuser/ns-winuser-rawinputdevice) structures returned in `rgelt`.</span></span>  
  
 `rgelt`  
  
 <span data-ttu-id="96973-107">dışı Numaralandırılmış ıRWıNPUTDEVICE yapılarını almak için bir boyut dizisi (veya daha büyük).</span><span class="sxs-lookup"><span data-stu-id="96973-107">[out] Array of size celt (or larger) to receive enumerated RAWINPUTDEVICE structures.</span></span>  
  
 `pceltFetched`  
  
 <span data-ttu-id="96973-108">dışı Gerçekte içinde `rgelt`sağlanan öğe sayısına yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="96973-108">[out] Pointer to the number of elements actually supplied in `rgelt`.</span></span> <span data-ttu-id="96973-109">`NULL` Eğer`rgelt` ise, arayan içinde geçiş yapabilir.</span><span class="sxs-lookup"><span data-stu-id="96973-109">Caller can pass in `NULL` if `rgelt` is one.</span></span>  
  
## <a name="property-valuereturn-value"></a><span data-ttu-id="96973-110">Özellik Değeri/Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="96973-110">Property Value/Return Value</span></span>  
 <span data-ttu-id="96973-111">HRESULT Sağlanan öğe sayısı ise `celt`S_OK; Aksi halde S_FALSE.</span><span class="sxs-lookup"><span data-stu-id="96973-111">HRESULT: S_OK if the number of elements supplied is `celt`; S_FALSE otherwise.</span></span>
