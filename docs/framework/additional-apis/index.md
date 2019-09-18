---
title: Ek sınıf kitaplıkları ve API'ler
ms.date: 01/29/2018
helpviewer_keywords:
- Additional class libraries
- Additional managed libraries
- .NET Framework out-of-band releases
- out-of-band releases
ms.assetid: cf2d9006-b631-4e5d-81cd-20aab78c60f1
author: mairaw
ms.author: mairaw
ms.topic: conceptual
ms.openlocfilehash: 0aed6f32bbd3ffdc9446e9d17be2d90c62444ee1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053252"
---
# <a name="additional-class-libraries-and-apis"></a><span data-ttu-id="b7a9d-102">Ek sınıf kitaplıkları ve API'ler</span><span class="sxs-lookup"><span data-stu-id="b7a9d-102">Additional class libraries and APIs</span></span>

<span data-ttu-id="b7a9d-103">.NET Framework sürekli olarak gelişiyor.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-103">The .NET Framework is constantly evolving.</span></span> <span data-ttu-id="b7a9d-104">Platformlar arası geliştirmeyi artırmak ve yeni işlevselliği erken sunmak için yeni özellikler bant dışı (OOB) olarak serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-104">To improve cross-platform development and introduce new functionality early, new features are released out of band (OOB).</span></span> <span data-ttu-id="b7a9d-105">Bu konu, için belge sağlamamız gereken OOB projelerini listeler.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-105">This topic lists the OOB projects that we provide documentation for.</span></span>  
  
<span data-ttu-id="b7a9d-106">Ayrıca, bazı kitaplıklar belirli platformları veya .NET Framework uygulamalarını hedeflemelidir.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-106">In addition, some libraries target specific platforms or implementations of the .NET Framework.</span></span> <span data-ttu-id="b7a9d-107">Örneğin, <xref:System.Text.CodePagesEncodingProvider> sınıfı kod sayfası kodlamalarını .NET Framework kullanılarak geliştirilen UWP uygulamaları için kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-107">For example, the <xref:System.Text.CodePagesEncodingProvider> class makes code page encodings available to UWP apps developed using the .NET Framework.</span></span> <span data-ttu-id="b7a9d-108">Bu konu başlığı altında da bu kitaplıklar listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-108">This topic lists these libraries as well.</span></span>  
  
## <a name="oob-projects"></a><span data-ttu-id="b7a9d-109">OOB projeleri</span><span class="sxs-lookup"><span data-stu-id="b7a9d-109">OOB projects</span></span>
  
| <span data-ttu-id="b7a9d-110">Project</span><span class="sxs-lookup"><span data-stu-id="b7a9d-110">Project</span></span> | <span data-ttu-id="b7a9d-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b7a9d-111">Description</span></span> |  
| ------- | ----------- |  
| <xref:System.Collections.Immutable> | <span data-ttu-id="b7a9d-112">, İş parçacığı açısından güvenli olan ve içeriklerinin hiçbir şekilde değişmeme garantisi sağlayan koleksiyonlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-112">Provides collections that are thread safe and guaranteed to never change their contents.</span></span> |
| <xref:System.Net.Http.WinHttpHandler> | <span data-ttu-id="b7a9d-113">Windows 'un WinHTTP arabirimine <xref:System.Net.Http.HttpClient> dayalı olarak bir ileti işleyicisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-113">Provides a message handler for <xref:System.Net.Http.HttpClient> based on the WinHTTP interface of Windows.</span></span> |
| <xref:System.Numerics> | <span data-ttu-id="b7a9d-114">SıMD donanım tabanlı hızlandırmasının avantajlarından yararlanan bir vektör türleri kitaplığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-114">Provides a library of vector types that can take advantage of SIMD hardware-based acceleration.</span></span>| 
| <xref:System.Threading.Tasks.Dataflow> | <span data-ttu-id="b7a9d-115">TPL veri akışı kitaplığı, eşzamanlılık özellikli uygulamaların sağlamlığını artırmaya yardımcı olmak için veri akışı bileşenleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-115">The TPL Dataflow Library provides dataflow components to help increase the robustness of concurrency-enabled applications.</span></span> |  

## <a name="platform-specific-libraries"></a><span data-ttu-id="b7a9d-116">Platforma özgü kitaplıklar</span><span class="sxs-lookup"><span data-stu-id="b7a9d-116">Platform-specific libraries</span></span>
  
| <span data-ttu-id="b7a9d-117">Project</span><span class="sxs-lookup"><span data-stu-id="b7a9d-117">Project</span></span> | <span data-ttu-id="b7a9d-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b7a9d-118">Description</span></span> |  
| ------- | ----------- |  
| <xref:System.Text.CodePagesEncodingProvider> | <span data-ttu-id="b7a9d-119">Kod sayfası kodlamalarını Evrensel Windows platformu hedefleyen uygulamalar için kullanılabilir hale getirmek için sınıfınıgenişletir.<xref:System.Text.EncodingProvider></span><span class="sxs-lookup"><span data-stu-id="b7a9d-119">Extends the <xref:System.Text.EncodingProvider> class to make code page encodings available to apps that target the Universal Windows Platform.</span></span> |  
  
## <a name="private-apis"></a><span data-ttu-id="b7a9d-120">Özel API 'Ler</span><span class="sxs-lookup"><span data-stu-id="b7a9d-120">Private APIs</span></span>  

<span data-ttu-id="b7a9d-121">Bu API 'Ler ürün altyapısını destekler ve doğrudan kodunuzdan kullanılmak üzere tasarlanmamıştır/desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-121">These APIs support the product infrastructure and are not intended/supported to be used directly from your code.</span></span>  
  
| <span data-ttu-id="b7a9d-122">API adı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-122">API Name</span></span> |
| -------- |
| [<span data-ttu-id="b7a9d-123">System .net. Connection sınıfı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-123">System.Net.Connection Class</span></span>](connection.md) |
| [<span data-ttu-id="b7a9d-124">System .net. Connection. d\_writelist alanı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-124">System.Net.Connection.m\_WriteList Field</span></span>](m_writelist.md) |
| [<span data-ttu-id="b7a9d-125">System .net. ConnectionGroup sınıfı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-125">System.Net.ConnectionGroup Class</span></span>](connectiongroup.md) |
| [<span data-ttu-id="b7a9d-126">System.Net.ConnectionGroup.m\_ConnectionList Field</span><span class="sxs-lookup"><span data-stu-id="b7a9d-126">System.Net.ConnectionGroup.m\_ConnectionList Field</span></span>](m_connectionlist.md) |
| [<span data-ttu-id="b7a9d-127">System .net. CoreResponseData sınıfı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-127">System.Net.CoreResponseData Class</span></span>](coreresponsedata.md) |
| [<span data-ttu-id="b7a9d-128">System .net. CoreResponseData. d\_ResponseHeaders alanı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-128">System.Net.CoreResponseData.m\_ResponseHeaders Field</span></span>](coreresponsedata_m_responseheaders.md) |
| [<span data-ttu-id="b7a9d-129">System .net. CoreResponseData.\_mstatuscode alanı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-129">System.Net.CoreResponseData.m\_StatusCode Field</span></span>](coreresponsedata_m_statuscode.md) |
| [<span data-ttu-id="b7a9d-130">Sistem .net. HttpWebRequest. \_Oto yeniden yönlendirmeler alanı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-130">System.Net.HttpWebRequest.\_AutoRedirects Field</span></span>](_autoredirects.md) |
| [<span data-ttu-id="b7a9d-131">Sistem .net. HttpWebRequest. \_CoreResponse alanı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-131">System.Net.HttpWebRequest.\_CoreResponse Field</span></span>](httpwebrequest__coreresponse.md) |
| [<span data-ttu-id="b7a9d-132">Sistem .net. HttpWebRequest. \_HttpResponse alanı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-132">System.Net.HttpWebRequest.\_HttpResponse Field</span></span>](_httpresponse.md) |
| [<span data-ttu-id="b7a9d-133">System.Net.ServicePoint.m\_ConnectionGroupList Field</span><span class="sxs-lookup"><span data-stu-id="b7a9d-133">System.Net.ServicePoint.m\_ConnectionGroupList Field</span></span>](m_connectiongrouplist.md) |
| [<span data-ttu-id="b7a9d-134">System.Net.ServicePointManager.s\_ServicePointTable Field</span><span class="sxs-lookup"><span data-stu-id="b7a9d-134">System.Net.ServicePointManager.s\_ServicePointTable Field</span></span>](s_servicepointtable.md) |
| [<span data-ttu-id="b7a9d-135">System. Windows. Diagnostics. VisualDiagnostics. s\_ıdebuggercheckdisabledfortestamaçlar alanı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-135">System.Windows.Diagnostics.VisualDiagnostics.s\_isDebuggerCheckDisabledForTestPurposes Field</span></span>](s-isdebuggercheckdisabledfortestpurposes-field.md) |
| [<span data-ttu-id="b7a9d-136">System. Windows. Forms. Design. DataMemberFieldEditor sınıfı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-136">System.Windows.Forms.Design.DataMemberFieldEditor Class</span></span>](datamemberfieldeditor-class.md) |
| [<span data-ttu-id="b7a9d-137">System. Windows. Forms. Design. Datamemberlistedıtor sınıfı</span><span class="sxs-lookup"><span data-stu-id="b7a9d-137">System.Windows.Forms.Design.DataMemberListEditor Class</span></span>](datamemberlisteditor-class.md) |
  
## <a name="see-also"></a><span data-ttu-id="b7a9d-138">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b7a9d-138">See also</span></span>

- [<span data-ttu-id="b7a9d-139">.NET Framework ve Bant Dışı Yayınlar</span><span class="sxs-lookup"><span data-stu-id="b7a9d-139">The .NET Framework and Out-of-Band Releases</span></span>](../get-started/the-net-framework-and-out-of-band-releases.md)
