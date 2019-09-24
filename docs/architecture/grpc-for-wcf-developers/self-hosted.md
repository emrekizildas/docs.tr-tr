---
title: Self-hosted gRPC uygulamaları-WCF geliştiricileri için gRPC
description: ASP.NET Core gRPC uygulamalarını self-hosted Hizmetleri olarak dağıtma.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 1269137b58f4d25f407a6a04327c51bc9f069c1b
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184108"
---
# <a name="self-hosted-grpc-applications"></a><span data-ttu-id="5994f-103">Şirket içinde barındırılan gRPC uygulamaları</span><span class="sxs-lookup"><span data-stu-id="5994f-103">Self-hosted gRPC applications</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="5994f-104">ASP.NET Core 3,0 uygulamaları Windows Server 'da IIS 'de barındırılamasa da, HTTP/2 işlevselliğinin bazıları henüz desteklenmediğinden, şu anda IIS 'de bir gRPC uygulaması barındırılamaz.</span><span class="sxs-lookup"><span data-stu-id="5994f-104">Although ASP.NET Core 3.0 applications can be hosted in IIS on Windows Server, currently it isn't possible to host a gRPC application in IIS because some of the HTTP/2 functionality isn't yet supported.</span></span> <span data-ttu-id="5994f-105">Bu işlevsellik, gelecekteki bir Windows Server güncelleştirmesinde beklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="5994f-105">This functionality is expected in a future update to Windows Server.</span></span>

<span data-ttu-id="5994f-106">.NET Core 3,0 barındırma uzantılarında bazı yeni özellikler sayesinde uygulamanızı Windows hizmeti olarak veya [systemd](https://en.wikipedia.org/wiki/Systemd)tarafından denetlenen bir Linux hizmeti olarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5994f-106">You can run your application as a Windows Service, or as a Linux service controlled by [systemd](https://en.wikipedia.org/wiki/Systemd), thanks to some new features in the .NET Core 3.0 hosting extensions.</span></span>

## <a name="run-your-app-as-a-windows-service"></a><span data-ttu-id="5994f-107">Uygulamanızı bir Windows hizmeti olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5994f-107">Run your app as a Windows service</span></span>

<span data-ttu-id="5994f-108">ASP.NET Core uygulamanızı bir Windows hizmeti olarak çalışacak şekilde yapılandırmak için, NuGet 'den [Microsoft. Extensions. Hosting. WindowsServices](https://www.nuget.org/packages/Microsoft.Extensions.Hosting.WindowsServices) paketini yüklersiniz.</span><span class="sxs-lookup"><span data-stu-id="5994f-108">To configure your ASP.NET Core application to run as a Windows service, install the [Microsoft.Extensions.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.Extensions.Hosting.WindowsServices) package from NuGet.</span></span> <span data-ttu-id="5994f-109">Sonra ' de `UseWindowsService` `CreateHostBuilder` yönteminebirçağrıekleyin`Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="5994f-109">Then add a call to `UseWindowsService` to the `CreateHostBuilder` method in `Program.cs`.</span></span>

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .UseWindowsService() // Enable running as a Windows service
        .ConfigureWebHostDefaults(webBuilder =>
        {
            webBuilder.UseStartup<Startup>();
        });
```

> [!NOTE]
> <span data-ttu-id="5994f-110">Uygulama bir Windows hizmeti olarak çalışmıyorsa, `UseWindowsService` yöntem hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="5994f-110">If the application isn't running as a Windows service, the `UseWindowsService` method doesn't do anything.</span></span>

<span data-ttu-id="5994f-111">Şimdi, Visual Studio 'dan projeye sağ tıklayıp bağlam menüsünden *Yayımla* ' yı seçerek veya .NET Core CLI uygulamanızı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="5994f-111">Now publish your application, either from Visual Studio by right-clicking the project and choosing *Publish* from the context menu, or from the .NET Core CLI.</span></span>

<span data-ttu-id="5994f-112">Bir .NET Core uygulaması yayımladığınızda, *çerçeveye bağımlı* bir dağıtım veya *kendi kendine dahil* edilen bir dağıtım oluşturmayı tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5994f-112">When you publish a .NET Core application, you can choose to create a *framework-dependent* deployment or a *self-contained* deployment.</span></span> <span data-ttu-id="5994f-113">Çerçeveye bağımlı dağıtımlar, çalıştırıldıkları konakta .NET Core paylaşılan çalışma zamanının yüklenmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5994f-113">Framework-dependent deployments require the .NET Core Shared Runtime to be installed on the host where they are run.</span></span> <span data-ttu-id="5994f-114">Kendi içindeki dağıtımlar, .NET Core çalışma zamanının ve çerçevesinin tam kopyasıyla yayımlanır ve herhangi bir konakta çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5994f-114">Self-contained deployments are published with a complete copy of the .NET Core runtime and framework and can be run on any host.</span></span> <span data-ttu-id="5994f-115">Her yaklaşımın avantajları ve dezavantajları dahil daha fazla bilgi için [.NET Core uygulama dağıtım](https://docs.microsoft.com/dotnet/core/deploying/) belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="5994f-115">For more information, including the advantages and disadvantages of each approach, refer to the [.NET Core application deployment](https://docs.microsoft.com/dotnet/core/deploying/) documentation.</span></span>

<span data-ttu-id="5994f-116">.NET Core 3,0 çalışma zamanının konakta yüklü olmasını gerektirmeyen uygulamanın kendi kendine dahil edilmiş bir derlemesini yayımlamak için, `-r` (veya `--runtime`) bayrağını kullanarak uygulamaya dahil edilecek çalışma zamanını belirtin.</span><span class="sxs-lookup"><span data-stu-id="5994f-116">To publish a self-contained build of the application that does not require the .NET Core 3.0 runtime to be installed on the host, specify the runtime to be included with the application using the `-r` (or `--runtime`) flag.</span></span>

```console
dotnet publish -c Release -r win-x64 -o ./publish
```

<span data-ttu-id="5994f-117">Çerçeveye bağımlı bir yapı yayımlamak için `-r` bayrağını atlayın.</span><span class="sxs-lookup"><span data-stu-id="5994f-117">To publish a framework-dependent build, omit the `-r` flag.</span></span>

```console
dotnet publish -c Release -o ./publish
```

<span data-ttu-id="5994f-118">`publish` Dizinin tüm içeriğini bir yükleme klasörüne kopyalayın ve bir yürütülebilir dosya için Windows hizmeti oluşturmak üzere [sc yardımcı programını](https://docs.microsoft.com/windows/desktop/services/controlling-a-service-using-sc) kullanın.</span><span class="sxs-lookup"><span data-stu-id="5994f-118">Copy the complete contents of the `publish` directory to an installation folder, and use the [sc utility](https://docs.microsoft.com/windows/desktop/services/controlling-a-service-using-sc) to create a Windows service for the executable.</span></span>

```console
sc create MyService binPath=C:\MyService\MyService.exe
```

### <a name="log-to-windows-event-log"></a><span data-ttu-id="5994f-119">Windows olay günlüğü 'ne Kaydet</span><span class="sxs-lookup"><span data-stu-id="5994f-119">Log to Windows Event Log</span></span>

<span data-ttu-id="5994f-120">Yöntemi `UseWindowsService` , Windows olay günlüğüne günlük iletilerini yazan bir [günlüğe kaydetme](https://docs.microsoft.com/aspnet/core/fundamentals/logging/?view=aspnetcore-3.0) sağlayıcısını otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="5994f-120">The `UseWindowsService` method automatically adds a [Logging](https://docs.microsoft.com/aspnet/core/fundamentals/logging/?view=aspnetcore-3.0) provider that writes log messages to the Windows Event Log.</span></span> <span data-ttu-id="5994f-121">Veya diğer yapılandırma kaynağı `EventLog` `Logging` bölümüne bir giriş ekleyerek bu sağlayıcının günlüğünü yapılandırabilirsiniz. `appsettings.json`</span><span class="sxs-lookup"><span data-stu-id="5994f-121">You can configure logging for this provider by adding an `EventLog` entry to the `Logging` section of `appsettings.json` or other configuration source.</span></span> <span data-ttu-id="5994f-122">Olay günlüğünde kullanılan kaynak adı, bu ayarlarda bir `SourceName` özellik ayarlanarak geçersiz kılınabilir; bir ad belirtmezseniz, varsayılan uygulama adı (normalde yürütülebilir derleme adı) kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="5994f-122">The source name used in Event Log can be overridden by setting a `SourceName` property in these settings; if you don't specify a name, the default application name (normally the executable assembly name) will be used.</span></span>

<span data-ttu-id="5994f-123">Günlüğe kaydetme hakkında daha fazla bilgi bu bölümün sonunda yer alır.</span><span class="sxs-lookup"><span data-stu-id="5994f-123">More information on logging is at the end of this chapter.</span></span>

## <a name="run-your-app-as-a-linux-service-with-systemd"></a><span data-ttu-id="5994f-124">Uygulamanızı systemd ile Linux hizmeti olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5994f-124">Run your app as a Linux service with systemd</span></span>

<span data-ttu-id="5994f-125">ASP.NET Core uygulamanızı bir Linux hizmeti olarak çalışacak şekilde yapılandırmak için (veya Linux paranın *arka plan programı* ), NuGet 'den [Microsoft. Extensions. Hosting. systemd](https://www.nuget.org/packages/Microsoft.Extensions.Hosting.Systemd) paketini yüklersiniz.</span><span class="sxs-lookup"><span data-stu-id="5994f-125">To configure your ASP.NET Core application to run as a Linux service (or *daemon* in Linux parlance), install the [Microsoft.Extensions.Hosting.Systemd](https://www.nuget.org/packages/Microsoft.Extensions.Hosting.Systemd) package from NuGet.</span></span> <span data-ttu-id="5994f-126">Sonra ' de `UseSystemd` `CreateHostBuilder` yönteminebirçağrıekleyin`Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="5994f-126">Then add a call to `UseSystemd` to the `CreateHostBuilder` method in `Program.cs`.</span></span>

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .UseSystemd() // Enable running as a Systemd service
        .ConfigureWebHostDefaults(webBuilder =>
        {
            webBuilder.UseStartup<Startup>();
        });
```

> [!NOTE]
> <span data-ttu-id="5994f-127">Uygulama bir Linux hizmeti olarak çalışmıyorsa, `UseSystemd` yöntem hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="5994f-127">If the application isn't running as a Linux service, the `UseSystemd` method doesn't do anything.</span></span>

<span data-ttu-id="5994f-128">Şimdi, Visual Studio 'dan projeye sağ tıklayıp bağlam menüsünden *Yayımla* ' yı seçerek veya .net ' den, uygulamanızı (Framework `linux-x64`'e bağımlı veya ilgili Linux çalışma zamanı için bağımsız) yayımlayın. Aşağıdaki komutu kullanarak çekirdek CLı.</span><span class="sxs-lookup"><span data-stu-id="5994f-128">Now publish your application (either framework-dependent, or self-contained for the relevant Linux runtime, e.g. `linux-x64`), either from Visual Studio by right-clicking the project and choosing *Publish* from the context menu, or from the .NET Core CLI using the following command.</span></span>

```console
dotnet publish -c Release -r linux-x64 -o ./publish
```

<span data-ttu-id="5994f-129">`publish` Dizinin tüm içeriğini Linux ana bilgisayarındaki bir yükleme klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5994f-129">Copy the complete contents of the `publish` directory to an installation folder on the Linux host.</span></span> <span data-ttu-id="5994f-130">Hizmeti kaydettirmek, `/etc/systemd/system` dizine eklenmek üzere "birim dosyası" olarak adlandırılan özel bir dosya gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5994f-130">Registering the service requires a special file, called a "unit file", to be added to the `/etc/systemd/system` directory.</span></span> <span data-ttu-id="5994f-131">Bu klasörde bir dosya oluşturmak için kök izninizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5994f-131">You'll need root permission to create a file in this folder.</span></span> <span data-ttu-id="5994f-132">Dosyayı kullanmak istediğiniz tanımlayıcıya `systemd` `.service` ve uzantıyı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="5994f-132">Name the file with the identifier you want `systemd` to use and the `.service` extension.</span></span> <span data-ttu-id="5994f-133">Örneğin, uygulamasında yönetilen Hyper-V konakları olarak eklemek için aşağıdaki yordamı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5994f-133">For example, `/etc/systemd/system/myapp.service`.</span></span>

<span data-ttu-id="5994f-134">Hizmet dosyası, bu örnekte gösterildiği gibi ıNı biçimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="5994f-134">The service file uses INI format, as shown in this example.</span></span>

```ini
[Unit]
Description=My gRPC Application

[Service]
Type=notify
ExecStart=/usr/sbin/myapp

[Install]
WantedBy=multi-user.target
```

<span data-ttu-id="5994f-135">Özelliği, uygulamanın bu uygulamayı başlatma ve kapatmayla bilgilendirmeyeceğini söyler `systemd`. `Type=notify`</span><span class="sxs-lookup"><span data-stu-id="5994f-135">The `Type=notify` property tells `systemd` that the application will notify it on startup and shutdown.</span></span> <span data-ttu-id="5994f-136">Bu `WantedBy=multi-user.target` ayar, Linux sistemi "Runlevel 2" değerine ulaştığında hizmetin başlatılmasına neden olur, yani grafik olmayan bir çok kullanıcılı kabuk etkin olur.</span><span class="sxs-lookup"><span data-stu-id="5994f-136">The `WantedBy=multi-user.target` setting will cause the service to start when the Linux system reaches "runlevel 2", meaning a non-graphical multi-user shell is active.</span></span>

<span data-ttu-id="5994f-137">Hizmeti `systemd` tanıyamadan önce, yapılandırmasını yeniden yüklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5994f-137">Before `systemd` will recognize the service, it needs to reload its configuration.</span></span> <span data-ttu-id="5994f-138">Komutunu kullanarak kontrol `systemd`edersiniz. `systemctl`</span><span class="sxs-lookup"><span data-stu-id="5994f-138">You control `systemd` using the `systemctl` command.</span></span> <span data-ttu-id="5994f-139">Yeniden yükledikten sonra, uygulamanın `status` başarıyla kaydedildiğini doğrulamak için alt komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5994f-139">After reloading, use the `status` subcommand to confirm the application has registered successfully.</span></span>

```console
sudo systemctl daemon-reload
sudo systemctl status myapp
```

<span data-ttu-id="5994f-140">Hizmeti doğru şekilde yapılandırdıysanız aşağıdaki çıktı gösterilir:</span><span class="sxs-lookup"><span data-stu-id="5994f-140">If you've configured the service correctly, the following output will be shown:</span></span>

```text
myapp.service - My gRPC Application
 Loaded: loaded (/etc/systemd/system/myapp.service; disabled; vendor preset: enabled)
 Active: inactive (dead)
```

<span data-ttu-id="5994f-141">Hizmeti başlatmak için komutunu kullanın. `start`</span><span class="sxs-lookup"><span data-stu-id="5994f-141">Use the `start` command to start the service.</span></span>

```console
sudo systemctl start myapp.service
```

> [!TIP]
> <span data-ttu-id="5994f-142">Uzantı `.service` , kullanılırken `systemctl start`isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5994f-142">The `.service` extension is optional when using `systemctl start`.</span></span>

<span data-ttu-id="5994f-143">Hizmeti sistem `systemd` başlangıcında otomatik olarak başlatmaya söylemek için `enable` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5994f-143">To tell `systemd` to start the service automatically on system startup, use the `enable` command.</span></span>

```console
sudo systemctl enable myapp
```

### <a name="log-to-journald"></a><span data-ttu-id="5994f-144">Journald 'de günlüğe kaydet</span><span class="sxs-lookup"><span data-stu-id="5994f-144">Log to journald</span></span>

<span data-ttu-id="5994f-145">Windows olay günlüğü `journald`'nün Linux eşdeğeri, bir `systemd`parçası olan yapılandırılmış bir günlük sistem hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="5994f-145">The Linux equivalent of the Windows Event Log is `journald`, a structured logging system service that is part of `systemd`.</span></span> <span data-ttu-id="5994f-146">Bir Linux Daemon tarafından standart çıktıya yazılan günlük iletileri otomatik olarak öğesine `journald`yazılır, bu nedenle günlüğe kaydetme düzeylerini yapılandırmak için günlük yapılandırmasının `Console` bölümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="5994f-146">Log messages written to the standard output by a Linux daemon are automatically written to `journald`, so to configure logging levels, use the `Console` section of the logging configuration.</span></span> <span data-ttu-id="5994f-147">`UseSystemd` Konak Oluşturucu yöntemi, konsol çıkış biçimini otomatik olarak günlüğe uyacak şekilde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5994f-147">The `UseSystemd` host builder method automatically configures the console output format to suit the journal.</span></span>

<span data-ttu-id="5994f-148">, Linux günlükleri için standart olduğundan, bununla tümleştirilen çeşitli araçlar vardır ve `journald` günlükleri bir dış günlük sistemine kolayca yönlendirebilirsiniz. `journald`</span><span class="sxs-lookup"><span data-stu-id="5994f-148">Because `journald` is the standard for Linux logs, there are a variety of tools that integrate with it, and you can easily route logs from `journald` to an external logging system.</span></span> <span data-ttu-id="5994f-149">Yerel olarak konakta çalışırken komut satırından günlükleri görüntülemek için `journalctl` komutunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5994f-149">Working locally on the host, you can use the `journalctl` command to view logs from the command line.</span></span>

```console
sudo journalctl -u myapp
```

> [!TIP]
> <span data-ttu-id="5994f-150">Ana bilgisayarınızda kullanılabilir bir GUI ortamınız varsa, Linux için *Qjournalctl* ve *GNOME günlükleri*gibi birkaç grafik günlük görüntüleyicileri vardır.</span><span class="sxs-lookup"><span data-stu-id="5994f-150">If you have a GUI environment available on your host, a few graphical log viewers are available for Linux, such as *QJournalctl* and *gnome-logs*.</span></span>

<span data-ttu-id="5994f-151">İle `journalctl`komut satırından systemd günlüğünü sorgulama hakkında daha fazla bilgi edinmek için, [Man sayfalarına](https://manpages.debian.org/buster/systemd/journalctl.1)bakın.</span><span class="sxs-lookup"><span data-stu-id="5994f-151">To learn more about querying the systemd journal from the command line with `journalctl`, see [the man pages](https://manpages.debian.org/buster/systemd/journalctl.1).</span></span>

## <a name="https-certificates-for-self-hosted-applications"></a><span data-ttu-id="5994f-152">Şirket içinde barındırılan uygulamalar için HTTPS sertifikaları</span><span class="sxs-lookup"><span data-stu-id="5994f-152">HTTPS Certificates for self-hosted applications</span></span>

<span data-ttu-id="5994f-153">Bir gRPC uygulamasını üretimde çalıştırırken, güvenilir bir sertifika yetkilisinden (CA) bir TLS sertifikası kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5994f-153">When running a gRPC application in production, you should use a TLS certificate from a trusted Certificate Authority (CA).</span></span> <span data-ttu-id="5994f-154">Bu CA, genel bir CA veya kuruluşunuz için bir dahili olabilir.</span><span class="sxs-lookup"><span data-stu-id="5994f-154">This CA could be a public CA, or an internal one for your organization.</span></span>

<span data-ttu-id="5994f-155">Windows konakları üzerinde, sertifika, [X509Store sınıfı](https://docs.microsoft.com/dotnet/api/system.security.cryptography.x509certificates.x509store?view=netcore-3.0)kullanılarak güvenli bir [sertifika deposundan](https://docs.microsoft.com/windows/win32/seccrypto/managing-certificates-with-certificate-stores) yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5994f-155">On Windows hosts, the certificate may be loaded from a secure [Certificate Store](https://docs.microsoft.com/windows/win32/seccrypto/managing-certificates-with-certificate-stores) using the [X509Store class](https://docs.microsoft.com/dotnet/api/system.security.cryptography.x509certificates.x509store?view=netcore-3.0).</span></span> <span data-ttu-id="5994f-156">`X509Store` Sınıfı, bazı Linux konaklarındaki OpenSSL anahtar deposu ile de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5994f-156">The `X509Store` class can also be used with the OpenSSL key-store on some Linux hosts.</span></span>

<span data-ttu-id="5994f-157">Sertifikalar, bir dosyadan ( [Örneğin, güçlü](https://docs.microsoft.com/dotnet/api/system.security.cryptography.x509certificates.x509certificate.-ctor?view=netcore-3.0)bir parolayla korunan bir `.pfx` dosya) veya Azure Key Vault gibi güvenli bir depolama hizmetinden alınan ikili verilerden biri kullanılarak da oluşturulabilir. [ ](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="5994f-157">Certificates may also be created using one of the [X509Certificate2 constructors](https://docs.microsoft.com/dotnet/api/system.security.cryptography.x509certificates.x509certificate.-ctor?view=netcore-3.0), either from a file (for example a `.pfx` file protected by a strong password), or from binary data retrieved from a secure storage service such as [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span></span>

<span data-ttu-id="5994f-158">Kestrel, bir sertifikayı iki şekilde kullanacak şekilde yapılandırılabilir: yapılandırmadan veya kodda.</span><span class="sxs-lookup"><span data-stu-id="5994f-158">Kestrel can be configured to use a certificate in two ways: from configuration, or in code.</span></span>

### <a name="set-https-certificates-using-configuration"></a><span data-ttu-id="5994f-159">Yapılandırma kullanarak HTTPS sertifikaları ayarlama</span><span class="sxs-lookup"><span data-stu-id="5994f-159">Set HTTPS certificates using configuration</span></span>

<span data-ttu-id="5994f-160">Yapılandırma yaklaşımı, Kestrel yapılandırma bölümünde sertifika `.pfx` dosyası yolunu ve parolayı ayarlamayı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5994f-160">The configuration approach requires setting the path to the certificate `.pfx` file and the password in the Kestrel configuration section.</span></span> <span data-ttu-id="5994f-161">Bu `appsettings.json` , içinde olduğu gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="5994f-161">In `appsettings.json` that would look like this.</span></span>

```json
{
  "Kestrel": {
    "Certificates": {
      "Default": {
        "Path": "cert.pfx",
        "Password": "DO NOT STORE PLAINTEXT PASSWORDS IN APPSETTINGS FILES"
      }
    }
  }
}
```

<span data-ttu-id="5994f-162">Parolanın Azure Keykasası veya HashiCorp kasası gibi güvenli bir yapılandırma kaynağı kullanılarak sağlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5994f-162">The password should be provided using a secure configuration source such as Azure KeyVault or Hashicorp Vault.</span></span>

<span data-ttu-id="5994f-163">Şifrelenmemiş parolaları yapılandırma dosyalarında depolamamalısınız.</span><span class="sxs-lookup"><span data-stu-id="5994f-163">You SHOULD NOT store unencrypted passwords in configuration files.</span></span>

### <a name="set-https-certificates-in-code"></a><span data-ttu-id="5994f-164">Kodda HTTPS sertifikaları ayarlama</span><span class="sxs-lookup"><span data-stu-id="5994f-164">Set HTTPS certificates in code</span></span>

<span data-ttu-id="5994f-165">Kodda https 'yi yapılandırmak için, `ConfigureKestrel` `Program` sınıfındaki `IWebHostBuilder` içindeki yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="5994f-165">To configure HTTPS on Kestrel in code, use the `ConfigureKestrel` method on `IWebHostBuilder` in the `Program` class.</span></span>

```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureWebHostDefaults(webBuilder =>
        {
            webBuilder.UseStartup<Startup>();
            webBuilder.ConfigureKestrel(kestrel =>
            {
                kestrel.ConfigureHttpsDefaults(https =>
                {
                    https.ServerCertificate = new X509Certificate2("mycert.pfx", "password");
                });
            });
        });
```

<span data-ttu-id="5994f-166">Yine, `.pfx` dosyanın parolasının ' de depolanması ve güvenli bir yapılandırma kaynağından alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5994f-166">Again, the password for the `.pfx` file should be stored in and retrieved from a secure configuration source.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="5994f-167">[Önceki](grpc-in-production.md)
>[İleri](docker.md)</span><span class="sxs-lookup"><span data-stu-id="5994f-167">[Previous](grpc-in-production.md)
[Next](docker.md)</span></span>