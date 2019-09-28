---
title: Biriktirme
ms.date: 03/30/2017
ms.assetid: 688dfb30-b79a-4cad-a687-8302f8a9ad6a
ms.openlocfilehash: 846e93022145495518489e652707e5cb06a9c7e2
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71353339"
---
# <a name="pooling"></a>Biriktirme
Bu örnek, nesne havuzlamayı desteklemek için Windows Communication Foundation (WCF) genişletmeyi gösterir. Örnek, Enterprise Services 'ın `ObjectPoolingAttribute` öznitelik işlevselliğine benzer bir şekilde sözdizimi ve anlamsal olan bir öznitelik oluşturmayı gösterir. Nesne havuzu oluşturma, uygulamanın performansına çarpıcı bir artırma sağlayabilir. Ancak, düzgün bir şekilde kullanılmıyorsa, bu, karşı etkiye sahip olabilir. Nesne havuzu oluşturma, kapsamlı başlatma gerektiren sık kullanılan nesneleri yeniden oluşturma yükünü azaltmaya yardımcı olur. Ancak, havuza alınmış bir nesne üzerindeki bir yönteme yapılan çağrının tamamlanmak için önemli miktarda zaman alırsa, en yüksek havuz boyutuna ulaşıldığında nesne havuzu oluşturma ek istekleri sıraya alır. Bu nedenle, bir zaman aşımı özel durumu oluşturarak bazı nesne oluşturma isteklerine yönelik bir hata verebilir.  
  
> [!NOTE]
> Bu örneğe ilişkin Kurulum yordamı ve derleme yönergeleri bu konunun sonunda bulunur.  
  
 WCF uzantısı oluşturmanın ilk adımı, genişletilebilirlik noktasının kullanılmasına karar vermaktır.  
  
 WCF 'de *dağıtıcı* terimi, gelen iletileri kullanıcının hizmetinde Yöntem etkinleştirmeleri içine dönüştürmeden ve dönüş değerlerini Bu yöntemden giden bir iletiye dönüştürmekten sorumlu bir çalışma zamanı bileşenine başvurur. WCF hizmeti her uç nokta için bir dağıtıcı oluşturur. Bir WCF istemcisinin, bu istemciyle ilişkili sözleşme bir çift yönlü sözleşirse bir dağıtıcı kullanması gerekir.  
  
 Kanal ve uç nokta sevkiyatcılar, Dispatcher 'ın davranışını denetleyen çeşitli özellikleri açığa çıkarmak için kanal ve sözleşme genelinde genişletilebilirlik sağlar. @No__t-0 özelliği ayrıca gönderme işlemini incelemenizi, değiştirmenize veya özelleştirmenize olanak sağlar. Bu örnek, hizmet sınıfının <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A> örneklerini sağlayan nesnesine işaret eden özelliğine odaklanır.  
  
## <a name="the-iinstanceprovider"></a>IInstanceProvider  
 WCF 'de, dağıtıcı, <xref:System.ServiceModel.Dispatcher.IInstanceProvider> arabirimini uygulayan <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A> kullanarak hizmet sınıfının örneklerini oluşturur. Bu arabirimin üç yöntemi vardır:  
  
- <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29>: Bir ileti geldiğinde dağıtıcı iletiyi işlemek için hizmet sınıfının bir örneğini oluşturmak üzere <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29> yöntemini çağırır. Bu yönteme yapılan çağrıların sıklığı, <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> özelliği tarafından belirlenir. Örneğin, <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> özelliği <xref:System.ServiceModel.InstanceContextMode.PerCall> olarak ayarlandıysa, gelen her iletiyi işlemek için yeni bir hizmet sınıfı örneği oluşturulur. bu nedenle, ileti her geldiğinde <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29> çağırılır.  
  
- <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%29>: Bu, bir Ileti bağımsız değişkeni olmadığında çağrılır hariç, önceki yöntemiyle aynıdır.  
  
- <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%28System.ServiceModel.InstanceContext%2CSystem.Object%29>: Bir hizmet örneğinin ömrü geçtiğinde, dağıtıcı <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%28System.ServiceModel.InstanceContext%2CSystem.Object%29> yöntemini çağırır. @No__t-0 yönteminde olduğu gibi, bu yönteme yapılan çağrıların sıklığı <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> özelliği tarafından belirlenir.  
  
## <a name="the-object-pool"></a>Nesne havuzu  
 Özel bir <xref:System.ServiceModel.Dispatcher.IInstanceProvider> uygulamasının, bir hizmet için gereken nesne havuzu semantiğini sağlar. Bu nedenle, bu örnekte havuz için <xref:System.ServiceModel.Dispatcher.IInstanceProvider> ' in özel uygulamasını sağlayan `ObjectPoolingInstanceProvider` türü vardır. @No__t-0 <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29> yöntemini çağırdığında, yeni bir örnek oluşturmak yerine, özel uygulama bellek içi havuzda var olan bir nesneyi arar. Kullanılabilir bir tane varsa, döndürülür. Aksi takdirde, yeni bir nesne oluşturulur. İçin `GetInstance` uygulanması aşağıdaki örnek kodda gösterilmiştir.  
  
```  
object IInstanceProvider.GetInstance(InstanceContext instanceContext, Message message)  
{  
    object obj = null;  
  
    lock (poolLock)  
    {  
        if (pool.Count > 0)  
        {  
            obj = pool.Pop();  
        }  
        else  
        {  
            obj = CreateNewPoolObject();  
        }  
        activeObjectsCount++;  
    }  
  
    WritePoolMessage(ResourceHelper.GetString("MsgNewObject"));  
  
    idleTimer.Stop();  
  
    return obj;            
}  
```  
  
 Özel `ReleaseInstance` uygulama, yayımlanan örneği havuza geri ekler ve `ActiveObjectsCount` değeri azaltır. @No__t-0 farklı iş parçacıklarında bu yöntemleri çağırabilir ve bu nedenle `ObjectPoolingInstanceProvider` sınıfındaki sınıf düzeyi üyelerine eşitlenen erişim gereklidir.  
  
```  
void IInstanceProvider.ReleaseInstance(InstanceContext instanceContext, object instance)  
{  
    lock (poolLock)  
    {  
        pool.Push(instance);  
        activeObjectsCount--;  
  
        WritePoolMessage(  
        ResourceHelper.GetString("MsgObjectPooled"));  
  
        // When the service goes completely idle (no requests   
        // are being processed), the idle timer is started  
        if (activeObjectsCount == 0)  
            idleTimer.Start();                       
    }  
}  
```  
  
 @No__t-0 yöntemi "temiz başlatma" özelliği sağlar. Normalde havuz, havuzun ömrü boyunca en az sayıda nesne tutar. Ancak, yapılandırmada belirtilen en yüksek sınıra ulaşmak için havuzda ek nesneler oluşturulmasını gerektiren aşırı kullanım süreleri olabilir. Sonuç olarak, havuz daha az etkin hale geldiğinde, bu fazlalık nesneler ek bir ek yük haline gelebilir. Bu nedenle, `activeObjectsCount` sıfıra ulaştığında, bir boşta zamanlayıcının tetiklediği ve Temizleme döngüsünü gerçekleştirdiği bir boşta kalma süreölçeri başlatılır.  
  
## <a name="adding-the-behavior"></a>Davranışı ekleme  
 Dağıtıcı katmanı uzantıları aşağıdaki davranışlar kullanılarak bağlanır:  
  
- Hizmet davranışları. Bu, tüm hizmet çalışma zamanının özelleştirilmesine izin verir.  
  
- Uç nokta davranışları. Bu, özellikle bir kanal ve uç nokta dağıtıcısı olan hizmet uç noktalarının özelleştirilmesine izin verir.  
  
- Sözleşme davranışları. Bu, hem <xref:System.ServiceModel.Dispatcher.ClientRuntime> hem de istemci ve hizmet üzerindeki <xref:System.ServiceModel.Dispatcher.DispatchRuntime> sınıflarının özelleştirilmesine izin verir.  
  
 Bir nesne havuzu uzantısının amacı için bir hizmet davranışı oluşturulmalıdır. Hizmet davranışları <xref:System.ServiceModel.Description.IServiceBehavior> arabirimi uygulayarak oluşturulur. Hizmet modelinin özel davranışlardan haberdar olması için çeşitli yollar vardır:  
  
- Özel bir öznitelik kullanma.  
  
- Imperatively, hizmet açıklamasının davranış koleksiyonuna ekleniyor.  
  
- Yapılandırma dosyası genişletiliyor.  
  
 Bu örnek özel bir özniteliği kullanır. @No__t-0 oluşturulduğunda, hizmetin tür tanımında kullanılan öznitelikleri inceler ve kullanılabilir davranışları hizmet açıklamasının davranış koleksiyonuna ekler.  
  
 @No__t-0 arabiriminin içinde üç yöntemi vardır--<xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A>, <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A> ve <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A>. @No__t-0 yöntemi, davranışın hizmete uygulanabileceğini sağlamak için kullanılır. Bu örnekte, uygulama hizmetin <xref:System.ServiceModel.InstanceContextMode.Single> ile yapılandırılmamasını sağlar. @No__t-0 yöntemi, hizmetin bağlamalarını yapılandırmak için kullanılır. Bu senaryoda gerekli değildir. @No__t-0, hizmetin dispatchlarını yapılandırmak için kullanılır. Bu yöntem, <xref:System.ServiceModel.ServiceHost> başlatıldığında WCF tarafından çağırılır. Aşağıdaki parametreler bu yönteme geçirilir:  
  
- `Description`: Bu bağımsız değişken, hizmetin tamamı için hizmet açıklamasını sağlar. Bu, hizmetin uç noktaları, sözleşmeleri, bağlamaları ve diğer veriler hakkındaki açıklama verilerini denetlemek için kullanılabilir.  
  
- `ServiceHostBase`: Bu bağımsız değişken, şu anda başlatılmış olan <xref:System.ServiceModel.ServiceHostBase> ' i sağlar.  
  
 Özel <xref:System.ServiceModel.Description.IServiceBehavior> uygulamasında, `ObjectPoolingInstanceProvider` ' in yeni bir örneği örneklenmiştir ve ServiceHostBase içindeki her <xref:System.ServiceModel.Dispatcher.DispatchRuntime> ' teki <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A> özelliğine atanır.  
  
```  
void IServiceBehavior.ApplyDispatchBehavior(ServiceDescription description, ServiceHostBase serviceHostBase)  
{  
    // Create an instance of the ObjectPoolInstanceProvider.  
    ObjectPoolingInstanceProvider instanceProvider = new  
           ObjectPoolingInstanceProvider(description.ServiceType,   
                                                    minPoolSize);  
  
    // Forward the call if we created a ServiceThrottlingBehavior.  
    if (this.throttlingBehavior != null)  
    {  
        ((IServiceBehavior)this.throttlingBehavior).ApplyDispatchBehavior(description, serviceHostBase);  
    }  
  
    // In case there was already a ServiceThrottlingBehavior   
    // (this.throttlingBehavior==null), it should have initialized   
    // a single ServiceThrottle on all ChannelDispatchers.    
    // As we loop through the ChannelDispatchers, we verify that   
    // and modify the ServiceThrottle to guard MaxPoolSize.  
    ServiceThrottle throttle = null;  
  
    foreach (ChannelDispatcherBase cdb in   
            serviceHostBase.ChannelDispatchers)  
    {  
        ChannelDispatcher cd = cdb as ChannelDispatcher;  
        if (cd != null)  
        {  
            // Make sure there is exactly one throttle used by all   
            // endpoints. If there were others, we could not enforce   
            // MaxPoolSize.  
            if ((this.throttlingBehavior == null) &&   
                        (this.maxPoolSize != Int32.MaxValue))  
            {  
                throttle ??= cd.ServiceThrottle;
                if (cd.ServiceThrottle == null)  
                {  
                    throw new   
InvalidOperationException(ResourceHelper.GetString("ExNullThrottle"));  
                }  
                if (throttle != cd.ServiceThrottle)  
                {  
                    throw new InvalidOperationException(ResourceHelper.GetString("ExDifferentThrottle"));  
                }  
             }  
  
             foreach (EndpointDispatcher ed in cd.Endpoints)  
             {  
                 // Assign it to DispatchBehavior in each endpoint.  
                 ed.DispatchRuntime.InstanceProvider =   
                                      instanceProvider;  
             }  
         }  
     }  
  
     // Set the MaxConcurrentInstances to limit the number of items   
     // that will ever be requested from the pool.  
     if ((throttle != null) && (throttle.MaxConcurrentInstances >   
                                      this.maxPoolSize))  
     {  
         throttle.MaxConcurrentInstances = this.maxPoolSize;  
     }  
}  
```  
  
 Bir <xref:System.ServiceModel.Description.IServiceBehavior> uygulamaya ek olarak, <xref:System.EnterpriseServices.ObjectPoolingAttribute> sınıfı öznitelik bağımsız değişkenlerini kullanarak nesne havuzunu özelleştirmek için çeşitli üyelere sahiptir. Bu Üyeler, .NET Enterprise Services tarafından sunulan nesne havuzu özellik kümesini eşleştirmek için <xref:System.EnterpriseServices.ObjectPoolingAttribute.MaxPoolSize%2A>, <xref:System.EnterpriseServices.ObjectPoolingAttribute.MinPoolSize%2A> ve <xref:System.EnterpriseServices.ObjectPoolingAttribute.CreationTimeout%2A> ' yi içerir.  
  
 Nesne havuzu oluşturma davranışı artık yeni oluşturulan özel `ObjectPooling` öznitelikle hizmet uygulamasına ek olarak bir WCF hizmetine eklenebilir.  
  
```  
[ObjectPooling(MaxPoolSize=1024, MinPoolSize=10, CreationTimeout=30000)]      
public class PoolService : IPoolService  
{  
  // …  
}  
```  
  
## <a name="running-the-sample"></a>Örnek çalıştırma  
 Örnek, belirli senaryolarda nesne havuzu kullanarak kazanılabilir performans avantajlarını gösterir.  
  
 Hizmet uygulaması iki hizmet uygular--`WorkService` ve `ObjectPooledWorkService`. Her iki hizmet de aynı uygulamayı paylaşır; her ikisi de pahalı başlatma gerektirir ve görece bir `DoWork()` yöntemi kullanıma sunar. Tek fark, `ObjectPooledWorkService` ' ın bir nesne havuzlama yapılandırması vardır:  
  
```  
[ObjectPooling(MinPoolSize = 0, MaxPoolSize = 5)]  
public class ObjectPooledWorkService : IDoWork  
{  
    public ObjectPooledWorkService()  
    {  
        Thread.Sleep(5000);  
        ColorConsole.WriteLine(ConsoleColor.Blue, "ObjectPooledWorkService instance created.");  
    }  
  
    public void DoWork()  
    {  
        ColorConsole.WriteLine(ConsoleColor.Blue, "ObjectPooledWorkService.GetData() completed.");  
    }          
}  
```  
  
 İstemcisini çalıştırdığınızda, `WorkService` 5 kez çağıran BT süresi. Daha sonra `ObjectPooledWorkService` 5 kez çağırır. Zaman içindeki fark daha sonra görüntülenir:  
  
```  
Press <ENTER> to start the client.  
  
Calling WorkService:  
1 - DoWork() Done  
2 - DoWork() Done  
3 - DoWork() Done  
4 - DoWork() Done  
5 - DoWork() Done  
Calling WorkService took: 26722 ms.  
Calling ObjectPooledWorkService:  
1 - DoWork() Done  
2 - DoWork() Done  
3 - DoWork() Done  
4 - DoWork() Done  
5 - DoWork() Done  
Calling ObjectPooledWorkService took: 5323 ms.  
Press <ENTER> to exit.  
```  
  
> [!NOTE]
> İstemci her iki hizmet de ilk kez çalıştırıldığında aynı süre içinde olacak şekilde görünür. Örneği yeniden çalıştırırsanız, bu nesnenin bir örneği zaten havuzda bulunduğundan `ObjectPooledWorkService` ' ın çok daha hızlı döndürdüğünden emin olabilirsiniz.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Örneği ayarlamak, derlemek ve çalıştırmak için  
  
1. [Windows Communication Foundation Örnekleri Için tek seferlik Kurulum yordamını](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)gerçekleştirdiğinizden emin olun.  
  
2. Çözümü derlemek için [Windows Communication Foundation örnekleri oluşturma](../../../../docs/framework/wcf/samples/building-the-samples.md)bölümündeki yönergeleri izleyin.  
  
3. Örneği tek veya bir çapraz makine yapılandırmasında çalıştırmak için [Windows Communication Foundation Örnekleri çalıştırma](../../../../docs/framework/wcf/samples/running-the-samples.md)bölümündeki yönergeleri izleyin.  
  
> [!NOTE]
> Bu örneğe yönelik yapılandırmayı yeniden oluşturmak için Svcutil. exe ' yi kullanırsanız, istemci yapılandırmasındaki uç nokta adını istemci koduyla eşleşecek şekilde değiştirdiğinizden emin olun.  
  
> [!IMPORTANT]
> Örnekler makinenizde zaten yüklü olabilir. Devam etmeden önce aşağıdaki (varsayılan) dizini denetleyin.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> Bu dizin yoksa, tüm Windows Communication Foundation (WCF) ve [!INCLUDE[wf1](../../../../includes/wf1-md.md)] örnekleri indirmek için [Windows Communication Foundation (WCF) ve Windows Workflow Foundation (WF) örneklerine .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) ' e gidin. Bu örnek, aşağıdaki dizinde bulunur.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Pooling`  
