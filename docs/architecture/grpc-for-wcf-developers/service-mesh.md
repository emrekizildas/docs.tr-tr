---
title: Hizmet kafesleri-WCF geliştiricileri için gRPC
description: Bir Kubernetes kümesinde gRPC hizmetlerine istekleri yönlendirmek ve dengelemek için bir hizmet ağı kullanma.
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 7fc80b95937dab9153b72aa6bc8da90f6453779f
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184094"
---
# <a name="service-meshes"></a>Hizmet kafesleri

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Hizmet ağı, bir ağ içindeki yönlendirme hizmeti isteklerinin denetimini alan bir altyapı bileşenidir. Hizmet kafesleri, bir Kubernetes kümesi içindeki her türlü ağ düzeyi kaygılarını işleyebilir, örneğin:

- Hizmet bulma
- Yük Dengeleme
- Hataya dayanıklılık
- Şifreleme
- İzleme

Kubernetes hizmet kafesleri, kafeste bulunan her Pod 'a *sepet proxy 'si*olarak adlandırılan ek bir kapsayıcı ekleyerek çalışır. Ara sunucu tüm gelen ve giden ağ isteklerini işlemeyi, ağ yapılandırma ve yönetiminin önemli bir şekilde uygulama kapsayıcılarından ayrı tutulmasını sağlar ve birçok durumda uygulama kodunda herhangi bir değişiklik yapılmasına gerek kalmadan yapılır.

Web uygulamasındaki gRPC isteklerinin hepsi gRPC hizmetinin tek bir örneğine yönlendirildiği [önceki bölümün örneğini](kubernetes.md#testing-the-application)alın. Bu durum hizmetin ana bilgisayar adının bir IP adresine çözümlenmesi ve bu IP adresinin `HttpClientHandler` Örneğin kullanım ömrü boyunca önbelleğe alınması nedeniyle oluşur. DNS aramalarını el ile veya birden çok istemci oluşturarak bu sorunu geçici olarak çözmek mümkün olabilir, ancak bu, herhangi bir iş veya müşteri değeri eklemeden uygulama kodunu önemli ölçüde karmaşıklaştırır.

Bir hizmet ağı kullanarak, uygulama kapsayıcısından gelen istekler sepet proxy 'sine gönderilir ve bu da bunları diğer hizmetin tüm örneklerine akıllıca dağıtabilen. Kafes de şunları yapabilir:

- Bir hizmetin tek tek örneklerinden oluşan hatalara sorunsuz bir şekilde yanıt verin.
- Başarısız çağrılar veya zaman aşımları için yeniden deneme semantiğini işle
- Başarısız istekleri, istemci uygulamasına hiç döndürülmeksizin alternatif bir örneğe yeniden yönlendir.

Aşağıdaki ekran görüntüsünde, Linkerd hizmet ağıyla çalışan StockWeb uygulaması, uygulama kodunda hiçbir değişiklik yapılmıyor veya hatta kullanılan Docker görüntüsü gösterilmektedir. Gerekli tek değişiklik, `stockdata` ve `stockweb` Hizmetleri için YAML dosyalarındaki dağıtıma ek açıklamanın ekleniydi.

![Hizmet ağı ile StockWeb](media/service-mesh/stockweb-servicemesh-screenshot.png)

StockWeb uygulamasından gelen isteklerin, uygulama kodundaki tek `HttpClient` bir örnekten kaynaklanan StockData hizmetinin her iki çoğaltmasına de yönlendirildiğini sunucu sütunundan görebilirsiniz. Aslında, kodu gözden geçirdikten sonra, StockData Service 'e yönelik tüm 100 isteklerinin aynı örneği kullanarak aynı `HttpClient` anda (hizmet ağı ile) yapıldığını görürsünüz, ancak bu istekler arasında dengelenebilir ve birçok hizmet örneği mevcuttur.

Hizmet kafesleri yalnızca bir küme içindeki trafiğe uygulanır. Dış istemciler için, bkz. bir [sonraki bölüm, Yük Dengeleme](load-balancing.md).

## <a name="service-mesh-options"></a>Hizmet ağ seçenekleri

Şu anda Kubernetes ile kullanılabilecek üç genel amaçlı hizmet kafesi uygulaması vardır: İstio, Linkerd ve Tüketil Connect. Tüm üç istek yönlendirme/proxy sağlama, trafik şifreleme, esnekliği, konaktan konağa kimlik doğrulaması ve trafik denetimi sağlar.

Hizmet kafesi seçme, birden fazla etkene bağlıdır: 

- Kuruluşun maliyetler, uyumluluk, ücretli destek planları vb. için özel gereksinimleri. 
- Kümenin doğası, boyutu, dağıtılan hizmet sayısı ve küme ağı içindeki trafik hacmi.
- Ağı dağıtma ve yönetme kolaylığı ve hizmetlerle kullanma.

Her hizmet ağı hakkında daha fazla bilgiyi ilgili web sitelerinden bulabilirsiniz.

- [**Istio** -istio.io](https://istio.io)
- [**Linkerd** -linkerd.io](https://linkerd.io)
- [**Tüketil** -Consul.io/mesh.html](https://consul.io/mesh.html)

## <a name="example-add-linkerd-to-a-deployment"></a>Örnek: bir dağıtıma Linkerd ekleme

Bu örnekte, [önceki bölümde](kubernetes.md) *StockKube* uygulamasıyla linkerd hizmet ağı 'nı nasıl kullanacağınızı öğreneceksiniz.
Bu örneği izlemek için, [Linkerd CLI 'yı yüklemeniz](https://linkerd.io/2/getting-started/#step-1-install-the-cli)gerekir. Windows ikili dosyaları GitHub yayınları bölümünden indirilebilir; uç sürümlerden birini değil en son **kararlı** yayını kullandığınızdan emin olun.

Linkerd CLı yüklü olduğunda, Kubernetes kümenize Linkerd bileşenlerini yüklemek için [Linkerd Web sitesinde*kullanmaya* başlama yönergeleri ' ni izleyin. Yönergeler doğrudan ileriye doğru ve yükleme, yerel bir Kubernetes örneği üzerinde yalnızca birkaç dakika sürer.

### <a name="add-linkerd-to-kubernetes-deployments"></a>Kubernetes dağıtımlarını Linkerd 'e ekleme

Linkerd CLI, Kubernetes dosyalarına gerekli bölümleri ve özellikleri eklemek için bir `inject` komut sağlar. Komutu çalıştırabilir ve çıktıyı yeni bir dosyaya yazabilirsiniz.

```console
linkerd inject stockdata.yml > stockdata-with-mesh.yml
linkerd inject stockweb.yml > stockweb-with-mesh.yml
```

Yapılan değişiklikleri görmek için yeni dosyaları inceleyebilirsiniz. Dağıtım nesneleri için, Linkerd 'nin oluşturulduğu sırada Pod 'a bir sepet ara sunucu kapsayıcısı eklemesine söylemek için bir meta veri ek açıklaması eklenir.

`linkerd inject` Komutun çıkışını doğrudankanalayöneltmeyide`kubectl` mümkün hale gelir. Aşağıdaki komutlar PowerShell veya herhangi bir Linux kabuğunda çalışır.

```console
linkerd inject stockdata.yml | kubectl apply -f -
linkerd inject stockweb.yml | kubectl apply -f -
```

### <a name="inspect-services-in-the-linkerd-dashboard"></a>Linkerd panosundaki Hizmetleri inceleyin

`linkerd` CLI kullanarak linkerd panosunu başlatın.

```console
linkerd dashboard
```

Pano, ağa bağlı tüm hizmetler hakkında ayrıntılı bilgi sağlar.

![StockKube uygulamalarını gösteren linkerd panosu](media/service-mesh/linkerd-screenshot.png)

Aşağıdaki örnekte gösterildiği gibi StockData gRPC hizmetinin çoğaltmaların sayısını artırabilir ve tarayıcıdaki StockWeb sayfasını yenilediğinizde, sunucu sütununda isteklerin tüm kullanılabilir örneklerle sunulduğunu belirten bir kimlik karışımı görmeniz gerekir. .

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: stockdata
  namespace: stocks
spec:
  selector:
    matchLabels:
      run: stockdata
  replicas: 2 # Increase the target number of instances
  template:
    metadata:
      annotations:
        linkerd.io/inject: enabled
      creationTimestamp: null
      labels:
        run: stockdata
    spec:
      containers:
      - name: stockdata
        image: stockdata:1.0.0
        imagePullPolicy: Never
        resources:
          limits:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 80
```

>[!div class="step-by-step"]
>[Önceki](kubernetes.md)
>[İleri](load-balancing.md)
