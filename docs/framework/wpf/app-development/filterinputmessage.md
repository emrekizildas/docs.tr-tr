---
title: FilterInputMessage
ms.date: 03/30/2017
helpviewer_keywords:
- raw input [WPF]
- FilterInputMessage method [WPF]
ms.assetid: 4d74c6cf-7d1d-49ff-96c1-231340ce54f5
ms.openlocfilehash: 1453946766e33843ae9e56f7a7f4dbf1678b81b5
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991394"
---
# <a name="filterinputmessage"></a><span data-ttu-id="43ef2-102">FilterInputMessage</span><span class="sxs-lookup"><span data-stu-id="43ef2-102">FilterInputMessage</span></span>
<span data-ttu-id="43ef2-103">E_NOTIMPL döndürülmediği müddetçe PresentationHost. exe tarafından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="43ef2-103">Called by PresentationHost.exe whenever a message is received unless E_NOTIMPL is returned.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="43ef2-104">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="43ef2-104">Syntax</span></span>  
  
```cpp  
HRESULT FilterInputMessage( [in] MSG* pMsg ) ;  
```  
  
## <a name="parameters"></a><span data-ttu-id="43ef2-105">Parametreler</span><span class="sxs-lookup"><span data-stu-id="43ef2-105">Parameters</span></span>  
 `pMsg`  
  
 <span data-ttu-id="43ef2-106">'ndaki Ham giriş alan pencereye gönderilen WM_INPUT iletisi.</span><span class="sxs-lookup"><span data-stu-id="43ef2-106">[in] The WM_INPUT message sent to the window that is getting raw input.</span></span>  
  
## <a name="property-valuereturn-value"></a><span data-ttu-id="43ef2-107">Özellik Değeri/Dönüş Değeri</span><span class="sxs-lookup"><span data-stu-id="43ef2-107">Property Value/Return Value</span></span>  
 <span data-ttu-id="43ef2-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="43ef2-108">HRESULT:</span></span>  
  
 <span data-ttu-id="43ef2-109">S_OK-filtre iletiyi işlemedi ve başka işlemler meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="43ef2-109">S_OK - The filter did not process the message and further processing may occur.</span></span>  
  
 <span data-ttu-id="43ef2-110">S_FALSE-filtre bu iletiyi işledi ve başka bir işleme gerçekleşmemelidir.</span><span class="sxs-lookup"><span data-stu-id="43ef2-110">S_FALSE - The filter processed this message and no further processing should occur.</span></span>  
  
 <span data-ttu-id="43ef2-111">E_NOTIMPL – Bu değer döndürülürse [FilterInputMessage](filterinputmessage.md) yeniden çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="43ef2-111">E_NOTIMPL – If this value is returned, [FilterInputMessage](filterinputmessage.md) is not called again.</span></span> <span data-ttu-id="43ef2-112">Bu, yalnızca özel ilerleme sağlamak isteyen bir konak uygulamasından döndürülebilir ve PresentationHost. exe ' ye yönelik kullanıcı arabirimleri, PresentationHost. exe ' den ham giriş iletileri iletilmek üzere değildir.</span><span class="sxs-lookup"><span data-stu-id="43ef2-112">This might be returned from a host application that is only interested in providing custom progress and error user interfaces to PresentationHost.exe is not interested in being forwarded raw input messages from PresentationHost.exe.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="43ef2-113">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="43ef2-113">Remarks</span></span>  
 <span data-ttu-id="43ef2-114">PresentationHost. exe, klavye, fare ve uzak denetimler de dahil olmak üzere çeşitli ham giriş cihazlarının hedefidir.</span><span class="sxs-lookup"><span data-stu-id="43ef2-114">PresentationHost.exe is the target of various raw input devices, including keyboard, mice, and remote controls.</span></span> <span data-ttu-id="43ef2-115">Bazen, ana bilgisayar uygulamasındaki davranış, aksi durumda PresentationHost. exe tarafından tüketilen girişe bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="43ef2-115">Sometimes, behavior in the host application is dependent on input that would otherwise be consumed by PresentationHost.exe.</span></span> <span data-ttu-id="43ef2-116">Örneğin, bir konak uygulama belirli kullanıcı arabirimi öğelerinin görüntülenip görüntülenmeyeceğini anlamak için belirli giriş iletilerinin alınmasına bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="43ef2-116">For example, a host application may depend on receiving certain input messages to determine whether or not to display specific user interface elements.</span></span>  
  
 <span data-ttu-id="43ef2-117">Konak uygulamasının bu davranışları sağlamak üzere gerekli giriş iletilerini almasına izin vermek için, PresentationHost. exe, [FilterInputMessage](filterinputmessage.md)' ı çağırarak, barındırılan uygulamaya uygun ham giriş iletilerini iletir.</span><span class="sxs-lookup"><span data-stu-id="43ef2-117">To allow the host application to receive the necessary input messages to provide these behaviors, PresentationHost.exe forwards appropriate raw input messages to the hosted application by calling [FilterInputMessage](filterinputmessage.md).</span></span>  
  
 <span data-ttu-id="43ef2-118">Barındırılan uygulama, [Getpwınputdevices](getrawinputdevices.md)tarafından döndürülen ham giriş aygıtları (Insan arabirim aygıtları) kümesiyle kaydederek ham giriş iletilerini alır.</span><span class="sxs-lookup"><span data-stu-id="43ef2-118">The hosted application receives raw input messages by registering with the set of raw input devices (Human Interface Devices) returned by [GetRawInputDevices](getrawinputdevices.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="43ef2-119">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="43ef2-119">See also</span></span>

- [<span data-ttu-id="43ef2-120">WM_INPUT iletisi</span><span class="sxs-lookup"><span data-stu-id="43ef2-120">WM_INPUT message</span></span>](/windows/desktop/inputdev/wm-input)
