---
title: Mikro hizmet başına veri hakimiyeti
description: Mikro hizmet başına veri egementy, mikro hizmetlerin önemli noktalarından biridir. Her mikro hizmet veritabanının tek sahibi olmalıdır ve onu başka hiçbir olmadan paylaşmalıdır. Tabii ki, bir mikro hizmetin tüm örnekleri aynı yüksek kullanılabilirlik veritabanına bağlanır.
ms.date: 09/20/2018
ms.openlocfilehash: cd7be23800394b231e15bdc503d15a960a25a20a
ms.sourcegitcommit: 29a9b29d8b7d07b9c59d46628da754a8bff57fa4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/17/2019
ms.locfileid: "70296806"
---
# <a name="data-sovereignty-per-microservice"></a><span data-ttu-id="a4ab7-105">Mikro hizmet başına veri hakimiyeti</span><span class="sxs-lookup"><span data-stu-id="a4ab7-105">Data sovereignty per microservice</span></span>

<span data-ttu-id="a4ab7-106">Mikro hizmetler mimarisi için önemli bir kural, her mikro hizmetin kendi etki alanı verilerine ve mantığına sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-106">An important rule for microservices architecture is that each microservice must own its domain data and logic.</span></span> <span data-ttu-id="a4ab7-107">Tam bir uygulamanın Logic ve verilerinin sahibi olduğu için, her mikro hizmetin kendi mantığını ve verileri, mikro hizmet başına bağımsız dağıtım ile bir otonom yaşam döngüsü altında sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-107">Just as a full application owns its logic and data, so must each microservice own its logic and data under an autonomous lifecycle, with independent deployment per microservice.</span></span>

<span data-ttu-id="a4ab7-108">Bu, etki alanı kavramsal modelinin alt sistemler veya mikro hizmetler arasında farklı olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-108">This means that the conceptual model of the domain will differ between subsystems or microservices.</span></span> <span data-ttu-id="a4ab7-109">Müşteri ilişkileri yönetimi (CRM) uygulamaları, işlem satın alma alt sistemleri ve müşteri destek alt sistemlerinin her biri benzersiz müşteri varlığı öznitelikleri ve verileri üzerinde her çağrının ve her birinin farklı bir şekilde kullanıldığı kurumsal uygulamaları göz önünde bulundurun. Sınırlanmış bağlam (BC).</span><span class="sxs-lookup"><span data-stu-id="a4ab7-109">Consider enterprise applications, where customer relationship management (CRM) applications, transactional purchase subsystems, and customer support subsystems each call on unique customer entity attributes and data, and where each employs a different Bounded Context (BC).</span></span>

<span data-ttu-id="a4ab7-110">Bu ilke, her [sınırlanmış bağlam](https://martinfowler.com/bliki/BoundedContext.html) veya özerk alt sistem ya da hizmetin kendi etki alanı modeline sahip olması gerektiği [etki alanı ODAKLı tasarım (DDD)](https://en.wikipedia.org/wiki/Domain-driven_design)ile benzerdir (veri ve mantık ve davranış).</span><span class="sxs-lookup"><span data-stu-id="a4ab7-110">This principle is similar in [Domain-driven design (DDD)](https://en.wikipedia.org/wiki/Domain-driven_design), where each [Bounded Context](https://martinfowler.com/bliki/BoundedContext.html) or autonomous subsystem or service must own its domain model (data plus logic and behavior).</span></span> <span data-ttu-id="a4ab7-111">Her DDD sınırlı bağlam, bir iş mikro hizmeti (bir veya birkaç hizmet) ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-111">Each DDD Bounded Context correlates to one business microservice (one or several services).</span></span> <span data-ttu-id="a4ab7-112">Sınırlanmış bağlam deseninin bu noktası sonraki bölümde genişletilir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-112">This point about the Bounded Context pattern is expanded in the next section.</span></span>

<span data-ttu-id="a4ab7-113">Diğer taraftan, birçok uygulamada kullanılan geleneksel (tek parçalı veriler) yaklaşımının tek bir merkezi veritabanı veya yalnızca birkaç veritabanı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-113">On the other hand, the traditional (monolithic data) approach used in many applications is to have a single centralized database or just a few databases.</span></span> <span data-ttu-id="a4ab7-114">Bu genellikle Şekil 4-7 ' de gösterildiği gibi, tüm uygulama ve tüm iç alt sistemleri için kullanılan normalleştirilmiş bir SQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-114">This is often a normalized SQL database that's used for the whole application and all its internal subsystems, as shown in Figure 4-7.</span></span>

![Geleneksel yaklaşımda, genellikle katmanlı bir mimaride tüm hizmetler genelinde paylaşılan tek bir veritabanı vardır.](./media/image7.png)

<span data-ttu-id="a4ab7-117">**Şekil 4-7**.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-117">**Figure 4-7**.</span></span> <span data-ttu-id="a4ab7-118">Veri egemenlik karşılaştırması: tek parçalı veritabanı ve mikro hizmetler karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="a4ab7-118">Data sovereignty comparison: monolithic database versus microservices</span></span>

<span data-ttu-id="a4ab7-119">Merkezi veritabanı yaklaşımı başlangıçta daha basit bir şekilde görünür ve her şeyi tutarlı hale getirmek için farklı alt sistemlerde varlıkların yeniden kullanımını etkinleştirmek gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-119">The centralized database approach initially looks simpler and seems to enable reuse of entities in different subsystems to make everything consistent.</span></span> <span data-ttu-id="a4ab7-120">Ancak gerçekliği, birçok farklı alt sistemi sunan ve çoğu durumda gerekmeyen öznitelikleri ve sütunları içeren çok büyük tablolar ile sona erdirmek ister.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-120">But the reality is you end up with huge tables that serve many different subsystems, and that include attributes and columns that aren't needed in most cases.</span></span> <span data-ttu-id="a4ab7-121">Kısa bir izleme için aynı fiziksel eşlemeyi kullanmaya çalışmak, gün uzunluğunda bir otomobil yolculuğu ve öğrenme Coğrafya almak gibidir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-121">It's like trying to use the same physical map for hiking a short trail, taking a day-long car trip, and learning geography.</span></span>

<span data-ttu-id="a4ab7-122">Genellikle tek bir ilişkisel veritabanına sahip tek parçalı bir uygulama iki önemli avantaja sahiptir: [ACID işlemleri](https://en.wikipedia.org/wiki/ACID) ve SQL dili, her ikisi de uygulamanızla ilgili tüm tablolar ve veriler üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-122">A monolithic application with typically a single relational database has two important benefits: [ACID transactions](https://en.wikipedia.org/wiki/ACID) and the SQL language, both working across all the tables and data related to your application.</span></span> <span data-ttu-id="a4ab7-123">Bu yaklaşım, birden çok tablodan verileri birleştiren bir sorguyu kolayca yazmak için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-123">This approach provides a way to easily write a query that combines data from multiple tables.</span></span>

<span data-ttu-id="a4ab7-124">Ancak, mikro hizmetler mimarisine geçtiğinizde veri erişimi çok daha karmaşık hale gelir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-124">However, data access becomes much more complex when you move to a microservices architecture.</span></span> <span data-ttu-id="a4ab7-125">Ancak, bir mikro hizmet veya sınırlı bağlam içinde ACID işlemleri de kullanılabilir olduğunda bile, her bir mikro hizmetin sahip olduğu veriler bu mikro hizmete özeldir ve yalnızca mikro hizmet API 'SI aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-125">But even when ACID transactions can or should be used within a microservice or Bounded Context, the data owned by each microservice is private to that microservice and can only be accessed via its microservice API.</span></span> <span data-ttu-id="a4ab7-126">Verilerin kapsüllenmesi, mikro hizmetlerin gevşek bir şekilde bağlanmış olmasını sağlar ve birbirinden bağımsız olarak gelişebilirler.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-126">Encapsulating the data ensures that the microservices are loosely coupled and can evolve independently of one another.</span></span> <span data-ttu-id="a4ab7-127">Aynı verilere birden çok hizmet erişiyorsa, şema güncelleştirmeleri tüm hizmetlere yönelik Eşgüdümlü güncelleştirmeler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-127">If multiple services were accessing the same data, schema updates would require coordinated updates to all the services.</span></span> <span data-ttu-id="a4ab7-128">Bu, mikro hizmet yaşam döngüsü bağımsız çalışma sınırı kesintiye uğratır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-128">This would break the microservice lifecycle autonomy.</span></span> <span data-ttu-id="a4ab7-129">Ancak dağıtılmış veri yapıları, mikro hizmetler genelinde tek bir ACID işlemi yapamayacağınız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-129">But distributed data structures mean that you can't make a single ACID transaction across microservices.</span></span> <span data-ttu-id="a4ab7-130">Buna karşılık, bir iş süreci birden çok mikro hizmete yayıldığında nihai tutarlılığı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-130">This in turn means you must use eventual consistency when a business process spans multiple microservices.</span></span> <span data-ttu-id="a4ab7-131">Bu, daha sonra açıklandığımız gibi, bütünlük kısıtlamaları oluşturamadığından veya ayrı veritabanları arasında dağıtılmış işlemler kullanamadığından basit SQL birleştirmelere uygulama çok daha zordur.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-131">This is much harder to implement than simple SQL joins, because you can't create integrity constraints or use distributed transactions between separate databases, as we'll explain later on.</span></span> <span data-ttu-id="a4ab7-132">Benzer şekilde, çok sayıda diğer ilişkisel veritabanı özelliği birden fazla mikro hizmette kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-132">Similarly, many other relational database features aren't available across multiple microservices.</span></span>

<span data-ttu-id="a4ab7-133">Daha da farklı mikro hizmetler, genellikle farklı *türlerde* veritabanları kullanır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-133">Going even further, different microservices often use different *kinds* of databases.</span></span> <span data-ttu-id="a4ab7-134">Modern uygulamalar çeşitli veri türlerini depolar ve işler ve ilişkisel veritabanı her zaman en iyi seçenektir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-134">Modern applications store and process diverse kinds of data, and a relational database isn't always the best choice.</span></span> <span data-ttu-id="a4ab7-135">Bazı kullanım durumları için, Azure CosmosDB veya MongoDB gibi bir NoSQL veritabanının daha uygun bir veri modeli olabilir ve SQL Server veya Azure SQL veritabanı gibi bir SQL veritabanından daha iyi performans ve ölçeklenebilirlik sunar.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-135">For some use cases, a NoSQL database such as Azure CosmosDB or MongoDB might have a more convenient data model and offer better performance and scalability than a SQL database like SQL Server or Azure SQL Database.</span></span> <span data-ttu-id="a4ab7-136">Diğer durumlarda, ilişkisel bir veritabanı hala en iyi yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-136">In other cases, a relational database is still the best approach.</span></span> <span data-ttu-id="a4ab7-137">Bu nedenle, mikro hizmet tabanlı uygulamalar genellikle [çok yönlü Kalıcılık](https://martinfowler.com/bliki/PolyglotPersistence.html) yaklaşımı olarak adlandırılan SQL ve NoSQL veritabanlarının bir karışımını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-137">Therefore, microservices-based applications often use a mixture of SQL and NoSQL databases, which is sometimes called the [polyglot persistence](https://martinfowler.com/bliki/PolyglotPersistence.html) approach.</span></span>

<span data-ttu-id="a4ab7-138">Veri depolama için bölümlenmiş, çok yönlü kalıcı mimarinin birçok avantajı vardır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-138">A partitioned, polyglot-persistent architecture for data storage has many benefits.</span></span> <span data-ttu-id="a4ab7-139">Bunlar arasında gevşek olarak bağlanmış hizmetler, daha iyi performans, ölçeklenebilirlik, maliyetler ve yönetilebilirlik bulunur.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-139">These include loosely coupled services and better performance, scalability, costs, and manageability.</span></span> <span data-ttu-id="a4ab7-140">Ancak, bu bölümün devamındaki "[etki alanı model sınırlarını tanımlama](identify-microservice-domain-model-boundaries.md)" bölümünde açıklandığı gibi bazı dağıtılmış veri yönetimi sorunlarını ortaya çıkarabilir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-140">However, it can introduce some distributed data management challenges, as explained in "[Identifying domain-model boundaries](identify-microservice-domain-model-boundaries.md)" later in this chapter.</span></span>

## <a name="the-relationship-between-microservices-and-the-bounded-context-pattern"></a><span data-ttu-id="a4ab7-141">Mikro hizmetler ve sınırlanmış bağlam deseninin arasındaki ilişki</span><span class="sxs-lookup"><span data-stu-id="a4ab7-141">The relationship between microservices and the Bounded Context pattern</span></span>

<span data-ttu-id="a4ab7-142">Mikro hizmet kavramı, [etki alanı odaklı tasarımda (DDD)](https://en.wikipedia.org/wiki/Domain-driven_design) [SıNıRLANMıŞ bağlam (BC)](https://martinfowler.com/bliki/BoundedContext.html) düzeninden türetilir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-142">The concept of microservice derives from the [Bounded Context (BC) pattern](https://martinfowler.com/bliki/BoundedContext.html) in [domain-driven design (DDD)](https://en.wikipedia.org/wiki/Domain-driven_design).</span></span> <span data-ttu-id="a4ab7-143">DDD, büyük modellerle anlaşmalar yaparak bunları birden çok BCs dönüştürür ve sınırları hakkında açık bir şekilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-143">DDD deals with large models by dividing them into multiple BCs and being explicit about their boundaries.</span></span> <span data-ttu-id="a4ab7-144">Her bir BC kendi modeli ve veritabanına sahip olmalıdır; benzer şekilde, her mikro hizmet ilgili verilerin sahibidir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-144">Each BC must have its own model and database; likewise, each microservice owns its related data.</span></span> <span data-ttu-id="a4ab7-145">Ayrıca, her bir BC yazılım geliştiricileri ve etki alanı uzmanları arasındaki iletişime yardımcı olmak için genellikle kendi [ubititous diline](https://martinfowler.com/bliki/UbiquitousLanguage.html) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-145">In addition, each BC usually has its own [ubiquitous language](https://martinfowler.com/bliki/UbiquitousLanguage.html) to help communication between software developers and domain experts.</span></span>

<span data-ttu-id="a4ab7-146">Ubititous dilinde söz konusu şartlar (genellikle etki alanı varlıkları) farklı sınırlanmış bağlamlarda farklı adlara sahip olabilir, farklı etki alanı varlıkları aynı kimliği paylaşır (yani, varlığı depolamadan okumak için kullanılan benzersiz KIMLIK).</span><span class="sxs-lookup"><span data-stu-id="a4ab7-146">Those terms (mainly domain entities) in the ubiquitous language can have different names in different Bounded Contexts, even when different domain entities share the same identity (that is, the unique ID that's used to read the entity from storage).</span></span> <span data-ttu-id="a4ab7-147">Örneğin, Kullanıcı profili sınırlı bağlamında, Kullanıcı etki alanı varlığı, kimlik sıralama bağlantılı bağlamdaki alıcı etki alanı varlığı ile kimlik paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-147">For instance, in a user-profile Bounded Context, the User domain entity might share identity with the Buyer domain entity in the ordering Bounded Context.</span></span>

<span data-ttu-id="a4ab7-148">Bu nedenle, bir mikro hizmet sınırlanmış bir bağlam gibidir, ancak aynı zamanda dağıtılmış bir hizmet olduğunu da belirtir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-148">A microservice is therefore like a Bounded Context, but it also specifies that it's a distributed service.</span></span> <span data-ttu-id="a4ab7-149">Her sınırlanmış bağlam için ayrı bir işlem olarak oluşturulmuştur ve HTTP/HTTPS, WebSockets veya [AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol)gibi daha önce belirtilen dağıtılmış protokolleri kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-149">It's built as a separate process for each Bounded Context, and it must use the distributed protocols noted earlier, like HTTP/HTTPS, WebSockets, or [AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol).</span></span> <span data-ttu-id="a4ab7-150">Bununla sınırlı bağlam deseninin, bir tek parçalı dağıtım uygulaması içinde, sınırlanmış bağlamın dağıtılmış bir hizmet olup olmadığını ya da yalnızca bir mantıksal sınır (genel alt sistem gibi) belirtilmediğini belirtmez.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-150">The Bounded Context pattern, however, doesn't specify whether the Bounded Context is a distributed service or if it's simply a logical boundary (such as a generic subsystem) within a monolithic-deployment application.</span></span>

<span data-ttu-id="a4ab7-151">Her sınırlanmış bağlam için bir hizmet tanımlamanın başlamak için iyi bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-151">It's important to highlight that defining a service for each Bounded Context is a good place to start.</span></span> <span data-ttu-id="a4ab7-152">Ancak tasarımınızı buna karşı kısıtlamak zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-152">But you don't have to constrain your design to it.</span></span> <span data-ttu-id="a4ab7-153">Bazen, birkaç fiziksel hizmetten oluşan sınırlı bir bağlam veya iş mikro hizmeti tasarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-153">Sometimes you must design a Bounded Context or business microservice composed of several physical services.</span></span> <span data-ttu-id="a4ab7-154">Ancak, her ikisi de desenler ile sınırlanmış bağlam ve mikro hizmet ile yakından ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-154">But ultimately, both patterns -Bounded Context and microservice- are closely related.</span></span>

<span data-ttu-id="a4ab7-155">, Dağıtılmış mikro hizmetler biçiminde gerçek sınırlar alarak mikro hizmetlerden faydalanır.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-155">DDD benefits from microservices by getting real boundaries in the form of distributed microservices.</span></span> <span data-ttu-id="a4ab7-156">Bununla birlikte, mikro hizmetler arasında modeli paylaşmayan fikirler da sınırlanmış bir bağlamda olmasını istediğiniz şeydir.</span><span class="sxs-lookup"><span data-stu-id="a4ab7-156">But ideas like not sharing the model between microservices are what you also want in a Bounded Context.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="a4ab7-157">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a4ab7-157">Additional resources</span></span>

- <span data-ttu-id="a4ab7-158">**Chris Richardson. Kalıp Hizmet başına veritabanı** </span><span class="sxs-lookup"><span data-stu-id="a4ab7-158">**Chris Richardson. Pattern: Database per service** </span></span>\
  <https://microservices.io/patterns/data/database-per-service.html>

- <span data-ttu-id="a4ab7-159">**Marwler. BoundedContext** </span><span class="sxs-lookup"><span data-stu-id="a4ab7-159">**Martin Fowler. BoundedContext** </span></span>\
  <https://martinfowler.com/bliki/BoundedContext.html>

- <span data-ttu-id="a4ab7-160">**Marwler. PolyglotPersistence** </span><span class="sxs-lookup"><span data-stu-id="a4ab7-160">**Martin Fowler. PolyglotPersistence** </span></span>\
  <https://martinfowler.com/bliki/PolyglotPersistence.html>

- <span data-ttu-id="a4ab7-161">**Alberto Brandolini. Bağlam eşleme ile stratejik etki alanı odaklı tasarım** </span><span class="sxs-lookup"><span data-stu-id="a4ab7-161">**Alberto Brandolini. Strategic Domain Driven Design with Context Mapping** </span></span>\
  <https://www.infoq.com/articles/ddd-contextmapping>

>[!div class="step-by-step"]
><span data-ttu-id="a4ab7-162">[Önceki](microservices-architecture.md)İleri
>[](logical-versus-physical-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="a4ab7-162">[Previous](microservices-architecture.md)
[Next](logical-versus-physical-architecture.md)</span></span>