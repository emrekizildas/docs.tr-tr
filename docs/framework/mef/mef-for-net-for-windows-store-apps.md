---
title: Windows Mağazası uygulamaları için .NET için MEF
ms.date: 03/30/2017
ms.assetid: 7667770e-d163-4ad6-a303-085cf73db2f2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 255892e4dd3938028f488f80d8fba367590976f7
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051625"
---
# <a name="mef-for-net-for-windows-store-apps"></a><span data-ttu-id="26e3c-102">Windows Mağazası uygulamaları için .NET için MEF</span><span class="sxs-lookup"><span data-stu-id="26e3c-102">MEF for .NET for Windows Store Apps</span></span>
<span data-ttu-id="26e3c-103"><xref:System.Composition?displayProperty=nameWithType>ve alt ad alanları Managed Extensibility Framework (MEF) ile [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] Genişletilebilir uygulamalar geliştirmeye yönelik türler içerir.</span><span class="sxs-lookup"><span data-stu-id="26e3c-103"><xref:System.Composition?displayProperty=nameWithType> and its child namespaces contain types for developing extensible [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] apps with Managed Extensibility Framework (MEF).</span></span> <span data-ttu-id="26e3c-104">Bu ad alanları, [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] [!INCLUDE[win8](../../../includes/win8-md.md)] işletim sistemi için alt kümenin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="26e3c-104">These namespaces are part of the [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] subset for the [!INCLUDE[win8](../../../includes/win8-md.md)] operating system.</span></span>  
  
 <span data-ttu-id="26e3c-105">Bu ad alanları, .NET Framework dağıtılan çekirdek sınıf kitaplığının bir parçası değildir.</span><span class="sxs-lookup"><span data-stu-id="26e3c-105">These namespaces are not part of the core class library distributed with the .NET Framework.</span></span> <span data-ttu-id="26e3c-106">Bu ad alanlarını yüklemek için projenizi Visual Studio 'da açın, **Proje** menüsünden **NuGet Paketlerini Yönet** ' i seçin ve Microsoft. Composition paketini çevrimiçi olarak arayın.</span><span class="sxs-lookup"><span data-stu-id="26e3c-106">To install these namespaces, open your project in Visual Studio, choose **Manage NuGet Packages** from the **Project** menu, and search online for the Microsoft.Composition package.</span></span>  
  
- <span data-ttu-id="26e3c-107"><xref:System.Composition?displayProperty=nameWithType>uygulamalar için [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] çekirdek MEF 'i oluşturan sınıflar sağlar.</span><span class="sxs-lookup"><span data-stu-id="26e3c-107"><xref:System.Composition?displayProperty=nameWithType> provides classes that constitute the core MEF for [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] apps.</span></span>  
  
- <span data-ttu-id="26e3c-108"><xref:System.Composition.Convention?displayProperty=nameWithType>kural tabanlı bir yapılandırma modeliyle MEF kullanmayı destekleyen türler sağlar.</span><span class="sxs-lookup"><span data-stu-id="26e3c-108"><xref:System.Composition.Convention?displayProperty=nameWithType> provides types that support using MEF with a convention-based configuration model.</span></span>  
  
- <span data-ttu-id="26e3c-109"><xref:System.Composition.Hosting?displayProperty=nameWithType>, ana bilgisayar uygulamaları geliştiricileri için yararlı olan MEF türleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="26e3c-109"><xref:System.Composition.Hosting?displayProperty=nameWithType> provides MEF types that are useful to developers of host applications.</span></span>  
  
- <span data-ttu-id="26e3c-110"><xref:System.Composition.Hosting.Core?displayProperty=nameWithType>bileşim altyapısı tarafından dahili olarak kullanılan MEF türleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="26e3c-110"><xref:System.Composition.Hosting.Core?displayProperty=nameWithType> provides MEF types used internally by the composition engine.</span></span>  
  
 <span data-ttu-id="26e3c-111">Ve içerdiği ad alanları [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] ve türlerin listesi hakkında daha fazla bilgi için, Windows Geliştirme Merkezi 'nde [Windows Mağazası uygulamalarına genel bakış için .net](https://go.microsoft.com/fwlink/p/?LinkID=238312) başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="26e3c-111">For more information about [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] and a list of namespaces and types that it contains, see [.NET for Windows Store apps overview](https://go.microsoft.com/fwlink/p/?LinkID=238312) in the Windows Dev Center.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="26e3c-112">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="26e3c-112">See also</span></span>

- [<span data-ttu-id="26e3c-113">Windows Mağazası uygulamalarına yönelik .NET genel bakış</span><span class="sxs-lookup"><span data-stu-id="26e3c-113">.NET for Windows Store apps overview</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=238312)
- [<span data-ttu-id="26e3c-114">Windows Mağazası uygulamaları için .NET – desteklenen API 'Ler</span><span class="sxs-lookup"><span data-stu-id="26e3c-114">.NET for Windows Store apps – supported APIs</span></span>](https://go.microsoft.com/fwlink/p/?LinkID=247912)
- [<span data-ttu-id="26e3c-115">Managed Extensibility Framework (MEF)</span><span class="sxs-lookup"><span data-stu-id="26e3c-115">Managed Extensibility Framework (MEF)</span></span>](index.md)
