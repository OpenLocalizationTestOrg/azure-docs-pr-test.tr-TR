---
title: "aaaScheduled olayları için Windows azure'da Vm'leri | Microsoft Docs"
description: "Hello Azure meta veri hizmeti için Windows sanal makinelerde kullanarak zamanlanmış olayları."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="061ac-103">Azure meta veri hizmeti: Windows VM'ler zamanlanmış olaylar (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="061ac-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="061ac-104">Önizlemeler kullanılabilir tooyou toohello kullanım koşullarını kabul ediyorum hello koşula yapılır.</span><span class="sxs-lookup"><span data-stu-id="061ac-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="061ac-105">Daha fazla bilgi için bkz. [Microsoft Azure Önizlemeleri için Microsoft Azure Ek Kullanım Koşulları](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="061ac-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="061ac-106">Zamanlanmış olaylar biridir hello alt Servisleri hello Azure meta veri hizmeti altında.</span><span class="sxs-lookup"><span data-stu-id="061ac-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="061ac-107">Yaklaşan olayları ile ilgili bilgiler görünmesini sorumludur (örneğin, yeniden başlatma) uygulamanız için hazırlamak ve sınırlamak için kesintisi.</span><span class="sxs-lookup"><span data-stu-id="061ac-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="061ac-108">PaaS ve Iaas dahil olmak üzere tüm Azure sanal makine türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="061ac-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="061ac-109">Zamanlanmış olaylar toominimize hello etkisi bir olay, sanal makine zaman tooperform önleyici görevlerinizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="061ac-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="061ac-110">Zamanlanmış olaylar hem Linux hem de Windows VM'ler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="061ac-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="061ac-111">Linux üzerinde zamanlanmış olaylar hakkında bilgi için bkz: [Linux VM'ler için zamanlanmış olayları](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="061ac-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="061ac-112">Neden zamanlanmış olayları?</span><span class="sxs-lookup"><span data-stu-id="061ac-112">Why Scheduled Events?</span></span>

<span data-ttu-id="061ac-113">Zamanlanmış olaylarla hizmetinizde toolimit hello etkisini platform intiated Bakım veya kullanıcı tarafından başlatılan Eylemler adımlar atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="061ac-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="061ac-114">Çoğaltma teknikleri toomaintain durumu kullanın, çok örnekli iş yükleri arasında birden çok örneği gerçekleştiği savunmasız toooutages olabilir.</span><span class="sxs-lookup"><span data-stu-id="061ac-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="061ac-115">Bu tür kayıpları, pahalı görevler (örneğin, yeniden dizinler) veya çoğaltma kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="061ac-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="061ac-116">Diğer birçok durumda hello genel hizmet kullanılabilirliği kapama dizisi gibi gerçekleştirerek iyileştirilebilir (el ile yük devretme) hello kümedeki görevleri tooother VM'ler yeniden atama veya hello kaldırılması Tamamlanıyor (veya iptal etme) yürütülen işlemler, Sanal makine bir ağ yük dengeleyici havuzundan.</span><span class="sxs-lookup"><span data-stu-id="061ac-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="061ac-117">Burada, yönetici yaklaşan bir olay hakkında bilgilendirmek veya böyle bir olay günlüğü yardımcı hello bakım yapılabilirliğini hello bulutta barındırılan uygulamalar geliştirme durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="061ac-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="061ac-118">Azure meta veri hizmeti yüzeyleri zamanlanmış olayları hello aşağıdaki durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="061ac-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="061ac-119">Başlatılan platform Bakım (örneğin, ana bilgisayar işletim sistemi dağıtımı)</span><span class="sxs-lookup"><span data-stu-id="061ac-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="061ac-120">Kullanıcı tarafından başlatılan çağrıları (örneğin, kullanıcı yeniden başlatma veya yeniden dağıtır VM)</span><span class="sxs-lookup"><span data-stu-id="061ac-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="061ac-121">Merhaba temelleri</span><span class="sxs-lookup"><span data-stu-id="061ac-121">hello basics</span></span>  

<span data-ttu-id="061ac-122">Azure meta veri hizmeti REST uç noktasını hello VM içinde erişilebilir kullanarak sanal makineleri çalıştırma hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="061ac-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="061ac-123">Böylece VM hello dışında gösterilmeyen hello bilgi yönlendirilemeyen bir IP kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="061ac-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="061ac-124">Kapsam</span><span class="sxs-lookup"><span data-stu-id="061ac-124">Scope</span></span>
<span data-ttu-id="061ac-125">Zamanlanmış olaylar ortaya tooall sanal makineler bir bulut hizmetinde veya bir kullanılabilirlik kümesindeki sanal makineleri tooall verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="061ac-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="061ac-126">Sonuç olarak, hello denetlemelisiniz `Resources` VM'ler etkilenen toobe kalacaklarını hello olay tooidentify alanındaki.</span><span class="sxs-lookup"><span data-stu-id="061ac-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="061ac-127">Merhaba endpoint keşfetme</span><span class="sxs-lookup"><span data-stu-id="061ac-127">Discovering hello endpoint</span></span>
<span data-ttu-id="061ac-128">Bir sanal makine bir sanal ağ (VNet) içinde oluşturulduğu burada hello durumda hello meta veri hizmeti bir statik yönlendirilemeyen bir IP, kullanılabilir `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="061ac-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="061ac-129">İlave bir mantık gerekli toodiscover hello uç nokta toouse ise Hello sanal makine bulut Hizmetleri ve klasik sanal makineleri için hello varsayılan durumlar bir sanal ağ içinde oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="061ac-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="061ac-130">Toothis örnek toolearn nasıl çok başvuran[hello konak uç noktası bulunamadı](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="061ac-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="061ac-131">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="061ac-131">Versioning</span></span> 
<span data-ttu-id="061ac-132">Merhaba örneği meta veri hizmeti sürümü tutulan ' dir.</span><span class="sxs-lookup"><span data-stu-id="061ac-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="061ac-133">Sürümleri zorunludur ve hello geçerli sürümü `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="061ac-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="061ac-134">Önceki Önizleme sürümleri {son} hello api sürümü desteklenen zamanlanmış olaylar.</span><span class="sxs-lookup"><span data-stu-id="061ac-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="061ac-135">Bu biçim artık desteklenmemektedir ve hello gelecekteki kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="061ac-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="061ac-136">Üst bilgileri kullanma</span><span class="sxs-lookup"><span data-stu-id="061ac-136">Using headers</span></span>
<span data-ttu-id="061ac-137">Merhaba meta veri hizmeti sorguladığınızda hello üstbilgi sağlamalısınız `Metadata: true` tooensure hello talep istemeden yönlendirilmeyen.</span><span class="sxs-lookup"><span data-stu-id="061ac-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="061ac-138">Zamanlanmış olayları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="061ac-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="061ac-139">Merhaba zamanlanmış olaylar, istekte ilk kez Azure örtük olarak hello özelliği, sanal makinenizde sağlar.</span><span class="sxs-lookup"><span data-stu-id="061ac-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="061ac-140">Sonuç olarak, ilk çağrısında tootwo dakika yukarı Gecikmeli yanıt beklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="061ac-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="061ac-141">Kullanıcı tarafından başlatılan bakım</span><span class="sxs-lookup"><span data-stu-id="061ac-141">User initiated maintenance</span></span>
<span data-ttu-id="061ac-142">Sanal makine Bakımı hello Azure portal, API, CLI, aracılığıyla kullanıcı tarafından başlatılan veya PowerShell zamanlanmış bir olayı sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="061ac-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="061ac-143">Bu, uygulamanızda tootest hello bakım hazırlık mantığı sağlar ve kullanıcı tarafından başlatılan bakım için uygulama tooprepare sağlar.</span><span class="sxs-lookup"><span data-stu-id="061ac-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="061ac-144">Bir sanal makinenin yeniden başlatılması zamanlar türüne sahip bir olay `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="061ac-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="061ac-145">Bir sanal makineyi dağıtarak zamanlar türüne sahip bir olay `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="061ac-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="061ac-146">Şu anda en fazla 10 kullanıcı tarafından başlatılan bakım işlemleri aynı anda zamanlanabilir.</span><span class="sxs-lookup"><span data-stu-id="061ac-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="061ac-147">Bu sınır zamanlanmış olayları genel kullanılabilirlik önce rahat olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="061ac-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="061ac-148">Şu anda zamanlanmış olayları kaynaklanan kullanıcı tarafından başlatılan bakım yapılandırılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="061ac-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="061ac-149">Yapılandırılabilirlik gelecekteki bir sürümde planlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="061ac-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="061ac-150">Merhaba API'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="061ac-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="061ac-151">Olaylar için sorgu</span><span class="sxs-lookup"><span data-stu-id="061ac-151">Query for events</span></span>
<span data-ttu-id="061ac-152">Zamanlanmış olaylar için çağrı hello aşağıdakileri yaparak sorgulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="061ac-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="061ac-153">Bir yanıt zamanlanmış olaylar dizisini içerir.</span><span class="sxs-lookup"><span data-stu-id="061ac-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="061ac-154">Boş bir dizi var. şu anda zamanlanmış bir olay yok demektir.</span><span class="sxs-lookup"><span data-stu-id="061ac-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="061ac-155">Merhaba durumda Zamanlanmış olaylar olduğu hello yanıt olaylar dizisini içerir:</span><span class="sxs-lookup"><span data-stu-id="061ac-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="061ac-156">Olay Özellikleri</span><span class="sxs-lookup"><span data-stu-id="061ac-156">Event properties</span></span>
|<span data-ttu-id="061ac-157">Özellik</span><span class="sxs-lookup"><span data-stu-id="061ac-157">Property</span></span>  |  <span data-ttu-id="061ac-158">Açıklama</span><span class="sxs-lookup"><span data-stu-id="061ac-158">Description</span></span> |
| - | - |
| <span data-ttu-id="061ac-159">Olay Kimliği</span><span class="sxs-lookup"><span data-stu-id="061ac-159">EventId</span></span> | <span data-ttu-id="061ac-160">Bu olay için genel benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="061ac-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="061ac-161">Örnek:</span><span class="sxs-lookup"><span data-stu-id="061ac-161">Example:</span></span> <br><ul><li><span data-ttu-id="061ac-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="061ac-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="061ac-163">Olay türü</span><span class="sxs-lookup"><span data-stu-id="061ac-163">EventType</span></span> | <span data-ttu-id="061ac-164">Bu olaya neden olan etkisi.</span><span class="sxs-lookup"><span data-stu-id="061ac-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="061ac-165">Değerler:</span><span class="sxs-lookup"><span data-stu-id="061ac-165">Values:</span></span> <br><ul><li> <span data-ttu-id="061ac-166">`Freeze`: hello sanal makine için birkaç saniye zamanlanmış toopause değil.</span><span class="sxs-lookup"><span data-stu-id="061ac-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="061ac-167">Merhaba CPU askıya alındı, ancak bellek, açık dosyalar veya ağ bağlantıları üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="061ac-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="061ac-168">`Reboot`: sanal makine için yeniden başlatma Zamanlanmış Başlangıç (kalıcı olmayan bellek kaybolur).</span><span class="sxs-lookup"><span data-stu-id="061ac-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="061ac-169">`Redeploy`: hello sanal makine olan zamanlanmış toomove tooanother düğümü (kısa ömürlü diskleri kaybolur).</span><span class="sxs-lookup"><span data-stu-id="061ac-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="061ac-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="061ac-170">ResourceType</span></span> | <span data-ttu-id="061ac-171">Bu olay etkiler kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="061ac-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="061ac-172">Değerler:</span><span class="sxs-lookup"><span data-stu-id="061ac-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="061ac-173">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="061ac-173">Resources</span></span>| <span data-ttu-id="061ac-174">Bu olay etkiler kaynakların listesi.</span><span class="sxs-lookup"><span data-stu-id="061ac-174">List of resources this event impacts.</span></span> <span data-ttu-id="061ac-175">Bu toocontain makineler en fazla bir garanti [güncelleştirme etki alanı](manage-availability.md), hello UD tüm makinelerde içerebilir ancak.</span><span class="sxs-lookup"><span data-stu-id="061ac-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="061ac-176">Örnek:</span><span class="sxs-lookup"><span data-stu-id="061ac-176">Example:</span></span> <br><ul><li> <span data-ttu-id="061ac-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="061ac-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="061ac-178">Olay durumu</span><span class="sxs-lookup"><span data-stu-id="061ac-178">Event Status</span></span> | <span data-ttu-id="061ac-179">Bu olay durumu.</span><span class="sxs-lookup"><span data-stu-id="061ac-179">Status of this event.</span></span> <br><br> <span data-ttu-id="061ac-180">Değerler:</span><span class="sxs-lookup"><span data-stu-id="061ac-180">Values:</span></span> <ul><li><span data-ttu-id="061ac-181">`Scheduled`: Bu olay hello belirtilen başlangıç saati zamanlanmış toostart sonradır `NotBefore` özelliği.</span><span class="sxs-lookup"><span data-stu-id="061ac-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="061ac-182">`Started`: Bu olay başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="061ac-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="061ac-183">Hayır `Completed` veya benzer durumu hiç sağlanır; hello olay, artık hello olay tamamlandığında döndürülecek.</span><span class="sxs-lookup"><span data-stu-id="061ac-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="061ac-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="061ac-184">NotBefore</span></span>| <span data-ttu-id="061ac-185">Süre geçtikten sonra bu olay başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="061ac-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="061ac-186">Örnek:</span><span class="sxs-lookup"><span data-stu-id="061ac-186">Example:</span></span> <br><ul><li> <span data-ttu-id="061ac-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="061ac-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="061ac-188">Olay planlama</span><span class="sxs-lookup"><span data-stu-id="061ac-188">Event scheduling</span></span>
<span data-ttu-id="061ac-189">Her olay zamanlanmış bir minimum süreyi hello gelecekteki olay türüne bağlı.</span><span class="sxs-lookup"><span data-stu-id="061ac-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="061ac-190">Bu süre bir olayın içinde yansıtılır `NotBefore` özelliği.</span><span class="sxs-lookup"><span data-stu-id="061ac-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="061ac-191">Olay türü</span><span class="sxs-lookup"><span data-stu-id="061ac-191">EventType</span></span>  | <span data-ttu-id="061ac-192">Minimum dikkat edin</span><span class="sxs-lookup"><span data-stu-id="061ac-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="061ac-193">Dondurma</span><span class="sxs-lookup"><span data-stu-id="061ac-193">Freeze</span></span>| <span data-ttu-id="061ac-194">15 dakika</span><span class="sxs-lookup"><span data-stu-id="061ac-194">15 minutes</span></span> |
| <span data-ttu-id="061ac-195">Yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="061ac-195">Reboot</span></span> | <span data-ttu-id="061ac-196">15 dakika</span><span class="sxs-lookup"><span data-stu-id="061ac-196">15 minutes</span></span> |
| <span data-ttu-id="061ac-197">Yeniden dağıtım</span><span class="sxs-lookup"><span data-stu-id="061ac-197">Redeploy</span></span> | <span data-ttu-id="061ac-198">10 dakika</span><span class="sxs-lookup"><span data-stu-id="061ac-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="061ac-199">Bir olayı başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="061ac-199">Starting an event</span></span> 

<span data-ttu-id="061ac-200">Yaklaşan olay öğrenilen ve normal olarak kapatmak için mantığınızı tamamlandı sonra yaparak hello bekleyen olay onaylayabilirsiniz bir `POST` çağrısı toohello meta veri hizmeti ile Merhaba `EventId`.</span><span class="sxs-lookup"><span data-stu-id="061ac-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="061ac-201">Bu hello minimum bildirim kısaltabilir tooAzure gösterir (uygunsa) süresi.</span><span class="sxs-lookup"><span data-stu-id="061ac-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="061ac-202">Bir olay aktarımının verir hello olay tooproceed tüm `Resources` hello olayda hello olay kabul ettikten sanal makine yalnızca hello.</span><span class="sxs-lookup"><span data-stu-id="061ac-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="061ac-203">Bu nedenle hello ilk makine hello olarak basit bir kılavuz toocoordinate hello bildirim tooelect tercih edebilirsiniz `Resources` alan.</span><span class="sxs-lookup"><span data-stu-id="061ac-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="061ac-204">PowerShell örnek</span><span class="sxs-lookup"><span data-stu-id="061ac-204">PowerShell sample</span></span> 

<span data-ttu-id="061ac-205">Merhaba aşağıdaki örnek sorgularda zamanlanmış olaylar için meta veri hizmeti hello ve her bekleyen olay onaylar.</span><span class="sxs-lookup"><span data-stu-id="061ac-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a><span data-ttu-id="061ac-206">C\# örnek</span><span class="sxs-lookup"><span data-stu-id="061ac-206">C\# sample</span></span> 

<span data-ttu-id="061ac-207">Merhaba aşağıdaki hello meta veri hizmeti ile iletişim kuracağını basit bir istemcinin örnektir.</span><span class="sxs-lookup"><span data-stu-id="061ac-207">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="061ac-208">Zamanlanmış olaylar veri yapılarını aşağıdaki hello kullanılarak temsil edilebilir:</span><span class="sxs-lookup"><span data-stu-id="061ac-208">Scheduled Events can be represented using hello following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="061ac-209">Merhaba aşağıdaki örnek sorgularda zamanlanmış olaylar için meta veri hizmeti hello ve her bekleyen olay onaylar.</span><span class="sxs-lookup"><span data-stu-id="061ac-209">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a><span data-ttu-id="061ac-210">Python örneği</span><span class="sxs-lookup"><span data-stu-id="061ac-210">Python sample</span></span> 

<span data-ttu-id="061ac-211">Merhaba aşağıdaki örnek sorgularda zamanlanmış olaylar için meta veri hizmeti hello ve her bekleyen olay onaylar.</span><span class="sxs-lookup"><span data-stu-id="061ac-211">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="061ac-212">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="061ac-212">Next steps</span></span> 

- <span data-ttu-id="061ac-213">Merhaba hello kullanılabilir API'ler hakkında daha fazla bilgiyi [örneği meta veri hizmeti](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="061ac-213">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="061ac-214">Hakkında bilgi edinin [planlı bakım azure'da Windows sanal makineler için](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="061ac-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

