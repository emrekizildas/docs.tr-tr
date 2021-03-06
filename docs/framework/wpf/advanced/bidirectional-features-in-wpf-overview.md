---
title: WPF Genel Bakışında Çift Yönlü Özellikler
ms.date: 03/30/2017
helpviewer_keywords:
- Span elements [WPF]
- bidirectional features [WPF]
ms.assetid: fd850e25-7dba-408c-b521-8873e51dc968
ms.openlocfilehash: 6cd16f4d5586dcee54152b430f14911f5a9c5682
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005131"
---
# <a name="bidirectional-features-in-wpf-overview"></a>WPF Genel Bakışında Çift Yönlü Özellikler

Diğer herhangi bir geliştirme platformunun aksine, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] çift yönlü içeriğin hızlı bir şekilde geliştirilmesini destekleyen birçok özelliğe sahiptir (örneğin, soldan sağa ve sağdan sola veriler aynı belgede bulunur). Aynı zamanda, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], Arapça ve Ibranice kullanıcılar gibi çift yönlü özellikler gerektiren kullanıcılar için mükemmel bir deneyim oluşturur.

Aşağıdaki bölümlerde çift yönlü içeriğin en iyi görüntüsüne nasıl ulaşılacağını gösteren örneklerle birlikte birçok çift yönlü özellikler açıklanmaktadır. Çoğu örnek XAML kullanır, ancak bu kavramları C# veya Microsoft Visual Basic koduna kolayca uygulayabilirsiniz.

<a name="FlowDirection"></a>

## <a name="flowdirection"></a>FlowDirection

@No__t-0 uygulamasında içerik akışı yönünü tanımlayan temel özellik <xref:System.Windows.FrameworkElement.FlowDirection%2A> ' dir. Bu özellik iki numaralandırma değerinden birine ayarlanabilir, <xref:System.Windows.FlowDirection.LeftToRight> veya <xref:System.Windows.FlowDirection.RightToLeft>. Özelliği, <xref:System.Windows.FrameworkElement> ' den kalıtımla alan tüm @no__t 0 öğeleri için kullanılabilir.

Aşağıdaki örneklerde <xref:System.Windows.Controls.TextBox> öğesinin akış yönü ayarlanır.

**Soldan sağa akış yönü**

[!code-xaml[LTRRTL#LTR](~/samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#ltr)]

**Sağdan sola akış yönü**

[!code-xaml[LTRRTL#RTL](~/samples/snippets/csharp/VS_Snippets_Wpf/LTRRTL/CS/Pane1.xaml#rtl)]

Aşağıdaki grafik, önceki kodun nasıl işlediğini gösterir.

![Farklı akış yönlerini gösteren grafik.](./media/bidirectional-features-in-wpf-overview/left-right-right-left.png)

@No__t-0 ağacı içindeki bir öğe, kapsayıcısından <xref:System.Windows.FrameworkElement.FlowDirection%2A> ' i miras alacak. Aşağıdaki örnekte <xref:System.Windows.Controls.TextBlock>, <xref:System.Windows.Window> ' de bulunan bir <xref:System.Windows.Controls.Grid> içindedir. @No__t-1 için <xref:System.Windows.FrameworkElement.FlowDirection%2A> ayarlanması, <xref:System.Windows.Controls.Grid> ve <xref:System.Windows.Controls.TextBlock> ' ü de ayarlamayı gerektirir.

Aşağıdaki örnek <xref:System.Windows.FrameworkElement.FlowDirection%2A> ayarını gösterir.

[!code-xaml[FlowDirection#FlowDirection](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDirection/CS/Window1.xaml#flowdirection)]

@No__t-0 ' en üst düzey bir <xref:System.Windows.FlowDirection.RightToLeft> @ no__t-2 ' dir. bu nedenle, içinde içerilen tüm öğeler aynı <xref:System.Windows.FrameworkElement.FlowDirection%2A> ' ü de de içerir. Bir öğenin belirtilen @no__t geçersiz kılması için-0, önceki örnekte <xref:System.Windows.FlowDirection.LeftToRight> ' ye yapılan ikinci <xref:System.Windows.Controls.TextBlock> gibi bir açık yön değişikliği eklemeli. @No__t-0 tanımlanmadığında, varsayılan <xref:System.Windows.FlowDirection.LeftToRight> geçerli olur.

Aşağıdaki grafikte, önceki örneğin çıktısı gösterilmektedir:

![Açık akış yönü değişikliğini gösteren grafik.](./media/bidirectional-features-in-wpf-overview/explicit-direction-change.png)

<a name="FlowDocument"></a>

## <a name="flowdocument"></a>FlowDocument

HTML, [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] ve Java gibi birçok geliştirme platformu çift yönlü içerik geliştirmeye yönelik özel destek sağlar. HTML gibi biçimlendirme dilleri içerik yazıcılarını, metni gerekli herhangi bir yöne (4,0 Örneğin, "RTL" veya "LTR" değeri olarak alan "dir") göstermek için gerekli işaretlemeleri sağlar. Bu etiket <xref:System.Windows.FrameworkElement.FlowDirection%2A> özelliğine benzerdir, ancak <xref:System.Windows.FrameworkElement.FlowDirection%2A> özelliği metin içeriğini düzene eklemek için daha gelişmiş bir şekilde çalışabilir ve metin dışındaki içerikler için kullanılabilir.

@No__t-0 ' da, bir <xref:System.Windows.Documents.FlowDocument>, metin, tablo, resim ve diğer öğelerin birleşimini barındırabileceğiniz çok yönlü bir [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] öğesidir. Aşağıdaki bölümlerdeki örnekler bu öğeyi kullanır.

@No__t-0 ' a metin ekleme, tek bir şekilde yapılabilir. Bunu yapmanın basit bir yolu, metin gibi içerikleri gruplamak için kullanılan blok düzeyinde bir öğe olan <xref:System.Windows.Documents.Paragraph> ' dır. Satır içi düzeyindeki öğelere metin eklemek için örnekler <xref:System.Windows.Documents.Span> ve <xref:System.Windows.Documents.Run> kullanır. <xref:System.Windows.Documents.Span>, diğer satır içi öğeleri gruplandırmak için kullanılan bir satır içi düzey akış içerik öğesidir, bir <xref:System.Windows.Documents.Run>, biçimlendirilmemiş bir metnin çalıştırılmasını amaçlanan bir satır içi düzey akış içerik öğesidir. @No__t-0, birden çok <xref:System.Windows.Documents.Run> öğesi içerebilir.

İlk belge örneği, çeşitli ağ paylaşma adlarına sahip bir belge içerir; Örneğin `\\server1\folder\file.ext`. Arapça veya Ingilizce bir belgede bu ağ bağlantısına sahip olmanız, her zaman aynı şekilde görünmesini ister. Aşağıdaki grafik, span öğesinin kullanımını gösterir ve bağlantıyı bir Arap <xref:System.Windows.FlowDirection.RightToLeft> belgesinde gösterir:

![Span öğesini kullanmayı gösteren grafik.](./media/bidirectional-features-in-wpf-overview/flow-direction-span-element.png "FlowDocument")

Metin <xref:System.Windows.FlowDirection.RightToLeft> olduğundan, "\\" gibi tüm özel karakterler metni sağdan sola sırada ayırır. Bu, bağlantının doğru sırada gösterilmeme sonucu olarak, bu nedenle sorunu çözmek için metnin, ayrı bir <xref:System.Windows.Documents.Run> akışı <xref:System.Windows.FlowDirection.LeftToRight> ' i korumak için katıştırılması gerekir. Her dil için ayrı bir @no__t olmak yerine, sorunu çözmenin daha iyi bir yolu, daha az sıklıkta kullanılan Ingilizce metni daha büyük bir Arapça <xref:System.Windows.Documents.Span> içine katıştırmaktır.

Aşağıdaki grafikte, bir span öğesinde gömülü Run öğesi kullanılarak gösterilmektedir:

![Span öğesine gömülü Run öğesini gösteren grafik.](./media/bidirectional-features-in-wpf-overview/embedded-span-element.png)

Aşağıdaki örnek, belgelerinde <xref:System.Windows.Documents.Run> ve <xref:System.Windows.Documents.Span> öğelerinin kullanımını gösterir.

[!code-xaml[RunSpan#RunSpan](~/samples/snippets/csharp/VS_Snippets_Wpf/RunSpan/CS/Window1.xaml#runspan)]

<a name="SpanElements"></a>

## <a name="span-elements"></a>Span öğeleri

@No__t-0 öğesi, farklı akış yönlerine sahip metinler arasında bir sınır ayırıcısı olarak çalışarak.  Aynı akış yönüne sahip <xref:System.Windows.Documents.Span> öğeleri, <xref:System.Windows.Documents.Span> öğelerinin kapsayıcının <xref:System.Windows.FlowDirection> ' ye sıralı olduğu anlamına gelen farklı çift yönlü kapsamlara sahip olduğu kabul edilir, ancak yalnızca <xref:System.Windows.Documents.Span> öğesi içindeki içerikler @no__t @no__ t-5.

Aşağıdaki grafikte, birkaç <xref:System.Windows.Controls.TextBlock> öğesinin akış yönü gösterilmektedir.

![Farklı akış yönlerine sahip metin bloklarını gösteren grafik.](./media/bidirectional-features-in-wpf-overview/flow-direction-text-blocks.png)

Aşağıdaki örnek, önceki grafikte gösterilen sonuçları oluşturmak için <xref:System.Windows.Documents.Span> ve <xref:System.Windows.Documents.Run> öğelerinin nasıl kullanılacağını gösterir.

[!code-xaml[Span#Span](~/samples/snippets/csharp/VS_Snippets_Wpf/Span/CS/Window1.xaml#span)]

Örnekteki <xref:System.Windows.Controls.TextBlock> öğelerinde, <xref:System.Windows.Documents.Span> öğeleri üst öğelerinin <xref:System.Windows.FlowDirection> ' ına göre düzenlenir, ancak her @no__t 3 öğesi içindeki metin kendi <xref:System.Windows.FlowDirection> ' e göre akar. Bu, Latin ve Arapça ya da başka bir dil için geçerlidir.

### <a name="adding-xmllang"></a>XML ekleme: lang

Aşağıdaki grafikte, `"200.0+21.4=221.4"` gibi sayılar ve aritmetik ifadeler kullanan başka bir örnek gösterilmektedir. Yalnızca <xref:System.Windows.FlowDirection> ' ın ayarlanmış olduğuna dikkat edin.

![Yalnızca FlowDirection kullanarak sayıları görüntüleyen grafik.](./media/bidirectional-features-in-wpf-overview/numbers-flow-right-left.png)

@No__t-0 doğru olsa bile, bu uygulamanın kullanıcıları çıktı tarafından geri alınacaktır, ancak Arapça sayıların şekillendirilmiş olması gerekir.

XAML öğeleri, her bir öğenin dilini tanımlayan bir [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] özniteliği (`xml:lang`) içerebilir. XAML ayrıca ağaç içindeki üst öğelere uygulanan @no__t 1 değerlerinin alt öğeler tarafından kullanıldığı [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] Dil ilkesini destekler. Önceki örnekte, <xref:System.Windows.Documents.Run> öğesi veya en üst düzey öğelerinden herhangi biri için bir dil tanımlanmadığı için, XAML için `en-US` olan varsayılan `xml:lang` kullanılmıştır. @No__t-0 ' ın iç sayı şekillendirme algoritması, ilgili dildeki sayıları seçer; Bu durumda Ingilizce. Arapça sayıların doğru şekilde işlemesini sağlamak için-0 ' ın ayarlanması gerekir @no__t.

Aşağıdaki grafikte `xml:lang` eklenen örnek gösterilmektedir.

![Sağdan sola akan Arapça sayıları gösteren grafik.](./media/bidirectional-features-in-wpf-overview/arabic-numbers-flow-right-left.png)

Aşağıdaki örnek, `xml:lang` ' i uygulamaya ekler.

[!code-xaml[LangAttribute#LangAttribute](~/samples/snippets/csharp/VS_Snippets_Wpf/LangAttribute/CS/Window1.xaml#langattribute)]

Birçok dilin hedeflenen bölgeye göre farklı `xml:lang` değerleri olduğunu unutmayın, örneğin, `"ar-SA"` ve `"ar-EG"` Arapça iki çeşitlemeyi temsil eder. Önceki örneklerde `xml:lang` ve <xref:System.Windows.FlowDirection> değerlerinin her ikisini de tanımlamanız gerektiğini gösterir.

<a name="FlowDirectionNontext"></a>

## <a name="flowdirection-with-non-text-elements"></a>Metin olmayan öğelerle FlowDirection

<xref:System.Windows.FlowDirection>, metnin metinsel bir öğe içinde nasıl akacağını, aynı zamanda neredeyse her bir [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] öğesinin akış yönünü de tanımlar. Aşağıdaki grafikte, soldan sağa degradeyle arka planını çizmek için yatay <xref:System.Windows.Media.LinearGradientBrush> kullanan <xref:System.Windows.Controls.ToolBar> gösterilmektedir.

![Soldan sağa degradeyle bir araç çubuğu gösteren grafik.](./media/bidirectional-features-in-wpf-overview/toolbar-left-right-gradient.png)

@No__t-0 ' ı <xref:System.Windows.FlowDirection.RightToLeft> olarak ayarladıktan sonra, yalnızca <xref:System.Windows.Controls.ToolBar> düğmeleri sağdan sola düzenlenirler, ancak <xref:System.Windows.Media.LinearGradientBrush> de uzaklıklarını sağdan sola doğru bir şekilde yeniden hizalar.

Aşağıdaki grafikte <xref:System.Windows.Media.LinearGradientBrush> ' ın yeniden hizalaması gösterilmektedir.

![Sağdan sola degradeyle bir araç çubuğu gösteren grafik.](./media/bidirectional-features-in-wpf-overview/toolbar-right-left-gradient.png)

Aşağıdaki örnek bir @no__t çizer-0 @ no__t-1. (Sola doğru çizmek için, <xref:System.Windows.Controls.ToolBar> ' de <xref:System.Windows.FlowDirection> özniteliğini kaldırın.

[!code-xaml[Gradient#Gradient](~/samples/snippets/csharp/VS_Snippets_Wpf/Gradient/CS/Window1.xaml#gradient)]

<a name="FlowDirectionExceptions"></a>

### <a name="flowdirection-exceptions"></a>FlowDirection özel durumları

@No__t-0 ' ın beklendiği gibi davranmayan birkaç durum vardır. Bu bölümde bu özel durumların ikisi ele alınmaktadır.

**Görüntü**

@No__t-0 bir görüntüyü görüntüleyen bir denetimi temsil eder. XAML 'de, görüntülenecek <xref:System.Windows.Controls.Image> ' nin @no__t tanımlayan bir <xref:System.Windows.Controls.Image.Source%2A> özelliği ile birlikte kullanılabilir.

Diğer [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] öğelerinden farklı olarak, bir <xref:System.Windows.Controls.Image> kapsayıcının <xref:System.Windows.FlowDirection> ' i döndürmez. Ancak, <xref:System.Windows.FlowDirection> açıkça <xref:System.Windows.FlowDirection.RightToLeft> olarak ayarlandıysa, yatay olarak çevrilmiş bir <xref:System.Windows.Controls.Image> görüntülenir. Bu, çift yönlü içerik geliştiricileri için kullanışlı bir özellik olarak uygulanır; Bazı durumlarda görüntüyü yatay olarak çevirme istenen etkiyi üretir.

Aşağıdaki grafikte çevrilmiş <xref:System.Windows.Controls.Image> gösterilmektedir.

![Çevrilmiş bir görüntüyü gösteren grafik.](./media/bidirectional-features-in-wpf-overview/flipped-image-example.png)

Aşağıdaki örnek, <xref:System.Windows.Controls.Image> ' i içeren <xref:System.Windows.Controls.StackPanel> ' den <xref:System.Windows.FlowDirection> ' i kalýtýmla gerçekleştiremediği gösterilmektedir.

> [!NOTE]
> C:\ uygulamanızda **ms_logo. jpg** adlı bir dosyanız olmalıdır Bu örneği çalıştırmak için sürücü.

[!code-xaml[Image#Image](~/samples/snippets/csharp/VS_Snippets_Wpf/Image/CS/Window1.xaml#image)]

> [!NOTE]
> İndirme dosyalarında yer alan bir **ms_logo. jpg** dosyasıdır. Kod. jpg dosyasının projenizin içinde, ancak C:\ ' da bir yerde olduğunu varsayar. sürücü. . Jpg dosyasını proje dosyalarından C:\ uygulamanıza kopyalamanız gerekir projenin içindeki dosyayı aramak için kodu sürücü olarak değiştirin veya değiştirin. Bu değişikliği yapmak için `Source="file://c:/ms_logo.jpg"`-1 `Source="ms_logo.jpg"`.

**Yollar**

@No__t-0 ' a ek olarak, başka bir ilginç öğe <xref:System.Windows.Shapes.Path> ' dir. Yol, bir dizi bağlantılı çizgi ve eğri çizebileceğiniz bir nesnedir. @No__t-0 ile benzer bir şekilde davranır <xref:System.Windows.FlowDirection>; Örneğin <xref:System.Windows.FlowDirection.RightToLeft> @ no__t-3, <xref:System.Windows.FlowDirection.LeftToRight> 1 ' in yatay bir yansıtmasıdır. Ancak, bir <xref:System.Windows.Controls.Image> ' dan farklı olarak, <xref:System.Windows.Shapes.Path> <xref:System.Windows.FlowDirection> ' i kapsayımla devralır ve bunun açıkça belirtilmesi gerekmez.

Aşağıdaki örnek 3 satır kullanarak basit bir ok çizer. İlk ok, başlangıç ve bitiş noktalarının sağ taraftaki bir köke göre ölçülmesi için <xref:System.Windows.Controls.StackPanel> ' den <xref:System.Windows.FlowDirection.RightToLeft> akış yönünü devralır. Açık bir @no__t olan ikinci ok-0 @ no__t-1 ' i sağ tarafta da başlatılır. Ancak, üçüncü ok sol tarafta başlangıç köküne sahiptir. Çizim hakkında daha fazla bilgi için bkz. <xref:System.Windows.Media.LineGeometry> ve <xref:System.Windows.Media.GeometryGroup>.

[!code-xaml[Paths#Paths](~/samples/snippets/csharp/VS_Snippets_Wpf/Paths/CS/Window1.xaml#paths)]

Aşağıdaki grafikte, `Path` öğesi kullanılarak çizilen oklarla birlikte önceki örneğin çıktısı gösterilmektedir:

![Yol öğesi kullanılarak çizilen okları gösteren grafik.](./media/bidirectional-features-in-wpf-overview/arrows-drawn-path-element.png)

@No__t-0 ve <xref:System.Windows.Shapes.Path>, [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] ' nin <xref:System.Windows.FlowDirection> ' ü nasıl kullandığını gösteren iki örnektir. @No__t-0 öğelerinin bir kapsayıcı içinde belirli bir yönde yerleştirme sonrasında, <xref:System.Windows.FlowDirection>, bir yüzey üzerinde mürekkep işleyen <xref:System.Windows.Media.LinearGradientBrush>, <xref:System.Windows.Media.RadialGradientBrush> gibi <xref:System.Windows.Controls.InkPresenter> gibi öğeler ile kullanılabilir. İçeriğiniz için soldan sağa davranış sağlayan sağdan sola davranış gerektiğinde veya tam tersi durumda, [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] bu yeteneği sağlar.

<a name="NumberSubstitution"></a>

## <a name="number-substitution"></a>Sayı değiştirme

Tarihsel olarak, Windows, farklı kültürel şekillerin farklı yerel ayarlar arasında birleşirken aynı basamakların gösterimine izin vererek, sayı değişimini destekliyordu, örneğin sayılar bilinen onaltılık değerler, 0x40, 0x41, ancak seçilen dile göre gösteriliyor.

Bu, uygulamaların bir dilden diğerine dönüştürülmesi gerekmeden sayısal değerleri işlemesini izin bıraktı. Örneğin, bir Kullanıcı yerelleştirilmiş bir Arapça Windows 'ta [!INCLUDE[TLA#tla_xl](../../../../includes/tlasharptla-xl-md.md)] elektronik tablosu açabilir ve Arapça şeklinde rakamları görebilir, ancak bunu Avrupa 'da açabilir Windows sürümü ve aynı sayıların Avrupa gösterimine bakın. Bu Ayrıca, genellikle aynı belgedeki sayıları karşılamadığı için virgül ayırıcıları ve yüzde simgesi gibi diğer semboller için de gereklidir.

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] aynı gelenek devam eder ve bu özellik için, değiştirme ne zaman ve nasıl kullanıldığı konusunda daha fazla kullanıcı denetimine izin veren daha fazla destek ekler. Bu özellik herhangi bir dil için tasarlanırken, özellikle bir uygulamanın üzerinde çalışacağı çeşitli kültürler nedeniyle, belirli bir dile ait basamakların şekillendirmesinde genellikle uygulama geliştiricileri için bir zorluk olduğu çift yönlü içerik için yararlıdır.

# Değiştirme 'nin [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] ' da nasıl çalıştığını denetleyen Core özelliği <xref:System.Windows.Media.NumberSubstitution.Substitution%2A> bağımlılık özelliğidir. @No__t-0 sınıfı, metindeki sayıların nasıl görüntüleneceğini belirtir. Davranışını tanımlayan üç ortak özelliği vardır. Aşağıda her bir özellik özeti verilmiştir:

**Külsal kaynak:**

Bu özellik, sayıların kültürünün nasıl belirlendiğini belirtir. Üç @no__t 0 numaralandırma değerinden birini alır.

- Override: Number kültürü <xref:System.Windows.Media.NumberSubstitution.CultureOverride%2A> özelliğinden oluşur.

- Metin: sayı kültürü, metin çalıştırmasının kültürüdür. Biçimlendirme bölümünde bu `xml:lang` veya diğer adı `Language` özelliği (<xref:System.Windows.FrameworkElement.Language%2A> veya <xref:System.Windows.FrameworkContentElement.Language%2A>) olur. Ayrıca, <xref:System.Windows.FrameworkContentElement> ' dan türetilen sınıflar için varsayılandır. Bu tür sınıflar <xref:System.Windows.Documents.Paragraph?displayProperty=nameWithType>, <xref:System.Windows.Documents.Table?displayProperty=nameWithType>, <xref:System.Windows.Documents.TableCell?displayProperty=nameWithType> vb. içerir.

- Kullanıcı: sayı kültürü geçerli iş parçacığının kültürüdür. Bu özellik, <xref:System.Windows.Controls.Page>, <xref:System.Windows.Window> ve <xref:System.Windows.Controls.TextBlock> gibi <xref:System.Windows.FrameworkElement> ' ın tüm alt sınıfları için varsayılandır.

**CultureOverride**:

@No__t-0 özelliği, yalnızca <xref:System.Windows.Media.NumberSubstitution.CultureSource%2A> özelliği <xref:System.Windows.Media.NumberCultureSource.Override> olarak ayarlandıysa ve aksi durumda yoksayılırsa kullanılır. Kültür sayısını belirtir. @No__t-0 değeri, varsayılan değer en-US olarak yorumlanır.

**Değiştirme**:

Bu özellik, gerçekleştirilecek sayı değiştirme türünü belirtir. Aşağıdaki <xref:System.Windows.Media.NumberSubstitutionMethod> sabit listesi değerlerinden birini alır:

- <xref:System.Windows.Media.NumberSubstitutionMethod.AsCulture>: değiştirme yöntemi, sayı kültürünün <xref:System.Globalization.NumberFormatInfo.DigitSubstitution%2A?displayProperty=nameWithType> özelliğine göre belirlenir. Bu varsayılandır.

- <xref:System.Windows.Media.NumberSubstitutionMethod.Context>: sayı kültürü bir Arap veya Farsça kültürü ise, basamakların içeriğe göre olduğunu belirtir.

- <xref:System.Windows.Media.NumberSubstitutionMethod.European>: sayılar her zaman Avrupa basamağı olarak işlenir.

- <xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational>: sayılar, kültürün <xref:System.Globalization.CultureInfo.NumberFormat%2A> ' i tarafından belirtildiği gibi, sayı kültürü için ulusal basamaklar kullanılarak işlenir.

- <xref:System.Windows.Media.NumberSubstitutionMethod.Traditional>: sayılar, sayı kültürü için geleneksel basamaklar kullanılarak işlenir. Çoğu kültürde, bu <xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational> ' dır. Ancak, <xref:System.Windows.Media.NumberSubstitutionMethod.NativeNational> bazı Arap kültürleri için Latin rakamlarına neden olur, ancak bu değer tüm Arap kültürleri için Arapça basamağa neden olur.

Bu değerler çift yönlü içerik geliştiricisi için ne anlama geliyor? Çoğu durumda, geliştiricinin yalnızca <xref:System.Windows.FlowDirection> ve her metinsel [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] öğesinin dilini tanımlamasına ihtiyacı vardır, örneğin, `Language="ar-SA"` ve <xref:System.Windows.Media.NumberSubstitution> mantığı, sayıları doğru [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] ' e göre görüntüleme konusunda işlem gerçekleştirir. Aşağıdaki örnek, Windows 'un Arapça bir sürümünde çalışan [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] uygulamasında Arapça ve Ingilizce sayıların kullanımını gösterir.

[!code-xaml[Numbers#Numbers](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers/CS/Window1.xaml#numbers)]

Aşağıdaki grafikte, Arapça ve Ingilizce sayılarla Windows 'un Arapça bir sürümünde çalıştırıyorsanız önceki örneğin çıktısı gösterilmektedir:

![Arapça ve Ingilizce sayıları gösteren grafik.](./media/bidirectional-features-in-wpf-overview/arabic-english-numbers.png)

@No__t-0, bu durumda, <xref:System.Windows.FlowDirection> ' i <xref:System.Windows.FlowDirection.LeftToRight> ' ye ayarlandığında, bu örnekte önemlidir. Aşağıdaki bölümlerde, belgenizin tamamında nasıl Birleşik bir basamak görüntüleneceği ele alınmaktadır. Bu örnek Arapça Windows üzerinde çalışmıyorsa, tüm basamaklar Avrupa rakamları olarak görüntülenir.

**Değiştirme kurallarını tanımlama**

Gerçek bir uygulamada dili programlı olarak ayarlamanız gerekebilir. Örneğin, `xml:lang` özniteliğini sistemin [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] ' i tarafından kullanılan ile aynı olacak şekilde ayarlamak ya da uygulamanın durumuna bağlı olarak dili değiştirmek isteyebilirsiniz.

Uygulamanın durumuna göre değişiklik yapmak istiyorsanız, [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] tarafından sunulan diğer özelliklerden yararlanabilirsiniz.

İlk olarak, uygulama bileşeninin `NumberSubstitution.CultureSource="Text"` ' ı ayarlayın. Bu ayarın kullanılması, ayarların <xref:System.Windows.Controls.TextBlock> gibi "user" olan metin öğeleri için [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] ' dan gelmediğinden emin olur.

Örneğin:

```xaml
<TextBlock
   Name="text1" NumberSubstitution.CultureSource="Text">
   1234+5679=6913
</TextBlock>
```

Karşılık gelen C# kodda `Language` özelliğini, örneğin, `"ar-SA"` olarak ayarlayın.

```csharp
text1.Language = System.Windows.Markup.XmlLanguage.GetLanguage("ar-SA");
```

@No__t-0 özelliğini geçerli kullanıcının kullanıcı arabirimi diline ayarlamanız gerekirse aşağıdaki kodu kullanın.

```csharp
text1.Language = System.Windows.Markup.XmlLanguage.GetLanguage(System.Globalization.CultureInfo.CurrentUICulture.IetfLanguageTag);
```

<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>, geçerli iş parçacığı tarafından çalışma zamanında kullanılan geçerli kültürü temsil eder.

Son XAML örneğinizi aşağıdaki örneğe benzer olmalıdır.

[!code-xaml[Numbers2#Numbers2](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers2/CS/Window1.xaml#numbers2)]

Son C# örneğinizi aşağıdakine benzer olmalıdır.

[!code-csharp[NumbersCSharp#NumbersCSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/NumbersCSharp/CSharp/Window1.xaml.cs#numberscsharp)]

Aşağıdaki grafik, pencerenin programlama dili için nasıl göründüğünü gösterir, Arapça sayıları görüntüler:

![Arapça sayıları görüntüleyen grafik.](./media/bidirectional-features-in-wpf-overview/displays-arabic-numbers.png)

**Değiştirme özelliğini kullanma**

@No__t-0 ' da bulunan sayı değiştirme yöntemi, hem metin öğesinin diline hem de <xref:System.Windows.FlowDirection> ' ne bağlıdır. @No__t-0 ' ı sağdan sola, Avrupa rakamları işlenir. Ancak, daha önce Arapça metindiyse veya dili "ar" olarak ve <xref:System.Windows.FlowDirection> ' ı <xref:System.Windows.FlowDirection.RightToLeft> ise, bunun yerine Arapça rakamlar işlenir.

Ancak bazı durumlarda, birleştirilmiş bir uygulama oluşturmak isteyebilirsiniz, örneğin, tüm kullanıcılar için Avrupa rakamları. Ya da <xref:System.Windows.Documents.Table> hücrelerinde belirli bir <xref:System.Windows.Style> olan Arapça rakamlar. Bunu yapmanın kolay bir yolu <xref:System.Windows.Media.NumberSubstitution.Substitution%2A> özelliğini kullanmaktır.

Aşağıdaki örnekte, ilk <xref:System.Windows.Controls.TextBlock> ' ın <xref:System.Windows.Media.NumberSubstitution.Substitution%2A> özelliği ayarlanmamış, bu nedenle algoritma, beklenen Arapça rakamları görüntüler. Ancak ikinci <xref:System.Windows.Controls.TextBlock> ' da değiştirme, Arapça sayılar için varsayılan değişikliği geçersiz kılan Avrupa olarak ayarlanır ve Avrupa rakamları görüntülenir.

[!code-xaml[Numbers3#Numbers3](~/samples/snippets/csharp/VS_Snippets_Wpf/Numbers3/CS/Window1.xaml#numbers3)]
