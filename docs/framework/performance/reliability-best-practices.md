---
title: Güvenilirlik En İyi Yöntemleri
ms.date: 03/30/2017
helpviewer_keywords:
- marking locks
- rebooting databases
- denial of service attacks
- back-out code
- SQL Server [.NET Framework], reliability
- synchronization, reliability
- single-threaded COM components
- slow leaks
- suspending threads
- asynchronous exception handling
- leaked resources [.NET Framework]
- unmanaged memory
- memory, reliability
- threading [.NET Framework], reliability
- process-wide domain shared states
- shared states
- SafeHandle class, reliability
- reliability contracts [.NET Framework]
- cleanup operations
- constrained execution regions
- CERs
- finalizers, reliability
- reliability [.NET Framework]
- blocks, reliability
- finally clauses
- cross-application domain shared states
- catch blocks
- identifying locks
- writing reliable code
- impersonation
- GC.KeepAlive method
- managed threading
- locks, reliability
- STA-dependent features
- fibers
ms.assetid: cf624c1f-c160-46a1-bb2b-213587688da7
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 40c1b98f82fe53819edc437bbac575c1df206496
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834537"
---
# <a name="reliability-best-practices"></a>Güvenilirlik En İyi Yöntemleri

Aşağıdaki güvenilirlik kuralları SQL Server için yönelimlidir; Ancak, bunlar ana bilgisayar tabanlı sunucu uygulamaları için de geçerlidir. SQL Server gibi sunucularda kaynakları sızıntı ve bunların yapılmaması çok önemlidir.  Ancak, bir nesnenin durumunu değiştiren her yöntem için geri dönüş kodu yazılarak gerçekleştirilemez.  Amaç, her konumdaki herhangi bir hatalardan geri dönüş kodu ile kurtarılacak, yüzde 100 güvenilir yönetilen kod yazmak değildir.  Bu, kısa bir süre sonra çok düşük bir görev olacaktır.  Ortak dil çalışma zamanı (CLR), mükemmel kod yazmayı olanaklı hale getirmek için, yönetilen koda kolayca güçlü bir garanti sağlayamaz.  ASP.NET aksine SQL Server, bir veritabanını kabul edilemez bir süre için bir veritabanı kapatılmadan geri dönüştürülmeden yalnızca bir işlem kullandığını unutmayın.

Bu daha zayıf garanti ve tek bir işlemde çalışırken, güvenilirlik, gerekli olduğunda iş parçacıklarını sonlandırarak veya uygulama etki alanlarını geri dönüşüme göre yapılır ve işlemler ya da bellek gibi işletim sistemi kaynaklarının sızmasını sağlamak için önlemler alır.  Bu daha basit bir güvenilirlik kısıtlaması olsa da, önemli bir güvenilirlik gereksinimi de vardır:

- İşletim sistemi kaynaklarını hiçbir şekilde sızıntı.

- Tüm formlardaki tüm yönetilen kilitleri CLR 'ye belirler.

- Çapraz uygulama etki alanı paylaşılan durumunu hiçbir şekilde kesmeyin, <xref:System.AppDomain> geri dönüşüme sorunsuz bir şekilde çalışmasını sağlar.

@No__t-0, <xref:System.StackOverflowException> ve <xref:System.OutOfMemoryException> özel durumları işlemek üzere yönetilen kod yazmak teorik olsa da, geliştiricilerin tüm uygulama genelinde bu tür güçlü kodları yazması beklenmez.  Bu nedenle, bant dışı özel durumlar, yürütülmekte olan iş parçacığının sonlandırılmasının sonucu olarak sonuçlanır; ve sonlandırılan iş parçacığı paylaşılan durum düzenleiyorsa, iş parçacığının bir kilit içerip içermediğini tespit edebilir, <xref:System.AppDomain> ' ı kaldırılır.  Paylaşılan durumu düzenleyen bir yöntem sonlandırıldığında, paylaşılan duruma güncelleştirmeler için güvenilir bir geri alma kodu yazılması mümkün olmadığından durum bozuk olur.

.NET Framework sürüm 2,0 ' de, güvenilirlik gerektiren tek konak SQL Server.  Derlemeniz üzerinde çalışacağınızı SQL Server, veritabanında çalışırken devre dışı bırakılan belirli özellikler olsa bile, bu derlemenin her bölümü için güvenilirlik işini yapmalısınız.  Kod Analizi altyapısı kodu derleme düzeyinde incelediği ve devre dışı bırakılan kodu ayırt edemediği için bu gereklidir. Başka bir SQL Server programlama, SQL Server her şeyi tek bir işlemde çalıştırmasının yanı sıra bellek ve işletim sistemi tanıtıcıları gibi tüm kaynakları temizlemek için <xref:System.AppDomain> geri dönüştürme kullanılır.

Sonlandırıcılar veya Yıkıcılar ya da geri dönüş kodu için `try/finally` bloklarına bağlı olamaz. Bunlar kesintiye uğramış veya çağrılmayabilir.

Zaman uyumsuz özel durumlar beklenmeyen konumlarda, büyük olasılıkla her makine yönergesi: <xref:System.Threading.ThreadAbortException>, <xref:System.StackOverflowException> ve <xref:System.OutOfMemoryException> olabilir.

Yönetilen iş parçacıklarının SQL 'de Win32 iş parçacığı olmaması gerekmez; Bunlar fibers olabilir.

İşlem genelinde veya çapraz uygulama etki alanı kesilebilir paylaşılan durum güvenli bir şekilde değiştirilebilir ve mümkün olduğunda kaçınılmalıdır.

Yetersiz bellek koşulları SQL Server nadir değildir.

SQL Server ' de barındırılan kitaplıklar paylaşılan durumlarını doğru güncelleştirmediğinden, veritabanı yeniden başlatılana kadar kodun kurtarılmaması büyük bir olasılık olur.  Ayrıca, bazı çok büyük durumlarda bu durum SQL Server işleminin başarısız olmasına neden olabilir ve veritabanının yeniden başlatılmasına neden olabilir.  Veritabanının yeniden başlatılması bir Web sitesi alabilir veya şirket işlemlerini, kullanım dışı bir şekilde etkileyebilir.  Bellek veya tanıtıcı gibi işletim sistemi kaynaklarının yavaş sızıntısı, sunucunun, bir kurtarma işlemi olmadan bir veya daha fazla performans düşmesine neden olabilir veya bir müşterinin uygulamasını azaltabilecek sonrası.  Bu senaryolarınızı açıkça önlemek istiyoruz.

## <a name="best-practice-rules"></a>En iyi yöntem kuralları

Sunucuda çalışan yönetilen koda yönelik kod incelemesinin, Framework 'ün kararlılığını ve güvenilirliğini artırmak için yakalayabilecekleri tanıtım. Tüm bu denetimler, genel olarak iyi bir uygulamadır ve sunucuda bir mutlak olmalıdır.

Kullanılmayan bir kilit veya kaynak kısıtlaması tarafında SQL Server, bir iş parçacığını iptal eder veya bir @no__t (0).  Bu durumda, yalnızca kısıtlı yürütme bölgesindeki (CER) bir yedek kodun çalıştırılması garanti edilir.

### <a name="use-safehandle-to-avoid-resource-leaks"></a>Kaynak sızıntılarını önlemek için SafeHandle kullanın

@No__t-0 ' ı bir kaldırma durumunda, yürütülen `finally` bloklarında veya sonlandırıcılara bağlı olarak, <xref:System.IntPtr>, <xref:System.Runtime.InteropServices.HandleRef> veya benzer sınıflar yerine <xref:System.Runtime.InteropServices.SafeHandle> sınıfı aracılığıyla tüm işletim sistemi kaynak erişiminin soyut olması önemlidir. Bu, CLR 'nin <xref:System.AppDomain> koparma durumunda bile kullandığınız tutamaçları izlemesine ve kapatılmasına izin verir.  <xref:System.Runtime.InteropServices.SafeHandle>, CLR 'nin her zaman çalışacağı kritik bir Sonlandırıcı kullanacaktır.

İşletim sistemi tanıtıcısı, serbest bırakılana kadar, oluşturulduğu andan itibaren güvenli tanıtıcıda depolanır.  Bir tutamacı sızmak için <xref:System.Threading.ThreadAbortException> olabileceği bir pencere yoktur.  Buna ek olarak, platform Invoke, tanıtıcının yaşam süresini izlemeye izin veren tanıtıcı sayısını, `Dispose` ve şu anda tanıtıcıyı kullanan bir yöntemi arasında yarış durumu ile ilgili bir güvenlik sorununu önler.

Yalnızca bir işletim sistemi işleyicisini temizlemek için bir sonlandırıcısı olan çoğu sınıf artık sonlandırıcıyı gerektirmez. Bunun yerine, Sonlandırıcı <xref:System.Runtime.InteropServices.SafeHandle> türetilmiş sınıfında olur.

@No__t-0 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> ' in yerini almaz.  İşletim sistemi kaynaklarını açıkça atılırken hala olası kaynak çekişmesi ve performans avantajları vardır.  Yalnızca kaynakların açıkça atılırken `finally` bloklarının tamamlanmasını yürütülemeyebilir.

<xref:System.Runtime.InteropServices.SafeHandle>, bir işletim sistemi tutamacı boşaltma veya bir döngüde bir dizi tutamacı boşaltma gibi tanıtıcıyı serbest bırakmak için çalışmayı gerçekleştiren kendi <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> yönteminizi uygulamanıza olanak tanır.  CLR bu yöntemin çalıştırılmasını garanti eder.  Bu, tanıtıcının tüm koşullarda serbest bırakılacağını sağlamak için <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> uygulamasının yazarının sorumluluğundadır. Bunun yapılmaması, tanıtıcının sızmasına neden olur, bu da genellikle tanıtıcıyla ilişkili yerel kaynakların sızıntısını sağlar. Bu nedenle <xref:System.Runtime.InteropServices.SafeHandle> türetilmiş sınıfları, <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> uygulamasının çağırma sırasında kullanılamayan kaynakların ayrılmasını gerektirmeyecek şekilde yapılandırmak önemlidir. Kodunuzun bu sorunları işleyebilmesi ve yerel tanıtıcıyı serbest bırakmak için sözleşmeyi tamamlamasıdır <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> ' ın uygulanması içinde başarısız olabilecek Yöntemler çağırma yöntemine izin verildiğine unutmayın. Hata ayıklama amacıyla, <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> ' a bir <xref:System.Boolean> dönüş değeri bulunur ve bu, kaynağın yayınlanmasını engelleyen çok zararlı bir hatayla karşılaşılırsa `false` olarak ayarlanabilir. Bunun yapılması, sorunu tanımlamaya yardımcı olması için, etkinleştirilirse [releaseHandleFailed](../debug-trace-profile/releasehandlefailed-mda.md) MDA öğesini etkinleştirir. Çalışma zamanını başka hiçbir şekilde etkilemez; <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> aynı kaynak için yeniden çağrılmaz ve bu nedenle tanıtıcı sızacaktır.

<xref:System.Runtime.InteropServices.SafeHandle>, belirli bağlamlarda uygun değildir.  @No__t-0 yöntemi bir <xref:System.GC> Sonlandırıcı iş parçacığında çalıştırılabileceğinizden, belirli bir iş parçacığında serbest olması gereken tüm tutamaçlar <xref:System.Runtime.InteropServices.SafeHandle> ' ye sarmalanmamalıdır.

Çalışma zamanı çağrılabilir sarmalayıcılar (RCWs) ek kod olmadan CLR tarafından temizlenebilir.  Platform Invoke kullanan ve bir COM nesnesini `IUnknown*` veya <xref:System.IntPtr> olarak karşılayan kod için, kodun bir RCW kullanması için yeniden yazılması gerekir.  yönetilen koda geri çağıran yönetilmeyen bir yayın yönteminin olasılığı nedeniyle <xref:System.Runtime.InteropServices.SafeHandle> Bu senaryo için yeterli olmayabilir.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

İşletim sistemi kaynaklarını kapsüllemek için <xref:System.Runtime.InteropServices.SafeHandle> kullanın. @No__t-0 veya <xref:System.IntPtr> türündeki alanları kullanmayın.

### <a name="ensure-finalizers-do-not-have-to-run-to-prevent-leaking-operating-system-resources"></a>İşletim sistemi kaynaklarının sızmasını engellemek için sonlandırıcılardan çalıştırmak zorunda olmadığından emin olun

Sonlandırıcılarınızı dikkatlice inceleyerek, çalıştırılmasa bile önemli bir işletim sistemi kaynağı sızdırılmaz.  Normal @no__t 'den farklı olarak, uygulama kararlı bir durumda yürütülürken veya SQL Server gibi bir sunucu kapandığında, nesneler ani bir <xref:System.AppDomain> bellekten sonlandırılmaz.  Bir uygulamanın doğruluğu garanti edilemez, ancak sunucunun bütünlüğü, kaynak sızıntısı olmadan tutulması gerektiğinden, kaynakların bir ani kaldırma durumunda sızdırılmadığından emin olun.  Herhangi bir işletim sistemi kaynağını boşaltmak için <xref:System.Runtime.InteropServices.SafeHandle> kullanın.

### <a name="ensure-that-finally-clauses-do-not-have-to-run-to-prevent-leaking-operating-system-resources"></a>İşletim sistemi kaynaklarının sızmasını engellemek için finally yan tümcelerinin çalıştırmak zorunda olmadığından emin olun

`finally` yan tümcelerinin CERs dışında çalışması garanti edilmez. Bu, kitaplık geliştiricilerinin yönetilmeyen kaynakları serbest bırakmak için bir `finally` bloğunda kod dayanmasına gerek yoktur.  @No__t-0 kullanılması önerilen çözümdür.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

@No__t-1 yerine işletim sistemi kaynaklarını temizlemek için <xref:System.Runtime.InteropServices.SafeHandle> kullanın. @No__t kullanmayın-0; kaynakları kapsüllemek için <xref:System.Runtime.InteropServices.SafeHandle> kullanın. Finally yan tümcesinin çalışması gerekiyorsa, bunu bir CER içine koyun.

### <a name="all-locks-should-go-through-existing-managed-locking-code"></a>Tüm kilitler mevcut yönetilen kilitleme kodu ' na gitmelidir

CLR, kod bir kilit içinde olduğunda, yalnızca iş parçacığını iptal etmek yerine <xref:System.AppDomain> ' ın yok etmek için bir kilit içinde olduğunda bilmelidir.  İş parçacığı tarafından çalıştırılan veriler tutarsız bir durumda bırakılmış olduğundan iş parçacığını iptal etmek tehlikeli olabilir. Bu nedenle, tüm <xref:System.AppDomain> ' ın geri dönüştürülmesi gerekir.  Bir kilidi tespit etmek için başarısız olma sonuçları kilitlenmeler veya hatalı sonuçlar olabilir. Kilit bölgelerini belirlemek için <xref:System.Threading.Thread.BeginCriticalRegion%2A> ve <xref:System.Threading.Thread.EndCriticalRegion%2A> yöntemlerini kullanın.  Yalnızca geçerli iş parçacığına uygulanan <xref:System.Threading.Thread> sınıfında statik yöntemlerdir, bir iş parçacığının başka bir iş parçacığının kilit sayısını düzenlemesini önlemeye yardımcı olur.

<xref:System.Threading.Monitor.Enter%2A> ve <xref:System.Threading.Monitor.Exit%2A> ' de bu CLR bildirimi yerleşik olarak bulunur, bu nedenle kullanımları ve bu yöntemleri kullanan [Lock ifadesinin](../../csharp/language-reference/keywords/lock-statement.md)kullanımı önerilir.

Döndürme kilitleri ve <xref:System.Threading.AutoResetEvent> gibi diğer kilitleme mekanizmaları, CLR 'ye kritik bir bölümün girildiğini bildirmek için bu yöntemleri çağırmalıdır.  Bu yöntemler herhangi bir kilit almaz; kritik bir bölümde kodun yürütüldüğü CLR 'yi bilgilendirir ve iş parçacığını iptal etmek paylaşılan durumu tutarsız bırakabilir.  Özel bir <xref:System.Threading.ReaderWriterLock> sınıfı gibi kendi kilit türünü tanımladıysanız, bu kilit sayısı yöntemlerini kullanın.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

@No__t-0 ve <xref:System.Threading.Thread.EndCriticalRegion%2A> kullanarak tüm kilitleri işaretleyin ve belirler. @No__t-0, <xref:System.Threading.Interlocked.Increment%2A> ve <xref:System.Threading.Interlocked.Decrement%2A> ' yi bir döngüde kullanmayın.  Bu yöntemlerin Win32 türevleri için platform çağırma kullanmayın.  Bir döngüde <xref:System.Threading.Thread.Sleep%2A> kullanmayın.  Geçici alanları kullanmayın.

### <a name="cleanup-code-must-be-in-a-finally-or-a-catch-block-not-following-a-catch"></a>Temizleme kodu bir catch ve catch bloğunda olmalıdır, catch takip edilmez

Temizleme kodu asla `catch` bloğunu izlemelidir; `finally` veya `catch` bloğunda olması gerekir. Bu, normal bir iyi uygulama olmalıdır. Bir özel durum oluştuğunda ve `try` bloğunun sonuna rastlamadığında aynı kodu çalıştırdığı için genellikle `finally` bloğu tercih edilir.  Beklenmeyen bir özel durum oluştuğunda (örneğin, <xref:System.Threading.ThreadAbortException>), temizleme kodu çalışmaz.  @No__t-0 ' da temizleyene kadar tüm yönetilmeyen kaynaklar, sızıntıları engellemek için ideal olarak bir <xref:System.Runtime.InteropServices.SafeHandle> ile sarmalanmalıdır.  C# @No__t-1 anahtar sözcüğünün tutamaçlar dahil olmak üzere nesneleri atmak için etkili bir şekilde kullanılabileceğini aklınızda bulabilirsiniz.

@No__t-0 geri dönüşümü sonlandırıcının iş parçacığında kaynakları temizleyebilse de, temizleme kodunu doğru yere yerleştirmek de önemlidir. Bir iş parçacığı kilidi olmayan bir zaman uyumsuz özel durum alırsa, CLR @no__t geri dönüştürmek zorunda kalmadan iş parçacığının kendisini sonlandırmayı dener.  Kaynakların daha sonra daha önce temizlenmesini sağlamak yerine daha fazla kaynak kullanılabilir hale getirerek ve yaşam süresini daha iyi yönetebilmenizi sağlar. Bazı hata kodu yollarındaki bir dosya işleyicisini açık bir şekilde kapatmadıysanız <xref:System.Runtime.InteropServices.SafeHandle> sonlandırıcının temizlenmesi için bekleyin, bu işlem sonlandırıcının zaten çalıştırılmamasından sonra tam olarak aynı dosyaya erişmeye çalışmayabilir.  Bu nedenle, temizleme kodunun var olduğunu ve düzgün çalışmasını sağlamak, kesin olarak gerekli olmasa bile hatalardan daha düzgün ve hızlı bir şekilde kurtarılmasına yardımcı olur.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

@No__t-0 ' dan sonra temizleme kodu bir `finally` bloğunda olması gerekir. Finally bloğunda Dispose için çağrılar yerleştir. `catch` blokları throw veya Rethrow ile bitmelidir. Çok sayıda özel durum alabileceğiniz yerde bir ağ bağlantısının yapılıp yapılmayacağını algılayan kod gibi özel durumlar da olsa da, normal koşullarda bir dizi özel durum yakalamak gerektiren tüm kodlar bir kodun başarılı olup olmadığını görmek için test edilmiş olması gerektiğini belirtir.

### <a name="process-wide-mutable-shared-state-between-application-domains-should-be-eliminated-or-use-a-constrained-execution-region"></a>Uygulama etki alanları arasında işlem genelindeki kesilebilir paylaşılan durum, elemeli veya kısıtlı bir yürütme bölgesi kullanmalıdır

Giriş bölümünde açıklandığı gibi, uygulama etki alanları genelinde işlem genelinde paylaşılan durumları güvenli bir şekilde izleyen yönetilen kodu yazmak çok zor olabilir.  İşlem genelinde paylaşılan durum, uygulama etki alanları arasında, Win32 kodunda, CLR içinde veya uzaktan iletişim kullanılarak yönetilen kodda paylaşılan bir veri yapısı sıralarından oluşur.  Herhangi bir kesilebilir paylaşılan durum, yönetilen kodda doğru şekilde yazılması çok zordur ve statik paylaşılan durum yalnızca harika bir sorun ile yapılabilir.  İşlem genelinde veya makine genelinde paylaşılan durumdaysa, bu dosyayı ortadan kaldırmanın veya kısıtlanmış bir yürütme bölgesi (CER) kullanarak paylaşılan durumu korumanın bir yolunu bulun.  Tanımlanmayan ve düzeltilen paylaşılan duruma sahip tüm kitaplık SQL Server, temizleme <xref:System.AppDomain> ' ı temizleme için kaldırma gerektiren bir konağa neden olabileceğini unutmayın.

Kod bir COM nesnesi kullanıyorsa, bu COM nesnesinin uygulama etki alanları arasında paylaşılmasını önleyin.

### <a name="locks-do-not-work-process-wide-or-between-application-domains"></a>Kilitler işlem genelinde veya uygulama etki alanları arasında çalışmaz.

Geçmişte, <xref:System.Threading.Monitor.Enter%2A> ve [Lock deyimleri](../../csharp/language-reference/keywords/lock-statement.md) genel işlem kilitleri oluşturmak için kullanılır.  Örneğin, bu durum, paylaşılmayan derlemelerden <xref:System.Type> örnekleri, <xref:System.Threading.Thread> nesneleri, yerleşik dizeler ve uzaktan iletişim kullanılarak uygulama etki alanları arasında paylaşılan bazı dizeler gibi <xref:System.AppDomain> çevik sınıflarında kilitlenirken oluşur.  Bu kilitler artık işlem genelinde değildir.  İşlem genelinde bir uygulama etki alanı kilidinin varlığını belirlemek için, kilit içindeki kodun diskteki bir dosya veya muhtemelen bir veritabanı gibi herhangi bir harici, kalıcı kaynak kullanıp kullanmadığını belirler.

@No__t-0 ' dan kilit alınması, korunan kod bir dış kaynak kullanıyorsa, bu kod birden çok uygulama etki alanında eşzamanlı olarak çalıştırılabildiğinden sorun oluşmasına neden olabilir.  Bu, bir günlük dosyasına yazarken veya tüm işlem için bir yuvaya bağlamakla ilgili bir sorun olabilir.  Bu değişiklikler, adlandırılmış bir <xref:System.Threading.Mutex> veya <xref:System.Threading.Semaphore> örneği kullanmaktan başka bir işlem genel kilidi almak için, yönetilen kod kullanmanın kolay bir yolu olmadığı anlamına gelir.  Aynı anda iki uygulama etki alanında çalıştırmayan kodu oluşturun veya <xref:System.Threading.Mutex> veya <xref:System.Threading.Semaphore> sınıflarını kullanın.  Varolan kod değiştirilemediğinden, bu eşitlemeye ulaşmak için Win32 adlı bir mutex kullanmayın çünkü fiber modda çalıştırmak, aynı işletim sistemi iş parçacığının bir mutex 'i elde edeceğini ve yayınlamadığını garanti edemeyeceğiniz anlamına gelir.  Kod kilidini, yönetilmeyen kod kullanarak kilidi eşitlemek yerine CLR 'nin farkında olacak şekilde eşitlemek için, yönetilen <xref:System.Threading.Mutex> sınıfını veya adlandırılmış bir <xref:System.Threading.ManualResetEvent>, <xref:System.Threading.AutoResetEvent> veya bir <xref:System.Threading.Semaphore> ' ü kullanmanız gerekir.

#### <a name="avoid-locktypeofmytype"></a>Kilit kullanmaktan kaçının (typeof (MyType))

Tüm uygulama etki alanları genelinde paylaşılan derlemelerin yalnızca bir kopyasına sahip paylaşılan derlemelerdeki özel ve genel <xref:System.Type> nesneleri de sorunlar var.  Paylaşılan derlemeler için, işlem başına <xref:System.Type> ' ın yalnızca bir örneği vardır. Bu, birden çok uygulama etki alanının tam aynı <xref:System.Type> örneğini paylaştığı anlamına gelir.  @No__t-0 örneğinde kilit alınması, yalnızca <xref:System.AppDomain> değil, tüm işlemi etkileyen bir kilit alır.  Bir <xref:System.AppDomain> <xref:System.Type> nesnesi üzerinde kilit alırsa, bu iş parçacığı aniden iptal edildiğinde kilidi serbest bırakmaz.  Bu kilit daha sonra diğer uygulama etki alanlarının kilitlenmesine neden olabilir.

Statik yöntemlerde kilit almanın iyi bir yolu, koda statik bir iç eşitleme nesnesi eklemekten oluşur.  Bu, bir tane varsa sınıf oluşturucusunda başlatılabilir, ancak şu şekilde başlatılabilir:

```csharp
private static Object s_InternalSyncObject;
private static Object InternalSyncObject
{
    get
    {
        if (s_InternalSyncObject == null)
        {
            Object o = new Object();
            Interlocked.CompareExchange(
                ref s_InternalSyncObject, o, null);
        }
        return s_InternalSyncObject;
    }
}
```

Ardından bir kilit alırken, kilitlenecek bir nesne almak için `InternalSyncObject` özelliğini kullanın.  Sınıf oluşturucuda iç eşitleme nesnesini oluşturduysanız özelliğini kullanmanız gerekmez.  Çift denetim kilidi başlatma kodu şu örnekteki gibi görünmelidir:

```csharp
public static MyClass SingletonProperty
{
    get
    {
        if (s_SingletonProperty == null)
        {
            lock(InternalSyncObject)
            {
                // Do not use lock(typeof(MyClass))
                if (s_SingletonProperty == null)
                {
                    MyClass tmp = new MyClass(…);
                    // Do all initialization before publishing
                    s_SingletonProperty = tmp;
                }
            }
        }
        return s_SingletonProperty;
    }
}
```

#### <a name="a-note-about-lockthis"></a>Kilit (Bu) ile ilgili bir nota

Genel olarak erişilebilen tek bir nesne üzerinde kilit almak için genellikle kabul edilebilir.  Ancak nesne, tüm alt sistemin kilitlenmesine neden olabilecek bir tekil nesnedeyse, yukarıdaki tasarım modelini de kullanmayı göz önünde bulundurun.  Örneğin, bir <xref:System.Security.SecurityManager> nesnesi üzerindeki bir kilit, @no__t 2 ' nin tamamını kullanılamaz hale getirmek <xref:System.AppDomain> içinde kilitlenmeyle sonuçlanabilir. Bu türden herkese açık erişilebilen bir nesne üzerinde kilit almak iyi bir uygulamadır.  Ancak, tek bir koleksiyon veya dizide bir kilit genellikle bir sorun sunmamalıdır.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

Uygulama etki alanları genelinde kullanılabilecek veya tanımlayıcı bir kimlik tanıma olmayan türler üzerinde kilit almaz. @No__t-1, <xref:System.Reflection.MethodInfo>, <xref:System.Reflection.PropertyInfo>, <xref:System.String>, <xref:System.ValueType>, <xref:System.Threading.Thread> veya <xref:System.MarshalByRefObject> ' den türetilen herhangi bir nesne üzerinde <xref:System.Threading.Monitor.Enter%2A> ' ı çağırmayın.

### <a name="remove-gckeepalive-calls"></a>GC 'yi kaldırın. Canlı tutma çağrıları

Uygun olmayan, var olan kodun önemli bir miktarı <xref:System.GC.KeepAlive%2A> kullanmaz.  @No__t-0 ' a dönüştürdükten sonra sınıfların sonlandırıcılara sahip olmadıkları, ancak işletim sistemi tutamaçlarını sonuçlandırmak için @no__t 2 ' ye güvenen <xref:System.GC.KeepAlive%2A> ' i çağırması gerekmez.  @No__t-0 ' a bir çağrının performans maliyeti göz ardı edilebilir olsa da, bir <xref:System.GC.KeepAlive%2A> ' e yapılan çağrının gerekli olduğunu veya artık mevcut olmayan bir yaşam süresi sorununu gidermek için yeterli olduğunu belirten bir işlem, kodun bakımını daha zor hale getirir.  Ancak, COM birlikte çalışabilirlik CLR çağrılabilir sarmalayıcıları (RCWs) kullanılırken, kod için hala <xref:System.GC.KeepAlive%2A> gerekir.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

@No__t kaldırın-0.

### <a name="use-the-hostprotection-attribute"></a>HostProtection özniteliğini kullanma

@No__t-0 (HPA), konak koruma gereksinimlerini belirleyen bildirim temelli güvenlik eylemlerinin kullanımını, ana bilgisayarın, <xref:System.Environment.Exit%2A> veya @no__ gibi belirli bir ana bilgisayar için uygun olmayan bazı yöntemleri aramasını engellemesine olanak sağlar. SQL Server için t-2.

HPA yalnızca ortak dil çalışma zamanını barındıran ve SQL Server gibi konak korumasını uygulayan yönetilmeyen uygulamaları etkiler. Uygulandığında, güvenlik eylemi, sınıf veya yöntemin açığa çıkardığı konak kaynaklarına dayalı bir bağlantı talebi oluşturulmasına neden olur. Kod bir istemci uygulamasında veya konak korumalı olmayan bir sunucuda çalışıyorsa, "oturum" özniteliği algılanmadı ve bu nedenle uygulanmadı.

> [!IMPORTANT]
> Bu özniteliğin amacı, güvenlik davranışını değil, konağa özgü programlama modeli kılavuzlarını zorlayasağlamaktır.  Model gereksinimleriyle ilgili uygunluğu denetlemek için bir bağlantı isteği kullanılmasına karşın, <xref:System.Security.Permissions.HostProtectionAttribute> bir güvenlik izni değildir.

Konağın programlama modeli gereksinimleri yoksa bağlantı talepleri gerçekleşmez.

Bu öznitelik aşağıdakileri tanımlar:

- Konak programlama modeline uymayan, ancak zararsız olan Yöntemler veya sınıflar.

- Konak programlama modeline uymayan Yöntemler veya sınıflar ve sunucu tarafından yönetilen kullanıcı kodunun sabitleştirilmesi için yol açabilir.

- Konak programlama modeline uymayan Yöntemler veya sınıflar ve sunucu işleminin sabitinin kararlı hale getirilmesine neden olabilir.

> [!NOTE]
> Konak korumalı bir ortamda yürütülebileceği uygulamalar tarafından çağrılacak bir sınıf kitaplığı oluşturuyorsanız, bu özniteliği <xref:System.Security.Permissions.HostProtectionResource> kaynak kategorilerini sunan üyelere uygulamalısınız. Bu özniteliğe sahip .NET Framework sınıf kitaplığı üyeleri yalnızca hemen çağıranın denetlenmesi için yol açabilir.  Kitaplık üyeüme aynı zamanda kendi arayanın aynı şekilde denetimine neden olmalıdır.

Lütfen <xref:System.Security.Permissions.HostProtectionAttribute> ' da HPA hakkında daha fazla bilgi bulabilirsiniz.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

SQL Server için, eşitleme veya iş parçacığı tanıtmak için kullanılan tüm yöntemlerin HPA ile tanımlanması gerekir. Bu durum, durumu paylaşan, eşitlenen veya dış süreçler yöneten yöntemleri içerir. SQL Server etkileyen @no__t 0 değerleri <xref:System.Security.Permissions.HostProtectionResource.SharedState>, <xref:System.Security.Permissions.HostProtectionResource.Synchronization> ve <xref:System.Security.Permissions.HostProtectionResource.ExternalProcessMgmt> ' dir. Ancak, herhangi bir @no__t içeren herhangi bir yöntem yalnızca SQL 'i etkileyen kaynakları kullanan bir HPA tarafından tanımlanmalıdır.

### <a name="do-not-block-indefinitely-in-unmanaged-code"></a>Yönetilmeyen kodda süresiz olarak engellenmeyin

Yönetilen kod yerine yönetilmeyen kodda engelleme, CLR iş parçacığını durduramadığı için hizmet reddi saldırısına neden olabilir.  Engellenen bir iş parçacığı, CLR 'nin <xref:System.AppDomain> ' ı yüklemesini, en azından, son derece güvenli olmayan işlemler yapmadan engeller.  Windows eşitleme temel kullanımını engellemek, izin verdiğimiz bir şeyin açık bir örneğidir.  Bir yuvada bir `ReadFile` ' a yapılan çağrının engellenmesi, mümkünse kaçınılması gerekir — ideal olarak, Windows API bunun zaman aşımı gibi bir işlem için bir mekanizma sağlamalıdır.

Doğal olarak çağıran herhangi bir yöntem ideal, sınırlı bir zaman aşımıyla bir Win32 çağrısı kullanmalıdır.  Kullanıcının zaman aşımını belirtmesini izin veriliyorsa, kullanıcının belirli bir güvenlik izni olmadan sonsuz bir zaman aşımı belirtmemelidir.  Bir kılavuz olarak, bir yöntem ~ 10 saniyeden uzun bir süre boyunca engellense, zaman aşımlarını destekleyen bir sürüm kullanmanız veya ek CLR desteği almanız gerekir.

Soruna neden olan API 'Ler örnekleri aşağıda verilmiştir.  Kanallar (hem anonim hem de adlandırılmış), bir zaman aşımı ile oluşturulabilir; Ancak, kod `CreateNamedPipe` ' ı veya `WaitNamedPipe` ' i hiçbir şekilde çağırdığından emin olmalıdır.  Ayrıca, zaman aşımı belirtilmiş olsa bile beklenmedik engelleme olabilir.  Anonim bir kanalda `WriteFile` ' ı çağırmak, tüm baytlar yazılana kadar engeller, yani arabellekte okunmamış veriler varsa, bu, okuyucunun kanal arabelleğinde alan boşaltıncaya kadar, `WriteFile` çağrısının blok olacağını engeller.  Yuvalar her zaman bir zaman aşımı mekanizmasını karşılayan bazı API 'leri kullanmalıdır.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

Yönetilmeyen kodda zaman aşımı olmadan engelleme, bir hizmet reddi saldırıdır. @No__t-0, `WaitForSingleObjectEx`, `WaitForMultipleObjects`, `MsgWaitForMultipleObjects` ve `MsgWaitForMultipleObjectsEx` ' e yönelik platform çağırma çağrıları gerçekleştirmeyin.  NMPWAIT_WAIT_FOREVER kullanmayın.

### <a name="identify-any-sta-dependent-features"></a>STA bağımlı tüm özellikleri tanımla

COM tek iş parçacıklı apartmanlar (STAs) kullanan herhangi bir kodu belirler.  SQL Server işleminde STAs devre dışı bırakıldı.  Performans sayaçları veya pano gibi `CoInitialize` ' a bağlı olan özellikler SQL Server içinde devre dışı bırakılmalıdır.

### <a name="ensure-finalizers-are-free-of-synchronization-problems"></a>Sonlandırıcılar eşitleme sorunlarından muaf olduğundan emin olun

.NET Framework sonraki sürümlerinde birden çok Sonlandırıcı iş parçacığı bulunabilir, yani aynı türdeki farklı örneklere yönelik sonlandırıcılar aynı anda çalışır.  Tamamen iş parçacığı güvenli olması gerekmez; Çöp toplayıcı, belirli bir nesne örneği için sonlandırıcıyı yalnızca bir iş parçacığının çalıştıracaktır.  Ancak, birden çok farklı nesne örneğinde eşzamanlı olarak çalışırken yarış durumlarının ve kilitlenmeleri önlemek için Sonlandırıcıların kodlanmış olması gerekir.  Bir günlük dosyasına yazma gibi herhangi bir dış durumu kullanırken, bir sonlandırıcının iş parçacığı sorunları ele alınmalıdır.  İş parçacığı güvenliği sağlamak için sonlandırmada güvenmeyin. Sonlandırıcı iş parçacığında durumu depolamak için iş parçacığı yerel depolama, yönetilen veya yerel olarak kullanmayın.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

Sonlandırıcılar, eşitleme sorunlarından muaf olmalıdır. Sonlandırıcıda statik kesilebilir durum kullanmayın.

### <a name="avoid-unmanaged-memory-if-possible"></a>Mümkünse yönetilmeyen belleği önleyin

Yönetilmeyen bellek, tıpkı bir işletim sistemi tutamacı gibi sızmış olabilir. Mümkünse, [stackalloc](../../csharp/language-reference/operators/stackalloc.md) [veya bir](../../csharp/language-reference/keywords/fixed-statement.md) byte [] kullanarak <xref:System.Runtime.InteropServices.GCHandle> gibi sabitlenmiş bir yönetilen nesne kullanarak yığındaki belleği kullanmayı deneyin. @No__t-0 sonunda bunları temizler. Ancak, yönetilmeyen bellek ayırmanız gerekiyorsa, bellek ayırmayı kaydırmak için <xref:System.Runtime.InteropServices.SafeHandle> ' dan türetilen bir sınıf kullanmayı düşünün.

@No__t-0 ' ın yeterli olmadığı en az bir örnek olduğunu unutmayın. Bellek ayıran veya boşaltan COM Yöntem çağrıları için, bir DLL 'nin `CoTaskMemAlloc` ile bellek ayırması, başka bir DLL ise bu belleği `CoTaskMemFree` ile boşaltır.  @No__t-0 ' ın kullanılması, diğer DLL 'nin belleğin yaşam süresini denetlemek yerine, yönetilmeyen belleğin yaşam süresini <xref:System.Runtime.InteropServices.SafeHandle> ' in ömrüne kadar bir yere bağlamaktır.

### <a name="review-all-uses-of-catchexception"></a>Tüm catch (özel durum) kullanımlarını gözden geçirin

Belirli bir özel durum yerine tüm özel durumları yakalayacak catch blokları artık zaman uyumsuz özel durumları da yakalar. Her catch (özel durum) bloğunu inceleyerek, atlanan önemli bir kaynak bırakma veya geri alma kodu yoksa, bir <xref:System.Threading.ThreadAbortException>, <xref:System.StackOverflowException> veya <xref:System.OutOfMemoryException> ' yi işlemek için de catch bloğunun içinde hatalı davranış olup olmadığını araştırın.  Bu kodun günlüğe kaydedilmesine veya yalnızca belirli özel durumları görebileceğine veya bir özel durumun tam olarak tek bir nedenden dolayı başarısız olduğu varsayımda olabileceğini unutmayın.  Bu varsayımlar <xref:System.Threading.ThreadAbortException> içerecek şekilde güncelleştirilmeleri gerekebilir.

Dize biçimlendirme yöntemlerinden <xref:System.FormatException> gibi, sizin belirttiğiniz özel durum türünü yakalamak için tüm özel durumları yakalayan tüm yerleri değiştirmeyi göz önünde bulundurun.  Bu, catch bloğunun beklenmeyen özel durumlar üzerinde çalışmasını önler ve kodun beklenmeyen özel durumları yakalayarak hataları gizlemez olmasını sağlamaya yardımcı olur.  Genel bir kural olarak kitaplık kodunda bir özel durumu işlemez (bir özel durum yakalamanızı gerektiren kod, aradığınız kodda bir tasarım kusurunu belirtebilir).  Bazı durumlarda, bir özel durumu yakalamak ve daha fazla veri sağlamak için farklı bir özel durum türü oluşturmak isteyebilirsiniz.  Bu durumda iç içe geçmiş özel durumları kullanın ve hatanın gerçek nedenini yeni özel durumun <xref:System.Exception.InnerException%2A> özelliğinde depolarsınız.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

Tüm nesneleri yakalar veya tüm özel durumları yakalayacak Yönetilen koddaki tüm catch bloklarını gözden geçirin.  İçinde C#bu, hem `catch` {} hem de `catch(Exception)` {} ' ü bayrak olarak gösterir.  Özel durum türünü çok özel yapmayı düşünün veya beklenmeyen bir özel durum türünü yakaladığı için hatalı bir şekilde hareket etmemesini sağlamak üzere kodu gözden geçirin.

### <a name="do-not-assume-a-managed-thread-is-a-win32-thread--it-is-a-fiber"></a>Yönetilen bir iş parçacığının bir Win32 iş parçacığı olduğunu varsaymayın; bu bir fiber

Yönetilen iş parçacığı yerel depolama kullanmak çalışır, ancak yönetilmeyen iş parçacığı yerel depolama birimini veya kodun geçerli işletim sistemi iş parçacığında yeniden çalışacağını varsayabilirsiniz. İş parçacığının yerel ayarı gibi ayarları değiştirmeyin. Platform Invoke aracılığıyla `InitializeCriticalSection` veya `CreateMutex` ' i çağırmayın. Fibers kullanılırken bu durum olmadığı için, Win32 kritik bölümleri ve zaman uyumu sağlayıcılar doğrudan SQL 'de kullanılamaz.  Yönetilen <xref:System.Threading.Mutex> sınıfının bu iş parçacığı benzeşim sorunlarını işlemediğini unutmayın.

Yönetilen iş parçacığı yerel depolama alanı ve iş parçacığının geçerli kullanıcı arabirimi kültürü dahil olmak üzere yönetilen bir <xref:System.Threading.Thread> nesnesi üzerinde, durumun büyük bir bölümünü güvenle kullanabilirsiniz. Ayrıca, var olan bir statik değişkenin değerini yalnızca geçerli yönetilen iş parçacığı tarafından erişilebilir hale getiren <xref:System.ThreadStaticAttribute> ' ı kullanabilirsiniz (Bu, CLR 'de fiber yerel depolama yapmanın başka bir yoludur). Programlama modeli nedenleriyle, SQL 'de çalışırken bir iş parçacığının geçerli kültürünü değiştiremezsiniz.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

SQL Server, fiber modda çalışır; iş parçacığı yerel depolama kullanmayın. @No__t-0, `TlsFree`, `TlsGetValue` ve `TlsSetValue.` ' e yönelik platform çağırma çağrılarından kaçının

### <a name="let-sql-server-handle-impersonation"></a>SQL Server tanıtıcı kimliğe bürünmeye izin ver

Kimliğe bürünme iş parçacığı düzeyinde çalışır ve SQL fiber modda çalışabilir, yönetilen kod kullanıcıları taklit etmez ve `RevertToSelf` ' ı çağırmamalıdır.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

SQL Server tanıtıcı kimliğe bürünmeye izin verin. @No__t-0, `ImpersonateAnonymousToken`, `DdeImpersonateClient`, `ImpersonateDdeClientWindow`, `ImpersonateLoggedOnUser`, `ImpersonateNamedPipeClient`, `ImpersonateSelf`, `RpcImpersonateClient`, `RpcRevertToSelf`, `RpcRevertToSelfEx` veya 0 kullanmayın.

### <a name="do-not-call-threadsuspend"></a>Thread:: Suspend çağrısını çağırma

Bir iş parçacığını askıya alma özelliği basit bir işlem görünebilir, ancak kilitlenmeleri neden olabilir.  Kilit tutan bir iş parçacığı ikinci bir iş parçacığı tarafından askıya alınırsa ve ikinci iş parçacığı aynı kilidi gerçekleştirmeye çalışırsa, bir kilitlenme oluşur.  <xref:System.Threading.Thread.Suspend%2A>, güvenlik, sınıf yükleme, uzaktan iletişim ve yansıma ile karışabilir.

#### <a name="code-analysis-rule"></a>Kod Analizi kuralı

@No__t-0 çağırmayın. @No__t-0 veya <xref:System.Threading.ManualResetEvent> gibi gerçek bir eşitleme temel kullanmayı düşünün.

### <a name="protect-critical-operations-with-constrained-execution-regions-and-reliability-contracts"></a>Kısıtlı yürütme bölgeleri ve güvenilirlik sözleşmeleri ile kritik işlemleri koruma

Paylaşılan bir durumu güncelleştiren veya tamamen başarılı ya da tamamen başarısız olması gereken karmaşık bir işlem gerçekleştirirken, kısıtlı bir yürütme bölgesi (CER) tarafından korunduğundan emin olun. Bu, kodun her durumda çalışmasını, hatta ani bir iş parçacığı iptali veya ani bir <xref:System.AppDomain> kaldırma işlemi olmasını güvence altına alır.

Bir CER, bir <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> ' e yapılan çağrının hemen öncesinde belirli bir `try/finally` bloğudur.

Bunun yapılması, tam zamanında derleyicinin `try` bloğunu çalıştırmadan önce finally bloğundaki tüm kodu hazırlamasını söyler. Bu, finally bloğundaki kodun oluşturuldığına ve her durumda çalışacak şekilde emin olur. Boş bir `try` bloğuna sahip olmak için bir CER 'de yaygın olmayan bir durumdur. Bir CER kullanılması zaman uyumsuz iş parçacığı iptal ve bellek dışı özel durumlara karşı koruma sağlar. Ayrıca, diğer bir deyişle, daha fazla derin kod için yığın taşlarını işleyen bir CER formu için bkz. <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup%2A>.

## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Runtime.ConstrainedExecution>
- [SQL Server Programlama ve Konak Koruması Öznitelikleri](sql-server-programming-and-host-protection-attributes.md)
