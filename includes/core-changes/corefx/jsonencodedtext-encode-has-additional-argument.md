---
ms.openlocfilehash: 101740e828589d7d210527e3db82a1c949a6e0fd
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117101"
---
### <a name="jsonencodedtextencode-methods-have-an-additional-javascriptencoder-argument"></a><span data-ttu-id="2fc05-101">JsonEncodedText. Encode yöntemlerinde ek bir JavaScriptEncoder bağımsız değişkeni vardır</span><span class="sxs-lookup"><span data-stu-id="2fc05-101">JsonEncodedText.Encode methods have an additional JavaScriptEncoder argument</span></span>

<span data-ttu-id="2fc05-102">.NET Core 3,0 Preview 8 ' <xref:System.Text.Json.JsonEncodedText.Encode%2A?displayProperty=nameWithType> den itibaren Yöntemler isteğe bağlı <xref:System.Text.Encodings.Web.JavaScriptEncoder> bir bağımsız değişken içerir.</span><span class="sxs-lookup"><span data-stu-id="2fc05-102">Starting with .NET Core 3.0 Preview 8, the <xref:System.Text.Json.JsonEncodedText.Encode%2A?displayProperty=nameWithType> methods contain an optional <xref:System.Text.Encodings.Web.JavaScriptEncoder> argument.</span></span> 

#### <a name="details"></a><span data-ttu-id="2fc05-103">Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="2fc05-103">Details</span></span>

<span data-ttu-id="2fc05-104">.NET Core 3,0 yeni bir tür içerir: XREF: System. Text. JSON. JsonEncodedText. Encode% 2A? displayProperty = nameWithType >.</span><span class="sxs-lookup"><span data-stu-id="2fc05-104">.NET Core 3.0 includes a new type, xref:System.Text.Json.JsonEncodedText.Encode%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="2fc05-105">.NET Core 3,0 Preview 8 ' den itibaren, tüm <xref:System.Text.Json.JsonEncodedText.Encode%2A?displayProperty=nameWithType> yöntem aşırı yüklemelerinin imzası isteğe bağlı <xref:System.Text.Encodings.Web.JavaScriptEncoder> bir parametre içerecek şekilde değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2fc05-105">Starting with .NET Core 3.0 Preview 8, the signature of all <xref:System.Text.Json.JsonEncodedText.Encode%2A?displayProperty=nameWithType> method overloads has changed to include an optional <xref:System.Text.Encodings.Web.JavaScriptEncoder> parameter.</span></span> <span data-ttu-id="2fc05-106">Bu değişiklik, farklı veya özel bir kodlayıcı için izin vermek üzere yapılmıştır.</span><span class="sxs-lookup"><span data-stu-id="2fc05-106">This change was made to allow for a different or custom encoder.</span></span>

<span data-ttu-id="2fc05-107">.NET Core 3,0 Preview `Encode` 7 ' deki yöntemlerin imzası şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2fc05-107">The signature of the `Encode` methods in .NET Core 3.0 Preview 7 is:</span></span>

```csharp
namespace System.Text.Json
{
    public readonly struct JsonEncodedText
    {
        public static JsonEncodedText Encode(ReadOnlySpan<byte> utf8Value);
        public static JsonEncodedText Encode(ReadOnlySpan<char> value);
        public static JsonEncodedText Encode(string value);
    }
}
```

<span data-ttu-id="2fc05-108">.NET Core 3,0 Preview 8 `Encode` ve sonraki sürümlerinde aynı yöntemlerin imzası:</span><span class="sxs-lookup"><span data-stu-id="2fc05-108">The signature of the same `Encode` methods in .NET Core 3.0 Preview 8 and later versions is:</span></span>

```csharp
namespace System.Text.Json
{
    public readonly struct JsonEncodedText
    {
        public static JsonEncodedText Encode(ReadOnlySpan<byte> utf8Value, JavaScriptEncoder encoder = null);
        public static JsonEncodedText Encode(ReadOnlySpan<char> value, JavaScriptEncoder encoder = null);
        public static JsonEncodedText Encode(string value, JavaScriptEncoder encoder = null);
    }
}
```

#### <a name="version-introduced"></a><span data-ttu-id="2fc05-109">Sunulan sürüm</span><span class="sxs-lookup"><span data-stu-id="2fc05-109">Version introduced</span></span>

<span data-ttu-id="2fc05-110">.NET Core 3,0 Preview 8</span><span class="sxs-lookup"><span data-stu-id="2fc05-110">.NET Core 3.0 Preview 8</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="2fc05-111">Önerilen eylem</span><span class="sxs-lookup"><span data-stu-id="2fc05-111">Recommended action</span></span>

<span data-ttu-id="2fc05-112">Bu yalnızca ikili bir son değişiklik. .NET Core 3,0 Preview 8 veya sonraki bir sürüme yönelik yeniden derleme, çalışma zamanı sorunlarını düzeltir.</span><span class="sxs-lookup"><span data-stu-id="2fc05-112">This is a binary breaking change only; a recompile against .NET Core 3.0 Preview 8 or a later version will fix any runtime issues.</span></span>

#### <a name="category"></a><span data-ttu-id="2fc05-113">Kategori</span><span class="sxs-lookup"><span data-stu-id="2fc05-113">Category</span></span>

<span data-ttu-id="2fc05-114">CoreFx</span><span class="sxs-lookup"><span data-stu-id="2fc05-114">CoreFx</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="2fc05-115">Etkilenen API’ler</span><span class="sxs-lookup"><span data-stu-id="2fc05-115">Affected APIs</span></span>

<xref:System.Text.Json.JsonEncodedText.Encode(System.ReadOnlySpan%7BSystem.Byte%7D,System.Text.Encodings.Web.JavaScriptEncoder)?displayProperty=nameWithType>
<xref:System.Text.Json.JsonEncodedText.Encode(System.ReadOnlySpan%7BSystem.Char%7D,System.Text.Encodings.Web.JavaScriptEncoder)?displayProperty=nameWithType>
<xref:System.Text.Json.JsonEncodedText.Encode(System.String,System.Text.Encodings.Web.JavaScriptEncoder)?displayProperty=nameWithType>

<!--

### Affected APIs 

- `M:System.Text.Json.JsonEncodedText.Encode(System.ReadOnlySpan{System.Byte},System.Text.Encodings.Web.JavaScriptEncoder)`
- `M:System.Text.Json.JsonEncodedText.Encode(System.ReadOnlySpan{System.Char},System.Text.Encodings.Web.JavaScriptEncoder)`
- `M:System.Text.Json.JsonEncodedText.Encode(System.String,System.Text.Encodings.Web.JavaScriptEncoder)`

-->