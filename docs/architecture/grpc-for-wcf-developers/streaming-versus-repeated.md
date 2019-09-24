---
title: gRPC akış Hizmetleri ve yinelenen alanlar-WCF geliştiricileri için gRPC
description: GRPC ile veri koleksiyonlarını geçirme yöntemi olarak yinelenen alanları akış Hizmetleri ile karşılaştırma.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 7dc3c8f5bf2efc304da7d50661ba47db500e67a0
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184073"
---
# <a name="grpc-streaming-services-versus-repeated-fields"></a><span data-ttu-id="3ddf4-103">gRPC akış Hizmetleri ve yinelenen alanlara karşı</span><span class="sxs-lookup"><span data-stu-id="3ddf4-103">gRPC streaming services versus repeated fields</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="3ddf4-104">gRPC Hizmetleri, veri kümelerini veya nesne listelerini döndürmenin iki yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-104">gRPC services provide two ways of returning datasets, or lists of objects.</span></span> <span data-ttu-id="3ddf4-105">Protokol arabellekleri ileti belirtimi, başka bir `repeated` iletideki ileti türlerini veya ileti dizilerini bildirmek için anahtar sözcüğünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-105">The Protocol Buffers message specification uses the `repeated` keyword for declaring lists or arrays of messages within another message.</span></span> <span data-ttu-id="3ddf4-106">GRPC hizmeti belirtimi, birden fazla `stream` iletinin gönderildiği ve tek tek işlenebileceği uzun süre çalışan kalıcı bir bağlantı bildirmek için anahtar sözcüğünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-106">The gRPC service specification uses the `stream` keyword to declare a long-running persistent connection over which multiple messages are sent, and can be processed, individually.</span></span> <span data-ttu-id="3ddf4-107">`stream` Özelliği, bildirimler veya günlük iletileri gibi uzun süre çalışan zamana bağlı veriler için de kullanılabilir, ancak bu bölüm, tek bir veri kümesi döndürmek için kullanımını göz önünde bulunduracaktır.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-107">The `stream` feature can also be used for long-running temporal data such as notifications or log messages, but this chapter will consider its use for returning a single dataset.</span></span>

<span data-ttu-id="3ddf4-108">Kullanmanız gereken, veri kümesinin genel boyutu, istemci veya sunucu ucunda veri kümesini oluşturmak için geçen süre ve veri kümesinin tüketicisi ilk öğe kullanılabilir duruma geldiğinde bu işlemi yapmaya başlayıp başlamadığı gibi çeşitli faktörlere bağlıdır. ya da tüm yararlı bir işlem yapmak için veri kümesinin tamamını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-108">Which you should use depends on various factors, such as the overall size of the dataset, the time it took to create the dataset at either the client or server end, and whether the consumer of the dataset can start acting on it as soon as the first item is available, or needs the complete dataset to do anything useful.</span></span>

## <a name="when-to-use-repeated-fields"></a><span data-ttu-id="3ddf4-109">Alanlar ne zaman `repeated` kullanılır?</span><span class="sxs-lookup"><span data-stu-id="3ddf4-109">When to use `repeated` fields</span></span>

<span data-ttu-id="3ddf4-110">Boyut açısından kısıtlanmış olan ve kısa bir süre içinde tek bir şekilde oluşturulabilecek tüm veri kümeleri için — bir saniye altında, normal bir prototipte ileti içinde bir `repeated` alan kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-110">For any dataset that is constrained in size and that can be generated in its entirety in a short time—say, under one second—you should use a `repeated` field in a regular Protobuf message.</span></span> <span data-ttu-id="3ddf4-111">Örneğin, bir e-ticaret sisteminde, bir sipariş içindeki öğelerin listesini oluşturmak büyük olasılıkla hızlıdır ve liste çok büyük olmaz.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-111">For example, in an e-commerce system, to build a list of items within an order is probably quick and the list won't be very large.</span></span> <span data-ttu-id="3ddf4-112">Bir `repeated` alan içeren tek bir iletinin döndürülmesi, ' ın kullanılmasından daha hızlı bir şekilde bir `stream` sıralama düzeni ve daha az ağ yükü doğurur.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-112">Returning a single message with a `repeated` field is an order of magnitude faster than using a `stream` and incurs less network overhead.</span></span>

<span data-ttu-id="3ddf4-113">İstemci, işleme başlamadan önce tüm verilere ihtiyaç duyuyorsa ve veri kümesi bellekte oluşturmaya yetecek kadar küçükse, sunucudaki bellekte veri kümesinin gerçek oluşturulması daha yavaş olsa `repeated` bile bir alan kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-113">If the client needs all the data before starting to process it and the dataset is small enough to construct in memory, then consider using a `repeated` field even if the actual creation of the dataset in memory on the server is slower.</span></span>

## <a name="when-to-use-stream-methods"></a><span data-ttu-id="3ddf4-114">Yöntemler ne zaman `stream` kullanılır?</span><span class="sxs-lookup"><span data-stu-id="3ddf4-114">When to use `stream` methods</span></span>

<span data-ttu-id="3ddf4-115">İleti nesnelerinin potansiyel olarak çok büyük olduğu veri kümeleri, akış istekleri veya yanıtları kullanılarak en iyi şekilde aktarılır.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-115">Datasets where the message objects are potentially very large are best transferred using streaming requests or responses.</span></span> <span data-ttu-id="3ddf4-116">Bellekte büyük bir nesne oluşturmak, ağa yazmak ve sonra kaynakları boşaltmak daha etkilidir.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-116">It's more efficient to construct a large object in memory, write it to the network and then free up the resources.</span></span> <span data-ttu-id="3ddf4-117">Bu yaklaşım, hizmetinizin ölçeklenebilirliğini geliştirir.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-117">This approach will improve the scalability of your service.</span></span>

<span data-ttu-id="3ddf4-118">Benzer şekilde, bu dosyaları oluştururken belleğin tükenmemesi için, kısıtlanmış olmayan boyutun veri kümelerinin akış üzerinden gönderilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-118">Similarly, datasets of unconstrained size should be sent over streams to avoid running out of memory while constructing them.</span></span>

<span data-ttu-id="3ddf4-119">Her bir öğenin tüketici tarafından ayrı olarak işlenebildiği veri kümelerinde, ilerlemenin son kullanıcıya belirtilebileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-119">For datasets where each individual item can be processed separately by the consumer, you should consider using a stream if it means that progress can be indicated to the end user.</span></span> <span data-ttu-id="3ddf4-120">Bu, uygulamanın genel performansına karşı dengelenmesi gerekse de bir uygulamanın görünen yanıt hızını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-120">This could improve the apparent responsiveness of an application, although this should be balanced against the overall performance of the application.</span></span>

<span data-ttu-id="3ddf4-121">Akışların yararlı olabilecek başka bir senaryo da birçok hizmet arasında bir iletinin işlendiği yerdir.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-121">Another scenario where streams can be useful is where a message is being processed across multiple services.</span></span> <span data-ttu-id="3ddf4-122">Bir zincirdeki her bir hizmet bir akış döndürürse, Terminal Hizmeti (diğer bir deyişle, zincirdeki son), işlenen ve bir akış döndürebilen ya da bir akışa geri alınabilecek iletileri geri dönerek tek bir yanıt iletisine neden olur.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-122">If each service in a chain returns a stream, then the terminal service (that is, the last one in the chain) can start returning messages that can be processed and passed back along the chain to the original requestor, which can either return a stream or aggregate the results into a single response message.</span></span> <span data-ttu-id="3ddf4-123">Bu yaklaşım, eşleme/azaltma gibi desenlerin kendisini geliştirir.</span><span class="sxs-lookup"><span data-stu-id="3ddf4-123">This approach lends itself well to patterns like Map/Reduce.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="3ddf4-124">[Önceki](migrate-duplex-services.md)
>[İleri](client-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="3ddf4-124">[Previous](migrate-duplex-services.md)
[Next](client-libraries.md)</span></span>