---
title: Mac üzerinde .NET Core önkoşulları
description: MacOS makinelerinde .NET Core uygulamaları geliştirmek, dağıtmak ve çalıştırmak için desteklenen macOS sürümleri ve .NET Core bağımlılıkları.
author: thraka
ms.author: adegeo
ms.custom: updateeachvsrelease
ms.date: 09/27/2019
ms.openlocfilehash: 13eea0043be9cf5d5574d6b38f144853c22e8d07
ms.sourcegitcommit: 35da8fb45b4cca4e59cc99a5c56262c356977159
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/28/2019
ms.locfileid: "71591684"
---
# <a name="prerequisites-for-net-core-on-macos"></a>MacOS 'ta .NET Core önkoşulları

Bu makalede, macOS makinelerinde .NET Core uygulamaları geliştirmek, dağıtmak ve çalıştırmak için ihtiyacınız olan desteklenen macOS sürümleri ve .NET Core bağımlılıkları gösterilmektedir. Desteklenen işletim sistemi sürümleri ve bağımlılıklar, bir Mac üzerinde .NET Core uygulamaları geliştirmenin üç yolu için geçerlidir: en sevdiğiniz düzenleyici, [Visual Studio Code](https://code.visualstudio.com/)ve [Mac için Visual Studio](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) [ile komut satırı](tutorials/using-with-xplat-cli.md)aracılığıyla.

## <a name="downloads-and-dependencies"></a>İndirmeler ve bağımlılıklar

<!-- markdownlint-disable MD025 -->

# <a name="net-core-30tabnetcore30"></a>[.NET Core 3.0](#tab/netcore30)

.NET Core 3,0, **MacOS High Sierra (sürüm 10,13)** ve sonraki sürümlerde desteklenir. **X64** CPU mimarisi gereklidir.

.NET Core SDK [.NET Core 3,0 İndirmeleri](https://dotnet.microsoft.com/download/dotnet-core/3.0) sayfasından indirin ve yükleyin. .NET Core 3,0 desteklenen işletim sistemlerinin, dağıtımların ve sürümlerin tamamı, destek SISTEMI sürümlerinden ve yaşam döngüsü ilkesi bağlantılarından 3,0 oluşan tüm liste için [.net core tarafından desteklenen IŞLETIM sistemi sürümleri](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md) .

Bilinen sorunların listesi için bkz. [.NET Core bilinen sorunlar](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-known-issues.md).

# <a name="net-core-22tabnetcore22"></a>[.NET Core 2,2](#tab/netcore22)

.NET Core 2,2 **macOS Sierra (sürüm 10,12)** ve sonraki sürümlerde desteklenir. **X64** CPU mimarisi gereklidir.

.NET Core SDK [.NET Core 2,2 İndirmeleri](https://dotnet.microsoft.com/download/dotnet-core/2.2) sayfasından indirin ve yükleyin. .NET Core 2,2 desteklenen işletim sistemlerinin, dağıtımların ve sürümlerin tamamı, destek SISTEMI sürümlerinden ve yaşam döngüsü ilkesi bağlantılarından 2,2 oluşan tüm liste için [.net core tarafından desteklenen IŞLETIM sistemi sürümleri](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md) .

Bilinen sorunların listesi için bkz. [.NET Core bilinen sorunlar](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-known-issues.md).

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2,1](#tab/netcore21)

.NET Core 2,1 **macOS Sierra (sürüm 10,12)** ve sonraki sürümlerde desteklenir. **X64** CPU mimarisi gereklidir.

.NET Core SDK [.NET Core 2,1 İndirmeleri](https://dotnet.microsoft.com/download/dotnet-core/2.1) sayfasından indirin ve yükleyin. .NET Core 2,1 desteklenen işletim sistemlerinin, dağıtımların ve sürümlerin tamamı, destek SISTEMI sürümlerinden ve yaşam döngüsü ilkesi bağlantılarından 2,1 oluşan tüm liste için [.net core tarafından desteklenen IŞLETIM sistemi sürümleri](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md) .

Bilinen sorunların listesi için bkz. [.NET Core bilinen sorunlar](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-known-issues.md).

---

## <a name="visual-studio-for-mac"></a>Mac için Visual Studio

.NET Core SDK kullanarak .NET Core uygulamaları geliştirmek için herhangi bir düzenleyici kullanabilirsiniz. Ancak, tümleşik bir geliştirme ortamında Mac 'te .NET Core uygulamaları geliştirmek istiyorsanız [Mac için Visual Studio](https://visualstudio.microsoft.com/vs/mac/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)kullanabilirsiniz.
