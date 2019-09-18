---
title: UI Otomasyon MultipleView Denetim Düzeni Uygulama
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, MultipleView control pattern
- MultipleView control pattern
- control patterns, MultipleView
ms.assetid: 5bf1b248-ffee-48c8-9613-0b134bbe9f6a
ms.openlocfilehash: 699644b98fbf818c71553775f4dff8dfb0726977
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043435"
---
# <a name="implementing-the-ui-automation-multipleview-control-pattern"></a><span data-ttu-id="c81cf-102">UI Otomasyon MultipleView Denetim Düzeni Uygulama</span><span class="sxs-lookup"><span data-stu-id="c81cf-102">Implementing the UI Automation MultipleView Control Pattern</span></span>
> [!NOTE]
> <span data-ttu-id="c81cf-103">Bu belge, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] <xref:System.Windows.Automation> ad alanında tanımlanan yönetilen sınıfları kullanmak isteyen .NET Framework geliştiricilere yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="c81cf-103">This documentation is intended for .NET Framework developers who want to use the managed [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] classes defined in the <xref:System.Windows.Automation> namespace.</span></span> <span data-ttu-id="c81cf-104">Hakkında [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]en son bilgiler için bkz [. Windows Otomasyonu API 'si: UI Otomasyonu](https://go.microsoft.com/fwlink/?LinkID=156746).</span><span class="sxs-lookup"><span data-stu-id="c81cf-104">For the latest information about [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], see [Windows Automation API: UI Automation](https://go.microsoft.com/fwlink/?LinkID=156746).</span></span>  
  
 <span data-ttu-id="c81cf-105">Bu konu, olaylar ve özellikler hakkında bilgiler <xref:System.Windows.Automation.Provider.IMultipleViewProvider>de dahil olmak üzere uygulama yönergelerini ve kurallarını tanıtır.</span><span class="sxs-lookup"><span data-stu-id="c81cf-105">This topic introduces guidelines and conventions for implementing <xref:System.Windows.Automation.Provider.IMultipleViewProvider>, including information about events and properties.</span></span> <span data-ttu-id="c81cf-106">Ek başvuruların bağlantıları konunun sonunda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="c81cf-106">Links to additional references are listed at the end of the topic.</span></span>  
  
 <span data-ttu-id="c81cf-107"><xref:System.Windows.Automation.MultipleViewPattern> Denetim stili, aynı bilgi kümesinin veya alt denetimlerin birden çok temsilini sağlayan ve arasında geçiş yapabilecek denetimleri desteklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c81cf-107">The <xref:System.Windows.Automation.MultipleViewPattern> control pattern is used to support controls that provide, and are able to switch between, multiple representations of the same set of information or child controls.</span></span>  
  
 <span data-ttu-id="c81cf-108">Birden çok görünüm sunan denetimlerin örnekleri, liste görünümünü (içeriğini küçük resimler, Kutucuklar, simgeler veya ayrıntılar olarak gösterebilir), [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] grafikler (pasta, çizgi, çubuk, formül içeren hücre değeri), [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)] belgeler (normal, Web düzeni, Yazdırma düzeni, okuma düzeni, ana hat), Microsoft Outlook Takvim (yıl, ay, hafta, gün) ve [!INCLUDE[TLA#tla_wmp](../../../includes/tlasharptla-wmp-md.md)] kaplamalar.</span><span class="sxs-lookup"><span data-stu-id="c81cf-108">Examples of controls that can present multiple views include the list view (which can show its contents as thumbnails, tiles, icons, or details), [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] charts (pie, line, bar, cell value with a formula), [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)] documents (normal, Web layout, print layout, reading layout, outline), Microsoft Outlook calendar (year, month, week, day), and [!INCLUDE[TLA#tla_wmp](../../../includes/tlasharptla-wmp-md.md)] skins.</span></span> <span data-ttu-id="c81cf-109">Desteklenen görünümler denetim geliştiricisi tarafından belirlenir ve her denetime özeldir.</span><span class="sxs-lookup"><span data-stu-id="c81cf-109">The supported views are determined by the control developer and are specific to each control.</span></span>  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a><span data-ttu-id="c81cf-110">Uygulama kılavuzları ve kuralları</span><span class="sxs-lookup"><span data-stu-id="c81cf-110">Implementation Guidelines and Conventions</span></span>  
 <span data-ttu-id="c81cf-111">Birden çok görünüm denetim modelini uygularken aşağıdaki kılavuz ve kurallara göz önünde yer verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c81cf-111">When implementing the Multiple View control pattern, note the following guidelines and conventions:</span></span>  
  
- <span data-ttu-id="c81cf-112"><xref:System.Windows.Automation.Provider.IMultipleViewProvider>geçerli görünümü sağlayan bir denetimden farklıysa geçerli görünümü yöneten bir kapsayıcıya de uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c81cf-112"><xref:System.Windows.Automation.Provider.IMultipleViewProvider> should also be implemented on a container that manages the current view if it is different from a control that provides the current view.</span></span> <span data-ttu-id="c81cf-113">Örneğin, Windows Gezgini, denetimin görünümü Windows Gezgini uygulamasından yönetilirken, geçerli klasör içeriği için bir liste denetimi içerir.</span><span class="sxs-lookup"><span data-stu-id="c81cf-113">For example, Windows Explorer contains a List control for the current folder content while the view for the control is managed from the Windows Explorer application.</span></span>  
  
- <span data-ttu-id="c81cf-114">İçeriğini sıralayacak bir denetim, birden fazla görünümü destekleyecek şekilde değerlendirilmez.</span><span class="sxs-lookup"><span data-stu-id="c81cf-114">A control that is able to sort its content is not considered to support multiple views.</span></span>  
  
- <span data-ttu-id="c81cf-115">Görünümler koleksiyonu örneklerin tamamında aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c81cf-115">The collection of views must be identical across instances.</span></span>  
  
- <span data-ttu-id="c81cf-116">Görünüm adları Metin Okuma, Braille ve diğer insan tarafından okunabilen uygulamalarda kullanım için uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c81cf-116">View names must be suitable for use in Text to Speech, Braille, and other human-readable applications.</span></span>  
  
<a name="Required_Members_for_IMultipleViewProvider"></a>   
## <a name="required-members-for-imultipleviewprovider"></a><span data-ttu-id="c81cf-117">IMultipleViewProvider için gerekli Üyeler</span><span class="sxs-lookup"><span data-stu-id="c81cf-117">Required Members for IMultipleViewProvider</span></span>  
 <span data-ttu-id="c81cf-118">IMultipleViewProvider uygulamak için aşağıdaki özellikler ve Yöntemler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c81cf-118">The following properties and methods are required for implementing IMultipleViewProvider.</span></span>  
  
|<span data-ttu-id="c81cf-119">Gerekli Üyeler</span><span class="sxs-lookup"><span data-stu-id="c81cf-119">Required members</span></span>|<span data-ttu-id="c81cf-120">Üye türü</span><span class="sxs-lookup"><span data-stu-id="c81cf-120">Member type</span></span>|<span data-ttu-id="c81cf-121">Notlar</span><span class="sxs-lookup"><span data-stu-id="c81cf-121">Notes</span></span>|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.CurrentView%2A>|<span data-ttu-id="c81cf-122">Özellik</span><span class="sxs-lookup"><span data-stu-id="c81cf-122">Property</span></span>|<span data-ttu-id="c81cf-123">Yok.</span><span class="sxs-lookup"><span data-stu-id="c81cf-123">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.GetSupportedViews%2A>|<span data-ttu-id="c81cf-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c81cf-124">Method</span></span>|<span data-ttu-id="c81cf-125">Yok.</span><span class="sxs-lookup"><span data-stu-id="c81cf-125">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.GetViewName%2A>|<span data-ttu-id="c81cf-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c81cf-126">Method</span></span>|<span data-ttu-id="c81cf-127">Yok.</span><span class="sxs-lookup"><span data-stu-id="c81cf-127">None</span></span>|  
|<xref:System.Windows.Automation.Provider.IMultipleViewProvider.SetCurrentView%2A>|<span data-ttu-id="c81cf-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c81cf-128">Method</span></span>|<span data-ttu-id="c81cf-129">Yok.</span><span class="sxs-lookup"><span data-stu-id="c81cf-129">None</span></span>|  
  
 <span data-ttu-id="c81cf-130">Bu denetim düzeniyle ilişkili hiçbir olay yok.</span><span class="sxs-lookup"><span data-stu-id="c81cf-130">There are no events associated with this control pattern.</span></span>  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a><span data-ttu-id="c81cf-131">Özel Durumlar</span><span class="sxs-lookup"><span data-stu-id="c81cf-131">Exceptions</span></span>  
 <span data-ttu-id="c81cf-132">Sağlayıcı aşağıdaki özel durumları oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c81cf-132">Provider must throw the following exceptions.</span></span>  
  
|<span data-ttu-id="c81cf-133">Özel durum türü</span><span class="sxs-lookup"><span data-stu-id="c81cf-133">Exception type</span></span>|<span data-ttu-id="c81cf-134">Koşul</span><span class="sxs-lookup"><span data-stu-id="c81cf-134">Condition</span></span>|  
|--------------------|---------------|  
|<xref:System.ArgumentException>|<span data-ttu-id="c81cf-135">Ya da <xref:System.Windows.Automation.Provider.IMultipleViewProvider.SetCurrentView%2A> <xref:System.Windows.Automation.Provider.IMultipleViewProvider.GetViewName%2A> desteklenen görünümler koleksiyonunun üyesi olmayan bir parametre ile çağrıldığında.</span><span class="sxs-lookup"><span data-stu-id="c81cf-135">When either <xref:System.Windows.Automation.Provider.IMultipleViewProvider.SetCurrentView%2A> or <xref:System.Windows.Automation.Provider.IMultipleViewProvider.GetViewName%2A> is called with a parameter that is not a member of the supported views collection.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="c81cf-136">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c81cf-136">See also</span></span>

- [<span data-ttu-id="c81cf-137">UI Otomasyonu Denetim Desenlerine Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c81cf-137">UI Automation Control Patterns Overview</span></span>](ui-automation-control-patterns-overview.md)
- [<span data-ttu-id="c81cf-138">UI Otomasyonu Sağlayıcıda Denetim Düzenleri Desteği</span><span class="sxs-lookup"><span data-stu-id="c81cf-138">Support Control Patterns in a UI Automation Provider</span></span>](support-control-patterns-in-a-ui-automation-provider.md)
- [<span data-ttu-id="c81cf-139">İstemciler İçin UI Otomasyonu Denetim Düzenleri</span><span class="sxs-lookup"><span data-stu-id="c81cf-139">UI Automation Control Patterns for Clients</span></span>](ui-automation-control-patterns-for-clients.md)
- [<span data-ttu-id="c81cf-140">UI Otomasyon Ağacına Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c81cf-140">UI Automation Tree Overview</span></span>](ui-automation-tree-overview.md)
- [<span data-ttu-id="c81cf-141">UI Otomasyonunda Önbelleğe Almayı Kullanma</span><span class="sxs-lookup"><span data-stu-id="c81cf-141">Use Caching in UI Automation</span></span>](use-caching-in-ui-automation.md)
