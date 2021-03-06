---
title: 'Nasıl yapılır: özel durumları yakalamak için try-catch bloğunu kullanma'
ms.date: 02/06/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- exceptions, try/catch blocks
- try blocks
- try/catch blocks
- catch blocks
ms.assetid: a3ce6dfd-1f64-471b-8ad8-8cfaf406275d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: eaa389f461e70aae41f2e09437fd725a3bcefa5e
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696726"
---
# <a name="how-to-use-the-trycatch-block-to-catch-exceptions"></a>Özel durumları yakalamak için try/catch bloğunu kullanma

@No__t-0 bloğunda bir özel durum oluşturabilen veya oluşturabilen herhangi bir kod deyimini yerleştirin ve `try` bloğunun altındaki bir veya daha fazla `catch` bloğunda özel durumu veya özel durumları işlemek için kullanılan deyimleri yerleştirin. Her `catch` bloğu özel durum türünü içerir ve bu özel durum türünü işlemek için gereken ek deyimler içerebilir.

Aşağıdaki örnekte, bir <xref:System.IO.StreamReader> *Data. txt* adlı bir dosya açar ve dosyadan bir satır alır. Kod üç özel durum oluşturmasından dolayı, `try` bloğuna yerleştirilir. Üç `catch` blok özel durumları yakalar ve sonuçları konsola görüntüleyerek işler.

[!code-csharp[CatchException#3](~/samples/snippets/csharp/VS_Snippets_CLR/CatchException/CS/catchexception2.cs#3)]
[!code-vb[CatchException#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/CatchException/VB/catchexception2.vb#3)]

Ortak dil çalışma zamanı (CLR), `catch` blokları tarafından işlenmeyen özel durumları yakalar. CLR tarafından bir özel durum yakalanmışsa, CLR yapılandırmanıza bağlı olarak aşağıdaki sonuçlardan biri ortaya çıkabilir:

- **Hata ayıklama** iletişim kutusu görüntülenir.
- Program yürütmeyi durduruyor ve özel durum bilgileri içeren bir iletişim kutusu görünür.
- Bir hata [Standart hata çıkış akışına](xref:System.Console.Error)yazdırılır.

> [!NOTE]
> Çoğu kod bir özel durum oluşturabilir ve <xref:System.OutOfMemoryException> gibi bazı özel durumlar, her zaman CLR tarafından oluşturulabilir. Uygulamalar bu özel durumlarla uğraşmak zorunda olmasa da, diğer kullanıcılar tarafından kullanılacak kitaplıkları yazma olasılıklarının farkında olun. @No__t-0 bloğunda kodun ne zaman ayarlanacağı hakkında öneriler için bkz. [özel durumlar Için En Iyi uygulamalar](best-practices-for-exceptions.md).

## <a name="see-also"></a>Ayrıca bkz.

- [Özel Durumlar](index.md)
- [.NET 'te g/ç hatalarını işleme](../io/handling-io-errors.md)
