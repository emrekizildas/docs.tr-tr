---
title: CorDebugChainReason Numaralandırması
ms.date: 03/30/2017
api_name:
- CorDebugChainReason
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugChainReason
helpviewer_keywords:
- CorDebugChainReason enumeration [.NET Framework debugging]
ms.assetid: c915da51-50b2-41df-841a-2b971f4d0975
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fce803544b393ac2c441779183cbf49d4c39bdae
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71273986"
---
# <a name="cordebugchainreason-enumeration"></a><span data-ttu-id="9caa0-102">CorDebugChainReason Numaralandırması</span><span class="sxs-lookup"><span data-stu-id="9caa0-102">CorDebugChainReason Enumeration</span></span>
<span data-ttu-id="9caa0-103">Bir çağrı zincirinin başlatılması için neden veya nedenleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="9caa0-103">Indicates the reason or reasons for the initiation of a call chain.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9caa0-104">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9caa0-104">Syntax</span></span>  
  
```cpp  
typedef enum CorDebugChainReason {  
    CHAIN_NONE              = 0x000,  
    CHAIN_CLASS_INIT        = 0x001,  
    CHAIN_EXCEPTION_FILTER  = 0x002,  
    CHAIN_SECURITY          = 0x004,  
    CHAIN_CONTEXT_POLICY    = 0x008,  
    CHAIN_INTERCEPTION      = 0x010,  
    CHAIN_PROCESS_START     = 0x020,  
    CHAIN_THREAD_START      = 0x040,  
    CHAIN_ENTER_MANAGED     = 0x080,  
    CHAIN_ENTER_UNMANAGED   = 0x100,  
    CHAIN_DEBUGGER_EVAL     = 0x200,  
    CHAIN_CONTEXT_SWITCH    = 0x400,  
    CHAIN_FUNC_EVAL         = 0x800  
} CorDebugChainReason;  
```  
  
## <a name="members"></a><span data-ttu-id="9caa0-105">Üyeler</span><span class="sxs-lookup"><span data-stu-id="9caa0-105">Members</span></span>  
  
|<span data-ttu-id="9caa0-106">Üye</span><span class="sxs-lookup"><span data-stu-id="9caa0-106">Member</span></span>|<span data-ttu-id="9caa0-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9caa0-107">Description</span></span>|  
|------------|-----------------|  
|`CHAIN_NONE`|<span data-ttu-id="9caa0-108">Hiçbir çağrı zinciri başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-108">No call chain has been initiated.</span></span>|  
|`CHAIN_CLASS_INIT`|<span data-ttu-id="9caa0-109">Zincir bir Oluşturucu tarafından başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-109">The chain was initiated by a constructor.</span></span>|  
|`CHAIN_EXCEPTION_FILTER`|<span data-ttu-id="9caa0-110">Zincir bir özel durum filtresi tarafından başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-110">The chain was initiated by an exception filter.</span></span>|  
|`CHAIN_SECURITY`|<span data-ttu-id="9caa0-111">Zincir, güvenliği zorlayan kod tarafından başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-111">The chain was initiated by code that enforces security.</span></span>|  
|`CHAIN_CONTEXT_POLICY`|<span data-ttu-id="9caa0-112">Zincir bir bağlam ilkesi tarafından başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-112">The chain was initiated by a context policy.</span></span>|  
|`CHAIN_INTERCEPTION`|<span data-ttu-id="9caa0-113">Kullanılmadı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-113">Not used.</span></span>|  
|`CHAIN_PROCESS_START`|<span data-ttu-id="9caa0-114">Kullanılmadı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-114">Not used.</span></span>|  
|`CHAIN_THREAD_START`|<span data-ttu-id="9caa0-115">Zincir, iş parçacığı yürütme başlangıcı tarafından başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-115">The chain was initiated by the start of a thread execution.</span></span>|  
|`CHAIN_ENTER_MANAGED`|<span data-ttu-id="9caa0-116">Zincir, yönetilen koda giriş tarafından başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-116">The chain was initiated by entry into managed code.</span></span>|  
|`CHAIN_ENTER_UNMANAGED`|<span data-ttu-id="9caa0-117">Zincir, yönetilmeyen koda giriş tarafından başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-117">The chain was initiated by entry into unmanaged code.</span></span>|  
|`CHAIN_DEBUGGER_EVAL`|<span data-ttu-id="9caa0-118">Kullanılmadı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-118">Not used.</span></span>|  
|`CHAIN_CONTEXT_SWITCH`|<span data-ttu-id="9caa0-119">Kullanılmadı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-119">Not used.</span></span>|  
|`CHAIN_FUNC_EVAL`|<span data-ttu-id="9caa0-120">Zincir bir işlev değerlendirmesi tarafından başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="9caa0-120">The chain was initiated by a function evaluation.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="9caa0-121">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="9caa0-121">Remarks</span></span>  
 <span data-ttu-id="9caa0-122">Bir çağrı zincirinin başlatılması nedenlerini belirlemek için [ıcordebugzincirine:: GetReason](icordebugchain-getreason-method.md) metodunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9caa0-122">Use the [ICorDebugChain::GetReason](icordebugchain-getreason-method.md) method to ascertain the reasons for the initiation of a call chain.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9caa0-123">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="9caa0-123">Requirements</span></span>  
 <span data-ttu-id="9caa0-124">**Platform** Bkz. [sistem gereksinimleri](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="9caa0-124">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9caa0-125">**Üst bilgi** CorDebug. IDL, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="9caa0-125">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="9caa0-126">**Kitaplığı** Corguid. lib</span><span class="sxs-lookup"><span data-stu-id="9caa0-126">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="9caa0-127">**.NET Framework sürümleri:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9caa0-127">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9caa0-128">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="9caa0-128">See also</span></span>

- [<span data-ttu-id="9caa0-129">Hata Ayıklama Sabit Listeleri</span><span class="sxs-lookup"><span data-stu-id="9caa0-129">Debugging Enumerations</span></span>](debugging-enumerations.md)
