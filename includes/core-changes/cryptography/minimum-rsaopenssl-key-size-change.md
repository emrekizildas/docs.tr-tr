---
ms.openlocfilehash: e3bda3cf6319d8c988b6c897b78869f517f9616a
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182076"
---
### <a name="minimum-size-for-rsaopenssl-key-generation-has-increased"></a><span data-ttu-id="a5aef-101">RSAOpenSsl anahtar üretimi için en düşük boyut arttı</span><span class="sxs-lookup"><span data-stu-id="a5aef-101">Minimum size for RSAOpenSsl key generation has increased</span></span>

<span data-ttu-id="a5aef-102">Linux üzerinde yeni RSA anahtarları oluşturmak için en düşük boyut, 384 bitten 512 bit 'e artmıştır.</span><span class="sxs-lookup"><span data-stu-id="a5aef-102">The minimum size for generating new RSA keys on Linux has increased from 384-bit to 512-bit.</span></span>

#### <a name="change-description"></a><span data-ttu-id="a5aef-103">Açıklamayı Değiştir</span><span class="sxs-lookup"><span data-stu-id="a5aef-103">Change description</span></span>

<span data-ttu-id="a5aef-104">.Net `LegalKeySizes` Core 3,0 ' den <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType>itibaren, Linux üzerinde, <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor%2A?displayProperty=nameWithType>ve <xref:System.Security.Cryptography.RSACryptoServiceProvider.%23ctor%2A?displayProperty=nameWithType> Linux üzerinde RSA örneklerinde özelliği tarafından raporlanan en düşük yasal anahtar boyutu 384 ' den 512 ' ye yükselmiştir.</span><span class="sxs-lookup"><span data-stu-id="a5aef-104">Starting with .NET Core 3.0, the minimum legal key size reported by the `LegalKeySizes` property on RSA instances from <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType>, <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor%2A?displayProperty=nameWithType>, and <xref:System.Security.Cryptography.RSACryptoServiceProvider.%23ctor%2A?displayProperty=nameWithType> on Linux has increased from 384 to 512.</span></span>

<span data-ttu-id="a5aef-105">Sonuç olarak, .NET Core 2,2 ve önceki sürümlerde, gibi bir yöntem çağrısı `RSA.Create(384)` başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="a5aef-105">As a result, in .NET Core 2.2 and earlier versions, a method call such as `RSA.Create(384)` succeeds.</span></span> <span data-ttu-id="a5aef-106">.NET Core 3,0 ve sonraki sürümlerinde Yöntem çağrısı `RSA.Create(384)` , boyutun çok küçük olduğunu belirten bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a5aef-106">In .NET Core 3.0 and later versions, the method call `RSA.Create(384)` throws an exception indicating the size is too small.</span></span>

<span data-ttu-id="a5aef-107">Bu değişiklik, Linux üzerinde şifreleme işlemlerini gerçekleştiren OpenSSL, 1.0.2 ve 1.1.0 sürümleri arasında en düşük bir değer oluşturduğundan yapılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a5aef-107">This change was made because OpenSSL, which performs the cryptographic operations on Linux, raised its minimum between versions 1.0.2 and 1.1.0.</span></span> <span data-ttu-id="a5aef-108">.NET Core 3,0, OpenSSL 1.1. x-1.0. x ' i tercih eder ve bildirilen en düşük sürüm, bu yeni daha yüksek bağımlılık sınırlamasını yansıtacak şekilde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="a5aef-108">.NET Core 3.0 prefers OpenSSL 1.1.x to 1.0.x, and the minimum reported version was raised to reflect this new higher dependency limitation.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="a5aef-109">Sunulan sürüm</span><span class="sxs-lookup"><span data-stu-id="a5aef-109">Version introduced</span></span>

<span data-ttu-id="a5aef-110">3.0</span><span class="sxs-lookup"><span data-stu-id="a5aef-110">3.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="a5aef-111">Önerilen eylem</span><span class="sxs-lookup"><span data-stu-id="a5aef-111">Recommended action</span></span>

<span data-ttu-id="a5aef-112">Etkilenen API 'lerden herhangi birini çağırırsanız, oluşturulan anahtarların boyutunun en düşük sağlayıcıdan daha az olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a5aef-112">If you call any of the affected APIs, ensure that the size of any generated keys is not less than the provider minimum.</span></span>

> [!NOTE]
> <span data-ttu-id="a5aef-113">384-bit RSA zaten güvenli değil (512 bit RSA olarak).</span><span class="sxs-lookup"><span data-stu-id="a5aef-113">384-bit RSA is already considered insecure (as is 512-bit RSA).</span></span> <span data-ttu-id="a5aef-114">[NIST özel yayını 800-57 1. Bölüm düzeltme 4](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf)gibi modern öneriler, yeni oluşturulan anahtarlar için en düşük boyut olarak 2048 bit önerilir.</span><span class="sxs-lookup"><span data-stu-id="a5aef-114">Modern recommendations, such as [NIST Special Publication 800-57 Part 1 Revision 4](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf), suggest 2048-bit as the minimum size for newly generated keys.</span></span>

#### <a name="category"></a><span data-ttu-id="a5aef-115">Kategori</span><span class="sxs-lookup"><span data-stu-id="a5aef-115">Category</span></span>

<span data-ttu-id="a5aef-116">To</span><span class="sxs-lookup"><span data-stu-id="a5aef-116">Cryptography</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="a5aef-117">Etkilenen API’ler</span><span class="sxs-lookup"><span data-stu-id="a5aef-117">Affected APIs</span></span>

- <xref:System.Security.Cryptography.AsymmetricAlgorithm.LegalKeySizes?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor%2A?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSACryptoServiceProvider.%23ctor%2A?displayProperty=nameWithType>

<!--
### Affected APIs

- `P:System.Security.Cryptography.AsymmetricAlgorithm.LegalKeySizes`
- `Overload:System.Security.Cryptography.RSA.Create`
- `Overload:System.Security.Cryptography.RSAOpenSsl.#ctor`
- `Overload:System.Security.Cryptography.RSACryptoServiceProvider.#ctor`


-->