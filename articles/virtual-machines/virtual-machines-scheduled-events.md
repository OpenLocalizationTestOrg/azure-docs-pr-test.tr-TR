---
title: aaaScheduled Azure meta veri hizmeti olaylarla | Microsoft Docs
description: "Gerçekleşmeden önce tooImpactful sanal makineniz olaylarına tepki."
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
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: b5c0849958c3ab48fa9c2cbff7db62f2e9d7daf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="ca62d-103">Azure meta veri hizmeti - zamanlanmış olaylar (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="ca62d-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="ca62d-104">Önizlemeler kullanılabilir tooyou toohello kullanım koşullarını kabul ediyorum hello koşula yapılır.</span><span class="sxs-lookup"><span data-stu-id="ca62d-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="ca62d-105">Daha fazla bilgi için bkz. [Microsoft Azure Önizlemeleri için Microsoft Azure Ek Kullanım Koşulları](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="ca62d-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="ca62d-106">Zamanlanmış olaylar biridir hello alt Servisleri hello Azure meta veri hizmeti altında.</span><span class="sxs-lookup"><span data-stu-id="ca62d-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="ca62d-107">Yaklaşan olayları ile ilgili bilgiler görünmesini sorumludur (örneğin, yeniden başlatma) uygulamanız için hazırlamak ve sınırlamak için kesintisi.</span><span class="sxs-lookup"><span data-stu-id="ca62d-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="ca62d-108">PaaS ve Iaas dahil olmak üzere tüm Azure sanal makine türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="ca62d-109">Zamanlanmış olaylar toominimize hello etkisi bir olay, sanal makine zaman tooperform önleyici görevlerinizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca62d-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="ca62d-110">Giriş - neden zamanlanmış olayları?</span><span class="sxs-lookup"><span data-stu-id="ca62d-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="ca62d-111">Zamanlanmış olaylarla hizmetinizde toolimit hello etkisini platform intiated Bakım veya kullanıcı tarafından başlatılan Eylemler adımlar atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca62d-111">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="ca62d-112">Çoğaltma teknikleri toomaintain durumu kullanın, çok örnekli iş yükleri arasında birden çok örneği gerçekleştiği savunmasız toooutages olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-112">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="ca62d-113">Bu tür kayıpları, pahalı görevler (örneğin, yeniden dizinler) veya çoğaltma kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="ca62d-114">Diğer birçok durumda hello genel hizmet kullanılabilirliği kapama dizisi gibi gerçekleştirerek iyileştirilebilir (el ile yük devretme) hello kümedeki görevleri tooother VM'ler yeniden atama veya hello kaldırılması Tamamlanıyor (veya iptal etme) yürütülen işlemler, Sanal makine bir ağ yük dengeleyici havuzundan.</span><span class="sxs-lookup"><span data-stu-id="ca62d-114">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="ca62d-115">Burada, yönetici yaklaşan bir olay hakkında bilgilendirmek veya böyle bir olay günlüğü yardımcı hello bakım yapılabilirliğini hello bulutta barındırılan uygulamalar geliştirme durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="ca62d-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="ca62d-116">Azure meta veri hizmeti yüzeyleri zamanlanmış olayları hello aşağıdaki durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="ca62d-116">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="ca62d-117">Başlatılan platform Bakım (örneğin, ana bilgisayar işletim sistemi dağıtımı)</span><span class="sxs-lookup"><span data-stu-id="ca62d-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="ca62d-118">Kullanıcı tarafından başlatılan çağrıları (örneğin, kullanıcı yeniden başlatma veya yeniden dağıtır VM)</span><span class="sxs-lookup"><span data-stu-id="ca62d-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---hello-basics"></a><span data-ttu-id="ca62d-119">Zamanlanmış etkinlikleri - hello temelleri</span><span class="sxs-lookup"><span data-stu-id="ca62d-119">Scheduled Events - hello Basics</span></span>  

<span data-ttu-id="ca62d-120">Azure meta veri hizmeti REST uç noktasını hello VM içinde erişilebilir kullanarak sanal makineleri çalıştırma hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="ca62d-121">Böylece VM hello dışında gösterilmeyen hello bilgi yönlendirilemeyen bir IP kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-121">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="ca62d-122">Kapsam</span><span class="sxs-lookup"><span data-stu-id="ca62d-122">Scope</span></span>
<span data-ttu-id="ca62d-123">Zamanlanmış olaylar ortaya tooall sanal makineler bir bulut hizmetinde veya bir kullanılabilirlik kümesindeki sanal makineleri tooall verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-123">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="ca62d-124">Sonuç olarak, hello denetlemelisiniz `Resources` VM'ler etkilenen toobe kalacaklarını hello olay tooidentify alanındaki.</span><span class="sxs-lookup"><span data-stu-id="ca62d-124">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="ca62d-125">Bulan hello uç noktası</span><span class="sxs-lookup"><span data-stu-id="ca62d-125">Discovering hello Endpoint</span></span>
<span data-ttu-id="ca62d-126">Bir sanal makine bir sanal ağ (VNet) içinde oluşturulduğu burada hello durumda hello meta veri hizmeti bir statik yönlendirilemeyen bir IP, kullanılabilir `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="ca62d-126">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="ca62d-127">İlave bir mantık gerekli toodiscover hello uç nokta toouse ise Hello sanal makine bulut Hizmetleri ve klasik sanal makineleri için hello varsayılan durumlar bir sanal ağ içinde oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="ca62d-127">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="ca62d-128">Toothis örnek toolearn nasıl çok başvuran[hello konak uç noktası bulunamadı](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="ca62d-128">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="ca62d-129">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca62d-129">Versioning</span></span> 
<span data-ttu-id="ca62d-130">Merhaba örneği meta veri hizmeti sürümü tutulan ' dir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="ca62d-131">Sürümleri zorunludur ve hello geçerli sürümü `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="ca62d-131">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="ca62d-132">Önceki Önizleme sürümleri {son} hello api sürümü desteklenen zamanlanmış olaylar.</span><span class="sxs-lookup"><span data-stu-id="ca62d-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="ca62d-133">Bu biçim artık desteklenmemektedir ve hello gelecekteki kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="ca62d-133">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="ca62d-134">Üst bilgileri kullanma</span><span class="sxs-lookup"><span data-stu-id="ca62d-134">Using Headers</span></span>
<span data-ttu-id="ca62d-135">Merhaba meta veri hizmeti sorguladığınızda hello üstbilgi sağlamalısınız `Metadata: true` tooensure hello talep istemeden yönlendirilmeyen.</span><span class="sxs-lookup"><span data-stu-id="ca62d-135">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="ca62d-136">Zamanlanmış olayları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ca62d-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="ca62d-137">Merhaba zamanlanmış olaylar, istekte ilk kez Azure örtük olarak hello özelliği, sanal makinenizde sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca62d-137">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="ca62d-138">Sonuç olarak, ilk çağrısında tootwo dakika yukarı Gecikmeli yanıt beklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="ca62d-138">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="ca62d-139">Kullanıcı tarafından başlatılan bakım</span><span class="sxs-lookup"><span data-stu-id="ca62d-139">User Initiated Maintenance</span></span>
<span data-ttu-id="ca62d-140">Sanal makine Bakımı hello Azure portal, API, CLI, aracılığıyla kullanıcı tarafından başlatılan veya PowerShell zamanlanmış olayları neden olur.</span><span class="sxs-lookup"><span data-stu-id="ca62d-140">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="ca62d-141">Bu, uygulamanızda tootest hello bakım hazırlık mantığı sağlar ve kullanıcı tarafından başlatılan bakım için uygulama tooprepare sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca62d-141">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="ca62d-142">Bir olay türüne sahip bir sanal makinenin yeniden başlatılması zamanlama `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="ca62d-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="ca62d-143">Bir olay türüne sahip bir sanal makine yeniden zamanlama `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="ca62d-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="ca62d-144">Şu anda en fazla 10 kullanıcı tarafından başlatılan bakım işlemleri aynı anda zamanlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="ca62d-145">Bu sınır olayları genel kullanılabilirlik zamanlanmış önce rahat olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ca62d-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="ca62d-146">Şu anda zamanlanmış olayları kaynaklanan kullanıcı tarafından başlatılan bakım yapılandırılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="ca62d-147">Yapılandırılabilirlik gelecekteki bir sürümde planlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ca62d-147">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="ca62d-148">Merhaba API'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="ca62d-148">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="ca62d-149">Olaylar için sorgu</span><span class="sxs-lookup"><span data-stu-id="ca62d-149">Query for events</span></span>
<span data-ttu-id="ca62d-150">Zamanlanmış olaylar için çağrı hello aşağıdakileri yaparak sorgulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ca62d-150">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="ca62d-151">Bir yanıt zamanlanmış olaylar dizisini içerir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="ca62d-152">Boş bir dizi var. şu anda zamanlanmış bir olay yok demektir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="ca62d-153">Merhaba durumda Zamanlanmış olaylar olduğu hello yanıt olaylar dizisini içerir:</span><span class="sxs-lookup"><span data-stu-id="ca62d-153">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="ca62d-154">Olay Özellikleri</span><span class="sxs-lookup"><span data-stu-id="ca62d-154">Event Properties</span></span>
|<span data-ttu-id="ca62d-155">Özellik</span><span class="sxs-lookup"><span data-stu-id="ca62d-155">Property</span></span>  |  <span data-ttu-id="ca62d-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ca62d-156">Description</span></span> |
| - | - |
| <span data-ttu-id="ca62d-157">Olay Kimliği</span><span class="sxs-lookup"><span data-stu-id="ca62d-157">EventId</span></span> | <span data-ttu-id="ca62d-158">Bu olay için genel benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="ca62d-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="ca62d-159">Örnek:</span><span class="sxs-lookup"><span data-stu-id="ca62d-159">Example:</span></span> <br><ul><li><span data-ttu-id="ca62d-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="ca62d-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="ca62d-161">Olay türü</span><span class="sxs-lookup"><span data-stu-id="ca62d-161">EventType</span></span> | <span data-ttu-id="ca62d-162">Bu olaya neden olan etkisi.</span><span class="sxs-lookup"><span data-stu-id="ca62d-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="ca62d-163">Değerler:</span><span class="sxs-lookup"><span data-stu-id="ca62d-163">Values:</span></span> <br><ul><li> <span data-ttu-id="ca62d-164">`Freeze`: hello sanal makine için birkaç saniye zamanlanmış toopause değil.</span><span class="sxs-lookup"><span data-stu-id="ca62d-164">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="ca62d-165">Merhaba CPU askıya alınır ancak bellek, açık dosyalar veya ağ bağlantıları üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="ca62d-165">hello CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="ca62d-166">`Reboot`: sanal makine için yeniden başlatma Zamanlanmış Başlangıç (kalıcı olmayan bellek kaybolur).</span><span class="sxs-lookup"><span data-stu-id="ca62d-166">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="ca62d-167">`Redeploy`: hello sanal makine olan zamanlanmış toomove tooanother düğümü (kısa ömürlü diskleri kaybolur).</span><span class="sxs-lookup"><span data-stu-id="ca62d-167">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="ca62d-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="ca62d-168">ResourceType</span></span> | <span data-ttu-id="ca62d-169">Bu olay etkiler kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="ca62d-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="ca62d-170">Değerler:</span><span class="sxs-lookup"><span data-stu-id="ca62d-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="ca62d-171">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ca62d-171">Resources</span></span>| <span data-ttu-id="ca62d-172">Bu olay etkiler kaynakların listesi.</span><span class="sxs-lookup"><span data-stu-id="ca62d-172">List of resources this event impacts.</span></span> <span data-ttu-id="ca62d-173">Bu toocontain makineler en fazla bir garanti [güncelleştirme etki alanı](windows/manage-availability.md), hello UD tüm makinelerde içerebilir ancak.</span><span class="sxs-lookup"><span data-stu-id="ca62d-173">This is guaranteed toocontain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="ca62d-174">Örnek:</span><span class="sxs-lookup"><span data-stu-id="ca62d-174">Example:</span></span> <br><ul><li> <span data-ttu-id="ca62d-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="ca62d-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="ca62d-176">Olay durumu</span><span class="sxs-lookup"><span data-stu-id="ca62d-176">Event Status</span></span> | <span data-ttu-id="ca62d-177">Bu olay durumu.</span><span class="sxs-lookup"><span data-stu-id="ca62d-177">Status of this event.</span></span> <br><br> <span data-ttu-id="ca62d-178">Değerler:</span><span class="sxs-lookup"><span data-stu-id="ca62d-178">Values:</span></span> <ul><li><span data-ttu-id="ca62d-179">`Scheduled`: Bu olay hello belirtilen başlangıç saati zamanlanmış toostart sonradır `NotBefore` özelliği.</span><span class="sxs-lookup"><span data-stu-id="ca62d-179">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="ca62d-180">`Started`: Bu olay başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="ca62d-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="ca62d-181">Hayır `Completed` veya benzer durumu hiç sağlanır; hello olay, artık hello olay tamamlandığında döndürülecek.</span><span class="sxs-lookup"><span data-stu-id="ca62d-181">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="ca62d-182">NotBefore</span><span class="sxs-lookup"><span data-stu-id="ca62d-182">NotBefore</span></span>| <span data-ttu-id="ca62d-183">Süre geçtikten sonra bu olay başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="ca62d-184">Örnek:</span><span class="sxs-lookup"><span data-stu-id="ca62d-184">Example:</span></span> <br><ul><li> <span data-ttu-id="ca62d-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="ca62d-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="ca62d-186">Olay planlama</span><span class="sxs-lookup"><span data-stu-id="ca62d-186">Event Scheduling</span></span>
<span data-ttu-id="ca62d-187">Her olay zamanlanmış bir minimum süreyi hello gelecekteki olay türüne bağlı.</span><span class="sxs-lookup"><span data-stu-id="ca62d-187">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="ca62d-188">Bu süre bir olayın içinde yansıtılır `NotBefore` özelliği.</span><span class="sxs-lookup"><span data-stu-id="ca62d-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="ca62d-189">Olay türü</span><span class="sxs-lookup"><span data-stu-id="ca62d-189">EventType</span></span>  | <span data-ttu-id="ca62d-190">Minimum dikkat edin</span><span class="sxs-lookup"><span data-stu-id="ca62d-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="ca62d-191">Dondurma</span><span class="sxs-lookup"><span data-stu-id="ca62d-191">Freeze</span></span>| <span data-ttu-id="ca62d-192">15 dakika</span><span class="sxs-lookup"><span data-stu-id="ca62d-192">15 minutes</span></span> |
| <span data-ttu-id="ca62d-193">Yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="ca62d-193">Reboot</span></span> | <span data-ttu-id="ca62d-194">15 dakika</span><span class="sxs-lookup"><span data-stu-id="ca62d-194">15 minutes</span></span> |
| <span data-ttu-id="ca62d-195">Yeniden dağıtım</span><span class="sxs-lookup"><span data-stu-id="ca62d-195">Redeploy</span></span> | <span data-ttu-id="ca62d-196">10 dakika</span><span class="sxs-lookup"><span data-stu-id="ca62d-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="ca62d-197">Bir olayı başlatılıyor (hızlandırmak)</span><span class="sxs-lookup"><span data-stu-id="ca62d-197">Starting an event (expedite)</span></span>

<span data-ttu-id="ca62d-198">Yaklaşan olay öğrenilen ve normal olarak kapatmak için mantığınızı tamamlandı sonra yaparak hello bekleyen olay onaylayabilirsiniz bir `POST` çağrısı toohello meta veri hizmeti ile Merhaba `EventId`.</span><span class="sxs-lookup"><span data-stu-id="ca62d-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="ca62d-199">Bu hello minimum bildirim kısaltabilir tooAzure gösterir (uygunsa) süresi.</span><span class="sxs-lookup"><span data-stu-id="ca62d-199">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="ca62d-200">Bir olay aktarımının izni verdiği hello olay tooproceed tüm `Resources` hello olayda hello olay kabul ettikten sanal makine yalnızca hello.</span><span class="sxs-lookup"><span data-stu-id="ca62d-200">Acknowledging a event will allow hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="ca62d-201">Bu nedenle hello ilk makine hello olarak basit bir kılavuz toocoordinate hello bildirim tooelect tercih edebilirsiniz `Resources` alan.</span><span class="sxs-lookup"><span data-stu-id="ca62d-201">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="ca62d-202">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ca62d-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="ca62d-203">PowerShell örnek</span><span class="sxs-lookup"><span data-stu-id="ca62d-203">PowerShell Sample</span></span> 

<span data-ttu-id="ca62d-204">Merhaba aşağıdaki örnek sorgularda zamanlanmış olaylar için meta veri hizmeti hello ve her bekleyen olay onaylar.</span><span class="sxs-lookup"><span data-stu-id="ca62d-204">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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


### <a name="c-sample"></a><span data-ttu-id="ca62d-205">C\# örnek</span><span class="sxs-lookup"><span data-stu-id="ca62d-205">C\# Sample</span></span> 

<span data-ttu-id="ca62d-206">Merhaba aşağıdaki hello meta veri hizmeti ile iletişim kuracağını basit bir istemcinin örnektir.</span><span class="sxs-lookup"><span data-stu-id="ca62d-206">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

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

<span data-ttu-id="ca62d-207">Zamanlanmış olaylar veri yapılarını aşağıdaki hello kullanılarak temsil edilebilir:</span><span class="sxs-lookup"><span data-stu-id="ca62d-207">Scheduled Events can be represented using hello following data structures:</span></span>

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

<span data-ttu-id="ca62d-208">Merhaba aşağıdaki örnek sorgularda zamanlanmış olaylar için meta veri hizmeti hello ve her bekleyen olay onaylar.</span><span class="sxs-lookup"><span data-stu-id="ca62d-208">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

### <a name="python-sample"></a><span data-ttu-id="ca62d-209">Python örneği</span><span class="sxs-lookup"><span data-stu-id="ca62d-209">Python Sample</span></span> 

<span data-ttu-id="ca62d-210">Merhaba aşağıdaki örnek sorgularda zamanlanmış olaylar için meta veri hizmeti hello ve her bekleyen olay onaylar.</span><span class="sxs-lookup"><span data-stu-id="ca62d-210">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ca62d-211">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ca62d-211">Next Steps</span></span> 

- <span data-ttu-id="ca62d-212">Merhaba hello kullanılabilir API'ler hakkında daha fazla bilgiyi [örnek meta veri hizmeti](virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ca62d-212">Read more about hello APIs available in hello [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="ca62d-213">Hakkında bilgi edinin [planlı bakım azure'da Windows sanal makineler için](windows/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="ca62d-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="ca62d-214">Hakkında bilgi edinin [planlı bakım için Linux sanal makineleri azure'da](linux/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="ca62d-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
