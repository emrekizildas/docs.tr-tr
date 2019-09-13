---
title: Mac için Visual Studio kullanarak macOS üzerinde .NET Core kullanmaya başlama
description: Bu konu, Mac için Visual Studio ve .NET Core kullanarak basit bir konsol uygulaması oluşturma konusunda size rehberlik eder.
author: mairaw
ms.date: 07/11/2019
ms.custom: seodec18
ms.openlocfilehash: ff508bbe8d72a88ea32adfbed984d4e9e8b8e7ca
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70925820"
---
# <a name="get-started-with-net-core-on-macos-using-visual-studio-for-mac"></a>Mac için Visual Studio kullanarak macOS üzerinde .NET Core kullanmaya başlama

Mac için Visual Studio .NET Core uygulamaları geliştirmek için tam özellikli bir tümleşik geliştirme ortamı (IDE) sağlar. Bu konu, Mac için Visual Studio ve .NET Core kullanarak basit bir konsol uygulaması oluşturma konusunda size rehberlik eder.

> [!NOTE]
> Geri bildiriminiz çok değerli. Mac için Visual Studio üzerinde geliştirme ekibine geri bildirimde bulunmak için kullanabileceğiniz iki yol vardır:
>
> * Mac için Visual Studio, menüden**sorun bildir** veya hoş geldiniz ekranından **sorun** **bildir ' i seçerek** > bir hata raporu dosyalayarak bir pencere açar. Geri bildiriminizi [Geliştirici Topluluğu](https://developercommunity.visualstudio.com/spaces/8/index.html) portalında izleyebilirsiniz.
> * Öneride bulunmak için, > menüden**bir öneri sağlayın** veya hoş geldiniz ekranından bir öneri sağlayın. Bu işlem sizi [Mac için Visual Studio Geliştirici topluluğu Web sayfasına](https://developercommunity.visualstudio.com/content/idea/post.html?space=41)götürür.

## <a name="prerequisites"></a>Önkoşullar

[Mac üzerinde .NET Core Için önkoşulları](../macos-prerequisites.md) konusuna bakın.

.NET Core 'un desteklenen bir sürümünü kullandığınızdan emin olmak için [.NET Core destek](https://docs.microsoft.com/visualstudio/mac/net-core-support?view=vsmac-2019) Kılavuzu ' nu kontrol edin.

## <a name="get-started"></a>Kullanmaya başlayın

Önkoşulları ve Mac için Visual Studio zaten yüklediyseniz, bu bölümü atlayın ve [proje oluşturmaya](#creating-a-project)devam edin. Önkoşulları ve Mac için Visual Studio yüklemek için şu adımları izleyin:

[Mac için Visual Studio yükleyicisini](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)indirin. Yükleyiciyi çalıştırın. Lisans sözleşmesini okuyun ve kabul edin. Yüklemesi sırasında .NET Core 'u yüklemek için seçeneği belirleyin. Platformlar arası mobil uygulama geliştirme teknolojisi olan Xamarin 'i yükleyebilirsiniz. Xamarin ve ilgili bileşenlerinin yüklenmesi .NET Core geliştirmesi için isteğe bağlıdır. Mac için Visual Studio yüklemesi işlemini adım adım için [Mac için Visual Studio belgelerine](/visualstudio/mac/)bakın. Yüklemesi tamamlandığında Mac için Visual Studio IDE 'yi başlatın.

## <a name="creating-a-project"></a>Proje oluşturma

1. Başlangıç penceresinde **Yeni** ' yi seçin.

   ![Mac için Visual Studio başlangıç ekranında yeni düğme](./media/using-on-mac-vs/visual-studio-mac-new-project.png)

1. **Yeni proje** iletişim kutusunda, **.NET Core** düğümünün altında **uygulama** ' yı seçin. **Konsol uygulaması** şablonunu ve ardından Ileri ' **yi**seçin.

   ![Yeni proje şablonları listesi](./media/using-on-mac-vs/visual-studio-mac-new-dialog.png)

1. .NET Core 'un birden fazla sürümü yüklüyse, projeniz için hedef çerçeveyi seçin.

1. **Proje adı**Için "HelloWorld" yazın. **Oluştur**’u seçin.

   ![Yeni konsol uygulamanızı yapılandırma iletişim kutusu](./media/using-on-mac-vs/visual-studio-mac-new-options.png)

1. Projenin bağımlılıkları geri yüklenirken bekleyin. Projenin bir C# `Program` yöntemiolanprogram.csbirsınıfiçerentekbirdosyası`Main` vardır. `Console.WriteLine` İfade "Merhaba Dünya!" çıktısını alacak uygulama çalıştırıldığında konsola.

   ![Program.cs dosyasının açık olduğu ana pencere](./media/using-on-mac-vs/visual-studio-mac-editor.png)

## <a name="run-the-application"></a>Uygulamayı çalıştırma

Uygulamayı hata ayıklama modunda ⌘ ↵ (komut + ENTER) kullanarak veya ⌥ ⌘ ↵ (Option + Command + ENTER) kullanarak yayın modunda çalıştırın.

![Uygulama çıkış bölmesi Merhaba Dünya gösterir!](./media/using-on-mac-vs/visual-studio-mac-output.png)

## <a name="next-step"></a>Sonraki adım

[MacOS üzerinde Mac için Visual Studio konu başlığı kullanarak tüm .NET Core çözümü oluşturma](using-on-mac-vs-full-solution.md) , yeniden kullanılabilir bir kitaplık ve birim testi içeren bir .NET Core çözümünün nasıl oluşturulacağını göstermektedir.
