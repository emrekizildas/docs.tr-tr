---
title: WS 2007 Federasyon HTTP Bağlama
ms.date: 03/30/2017
ms.assetid: 91c1b477-a96e-4bf5-9330-5e9312113371
ms.openlocfilehash: ad56665b5b6648fb93a9f31f18167a964b4cba92
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834650"
---
# <a name="ws-2007-federation-http-binding"></a><span data-ttu-id="ba3f6-102">WS 2007 Federasyon HTTP Bağlama</span><span class="sxs-lookup"><span data-stu-id="ba3f6-102">WS 2007 Federation HTTP Binding</span></span>

<span data-ttu-id="ba3f6-103">Bu örnek, WS-Trust belirtiminin 1,3 sürümünü destekleyen federe senaryolar oluşturmak için kullanabileceğiniz standart bir bağlama olan <xref:System.ServiceModel.WS2007FederationHttpBinding> ' ın kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-103">This sample demonstrates the use of <xref:System.ServiceModel.WS2007FederationHttpBinding>, a standard binding that you can use to build federated scenarios that support version 1.3 of the WS-Trust specification.</span></span>

> [!NOTE]
> <span data-ttu-id="ba3f6-104">Bu örneğe ilişkin Kurulum yordamı ve derleme yönergeleri bu konunun sonunda bulunur.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-104">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="ba3f6-105">Örnek, konsol tabanlı bir istemci programından (*Client. exe*), konsol tabanlı bir güvenlik belirteci hizmeti programından (*SecurityTokenService. exe*) ve konsol tabanlı bir hizmet programından (*Service. exe*) oluşur.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-105">The sample consists of a console-based client program (*Client.exe*), a console-based security token service program (*Securitytokenservice.exe*), and a console-based service program (*Service.exe*).</span></span> <span data-ttu-id="ba3f6-106">Hizmet, istek/yanıt iletişim modelini tanımlayan bir sözleşme uygular.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-106">The service implements a contract that defines a request/reply communication pattern.</span></span> <span data-ttu-id="ba3f6-107">Sözleşme, matematik işlemlerini (`Add`, `Subtract`, `Multiply` ve `Divide`) sunan `ICalculator` arabirimi tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-107">The contract is defined by the `ICalculator` interface, which exposes math operations (`Add`, `Subtract`, `Multiply`, and `Divide`).</span></span> <span data-ttu-id="ba3f6-108">İstemci, güvenlik belirteci hizmetinden (STS) bir güvenlik belirteci alır ve belirli bir matematik işlemi için hizmete zaman uyumlu istekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-108">The client obtains a security token from the Security Token Service (STS) and makes synchronous requests to the service for a given math operation.</span></span> <span data-ttu-id="ba3f6-109">Hizmet daha sonra sonuçla yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-109">The service then replies with the result.</span></span> <span data-ttu-id="ba3f6-110">İstemci etkinliği konsol penceresinde görünür.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-110">Client activity is visible in the console window.</span></span>

<span data-ttu-id="ba3f6-111">Örnek, `ICalculator` sözleşmesinin `ws2007FederationHttpBinding` öğesini kullanarak kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-111">The sample makes the `ICalculator` contract available using the `ws2007FederationHttpBinding` element.</span></span> <span data-ttu-id="ba3f6-112">İstemci üzerindeki bu bağlamanın yapılandırması aşağıdaki kodda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ba3f6-112">The configuration of this binding on the client is shown in the following code:</span></span>

```xml
<bindings>
  <ws2007FederationHttpBinding>
    <binding name="ServiceFed" >
      <security mode ="Message">
        <message issuedKeyType ="SymmetricKey"
                 issuedTokenType ="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" >
          <!-- Endpoint address and binding for Security Token Service -->
          <issuer address ="http://localhost:8000/sts/windows"
                  binding ="ws2007HttpBinding" />
        </message>
      </security>
    </binding>
  </ws2007FederationHttpBinding>
</bindings>
```

<span data-ttu-id="ba3f6-113">[@No__t-1güvenlik >](../../configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md), `security` değeri hangi güvenlik modunun kullanılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-113">On the [\<security>](../../configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md), the `security` value specifies which security mode should be used.</span></span> <span data-ttu-id="ba3f6-114">Bu örnekte, [\<message >](../../configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) [\<güvenlik >](../../configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md)içinde belirtildiğinde `message` güvenliği kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-114">In this sample, `message` security is used, which is why the [\<message>](../../configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) is specified inside the [\<security>](../../configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md).</span></span> <span data-ttu-id="ba3f6-115">[@No__t-3message >](../../configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) içindeki [\<ıssuer >](../../configure-apps/file-schema/wcf/issuer.md) öğesi, istemcinin `ICalculator` hizmetinde kimlik doğrulaması yapabilmesi için istemciye BIR güvenlik belirteci veren STS 'nin adresini ve bağlamasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-115">The [\<issuer>](../../configure-apps/file-schema/wcf/issuer.md) element inside the [\<message>](../../configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) specifies the address and binding for the STS that issues a security token to the client so that the client can authenticate to the `ICalculator` service.</span></span>
  
<span data-ttu-id="ba3f6-116">Hizmette Bu bağlamanın yapılandırması aşağıdaki kodda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ba3f6-116">The configuration of this binding on the service is shown in the following code:</span></span>

```xml
<bindings>
  <ws2007FederationHttpBinding>
    <binding name="ServiceFed" >
      <security mode ="Message">
        <message issuedKeyType ="SymmetricKey"
                 issuedTokenType ="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" >
          <!-- Metadata address for Security Token Service -->
          <issuerMetadata address ="http://localhost:8000/sts/mex" >
            <identity>
              <certificateReference storeLocation ="CurrentUser"
                                    storeName="TrustedPeople"
                                    x509FindType ="FindBySubjectDistinguishedName"
                                    findValue ="CN=STS" />
            </identity>
          </issuerMetadata>
        </message>
      </security>
    </binding>
  </ws2007FederationHttpBinding>
</bindings>
```

<span data-ttu-id="ba3f6-117">[@No__t-1güvenlik >](../../configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md), `security` değeri hangi güvenlik modunun kullanılması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-117">On the [\<security>](../../configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md), the `security` value specifies which security mode should be used.</span></span> <span data-ttu-id="ba3f6-118">Bu örnekte, [\<message >](../../configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) [\<güvenlik >](../../configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md)içinde belirtildiğinde `message` güvenliği kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-118">In this sample, `message` security is used, which is why the [\<message>](../../configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) is specified inside the [\<security>](../../configure-apps/file-schema/wcf/security-element-of-ws2007federationhttpbinding.md).</span></span> <span data-ttu-id="ba3f6-119">[@No__t-4message >](../../configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) içindeki `ws2007FederationHttpBinding` ' nin [\<ıssuermetadata >](../../configure-apps/file-schema/wcf/issuermetadata.md) öğesi, STS için meta verileri almak üzere kullanılabilecek bir uç noktanın adresini ve kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-119">The [\<issuerMetadata>](../../configure-apps/file-schema/wcf/issuermetadata.md) element of `ws2007FederationHttpBinding` inside the [\<message>](../../configure-apps/file-schema/wcf/message-element-of-ws2007federationhttpbinding.md) specifies the address and identity for an endpoint that can be used to retrieve metadata for the STS.</span></span>

<span data-ttu-id="ba3f6-120">Hizmetin davranışı aşağıdaki kodda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ba3f6-120">The behavior for the service is shown in the following code:</span></span>

```xml
<behaviors>
  <serviceBehaviors>
    <behavior name ="ServiceBehaviour" >
      <serviceDebug includeExceptionDetailInFaults ="true"/>
      <serviceMetadata httpGetEnabled ="true"/>
      <serviceCredentials>
        <issuedTokenAuthentication>
          <knownCertificates>
            <add storeLocation ="LocalMachine"
                 storeName="TrustedPeople"
                 x509FindType="FindBySubjectDistinguishedName"
                 findValue="CN=STS" />
          </knownCertificates>
        </issuedTokenAuthentication>
        <serviceCertificate storeLocation ="LocalMachine"
                            storeName ="My"
                            x509FindType ="FindBySubjectDistinguishedName"
                            findValue ="CN=localhost"/>
      </serviceCredentials>
    </behavior>
  </serviceBehaviors>
</behaviors>
```
  
<span data-ttu-id="ba3f6-121">[@No__t-1ıssuedtokenauthentication >](../../configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md)>, hizmetin kimlik doğrulaması sırasında istemcilerin sunmalarına izin verdiği belirteçlerde kısıtlamalar belirlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-121">The [\<issuedTokenAuthentication>](../../configure-apps/file-schema/wcf/issuedtokenauthentication-of-servicecredentials.md)> allows the service to specify constraints on the tokens it allows clients to present during authentication.</span></span> <span data-ttu-id="ba3f6-122">Bu yapılandırma, konu adı CN = STS olan bir sertifika tarafından imzalanmış belirteçlerin hizmet tarafından kabul edildiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-122">This configuration specifies that tokens signed by a certificate whose subject name is CN=STS are accepted by the service.</span></span>

<span data-ttu-id="ba3f6-123">STS, standart <xref:System.ServiceModel.WS2007HttpBinding> kullanarak tek bir uç noktanın kullanılabilir olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-123">STS makes a single endpoint available using the standard <xref:System.ServiceModel.WS2007HttpBinding>.</span></span> <span data-ttu-id="ba3f6-124">Hizmet, istemcilerden belirteç isteklerine yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-124">The service responds to requests from clients for tokens.</span></span> <span data-ttu-id="ba3f6-125">İstemcinin kimliği bir Windows hesabı kullanılarak doğrulandıysa, hizmet istemcinin kullanıcı adını bir talep olarak içeren bir belirteç yayınlar.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-125">If the client is authenticated using a Windows account, the service issues a token that contains the client's user name as a claim.</span></span> <span data-ttu-id="ba3f6-126">Belirteç oluşturmanın bir parçası olarak STS, CN = STS sertifikasıyla ilişkili özel anahtarı kullanarak belirteci imzalar.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-126">As part of creating the token, STS signs the token using the private key associated with the CN=STS certificate.</span></span> <span data-ttu-id="ba3f6-127">Ayrıca, bir simetrik anahtar oluşturur ve CN = localhost sertifikasıyla ilişkili ortak anahtarı kullanarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-127">In addition, it creates a symmetric key and encrypts it using the public key associated with the CN=localhost certificate.</span></span> <span data-ttu-id="ba3f6-128">Belirteci istemciye döndürmekte sonra STS simetrik anahtarı da döndürür.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-128">In returning the token to the client, STS also returns the symmetric key.</span></span> <span data-ttu-id="ba3f6-129">İstemci, verilen belirteci `ICalculator` hizmetine sunar ve iletiyi bu anahtarla imzalayarak simetrik anahtarı biliyor olduğunu kanıtlar.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-129">The client presents the issued token to the `ICalculator` service and proves that it knows the symmetric key by signing the message with that key.</span></span>

<span data-ttu-id="ba3f6-130">Örneği çalıştırdığınızda, güvenlik belirteci isteği STS konsol penceresinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-130">When you run the sample, the request for the security token is shown in the STS console window.</span></span> <span data-ttu-id="ba3f6-131">İşlemin istekleri ve yanıtları istemci ve hizmet konsolu pencereleri içinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-131">The operation's requests and responses are displayed in the client and service console windows.</span></span> <span data-ttu-id="ba3f6-132">Uygulamayı kapatmak için konsol pencerelerinin herhangi birinde ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-132">Press ENTER in any of the console windows to shut down the application.</span></span>

```console
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714
Press <ENTER> to terminate client.
```

<span data-ttu-id="ba3f6-133">Bu örneğe eklenen *Setup. bat* dosyası, şirket içinde barındırılan bir uygulamayı çalıştırmak için sunucuyu ve STS 'yi ilgili sertifikalarla yapılandırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-133">The *Setup.bat* file included with this sample allows you to configure the server and STS with the relevant certificates to run a self-hosted application.</span></span> <span data-ttu-id="ba3f6-134">Toplu iş dosyası, LocalMachine/Trustedkişileri sertifika deposunda iki sertifika oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-134">The batch file creates two certificates in the LocalMachine/TrustedPeople certificate store.</span></span> <span data-ttu-id="ba3f6-135">İlk sertifika, CN = STS 'nin konu adına sahiptir ve STS tarafından, istemciye verdiği güvenlik belirteçlerini imzalamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-135">The first certificate has a subject name of CN=STS and is used by STS to sign the security tokens that it issues to the client.</span></span> <span data-ttu-id="ba3f6-136">İkinci sertifika, CN = localhost konu adına sahiptir ve STS tarafından hizmetin şifresini çözebilmesi için bir anahtar şifrelemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-136">The second certificate has a subject name of CN=localhost and is used by STS to encrypt a key in a way that the service can decrypt.</span></span>

## <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="ba3f6-137">Örneği ayarlamak, derlemek ve çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="ba3f6-137">To set up, build, and run the sample</span></span>
  
1. <span data-ttu-id="ba3f6-138">[Windows Communication Foundation Örnekleri Için tek seferlik Kurulum yordamını](one-time-setup-procedure-for-the-wcf-samples.md)gerçekleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-138">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="ba3f6-139">Yönetici ayrıcalıklarına sahip bir Visual Studio Geliştirici Komut İstemi açın ve gerekli sertifikaları oluşturmak için Setup. bat dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-139">Open a Developer Command Prompt for Visual Studio with administrator privileges and run the Setup.bat file to create the required certificates.</span></span>

 <span data-ttu-id="ba3f6-140">Bu toplu iş dosyası, Windows SDK dağıtılan *certmgr. exe* ve Makecert. exe ' yi kullanır.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-140">This batch file uses *Certmgr.exe* and Makecert.exe, which are distributed with the Windows SDK.</span></span> <span data-ttu-id="ba3f6-141">Ancak, bu araçları bulmak için betiği etkinleştirmek üzere Visual Studio komut istemi içinden *Setup. bat* dosyasını çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-141">However, you must run *Setup.bat* from within a Visual Studio command prompt to enable the script to find these tools.</span></span>

1. <span data-ttu-id="ba3f6-142">Çözümün C# veya Visual Basic .NET sürümünü oluşturmak Için [Windows Communication Foundation örnekleri oluşturma](building-the-samples.md)konusundaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-142">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

2. <span data-ttu-id="ba3f6-143">Örneği tek veya bir çoklu bilgisayar yapılandırmasında çalıştırmak için [Windows Communication Foundation Örnekleri çalıştırma](running-the-samples.md)bölümündeki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-143">To run the sample in a single- or cross-computer configuration, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span> <span data-ttu-id="ba3f6-144">@No__t-0 kullanıyorsanız, *Service. exe*, *Client. exe*ve *SecurityTokenService. exe* ' yi yükseltilmiş ayrıcalıklarla çalıştırmanız gerekir (dosyalara sağ tıklayıp **yönetici olarak çalıştır**' a tıklayın).</span><span class="sxs-lookup"><span data-stu-id="ba3f6-144">If you are using [!INCLUDE[windowsver](../../../../includes/windowsver-md.md)], you must run *Service.exe*, *Client.exe*, and *SecurityTokenService.exe* with elevated privileges (right-click the files and then click **Run as administrator**).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba3f6-145">Örnekler bilgisayarınızda zaten yüklü olabilir.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-145">The samples may already be installed on your computer.</span></span> <span data-ttu-id="ba3f6-146">Devam etmeden önce aşağıdaki (varsayılan) dizini denetleyin:</span><span class="sxs-lookup"><span data-stu-id="ba3f6-146">Check for the following (default) directory before continuing:</span></span>
> 
> `<InstallDrive>:\WF_WCF_Samples`
> 
> <span data-ttu-id="ba3f6-147">Bu dizin yoksa, tüm Windows Communication Foundation (WCF) ve [!INCLUDE[wf1](../../../../includes/wf1-md.md)] örneklerini indirmek için [Windows Communication Foundation (WCF) ve Windows Workflow Foundation (WF) örneklerine .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) ' e gidin.</span><span class="sxs-lookup"><span data-stu-id="ba3f6-147">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="ba3f6-148">Bu örnek aşağıdaki dizinde bulunur:</span><span class="sxs-lookup"><span data-stu-id="ba3f6-148">This sample is located in the following directory:</span></span>
> 
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\WS\WS2007FederationHttp`
