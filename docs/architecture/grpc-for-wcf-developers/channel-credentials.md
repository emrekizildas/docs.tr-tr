---
title: Kanal kimlik bilgileri-WCF geliştiricileri için gRPC
description: ASP.NET Core 3,0 ' de gRPC kanal kimlik bilgilerini uygulama ve kullanma.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 61305ee47a2c09a0b2a0fd866beb9b7c102ffeaa
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184584"
---
# <a name="channel-credentials"></a><span data-ttu-id="c6c9a-103">Kanal kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="c6c9a-103">Channel credentials</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="c6c9a-104">Adından da anlaşılacağı gibi kanal kimlik bilgileri, temeldeki gRPC kanalına eklenir.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-104">As the name implies, channel credentials are attached to the underlying gRPC channel.</span></span> <span data-ttu-id="c6c9a-105">Kanal kimlik bilgileri standart biçimi istemci sertifikası kimlik doğrulamasını kullanır, burada istemci, bağlantı kurulurken bir TLS sertifikası sağlar ve herhangi bir çağrının yapılmasına izin vermeden önce sunucu tarafından doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-105">The standard form of channel credentials uses Client Certificate authentication, where the client provides a TLS certificate when it's making the connection, which is verified by the server before allowing any calls to be made.</span></span>

<span data-ttu-id="c6c9a-106">GRPC hizmeti için kapsamlı güvenlik sağlamak amacıyla kanal kimlik bilgileri, çağrı kimlik bilgileriyle birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-106">Channel credentials can be combined with call credentials to provide comprehensive security for a gRPC service.</span></span> <span data-ttu-id="c6c9a-107">Kanal kimlik bilgileri, istemci uygulamanın hizmete erişmesine izin verildiğini kanıtlayın ve çağrı kimlik bilgileri, istemci uygulamasını kullanan kişi hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-107">The channel credentials prove that the client application is allowed to access the service, and the call credentials provide information about the person using the client application.</span></span>

<span data-ttu-id="c6c9a-108">İstemci sertifikası kimlik doğrulaması, gRPC için ASP.NET Core çalıştığı şekilde çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-108">Client certificate authentication works for gRPC the same way it works for ASP.NET Core.</span></span> <span data-ttu-id="c6c9a-109">Yapılandırma işlemi burada özetlenmiştir, ancak [ASP.NET Core 'de sertifika kimlik doğrulamasını yapılandırma](https://docs.microsoft.com/aspnet/core/security/authentication/certauth?view=aspnetcore-3.0) makalesinde daha fazla bilgi bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-109">The configuration process will be summarized here, but more information is available in the [Configure certificate authentication in ASP.NET Core](https://docs.microsoft.com/aspnet/core/security/authentication/certauth?view=aspnetcore-3.0) article.</span></span>

<span data-ttu-id="c6c9a-110">Geliştirme amacıyla kendinden imzalı bir sertifika kullanabilirsiniz, ancak üretim için güvenilen bir yetkili tarafından imzalanmış uygun bir HTTPS sertifikası kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-110">For development purposes you can use a self-signed certificate, but for production you should use a proper HTTPS certificate signed by a trusted authority.</span></span>

## <a name="adding-certificate-authentication-to-the-server"></a><span data-ttu-id="c6c9a-111">Sunucuya sertifika kimlik doğrulaması ekleniyor</span><span class="sxs-lookup"><span data-stu-id="c6c9a-111">Adding certificate authentication to the server</span></span>

<span data-ttu-id="c6c9a-112">Sertifika kimlik doğrulamasını hem ana bilgisayar düzeyinde (örneğin, Kestrel sunucusu hem de ASP.NET Core işlem hattında yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-112">You need to configure certificate authentication both at the host level, for example on the Kestrel server, and in the ASP.NET Core pipeline.</span></span>

### <a name="configuring-certificate-validation-on-kestrel"></a><span data-ttu-id="c6c9a-113">Kestrel 'de sertifika doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c6c9a-113">Configuring certificate validation on Kestrel</span></span>

<span data-ttu-id="c6c9a-114">Kestrel (ASP.NET Core HTTP sunucusu) bir istemci sertifikası gerektirecek şekilde yapılandırabilir ve isteğe bağlı olarak, gelen bağlantıları kabul etmeden önce sağlanan sertifikanın bazı doğrulanmasını gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-114">You can configure Kestrel (the ASP.NET Core HTTP server) to require a client certificate, and optionally to carry out some validation of the supplied certificate before accepting incoming connections.</span></span> <span data-ttu-id="c6c9a-115">Bu yapılandırma, içindeki `CreateWebHostBuilder` `Startup`yerine, `Program` sınıfının yönteminde yapılır.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-115">This configuration is done in the `CreateWebHostBuilder` method of the `Program` class, rather than in `Startup`.</span></span>

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureWebHostDefaults(webBuilder =>
        {
            var serverCert = ObtainServerCertificate();
            webBuilder.UseStartup<Startup>()
                .ConfigureKestrel(kestrelServerOptions => {
                    kestrelServerOptions.ConfigureHttpsDefaults(opt =>
                    {
                        opt.ClientCertificateMode = ClientCertificateMode.RequireCertificate;

                        // Verify that client certificate was issued by same CA as server certificate
                        opt.ClientCertificateValidation = (certificate, chain, errors) =>
                            certificate.Issuer == serverCert.Issuer;
                    });
                });
        });

```

<span data-ttu-id="c6c9a-116">Ayar `ClientCertificateMode.RequireCertificate` , Kestrel istemci sertifikası sağlamayan tüm bağlantı isteklerini hemen reddetmesine neden olur, ancak sertifika doğrulanmaz.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-116">The `ClientCertificateMode.RequireCertificate` setting will cause Kestrel to immediately reject any connection request that doesn't provide a client certificate, but it won't validate the certificate.</span></span> <span data-ttu-id="c6c9a-117">Geri çağırma eklemek, Kestrel 'in istemci sertifikasını (Bu durumda sunucu sertifikasıyla aynı *sertifika yetkilisi* tarafından verildiğini güvence altına almak), bağlantının oluşturulduğu noktada, ASP.NET Core `ClientCertificateValidation` işlem hattı bağlı.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-117">Adding the `ClientCertificateValidation` callback enables Kestrel to validate the client certificate (in this case, ensuring that it was issued by the same *Certificate Authority* as the server certificate) at the point the connection is made, before the ASP.NET Core pipeline is engaged.</span></span>

### <a name="adding-aspnet-core-certificate-authentication"></a><span data-ttu-id="c6c9a-118">ASP.NET Core sertifikası kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="c6c9a-118">Adding ASP.NET Core certificate authentication</span></span>

<span data-ttu-id="c6c9a-119">Sertifika kimlik doğrulaması [Microsoft. AspNetCore. Authentication. Certificate](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Certificate) NuGet paketi tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-119">Certificate authentication is provided by the [Microsoft.AspNetCore.Authentication.Certificate](https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.Certificate) NuGet package.</span></span>

<span data-ttu-id="c6c9a-120">`ConfigureServices` Yöntemine sertifika kimlik doğrulama hizmetini ekleyin ve `Configure` yöntemdeki ASP.NET Core işlem hattına kimlik doğrulaması ve yetkilendirme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-120">Add the certificate authentication service in the `ConfigureServices` method, and add authentication and authorization to the ASP.NET Core pipeline in the `Configure` method.</span></span>

```csharp
public class Startup
{
    private readonly bool _isDevelopment;

    public Startup(IWebHostEnvironment env)
    {
        _isDevelopment = env.IsDevelopment();
    }

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddAuthentication(CertificateAuthenticationDefaults.AuthenticationScheme)
            .AddCertificate(options =>
            {
                if (_isDevelopment)
                {
                    // DO NOT DO THIS IN PRODUCTION!
                    options.RevocationMode = X509RevocationMode.NoCheck;
                }
            });
        services.AddAuthorization();
        services.AddGrpc();
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        app.UseRouting();

        app.UseAuthentication();
        app.UseAuthorization();

        app.UseEndpoints(endpoints => { endpoints.MapGrpcService<GreeterService>(); });
    }
}
```

## <a name="providing-channel-credentials-in-the-client-application"></a><span data-ttu-id="c6c9a-121">İstemci uygulamasında kanal kimlik bilgilerini sağlama</span><span class="sxs-lookup"><span data-stu-id="c6c9a-121">Providing channel credentials in the client application</span></span>

<span data-ttu-id="c6c9a-122">Paketiyle, sertifikalar, bağlantı için `GrpcChannel` kullanılan bir <xref:System.Net.Http.HttpClient> örnek üzerinde yapılandırılır. `Grpc.Net.Client`</span><span class="sxs-lookup"><span data-stu-id="c6c9a-122">With the `Grpc.Net.Client` package, certificates are configured on an <xref:System.Net.Http.HttpClient> instance that is provided to the `GrpcChannel` used for the connection.</span></span>

```csharp
class Program
{
    static async Task Main(string[] args)
    {
        // Assume path to a client .pfx file and password are passed from command line
        // On Windows this would probably be a reference to the Certificate Store
        var cert = new X509Certificate2(args[0], args[1]);

        var handler = new HttpClientHandler();
        handler.ClientCertificates.Add(cert);
        var httpClient = new HttpClient(handler);

        var channel = GrpcChannel.ForAddress("https://localhost:5001/", new GrpcChannelOptions
        {
            HttpClient = httpClient
        });

        var grpc = new Greeter.GreeterClient(channel);
        var response = await grpc.SayHelloAsync(new HelloRequest { Name = "Bob" });
        System.Console.WriteLine(response.Message);
    }
}
```

## <a name="combining-channelcredentials-and-callcredentials"></a><span data-ttu-id="c6c9a-123">ChannelCredentials ve CallCredentials birleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="c6c9a-123">Combining ChannelCredentials and CallCredentials</span></span>

<span data-ttu-id="c6c9a-124">Kestrel sunucusuna sertifika değişiklikleri uygulayarak ve ASP.NET Core içindeki JWT taşıyıcı ara yazılımını kullanarak sunucunuzu hem sertifika hem de belirteç kimlik doğrulamasını kullanacak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-124">You can configure your server to use both certificate and token authentication by applying the certificate changes to the Kestrel server and using the JWT bearer middleware in ASP.NET Core.</span></span>

<span data-ttu-id="c6c9a-125">İstemcide hem channelcredentials hem de callcredentials sağlamak için, çağrı kimlik bilgilerini `ChannelCredentials.Create` uygulamak için yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-125">To provide both ChannelCredentials and CallCredentials on the client, use the `ChannelCredentials.Create` method to apply the call credentials.</span></span> <span data-ttu-id="c6c9a-126">Sertifika kimlik doğrulamasının hala <xref:System.Net.Http.HttpClient> örnek kullanılarak uygulanması gerekir: `SslCredentials` oluşturucuya herhangi bir bağımsız değişken geçirirseniz, iç istemci kodu bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-126">Certificate authentication still needs to be applied using the <xref:System.Net.Http.HttpClient> instance: if you pass any arguments to the `SslCredentials` constructor, the internal client code throws an exception.</span></span> <span data-ttu-id="c6c9a-127">Parametresi, paketiyleuyumluluğu`Grpc.Core` sürdürmek için yalnızca `Grpc.Net.Client` paketin `Create` yöntemine dahil edilmiştir. `SslCredentials`</span><span class="sxs-lookup"><span data-stu-id="c6c9a-127">The `SslCredentials` parameter is only included in the `Grpc.Net.Client` package's `Create` method to maintain compatibility with the `Grpc.Core` package.</span></span>

```csharp
var handler = new HttpClientHandler();
handler.ClientCertificates.Add(cert);

var httpClient = new HttpClient(handler);

var callCredentials = CallCredentials.FromInterceptor(((context, metadata) =>
    {
        metadata.Add("Authorization", $"Bearer {_token}");
    }));

var channelCredentials = ChannelCredentials.Create(new SslCredentials(), callCredentials);

var channel = GrpcChannel.ForAddress("https://localhost:5001/", new GrpcChannelOptions
{
    HttpClient = httpClient,
    Credentials = channelCredentials
});

var grpc = new Portfolios.PortfoliosClient(channel);
```

> [!TIP]
> <span data-ttu-id="c6c9a-128">Belirteç kimlik bilgilerini kanalda `ChannelCredentials.Create` yapılan her çağrıya geçirmek için kullanışlı bir yol olarak sertifika kimlik doğrulaması olmadan bir istemci için yöntemini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-128">You can use the `ChannelCredentials.Create` method for a client without certificate authentication, as a useful way to pass token credentials with every call made on the channel.</span></span>

<span data-ttu-id="c6c9a-129">[FullStockTicker örnek gRPC uygulamasının sertifika kimlik doğrulaması eklenmiş](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/FullStockTickerSample/grpc/FullStockTickerAuth/FullStockTicker) bir sürümü GitHub üzerinde.</span><span class="sxs-lookup"><span data-stu-id="c6c9a-129">A version of the [FullStockTicker sample gRPC application with certificate authentication added](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/FullStockTickerSample/grpc/FullStockTickerAuth/FullStockTicker) is on GitHub.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="c6c9a-130">[Önceki](call-credentials.md)
>[İleri](encryption.md)</span><span class="sxs-lookup"><span data-stu-id="c6c9a-130">[Previous](call-credentials.md)
[Next](encryption.md)</span></span>