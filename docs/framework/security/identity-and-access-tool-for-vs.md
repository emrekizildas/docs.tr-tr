---
title: Visual Studio 2012 için Kimlik ve Erişim Aracı
ms.date: 03/30/2017
ms.assetid: 87b8f8f2-4074-44fd-9fd6-08278e877390
author: BrucePerlerMS
ms.openlocfilehash: d58cca13dc3ac67742e5371aed628a6a680e61e1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045423"
---
# <a name="identity-and-access-tool-for-visual-studio-2012"></a><span data-ttu-id="e97c1-102">Visual Studio 2012 için Kimlik ve Erişim Aracı</span><span class="sxs-lookup"><span data-stu-id="e97c1-102">Identity and Access Tool for Visual Studio 2012</span></span>
<span data-ttu-id="e97c1-103">Bu konuda, Visual Studio 11 için yeni Kimlik ve Erişim Aracı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e97c1-103">This topic describes the new Identity and Access Tool for Visual Studio 11.</span></span> <span data-ttu-id="e97c1-104">Bu aracı şu URL 'den indirebilirsiniz: <https://go.microsoft.com/fwlink/?LinkID=245849> veya doğrudan Extensions Manager 'da "kimlik" araması yaparak doğrudan Visual Studio 11 içinden.</span><span class="sxs-lookup"><span data-stu-id="e97c1-104">You can download this tool from the following URL: <https://go.microsoft.com/fwlink/?LinkID=245849> or directly from within Visual Studio 11 by searching for "identity" directly in the Extensions Manager.</span></span>  
  
 <span data-ttu-id="e97c1-105">Visual Studio 11 için Kimlik ve Erişim Aracı, aşağıdaki önemli özelliklerle birlikte önemli ölçüde basitleştirilmiş bir geliştirme zamanı deneyimi sağlar:</span><span class="sxs-lookup"><span data-stu-id="e97c1-105">The Identity and Access Tool for Visual Studio 11 delivers a dramatically simplified development-time experience with the following highlights:</span></span>  
  
- <span data-ttu-id="e97c1-106">Bu yeni araç ile, web uygulamaları proje türlerini kullanarak geliştirme yapabilir ve IIS express'i hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e97c1-106">Using the new tool, you can develop using web applications project types and target IIS express.</span></span>  
  
- <span data-ttu-id="e97c1-107">Yalnızca koruma paket kimlik doğrulamasının aksine, yeni araçla yerel ana bölge keşif sayfanızı/denetleyicinizi (uygulamanızda kimlik doğrulama deneyimini gerçekleştiren başka bir uç noktası) belirtebilirsiniz; WIF kimliği doğrulanmamış tüm istekleri STS'ye yönlendirmek yerine buraya gidecek şekilde yapılandıracaktır.</span><span class="sxs-lookup"><span data-stu-id="e97c1-107">Unlike with the blanket protection-only authentication, with the new tool, you can specify your local home realm discovery page/controller (or any other endpoint handling the authentication experience within your application) and WIF will configure all unauthenticated requests to go there, instead of redirecting them to the STS.</span></span>  
  
- <span data-ttu-id="e97c1-108">Araç, hata ayıklama oturumu başlattığınızda yerel makinenizde çalışan bir test Güvenlik Belirteci Hizmeti (STS) içerir.</span><span class="sxs-lookup"><span data-stu-id="e97c1-108">The tool includes a test Security Token Service (STS) which runs on your local machine when you launch a debug session.</span></span> <span data-ttu-id="e97c1-109">Bu nedenle, uygulamalarınızı test etmek için ihtiyacınız olan talepleri almak üzere artık özel STS projeleri oluşturmanıza ve bunlara ince ayar yapmanıza gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="e97c1-109">Therefore, you no longer need to create custom STS projects and tweak them in order to get the claims you need to test your applications.</span></span> <span data-ttu-id="e97c1-110">Talep türleri ve değerler tamamen özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e97c1-110">The claim types and values are fully customizable.</span></span>  
  
- <span data-ttu-id="e97c1-111">Ortak ayarları, web.config'i düzenlemek zorunda kalmadan doğrudan aracın kullanıcı arabirimiyle değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e97c1-111">You can modify common settings directly via the tool’s UI, without the need to edit web.config.</span></span>  
  
- <span data-ttu-id="e97c1-112">Tek bir ekranda Active Directory Federasyon Hizmetleri (AD FS) 2.0 (veya diğer WS-Federasyon sağlayıcıları) ile federasyon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e97c1-112">You can establish federation with Active Directory Federation Services (AD FS) 2.0 (or other WS-Federation providers) in a single screen.</span></span>  
  
- <span data-ttu-id="e97c1-113">Araç, kullanmak istediğiniz tüm kimlik sağlayıcıları için basit bir onay listesi ile Windows Azure Access Control Service (ACS) yeteneklerini kullanır: Facebook, Google, Live ID, Yahoo!, any OpenID sağlayıcısı ve herhangi bir WS-Federasyon sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="e97c1-113">The tool leverages Windows Azure Access Control Service (ACS) capabilities with a simple list of checkboxes for all the identity providers that you want to use: Facebook, Google, Live ID, Yahoo!, any OpenID provider, and any WS-Federation provider.</span></span> <span data-ttu-id="e97c1-114">Kimlik sağlayıcılarınızı seçin, Tamam'a tıklayın ve F5'e basın; hem uygulamanız hem de ACS otomatik olarak yapılandırılacak ve test uygulamanız ACS'yi kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="e97c1-114">Select your identity providers, click OK, then F5, and both your application and ACS will be automatically configured and your test application will be ACS-aware.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e97c1-115">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e97c1-115">See also</span></span>

- [<span data-ttu-id="e97c1-116">WIF Özellikleri</span><span class="sxs-lookup"><span data-stu-id="e97c1-116">WIF Features</span></span>](wif-features.md)
