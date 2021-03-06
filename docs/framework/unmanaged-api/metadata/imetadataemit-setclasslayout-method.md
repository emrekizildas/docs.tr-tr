---
title: IMetaDataEmit::SetClassLayout Yöntemi
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetClassLayout
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetClassLayout
helpviewer_keywords:
- IMetaDataEmit::SetClassLayout method [.NET Framework metadata]
- SetClassLayout method [.NET Framework metadata]
ms.assetid: 2576c449-388d-4434-a0e1-9f53991e11b6
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c455b5196ceafef924de59e9134b89ed62455520
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67737219"
---
# <a name="imetadataemitsetclasslayout-method"></a>IMetaDataEmit::SetClassLayout Yöntemi
Önceki bir çağrı tarafından tanımlanan bir sınıf için alanlarının düzenini tamamlandıktan [DefineTypeDef yöntemi](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetypedef-method.md).  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
HRESULT SetClassLayout (  
    [in]  mdTypeDef           td,   
    [in]  DWORD               dwPackSize,   
    [in]  COR_FIELD_OFFSET    rFieldOffsets[],   
    [in]  ULONG               ulClassSize   
);  
```  
  
## <a name="parameters"></a>Parametreler  
 `td`  
 [in] Bir `mdTypeDef` belirteci dışı sınıfını belirtir.  
  
 `dwPackSize`  
 [in] Paketleme boyutu: 1, 2, 4, 8 veya 16 bayt sayısı. Bitişik alanları arasında bulunan bayt sayısını paketleme boyutudur.  
  
 `rFieldOffsets`  
 [in] Bir dizi [cor_fıeld_offset](../../../../docs/framework/unmanaged-api/metadata/cor-field-offset-structure.md) yapıları, her biri belirtir sınıfının bir alanı ve alan içindeki sınıf uzaklığını. Dizi sonlandırmak `mdTokenNil`.  
  
 `ulClassSize`  
 [in] Sınıf bayt cinsinden boyutu.  
  
## <a name="remarks"></a>Açıklamalar  
 Sınıfı, başlangıçta çağırarak tanımlanır [Imetadataemit::definetypedef](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetypedef-method.md) yöntemi ve sınıf alanlar için üç düzenlerden birini belirterek: otomatik, sıralı ya da açık. Normalde, otomatik düzeni kullanma ve alanları düzenlemek için en iyi yolu seçin çalışma zamanının.  
  
 Ancak, kodunuz yönetilmeyen düzenleme göre düzenlendiği alanları isteyebilirsiniz. Bu durumda, doğrudan ya da ardışık düzen ve çağrı seçin `SetClassLayout` alanlarının düzenini tamamlamak için:  
  
- Ardışık Düzen: Paketleme boyutu belirtin. Alana göre doğal boyutu veya paketleme boyutu, hangi alanın daha küçük uzaklığı sonuçlarında hizalanır. Ayarlama `rFieldOffsets` ve `ulClassSize` sıfır.  
  
- Açık düzeni: Her alanın bir uzaklık belirtin ya da sınıf boyutu ve paketleme boyutu belirtin.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz: [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** COR.h  
  
 **Kitaplığı:** Bir kaynak olarak MSCorEE.dll kullanılan  
  
 **.NET framework sürümleri:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [IMetaDataEmit Arabirimi](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 Arabirimi](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
