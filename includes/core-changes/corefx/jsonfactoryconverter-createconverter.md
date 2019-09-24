---
ms.openlocfilehash: e16f0c8ede5e1a24d4fc4606c3c25225ea72e750
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117137"
---
### <a name="jsonfactoryconvertercreateconverter-signature-changed"></a><span data-ttu-id="8bd5d-101">JsonFactoryConverter. CreateConverter imzası değişti</span><span class="sxs-lookup"><span data-stu-id="8bd5d-101">JsonFactoryConverter.CreateConverter signature changed</span></span>

<span data-ttu-id="8bd5d-102"><xref:System.Text.Json.Serialization.JsonConverterFactory> Sınıfların oluşumunu kolaylaştırmak için <xref:System.Text.Json.Serialization.JsonConverterFactory.CreateConverter%2A> , yöntemi genel yapıldı ve türünde <xref:System.Text.Json.JsonSerializerOptions>ikinci bir bağımsız değişken verildi.</span><span class="sxs-lookup"><span data-stu-id="8bd5d-102">To facilitate the composition of <xref:System.Text.Json.Serialization.JsonConverterFactory> classes, the <xref:System.Text.Json.Serialization.JsonConverterFactory.CreateConverter%2A> method has been made public and given a second argument of type <xref:System.Text.Json.JsonSerializerOptions>.</span></span>

#### <a name="details"></a><span data-ttu-id="8bd5d-103">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="8bd5d-103">Details</span></span>

<span data-ttu-id="8bd5d-104">.NET Core sürümündeki 3,0 `CreateConverter` Preview 8 ' den önceki yöntemin imzası:</span><span class="sxs-lookup"><span data-stu-id="8bd5d-104">The signature of the `CreateConverter` method in .NET Core prior to version 3.0 Preview 8 was:</span></span> 

```csharp
namespace System.Text.Json.Serialization
{
    public abstract class JsonConverterFactory : JsonConverter
    {
        protected abstract JsonConverter CreateConverter(Type typeToConvert);
    }
}
```

<span data-ttu-id="8bd5d-105">.NET Core 3,0 Preview 8 ve sonraki sürümlerinde, şu şekilde olur:</span><span class="sxs-lookup"><span data-stu-id="8bd5d-105">In .NET Core 3.0 Preview 8 and later versions, it is:</span></span>

```csharp
namespace System.Text.Json.Serialization
{
    public abstract class JsonConverterFactory : JsonConverter
    {
        public abstract JsonConverter CreateConverter(Type typeToConvert, JsonSerializerOptions options);
    }
}
```

<span data-ttu-id="8bd5d-106">Bu değişiklikten önce, bunu yapmanın kolay bir yolu <xref:System.Text.Json.Serialization.JsonConverter%601> olmadığından, korumalı fabrika dönüştürücülerini oluşturmak zordur.</span><span class="sxs-lookup"><span data-stu-id="8bd5d-106">Before this change, it was difficult to compose sealed factory converters, since there was no easy way to get the <xref:System.Text.Json.Serialization.JsonConverter%601> from it.</span></span> <span data-ttu-id="8bd5d-107">Fabrika yöntemini herkese açık hale getirme ve ayrıca, daha <xref:System.Text.Json.JsonSerializerOptions> fazla esnek bileşim için geçerli izin vermeyi geçirme.</span><span class="sxs-lookup"><span data-stu-id="8bd5d-107">Making the factory method public and also passing the current <xref:System.Text.Json.JsonSerializerOptions> allow for much more flexible composition.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="8bd5d-108">Sunulan sürüm</span><span class="sxs-lookup"><span data-stu-id="8bd5d-108">Version introduced</span></span>

<span data-ttu-id="8bd5d-109">3,0 Preview 8</span><span class="sxs-lookup"><span data-stu-id="8bd5d-109">3.0 Preview 8</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="8bd5d-110">Önerilen eylem</span><span class="sxs-lookup"><span data-stu-id="8bd5d-110">Recommended action</span></span>

<span data-ttu-id="8bd5d-111">Türetilmiş sınıfların güncellenmesi ve yeniden derlenmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="8bd5d-111">Derived classes need to be updated and recompiled.</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="8bd5d-112">Etkilenen API’ler</span><span class="sxs-lookup"><span data-stu-id="8bd5d-112">Affected APIs</span></span>

<span data-ttu-id="8bd5d-113"><xref:System.Text.Json.Serialization.JsonConverterFactory.CreateConverter(System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="8bd5d-113"><xref:System.Text.Json.Serialization.JsonConverterFactory.CreateConverter(System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType>.</span></span>

<!-- For tool use only

### Affected APIs

- `M:System.Text.Json.Serialization.JsonConverterFactory.CreateConverter(System.Type,System.Text.Json.JsonSerializerOptions)`

-->