---
title: ILCodeKind Numaralandırması
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ILCodeKind
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: b91765e4-82db-46f9-a6dc-6b80610276af
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fea08331fffb85c91721d60764bae8bfe8b30e27
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928809"
---
# <a name="ilcodekind-enumeration"></a><span data-ttu-id="a71b1-102">ILCodeKind Numaralandırması</span><span class="sxs-lookup"><span data-stu-id="a71b1-102">ILCodeKind Enumeration</span></span>
<span data-ttu-id="a71b1-103">[.NET Framework 4.5.2 ve sonraki sürümlerde desteklenir]</span><span class="sxs-lookup"><span data-stu-id="a71b1-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
 <span data-ttu-id="a71b1-104">Hata ayıklayıcının profil oluşturucu ReJIT araçları 'nda eklenen yerel değişkenlere veya koda erişip erişemeyeceğini belirten değerler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a71b1-104">Provides values that specify whether the debugger is able to access local variables or code added in profiler ReJIT instrumentation.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a71b1-105">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a71b1-105">Syntax</span></span>  
  
```cpp
typedef enum ILCodeKind {  
   ILCODE_ORIGINAL_IL = 0x1,  
   ILCODE_REJIT_IL = 0x2,  
} ILCodeKind;  
```  
  
## <a name="members"></a><span data-ttu-id="a71b1-106">Üyeler</span><span class="sxs-lookup"><span data-stu-id="a71b1-106">Members</span></span>  
  
|<span data-ttu-id="a71b1-107">Üye adı</span><span class="sxs-lookup"><span data-stu-id="a71b1-107">Member name</span></span>|<span data-ttu-id="a71b1-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a71b1-108">Description</span></span>|  
|-----------------|-----------------|  
|`ILCODE_ORIGINAL_IL`|<span data-ttu-id="a71b1-109">Hata ayıklayıcının, ReJIT araçlarından bilgilere erişimi yok.</span><span class="sxs-lookup"><span data-stu-id="a71b1-109">The debugger does not have access to information from ReJIT instrumentation.</span></span>|  
|`ILCODE_REJIT_IL`|<span data-ttu-id="a71b1-110">Hata ayıklayıcının, ReJIT araçlarından bilgilere erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="a71b1-110">The debugger has access to information from ReJIT instrumentation.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="a71b1-111">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="a71b1-111">Remarks</span></span>  
 <span data-ttu-id="a71b1-112">Hata ayıklayıcının profil oluşturucu `ILCodeKind` ReJIT araçları ' na eklenen değişkenlere erişip [erişemeyeceğini ve](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-enumeratelocalvariablesex-method.md) bunun [](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-getlocalvariableex-method.md) için [bir numaralandırma üyesi olup olmadığını ](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-getcodeex-method.md)Hata ayıklayıcının IŞARETLENMIŞ Il 'ye erişip erişemeyeceğini belirleme GetCodeEx yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a71b1-112">A member of the `ILCodeKind` enumeration can be passed to the [EnumerateLocalVariablesEx](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-enumeratelocalvariablesex-method.md) and [GetLocalVariableEx](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-getlocalvariableex-method.md) methods to determine whether the debugger can access variables added in profiler ReJIT instrumentation, and to the [GetCodeEx](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-getcodeex-method.md) method to determine whether the debugger can access instrumented IL.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a71b1-113">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="a71b1-113">Requirements</span></span>  
 <span data-ttu-id="a71b1-114">**Platform** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a71b1-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a71b1-115">**Üst bilgi** CorDebug. IDL, CorDebug. h</span><span class="sxs-lookup"><span data-stu-id="a71b1-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a71b1-116">**Kitaplığı** Corguid. lib</span><span class="sxs-lookup"><span data-stu-id="a71b1-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a71b1-117">**.NET Framework sürümleri:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a71b1-117">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a71b1-118">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a71b1-118">See also</span></span>

- [<span data-ttu-id="a71b1-119">Hata Ayıklama Sabit Listeleri</span><span class="sxs-lookup"><span data-stu-id="a71b1-119">Debugging Enumerations</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
- [<span data-ttu-id="a71b1-120">ICorDebugILFrame4 Arabirimi</span><span class="sxs-lookup"><span data-stu-id="a71b1-120">ICorDebugILFrame4 Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-interface.md)
- [<span data-ttu-id="a71b1-121">ReJIT: Nasıl yapılır Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="a71b1-121">ReJIT: A How-To Guide</span></span>](https://blogs.msdn.microsoft.com/davbr/2011/10/12/rejit-a-how-to-guide/)
