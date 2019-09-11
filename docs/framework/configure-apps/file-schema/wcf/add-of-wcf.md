---
title: <add>WCF
ms.date: 03/30/2017
ms.assetid: c196f6d7-77f6-4266-973c-305b2b4dd8a2
ms.openlocfilehash: 0b21bdabc76ec4853a0f2664cdd3cead149417a1
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70850304"
---
# <a name="add-of-wcf"></a><span data-ttu-id="0d1ca-102">\<WCF > ekleyin</span><span class="sxs-lookup"><span data-stu-id="0d1ca-102">\<add> of WCF</span></span>
<span data-ttu-id="0d1ca-103">Çalışma zamanından doğrudan yayılmakta olan izleme kayıtlarını dinleyen bir izleme katılımcısı yapılandırın ve bunları ne şekilde yapılandırdığınıza göre işleyin.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-103">Configure a tracking participant that listens to the tracking records being emitted from the runtime directly and process them in whatever way it was configured.</span></span> <span data-ttu-id="0d1ca-104">Bu yazma içerir (örneğin, dosya, konsolu ETW), belirli bir çıktısına işleme/kayıtları veya gerekli olabilir herhangi bir birleşimini toplama.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-104">This includes writing to a specific output (e.g., file, Console, ETW), processing/aggregating the records, or any other combination that might be required.</span></span>  
  
 <span data-ttu-id="0d1ca-105">İş akışı izleme ve İzleme katılımcıları hakkında daha fazla bilgi için bkz. [Iş akışı izleme ve](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md) Izleme ve [İzleme katılımcıları](../../../windows-workflow-foundation/tracking-participants.md).</span><span class="sxs-lookup"><span data-stu-id="0d1ca-105">For more information in workflow tracking and tracking participants, see [Workflow Tracking and Tracing](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md) and [Tracking Participants](../../../windows-workflow-foundation/tracking-participants.md).</span></span>  
  
<span data-ttu-id="0d1ca-106">[ **\<Yapılandırma >** ](../configuration-element.md)</span><span class="sxs-lookup"><span data-stu-id="0d1ca-106">[**\<configuration>**](../configuration-element.md)</span></span>\
<span data-ttu-id="0d1ca-107">&nbsp;&nbsp;[ **\<System. serviceModel >** ](system-servicemodel.md)</span><span class="sxs-lookup"><span data-stu-id="0d1ca-107">&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)</span></span>\
<span data-ttu-id="0d1ca-108">&nbsp;&nbsp;&nbsp;&nbsp;[ **\<İzleme >** ](tracking-of-wcf.md)</span><span class="sxs-lookup"><span data-stu-id="0d1ca-108">&nbsp;&nbsp;&nbsp;&nbsp;[**\<tracking>**](tracking-of-wcf.md)</span></span>\
<span data-ttu-id="0d1ca-109">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<Katılımcılar >** ](participants-of-wcf.md)</span><span class="sxs-lookup"><span data-stu-id="0d1ca-109">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<participants>**](participants-of-wcf.md)</span></span>\
<span data-ttu-id="0d1ca-110">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> Ekle**</span><span class="sxs-lookup"><span data-stu-id="0d1ca-110">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0d1ca-111">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="0d1ca-111">Syntax</span></span>  
  
```xml  
<tracking>
  <participants>
    <add name="String"
         profileName="String"
         type="String" />
  </participants>
</tracking>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="0d1ca-112">Öznitelikler ve Öğeler</span><span class="sxs-lookup"><span data-stu-id="0d1ca-112">Attributes and Elements</span></span>  
 <span data-ttu-id="0d1ca-113">Öznitelikler, alt ve üst öğeler aşağıdaki bölümlerde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-113">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="0d1ca-114">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="0d1ca-114">Attributes</span></span>  
  
|<span data-ttu-id="0d1ca-115">Öğe</span><span class="sxs-lookup"><span data-stu-id="0d1ca-115">Element</span></span>|<span data-ttu-id="0d1ca-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0d1ca-116">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="0d1ca-117">name</span><span class="sxs-lookup"><span data-stu-id="0d1ca-117">name</span></span>|<span data-ttu-id="0d1ca-118">İzleme katılımcısının adını belirten bir dize.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-118">A string that specifies the name of a tracking participant.</span></span>|  
|<span data-ttu-id="0d1ca-119">ProfilAdı</span><span class="sxs-lookup"><span data-stu-id="0d1ca-119">profileName</span></span>|<span data-ttu-id="0d1ca-120">İzleme katılımcının abone olduğu izleme kayıtlarını tanımlayan izleme profili adını belirten bir dize.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-120">A string that specifies the name of the tracking profile which defines the tracking records the tracking participant has subscribed to.</span></span>|  
|<span data-ttu-id="0d1ca-121">türü</span><span class="sxs-lookup"><span data-stu-id="0d1ca-121">type</span></span>|<span data-ttu-id="0d1ca-122">İzleme katılımcısı türünü belirten bir dize.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-122">A string that specifies the type of a tracking participant.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="0d1ca-123">Alt Öğeler</span><span class="sxs-lookup"><span data-stu-id="0d1ca-123">Child Elements</span></span>  
 <span data-ttu-id="0d1ca-124">Yok.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-124">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="0d1ca-125">Üst Öğeler</span><span class="sxs-lookup"><span data-stu-id="0d1ca-125">Parent Elements</span></span>  
  
|<span data-ttu-id="0d1ca-126">Öğe</span><span class="sxs-lookup"><span data-stu-id="0d1ca-126">Element</span></span>|<span data-ttu-id="0d1ca-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0d1ca-127">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="0d1ca-128">\<Katılımcılar ></span><span class="sxs-lookup"><span data-stu-id="0d1ca-128">\<participants></span></span>](../windows-workflow-foundation/participants.md)|<span data-ttu-id="0d1ca-129">İzleme katılımcılarının listesi</span><span class="sxs-lookup"><span data-stu-id="0d1ca-129">A list of tracking participants</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="0d1ca-130">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="0d1ca-130">Remarks</span></span>  
 <span data-ttu-id="0d1ca-131">İzleme katılımcıları iş akışından yayılan izleme verilerini almak ve farklı ortalamalarına depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-131">Tracking participants are used to get the tracking data emitted from the workflow and store it into different mediums.</span></span> <span data-ttu-id="0d1ca-132">Benzer şekilde, izleme kayıtlarında yapılan tüm gönderi işlemleri izleme katılımcısının içinden de yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-132">Likewise, any post processing on the tracking Records can also be done within the tracking participant.</span></span>  
  
 <span data-ttu-id="0d1ca-133">Birden çok izleme katılımcısı izleme olaylarını eşzamanlı olarak kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-133">Multiple tracking participants can consume the tracking events simultaneously.</span></span> <span data-ttu-id="0d1ca-134">Her izleme katılımcısı, farklı bir izleme profiliyle ilişkilendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-134">Each tracking participant can be associated with a different tracking profile.</span></span>  
  
 <span data-ttu-id="0d1ca-135">İzleme kayıtlarını bir ETW oturumuna yazan standart bir izleme katılımcısı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-135">A standard tracking participant is provided which writes the tracking records to an ETW session.</span></span> <span data-ttu-id="0d1ca-136">Katılımcı bir yapılandırma dosyasına izlemeye özgü bir davranış ekleyerek bir iş akışı hizmeti üzerinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-136">The participant is configured on a workflow service by adding a tracking-specific behavior in a configuration file.</span></span> <span data-ttu-id="0d1ca-137">ETW izleme katılımcısının etkinleştirilmesi, Olay Görüntüleyicisi 'nde izleme kayıtlarının görüntülenmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-137">Enabling an ETW tracking participant allows tracking records to be viewed in the event viewer.</span></span> <span data-ttu-id="0d1ca-138">Gereksinimlerinizi karşılamıyorsa, özel bir izleme katılımcısı da yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-138">If that does not meet your requirements, you can also write a custom tracking participant.</span></span>  
  
## <a name="example"></a><span data-ttu-id="0d1ca-139">Örnek</span><span class="sxs-lookup"><span data-stu-id="0d1ca-139">Example</span></span>  
 <span data-ttu-id="0d1ca-140">Aşağıdaki yapılandırma örneği, Web. config dosyasında yapılandırılmış standart ETW izleme katılımcısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-140">The following configuration example shows the standard ETW tracking participant being configured in the Web.config file.</span></span>  
  
 <span data-ttu-id="0d1ca-141">ETW izleme katılımcısı tarafından ETW 'ye izleme kayıtlarını yazmak için kullanılan sağlayıcı kimliği `<diagnostics>` bölümünde tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-141">The Provider Id that the ETW Tracking Participant uses for writing the Tracking Records to ETW is defined in the `<diagnostics>` section.</span></span> <span data-ttu-id="0d1ca-142">İzleme katılımcısının, abone olduğu izleme kayıtlarını belirtmek için kendisiyle ilişkili bir profili vardır.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-142">The tracking participant has a profile associated with it to specify the tracking records it has subscribed to.</span></span> <span data-ttu-id="0d1ca-143">Bu, `profileName` `<add>` öğesinin özniteliği tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-143">This is defined by the `profileName` attribute of the `<add>` element.</span></span> <span data-ttu-id="0d1ca-144">Bunlar tanımlandıktan sonra, izleme katılımcısı `<etwTracking>` hizmet davranışına eklenir.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-144">Once these are defined, the Tracking Participant is added to the `<etwTracking>` service behavior.</span></span> <span data-ttu-id="0d1ca-145">Bu işlem, Izleme kayıtlarını almaya başlaması için seçilen Izleme katılımcılarını Iş akışı örneğinin uzantılarına ekler.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-145">This will add the selected Tracking Participants to the Workflow instance’s extensions, so that they begin to receive the Tracking Records.</span></span>  
  
```xml  
<configuration>
  <system.web>
    <compilation targetFrameworkMoniker=".NETFramework,Version=v4.0" />
  </system.web>
  <system.serviceModel>
    <diagnostics etwProviderId="52A3165D-4AD9-405C-B1E8-7D9A257EAC9F" />
    <tracking>
      <participants>
        <add name="EtwTrackingParticipant"
             type="System.Activities.Tracking.EtwTrackingParticipant, System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"
             profileName="HealthMonitoring_Tracking_Profile" />
      </participants>
    </tracking>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <etwTracking profileName="Sample Tracking Profile" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
  </system.serviceModel>
</configuration>
```  
  
## <a name="see-also"></a><span data-ttu-id="0d1ca-146">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0d1ca-146">See also</span></span>

- <xref:System.ServiceModel.Activities.Tracking.Configuration.TrackingSection>
- <xref:System.ServiceModel.Activities.Description.EtwTrackingBehavior>
- <xref:System.ServiceModel.Activities.Configuration.EtwTrackingBehaviorElement>
- [<span data-ttu-id="0d1ca-147">İş Akışı Takip ve İzleme</span><span class="sxs-lookup"><span data-stu-id="0d1ca-147">Workflow Tracking and Tracing</span></span>](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [<span data-ttu-id="0d1ca-148">İzleme Katılımcıları</span><span class="sxs-lookup"><span data-stu-id="0d1ca-148">Tracking Participants</span></span>](../../../windows-workflow-foundation/tracking-participants.md)
