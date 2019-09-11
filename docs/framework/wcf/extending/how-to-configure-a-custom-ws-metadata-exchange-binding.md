---
title: 'Nasıl yapılır: Özel Bir WS-Metadata Değişimi Bağlaması Yapılandırma'
ms.date: 03/30/2017
helpviewer_keywords:
- WS-Metadata Exchange [WCF]
- WS-Metadata Exchange [WCF], configuring a custom binding
ms.assetid: cdba4d73-da64-4805-bc56-9822becfd1e4
ms.openlocfilehash: b4a4005a23c8c74edecb00475669e019b50a17af
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70851229"
---
# <a name="how-to-configure-a-custom-ws-metadata-exchange-binding"></a><span data-ttu-id="5d0ab-102">Nasıl yapılır: Özel Bir WS-Metadata Değişimi Bağlaması Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5d0ab-102">How to: Configure a Custom WS-Metadata Exchange Binding</span></span>
<span data-ttu-id="5d0ab-103">Bu konu, özel bir WS-Metadata değişim bağlamasının nasıl yapılandırılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="5d0ab-103">This topic will explain how to configure a custom WS-Metadata exchange binding.</span></span> <span data-ttu-id="5d0ab-104">Windows Communication Foundation (WCF), sistem tarafından tanımlanan dört meta veri bağlaması içerir, ancak istediğiniz bağlamayı kullanarak meta verileri yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d0ab-104">Windows Communication Foundation (WCF) includes four system-defined metadata bindings, but you can publish metadata using any binding you want.</span></span> <span data-ttu-id="5d0ab-105">Bu konu, `wsHttpBinding`kullanarak meta verileri nasıl yayımlayacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5d0ab-105">This topic will show you how to publish metadata using the `wsHttpBinding`.</span></span> <span data-ttu-id="5d0ab-106">Bu bağlama, meta verileri güvenli bir şekilde gösterme seçeneği sunar.</span><span class="sxs-lookup"><span data-stu-id="5d0ab-106">This binding gives you the option of exposing metadata in a secure way.</span></span> <span data-ttu-id="5d0ab-107">Bu makaledeki kod, [Başlarken](../samples/getting-started-sample.md)' i temel alır.</span><span class="sxs-lookup"><span data-stu-id="5d0ab-107">The code in this article is based on the [Getting Started](../samples/getting-started-sample.md).</span></span>  
  
### <a name="using-a-configuration-file"></a><span data-ttu-id="5d0ab-108">Yapılandırma dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="5d0ab-108">Using a configuration file</span></span>  
  
1. <span data-ttu-id="5d0ab-109">Hizmetin yapılandırma dosyasında, `serviceMetadata` etiketi içeren bir hizmet davranışı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-109">In the service's configuration file, add a service behavior that contains the `serviceMetadata` tag:</span></span>  
  
    ```xml  
    <behaviors>  
       <serviceBehaviors>  
         <behavior name="CalculatorServiceBehavior">  
           <serviceMetadata httpGetEnabled="True"/>  
         </behavior>  
       </serviceBehaviors>  
    </behaviors>  
    ```  
  
2. <span data-ttu-id="5d0ab-110">Hizmet etiketine `behaviorConfiguration` bu yeni davranışa başvuran bir öznitelik ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-110">Add a `behaviorConfiguration` attribute to the service tag that references this new behavior:</span></span>  
  
    ```xml  
    <service        name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">   
    ```  
  
3. <span data-ttu-id="5d0ab-111">Adres `wsHttpBinding` olarak MEX, bağlama olarak ve <xref:System.ServiceModel.Description.IMetadataExchange> sözleşme olarak belirten bir meta veri uç noktası ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-111">Add a metadata endpoint specifying mex as the address, `wsHttpBinding` as the binding, and <xref:System.ServiceModel.Description.IMetadataExchange> as the contract:</span></span>  
  
    ```xml  
    <endpoint address="mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange" />  
    ```  
  
4. <span data-ttu-id="5d0ab-112">Meta veri değişimi uç noktasının düzgün çalıştığını doğrulamak için istemci yapılandırma dosyasına bir uç nokta etiketi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-112">To verify the metadata exchange endpoint is working correctly add an endpoint tag in the client configuration file:</span></span>  
  
    ```xml  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
5. <span data-ttu-id="5d0ab-113">İstemcinin Main () yönteminde, <xref:System.ServiceModel.Description.MetadataExchangeClient> yeni bir örnek oluşturun, <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> özelliğini olarak `true`ayarlayın, çağırın <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> ve ardından döndürülen meta veri koleksiyonunu yineleyin:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-113">In the client's Main() method, create a new <xref:System.ServiceModel.Description.MetadataExchangeClient> instance, set its <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> property to `true`, call <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> and then iterate through the collection of metadata returned:</span></span>  
  
    ```csharp
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
    ```  
  
### <a name="configuring-by-code"></a><span data-ttu-id="5d0ab-114">Kodla yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5d0ab-114">Configuring by code</span></span>  
  
1. <span data-ttu-id="5d0ab-115"><xref:System.ServiceModel.WSHttpBinding> Bağlama örneği oluştur:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-115">Create a <xref:System.ServiceModel.WSHttpBinding> binding instance:</span></span>  
  
    ```csharp  
    WSHttpBinding binding = new WSHttpBinding();  
    ```  
  
2. <span data-ttu-id="5d0ab-116"><xref:System.ServiceModel.ServiceHost> Örnek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-116">Create a <xref:System.ServiceModel.ServiceHost> instance:</span></span>  
  
    ```csharp  
    ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress);  
    ```  
  
3. <span data-ttu-id="5d0ab-117">Hizmet uç noktası ekleyin ve bir <xref:System.ServiceModel.Description.ServiceMetadataBehavior> örnek ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-117">Add a service endpoint and add a <xref:System.ServiceModel.Description.ServiceMetadataBehavior> instance:</span></span>  
  
    ```csharp  
    serviceHost.AddServiceEndpoint(typeof(ICalculator), binding, baseAddress);  
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();  
    smb.HttpGetEnabled = true;  
    serviceHost.Description.Behaviors.Add(smb);  
    ```  
  
4. <span data-ttu-id="5d0ab-118">Daha önce <xref:System.ServiceModel.WSHttpBinding> oluşturulmuş bir meta veri değişimi uç noktası ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-118">Add a metadata exchange endpoint, specifying the <xref:System.ServiceModel.WSHttpBinding> created earlier:</span></span>  
  
    ```csharp  
    serviceHost.AddServiceEndpoint(typeof(IMetadataExchange), binding, mexAddress);  
    ```  
  
5. <span data-ttu-id="5d0ab-119">Meta veri değişimi uç noktasının düzgün çalıştığını doğrulamak için, istemci yapılandırma dosyasına bir uç nokta etiketi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-119">To verify that the metadata exchange endpoint is working correctly, add an endpoint tag in the client configuration file:</span></span>  
  
    ```xml  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
6. <span data-ttu-id="5d0ab-120">İstemcinin Main () yönteminde, <xref:System.ServiceModel.Description.MetadataExchangeClient> yeni bir örnek oluşturun, <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> özelliğini olarak `true`ayarlayın, çağırın <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> ve ardından döndürülen meta veri koleksiyonu aracılığıyla yineleyin:</span><span class="sxs-lookup"><span data-stu-id="5d0ab-120">In the client's Main() method, create a new <xref:System.ServiceModel.Description.MetadataExchangeClient> instance, set the <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> property to `true`, call <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> and then iterate through the collection of metadata returned:</span></span>  
  
    ```csharp  
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="5d0ab-121">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="5d0ab-121">See also</span></span>

- [<span data-ttu-id="5d0ab-122">Meta Veri Yayımlama Davranışı</span><span class="sxs-lookup"><span data-stu-id="5d0ab-122">Metadata Publishing Behavior</span></span>](../samples/metadata-publishing-behavior.md)
- [<span data-ttu-id="5d0ab-123">Meta Verileri Alma</span><span class="sxs-lookup"><span data-stu-id="5d0ab-123">Retrieve Metadata</span></span>](../samples/retrieve-metadata.md)
- [<span data-ttu-id="5d0ab-124">Meta Veriler</span><span class="sxs-lookup"><span data-stu-id="5d0ab-124">Metadata</span></span>](../feature-details/metadata.md)
- [<span data-ttu-id="5d0ab-125">Meta Verileri Yayımlama</span><span class="sxs-lookup"><span data-stu-id="5d0ab-125">Publishing Metadata</span></span>](../feature-details/publishing-metadata.md)
- [<span data-ttu-id="5d0ab-126">Meta Veri Uç Noktalarını Yayımlama</span><span class="sxs-lookup"><span data-stu-id="5d0ab-126">Publishing Metadata Endpoints</span></span>](../publishing-metadata-endpoints.md)
