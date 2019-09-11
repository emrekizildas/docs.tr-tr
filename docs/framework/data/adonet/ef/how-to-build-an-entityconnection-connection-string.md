---
title: 'Nasıl yapılır: Bir EntityConnection Bağlantı Dizesi Oluşturma'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5bd1a748-3df7-4d0a-a607-14f25e3175e9
ms.openlocfilehash: f0918950921e620f724fedd8be027ffe0e2d3fa6
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854664"
---
# <a name="how-to-build-an-entityconnection-connection-string"></a><span data-ttu-id="a27a9-102">Nasıl yapılır: Bir EntityConnection Bağlantı Dizesi Oluşturma</span><span class="sxs-lookup"><span data-stu-id="a27a9-102">How to: Build an EntityConnection Connection String</span></span>
<span data-ttu-id="a27a9-103">Bu konu, oluşturma <xref:System.Data.EntityClient.EntityConnection>hakkında bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="a27a9-103">This topic provides an example of how to build an <xref:System.Data.EntityClient.EntityConnection>.</span></span>  
  
### <a name="to-run-the-code-in-this-example"></a><span data-ttu-id="a27a9-104">Bu örnekteki kodu çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="a27a9-104">To run the code in this example</span></span>  
  
1. <span data-ttu-id="a27a9-105">Projenize [AdventureWorks Sales modelini](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) ekleyin ve projenizi Entity Framework kullanacak şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a27a9-105">Add the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) to your project and configure your project to use the Entity Framework.</span></span> <span data-ttu-id="a27a9-106">Daha fazla bilgi için [nasıl yapılır: Varlık Veri Modeli Sihirbazı](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a27a9-106">For more information, see [How to: Use the Entity Data Model Wizard](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100)).</span></span>  
  
2. <span data-ttu-id="a27a9-107">Uygulamanızın kod sayfasında, aşağıdaki `using` deyimleri ekleyin (`Imports` Visual Basic):</span><span class="sxs-lookup"><span data-stu-id="a27a9-107">In the code page for your application, add the following `using` statements (`Imports` in Visual Basic):</span></span>  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## <a name="example"></a><span data-ttu-id="a27a9-108">Örnek</span><span class="sxs-lookup"><span data-stu-id="a27a9-108">Example</span></span>  
 <span data-ttu-id="a27a9-109">Aşağıdaki örnek, <xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=nameWithType> temel sağlayıcı için öğesini başlatır, sonra <xref:System.Data.EntityClient.EntityConnectionStringBuilder?displayProperty=nameWithType> nesneyi başlatır ve bu nesneyi öğesinin <xref:System.Data.EntityClient.EntityConnection>oluşturucusuna geçirir.</span><span class="sxs-lookup"><span data-stu-id="a27a9-109">The following example initializes the <xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=nameWithType> for the underlying provider, then initializes the <xref:System.Data.EntityClient.EntityConnectionStringBuilder?displayProperty=nameWithType> object and passes this object to the constructor of the <xref:System.Data.EntityClient.EntityConnection>.</span></span>  
  
 [!code-csharp[DP EntityServices Concepts#BuildingConnectionStringWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#buildingconnectionstringwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#BuildingConnectionStringWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#buildingconnectionstringwithentitycommand)]  
  
## <a name="see-also"></a><span data-ttu-id="a27a9-110">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a27a9-110">See also</span></span>

- <span data-ttu-id="a27a9-111">[Nasıl yapılır: Bir nesne bağlamı ile EntityConnection kullanma](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738461(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="a27a9-111">[How to: Use EntityConnection with an Object Context](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738461(v=vs.100))</span></span>
- [<span data-ttu-id="a27a9-112">Entity Framework için EntityClient Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="a27a9-112">EntityClient Provider for the Entity Framework</span></span>](entityclient-provider-for-the-entity-framework.md)
