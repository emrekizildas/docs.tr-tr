---
title: 'Özel durumlar: try...finally İfadesi'
description: F# ' TRY... finally ' ifadesi bir kod bloğu özel durum oluşturursa bile Temizleme kodunu yürütmenize olanak sağlar.
ms.date: 05/16/2016
ms.openlocfilehash: 0ddb64ac13b307404864ec5b54f26fd8a7a3d7d8
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083001"
---
# <a name="exceptions-the-tryfinally-expression"></a>Özel durumlar: try...finally İfadesi

İfade `try...finally` , bir kod bloğu özel durum oluşturursa bile temizleme kodu çalıştırmanızı sağlar.

## <a name="syntax"></a>Sözdizimi

```fsharp
try
    expression1
finally
    expression2
```

## <a name="remarks"></a>Açıklamalar

İfadesi, *İfade1*öğesinin yürütülmesi sırasında bir özel durumun oluşturulup oluşturulmadığına bakılmaksızın, Önceki sözdiziminde İfade2 içindeki kodu yürütmek için kullanılabilir. `try...finally`

*Deyim2* türü tüm ifadenin değerine katkıda bulunmaz; bir özel durum gerçekleşmediğinde döndürülen tür *İfade1*' deki son değerdir. Bir özel durum oluştuğunda, hiçbir değer döndürülmez ve denetim akışı, çağrı yığınını yukarı eşleşen bir sonraki özel durum işleyicisine aktarır. Hiçbir özel durum işleyici bulunmazsa program sonlanır. Eşleşen bir işleyicisindeki kod yürütülmeden veya program sonlandırıldığında, `finally` daldaki kod yürütülür.

Aşağıdaki kod, `try...finally` ifadesinin kullanımını gösterir.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5701.fs)]

Konsola giden çıkış aşağıdaki gibidir.

```console
Closing stream
Exception handled.
```

Çıktıdan görebileceğiniz gibi, akış, dıştaki özel durum işlendikten önce kapatılmıştır ve dosya `test.txt` , aktarılan özel durum olsa bile, arabelleklerin temizlendiğini ve diske yazıldığını belirten metni `test1`içerir. dış özel durum işleyicisine denetim.

Yapının yapıdan ayrı bir yapı `try...finally` olduğunu unutmayın. `try...with` Bu nedenle, kodunuz hem `with` blok `finally` hem de blok gerektiriyorsa, aşağıdaki kod örneğinde olduğu gibi iki yapıları iç içe almanız gerekir.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5702.fs)]

Sıra ifadeleri ve zaman uyumsuz iş akışları dahil hesaplama ifadeleri bağlamında, **deneyin... finally** ifadeleri özel bir uygulamaya sahip olabilir. Daha fazla bilgi için bkz. [Hesaplama ifadeleri](../computation-expressions.md).

## <a name="see-also"></a>Ayrıca bkz.

- [Özel Durum İşleme](index.md)
- [Özel Durumlar: `try...with` İfade](the-try-with-expression.md)
