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
# <a name="placement-policies-for-service-fabric-services"></a>Service fabric Hizmetleri için yerleşim ilkeleri
Yerleşim ilkeleri kullanılan toogovern hizmet yerleşimi bazı belirli, daha az yaygın senaryolarda olabilecek ek kurallardır. Bu senaryolarda bazı örnekleri şunlardır:

- Service Fabric kümesi coğrafi uzaklıkları, birden çok şirket içi veri merkezleri gibi veya Azure bölgelere yayılan
- Birden çok alana jeopolitik veya yasal denetiminin veya İlkesi sınırları olduğu diğer bir durum ortamınızı kapsayan tooenforce gerekir
- Son toolarge uzaklıklar veya yavaş bir veya daha az güvenilir ağ bağlantıları kullanımını iletişimi performans veya gecikme noktalar vardır
- Tookeep iş yüklerini en iyi çaba, diğer iş yükleri ile veya yakınlık toocustomers olarak birlikte bulunan belirli gerekir

Bu gereksinimleri çoğunu hello fiziksel düzenini hello küme hata etki alanları hello olarak temsil hello küme ile hizalar. 

Merhaba adresi yardımcı olan gelişmiş yerleştirme ilkeleri bu senaryolar şunlardır:

1. Geçersiz etki alanları
2. Gerekli etki alanları
3. Tercih edilen etki alanları
4. Çoğaltma paketleme izin vermeme

Denetimleri aşağıdaki hello çoğunu düğüm özellikleri ve kısıtlamalarından aracılığıyla yapılandırılabilir, ancak bazı daha karmaşıktır. toomake şeyleri daha basit, hello Service Fabric kümesi kaynak yöneticisi bu ek yerleşim ilkeleri sağlar. Yerleşim ilkeleri tek başına adlı hizmet örneği temelinde yapılandırılır. Bunlar ayrıca dinamik olarak güncelleştirilebilir.

## <a name="specifying-invalid-domains"></a>Geçersiz etki alanları belirtme
Merhaba **InvalidDomain** yerleştirme ilkesi için belirli bir hizmeti belirli bir hata etki alanı geçersiz toospecify sağlar. Bu ilke belirli bir hizmet hiçbir zaman jeopolitik veya şirket ilkesi nedenlerle örneğin belirli bir alandaki çalıştırmasını sağlar. Birden çok geçersiz etki alanı ayrı ilkeler belirtilebilir.

<center>
![Geçersiz etki alanı örneği][Image1]
</center>

Kod:

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a>Gerekli etki alanları belirtme
Merhaba, etki alanı yerleştirme İlkesi hello hizmetinin yalnızca hello belirtilen etki alanında mevcut olduğunu gerektirir gereklidir. Birden çok gerekli etki alanı ayrı ilkeler belirtilebilir.

<center>
![Gerekli etki alanı örneği][Image2]
</center>

Kod:

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a>Tercih edilen bir etki alanı için bir durum bilgisi olan hizmet birincil çoğaltmalarının hello belirtme
Merhaba tercih edilen birincil etki alanı belirtir hello hata etki alanı tooplace birincil hello. her şeyi iyi durumda olduğunda hello birincil bu etki alanında sona erer. Merhaba etki alanı veya hello birincil çoğaltma başarısız olur ya da kapatıldığında, hello birincil toosome hello ideal olarak, başka bir konuma taşır. aynı etki alanı. Bu yeni konumu hello tercih edilen etki alanında değilse, mümkün olan en kısa sürede toohello tercih edilen etki alanı geri küme Resource Manager taşır hello. Doğal olarak bu ayar yalnızca durum bilgisi olan hizmetler için anlamlıdır. Birden çok veri merkezi bir konumda yerleştirme tercih Hizmetleri ancak sahip veya bu ilkeyi Azure bölgeler arasında yayılmış kümelerinde en yararlı olur. Tutma ana tootheir kullanıcılar ya da yardımcı olur daha düşük gecikme süresi, özellikle okuma, ana tarafından varsayılan olarak işlenir için diğer hizmetler kapatın.

<center>
![Tercih edilen birincil etki alanları ve yük devretme][Image3]
</center>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a>Çoğaltma dağıtım gerektiren ve paket vermemek
Çoğaltmaları _normalde_ hello küme iyi durumda olduğunda hata ve yükseltme etki alanları arasında dağıtılmış. Ancak, belirli bir bölüm için birden fazla çoğaltma burada anlamayabilir durumlar vardır tek bir etki alanına geçici olarak paketlenmiş. Örneğin, bu hello küme sahip dokuz düğümleri üç hata etki alanlarında, fd varsayalım: / 0, fd: / 1 ve fd: / 2. Ayrıca hizmetinizi üç çoğaltmaları olduğunu düşünelim. Diyelim ki bu hello fd içinde bu çoğaltmalar için kullanılmakta düğümler: / 1 ve fd: / 2 kapandı. Normalde hello küme kaynak yöneticisi bu aynı hata etki alanları içindeki diğer düğümlere tercih edebilir. Bu durumda, toocapacity sorunları hiçbiri düşünelim Merhaba diğer düğümler bu etki alanlarındaki geçerli. Merhaba küme Resource Manager yinelemeler donanımlarının oluşturursa fd toochoose düğümleri gerekir: / 0. Ancak, bulunurken _,_ nerede hello hata etki alanı kısıtlaması ihlal bir durum oluşturur. Çoğaltmaları arttıkça tüm çoğaltma kümesi hello hello fırsat paketleme, Git aşağı oluşturulamadı veya kaybolur. 

> [!NOTE]
> Kısıtlamalar ve kısıtlama hakkında daha fazla bilgi için öncelikleri genellikle kullanıma [bu konuda](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).
>

Herhangi bir zamanda bir sistem durumu ileti gibi gördüğünüz ise "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", bu koşulu veya onu şöyle ziyaret sonra. Genellikle yalnızca bir veya iki çoğaltmaları paketlenmiş birlikte geçici olarak. Vardır sürece çoğaltmalarının belirli bir etki alanındaki bir çekirdek daha az, güvenli. Paketleme nadir, ancak olabilir ve bu gibi durumlarda hello düğümleri geri dönmeden bu yana genellikle geçicidir. Merhaba düğümleri kapalı kalmasını ve hello küme Resource Manager toobuild değişikliklerini gerekirse genellikle yok diğer düğümlere hello ideal hata etki alanı.

Bunlar daha az etki alanlarına paketlenmiş bile, bazı iş yükleri hello hedef sayısını çoğaltmalar, her zaman sahip tercih edebilir. Bu iş yükleri toplam eşzamanlı kalıcı etki alanı arızalarına karşı beklemek ve genellikle yerel durumu kurtarabilirsiniz. Diğer iş yükleri yerine hello kapalı kalma riskini doğruluk veya veri kaybı'den önceki alır. Çoğu üretim iş yükleri üçten fazla çoğaltmalar, üçten fazla hata etki alanları ve hata etki alanı başına çok sayıda geçerli düğüm çalıştırın. Bu nedenle, hello varsayılan davranışı varsayılan olarak etki alanı paketleme sağlar. Geçici etki alanı paketleme anlamına olsa bile hello varsayılan davranış bu gibi olağanüstü durumlarda, normal Dengeleme ve yük devretme toohandle sağlar.

Bu tür paketleme belirli bir iş yükü için toodisable istiyorsanız, hello belirtebilirsiniz `RequireDomainDistribution` hello hizmet ilkesi. Bu ilkeyi ayarladığınızda hello Küme Kaynak Yöneticisi'ni aynı bölüme çalıştırmak aynı arıza veya etki alanı yükseltme hello hello iki hiçbir çoğaltmalardan sağlar.

Kod:

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

Şimdi, misiniz değil coğrafi olarak dağıtılmış bir Küme Hizmetleri için bu yapılandırmalar olası toouse olabilir? Olabilir, ancak yok. büyük bir nedenle çok. Merhaba senaryoları bunları gerektirmedikçe hello gerekli, geçersiz ve tercih edilen etki alanı yapılandırmaları kaçınılmalıdır. Bunu tüm algılama tootry tooforce belirli iş yükü toorun bir tek raf veya tooprefer yapmaz yerel kümenizin başka üzerinden bazı kesimi. Farklı donanım yapılandırmaları hata etki alanlarında yayılan ve normal kısıtlamalarından ve düğüm özellikleri aracılığıyla işlenen.

## <a name="next-steps"></a>Sonraki adımlar
- Hizmetleri yapılandırma hakkında daha fazla bilgi için [hizmetleri yapılandırma hakkında bilgi edinin](service-fabric-cluster-resource-manager-configure-services.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
