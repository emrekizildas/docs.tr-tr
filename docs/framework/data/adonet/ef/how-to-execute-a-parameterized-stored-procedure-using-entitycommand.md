---
title: 'Nasıl yapılır: EntityCommand Kullanarak Parametreli Saklı Yordam Yürütme'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 4f5639bf-bb7f-4982-bb1d-c7caa4348888
ms.openlocfilehash: 27e756d8e44580d9205cc075367bce5a45536c69
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854687"
---
# <a name="how-to-execute-a-parameterized-stored-procedure-using-entitycommand"></a>Nasıl yapılır: EntityCommand Kullanarak Parametreli Saklı Yordam Yürütme
Bu konu, <xref:System.Data.EntityClient.EntityCommand> sınıfını kullanarak parametreli saklı yordamın nasıl yürütüleceğini gösterir.  
  
### <a name="to-run-the-code-in-this-example"></a>Bu örnekteki kodu çalıştırmak için  
  
1. [Okul modelini](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)) projenize ekleyin ve projenizi Entity Framework kullanacak şekilde yapılandırın. Daha fazla bilgi için [nasıl yapılır: Varlık Veri Modeli Sihirbazı](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))'nı kullanın.  
  
2. Uygulamanızın kod sayfasında, aşağıdaki `using` deyimleri ekleyin (`Imports` Visual Basic):  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
3. Saklı yordamı içeri aktarın ve varlık dönüş türü olarak belirtin `CourseGrade`. `GetStudentGrades` Saklı yordamı içeri aktarma hakkında daha fazla bilgi için bkz [. nasıl yapılır: Saklı yordamı](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896231(v=vs.100))içeri aktarın.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki kod, gerekli bir `GetStudentGrades` parametre `StudentId` olan saklı yordamı yürütür. Sonuçlar daha sonra bir <xref:System.Data.EntityClient.EntityDataReader>ile okunurdur.  
  
 [!code-csharp[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#storedprocwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#storedprocwithentitycommand)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Entity Framework için EntityClient Sağlayıcısı](entityclient-provider-for-the-entity-framework.md)
