---
title: WPF'de Tipografi
ms.date: 03/30/2017
helpviewer_keywords:
- typography [WPF], about typography
ms.assetid: 06cbf17b-6eff-4fe5-949d-2dd533e4e1f4
ms.openlocfilehash: 11087ed4da23d73fc8edc36680dd1b3587c011ce
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004919"
---
# <a name="typography-in-wpf"></a>WPF'de Tipografi
Bu konu, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ' ın önemli tipografik özelliklerini tanıtır. Bu özellikler, metin işleme, OpenType tipografi desteği, gelişmiş uluslararası metin, gelişmiş yazı tipi desteği ve yeni metin uygulama programlama arabirimleri (API 'Ler) için geliştirilmiş kalite ve performans içerir.  
  
<a name="Improved_Quality_and_Performance_of_Text"></a>   
## <a name="improved-quality-and-performance-of-text"></a>Metnin geliştirilmiş kalitesi ve performansı  
 @No__t-0 ' daki metin, metnin açıklık ve okunabilirliğini artıran Microsoft ClearType kullanılarak işlenir. ClearType, dizüstü ekranları, Pocket PC ekranları ve düz panel izleyicileri gibi mevcut LCD 'lerde (sıvı kristal ekranlar) metinlerin okunabilirliğini artıran Microsoft tarafından geliştirilen bir yazılım teknolojisidir. ClearType, bir pikselin kesirli bölümünde karakterler hizalanarak metnin gerçek şeklinin daha büyük bir uygunluğa eşit bir şekilde görüntülenmesine olanak sağlayan alt piksel işleme kullanır. Ek çözüm, metin görüntüleme içindeki küçük ayrıntıların keskinliğini artırarak uzun süreleri okumayı çok daha kolay hale getirir. @No__t-0 ' da ClearType 'ın başka bir geliştirmesi, metin karakterlerinin yüzeysel ve botları gibi, y yönlü kenar yumuşatmadır. ClearType özellikleri hakkında daha fazla bilgi için bkz. [ClearType Genel Bakış](cleartype-overview.md).  
  
 ![ClearType y yönü düzgünleştirmesini içeren metin](./media/typography-in-wpf/text-y-direction-antialiasing.gif)  
ClearType y yönünde düzgünleştirme içeren metin  
  
 Tüm metin işleme işlem hattı @no__t, makinenizde gereken en düşük donanım düzeyini karşıladığı için-0 ' da donanım hızlandırılır. Donanım kullanılarak gerçekleştirilemediği işleme, yazılım işlemeye geri döner. Donanım hızlandırma, metin işleme işlem hattının tüm aşamalarını etkiler. tek glifleri depolamadan, glifleri karakter çalıştırmalarıyla birleştirme, etkileri uygulama, son görünen çıktıya ClearType karıştırma algoritmasını uygulama. Donanım hızlandırma hakkında daha fazla bilgi için bkz. [grafik Işleme katmanları](graphics-rendering-tiers.md).  
  
 ![Metin işleme işlem hattının diyagramı](./media/typography-in-wpf/text-rendering-pipeline.png)  
  
 Buna ek olarak, karakter veya karakter olarak hareketli metin, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] tarafından etkinleştirilen grafik donanımı yeteneğinin tam olarak yararlanır. Bu, düz metin animasyonuna neden olur.  
  
<a name="Rich_Typography"></a>   
## <a name="rich-typography"></a>Zengin tipografi  
 OpenType yazı tipi biçimi, TrueType® yazı tipi biçiminin bir uzantısıdır. OpenType yazı tipi biçimi Microsoft ve Adobe tarafından ortaklaşa ortaklaşa geliştirilmiştir ve zengin bir gelişmiş tipografik özellikler sunar. @No__t-0 nesnesi, OpenType yazı tiplerinin stil alternatifleri ve süslemeler gibi gelişmiş özelliklerinin çoğunu gösterir. Windows SDK, Pericles ve Pescadero fontları gibi zengin özelliklerle tasarlanan örnek bir OpenType yazı tipi kümesi sağlar. Daha fazla bilgi için bkz. [örnek OpenType yazı tipi paketi](sample-opentype-font-pack.md).  
  
 Pericles OpenType yazı tipi, standart glif kümesine stil alternatifleri sağlayan ek glifler içerir. Aşağıdaki metin, biçimsel alternatif glifleri görüntüler.  
  
 (./media/typography-in-wpf/opentype-stylistic-alternate-glyphs.gif "OpenType biçimsel alternatif glifler kullanılarak") ![OpenType biçimsel diğer glif metinlerini kullanan metin]  
  
 Süslemeler, kaligrafi ile sık kullanılan süslemeler ile ilişkili olan dekoratif karakterlerdir. Aşağıdaki metin Pescadero yazı tipi için standart ve dalgalı glifleri görüntüler.  
  
 (./media/typography-in-wpf/opentype-standard-swash-glyphs.gif "OpenType standart ve dalgalı Glifler kullanılarak") ![OpenType standart ve dalgalı karakterler metnini kullanan metin]  
  
 OpenType özellikleri hakkında daha fazla bilgi için bkz. [OpenType yazı tipi özellikleri](opentype-font-features.md).  
  
<a name="Enhanced_International_Text_Support"></a>   
## <a name="enhanced-international-text-support"></a>Gelişmiş uluslararası metin desteği  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], aşağıdaki özellikleri sağlayarak gelişmiş uluslararası metin desteği sağlar:  
  
- Uyarlamalı ölçüm kullanarak tüm yazma sistemlerinde otomatik satır aralığı.  
  
- Uluslararası metin için geniş destek. Daha fazla bilgi için bkz. [WPF Için Genelleştirme](globalization-for-wpf.md).  
  
- Dil temelli satır sonu, heceleme ve gerekçe.  
  
<a name="Enhanced_Font_Support"></a>   
## <a name="enhanced-font-support"></a>Gelişmiş yazı tipi desteği  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], aşağıdaki özellikleri sağlayarak gelişmiş yazı tipi desteği sağlar:  
  
- Tüm metinler için Unicode. Yazı tipi davranışı ve seçimi artık karakter kümesi veya kod sayfası gerektirmez.  
  
- Sistem yerel ayarı gibi genel ayarlardan bağımsız yazı tipi davranışı.  
  
- @No__t 3 tanımlamak için <xref:System.Windows.FontWeight>, <xref:System.Windows.FontStretch> ve <xref:System.Windows.FontStyle> türlerini ayırın. Bu, [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] programından daha fazla esneklik sağlar, bu, italik ve kalın olan Boole birleşimlerinin bir yazı tipi ailesini tanımlamak için kullanılır.  
  
- Yazma yönü (yatay veya dikey), yazı tipi adından bağımsız olarak işlenir.  
  
- Bileşik yazı tipi teknolojisini kullanarak taşınabilir [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] dosyasına yazı tipi bağlama ve yazı tipi düşürme. Bileşik yazı tipleri, tam aralıklı çok dilli yazı tiplerinin oluşturulmasını sağlar. Bileşik yazı tipleri ayrıca eksik karakterlerin görüntülenmesini önleyen bir mekanizma sağlar. Daha fazla bilgi için <xref:System.Windows.Media.FontFamily> sınıfındaki açıklamalara bakın.  
  
- Tek dildeki bir yazı tipi grubu kullanılarak bileşik yazı tiplerinden oluşturulan uluslararası yazı tipleri. Bu, birden çok dil için yazı tipi geliştirirken kaynak maliyetlerine kaydedilir.  
  
- Belge taşınabilirliği sağlayan bileşik yazı tipleri bir belgeye katıştırılır. Daha fazla bilgi için <xref:System.Windows.Media.FontFamily> sınıfındaki açıklamalara bakın.  
  
<a name="New_Text_APIs"></a>   
## <a name="new-text-application-programming-interfaces-apis"></a>Yeni metin uygulama programlama arabirimleri (API 'Ler)  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], geliştiricilerin uygulamalarına metin eklerken kullanacağı birkaç metin API 'si sağlar. Bu API 'Ler üç kategoride gruplandırılır:  
  
- **Düzen ve Kullanıcı arabirimi**. Grafik Kullanıcı arabirimi (GUI) için ortak metin denetimleri.  
  
- **Hafif metin çizme**. Doğrudan nesnelere metin çizmenizi sağlar.  
  
- **Gelişmiş metin biçimlendirme**. Özel bir metin altyapısı uygulamanıza olanak tanır.  
  
### <a name="layout-and-user-interface"></a>Düzen ve Kullanıcı arabirimi  
 En yüksek işlevsellik düzeyinde, metin API 'Leri, <xref:System.Windows.Controls.Label>, <xref:System.Windows.Controls.TextBlock> ve <xref:System.Windows.Controls.TextBox> gibi ortak [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] denetimleri sağlar. Bu denetimler, bir uygulama içinde temel [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] öğeleri sağlar ve metin sunmak ve bunlarla etkileşim kurmak için kolay bir yol sunar. @No__t-0 ve <xref:System.Windows.Controls.PasswordBox> gibi denetimler daha gelişmiş veya özel metin işleme sağlar. Ve <xref:System.Windows.Documents.TextRange>, <xref:System.Windows.Documents.TextSelection> ve <xref:System.Windows.Documents.TextPointer> gibi sınıflar yararlı metin işlemesini etkinleştirir. Bu [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] denetimleri, metni oluşturmak için kullanılan yazı tipini denetlemenizi sağlayan <xref:System.Windows.Controls.Control.FontFamily%2A>, <xref:System.Windows.Controls.Control.FontSize%2A> ve <xref:System.Windows.Controls.Control.FontStyle%2A> gibi özellikler sağlar.  
  
#### <a name="using-bitmap-effects-transforms-and-text-effects"></a>Bit eşlem efektleri, dönüşümler ve metin efektlerini kullanma  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] bit eşlem efektleri, dönüşümler ve metin etkileri gibi özellikleri kullanarak metnin görsel açıdan ilgi çekici kullanımlarını oluşturmanızı sağlar. Aşağıdaki örnek, metin için uygulanan tipik bir gölge etkisi türünü gösterir.  
  
 ![Soflük &#61; 0,25 ile metin gölgesi](./media/typography-in-wpf/drop-shadow-text-effect.jpg) 
  
 Aşağıdaki örnekte, bir gölge efekti ve metne uygulanan gürültü gösterilmektedir.  
  
 ![Gürültü içeren metin gölgesi](./media/typography-in-wpf/drop-shadow-noise-text.jpg) 
  
 Aşağıdaki örnek, metne uygulanan bir dış ışıma efektini gösterir.  
  
 ![OuterGlowBitmapEffect kullanarak metin gölgesi](./media/typography-in-wpf/text-shadow-glow-effect.jpg)
  
 Aşağıdaki örnek, metne uygulanan bir bulanıklaştırma efektini gösterir.  
  
 ![Bir BlurBitmapEffect kullanarak metin gölgesi](./media/typography-in-wpf/text-shadow-blur-effect.jpg)  

 Aşağıdaki örnek, x ekseni ve y ekseni üzerinde% 150 ile ölçeklenmiş üçüncü metin satırındaki 150 metnin ikinci satırını gösterir.  
  
 ![ScaleTransform kullanılarak Ölçeklendirilmiş metin](./media/typography-in-wpf/scaled-text-scaletransform.jpg) 
  
 Aşağıdaki örnek, x ekseni üzerinde eğilmiş metni gösterir.  
  
 ![SkewTransform kullanarak eğilmiş metin](./media/typography-in-wpf/skewed-transformed-text.jpg)
  
 @No__t-0 nesnesi, metni bir metin dizesinde bir veya daha fazla karakter grubu olarak değerlendirme olanağı sağlayan bir yardımcı nesnedir. Aşağıdaki örnek, döndürülmekte olan ayrı bir karakteri gösterir. Her karakter, 1 saniyelik aralıklarla bağımsız olarak döndürülür.  
  
 ![Metin döndürme metin efektinin ekran görüntüsü](./media/typography-in-wpf/rotating-text-effect.jpg) 
  
#### <a name="using-flow-documents"></a>Flow belgelerini kullanma  
 Ortak [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] denetimlerine ek olarak, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], metin sunumu için bir düzen denetimi (<xref:System.Windows.Documents.FlowDocument> öğesi) sağlar. @No__t-1 öğesiyle birlikte <xref:System.Windows.Documents.FlowDocument> öğesi, farklı düzen gereksinimlerine sahip büyük miktarda metin için bir denetim sağlar. Düzen denetimleri <xref:System.Windows.Documents.Typography> nesnesi ve diğer [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] denetimlerinin yazı tipiyle ilişkili özellikleri aracılığıyla Gelişmiş tipografi erişimi sağlar.  
  
 Aşağıdaki örnek, arama, gezinme, sayfalandırma ve içerik ölçekleme desteği sağlayan <xref:System.Windows.Controls.FlowDocumentReader> ' da barındırılan metin içeriğini gösterir.  
  
 ![OpenType yazı tiplerini gösteren ekran görüntüsü.](./media/typography-in-wpf/typography-text-flowdocumentreader.png)
  
 Daha fazla bilgi için bkz. [WPF Içindeki belgeler](documents-in-wpf.md).  
  
### <a name="lightweight-text-drawing"></a>Hafif metin çizme  
 @No__t-2 nesnesinin <xref:System.Windows.Media.DrawingContext.DrawText%2A> yöntemini kullanarak doğrudan [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nesnelerine metin çizebilirsiniz. Bu yöntemi kullanmak için, <xref:System.Windows.Media.FormattedText> nesnesi oluşturursunuz. Bu nesne, metin içindeki her karakterin tek tek biçimlendirilebileceği çok satırlı metin çizmenizi sağlar. @No__t-0 nesnesinin işlevselliği, Windows API 'sindeki DrawText bayraklarının işlevlerinin çoğunu içerir. Ayrıca, <xref:System.Windows.Media.FormattedText> nesnesi, metin sınırlarını aştığında üç nokta da gösterildiği üç nokta desteği gibi işlevler içerir. Aşağıdaki örnek, ikinci ve üçüncü sözcüklere doğrusal bir gradyan dahil olmak üzere birkaç biçim uygulanmış olan metni gösterir.  
  
 ![FormattedText nesnesi kullanılarak görünen metin](./media/typography-in-wpf/text-formatted-linear-gradient.jpg) 
  
 Biçimli metni <xref:System.Windows.Media.Geometry> nesnelerine dönüştürebilirsiniz, böylece görsel açıdan ilgi çekici metin türlerini oluşturabilirsiniz. Örneğin, bir metin dizesinin ana hattını temel alan <xref:System.Windows.Media.Geometry> nesnesi oluşturabilirsiniz.  
  
 ![Doğrusal gradyan fırçası kullanan metin ana hattı](./media/typography-in-wpf/text-outline-linear-gradient.jpg)  
  
 Aşağıdaki örneklerde, dönüştürülmüş metnin vuruş, dolgusu ve vurgulanmasını değiştirerek ilginç görsel etkiler oluşturmanın birkaç yolu gösterilmektedir.  
  
 ![Fill ve Stroke için farklı renkler içeren metin](./media/typography-in-wpf/fill-stroke-text-effect.jpg)  
  
 ![Görüntüye resim fırçası uygulanmış metin](./media/typography-in-wpf/image-brush-application.jpg)
  
 ![Kontura ve vurgulamaya uygulanan resim fırçasının bulunduğu metin](./media/typography-in-wpf/image-brush-text-application.jpg)
  
 @No__t-0 nesnesi hakkında daha fazla bilgi için bkz. [biçimli metin çizme](drawing-formatted-text.md).  
  
### <a name="advanced-text-formatting"></a>Gelişmiş Metin Biçimlendirme  
 Metin API 'Lerinin en gelişmiş düzeyinde [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], <xref:System.Windows.Media.TextFormatting.TextFormatter> nesnesini ve <xref:System.Windows.Media.TextFormatting> ad alanındaki diğer türleri kullanarak özel metin düzeni oluşturma olanağı sağlar. @No__t-0 ve ilişkili sınıflar, kendi karakter biçimleri, paragraf stilleri, satır sonu kuralları ve uluslararası metin için diğer düzen özellikleri tanımlarını destekleyen özel metin düzeni uygulamanıza olanak tanır. @No__t-0 metin düzeni desteğinin varsayılan uygulamasını geçersiz kılmak isteyebileceğiniz çok az durum vardır. Ancak, bir metin düzenlemesi denetimi veya uygulaması oluşturuyorsanız, varsayılan [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] uygulamasından farklı bir uygulamaya sahip olmanız gerekebilir.  
  
 Geleneksel bir metin API 'sinin aksine, <xref:System.Windows.Media.TextFormatting.TextFormatter>, bir geri arama yöntemi kümesi aracılığıyla metin düzeni istemcisiyle etkileşime girer. İstemcinin bu yöntemleri <xref:System.Windows.Media.TextFormatting.TextSource> sınıfının bir uygulamasında sağlamasını gerektirir. Aşağıdaki diyagramda, istemci uygulaması ile <xref:System.Windows.Media.TextFormatting.TextFormatter> arasındaki metin düzeni etkileşimi gösterilmektedir.  
  
 ![Metin düzeni istemcisi ve TextFormatter diyagramı](./media/typography-in-wpf/text-layout-text-formatter-interaction.png)  
  
 Özel metin düzeni oluşturma hakkında daha fazla bilgi için bkz. [Gelişmiş metin biçimlendirme](advanced-text-formatting.md).  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Windows.Media.FormattedText>
- <xref:System.Windows.Media.TextFormatting.TextFormatter>
- [ClearType Genel Bakışı](cleartype-overview.md)
- [OpenType Yazı Tipi Özellikleri](opentype-font-features.md)
- [Biçimlendirilmiş Metin Çizme](drawing-formatted-text.md)
- [Gelişmiş Metin Biçimlendirme](advanced-text-formatting.md)
- [Metin](optimizing-performance-text.md)
- [Microsoft Tipografi](https://docs.microsoft.com/typography/)
