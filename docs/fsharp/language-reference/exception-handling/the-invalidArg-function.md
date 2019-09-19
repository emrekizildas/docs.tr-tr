---
title: 'Özel durumlar: invalidArg İşlevi'
description: F# ' InvalidArg ' işlevinin bir bağımsız değişken özel durumu üretme hakkında bilgi edinin.
ms.date: 05/16/2016
ms.openlocfilehash: 6b1c5fdb5a541da336977d3a67d471302edb36b6
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083021"
---
# <a name="exceptions-the-invalidarg-function"></a>Özel durumlar: invalidArg İşlevi

`invalidArg` İşlev bir bağımsız değişken özel durumu oluşturur.

## <a name="syntax"></a>Sözdizimi

```fsharp
invalidArg parameter-name error-message-string
```

## <a name="remarks"></a>Açıklamalar

Önceki söz diziminde parametre adı, bağımsız değişkeni geçersiz olan parametre adına sahip bir dizedir. *Hata-ileti-dize* , sabit bir dize veya türünde `string`bir değer. Özel durum nesnesinin `Message` özelliği olur.

Tarafından `invalidArg` oluşturulan özel durum bir `System.ArgumentException` istisnadır. Aşağıdaki kod, bir özel durum `invalidArg` oluşturmak için kullanımını gösterir.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6101.fs)]

Çıktı, izleyen bir yığın izlemesi (gösterilmez) tarafından gerçekleştirilir.

```console
December
January
System.ArgumentException: Month parameter out of range.
```

## <a name="see-also"></a>Ayrıca bkz.

- [Özel Durum İşleme](index.md)
- [Özel Durum Türleri](exception-types.md)
- [Özel Durumlar: `try...with` İfade](the-try-with-expression.md)
- [Özel Durumlar: `try...finally` İfade](the-try-finally-expression.md)
- [Özel durumlar: `raise` işlev](the-raise-function.md)
- [Özel Durumlar: `failwith` İşlevi](the-failwith-function.md)
