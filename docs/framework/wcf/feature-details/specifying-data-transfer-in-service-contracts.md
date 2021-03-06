---
title: Hizmet Sözleşmelerinde Veri Aktarımını Belirtme
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service contracts [WCF], data transfer
ms.assetid: 7c5a26c8-89c9-4bcb-a4bc-7131e6d01f0c
ms.openlocfilehash: 47544cf74b4fa09fd8ee868ea940ef24a453840e
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834640"
---
# <a name="specifying-data-transfer-in-service-contracts"></a>Hizmet Sözleşmelerinde Veri Aktarımını Belirtme
Windows Communication Foundation (WCF) bir mesajlaşma altyapısı olarak düşünülebilir. Hizmet işlemleri iletileri alabilir, işleyebilir ve iletileri gönderebilir. İletiler, işlem sözleşmeleri kullanılarak açıklanır. Örneğin, aşağıdaki sözleşmeyi göz önünde bulundurun.  
  
```csharp  
[ServiceContract]  
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    float GetAirfare(string fromCity, string toCity);  
}  
```  
  
```vb  
<ServiceContract()>  
Public Interface IAirfareQuoteService  
  
    <OperationContract()>  
    Function GetAirfare(fromCity As String, toCity As String) As Double  
End Interface  
```  
  
 Burada, `GetAirfare` işlemi `fromCity` ve `toCity` hakkında bilgi içeren bir ileti kabul eder ve ardından sayı içeren bir ileti döndürür.  
  
 Bu konu başlığı altında, bir işlem sözleşmesinin iletileri nasıl açıklayabileceği çeşitli yollar açıklanmaktadır.  
  
## <a name="describing-messages-by-using-parameters"></a>Parametreleri kullanarak Iletileri açıklama  
 Bir iletiyi tanımlamanın en kolay yolu bir parametre listesi ve dönüş değeri kullanmaktır. Yukarıdaki örnekte, istek iletisini anlatmak için `fromCity` ve `toCity` dize parametreleri kullanıldı ve yanıt iletisini anlatmak için float dönüş değeri kullanıldı. Dönüş değeri yalnızca bir yanıt iletisini anlatmak için yeterli değilse, out parametreleri kullanılabilir. Örneğin, aşağıdaki işlemin, istek iletisinde `fromCity` ve `toCity` ve yanıt iletisindeki bir para birimiyle birlikte bir sayı vardır:  
  
```csharp  
[OperationContract]  
float GetAirfare(string fromCity, string toCity, out string currency);  
```  
  
```vb  
<OperationContract()>  
    Function GetAirfare(fromCity As String, toCity As String) As Double  
```  
  
 Ayrıca, hem isteğin hem de yanıt iletisinin bir parametre parçasını oluşturmak için başvuru parametrelerini kullanabilirsiniz. Parametrelerin serileştirilemiyor (XML 'e dönüştürülebileceğinden) türler olmalıdır. Varsayılan olarak, WCF bu dönüştürmeyi gerçekleştirmek için <xref:System.Runtime.Serialization.DataContractSerializer> sınıfı olarak adlandırılan bir bileşeni kullanır. En basit türler (örneğin `int`, `string`, `float` ve `DateTime`.) desteklenir. Kullanıcı tanımlı türlerin normalde bir veri anlaşması olması gerekir. Daha fazla bilgi için bkz. [Veri Sözleşmelerini Kullanma](../../../../docs/framework/wcf/feature-details/using-data-contracts.md).  
  
```csharp
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    float GetAirfare(Itinerary itinerary, DateTime date);  
  
    [DataContract]  
    public class Itinerary  
    {  
        [DataMember]  
        public string fromCity;  
        [DataMember]  
        public string toCity;  
   }  
}  
```  
  
```vb  
Public Interface IAirfareQuoteService  
    <OperationContract()>  
    GetAirfare(itinerary as Itinerary, date as DateTime) as Double  
  
    <DataContract()>  
    Class Itinerary  
  
        <DataMember()>  
        Public fromCity As String  
        <DataMember()>  
        Public toCity As String  
    End Class  
End Interface  
```  
  
 Bazen `DataContractSerializer`, türlerinizi seri hale getirmek için yeterli değildir. WCF, parametreleri seri hale getirmek için de kullanabileceğiniz alternatif bir serileştirme altyapısını (<xref:System.Xml.Serialization.XmlSerializer>) destekler. @No__t-0, `XmlAttributeAttribute` gibi öznitelikleri kullanarak sonuçtaki XML üzerinde daha fazla denetim kullanmanıza olanak sağlar. @No__t-0 ' ı belirli bir işlem için veya tüm hizmet için kullanmak üzere değiştirmek için, <xref:System.ServiceModel.XmlSerializerFormatAttribute> özniteliğini bir işleme veya hizmete uygulayın. Örneğin:  
  
```csharp  
[ServiceContract]  
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    [XmlSerializerFormat]  
    float GetAirfare(Itinerary itinerary, DateTime date);  
}  
public class Itinerary  
{  
    public string fromCity;  
    public string toCity;  
    [XmlAttribute]  
    public bool isFirstClass;  
}  
```  
  
```vb  
<ServiceContract()>  
Public Interface IAirfareQuoteService  
    <OperationContract()>  
    <XmlSerializerFormat>  
    GetAirfare(itinerary as Itinerary, date as DateTime) as Double  
  
End Interface  
  
Class Itinerary  
  
    Public fromCity As String  
    Public toCity As String  
    <XmlSerializerFormat()>  
    Public isFirstClass As Boolean  
End Class  
```  
  
 Daha fazla bilgi için, bkz. [XmlSerializer sınıfını kullanma](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md). Burada gösterildiği gibi, bu konu başlığı altında açıklandığı gibi belirli bir nedenleriniz olmadığı sürece, burada gösterildiği gibi <xref:System.Xml.Serialization.XmlSerializer> ' a el ile geçiş yapmayı unutmayın.  
  
 .NET parametre adlarını sözleşme adlarından yalıtmak için <xref:System.ServiceModel.MessageParameterAttribute> özniteliğini kullanabilir ve `Name` özelliğini kullanarak sözleşme adını ayarlayabilirsiniz. Örneğin, aşağıdaki işlem sözleşmesi, bu konudaki ilk örnekle eşdeğerdir.  
  
```csharp  
[OperationContract]  
public float GetAirfare(  
    [MessageParameter(Name="fromCity")] string originCity,  
    [MessageParameter(Name="toCity")] string destinationCity);  
```  
  
```vb  
<OperationContract()>  
  Function GetAirfare(<MessageParameter(Name := "fromCity")> fromCity As String, <MessageParameter(Name := "toCity")> toCity As String) As Double  
```  
  
## <a name="describing-empty-messages"></a>Boş Iletileri açıklama  
 Boş bir istek iletisi, hiçbir giriş veya başvuru parametresi olmadan açıklanabilir. Örneğin C#:  
  
 `[OperationContract]`  
  
 `public int GetCurrentTemperature();`  
  
 Örneğin, VB:  
  
 `<OperationContract()>`  
  
 `Function GetCurrentTemperature() as Integer`  
  
 Boş bir yanıt iletisi `void` dönüş türü ve çıkış ya da başvuru parametresi olmadan açıklanabilir. Örneğin:  
  
```csharp  
[OperationContract]  
public void SetTemperature(int temperature);  
```  
  
```vb  
<OperationContract()>  
Sub SetTemperature(temperature As Integer)  
```  
  
 Bu, tek yönlü bir işlemden farklıdır, örneğin:  
  
```csharp  
[OperationContract(IsOneWay=true)]  
public void SetLightbulbStatus(bool isOn);  
```  
  
```vb  
<OperationContract(IsOneWay:=True)>  
Sub SetLightbulbStatus(isOne As Boolean)  
```  
  
 @No__t-0 işlemi boş bir ileti döndürüyor. Giriş iletisini işlerken bir sorun oluşursa bunun yerine bir hata döndürebilir. @No__t-0 işlemi hiçbir şey döndürmez. Bu işlemden bir hata koşulunu iletmenin bir yolu yoktur.  
  
## <a name="describing-messages-by-using-message-contracts"></a>Ileti sözleşmelerini kullanarak Iletileri açıklama  
 Tüm iletiyi göstermek için tek bir tür kullanmak isteyebilirsiniz. Bu amaçla bir veri sözleşmesi kullanmak mümkün olsa da, bunu yapmanın önerilen yolu bir ileti sözleşmesi kullanmaktır; bu, sonuçta elde edilen XML 'de gereksiz kaydırma düzeylerini önler. Ayrıca, ileti sözleşmeleri sonuç iletileri üzerinde daha fazla denetim yapmanıza olanak sağlar. Örneğin, ileti gövdesinde hangi bilgi parçalarının olması gerektiğine ve ileti üstbilgilerinde olması gerektiğine karar verebilirsiniz. Aşağıdaki örnek, ileti sözleşmelerinin kullanımını gösterir.  
  
```csharp  
[ServiceContract]  
public interface IAirfareQuoteService  
{  
    [OperationContract]  
    GetAirfareResponse GetAirfare(GetAirfareRequest request);  
}  
  
[MessageContract]  
public class GetAirfareRequest  
{  
    [MessageHeader] public DateTime date;  
    [MessageBodyMember] public Itinerary itinerary;  
}  
  
[MessageContract]  
public class GetAirfareResponse  
{  
    [MessageBodyMember] public float airfare;  
    [MessageBodyMember] public string currency;  
}  
  
[DataContract]  
public class Itinerary  
{  
    [DataMember] public string fromCity;  
    [DataMember] public string toCity;  
}  
```  
  
```vb  
<ServiceContract()>  
Public Interface IAirfareQuoteService  
    <OperationContract()>  
    Function GetAirfare(request As GetAirfareRequest) As GetAirfareResponse  
End Interface  
  
<MessageContract()>  
Public Class GetAirfareRequest  
    <MessageHeader()>   
    Public Property date as DateTime  
    <MessageBodyMember()>  
    Public Property itinerary As Itinerary  
End Class  
  
<MessageContract()>  
Public Class GetAirfareResponse  
    <MessageBodyMember()>  
    Public Property airfare As Double  
    <MessageBodyMember()> Public Property currency As String  
End Class  
  
<DataContract()>  
Public Class Itinerary  
    <DataMember()> Public Property fromCity As String  
    <DataMember()> Public Property toCity As String  
End Class  
```  
  
 Daha fazla bilgi için bkz. [Ileti sözleşmelerini kullanma](../../../../docs/framework/wcf/feature-details/using-message-contracts.md).  
  
 Önceki örnekte, <xref:System.Runtime.Serialization.DataContractSerializer> sınıfı varsayılan olarak hala kullanılmaktadır. @No__t-0 sınıfı ileti sözleşmeleri ile de kullanılabilir. Bunu yapmak için, <xref:System.ServiceModel.XmlSerializerFormatAttribute> özniteliğini işlem ya da sözleşmeye uygulayın ve ileti üstbilgilerinde ve gövde üyelerinde <xref:System.Xml.Serialization.XmlSerializer> sınıfıyla uyumlu türleri kullanın.  
  
## <a name="describing-messages-by-using-streams"></a>Akışları kullanarak Iletileri açıklama  
 İşlemdeki iletileri tanımlamanın bir başka yolu da <xref:System.IO.Stream> sınıfını veya bir işlem sözleşmesindeki türetilmiş sınıflarından birini ya da bir ileti sözleşmesi gövde üyesini (Bu durumda tek üye olmalıdır) kullanmaktır. Gelen iletilerde tür `Stream` olmalıdır; türetilmiş sınıfları kullanamazsınız.  
  
 WCF, seri hale getirici 'yi çağırmak yerine bir akıştan veri alır ve bunu doğrudan giden bir iletiye koyar veya gelen iletiden veri alıp doğrudan bir akışa koyar. Aşağıdaki örnek, akışlarının kullanımını gösterir.  
  
```csharp  
[OperationContract]  
public Stream DownloadFile(string fileName);  
```  
  
```vb  
<OperationContract()>  
Function DownloadFile(fileName As String) As String  
```  
  
 @No__t-0 ve akış olmayan verileri tek bir ileti gövdesinde birleştiremezsiniz. İleti üstbilgilerinde ek verileri yerleştirmek için bir ileti sözleşmesi kullanın. Aşağıdaki örnek, işlem sözleşmesini tanımlarken akış kullanımının yanlış kullanımını gösterir.  
  
```csharp  
//Incorrect:  
// [OperationContract]  
// public void UploadFile (string fileName, Stream fileData);  
```  
  
```vb  
'Incorrect:  
    '<OperationContract()>  
    Public Sub UploadFile(fileName As String, fileData As StreamingContext)  
```  
  
 Aşağıdaki örnek, bir işlem anlaşması tanımlarken akışlarının doğru kullanımını gösterir.  
  
```csharp  
[OperationContract]  
public void UploadFile (UploadFileMessage message);  
//code omitted  
[MessageContract]  
public class UploadFileMessage  
{  
    [MessageHeader] public string fileName;  
    [MessageBodyMember] public Stream fileData;  
}  
```  
  
```vb  
<OperationContract()>  
Public Sub UploadFile(fileName As String, fileData As StreamingContext)  
'Code Omitted  
<MessageContract()>  
Public Class UploadFileMessage  
   <MessageHeader()>  
    Public Property fileName As String  
    <MessageBodyMember()>  
    Public Property fileData As Stream  
End Class  
```  
  
 Daha fazla bilgi için bkz. [büyük veri ve akış](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md).  
  
## <a name="using-the-message-class"></a>İleti Sınıfını Kullanma  
 Gönderilen veya alınan iletiler üzerinde tam programlı denetim sağlamak için, aşağıdaki örnek kodda gösterildiği gibi, <xref:System.ServiceModel.Channels.Message> sınıfını doğrudan kullanabilirsiniz.  
  
```csharp  
[OperationContract]  
public void LogMessage(Message m);  
```  
  
```vb  
<OperationContract()>  
Sub LogMessage(m As Message)  
```  
  
 Bu, [Ileti sınıfını kullanma](../../../../docs/framework/wcf/feature-details/using-the-message-class.md)konusunda ayrıntılı olarak açıklanan gelişmiş bir senaryodur.  
  
## <a name="describing-fault-messages"></a>Hata Iletilerini açıklama  
 Dönüş değeri ve çıkış ya da başvuru parametreleri tarafından tanımlanan iletilere ek olarak, tek yönlü olmayan tüm işlemler en az iki olası ileti döndürebilir: normal yanıt iletisi ve bir hata iletisi. Aşağıdaki işlem sözleşmesini göz önünde bulundurun.  
  
```csharp  
[OperationContract]  
float GetAirfare(string fromCity, string toCity, DateTime date);  
```  
  
```vb  
<OperationContract()>  
Function GetAirfare(fromCity As String, toCity As String, date as DateTime)  
```  
  
 Bu işlem, `float` numarası içeren bir normal ileti ya da hata kodu ve açıklama içeren bir hata iletisi döndürebilir. Bunu, hizmet uygulamanızda bir <xref:System.ServiceModel.FaultException> vererek gerçekleştirebilirsiniz.  
  
 @No__t-0 özniteliğini kullanarak ek olası hata iletileri belirtebilirsiniz. Aşağıdaki örnek kodda gösterildiği gibi, ek hataların <xref:System.Runtime.Serialization.DataContractSerializer> kullanılarak seri hale getirilebilir olması gerekir.  
  
```csharp  
[OperationContract]  
[FaultContract(typeof(ItineraryNotAvailableFault))]  
float GetAirfare(string fromCity, string toCity, DateTime date);  
  
//code omitted  
  
[DataContract]  
public class ItineraryNotAvailableFault  
{  
    [DataMember]  
    public bool IsAlternativeDateAvailable;  
  
    [DataMember]  
    public DateTime alternativeSuggestedDate;  
}  
```  
  
```vb  
<OperationContract()>  
<FaultContract(GetType(ItineraryNotAvailableFault))>  
Function GetAirfare(fromCity As String, toCity As String, date as DateTime) As Double  
  
'Code Omitted  
<DataContract()>  
Public Class  
  <DataMember()>  
  Public Property IsAlternativeDateAvailable As Boolean  
  <DataMember()>  
  Public Property alternativeSuggestedDate As DateTime  
End Class  
```  
  
 Bu ek hatalar, uygun veri sözleşmesi türünün bir @no__t (0) üretilerek oluşturulabilir. Daha fazla bilgi için bkz. [özel durumları ve hataları işleme](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md).  
  
 Hataları anlatmak için <xref:System.Xml.Serialization.XmlSerializer> sınıfını kullanamazsınız. @No__t-0 ' ın hata sözleşmeleri üzerinde hiçbir etkisi yoktur.  
  
## <a name="using-derived-types"></a>Türetilmiş türleri kullanma  
 Bir işlemde veya bir ileti sözleşmesinde temel tür kullanmak ve ardından işlemi çağırırken türetilmiş bir tür kullanmak isteyebilirsiniz. Bu durumda, türetilmiş türlerin kullanılmasına izin vermek için <xref:System.ServiceModel.ServiceKnownTypeAttribute> özniteliğini ya da alternatif bir mekanizmayı kullanmanız gerekir. Aşağıdaki işlemi göz önünde bulundurun.  
  
```csharp  
[OperationContract]  
public bool IsLibraryItemAvailable(LibraryItem item);  
```  
  
```vb
<OperationContract()>  
    Function IsLibraryItemAvailable(item As LibraryItem) As Boolean  
```  
  
 @No__t-0 ve `Magazine` olan iki türün `LibraryItem` ' den türetildiğinden emin varsayın. Bu türleri `IsLibraryItemAvailable` işleminde kullanmak için, işlemi aşağıdaki şekilde değiştirebilirsiniz:  
  
 `[OperationContract]`  
  
 `[ServiceKnownType(typeof(Book))]`  
  
 `[ServiceKnownType(typeof(Magazine))]`  
  
 `public bool IsLibraryItemAvailable(LibraryItem item);`  
  
 Alternatif olarak, aşağıdaki örnek kodda gösterildiği gibi varsayılan <xref:System.Runtime.Serialization.DataContractSerializer> kullanılırken <xref:System.Runtime.Serialization.KnownTypeAttribute> özniteliğini kullanabilirsiniz.  
  
```csharp  
[OperationContract]  
public bool IsLibraryItemAvailable(LibraryItem item);  
  
// code omitted   
  
[DataContract]  
[KnownType(typeof(Book))]  
[KnownType(typeof(Magazine))]  
public class LibraryItem  
{  
    //code omitted  
}  
```  
  
```vb  
<OperationContract()>  
Function IsLibraryItemAvailable(item As LibraryItem) As Boolean  
  
'Code Omitted  
<DataContract()>  
<KnownType(GetType(Book))>  
<KnownType(GetType(Magazine))>  
Public Class LibraryItem  
  'Code Omitted  
End Class  
```  
  
 @No__t-1 kullanırken <xref:System.Xml.Serialization.XmlIncludeAttribute> özniteliğini kullanabilirsiniz.  
  
 @No__t-0 özniteliğini bir işleme veya tüm hizmete uygulayabilirsiniz. @No__t-0 özniteliği gibi bilinen türlerin bir listesini almak için çağrılacak yöntemin türünü ya da adını kabul eder. Daha fazla bilgi için bkz. [veri sözleşmesi bilinen türleri](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md).  
  
## <a name="specifying-the-use-and-style"></a>Kullanımı ve stili belirtme  
 Web Hizmetleri Açıklama Dili (WSDL) kullanarak hizmetleri açıkladığınızda, yaygın olarak kullanılan iki stil belge ve uzak yordam çağrısı (RPC) ' dir. Belge stilinde, tüm ileti gövdesi şema kullanılarak tanımlanır ve WSDL, bu şema içindeki öğelere başvurarak çeşitli ileti gövdesi parçalarını açıklar. RPC stilinde, WSDL bir öğesi yerine her ileti bölümü için bir şema türü anlamına gelir. Bazı durumlarda, bu stillerden birini el ile seçmeniz gerekir. Bunu, <xref:System.ServiceModel.DataContractFormatAttribute> özniteliğini uygulayarak ve `Style` özelliğini ayarlayarak (<xref:System.Runtime.Serialization.DataContractSerializer> kullanılırken) veya <xref:System.ServiceModel.XmlSerializerFormatAttribute> özniteliğinde `Style` ' i ayarlayarak (<xref:System.Xml.Serialization.XmlSerializer> kullanırken) yapabilirsiniz.  
  
 Ayrıca, <xref:System.Xml.Serialization.XmlSerializer> iki sıralı XML biçimini destekler: `Literal` ve `Encoded`. `Literal` en sık kabul edilen formdur ve <xref:System.Runtime.Serialization.DataContractSerializer> ' in desteklediği tek formdur. `Encoded`, SOAP belirtiminin 5. bölümünde açıklanan eski bir formdur ve yeni hizmetler için önerilmez. @No__t-0 moduna geçmek için <xref:System.ServiceModel.XmlSerializerFormatAttribute> özniteliğinde `Use` özelliğini `Encoded` olarak ayarlayın.  
  
 Çoğu durumda, `Style` ve `Use` özellikleri için varsayılan ayarları değiştirmemelisiniz.  
  
## <a name="controlling-the-serialization-process"></a>Serileştirme Işlemini denetleme  
 Verilerin serileştirilme şeklini özelleştirmek için çeşitli şeyler yapabilirsiniz.  
  
### <a name="changing-server-serialization-settings"></a>Sunucu serileştirme ayarlarını değiştirme  
 Varsayılan <xref:System.Runtime.Serialization.DataContractSerializer> kullanımda olduğunda, hizmete <xref:System.ServiceModel.ServiceBehaviorAttribute> özniteliğini uygulayarak serileştirme işleminin bazı yönlerini denetleyebilirsiniz. Özellikle, `MaxItemsInObjectGraph` özelliğini kullanarak <xref:System.Runtime.Serialization.DataContractSerializer> seri hale getirilen en fazla nesne sayısını sınırlayan kotayı ayarlayabilirsiniz. @No__t-0 özelliğini kullanarak gidiş yuvarlama sürümü özelliğini kapatabilirsiniz. Kotalar hakkında daha fazla bilgi için bkz. [veriler Için güvenlik konuları](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md). Gidiş dönüşü hakkında daha fazla bilgi için bkz. [Forward-uyumlu veri sözleşmeleri](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).  
  
```csharp  
[ServiceBehavior(MaxItemsInObjectGraph=100000)]  
public class MyDataService:IDataService  
{  
    public DataPoint[] GetData()  
    {  
       // Implementation omitted  
    }  
}  
```  
  
```vb  
<ServiceBehavior(MaxItemsInObjectGraph:=100000)>  
Public Class MyDataService Implements IDataService  
  
    Function GetData() As DataPoint()  
         ‘ Implementation omitted  
    End Function  
End Interface  
```  
  
### <a name="serialization-behaviors"></a>Serileştirme davranışları  
 WCF 'de iki davranış mevcuttur, <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> ve <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior>, belirli bir işlem için hangi seri hale getiricinin kullanımda olduğuna bağlı olarak otomatik olarak takılır. Bu davranışlar otomatik olarak uygulandığından, normalde bunların farkında olmanız gerekmez.  
  
 Ancak, `DataContractSerializerOperationBehavior`, serileştirme işlemini özelleştirmek için kullanabileceğiniz `MaxItemsInObjectGraph`, `IgnoreExtensionDataObject` ve `DataContractSurrogate` özelliklerine sahiptir. İlk iki özellik, önceki bölümde açıklanan anlama sahiptir. Serileştirme işlemini özelleştirmek ve genişletmek için güçlü bir mekanizma olan veri anlaşması kapılarını etkinleştirmek için `DataContractSurrogate` özelliğini kullanabilirsiniz. Daha fazla bilgi için bkz. [veri sözleşmesi yedeklerin kapıları](../../../../docs/framework/wcf/extending/data-contract-surrogates.md).  
  
 Hem istemci hem de sunucu serileştirmesini özelleştirmek için `DataContractSerializerOperationBehavior` ' yı kullanabilirsiniz. Aşağıdaki örnek, istemcisinde `MaxItemsInObjectGraph` kotasının nasıl arttıralınacağını gösterir.  
  
```csharp  
ChannelFactory<IDataService> factory = new ChannelFactory<IDataService>(binding, address);  
foreach (OperationDescription op in factory.Endpoint.Contract.Operations)  
{  
    DataContractSerializerOperationBehavior dataContractBehavior =  
                op.Behaviors.Find<DataContractSerializerOperationBehavior>()  
                as DataContractSerializerOperationBehavior;  
    if (dataContractBehavior != null)  
    {  
        dataContractBehavior.MaxItemsInObjectGraph = 100000;  
    }  
}  
IDataService client = factory.CreateChannel();  
```  
  
```vb  
Dim factory As ChannelFactory(Of IDataService) = New ChannelFactory(Of IDataService)(binding, address)  
For Each op As OperationDescription In factory.Endpoint.Contract.Operations  
        Dim dataContractBehavior As DataContractSerializerOperationBehavior = op.Behaviors.Find(Of DataContractSerializerOperationBehavior)()  
        If dataContractBehavior IsNot Nothing Then  
            dataContractBehavior.MaxItemsInObjectGraph = 100000  
        End If  
     Next  
    Dim client As IDataService = factory.CreateChannel  
```  
  
Şirket içinde barındırılan durumda, hizmette eşdeğer kod aşağıda verilmiştir:
  
```csharp  
ServiceHost serviceHost = new ServiceHost(typeof(IDataService))  
foreach (ServiceEndpoint ep in serviceHost.Description.Endpoints)  
{  
foreach (OperationDescription op in ep.Contract.Operations)  
{  
        DataContractSerializerOperationBehavior dataContractBehavior =  
           op.Behaviors.Find<DataContractSerializerOperationBehavior>()  
                as DataContractSerializerOperationBehavior;  
        if (dataContractBehavior != null)  
        {  
            dataContractBehavior.MaxItemsInObjectGraph = 100000;  
        }  
}  
}  
serviceHost.Open();  
```  
  
```vb  
Dim serviceHost As ServiceHost = New ServiceHost(GetType(IDataService))  
        For Each ep As ServiceEndpoint In serviceHost.Description.Endpoints  
            For Each op As OperationDescription In ep.Contract.Operations  
                Dim dataContractBehavior As DataContractSerializerOperationBehavior = op.Behaviors.Find(Of DataContractSerializerOperationBehavior)()  
  
                If dataContractBehavior IsNot Nothing Then  
                    dataContractBehavior.MaxItemsInObjectGraph = 100000  
                End If  
            Next  
        Next  
        serviceHost.Open()  
```  
  
 Web 'de barındırılan bir durumda, yeni bir `ServiceHost` türetilmiş sınıf oluşturmanız ve bir hizmet ana bilgisayar fabrikası kullanarak içine takabilirsiniz.  
  
### <a name="controlling-serialization-settings-in-configuration"></a>Yapılandırmada serileştirme ayarlarını denetleme  
 @No__t-0 ve `IgnoreExtensionDataObject`, aşağıdaki örnekte gösterildiği gibi `dataContractSerializer` uç noktası veya hizmet davranışı kullanılarak yapılandırma yoluyla denetlenebilir.  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="LargeQuotaBehavior">  
                    <dataContractSerializer  
                      maxItemsInObjectGraph="100000" />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
        <client>  
            <endpoint address="http://example.com/myservice"  
                  behaviorConfiguration="LargeQuotaBehavior"  
                binding="basicHttpBinding" bindingConfiguration=""   
                            contract="IDataService"  
                name="" />  
        </client>  
    </system.serviceModel>  
</configuration>  
```  
  
### <a name="shared-type-serialization-object-graph-preservation-and-custom-serializers"></a>Paylaşılan tür serileştirme, nesne grafik koruma ve özel serileştiriciler  
 @No__t-0, .NET tür adları değil, veri sözleşmesi adlarını kullanarak serileştirir. Bu, hizmet odaklı mimari olanakları ile tutarlıdır ve harika bir esneklik sağlar; .NET türleri, Tel sözleşmeyi etkilemeden değişebilir. Nadir durumlarda, gerçek .NET tür adlarını seri hale getirmek isteyebilirsiniz ve bu sayede istemci ile sunucu arasında sıkı bir şekilde iletişim kurarak, .NET Framework Remoting teknolojisine benzer. Bu, genellikle .NET Framework uzaktan iletişim 'dan WCF 'ye geçiş yapılırken oluşan nadir durumlar dışında, önerilen bir uygulama değildir. Bu durumda, <xref:System.Runtime.Serialization.DataContractSerializer> sınıfı yerine <xref:System.Runtime.Serialization.NetDataContractSerializer> sınıfını kullanmanız gerekir.  
  
 @No__t-0 normalde nesne grafiklerini nesne ağaçları olarak serileştirir. Diğer bir deyişle, aynı nesneye birden çok kez bahsedildiğinde birden çok kez serileştirilir. Örneğin, adres türü `billTo` ve `shipTo` olarak adlandırılan iki alanı olan bir `PurchaseOrder` örneği düşünün. Her iki alan de aynı adres örneğine ayarlanmışsa serileştirme ve serisini kaldırma sonrasında iki özdeş adres örneği vardır. Bu, XML 'deki nesne grafiklerini temsil etmek için standart birlikte çalışabilen bir yol olmadığından (`Style` ve `Use` ' deki önceki bölümde açıklandığı gibi, <xref:System.Xml.Serialization.XmlSerializer> ' da kullanılabilir olan eski SOAP kodlamalı standart hariç). Ağaç olarak nesne grafiklerinin serileştirilmesi, örneğin döngüsel başvuruları olan grafikler serileştirilemiyor. Bazen, birlikte çalışabilir olmasa bile, doğru nesne grafiği serileştirmesine geçiş yapmak gerekir. Bu işlem, `true` ' ye ayarlanmış `preserveObjectReferences` parametresiyle oluşturulan <xref:System.Runtime.Serialization.DataContractSerializer> kullanılarak yapılabilir.  
  
 Bazen, yerleşik serileştiriciler senaryonuz için yeterli değildir. Çoğu durumda, hem <xref:System.Runtime.Serialization.DataContractSerializer> hem de <xref:System.Runtime.Serialization.NetDataContractSerializer> ' den türetilen <xref:System.Runtime.Serialization.XmlObjectSerializer> soyutlamasını kullanmaya devam edebilirsiniz.  
  
 Önceki üç durum (.NET tür koruma, nesne Graph koruması ve tamamen özel @no__t -0 tabanlı serileştirme) tüm özel bir seri hale getirici takılmasına gerek duyar. Bunu yapmak için şu adımları izleyin:  
  
1. @No__t-0 ' dan türetilen kendi davranışınızı yazın.  
  
2. İki `CreateSerializer` yöntemini geçersiz kılın (<xref:System.Runtime.Serialization.NetDataContractSerializer>, `preserveObjectReferences` olan <xref:System.Runtime.Serialization.DataContractSerializer> ' yi `true` ' e veya kendi özel <xref:System.Runtime.Serialization.XmlObjectSerializer>) döndürür.  
  
3. Hizmet konağını açmadan veya bir istemci kanalı oluşturmadan önce, var olan <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> davranışını kaldırın ve önceki adımlarda oluşturduğunuz özel türetilmiş sınıfı takın.  
  
 Gelişmiş serileştirme kavramları hakkında daha fazla bilgi için bkz. [serileştirme ve seri durumundan çıkarma](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md).  
  
## <a name="see-also"></a>Ayrıca bkz.

- [XmlSerializer Sınıfını Kullanma](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md)
- [Nasıl yapılır: Akışı Etkinleştirme](../../../../docs/framework/wcf/feature-details/how-to-enable-streaming.md)
- [Nasıl yapılır: Bir Sınıf veya Yapı için Temel Bir Veri Anlaşması Oluşturma](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-data-contract-for-a-class-or-structure.md)
