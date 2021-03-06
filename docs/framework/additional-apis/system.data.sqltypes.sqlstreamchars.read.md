---
title: SqlStreamChars.Read (Char [], Int32, Int32) yöntemi (System.Data.SqlTypes)
author: stevestein
ms.author: sstein
ms.date: 12/20/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlStreamChars.Read
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: df715f622f874b3c9297c421eab9f4c7504e696b
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65634313"
---
# <a name="sqlstreamcharsreadchar-int32-int32-method"></a>SqlStreamChars.Read (Char [], Int32, Int32) yöntemi

Sonraki karakter kümesini, türetilen bir sınıfta geçersiz kılındığında, giriş akışından okur. Bu yöntemi içeren derlemenin SQLAccess.dll bir arkadaş ilişkisi vardır. Bu, SQL Server tarafından kullanıma yöneliktir. Diğer veritabanları için veritabanı tarafından sağlanan barındırma mekanizmasına kullanın.

```csharp
public abstract int Read (char[] buffer, int offset, int count);
```

## <a name="parameters"></a>Parametreler

`buffer`\
Okunacak karakter dizisi.

`offset`\
Kaynağa göre bir uzaklık.

`count`\
Geçerli akışından okunacak karakter sayısı.

## <a name="returns"></a>Döndürür

<xref:System.Int32>\
Arabelleğe okunan karakter sayısı.

## <a name="remarks"></a>Açıklamalar

> [!WARNING]
> `SqlStreamChars.Read` Yöntemi private olduğuna ve kodunuzda doğrudan kullanılmak üzere tasarlanmamıştır.
>
> Microsoft hiçbir koşulda, bir üretim uygulamasında bu alanı kullanımını desteklemez.

## <a name="requirements"></a>Gereksinimler

**Namespace:** <xref:System.Data.SqlTypes>

**Derleme:** System.Data (içinde System.Data.dll)

**.NET framework sürümleri:** 2.0 sürümünden itibaren kullanılabilir.
