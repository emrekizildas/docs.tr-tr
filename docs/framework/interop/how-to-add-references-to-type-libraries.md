---
title: 'Nasıl yapılır: Tür Kitaplıklarına Başvurular Ekleme'
ms.date: 03/30/2017
helpviewer_keywords:
- importing type library
- interop assemblies, generating
- type libraries
- COM interop, importing type library
ms.assetid: f5cfa6ba-cc25-4017-82cd-ba7391859113
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a666c0e079fb30ecdd32aad64f44434d8253acf4
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971897"
---
# <a name="how-to-add-references-to-type-libraries"></a>Nasıl yapılır: Tür Kitaplıklarına Başvurular Ekleme
Visual Studio, bir tür kitaplığına bir başvuru eklediğinizde meta verileri içeren bir birlikte çalışma derlemesi oluşturur. Birincil birlikte çalışma derlemesi varsa, Visual Studio yeni bir birlikte çalışma derlemesi oluşturmadan önce mevcut derlemeyi kullanır.  
  
### <a name="to-add-a-reference-to-a-type-library-in-visual-studio"></a>Visual Studio 'da bir tür kitaplığına başvuru eklemek için  
  
1. Bir Windows Kurulumu. exe dosyası yüklemeyi sizin için gerçekleştirmediği müddetçe COM DLL veya EXE dosyasını bilgisayarınıza yükleyebilirsiniz.  
  
2. **Proje**, **Başvuru Ekle**' yi seçin.  
  
3. Başvuru Yöneticisi 'nde **com**' u seçin.  
  
4. Listeden tür kitaplığını seçin veya. tlb dosyasına gözatamazsınız.  
  
5. **Tamam**’ı seçin.  
  
6. Çözüm Gezgini ' de, yeni eklediğiniz başvurunun kısayol menüsünü açın ve ardından **Özellikler**' i seçin.  
  
7. **Özellikler** penceresinde, **birlikte çalışma türlerini katıştır** özelliğinin **true**olarak ayarlandığından emin olun. Bu, Visual Studio 'Nun çalıştırılabilirlerinizdeki COM türlerine ait tür bilgilerini katıştırmasına ve birincil birlikte çalışma derlemelerini uygulamanızla birlikte dağıtma gereksinimini ortadan kaldırmaya neden olur.  
  
> [!NOTE]
> Menü ve iletişim kutusu seçenekleri, kullanmakta olduğunuz Visual Studio sürümüne bağlı olarak farklılık gösterebilir.  
  
### <a name="to-add-a-reference-to-a-type-library-for-command-line-compilation"></a>Komut satırı derlemesi için bir tür kitaplığına başvuru eklemek için  
  
1. Birlikte çalışma bütünleştirilmiş kodu [oluşturun: Tür kitaplıklarından](how-to-generate-interop-assemblies-from-type-libraries.md)birlikte çalışma derlemeleri oluşturun.  
  
2. Çalıştırılabilirlerinizde COM türlerine ilişkin tür bilgilerini eklemek için, birlikte çalışabilirlik derleme adıyla birlikte [/Link (C# derleyici seçenekleri)](../../csharp/language-reference/compiler-options/link-compiler-option.md) veya [/Link (Visual Basic)](../../visual-basic/reference/command-line-compiler/link.md) derleyici seçeneğini kullanın.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Tür Kitaplığını Bütünleştirilmiş Kod Olarak İçeri Aktarma](importing-a-type-library-as-an-assembly.md)
- [COM Bileşenlerini .NET Framework'te Gösterme](exposing-com-components.md)
- [İzlenecek yol: Visual Studio 'da yönetilen derlemelerden tür ekleme](../../standard/assembly/embed-types-visual-studio.md) 
- [/Link (C# derleyici seçenekleri)](../../csharp/language-reference/compiler-options/link-compiler-option.md)
- [/Link (Visual Basic)](../../visual-basic/reference/command-line-compiler/link.md)
