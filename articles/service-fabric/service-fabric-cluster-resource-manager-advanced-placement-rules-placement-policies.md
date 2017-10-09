---
title: "aaaService doku Küme Kaynak Yöneticisi - yerleşim ilkeleri | Microsoft Docs"
description: "Ek yerleşim ilkeleri ve hizmet doku hizmetler için kuralları genel bakış"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="14054-103">Service fabric Hizmetleri için yerleşim ilkeleri</span><span class="sxs-lookup"><span data-stu-id="14054-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="14054-104">Yerleşim ilkeleri kullanılan toogovern hizmet yerleşimi bazı belirli, daha az yaygın senaryolarda olabilecek ek kurallardır.</span><span class="sxs-lookup"><span data-stu-id="14054-104">Placement policies are additional rules that can be used toogovern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="14054-105">Bu senaryolarda bazı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="14054-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="14054-106">Service Fabric kümesi coğrafi uzaklıkları, birden çok şirket içi veri merkezleri gibi veya Azure bölgelere yayılan</span><span class="sxs-lookup"><span data-stu-id="14054-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="14054-107">Birden çok alana jeopolitik veya yasal denetiminin veya İlkesi sınırları olduğu diğer bir durum ortamınızı kapsayan tooenforce gerekir</span><span class="sxs-lookup"><span data-stu-id="14054-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need tooenforce</span></span>
- <span data-ttu-id="14054-108">Son toolarge uzaklıklar veya yavaş bir veya daha az güvenilir ağ bağlantıları kullanımını iletişimi performans veya gecikme noktalar vardır</span><span class="sxs-lookup"><span data-stu-id="14054-108">There are communication performance or latency considerations due toolarge distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="14054-109">Tookeep iş yüklerini en iyi çaba, diğer iş yükleri ile veya yakınlık toocustomers olarak birlikte bulunan belirli gerekir</span><span class="sxs-lookup"><span data-stu-id="14054-109">You need tookeep certain workloads collocated as a best effort, either with other workloads or in proximity toocustomers</span></span>

<span data-ttu-id="14054-110">Bu gereksinimleri çoğunu hello fiziksel düzenini hello küme hata etki alanları hello olarak temsil hello küme ile hizalar.</span><span class="sxs-lookup"><span data-stu-id="14054-110">Most of these requirements align with hello physical layout of hello cluster, represented as hello fault domains of hello cluster.</span></span> 

<span data-ttu-id="14054-111">Merhaba adresi yardımcı olan gelişmiş yerleştirme ilkeleri bu senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="14054-111">hello advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="14054-112">Geçersiz etki alanları</span><span class="sxs-lookup"><span data-stu-id="14054-112">Invalid domains</span></span>
2. <span data-ttu-id="14054-113">Gerekli etki alanları</span><span class="sxs-lookup"><span data-stu-id="14054-113">Required domains</span></span>
3. <span data-ttu-id="14054-114">Tercih edilen etki alanları</span><span class="sxs-lookup"><span data-stu-id="14054-114">Preferred domains</span></span>
4. <span data-ttu-id="14054-115">Çoğaltma paketleme izin vermeme</span><span class="sxs-lookup"><span data-stu-id="14054-115">Disallowing replica packing</span></span>

<span data-ttu-id="14054-116">Denetimleri aşağıdaki hello çoğunu düğüm özellikleri ve kısıtlamalarından aracılığıyla yapılandırılabilir, ancak bazı daha karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="14054-116">Most of hello following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="14054-117">toomake şeyleri daha basit, hello Service Fabric kümesi kaynak yöneticisi bu ek yerleşim ilkeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="14054-117">toomake things simpler, hello Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="14054-118">Yerleşim ilkeleri tek başına adlı hizmet örneği temelinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="14054-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="14054-119">Bunlar ayrıca dinamik olarak güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="14054-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="14054-120">Geçersiz etki alanları belirtme</span><span class="sxs-lookup"><span data-stu-id="14054-120">Specifying invalid domains</span></span>
<span data-ttu-id="14054-121">Merhaba **InvalidDomain** yerleştirme ilkesi için belirli bir hizmeti belirli bir hata etki alanı geçersiz toospecify sağlar.</span><span class="sxs-lookup"><span data-stu-id="14054-121">hello **InvalidDomain** placement policy allows you toospecify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="14054-122">Bu ilke belirli bir hizmet hiçbir zaman jeopolitik veya şirket ilkesi nedenlerle örneğin belirli bir alandaki çalıştırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="14054-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="14054-123">Birden çok geçersiz etki alanı ayrı ilkeler belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="14054-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="14054-124"><center>
![Geçersiz etki alanı örneği][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="14054-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="14054-125">Kod:</span><span class="sxs-lookup"><span data-stu-id="14054-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="14054-126">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="14054-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="14054-127">Gerekli etki alanları belirtme</span><span class="sxs-lookup"><span data-stu-id="14054-127">Specifying required domains</span></span>
<span data-ttu-id="14054-128">Merhaba, etki alanı yerleştirme İlkesi hello hizmetinin yalnızca hello belirtilen etki alanında mevcut olduğunu gerektirir gereklidir.</span><span class="sxs-lookup"><span data-stu-id="14054-128">hello required domain placement policy requires that hello service is present only in hello specified domain.</span></span> <span data-ttu-id="14054-129">Birden çok gerekli etki alanı ayrı ilkeler belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="14054-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="14054-130"><center>
![Gerekli etki alanı örneği][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="14054-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="14054-131">Kod:</span><span class="sxs-lookup"><span data-stu-id="14054-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="14054-132">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="14054-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="14054-133">Tercih edilen bir etki alanı için bir durum bilgisi olan hizmet birincil çoğaltmalarının hello belirtme</span><span class="sxs-lookup"><span data-stu-id="14054-133">Specifying a preferred domain for hello primary replicas of a stateful service</span></span>
<span data-ttu-id="14054-134">Merhaba tercih edilen birincil etki alanı belirtir hello hata etki alanı tooplace birincil hello.</span><span class="sxs-lookup"><span data-stu-id="14054-134">hello Preferred Primary Domain specifies hello fault domain tooplace hello Primary in.</span></span> <span data-ttu-id="14054-135">her şeyi iyi durumda olduğunda hello birincil bu etki alanında sona erer.</span><span class="sxs-lookup"><span data-stu-id="14054-135">hello Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="14054-136">Merhaba etki alanı veya hello birincil çoğaltma başarısız olur ya da kapatıldığında, hello birincil toosome hello ideal olarak, başka bir konuma taşır. aynı etki alanı.</span><span class="sxs-lookup"><span data-stu-id="14054-136">If hello domain or hello Primary replica fails or shuts down, hello Primary moves toosome other location, ideally in hello same domain.</span></span> <span data-ttu-id="14054-137">Bu yeni konumu hello tercih edilen etki alanında değilse, mümkün olan en kısa sürede toohello tercih edilen etki alanı geri küme Resource Manager taşır hello.</span><span class="sxs-lookup"><span data-stu-id="14054-137">If this new location isn't in hello preferred domain, hello Cluster Resource Manager moves it back toohello preferred domain as soon as possible.</span></span> <span data-ttu-id="14054-138">Doğal olarak bu ayar yalnızca durum bilgisi olan hizmetler için anlamlıdır.</span><span class="sxs-lookup"><span data-stu-id="14054-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="14054-139">Birden çok veri merkezi bir konumda yerleştirme tercih Hizmetleri ancak sahip veya bu ilkeyi Azure bölgeler arasında yayılmış kümelerinde en yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="14054-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="14054-140">Tutma ana tootheir kullanıcılar ya da yardımcı olur daha düşük gecikme süresi, özellikle okuma, ana tarafından varsayılan olarak işlenir için diğer hizmetler kapatın.</span><span class="sxs-lookup"><span data-stu-id="14054-140">Keeping Primaries close tootheir users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="14054-141"><center>
![Tercih edilen birincil etki alanları ve yük devretme][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="14054-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="14054-142">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="14054-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="14054-143">Çoğaltma dağıtım gerektiren ve paket vermemek</span><span class="sxs-lookup"><span data-stu-id="14054-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="14054-144">Çoğaltmaları _normalde_ hello küme iyi durumda olduğunda hata ve yükseltme etki alanları arasında dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="14054-144">Replicas are _normally_ distributed across fault and upgrade domains when hello cluster is healthy.</span></span> <span data-ttu-id="14054-145">Ancak, belirli bir bölüm için birden fazla çoğaltma burada anlamayabilir durumlar vardır tek bir etki alanına geçici olarak paketlenmiş.</span><span class="sxs-lookup"><span data-stu-id="14054-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="14054-146">Örneğin, bu hello küme sahip dokuz düğümleri üç hata etki alanlarında, fd varsayalım: / 0, fd: / 1 ve fd: / 2.</span><span class="sxs-lookup"><span data-stu-id="14054-146">For example, let's say that hello cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="14054-147">Ayrıca hizmetinizi üç çoğaltmaları olduğunu düşünelim.</span><span class="sxs-lookup"><span data-stu-id="14054-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="14054-148">Diyelim ki bu hello fd içinde bu çoğaltmalar için kullanılmakta düğümler: / 1 ve fd: / 2 kapandı.</span><span class="sxs-lookup"><span data-stu-id="14054-148">Let's say that hello nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="14054-149">Normalde hello küme kaynak yöneticisi bu aynı hata etki alanları içindeki diğer düğümlere tercih edebilir.</span><span class="sxs-lookup"><span data-stu-id="14054-149">Normally hello Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="14054-150">Bu durumda, toocapacity sorunları hiçbiri düşünelim Merhaba diğer düğümler bu etki alanlarındaki geçerli.</span><span class="sxs-lookup"><span data-stu-id="14054-150">In this case, let's say due toocapacity issues none of hello other nodes in those domains were valid.</span></span> <span data-ttu-id="14054-151">Merhaba küme Resource Manager yinelemeler donanımlarının oluşturursa fd toochoose düğümleri gerekir: / 0.</span><span class="sxs-lookup"><span data-stu-id="14054-151">If hello Cluster Resource Manager builds replacements for those replicas, it would have toochoose nodes in fd:/0.</span></span> <span data-ttu-id="14054-152">Ancak, bulunurken _,_ nerede hello hata etki alanı kısıtlaması ihlal bir durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="14054-152">However, doing _that_ creates a situation where hello Fault Domain constraint is violated.</span></span> <span data-ttu-id="14054-153">Çoğaltmaları arttıkça tüm çoğaltma kümesi hello hello fırsat paketleme, Git aşağı oluşturulamadı veya kaybolur.</span><span class="sxs-lookup"><span data-stu-id="14054-153">Packing replicas increases hello chance that hello whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="14054-154">Kısıtlamalar ve kısıtlama hakkında daha fazla bilgi için öncelikleri genellikle kullanıma [bu konuda](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="14054-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="14054-155">Herhangi bir zamanda bir sistem durumu ileti gibi gördüğünüz ise "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", bu koşulu veya onu şöyle ziyaret sonra.</span><span class="sxs-lookup"><span data-stu-id="14054-155">If you've ever seen a health message such as "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="14054-156">Genellikle yalnızca bir veya iki çoğaltmaları paketlenmiş birlikte geçici olarak.</span><span class="sxs-lookup"><span data-stu-id="14054-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="14054-157">Vardır sürece çoğaltmalarının belirli bir etki alanındaki bir çekirdek daha az, güvenli.</span><span class="sxs-lookup"><span data-stu-id="14054-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="14054-158">Paketleme nadir, ancak olabilir ve bu gibi durumlarda hello düğümleri geri dönmeden bu yana genellikle geçicidir.</span><span class="sxs-lookup"><span data-stu-id="14054-158">Packing is rare, but it can happen, and usually these situations are transient since hello nodes come back.</span></span> <span data-ttu-id="14054-159">Merhaba düğümleri kapalı kalmasını ve hello küme Resource Manager toobuild değişikliklerini gerekirse genellikle yok diğer düğümlere hello ideal hata etki alanı.</span><span class="sxs-lookup"><span data-stu-id="14054-159">If hello nodes do stay down and hello Cluster Resource Manager needs toobuild replacements, usually there are other nodes available in hello ideal fault domains.</span></span>

<span data-ttu-id="14054-160">Bunlar daha az etki alanlarına paketlenmiş bile, bazı iş yükleri hello hedef sayısını çoğaltmalar, her zaman sahip tercih edebilir.</span><span class="sxs-lookup"><span data-stu-id="14054-160">Some workloads would prefer always having hello target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="14054-161">Bu iş yükleri toplam eşzamanlı kalıcı etki alanı arızalarına karşı beklemek ve genellikle yerel durumu kurtarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14054-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="14054-162">Diğer iş yükleri yerine hello kapalı kalma riskini doğruluk veya veri kaybı'den önceki alır.</span><span class="sxs-lookup"><span data-stu-id="14054-162">Other workloads would rather take hello downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="14054-163">Çoğu üretim iş yükleri üçten fazla çoğaltmalar, üçten fazla hata etki alanları ve hata etki alanı başına çok sayıda geçerli düğüm çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="14054-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="14054-164">Bu nedenle, hello varsayılan davranışı varsayılan olarak etki alanı paketleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="14054-164">Because of this, hello default behavior allows domain packing by default.</span></span> <span data-ttu-id="14054-165">Geçici etki alanı paketleme anlamına olsa bile hello varsayılan davranış bu gibi olağanüstü durumlarda, normal Dengeleme ve yük devretme toohandle sağlar.</span><span class="sxs-lookup"><span data-stu-id="14054-165">hello default behavior allows normal balancing and failover toohandle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="14054-166">Bu tür paketleme belirli bir iş yükü için toodisable istiyorsanız, hello belirtebilirsiniz `RequireDomainDistribution` hello hizmet ilkesi.</span><span class="sxs-lookup"><span data-stu-id="14054-166">If you want toodisable such packing for a given workload, you can specify hello `RequireDomainDistribution` policy on hello service.</span></span> <span data-ttu-id="14054-167">Bu ilkeyi ayarladığınızda hello Küme Kaynak Yöneticisi'ni aynı bölüme çalıştırmak aynı arıza veya etki alanı yükseltme hello hello iki hiçbir çoğaltmalardan sağlar.</span><span class="sxs-lookup"><span data-stu-id="14054-167">When this policy is set, hello Cluster Resource Manager ensures no two replicas from hello same partition run in hello same fault or upgrade domain.</span></span>

<span data-ttu-id="14054-168">Kod:</span><span class="sxs-lookup"><span data-stu-id="14054-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="14054-169">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="14054-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="14054-170">Şimdi, misiniz değil coğrafi olarak dağıtılmış bir Küme Hizmetleri için bu yapılandırmalar olası toouse olabilir?</span><span class="sxs-lookup"><span data-stu-id="14054-170">Now, would it be possible toouse these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="14054-171">Olabilir, ancak yok. büyük bir nedenle çok.</span><span class="sxs-lookup"><span data-stu-id="14054-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="14054-172">Merhaba senaryoları bunları gerektirmedikçe hello gerekli, geçersiz ve tercih edilen etki alanı yapılandırmaları kaçınılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="14054-172">hello required, invalid, and preferred domain configurations should be avoided unless hello scenarios require them.</span></span> <span data-ttu-id="14054-173">Bunu tüm algılama tootry tooforce belirli iş yükü toorun bir tek raf veya tooprefer yapmaz yerel kümenizin başka üzerinden bazı kesimi.</span><span class="sxs-lookup"><span data-stu-id="14054-173">It doesn't make any sense tootry tooforce a given workload toorun in a single rack, or tooprefer some segment of your local cluster over another.</span></span> <span data-ttu-id="14054-174">Farklı donanım yapılandırmaları hata etki alanlarında yayılan ve normal kısıtlamalarından ve düğüm özellikleri aracılığıyla işlenen.</span><span class="sxs-lookup"><span data-stu-id="14054-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14054-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="14054-175">Next steps</span></span>
- <span data-ttu-id="14054-176">Hizmetleri yapılandırma hakkında daha fazla bilgi için [hizmetleri yapılandırma hakkında bilgi edinin](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="14054-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
