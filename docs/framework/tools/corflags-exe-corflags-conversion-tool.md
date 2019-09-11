---
title: CorFlags.exe (CorFlags Dönüştürme Aracı)
ms.date: 03/30/2017
helpviewer_keywords:
- CorFlags conversion tool
- CorFlags.exe
- portable executable files, CorFlags section
ms.assetid: ef900f8f-71ca-4dde-9b8c-95ddb0d7d89c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4228da6efe22091c86de95d846c14f504d51457f
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70851295"
---
# <a name="corflagsexe-corflags-conversion-tool"></a><span data-ttu-id="6f335-102">CorFlags.exe (CorFlags Dönüştürme Aracı)</span><span class="sxs-lookup"><span data-stu-id="6f335-102">CorFlags.exe (CorFlags Conversion Tool)</span></span>
<span data-ttu-id="6f335-103">CorFlags Dönüştürme aracı, taşınabilir çalıştırılabilir bir görüntünün üstbilgisinin CorFlags bölümünü yapılandırmanıza olanak verir.</span><span class="sxs-lookup"><span data-stu-id="6f335-103">The CorFlags Conversion tool allows you to configure the CorFlags section of the header of a portable executable image.</span></span>  
  
 <span data-ttu-id="6f335-104">Bu araç, Visual Studio ile birlikte otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="6f335-104">This tool is automatically installed with Visual Studio.</span></span> <span data-ttu-id="6f335-105">Aracı çalıştırmak için, Visual Studio için Geliştirici Komut İstemi (veya Windows 7 ' de Visual Studio komut Istemi) kullanın.</span><span class="sxs-lookup"><span data-stu-id="6f335-105">To run the tool, use the Developer Command Prompt for Visual Studio (or the Visual Studio Command Prompt in Windows 7).</span></span> <span data-ttu-id="6f335-106">Daha fazla bilgi için bkz. [komut istemleri](../../../docs/framework/tools/developer-command-prompt-for-vs.md).</span><span class="sxs-lookup"><span data-stu-id="6f335-106">For more information, see [Command Prompts](../../../docs/framework/tools/developer-command-prompt-for-vs.md).</span></span>  
  
 <span data-ttu-id="6f335-107">Komut satırına şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="6f335-107">At the command prompt, type the following:</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6f335-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="6f335-108">Syntax</span></span>  
  
```console  
CorFlags.exe assembly [options]  
```  
  
## <a name="parameters"></a><span data-ttu-id="6f335-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6f335-109">Parameters</span></span>  
  
|<span data-ttu-id="6f335-110">Gerekli parametre</span><span class="sxs-lookup"><span data-stu-id="6f335-110">Required parameter</span></span>|<span data-ttu-id="6f335-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6f335-111">Description</span></span>|  
|------------------------|-----------------|  
|`assembly`|<span data-ttu-id="6f335-112">CorFlags'in yapılandırılacağı derlemenin adı.</span><span class="sxs-lookup"><span data-stu-id="6f335-112">The name of the assembly for which to configure the CorFlags.</span></span>|  
  
|<span data-ttu-id="6f335-113">Seçenek</span><span class="sxs-lookup"><span data-stu-id="6f335-113">Option</span></span>|<span data-ttu-id="6f335-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6f335-114">Description</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="6f335-115">**/32BIT [REQ] +**</span><span class="sxs-lookup"><span data-stu-id="6f335-115">**/32BIT[REQ]+**</span></span>|<span data-ttu-id="6f335-116">32BITREQUIRED bayrağını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="6f335-116">Sets the 32BITREQUIRED flag.</span></span>|  
|<span data-ttu-id="6f335-117">**/32BIT [REQ]-**</span><span class="sxs-lookup"><span data-stu-id="6f335-117">**/32BIT[REQ]-**</span></span>|<span data-ttu-id="6f335-118">32BITREQUIRED bayrağını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="6f335-118">Clears the 32BITREQUIRED flag.</span></span>|  
|<span data-ttu-id="6f335-119">**/32BITPREF +**</span><span class="sxs-lookup"><span data-stu-id="6f335-119">**/32BITPREF+**</span></span>|<span data-ttu-id="6f335-120">32BITPREFERRED bayrağını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="6f335-120">Sets the 32BITPREFERRED flag.</span></span> <span data-ttu-id="6f335-121">Uygulama 64-bit platformlarda dahi 32-bit işlem olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="6f335-121">The app runs as a 32-bit process even on 64-bit platforms.</span></span> <span data-ttu-id="6f335-122">Bu bayrağı yalnızca EXE dosyalarında ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6f335-122">Set this flag only on EXE files.</span></span> <span data-ttu-id="6f335-123">Bayrak dll üzerinde ayarlandıysa, dll 64-bit işlemlerde yüklenemez ve bir <xref:System.BadImageFormatException> özel durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="6f335-123">If the flag is set on a DLL, the DLL fails to load in 64-bit processes, and a <xref:System.BadImageFormatException> exception is thrown.</span></span> <span data-ttu-id="6f335-124">Bu bayrağı içeren bir EXE dosyası bir 64-bit işleme yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6f335-124">An EXE file with this flag can be loaded into a 64-bit process.</span></span><br /><br /> <span data-ttu-id="6f335-125">.NET Framework 4,5 ' de yenidir.</span><span class="sxs-lookup"><span data-stu-id="6f335-125">New in the .NET Framework 4.5.</span></span>|  
|<span data-ttu-id="6f335-126">**/32BITTERCIH-**</span><span class="sxs-lookup"><span data-stu-id="6f335-126">**/32BITPREF-**</span></span>|<span data-ttu-id="6f335-127">32BITPREFERRED bayrağını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="6f335-127">Clears the 32BITPREFERRED flag.</span></span><br /><br /> <span data-ttu-id="6f335-128">.NET Framework 4,5 ' de yenidir.</span><span class="sxs-lookup"><span data-stu-id="6f335-128">New in the .NET Framework 4.5.</span></span>|  
|<span data-ttu-id="6f335-129">**/?**</span><span class="sxs-lookup"><span data-stu-id="6f335-129">**/?**</span></span>|<span data-ttu-id="6f335-130">Araç için komut sözdizimini ve seçenekleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6f335-130">Displays command syntax and options for the tool.</span></span>|  
|<span data-ttu-id="6f335-131">**/Force**</span><span class="sxs-lookup"><span data-stu-id="6f335-131">**/Force**</span></span>|<span data-ttu-id="6f335-132">Derleme bir tanımlayıcı adla adlandırılmış olsa da bir güncelleştirmenin yapılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6f335-132">Forces an update even if the assembly is strong-named.</span></span> <span data-ttu-id="6f335-133">**Önemli:**  Tanımlayıcı bir adla adlandırılmış bir derlemeyi güncelleştirirseniz, kodunu yürütülmeden önce onu tekrar imzalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f335-133">**Important:**  If you update a strong-named assembly, you must sign it again before executing its code.</span></span>|  
|<span data-ttu-id="6f335-134">**/ Help**</span><span class="sxs-lookup"><span data-stu-id="6f335-134">**/help**</span></span>|<span data-ttu-id="6f335-135">Araç için komut sözdizimini ve seçenekleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6f335-135">Displays command syntax and options for the tool.</span></span>|  
|<span data-ttu-id="6f335-136">**/ILONLY +**</span><span class="sxs-lookup"><span data-stu-id="6f335-136">**/ILONLY+**</span></span>|<span data-ttu-id="6f335-137">ILONLY bayrağını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="6f335-137">Sets the ILONLY flag.</span></span>|  
|<span data-ttu-id="6f335-138">**ILONLY**</span><span class="sxs-lookup"><span data-stu-id="6f335-138">**/ILONLY-**</span></span>|<span data-ttu-id="6f335-139">ILONLY bayrağını kaldırır.</span><span class="sxs-lookup"><span data-stu-id="6f335-139">Clears the ILONLY flag.</span></span>|  
|<span data-ttu-id="6f335-140">**/nologo**</span><span class="sxs-lookup"><span data-stu-id="6f335-140">**/nologo**</span></span>|<span data-ttu-id="6f335-141">Microsoft başlangıç başlığı görüntüsünü bastırır.</span><span class="sxs-lookup"><span data-stu-id="6f335-141">Suppresses the Microsoft startup banner display.</span></span>|  
|<span data-ttu-id="6f335-142">**/RevertCLRHeader**</span><span class="sxs-lookup"><span data-stu-id="6f335-142">**/RevertCLRHeader**</span></span>|<span data-ttu-id="6f335-143">CLR üstbilgisini 2.0 sürümüne döndürür.</span><span class="sxs-lookup"><span data-stu-id="6f335-143">Reverts the CLR header version to 2.0.</span></span>|  
|<span data-ttu-id="6f335-144">**/UpgradeCLRHeader**</span><span class="sxs-lookup"><span data-stu-id="6f335-144">**/UpgradeCLRHeader**</span></span>|<span data-ttu-id="6f335-145">CLR üstbilgisini 2.5 sürümüne yükseltir.</span><span class="sxs-lookup"><span data-stu-id="6f335-145">Upgrades the CLR header version to 2.5.</span></span> <span data-ttu-id="6f335-146">**Not:**  Yerel olarak çalışması için derlemelerde CLR üstbilgi sürümü 2.5 veya daha üstü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6f335-146">**Note:**  Assemblies must have a CLR header version of 2.5 or greater to run natively.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="6f335-147">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="6f335-147">Remarks</span></span>  
 <span data-ttu-id="6f335-148">Hiçbir seçenek belirtilmezse, CorFlags Dönüştürme aracı belirtilen derleme için bayrakları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6f335-148">If no options are specified, the CorFlags Conversion tool displays the flags for the specified assembly.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6f335-149">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="6f335-149">See also</span></span>

- [<span data-ttu-id="6f335-150">Araçlar</span><span class="sxs-lookup"><span data-stu-id="6f335-150">Tools</span></span>](../../../docs/framework/tools/index.md)
- [<span data-ttu-id="6f335-151">64 bit Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="6f335-151">64-bit Applications</span></span>](../../../docs/framework/64-bit-apps.md)
- [<span data-ttu-id="6f335-152">Komut İstemleri</span><span class="sxs-lookup"><span data-stu-id="6f335-152">Command Prompts</span></span>](../../../docs/framework/tools/developer-command-prompt-for-vs.md)
