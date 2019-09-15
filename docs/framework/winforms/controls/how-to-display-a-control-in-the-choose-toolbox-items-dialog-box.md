---
title: 'Nasıl yapılır: Araç Kutusu Öğelerini Seç İletişim Kutusunda bir Denetimi Görüntüleme'
ms.date: 08/23/2019
helpviewer_keywords:
- global assembly cache [Windows Forms], Choose Toolbox Items dialog box
- AssemblyFoldersEx [Windows Forms], Choose Toolbox Items dialog box
- controls [Windows Forms], display in Choose Toolbox Items dialog box
- assembly folder registration [Windows Forms], Choose Toolbox Items dialog box
- Choose Toolbox Items dialog box [Windows Forms], display control
ms.assetid: 01ef6eba-d044-40f0-951d-78eff7ebd9a9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f52c1d127df8f0e831db0749e3453bb1c54d5886
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972064"
---
# <a name="how-to-display-a-control-in-the-choose-toolbox-items-dialog-box"></a><span data-ttu-id="f7aff-102">Nasıl yapılır: Araç Kutusu Öğelerini Seç İletişim Kutusunda bir Denetimi Görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f7aff-102">How to: Display a Control in the Choose Toolbox Items Dialog Box</span></span>

<span data-ttu-id="f7aff-103">Denetimleri geliştirip dağıtırken, **araç** kutusunu sağ tıklayıp **öğeleri seç**' i seçtiğinizde görüntülenen Visual Studio 'Nun **araç kutusu öğelerini Seç** iletişim kutusunda bu denetimlerin görünmesini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7aff-103">As you develop and distribute controls, you may want those controls to appear in the **Choose Toolbox Items** dialog box of Visual Studio, which is displayed when you right-click the **Toolbox** and select **Choose Items**.</span></span> <span data-ttu-id="f7aff-104">AssemblyFoldersEx kayıt yordamını kullanarak denetiminizin bu iletişim kutusunda görünmesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7aff-104">You can enable your control to appear in this dialog box by using the AssemblyFoldersEx registration procedure.</span></span>

<span data-ttu-id="f7aff-105">Denetiminizi araç kutusu öğelerini Seç iletişim kutusunda göstermek için:</span><span class="sxs-lookup"><span data-stu-id="f7aff-105">To display your control in the Choose Toolbox Items dialog box:</span></span>

- <span data-ttu-id="f7aff-106">Denetim derlemenizi genel bütünleştirilmiş kod önbelleğine yükler.</span><span class="sxs-lookup"><span data-stu-id="f7aff-106">Install your control assembly to the global assembly cache.</span></span> <span data-ttu-id="f7aff-107">Daha fazla bilgi için [nasıl yapılır: Bir derlemeyi genel bütünleştirilmiş kod önbelleğine yükler](../../app-domains/install-assembly-into-gac.md)</span><span class="sxs-lookup"><span data-stu-id="f7aff-107">For more information, see [How to: Install an Assembly into the Global Assembly Cache](../../app-domains/install-assembly-into-gac.md)</span></span>

  <span data-ttu-id="f7aff-108">-veya-</span><span class="sxs-lookup"><span data-stu-id="f7aff-108">-or-</span></span>

- <span data-ttu-id="f7aff-109">AssemblyFoldersEx kayıt yordamını kullanarak denetiminizi ve onunla ilişkili tasarım zamanı derlemelerini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f7aff-109">Register your control and its associated design-time assemblies by using the AssemblyFoldersEx registration procedure.</span></span> <span data-ttu-id="f7aff-110">AssemblyFoldersEx, üçüncü taraf satıcıların destekledikleri her bir sürüm için yolları depolayacağı bir kayıt defteri konumudur.</span><span class="sxs-lookup"><span data-stu-id="f7aff-110">AssemblyFoldersEx is a registry location where third-party vendors store paths for each version of the framework that they support.</span></span> <span data-ttu-id="f7aff-111">Tasarım zamanı çözümlemesi, başvuru derlemelerini bulmak için bu kayıt defteri konumuna bakabilir.</span><span class="sxs-lookup"><span data-stu-id="f7aff-111">Design-time resolution can look in this registry location to find reference assemblies.</span></span> <span data-ttu-id="f7aff-112">Kayıt defteri betiği, araç kutusunda görünmesini istediğiniz denetimleri belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="f7aff-112">The registry script can specify the controls you want to appear in the Toolbox.</span></span>

## <a name="see-also"></a><span data-ttu-id="f7aff-113">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f7aff-113">See also</span></span>

- [<span data-ttu-id="f7aff-114">Tasarım Zamanında Windows Forms Denetimleri Geliştirme</span><span class="sxs-lookup"><span data-stu-id="f7aff-114">Developing Windows Forms Controls at Design Time</span></span>](developing-windows-forms-controls-at-design-time.md)
- [<span data-ttu-id="f7aff-115">Nasıl yapılır: Bir derlemeyi genel bütünleştirilmiş kod önbelleğine yükler</span><span class="sxs-lookup"><span data-stu-id="f7aff-115">How to: Install an Assembly into the Global Assembly Cache</span></span>](../../app-domains/install-assembly-into-gac.md)
- [<span data-ttu-id="f7aff-116">İzlenecek yol: Araç kutusunu özel bileşenlerle otomatik olarak doldurma</span><span class="sxs-lookup"><span data-stu-id="f7aff-116">Walkthrough: Automatically Populating the Toolbox with Custom Components</span></span>](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)
