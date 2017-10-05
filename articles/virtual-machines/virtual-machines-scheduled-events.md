---
title: "Azure meta veri hizmeti olaylarla zamanlanmış | Microsoft Docs"
description: "Gerçekleşmeden önce sanal makinenizde Impactful olaylarına tepki."
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
ms.openlocfilehash: 793803bfc12059a68ec881da9de37116f7a0eb8c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="2c495-103">Azure meta veri hizmeti - zamanlanmış olaylar (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="2c495-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="2c495-104">Kullanım koşullarını kabul ediyorum koşuluyla önizlemeleri için kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="2c495-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="2c495-105">Daha fazla bilgi için bkz. [Microsoft Azure Önizlemeleri için Microsoft Azure Ek Kullanım Koşulları](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="2c495-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="2c495-106">Zamanlanmış olaylar biridir alt Servisleri Azure meta veri hizmeti altında.</span><span class="sxs-lookup"><span data-stu-id="2c495-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="2c495-107">Yaklaşan olayları ile ilgili bilgiler görünmesini sorumludur (örneğin, yeniden başlatma) uygulamanız için hazırlamak ve sınırlamak için kesintisi.</span><span class="sxs-lookup"><span data-stu-id="2c495-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="2c495-108">PaaS ve Iaas dahil olmak üzere tüm Azure sanal makine türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2c495-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="2c495-109">Zamanlanmış olayları olay etkisini en aza indirmek için önleyici görevleri gerçekleştirmek için sanal makine zaman verir.</span><span class="sxs-lookup"><span data-stu-id="2c495-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="2c495-110">Giriş - neden zamanlanmış olayları?</span><span class="sxs-lookup"><span data-stu-id="2c495-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="2c495-111">Zamanlanmış olaylarla platform intiated Bakım veya hizmetinizi kullanıcı tarafından başlatılan Eylemler etkisini sınırlamak üzere adım atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c495-111">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="2c495-112">Durumunu korumak için çoğaltma tekniklerini kullanın, çok örnekli iş yükleri arasında birden çok örneği gerçekleştiği kesintileri etkilenebilir.</span><span class="sxs-lookup"><span data-stu-id="2c495-112">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="2c495-113">Bu tür kayıpları, pahalı görevler (örneğin, yeniden dizinler) veya çoğaltma kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="2c495-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="2c495-114">Çoğu durumda, genel hizmet kullanılabilirliği geliştirilmiş bir kapama sırası gibi gerçekleştirerek (el ile yük devretme) kümedeki diğer Vm'lerle görevlere yeniden atama ya da sanal kaldırılması Tamamlanıyor (veya iptal etme) yürütülen işlemler, Ağ Yük Dengeleyici havuzuna makineden.</span><span class="sxs-lookup"><span data-stu-id="2c495-114">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="2c495-115">Burada yöneticinin yaklaşan bir olay hakkında bilgilendirmek veya böyle bir olay günlüğü yardımcı bakım yapılabilirliğini bulutta barındırılan uygulamalar geliştirme durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="2c495-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="2c495-116">Azure meta veri hizmeti zamanlanmış olayları aşağıdaki kullanım örneklerini ortaya çıkarır:</span><span class="sxs-lookup"><span data-stu-id="2c495-116">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="2c495-117">Başlatılan platform Bakım (örneğin, ana bilgisayar işletim sistemi dağıtımı)</span><span class="sxs-lookup"><span data-stu-id="2c495-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="2c495-118">Kullanıcı tarafından başlatılan çağrıları (örneğin, kullanıcı yeniden başlatma veya yeniden dağıtır VM)</span><span class="sxs-lookup"><span data-stu-id="2c495-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---the-basics"></a><span data-ttu-id="2c495-119">Zamanlanmış etkinlikleri - temel</span><span class="sxs-lookup"><span data-stu-id="2c495-119">Scheduled Events - The Basics</span></span>  

<span data-ttu-id="2c495-120">Azure meta veri hizmeti REST uç noktasını VM içinden erişilebilen kullanarak sanal makineleri çalıştırma hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="2c495-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="2c495-121">Böylece dışında VM gösterilmeyen bilgileri yönlendirilemeyen bir IP kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2c495-121">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="2c495-122">Kapsam</span><span class="sxs-lookup"><span data-stu-id="2c495-122">Scope</span></span>
<span data-ttu-id="2c495-123">Zamanlanmış olaylar, tüm sanal makineler bir bulut hizmetinde veya bir kullanılabilirlik kümesindeki tüm sanal makineleri çıkmış.</span><span class="sxs-lookup"><span data-stu-id="2c495-123">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="2c495-124">Sonuç olarak, denetlemelisiniz `Resources` hangi VM'ler etkilenir olacak tanımlamak için olay alanındaki.</span><span class="sxs-lookup"><span data-stu-id="2c495-124">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="2c495-125">Uç nokta keşfetme</span><span class="sxs-lookup"><span data-stu-id="2c495-125">Discovering the Endpoint</span></span>
<span data-ttu-id="2c495-126">Bir sanal makine bir sanal ağ (VNet) içinde oluşturulduğu olduğu durumda meta veri hizmeti bir statik yönlendirilemeyen bir IP, kullanılabilir `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="2c495-126">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="2c495-127">Bulut Hizmetleri ve klasik sanal makineleri için varsayılan durumlar bir sanal ağ içinde sanal makine oluşturulmamışsa ek mantık kullanmak için uç nokta bulmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2c495-127">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="2c495-128">Bilgi edinmek için bu örneğe bakın nasıl [konak uç noktası bulunamadı](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="2c495-128">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="2c495-129">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c495-129">Versioning</span></span> 
<span data-ttu-id="2c495-130">Örnek meta veri sürümü tutulan hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="2c495-130">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="2c495-131">Sürümleri zorunludur ve geçerli sürümü `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="2c495-131">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="2c495-132">Önceki Önizleme sürümleri {son} API sürümü desteklenen zamanlanmış olaylar.</span><span class="sxs-lookup"><span data-stu-id="2c495-132">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="2c495-133">Bu biçim artık desteklenmemektedir ve gelecekte kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="2c495-133">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="2c495-134">Üst bilgileri kullanma</span><span class="sxs-lookup"><span data-stu-id="2c495-134">Using Headers</span></span>
<span data-ttu-id="2c495-135">Meta veri hizmeti sorguladığınızda başlık sağlamalısınız `Metadata: true` istek istemeden yönlendirilmeyen emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="2c495-135">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="2c495-136">Zamanlanmış olayları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2c495-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="2c495-137">Zamanlanmış olaylar, istekte ilk kez Azure örtük olarak sanal makinenizde özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="2c495-137">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="2c495-138">Sonuç olarak, iki dakika içinde ilk çağrıda Gecikmeli yanıt beklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="2c495-138">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="2c495-139">Kullanıcı tarafından başlatılan bakım</span><span class="sxs-lookup"><span data-stu-id="2c495-139">User Initiated Maintenance</span></span>
<span data-ttu-id="2c495-140">Sanal makine Bakımı API, CLI, Azure Portalı aracılığıyla kullanıcı tarafından başlatılan veya PowerShell zamanlanmış olayları neden olur.</span><span class="sxs-lookup"><span data-stu-id="2c495-140">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="2c495-141">Bu bakım hazırlık mantığı uygulamanıza test etmenizi sağlar ve kullanıcı tarafından başlatılan bakım için hazırlamak uygulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2c495-141">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="2c495-142">Bir olay türüne sahip bir sanal makinenin yeniden başlatılması zamanlama `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="2c495-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="2c495-143">Bir olay türüne sahip bir sanal makine yeniden zamanlama `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="2c495-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="2c495-144">Şu anda en fazla 10 kullanıcı tarafından başlatılan bakım işlemleri aynı anda zamanlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2c495-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="2c495-145">Bu sınır olayları genel kullanılabilirlik zamanlanmış önce rahat olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2c495-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="2c495-146">Şu anda zamanlanmış olayları kaynaklanan kullanıcı tarafından başlatılan bakım yapılandırılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="2c495-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="2c495-147">Yapılandırılabilirlik gelecekteki bir sürümde planlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2c495-147">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="2c495-148">API'yi kullanma</span><span class="sxs-lookup"><span data-stu-id="2c495-148">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="2c495-149">Olaylar için sorgu</span><span class="sxs-lookup"><span data-stu-id="2c495-149">Query for events</span></span>
<span data-ttu-id="2c495-150">Aşağıdaki çağrıyı yaparak zamanlanmış olaylar için sorgulama yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2c495-150">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="2c495-151">Bir yanıt zamanlanmış olaylar dizisini içerir.</span><span class="sxs-lookup"><span data-stu-id="2c495-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="2c495-152">Boş bir dizi var. şu anda zamanlanmış bir olay yok demektir.</span><span class="sxs-lookup"><span data-stu-id="2c495-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="2c495-153">Durumda Zamanlanmış olaylar olduğu yanıtı olaylar dizisini içerir:</span><span class="sxs-lookup"><span data-stu-id="2c495-153">In the case where there are scheduled events, the response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="2c495-154">Olay Özellikleri</span><span class="sxs-lookup"><span data-stu-id="2c495-154">Event Properties</span></span>
|<span data-ttu-id="2c495-155">Özellik</span><span class="sxs-lookup"><span data-stu-id="2c495-155">Property</span></span>  |  <span data-ttu-id="2c495-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2c495-156">Description</span></span> |
| - | - |
| <span data-ttu-id="2c495-157">Olay Kimliği</span><span class="sxs-lookup"><span data-stu-id="2c495-157">EventId</span></span> | <span data-ttu-id="2c495-158">Bu olay için genel benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="2c495-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="2c495-159">Örnek:</span><span class="sxs-lookup"><span data-stu-id="2c495-159">Example:</span></span> <br><ul><li><span data-ttu-id="2c495-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="2c495-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="2c495-161">Olay türü</span><span class="sxs-lookup"><span data-stu-id="2c495-161">EventType</span></span> | <span data-ttu-id="2c495-162">Bu olaya neden olan etkisi.</span><span class="sxs-lookup"><span data-stu-id="2c495-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="2c495-163">Değerler:</span><span class="sxs-lookup"><span data-stu-id="2c495-163">Values:</span></span> <br><ul><li> <span data-ttu-id="2c495-164">`Freeze`: Sanal makine, birkaç saniye duraklatmak için zamanlandı.</span><span class="sxs-lookup"><span data-stu-id="2c495-164">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="2c495-165">CPU askıya alınır, ancak bellek, açık dosyalar veya ağ bağlantıları üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="2c495-165">The CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="2c495-166">`Reboot`: Sanal makine yeniden başlatma için planlanmıştır (kalıcı olmayan bellek kaybolur).</span><span class="sxs-lookup"><span data-stu-id="2c495-166">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="2c495-167">`Redeploy`: Sanal makine başka bir düğüme taşımak için planlanmıştır (kısa ömürlü diskleri kaybolur).</span><span class="sxs-lookup"><span data-stu-id="2c495-167">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="2c495-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="2c495-168">ResourceType</span></span> | <span data-ttu-id="2c495-169">Bu olay etkiler kaynak türü.</span><span class="sxs-lookup"><span data-stu-id="2c495-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="2c495-170">Değerler:</span><span class="sxs-lookup"><span data-stu-id="2c495-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="2c495-171">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2c495-171">Resources</span></span>| <span data-ttu-id="2c495-172">Bu olay etkiler kaynakların listesi.</span><span class="sxs-lookup"><span data-stu-id="2c495-172">List of resources this event impacts.</span></span> <span data-ttu-id="2c495-173">Bu en fazla bir makinelerden içeren garanti [güncelleştirme etki alanı](windows/manage-availability.md), UD tüm makinelerde içerebilir ancak.</span><span class="sxs-lookup"><span data-stu-id="2c495-173">This is guaranteed to contain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="2c495-174">Örnek:</span><span class="sxs-lookup"><span data-stu-id="2c495-174">Example:</span></span> <br><ul><li> <span data-ttu-id="2c495-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="2c495-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="2c495-176">Olay durumu</span><span class="sxs-lookup"><span data-stu-id="2c495-176">Event Status</span></span> | <span data-ttu-id="2c495-177">Bu olay durumu.</span><span class="sxs-lookup"><span data-stu-id="2c495-177">Status of this event.</span></span> <br><br> <span data-ttu-id="2c495-178">Değerler:</span><span class="sxs-lookup"><span data-stu-id="2c495-178">Values:</span></span> <ul><li><span data-ttu-id="2c495-179">`Scheduled`: Bu olay belirtilen süre sonra başlayacak şekilde zamanlanırsa `NotBefore` özelliği.</span><span class="sxs-lookup"><span data-stu-id="2c495-179">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="2c495-180">`Started`: Bu olay başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="2c495-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="2c495-181">Hayır `Completed` veya benzer durumu hiç sağlanır; olay tamamlandığında, artık olay döndürülür.</span><span class="sxs-lookup"><span data-stu-id="2c495-181">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="2c495-182">NotBefore</span><span class="sxs-lookup"><span data-stu-id="2c495-182">NotBefore</span></span>| <span data-ttu-id="2c495-183">Süre geçtikten sonra bu olay başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="2c495-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="2c495-184">Örnek:</span><span class="sxs-lookup"><span data-stu-id="2c495-184">Example:</span></span> <br><ul><li> <span data-ttu-id="2c495-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="2c495-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="2c495-186">Olay planlama</span><span class="sxs-lookup"><span data-stu-id="2c495-186">Event Scheduling</span></span>
<span data-ttu-id="2c495-187">Her olay zamanlanmış bir minimum süre gelecekte olay türüne bağlı.</span><span class="sxs-lookup"><span data-stu-id="2c495-187">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="2c495-188">Bu süre bir olayın içinde yansıtılır `NotBefore` özelliği.</span><span class="sxs-lookup"><span data-stu-id="2c495-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="2c495-189">Olay türü</span><span class="sxs-lookup"><span data-stu-id="2c495-189">EventType</span></span>  | <span data-ttu-id="2c495-190">Minimum dikkat edin</span><span class="sxs-lookup"><span data-stu-id="2c495-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="2c495-191">Dondurma</span><span class="sxs-lookup"><span data-stu-id="2c495-191">Freeze</span></span>| <span data-ttu-id="2c495-192">15 dakika</span><span class="sxs-lookup"><span data-stu-id="2c495-192">15 minutes</span></span> |
| <span data-ttu-id="2c495-193">Yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="2c495-193">Reboot</span></span> | <span data-ttu-id="2c495-194">15 dakika</span><span class="sxs-lookup"><span data-stu-id="2c495-194">15 minutes</span></span> |
| <span data-ttu-id="2c495-195">Yeniden dağıtım</span><span class="sxs-lookup"><span data-stu-id="2c495-195">Redeploy</span></span> | <span data-ttu-id="2c495-196">10 dakika</span><span class="sxs-lookup"><span data-stu-id="2c495-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="2c495-197">Bir olayı başlatılıyor (hızlandırmak)</span><span class="sxs-lookup"><span data-stu-id="2c495-197">Starting an event (expedite)</span></span>

<span data-ttu-id="2c495-198">Yaklaşan olay öğrenilen ve normal olarak kapatmak için mantığınızı tamamlandı sonra yaparak bekleyen olay onaylayabilirsiniz bir `POST` çağrısı ile meta veri hizmetine `EventId`.</span><span class="sxs-lookup"><span data-stu-id="2c495-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="2c495-199">Bu, en düşük bildirim kısaltabilir Azure'a gösterir (uygunsa) süresi.</span><span class="sxs-lookup"><span data-stu-id="2c495-199">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="2c495-200">Bir olay aktarımının tüm devam etmek olay izni verdiği `Resources` olay bildirir yalnızca sanal makine durumunda.</span><span class="sxs-lookup"><span data-stu-id="2c495-200">Acknowledging a event will allow the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="2c495-201">Bu nedenle ilk makine olarak basit bildirim koordine etmek için bir kılavuz seçmediğiniz seçebileceği `Resources` alan.</span><span class="sxs-lookup"><span data-stu-id="2c495-201">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="2c495-202">Örnekler</span><span class="sxs-lookup"><span data-stu-id="2c495-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="2c495-203">PowerShell örnek</span><span class="sxs-lookup"><span data-stu-id="2c495-203">PowerShell Sample</span></span> 

<span data-ttu-id="2c495-204">Aşağıdaki örnek, zamanlanmış olaylar için meta veri hizmeti sorgular ve her bekleyen olay onaylar.</span><span class="sxs-lookup"><span data-stu-id="2c495-204">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How to get scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How to approve a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create the Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert to JSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with the following: `n" $approvalString

    # Post approval string to scheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up the scheduled events URI for a VNET-enabled VM
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


### <a name="c-sample"></a><span data-ttu-id="2c495-205">C\# örnek</span><span class="sxs-lookup"><span data-stu-id="2c495-205">C\# Sample</span></span> 

<span data-ttu-id="2c495-206">Meta veri hizmeti ile iletişim kuracağını basit bir istemci, aşağıdaki örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2c495-206">The following sample is of a simple client that communicates with the metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up the scheduled events URI for a VNET-enabled VM
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

<span data-ttu-id="2c495-207">Zamanlanmış olaylar aşağıdaki veri yapılarını kullanılarak temsil edilebilir:</span><span class="sxs-lookup"><span data-stu-id="2c495-207">Scheduled Events can be represented using the following data structures:</span></span>

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

<span data-ttu-id="2c495-208">Aşağıdaki örnek, zamanlanmış olaylar için meta veri hizmeti sorgular ve her bekleyen olay onaylar.</span><span class="sxs-lookup"><span data-stu-id="2c495-208">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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
            Console.WriteLine("Press Enter to approve executing events\n");
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

            Console.WriteLine("Complete. Press enter to repeat\n\n");
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

### <a name="python-sample"></a><span data-ttu-id="2c495-209">Python örneği</span><span class="sxs-lookup"><span data-stu-id="2c495-209">Python Sample</span></span> 

<span data-ttu-id="2c495-210">Aşağıdaki örnek, zamanlanmış olaylar için meta veri hizmeti sorgular ve her bekleyen olay onaylar.</span><span class="sxs-lookup"><span data-stu-id="2c495-210">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2c495-211">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="2c495-211">Next Steps</span></span> 

- <span data-ttu-id="2c495-212">Kullanılabilen API'leri hakkında daha fazla bilgiyi [örnek meta veri hizmeti](virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c495-212">Read more about the APIs available in the [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="2c495-213">Hakkında bilgi edinin [planlı bakım azure'da Windows sanal makineler için](windows/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="2c495-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="2c495-214">Hakkında bilgi edinin [planlı bakım için Linux sanal makineleri azure'da](linux/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="2c495-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
