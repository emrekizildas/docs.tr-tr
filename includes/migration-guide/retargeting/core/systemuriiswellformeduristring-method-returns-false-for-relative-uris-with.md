---
ms.openlocfilehash: 734041f5921571cd11225a359e794526cbd8d0e1
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62093639"
---
### <a name="systemuriiswellformeduristring-method-returns-false-for-relative-uris-with-a-colon-char-in-first-segment"></a>System.Uri.IsWellFormedUriString yöntemi, bir iki nokta üst üste char ilk kesimdeki ile göreli URI'ler için false değerini döndürür

|   |   |
|---|---|
|Ayrıntılar|.NET Framework 4.5 ile başlayarak <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)> ile göreli bir URI'leri değerlendirir bir <code>:</code> biçimlendirilmemiş gibi kendi ilk segment olarak. Bu farklıdır <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=name> davranış uymak için RFC3986 yapılmadan .NET Framework 4.0.|
|Öneri|(Gibi diğer birçok URI değişiklik) Bu değişiklik, yalnızca .NET Framework 4.5 (veya sonrası) hedefleyen uygulamaları etkiler. Eski davranışı kullanmaya devam etmek için uygulamayı .NET Framework 4.0 karşı hedefleyin. Alternatif olarak, URI'ın çağırmadan önce tarama <xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=name> aranırken <code>:</code> karakterler, eski davranışı arzu ise doğrulama amacıyla kaldırmak isteyebilirsiniz.|
|Kapsam|İkincil|
|Sürüm|4,5|
|Tür|Yeniden Hedefleme|
|Etkilenen API’ler|<ul><li><xref:System.Uri.IsWellFormedUriString(System.String,System.UriKind)?displayProperty=nameWithType></li></ul>|
