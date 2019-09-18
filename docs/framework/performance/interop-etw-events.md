---
title: Birlikte Çalışma ETW Olayları
ms.date: 03/30/2017
helpviewer_keywords:
- interop events [.NET Framework]
- ETW, interop events (CLR)
ms.assetid: eb6eac2e-45f4-4923-a32c-38f203da66df
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 787c6221b651a53dbb932a5a9d0edea123e1d97d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046429"
---
# <a name="interop-etw-events"></a><span data-ttu-id="cc2c3-102">Birlikte Çalışma ETW Olayları</span><span class="sxs-lookup"><span data-stu-id="cc2c3-102">Interop ETW Events</span></span>
<a name="top"></a><span data-ttu-id="cc2c3-103">Birlikte çalışma olayları, Microsoft ara dili (MSIL) saplama oluşturma ve önbelleğe alma hakkında bilgi yakalar.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-103">Interop events capture information about Microsoft intermediate language (MSIL) stub generation and caching.</span></span>  
  
 <span data-ttu-id="cc2c3-104">Bu kategori aşağıdaki olaylardan oluşur:</span><span class="sxs-lookup"><span data-stu-id="cc2c3-104">This category consists of the following events:</span></span>  
  
- [<span data-ttu-id="cc2c3-105">ILStubGenerated olayı</span><span class="sxs-lookup"><span data-stu-id="cc2c3-105">ILStubGenerated Event</span></span>](#ilstubgenerated_event)  
  
- [<span data-ttu-id="cc2c3-106">ILStubCacheHit olayı</span><span class="sxs-lookup"><span data-stu-id="cc2c3-106">ILStubCacheHit Event</span></span>](#ilstubcachehit_event)  
  
<a name="ilstubgenerated_event"></a>   
## <a name="ilstubgenerated-event"></a><span data-ttu-id="cc2c3-107">ILStubGenerated olayı</span><span class="sxs-lookup"><span data-stu-id="cc2c3-107">ILStubGenerated Event</span></span>  
 <span data-ttu-id="cc2c3-108">Aşağıdaki tabloda anahtar sözcüğü ve düzeyi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-108">The following table shows the keyword and level.</span></span> <span data-ttu-id="cc2c3-109">(Daha fazla bilgi için bkz. [CLR ETW anahtar sözcükleri ve düzeyleri](clr-etw-keywords-and-levels.md).)</span><span class="sxs-lookup"><span data-stu-id="cc2c3-109">(For more information, see [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md).)</span></span>  
  
|<span data-ttu-id="cc2c3-110">Olayı yükseltmek için anahtar sözcük</span><span class="sxs-lookup"><span data-stu-id="cc2c3-110">Keyword for raising the event</span></span>|<span data-ttu-id="cc2c3-111">Düzey</span><span class="sxs-lookup"><span data-stu-id="cc2c3-111">Level</span></span>|  
|-----------------------------------|-----------|  
|<span data-ttu-id="cc2c3-112">`InteropKeyword`(0x2000)</span><span class="sxs-lookup"><span data-stu-id="cc2c3-112">`InteropKeyword` (0x2000)</span></span>|<span data-ttu-id="cc2c3-113">Bilgilendirici (4)</span><span class="sxs-lookup"><span data-stu-id="cc2c3-113">Informational(4)</span></span>|  
  
 <span data-ttu-id="cc2c3-114">Aşağıdaki tabloda olay bilgileri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-114">The following table shows the event information.</span></span>  
  
|<span data-ttu-id="cc2c3-115">Olay</span><span class="sxs-lookup"><span data-stu-id="cc2c3-115">Event</span></span>|<span data-ttu-id="cc2c3-116">Olay Kimliği</span><span class="sxs-lookup"><span data-stu-id="cc2c3-116">Event ID</span></span>|<span data-ttu-id="cc2c3-117">Ne zaman oluşturulur</span><span class="sxs-lookup"><span data-stu-id="cc2c3-117">Raised when</span></span>|  
|-----------|--------------|-----------------|  
|`ILStubGenerated`|<span data-ttu-id="cc2c3-118">88</span><span class="sxs-lookup"><span data-stu-id="cc2c3-118">88</span></span>|<span data-ttu-id="cc2c3-119">MSIL saplaması oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-119">The MSIL stub has been generated.</span></span>|  
  
 <span data-ttu-id="cc2c3-120">Aşağıdaki tabloda olay verileri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-120">The following table shows the event data.</span></span>  
  
|<span data-ttu-id="cc2c3-121">Alan adı</span><span class="sxs-lookup"><span data-stu-id="cc2c3-121">Field name</span></span>|<span data-ttu-id="cc2c3-122">Veri türü</span><span class="sxs-lookup"><span data-stu-id="cc2c3-122">Data type</span></span>|<span data-ttu-id="cc2c3-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc2c3-123">Description</span></span>|  
|----------------|---------------|-----------------|  
|<span data-ttu-id="cc2c3-124">Modül kimliği</span><span class="sxs-lookup"><span data-stu-id="cc2c3-124">ModuleID</span></span>|<span data-ttu-id="cc2c3-125">Win: UInt16</span><span class="sxs-lookup"><span data-stu-id="cc2c3-125">win:UInt16</span></span>|<span data-ttu-id="cc2c3-126">Modül tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-126">The module identifier.</span></span>|  
|<span data-ttu-id="cc2c3-127">StubMethodID</span><span class="sxs-lookup"><span data-stu-id="cc2c3-127">StubMethodID</span></span>|<span data-ttu-id="cc2c3-128">Win: UInt64</span><span class="sxs-lookup"><span data-stu-id="cc2c3-128">win:UInt64</span></span>|<span data-ttu-id="cc2c3-129">Saplama yöntemi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-129">The stub method identifier.</span></span>|  
|<span data-ttu-id="cc2c3-130">StubFlags</span><span class="sxs-lookup"><span data-stu-id="cc2c3-130">StubFlags</span></span>|<span data-ttu-id="cc2c3-131">Win: UInt64</span><span class="sxs-lookup"><span data-stu-id="cc2c3-131">win:UInt64</span></span>|<span data-ttu-id="cc2c3-132">Saplama bayrakları:</span><span class="sxs-lookup"><span data-stu-id="cc2c3-132">The flags for the stub:</span></span><br /><br /> <span data-ttu-id="cc2c3-133">0x1-ters çalışabilirliği.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-133">0x1 - Reverse interop.</span></span><br /><br /> <span data-ttu-id="cc2c3-134">0x2-COM birlikte çalışma.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-134">0x2 - COM interop.</span></span><br /><br /> <span data-ttu-id="cc2c3-135">0x4-NGen. exe tarafından oluşturulan saplama.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-135">0x4 - Stub generated by NGen.exe.</span></span><br /><br /> <span data-ttu-id="cc2c3-136">0x8-temsilci.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-136">0x8 - Delegate.</span></span><br /><br /> <span data-ttu-id="cc2c3-137">0x10-değişken bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-137">0x10 - Variable argument.</span></span><br /><br /> <span data-ttu-id="cc2c3-138">0x20-yönetilmeyen aranan.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-138">0x20 - Unmanaged callee.</span></span>|  
|<span data-ttu-id="cc2c3-139">ManagedInteropMethodToken</span><span class="sxs-lookup"><span data-stu-id="cc2c3-139">ManagedInteropMethodToken</span></span>|<span data-ttu-id="cc2c3-140">Win: UInt32</span><span class="sxs-lookup"><span data-stu-id="cc2c3-140">win:UInt32</span></span>|<span data-ttu-id="cc2c3-141">Managed Interop yöntemi için belirteç.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-141">The token for the managed interop method.</span></span>|  
|<span data-ttu-id="cc2c3-142">ManagedInteropMethodNameSpace</span><span class="sxs-lookup"><span data-stu-id="cc2c3-142">ManagedInteropMethodNameSpace</span></span>|<span data-ttu-id="cc2c3-143">Win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="cc2c3-143">win:UnicodeString</span></span>|<span data-ttu-id="cc2c3-144">Managed Interop yönteminin ad alanı.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-144">The namespace of the managed interop method.</span></span>|  
|<span data-ttu-id="cc2c3-145">ManagedInteropMethodName</span><span class="sxs-lookup"><span data-stu-id="cc2c3-145">ManagedInteropMethodName</span></span>|<span data-ttu-id="cc2c3-146">Win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="cc2c3-146">win:UnicodeString</span></span>|<span data-ttu-id="cc2c3-147">Yönetilen birlikte çalışma yönteminin adı.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-147">The name of the managed interop method.</span></span>|  
|<span data-ttu-id="cc2c3-148">ManagedInteropMethodSignature</span><span class="sxs-lookup"><span data-stu-id="cc2c3-148">ManagedInteropMethodSignature</span></span>|<span data-ttu-id="cc2c3-149">Win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="cc2c3-149">win:UnicodeString</span></span>|<span data-ttu-id="cc2c3-150">Managed Interop yönteminin imzası.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-150">The signature of the managed interop method.</span></span>|  
|<span data-ttu-id="cc2c3-151">NativeMethodSignature</span><span class="sxs-lookup"><span data-stu-id="cc2c3-151">NativeMethodSignature</span></span>|<span data-ttu-id="cc2c3-152">Win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="cc2c3-152">win:UnicodeString</span></span>|<span data-ttu-id="cc2c3-153">Yerel Yöntem imzası.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-153">The native method signature.</span></span>|  
|<span data-ttu-id="cc2c3-154">StubMethodSignature</span><span class="sxs-lookup"><span data-stu-id="cc2c3-154">StubMethodSignature</span></span>|<span data-ttu-id="cc2c3-155">Win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="cc2c3-155">win:UnicodeString</span></span>|<span data-ttu-id="cc2c3-156">Saplama yöntemi imzası.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-156">The stub method signature.</span></span>|  
|<span data-ttu-id="cc2c3-157">StubMethodILCode</span><span class="sxs-lookup"><span data-stu-id="cc2c3-157">StubMethodILCode</span></span>|<span data-ttu-id="cc2c3-158">Win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="cc2c3-158">win:UnicodeString</span></span>|<span data-ttu-id="cc2c3-159">Saplama yöntemi için MSIL kodu.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-159">The MSIL code for the stub method.</span></span>|  
|<span data-ttu-id="cc2c3-160">ClrInstanceID</span><span class="sxs-lookup"><span data-stu-id="cc2c3-160">ClrInstanceID</span></span>|<span data-ttu-id="cc2c3-161">Win: UInt16</span><span class="sxs-lookup"><span data-stu-id="cc2c3-161">win:UInt16</span></span>|<span data-ttu-id="cc2c3-162">CLR veya CoreCLR örneği için benzersiz KIMLIK.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-162">Unique ID for the instance of CLR or CoreCLR.</span></span>|  
  
 [<span data-ttu-id="cc2c3-163">Başa dön</span><span class="sxs-lookup"><span data-stu-id="cc2c3-163">Back to top</span></span>](#top)  
  
<a name="ilstubcachehit_event"></a>   
## <a name="ilstubcachehit-event"></a><span data-ttu-id="cc2c3-164">ILStubCacheHit olayı</span><span class="sxs-lookup"><span data-stu-id="cc2c3-164">ILStubCacheHit Event</span></span>  
 <span data-ttu-id="cc2c3-165">Aşağıdaki tabloda anahtar sözcüğü ve düzeyi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-165">The following table shows the keyword and level.</span></span>  
  
|<span data-ttu-id="cc2c3-166">Olayı yükseltmek için anahtar sözcük</span><span class="sxs-lookup"><span data-stu-id="cc2c3-166">Keyword for raising the event</span></span>|<span data-ttu-id="cc2c3-167">Düzey</span><span class="sxs-lookup"><span data-stu-id="cc2c3-167">Level</span></span>|  
|-----------------------------------|-----------|  
|<span data-ttu-id="cc2c3-168">`InteropKeyword`(0x2000)</span><span class="sxs-lookup"><span data-stu-id="cc2c3-168">`InteropKeyword` (0x2000)</span></span>|<span data-ttu-id="cc2c3-169">Bilgilendirici (4)</span><span class="sxs-lookup"><span data-stu-id="cc2c3-169">Informational(4)</span></span>|  
  
 <span data-ttu-id="cc2c3-170">Aşağıdaki tabloda olay bilgileri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-170">The following table shows the event information.</span></span>  
  
|<span data-ttu-id="cc2c3-171">Olay</span><span class="sxs-lookup"><span data-stu-id="cc2c3-171">Event</span></span>|<span data-ttu-id="cc2c3-172">Olay Kimliği</span><span class="sxs-lookup"><span data-stu-id="cc2c3-172">Event ID</span></span>|<span data-ttu-id="cc2c3-173">Ne zaman oluşturulur</span><span class="sxs-lookup"><span data-stu-id="cc2c3-173">Raised when</span></span>|  
|-----------|--------------|-----------------|  
|`ILStubCacheHit`|<span data-ttu-id="cc2c3-174">89</span><span class="sxs-lookup"><span data-stu-id="cc2c3-174">89</span></span>|<span data-ttu-id="cc2c3-175">MSIL önbelleğine erişildi.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-175">The MSIL cache has been accessed.</span></span>|  
  
 <span data-ttu-id="cc2c3-176">Aşağıdaki tabloda olay verileri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-176">The following table shows the event data.</span></span>  
  
|<span data-ttu-id="cc2c3-177">Alan adı</span><span class="sxs-lookup"><span data-stu-id="cc2c3-177">Field name</span></span>|<span data-ttu-id="cc2c3-178">Veri türü</span><span class="sxs-lookup"><span data-stu-id="cc2c3-178">Data type</span></span>|<span data-ttu-id="cc2c3-179">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc2c3-179">Description</span></span>|  
|----------------|---------------|-----------------|  
|<span data-ttu-id="cc2c3-180">Modül kimliği</span><span class="sxs-lookup"><span data-stu-id="cc2c3-180">ModuleID</span></span>|<span data-ttu-id="cc2c3-181">Win: UInt16</span><span class="sxs-lookup"><span data-stu-id="cc2c3-181">win:UInt16</span></span>|<span data-ttu-id="cc2c3-182">Modül tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-182">The module identifier.</span></span>|  
|<span data-ttu-id="cc2c3-183">StubMethodID</span><span class="sxs-lookup"><span data-stu-id="cc2c3-183">StubMethodID</span></span>|<span data-ttu-id="cc2c3-184">Win: UInt64</span><span class="sxs-lookup"><span data-stu-id="cc2c3-184">win:UInt64</span></span>|<span data-ttu-id="cc2c3-185">Saplama yöntemi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-185">The stub method identifier.</span></span>|  
|<span data-ttu-id="cc2c3-186">ManagedInteropMethodToken</span><span class="sxs-lookup"><span data-stu-id="cc2c3-186">ManagedInteropMethodToken</span></span>|<span data-ttu-id="cc2c3-187">Win: UInt32</span><span class="sxs-lookup"><span data-stu-id="cc2c3-187">win:UInt32</span></span>|<span data-ttu-id="cc2c3-188">Managed Interop yöntemi için belirteç.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-188">The token for the managed interop method.</span></span>|  
|<span data-ttu-id="cc2c3-189">ManagedInteropMethodNameSpace</span><span class="sxs-lookup"><span data-stu-id="cc2c3-189">ManagedInteropMethodNameSpace</span></span>|<span data-ttu-id="cc2c3-190">Win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="cc2c3-190">win:UnicodeString</span></span>|<span data-ttu-id="cc2c3-191">Managed Interop yönteminin ad alanı.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-191">The namespace of the managed interop method.</span></span>|  
|<span data-ttu-id="cc2c3-192">ManagedInteropMethodName</span><span class="sxs-lookup"><span data-stu-id="cc2c3-192">ManagedInteropMethodName</span></span>|<span data-ttu-id="cc2c3-193">Win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="cc2c3-193">win:UnicodeString</span></span>|<span data-ttu-id="cc2c3-194">Yönetilen birlikte çalışma yönteminin adı.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-194">The name of the managed interop method.</span></span>|  
|<span data-ttu-id="cc2c3-195">ManagedInteropMethodSignature</span><span class="sxs-lookup"><span data-stu-id="cc2c3-195">ManagedInteropMethodSignature</span></span>|<span data-ttu-id="cc2c3-196">Win: UnicodeString</span><span class="sxs-lookup"><span data-stu-id="cc2c3-196">win:UnicodeString</span></span>|<span data-ttu-id="cc2c3-197">Managed Interop yönteminin imzası.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-197">The signature of the managed interop method.</span></span>|  
|<span data-ttu-id="cc2c3-198">ClrInstanceID</span><span class="sxs-lookup"><span data-stu-id="cc2c3-198">ClrInstanceID</span></span>|<span data-ttu-id="cc2c3-199">Win: UInt16</span><span class="sxs-lookup"><span data-stu-id="cc2c3-199">win:UInt16</span></span>|<span data-ttu-id="cc2c3-200">CLR veya CoreCLR örneği için benzersiz KIMLIK.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-200">Unique ID for the instance of CLR or CoreCLR.</span></span>|  
  
 [<span data-ttu-id="cc2c3-201">Başa dön</span><span class="sxs-lookup"><span data-stu-id="cc2c3-201">Back to top</span></span>](#top)  
  
## <a name="see-also"></a><span data-ttu-id="cc2c3-202">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="cc2c3-202">See also</span></span>

- [<span data-ttu-id="cc2c3-203">CLR ETW Olayları</span><span class="sxs-lookup"><span data-stu-id="cc2c3-203">CLR ETW Events</span></span>](clr-etw-events.md)
