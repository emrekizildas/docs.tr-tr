---
title: COR_IL_MAP Yapısı
ms.date: 03/30/2017
api_name:
- COR_IL_MAP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_IL_MAP
helpviewer_keywords:
- COR_IL_MAP structure [.NET Framework debugging]
ms.assetid: 534ebc17-963d-4b26-8375-8cd940281db3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5ae4c5743b01c4a9087323678d315473631cb32f
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274045"
---
# <a name="cor_il_map-structure"></a>COR_IL_MAP Yapısı
Bir işlevin göreli uzaklığının değişikliklerini belirtir.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
typedef struct _COR_IL_MAP {  
    ULONG32 oldOffset;   
    ULONG32 newOffset;   
    BOOL    fAccurate;  
} COR_IL_MAP;  
```  
  
## <a name="members"></a>Üyeler  
  
|Üye|Açıklama|  
|------------|-----------------|  
|`oldOffset`|İşlevin başlangıcına göre eski Microsoft ara dili (MSIL) uzaklıkları.|  
|`newOffset`|İşlevin başlangıcına göre yeni MSIL fark.|  
|`fAccurate`|`true`eşlemenin doğru olduğu bilinmektedir; Aksi takdirde `false`,.|  
  
## <a name="remarks"></a>Açıklamalar  
 Haritanın biçimi aşağıdaki gibidir: Hata ayıklayıcı, orijinal, `oldOffset` değiştirilmemiş MSIL kodu içindeki bir MSIL denkleşeceğini varsayacaktır. `newOffset` Parametresi, yeni ve belgelenmiş kod içindeki karşılık gelen MSIL sapmasını ifade eder.  
  
 Adımların düzgün çalışması için aşağıdaki gereksinimlerin karşılanması gerekir:  
  
- Haritanın artan sırada sıralanması gerekir.  
  
- Belgelenmiş MSIL kodu yeniden sıralanmaz.  
  
- Orijinal MSIL kodu kaldırılmamalıdır.  
  
- Map, program veritabanı (PDB) dosyasındaki tüm sıra noktalarını eşlemek için girdiler içermelidir.  
  
 Eşleme, eksik girişleri enterpolamıyor. Aşağıdaki örnek bir eşlemeyi ve sonuçlarını gösterir.  
  
 Harita  
  
- 0 eski fark, 0 yeni fark  
  
- 5 eski fark, 10 yeni fark  
  
- 9 eski fark, 20 yeni fark  
  
 Sonucunun  
  
- 0, 1, 2, 3 veya 4 ' ün eski bir kayması, 0 ' ın yeni bir uzaklığa eşlenir.  
  
- 5, 6, 7 veya 8 ' in eski bir kayması, yeni% 10 ' a eşlenir.  
  
- Daha eski bir 9 veya üzeri fark, 20. yeni uzaklığa eşlenir.  
  
- 0, 1, 2, 3, 4, 5, 6, 7, 8 ya da 9 ' un yeni bir kayması, 0 ' dan eski uzaklığa eşlenir.  
  
- 10, 11, 12, 13, 14, 15, 16, 17, 18 veya 19 ' un yeni bir kayması, 5 eski uzaklığa eşlenir.  
  
- 20 veya üzeri yeni bir konum, eski konum 9 ' A eşlenir.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platform** Bkz. [sistem gereksinimleri](../../get-started/system-requirements.md).  
  
 **Üst bilgi** CorDebug. IDL, CorProf. IDL  
  
 **Kitaplığı** Corguid. lib  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Hata Ayıklama Yapıları](debugging-structures.md)
- [Hata Ayıklama](index.md)
