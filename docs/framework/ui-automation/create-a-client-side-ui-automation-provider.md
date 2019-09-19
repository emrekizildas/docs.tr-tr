---
title: İstemci Tarafı UI Otomasyon Sağlayıcı Oluşturma
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UI Automation, creating client-side provider
- client-side UI Automation provider, creating
ms.assetid: d91edaf2-be28-41ec-a508-af421cb43c3d
ms.openlocfilehash: 483090b38f58481c992ebabaf26e6cbcf9c6cae8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043832"
---
# <a name="create-a-client-side-ui-automation-provider"></a><span data-ttu-id="9016b-102">İstemci Tarafı UI Otomasyon Sağlayıcı Oluşturma</span><span class="sxs-lookup"><span data-stu-id="9016b-102">Create a Client-Side UI Automation Provider</span></span>
> [!NOTE]
> <span data-ttu-id="9016b-103">Bu belge, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] <xref:System.Windows.Automation> ad alanında tanımlanan yönetilen sınıfları kullanmak isteyen .NET Framework geliştiricilere yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="9016b-103">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="9016b-104">Hakkında [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]en son bilgiler için bkz [. Windows Otomasyonu API 'si: UI Otomasyonu](https://go.microsoft.com/fwlink/?LinkID=156746).</span><span class="sxs-lookup"><span data-stu-id="9016b-104">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](https://go.microsoft.com/fwlink/?LinkID=156746).</span></span>  
  
 <span data-ttu-id="9016b-105">Bu konu, bir istemci tarafı UI Otomasyon sağlayıcısının nasıl uygulanacağını gösteren örnek kodu içerir.</span><span class="sxs-lookup"><span data-stu-id="9016b-105">This topic contains example code that shows how to implement a client-side UI Automation provider.</span></span>  
  
## <a name="example"></a><span data-ttu-id="9016b-106">Örnek</span><span class="sxs-lookup"><span data-stu-id="9016b-106">Example</span></span>  
 <span data-ttu-id="9016b-107">Aşağıdaki örnek kod, bir konsol penceresi için çok basit bir istemci tarafı sağlayıcı uygulayan bir dinamik bağlantı kitaplığı (DLL) içinde oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="9016b-107">The following example code can be built into a dynamic-link library (DLL) that implements a very simple client-side provider for a console window.</span></span> <span data-ttu-id="9016b-108">Kod yararlı bir işlevselliğe sahip değildir, ancak bir UI Otomasyonu istemci uygulaması tarafından kaydedilebileceği bir sağlayıcı derlemesini ayarlamaya yönelik temel adımları göstermeye yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="9016b-108">The code does not have any useful functionality, but is intended to demonstrate the basic steps in setting up a provider assembly that can be registered by a UI Automation client application.</span></span>  
  
 [!code-csharp[UIAClientSideProvider_snip#101](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClientSideProvider_snip/CSharp/CSProviderProgram.cs#101)]
 [!code-vb[UIAClientSideProvider_snip#101](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClientSideProvider_snip/visualbasic/csproviderprogram.vb#101)]  
  
## <a name="see-also"></a><span data-ttu-id="9016b-109">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="9016b-109">See also</span></span>

- [<span data-ttu-id="9016b-110">UI Otomasyonu Sağlayıcılara Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9016b-110">UI Automation Providers Overview</span></span>](ui-automation-providers-overview.md)
- [<span data-ttu-id="9016b-111">İstemci Tarafı Sağlayıcı Bütünleştirilmiş Kodunu Kaydetme</span><span class="sxs-lookup"><span data-stu-id="9016b-111">Register a Client-Side Provider Assembly</span></span>](register-a-client-side-provider-assembly.md)
