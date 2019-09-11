---
title: 'Nasıl yapılır: Görsel Taslağı Başladıktan Sonra Denetlemek için Olay Tetikleyicilerini Kullanma'
ms.date: 03/30/2017
helpviewer_keywords:
- triggers [WPF], controlling Storyboards
- event triggers [WPF], controlling Storyboards
- Storyboards [WPF], controlling after start
ms.assetid: 3b115594-6a93-4972-b24d-61aa16f1c15f
ms.openlocfilehash: 32591edd065a8122b84ff14102f672ccf6001d67
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855853"
---
# <a name="how-to-use-event-triggers-to-control-a-storyboard-after-it-starts"></a><span data-ttu-id="e60ca-102">Nasıl yapılır: Görsel Taslağı Başladıktan Sonra Denetlemek için Olay Tetikleyicilerini Kullanma</span><span class="sxs-lookup"><span data-stu-id="e60ca-102">How to: Use Event Triggers to Control a Storyboard After It Starts</span></span>

<span data-ttu-id="e60ca-103">Bu örnek, başladıktan <xref:System.Windows.Media.Animation.Storyboard> sonra nasıl kontrol yapılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e60ca-103">This example shows how to control a <xref:System.Windows.Media.Animation.Storyboard> after it starts.</span></span> <span data-ttu-id="e60ca-104"><xref:System.Windows.Media.Animation.BeginStoryboard>Kullanarak <xref:System.Windows.Media.Animation.Storyboard> başlatmakiçin,animasyonlarınıcanlandırdıklarınesnelereveözellikleredağıtanvesonrafilmşeridiniBaşlatanöğesinikullanın.[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e60ca-104">To start a <xref:System.Windows.Media.Animation.Storyboard> by using [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], use <xref:System.Windows.Media.Animation.BeginStoryboard>, which distributes the animations to the objects and properties they animate and then starts the storyboard.</span></span> <span data-ttu-id="e60ca-105">Özelliğini belirterek bir <xref:System.Windows.Media.Animation.BeginStoryboard> ad verirseniz, denetlenebilir bir <xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A> görsel taslak yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="e60ca-105">If you give <xref:System.Windows.Media.Animation.BeginStoryboard> a name by specifying its <xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A> property, you make it a controllable storyboard.</span></span> <span data-ttu-id="e60ca-106">Sonra film şeridini başladıktan sonra etkileşimli bir şekilde denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e60ca-106">You can then interactively control the storyboard after it starts.</span></span>

<span data-ttu-id="e60ca-107">Film şeridini denetlemek için aşağıdaki film şeridi <xref:System.Windows.EventTrigger> eylemlerini nesneleriyle birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="e60ca-107">Use the following storyboard actions together with <xref:System.Windows.EventTrigger> objects to control a storyboard.</span></span>

- <span data-ttu-id="e60ca-108"><xref:System.Windows.Media.Animation.PauseStoryboard>: Film şeridini duraklatır.</span><span class="sxs-lookup"><span data-stu-id="e60ca-108"><xref:System.Windows.Media.Animation.PauseStoryboard>: Pauses the storyboard.</span></span>

- <span data-ttu-id="e60ca-109"><xref:System.Windows.Media.Animation.ResumeStoryboard>: Duraklatılmış bir film şeridini sürdürür.</span><span class="sxs-lookup"><span data-stu-id="e60ca-109"><xref:System.Windows.Media.Animation.ResumeStoryboard>: Resumes a paused storyboard.</span></span>

- <span data-ttu-id="e60ca-110"><xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>: Görsel taslak hızını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="e60ca-110"><xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>: Changes the storyboard speed.</span></span>

- <span data-ttu-id="e60ca-111"><xref:System.Windows.Media.Animation.SkipStoryboardToFill>: Bir film şeridini, varsa, kendi Fill döneminin sonuna ilerletir.</span><span class="sxs-lookup"><span data-stu-id="e60ca-111"><xref:System.Windows.Media.Animation.SkipStoryboardToFill>: Advances a storyboard to the end of its fill period, if it has one.</span></span>

- <span data-ttu-id="e60ca-112"><xref:System.Windows.Media.Animation.StopStoryboard>: Film şeridini sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="e60ca-112"><xref:System.Windows.Media.Animation.StopStoryboard>: Stops the storyboard.</span></span>

- <span data-ttu-id="e60ca-113"><xref:System.Windows.Media.Animation.RemoveStoryboard>: Kaynak şeridi kaldırır ve kaynakları serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="e60ca-113"><xref:System.Windows.Media.Animation.RemoveStoryboard>: Removes the storyboard, freeing resources.</span></span>

## <a name="example"></a><span data-ttu-id="e60ca-114">Örnek</span><span class="sxs-lookup"><span data-stu-id="e60ca-114">Example</span></span>

<span data-ttu-id="e60ca-115">Aşağıdaki örnek, bir görsel taslağı etkileşimli olarak denetlemek için denetlenebilir görsel taslak eylemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e60ca-115">The following example uses controllable storyboard actions to interactively control a storyboard.</span></span>

> [!NOTE]
> <span data-ttu-id="e60ca-116">Kodu kullanarak bir film şeridini denetlemeye ilişkin bir örnek görmek için bkz. [etkileşimli yöntemlerini kullanarak başladıktan sonra bir görsel taslağı denetleme](how-to-control-a-storyboard-after-it-starts.md).</span><span class="sxs-lookup"><span data-stu-id="e60ca-116">To see an example of controlling a storyboard by using code, see [Control a Storyboard After It Starts Using Its Interactive Methods](how-to-control-a-storyboard-after-it-starts.md).</span></span>

[!code-xaml[timingbehaviors_snip#ControlStoryboardExampleUsingWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/ControlStoryboardExample.xaml#controlstoryboardexampleusingwholepage)]

<span data-ttu-id="e60ca-117">Daha fazla örnek için [animasyon örnek galerisine](https://go.microsoft.com/fwlink/?LinkID=159969)bakın.</span><span class="sxs-lookup"><span data-stu-id="e60ca-117">For additional examples, see the [Animation Example Gallery](https://go.microsoft.com/fwlink/?LinkID=159969).</span></span>

## <a name="see-also"></a><span data-ttu-id="e60ca-118">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e60ca-118">See also</span></span>

- <xref:System.Windows.Media.Animation.ResumeStoryboard>
- <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>
- <xref:System.Windows.Media.Animation.SkipStoryboardToFill>
- <xref:System.Windows.Media.Animation.PauseStoryboard>
- <xref:System.Windows.Media.Animation.StopStoryboard>
- <xref:System.Windows.Media.Animation.SeekStoryboard>
- [<span data-ttu-id="e60ca-119">Görsel Taslağı Başladıktan Sonra Etkileşimli Yöntemlerini Kullanarak Denetleme</span><span class="sxs-lookup"><span data-stu-id="e60ca-119">Control a Storyboard After It Starts Using Its Interactive Methods</span></span>](how-to-control-a-storyboard-after-it-starts.md)
- [<span data-ttu-id="e60ca-120">Animasyona Genel bakış</span><span class="sxs-lookup"><span data-stu-id="e60ca-120">Animation Overview</span></span>](animation-overview.md)
- [<span data-ttu-id="e60ca-121">Görsel Taslaklara Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e60ca-121">Storyboards Overview</span></span>](storyboards-overview.md)
