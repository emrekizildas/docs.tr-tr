---
title: /debug (Visual Basic)
ms.date: 03/10/2018
helpviewer_keywords:
- debug compiler switches
- /debug compiler option [Visual Basic]
- -debug compiler option [Visual Basic]
- debug compiler option [Visual Basic]
ms.assetid: c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2
ms.openlocfilehash: c2fbe5aa6f0b9ac8c99c9b9ec5cdf0a7d9764ab8
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002399"
---
# <a name="-debug-visual-basic"></a>-Debug (Visual Basic)
Derleyicinin hata ayıklama bilgileri oluşturmasına ve bunu çıkış dosyasına yerleştirmesine neden olur.  
  
## <a name="syntax"></a>Sözdizimi  
  
```console 
-debug[+ | -]  
```

veya

```console  
-debug:[full | pdbonly]  
```
  
## <a name="arguments"></a>Arguments  
  
|Terim|Tanım|  
|---|---|  
|`+` &#124; `-`|İsteğe bağlı. @No__t-0 veya `/debug` belirtildiğinde derleyicinin hata ayıklama bilgileri oluşturmasına ve bir. pdb dosyasına yerleştirmesine neden olur. @No__t-0 belirtildiğinde, `/debug` Belirtmemeye yönelik aynı etkiye sahip olur.|  
|`full` &#124; `pdbonly`|İsteğe bağlı. Derleyici tarafından oluşturulan hata ayıklama bilgilerinin türünü belirtir. @No__t-0 belirtmezseniz, varsayılan değer, çalışan programa bir hata ayıklayıcı eklemenize olanak sağlayan `full` ' dir. @No__t-0 bağımsız değişkeni, program hata ayıklayıcıda başlatıldığında kaynak kodu hata ayıklamasına izin verir, ancak yalnızca çalışan program hata ayıklayıcıya eklendiğinde derleme dili kodunu görüntüler.|  
  
## <a name="remarks"></a>Açıklamalar  
 Hata ayıklama derlemeleri oluşturmak için bu seçeneği kullanın. @No__t-0, `/debug+` veya `/debug:full` ' yi belirtmezseniz, programınızın çıkış dosyasında hata ayıklaması yapamazsınız.  
  
 Varsayılan olarak, hata ayıklama bilgileri yayınlanmaz (`/debug-`). Hata ayıklama bilgilerini göstermek için `/debug` veya `/debug+` belirtin.  
  
 Bir uygulamanın hata ayıklama performansını yapılandırma hakkında daha fazla bilgi için bkz. [bir görüntüyü hata ayıklamayı kolaylaştırın](../../../framework/debug-trace-profile/making-an-image-easier-to-debug.md).  
  
|Visual Studio tümleşik geliştirme ortamında ayarlamak için-hata ayıklayın|  
|---|  
|1. **Çözüm Gezgini**' de bir proje seçiliyken, **Proje** menüsünde **Özellikler**' e tıklayın. <br />2. **Derle** sekmesine tıklayın.<br />3. **Gelişmiş derleme seçenekleri**'ne tıklayın.<br />4. **hata ayıklama bilgisi oluştur** kutusundaki değeri değiştirin.|  
  
## <a name="example"></a>Örnek  
 Aşağıdaki örnek hata ayıklama bilgilerini çıkış dosyasında `App.exe` olarak yerleştirir.  
  
```console  
vbc -debug -out:app.exe test.vb  
```  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Visual Basic komut satırı derleyicisi](../../../visual-basic/reference/command-line-compiler/index.md)
- [/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)
- [Örnek Derleme Komut Satırları](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
