---
title: COR_ACTIVE_FUNCTION Yapısı
ms.date: 03/30/2017
api_name:
- COR_ACTIVE_FUNCTION
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_ACTIVE_FUNCTION
helpviewer_keywords:
- COR_ACTIVE_FUNCTION structure [.NET Framework debugging]
ms.assetid: ed86185f-2152-459c-961f-10c06d62e83f
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 50dd4acece43628b20b6bc50a539ee197e865855
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274152"
---
# <a name="cor_active_function-structure"></a><span data-ttu-id="d236a-102">COR_ACTIVE_FUNCTION Yapısı</span><span class="sxs-lookup"><span data-stu-id="d236a-102">COR_ACTIVE_FUNCTION Structure</span></span>
<span data-ttu-id="d236a-103">Şu anda bir iş parçacığının çerçevelerinde etkin olan işlevlerle ilgili bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="d236a-103">Contains information about the functions that are currently active in a thread's frames.</span></span> <span data-ttu-id="d236a-104">Bu yapı, [ICorDebugThread2:: GetActiveFunctions](icordebugthread2-getactivefunctions-method.md) yöntemi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d236a-104">This structure is used by the [ICorDebugThread2::GetActiveFunctions](icordebugthread2-getactivefunctions-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d236a-105">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d236a-105">Syntax</span></span>  
  
```cpp  
typedef struct  _COR_ACTIVE_FUNCTION {  
    ICorDebugAppDomain   *pAppDomain;  
    ICorDebugModule      *pModule;  
    ICorDebugFunction2   *pFunction;  
    ULONG32              ilOffset;  
    ULONG32              flags;  
} COR_ACTIVE_FUNCTION;  
```  
  
## <a name="members"></a><span data-ttu-id="d236a-106">Üyeler</span><span class="sxs-lookup"><span data-stu-id="d236a-106">Members</span></span>  
  
|<span data-ttu-id="d236a-107">Üye</span><span class="sxs-lookup"><span data-stu-id="d236a-107">Member</span></span>|<span data-ttu-id="d236a-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d236a-108">Description</span></span>|  
|------------|-----------------|  
|`pAppDomain`|<span data-ttu-id="d236a-109">`ilOffset` Alanın uygulama etki alanı sahibine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d236a-109">Pointer to the application domain owner of the `ilOffset` field.</span></span>|  
|`pModule`|<span data-ttu-id="d236a-110">`ilOffset` Alanın modül sahibine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d236a-110">Pointer to the module owner of the `ilOffset` field.</span></span>|  
|`pFunction`|<span data-ttu-id="d236a-111">`ilOffset` Alanın işlev sahibine yönelik işaretçi.</span><span class="sxs-lookup"><span data-stu-id="d236a-111">Pointer to the function owner of the `ilOffset` field.</span></span>|  
|`ilOffset`|<span data-ttu-id="d236a-112">Çerçevenin Microsoft ara dili (MSIL) kayması.</span><span class="sxs-lookup"><span data-stu-id="d236a-112">The Microsoft intermediate language (MSIL) offset of the frame.</span></span>|  
|`flags`|<span data-ttu-id="d236a-113">Gelecekteki genişletilebilirlik için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d236a-113">Reserved for future extensibility.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="d236a-114">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="d236a-114">Requirements</span></span>  
 <span data-ttu-id="d236a-115">**Platform** Bkz. [sistem gereksinimleri](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="d236a-115">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d236a-116">**Üst bilgi** CorDebug. IDL</span><span class="sxs-lookup"><span data-stu-id="d236a-116">**Header:** CorDebug.idl</span></span>  
  
 <span data-ttu-id="d236a-117">**Kitaplığı** Corguid. lib</span><span class="sxs-lookup"><span data-stu-id="d236a-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d236a-118">**.NET Framework sürümleri:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d236a-118">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d236a-119">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d236a-119">See also</span></span>

- [<span data-ttu-id="d236a-120">Hata Ayıklama Yapıları</span><span class="sxs-lookup"><span data-stu-id="d236a-120">Debugging Structures</span></span>](debugging-structures.md)
- [<span data-ttu-id="d236a-121">Hata Ayıklama</span><span class="sxs-lookup"><span data-stu-id="d236a-121">Debugging</span></span>](index.md)
