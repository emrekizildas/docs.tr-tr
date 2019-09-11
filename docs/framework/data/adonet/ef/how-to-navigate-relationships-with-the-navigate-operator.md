---
title: 'Nasıl yapılır: Nasıl yapılır: Navigate İşleci ile İlişkilerde Gezinme'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 79996d2d-9b03-4a9d-82cc-7c5e7c2ad93d
ms.openlocfilehash: dca8c25babcbc1676552af8ef49b7a7e71cd6136
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854522"
---
# <a name="how-to-navigate-relationships-with-the-navigate-operator"></a><span data-ttu-id="b8878-102">Nasıl yapılır: Nasıl yapılır: Navigate İşleci ile İlişkilerde Gezinme</span><span class="sxs-lookup"><span data-stu-id="b8878-102">How to: Navigate Relationships with the Navigate Operator</span></span>
<span data-ttu-id="b8878-103">Bu konu, bir <xref:System.Data.EntityClient.EntityCommand> nesne kullanarak bir kavramsal modele karşı bir komutun nasıl yürütüleceğini ve bir <xref:System.Data.EntityClient.EntityDataReader>kullanarak <xref:System.Data.Metadata.Edm.RefType> sonuçların nasıl alınacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b8878-103">This topic shows how to execute a command against a conceptual model by using an <xref:System.Data.EntityClient.EntityCommand> object, and how to retrieve the <xref:System.Data.Metadata.Edm.RefType> results by using an <xref:System.Data.EntityClient.EntityDataReader>.</span></span>  
  
### <a name="to-run-the-code-in-this-example"></a><span data-ttu-id="b8878-104">Bu örnekteki kodu çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="b8878-104">To run the code in this example</span></span>  
  
1. <span data-ttu-id="b8878-105">Projenize [AdventureWorks Sales modelini](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) ekleyin ve projenizi Entity Framework kullanacak şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b8878-105">Add the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) to your project and configure your project to use the Entity Framework.</span></span> <span data-ttu-id="b8878-106">Daha fazla bilgi için [nasıl yapılır: Varlık Veri Modeli Sihirbazı](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b8878-106">For more information, see [How to: Use the Entity Data Model Wizard](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).</span></span>  
  
2. <span data-ttu-id="b8878-107">Uygulamanızın kod sayfasında, aşağıdaki `using` deyimleri ekleyin (`Imports` Visual Basic):</span><span class="sxs-lookup"><span data-stu-id="b8878-107">In the code page for your application, add the following `using` statements (`Imports` in Visual Basic):</span></span>  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## <a name="example"></a><span data-ttu-id="b8878-108">Örnek</span><span class="sxs-lookup"><span data-stu-id="b8878-108">Example</span></span>  
 <span data-ttu-id="b8878-109">Aşağıdaki örnek, ' de [gezinme](./language-reference/navigate-entity-sql.md) işleci kullanarak içindeki [!INCLUDE[esql](../../../../../includes/esql-md.md)] ilişkilerin nasıl gezinileni gösterir.</span><span class="sxs-lookup"><span data-stu-id="b8878-109">The following example shows how to navigate relationships in [!INCLUDE[esql](../../../../../includes/esql-md.md)] by using the [NAVIGATE](./language-reference/navigate-entity-sql.md) operator.</span></span> <span data-ttu-id="b8878-110">`Navigate` İşleci şu parametreleri alır: bir varlık örneği, ilişki türü, ilişkinin sonu ve ilişkinin başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="b8878-110">The `Navigate` operator takes the following parameters: an instance of an entity, the relationship type, the end of the relationship, and the beginning of the relationship.</span></span> <span data-ttu-id="b8878-111">İsteğe bağlı olarak, bir varlığın yalnızca bir örneğini ve ilişki türünü `Navigate` işlecine geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8878-111">Optionally, you can pass only an instance of an entity and the relationship type to the `Navigate` operator.</span></span>  
  
 [!code-csharp[DP EntityServices Concepts#NavigateWithNavOperatorWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#navigatewithnavoperatorwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#NavigateWithNavOperatorWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#navigatewithnavoperatorwithentitycommand)]  
  
## <a name="see-also"></a><span data-ttu-id="b8878-112">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b8878-112">See also</span></span>

- [<span data-ttu-id="b8878-113">Entity Framework için EntityClient Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="b8878-113">EntityClient Provider for the Entity Framework</span></span>](entityclient-provider-for-the-entity-framework.md)
- [<span data-ttu-id="b8878-114">Entity SQL Dili</span><span class="sxs-lookup"><span data-stu-id="b8878-114">Entity SQL Language</span></span>](./language-reference/entity-sql-language.md)
