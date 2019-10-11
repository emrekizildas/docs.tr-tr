---
title: DataContractJsonSerializer örneği
ms.date: 03/30/2017
ms.assetid: 3c2c4747-7510-4bdf-b4fe-64f98428ef4a
ms.openlocfilehash: 1711c826397dfb8b54ecedee08e88e67cb58d2a4
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72180237"
---
# <a name="datacontractjsonserializer-sample"></a><span data-ttu-id="e3906-102">DataContractJsonSerializer örneği</span><span class="sxs-lookup"><span data-stu-id="e3906-102">DataContractJsonSerializer sample</span></span>
<span data-ttu-id="e3906-103">Bu örnek, JavaScript Nesne Gösterimi (JSON) biçimindeki verileri seri hale getirmek ve seri durumdan çıkarmak için <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> ' nın nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3906-103">This sample demonstrates how to use the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> to serialize and deserialize data in the JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="e3906-104">Bu serileştirme altyapısı JSON verilerini .NET Framework türü örneklerine ve JSON verilerine geri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="e3906-104">This serialization engine converts JSON data into instances of .NET Framework types and back into JSON data.</span></span> <span data-ttu-id="e3906-105"><xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> <xref:System.Runtime.Serialization.DataContractSerializer> ile aynı türleri destekler.</span><span class="sxs-lookup"><span data-stu-id="e3906-105"><xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> supports the same types as <xref:System.Runtime.Serialization.DataContractSerializer>.</span></span> <span data-ttu-id="e3906-106">JSON veri biçimi, zaman uyumsuz JavaScript ve XML (AJAX) stili Web uygulamaları yazarken özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="e3906-106">The JSON data format is especially useful when writing Asynchronous JavaScript and XML (AJAX)-style Web applications.</span></span> <span data-ttu-id="e3906-107">Windows Communication Foundation (WCF) ' de AJAX desteği, ScriptManager denetimi aracılığıyla ASP.NET AJAX ile kullanım için iyileştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e3906-107">AJAX support in Windows Communication Foundation (WCF) is optimized for use with ASP.NET AJAX through the ScriptManager control.</span></span> <span data-ttu-id="e3906-108">ASP.NET AJAX ile Windows Communication Foundation (WCF) kullanmanın örnekleri için bkz. [Ajax örnekleri](ajax.md).</span><span class="sxs-lookup"><span data-stu-id="e3906-108">For examples of how to use Windows Communication Foundation (WCF) with ASP.NET AJAX, see the [AJAX Samples](ajax.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="e3906-109">Bu örneğe ilişkin Kurulum yordamı ve derleme yönergeleri bu konunun sonunda bulunur.</span><span class="sxs-lookup"><span data-stu-id="e3906-109">The set-up procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="e3906-110">Örnek, serileştirme ve seri durumdan çıkarma göstermek için `Person` veri sözleşmesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="e3906-110">The sample uses a `Person` data contract to demonstrate serialization and deserialization.</span></span>  

```csharp
[DataContract]
class Person
{
    [DataMember]
    internal string name;

    [DataMember]
    internal int age;
}
```

 <span data-ttu-id="e3906-111">@No__t-0 türünün bir örneğini JSON olarak seri hale getirmek için önce <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> ' i oluşturun ve JSON verilerini bir akışa yazmak için `WriteObject` yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3906-111">To serialize an instance of the `Person` type to JSON, create the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> first and use the `WriteObject` method to write JSON data to a stream.</span></span>  

```csharp
Person p = new Person();
//Set up Person object...
MemoryStream stream1 = new MemoryStream();
DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(Person));
ser.WriteObject(stream1, p);
```

 <span data-ttu-id="e3906-112">Bellek akışı geçerli JSON verileri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="e3906-112">The memory stream contains valid JSON data.</span></span>
  
```json  
{"age":42,"name":"John"}  
```  
  
 <span data-ttu-id="e3906-113">Örnek, JSON verilerinden bir nesne olarak seri durumdan çıkarmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3906-113">The sample demonstrates deserializing from JSON data into an object.</span></span> <span data-ttu-id="e3906-114">Sonra akışı geri sarın ve `ReadObject` ' ı çağırın.</span><span class="sxs-lookup"><span data-stu-id="e3906-114">You then rewind the stream and call `ReadObject`.</span></span>  

```csharp
Person p2 = (Person)ser.ReadObject(stream1);
```

 <span data-ttu-id="e3906-115">@No__t-0 nesnesini incelemek, JSON verilerinin doğru şekilde seri durumdan çıkarılmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3906-115">Examining the `p2` object reveals that the JSON data has been deserialized correctly.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="e3906-116">Örnekler makinenizde zaten yüklü olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3906-116">The samples may already be installed on your machine.</span></span> <span data-ttu-id="e3906-117">Devam etmeden önce aşağıdaki (varsayılan) dizini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e3906-117">Check for the following (default) directory before continuing.</span></span>  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> <span data-ttu-id="e3906-118">Bu dizin yoksa, tüm Windows Communication Foundation (WCF) ve [!INCLUDE[wf1](../../../../includes/wf1-md.md)] örneklerini indirmek için [Windows Communication Foundation (WCF) ve Windows Workflow Foundation (WF) örneklerine .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) ' e gidin.</span><span class="sxs-lookup"><span data-stu-id="e3906-118">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="e3906-119">Bu örnek, aşağıdaki dizinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="e3906-119">This sample is located in the following directory.</span></span>  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Ajax\JsonSerialization`  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="e3906-120">Bunu ayarlamak için örneği oluşturun ve çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e3906-120">To set up, build and run the sample</span></span>  
  
1. <span data-ttu-id="e3906-121">[Windows Communication Foundation örnekleri oluşturma](../../../../docs/framework/wcf/samples/building-the-samples.md)bölümünde açıklandığı gibi jsonSerialization. sln çözümünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e3906-121">Build the solution JsonSerialization.sln as described in [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).</span></span>  
  
2. <span data-ttu-id="e3906-122">Ortaya çıkan konsol uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e3906-122">Run the resulting console application.</span></span>  
