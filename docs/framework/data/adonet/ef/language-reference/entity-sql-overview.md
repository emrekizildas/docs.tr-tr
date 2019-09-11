---
title: Entity SQL’e Genel Bakış
ms.date: 03/30/2017
ms.assetid: f0bb8120-e709-40a3-ac1e-5520dc47477d
ms.openlocfilehash: 8f40a34f361669d2b8d89b63b3187cae6bf705d2
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854490"
---
# <a name="entity-sql-overview"></a><span data-ttu-id="33644-102">Entity SQL’e Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="33644-102">Entity SQL Overview</span></span>
[!INCLUDE[esql](../../../../../../includes/esql-md.md)]<span data-ttu-id="33644-103">, Entity Framework kavramsal modelleri sorgulamanızı sağlayan bir SQL benzeri dildir.</span><span class="sxs-lookup"><span data-stu-id="33644-103">is a SQL-like language that enables you to query conceptual models in the Entity Framework.</span></span> <span data-ttu-id="33644-104">Kavramsal modeller verileri varlıklar ve ilişkiler olarak temsil eder ve [!INCLUDE[esql](../../../../../../includes/esql-md.md)] bu varlıkları ve ilişkileri SQL kullanan kullanıcılara tanıdık bir biçimde sorgulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="33644-104">Conceptual models represent data as entities and relationships, and [!INCLUDE[esql](../../../../../../includes/esql-md.md)] allows you to query those entities and relationships in a format that is familiar to those who have used SQL.</span></span>  
      
 <span data-ttu-id="33644-105">Entity Framework, genel [!INCLUDE[esql](../../../../../../includes/esql-md.md)] olarak depolamaya özgü sorgulara çevirmek için depolama 'ya özgü veri sağlayıcılarıyla birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="33644-105">The Entity Framework works with storage-specific data providers to translate generic [!INCLUDE[esql](../../../../../../includes/esql-md.md)] into storage-specific queries.</span></span> <span data-ttu-id="33644-106">EntityClient sağlayıcısı bir varlık modeline karşı bir [!INCLUDE[esql](../../../../../../includes/esql-md.md)] komut yürütmek ve skaler sonuçlar, sonuç kümeleri ve nesne grafikleri dahil zengin veri türlerini döndürmek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="33644-106">The EntityClient provider supplies a way to execute an [!INCLUDE[esql](../../../../../../includes/esql-md.md)] command against an entity model and return rich types of data including scalar results, result sets, and object graphs.</span></span> <span data-ttu-id="33644-107">Nesneleri oluştururken, <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=nameWithType> özelliğine bir [!INCLUDE[esql](../../../../../../includes/esql-md.md)] sorgu dizesi atayarak bir saklı yordam adı veya bir sorgu metni belirtebilirsiniz. <xref:System.Data.EntityClient.EntityCommand></span><span class="sxs-lookup"><span data-stu-id="33644-107">When you construct <xref:System.Data.EntityClient.EntityCommand> objects, you can specify a stored procedure name or the text of a query by assigning an [!INCLUDE[esql](../../../../../../includes/esql-md.md)] query string to its <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="33644-108">, <xref:System.Data.EntityClient.EntityDataReader> Bir<xref:System.Data.EntityClient.EntityCommand> EDM için yürütme sonuçlarını sunar.</span><span class="sxs-lookup"><span data-stu-id="33644-108">The <xref:System.Data.EntityClient.EntityDataReader> exposes the results of executing a <xref:System.Data.EntityClient.EntityCommand> against an EDM.</span></span> <span data-ttu-id="33644-109"><xref:System.Data.EntityClient.EntityDataReader>Öğesini döndüren komutunu yürütmek için çağrısı <xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A>yapın.</span><span class="sxs-lookup"><span data-stu-id="33644-109">To execute the command that returns the <xref:System.Data.EntityClient.EntityDataReader>, call <xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A>.</span></span>  
  
 <span data-ttu-id="33644-110">EntityClient sağlayıcısına ek olarak Entity Framework, sorguları kavramsal bir modele karşı yürütmek ve [!INCLUDE[esql](../../../../../../includes/esql-md.md)] verileri varlık türlerinin örnekleri olan kesin türü belirtilmiş CLR nesneleri olarak döndürmek için kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="33644-110">In addition to the EntityClient provider, the Entity Framework enables you to use [!INCLUDE[esql](../../../../../../includes/esql-md.md)] to execute queries against a conceptual model and return data as strongly-typed CLR objects that are instances of entity types.</span></span> <span data-ttu-id="33644-111">Daha fazla bilgi için bkz. [nesneleriyle çalışma](../working-with-objects.md).</span><span class="sxs-lookup"><span data-stu-id="33644-111">For more information, see [Working with Objects](../working-with-objects.md).</span></span>  
  
 <span data-ttu-id="33644-112">Bu bölüm hakkında [!INCLUDE[esql](../../../../../../includes/esql-md.md)]kavramsal bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="33644-112">This section provides conceptual information about [!INCLUDE[esql](../../../../../../includes/esql-md.md)].</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="33644-113">Bu Bölümde</span><span class="sxs-lookup"><span data-stu-id="33644-113">In This Section</span></span>  
 [<span data-ttu-id="33644-114">Entity SQL ile Transact-SQL Arasındaki Farklar</span><span class="sxs-lookup"><span data-stu-id="33644-114">How Entity SQL Differs from Transact-SQL</span></span>](how-entity-sql-differs-from-transact-sql.md)  
  
 [<span data-ttu-id="33644-115">Entity SQL Hızlı Başvurusu</span><span class="sxs-lookup"><span data-stu-id="33644-115">Entity SQL Quick Reference</span></span>](entity-sql-quick-reference.md)  
  
 [<span data-ttu-id="33644-116">Tür Sistemi</span><span class="sxs-lookup"><span data-stu-id="33644-116">Type System</span></span>](type-system-entity-sql.md)  
  
 [<span data-ttu-id="33644-117">Tür Tanımları</span><span class="sxs-lookup"><span data-stu-id="33644-117">Type Definitions</span></span>](type-definitions-entity-sql.md)  
  
 [<span data-ttu-id="33644-118">Oluşturma Türleri</span><span class="sxs-lookup"><span data-stu-id="33644-118">Constructing Types</span></span>](constructing-types-entity-sql.md)  
  
 [<span data-ttu-id="33644-119">Sorgu Planını Önbelleğe Alma</span><span class="sxs-lookup"><span data-stu-id="33644-119">Query Plan Caching</span></span>](query-plan-caching-entity-sql.md)  
  
 [<span data-ttu-id="33644-120">Ad Alanları</span><span class="sxs-lookup"><span data-stu-id="33644-120">Namespaces</span></span>](namespaces-entity-sql.md)  
  
 [<span data-ttu-id="33644-121">Tanımlayıcılar</span><span class="sxs-lookup"><span data-stu-id="33644-121">Identifiers</span></span>](identifiers-entity-sql.md)  
  
 [<span data-ttu-id="33644-122">Parametreler</span><span class="sxs-lookup"><span data-stu-id="33644-122">Parameters</span></span>](parameters-entity-sql.md)  
  
 [<span data-ttu-id="33644-123">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="33644-123">Variables</span></span>](variables-entity-sql.md)  
  
 [<span data-ttu-id="33644-124">Desteklenmeyen İfadeler</span><span class="sxs-lookup"><span data-stu-id="33644-124">Unsupported Expressions</span></span>](unsupported-expressions-entity-sql.md)  
  
 [<span data-ttu-id="33644-125">Değişmez Değerler</span><span class="sxs-lookup"><span data-stu-id="33644-125">Literals</span></span>](literals-entity-sql.md)  
  
 [<span data-ttu-id="33644-126">Null Değişmez Değerler ve Tür Çıkarımı</span><span class="sxs-lookup"><span data-stu-id="33644-126">Null Literals and Type Inference</span></span>](null-literals-and-type-inference-entity-sql.md)  
  
 [<span data-ttu-id="33644-127">Giriş Karakter Kümesi</span><span class="sxs-lookup"><span data-stu-id="33644-127">Input Character Set</span></span>](input-character-set-entity-sql.md)  
  
 [<span data-ttu-id="33644-128">Sorgu İfadeleri</span><span class="sxs-lookup"><span data-stu-id="33644-128">Query Expressions</span></span>](query-expressions-entity-sql.md)  
  
 [<span data-ttu-id="33644-129">İşlevler</span><span class="sxs-lookup"><span data-stu-id="33644-129">Functions</span></span>](functions-entity-sql.md)  
  
 [<span data-ttu-id="33644-130">İşleç Önceliği</span><span class="sxs-lookup"><span data-stu-id="33644-130">Operator Precedence</span></span>](operator-precedence-entity-sql.md)  
  
 [<span data-ttu-id="33644-131">Disk Belleği</span><span class="sxs-lookup"><span data-stu-id="33644-131">Paging</span></span>](paging-entity-sql.md)  
  
 [<span data-ttu-id="33644-132">Karşılaştırma Semantiği</span><span class="sxs-lookup"><span data-stu-id="33644-132">Comparison Semantics</span></span>](comparison-semantics-entity-sql.md)  
  
 [<span data-ttu-id="33644-133">İç İçe Geçmiş Entity SQL Sorguları Oluşturma</span><span class="sxs-lookup"><span data-stu-id="33644-133">Composing Nested Entity SQL Queries</span></span>](composing-nested-entity-sql-queries.md)  
  
 [<span data-ttu-id="33644-134">Null Değer Atanabilir Yapılandırılmış Türler</span><span class="sxs-lookup"><span data-stu-id="33644-134">Nullable Structured Types</span></span>](nullable-structured-types-entity-sql.md)  
  
## <a name="see-also"></a><span data-ttu-id="33644-135">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="33644-135">See also</span></span>

- [<span data-ttu-id="33644-136">Entity SQL Başvurusu</span><span class="sxs-lookup"><span data-stu-id="33644-136">Entity SQL Reference</span></span>](entity-sql-reference.md)
- [<span data-ttu-id="33644-137">Entity SQL Dili</span><span class="sxs-lookup"><span data-stu-id="33644-137">Entity SQL Language</span></span>](entity-sql-language.md)
- [<span data-ttu-id="33644-138">CSDL, SSDL ve MSL Belirtimleri</span><span class="sxs-lookup"><span data-stu-id="33644-138">CSDL, SSDL, and MSL Specifications</span></span>](csdl-ssdl-and-msl-specifications.md)
