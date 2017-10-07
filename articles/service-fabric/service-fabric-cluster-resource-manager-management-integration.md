---
title: "aaaService doku Küme Kaynak Yöneticisi - Yönetim tümleştirme | Microsoft Docs"
description: "Merhaba tümleştirme noktaları hello Küme Kaynak Yöneticisi ve hizmet doku Yönetimi arasında genel bakış."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 956cd0b8-b6e3-4436-a224-8766320e8cd7
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9a24c9de121fbe2e8e5e8e4d117e64686918936a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-integration-with-service-fabric-cluster-management"></a>Service Fabric kümesi yönetimi ile Küme Kaynak Yöneticisi tümleştirme
Service Fabric yükseltme Hello Service Fabric kümesi Kaynak Yöneticisi sürücü değil, ancak söz konusu. Merhaba hello Küme Kaynak Yöneticisi yardımcı yönetimi ile izleme hello tarafından ilk şekilde hello küme ve onun içindeki hello Hizmetleri durumunu istenen. Bunu hello küme hello istenen yapılandırma yerleştirin zaman hello küme Resource Manager sistem durumu raporlarını gönderir. Örneğin, varsa yeterli kapasitesi hello küme Resource Manager sistem durumu uyarıları ve hataları hello sorunu belirten gönderir. Başka bir parçasını tümleştirme yükseltme nasıl çalışır ile toodo sahiptir. Merhaba küme Resource Manager davranışını biraz yükseltmeler sırasında değiştirir.  

## <a name="health-integration"></a>Sistem durumu tümleştirme
Merhaba küme Resource Manager hizmetlerinizi yerleştirmek için tanımladığınız hello kuralları sürekli olarak izler. Ayrıca, bir bütün olarak hello düğümlerinde ve hello kümedeki ve hello kümedeki her ölçümü için kapasite kalan hello izler. Bu kurallar gerçekleştiremiyor veya yeterli kapasitesi varsa, sistem durumu uyarıları ve hataları gösterilen. Örneğin, bir düğüm kapasitesi ve hello ise küme kaynak yöneticisi hizmetleri taşıyarak toofix hello durum çalışacaktır. Merhaba durum düzeltemezsiniz, hangi düğümün hangi ölçümleri ve kapasite üzerinden olduğunu belirten bir sistem durumu uyarısı yayar.

Başka bir hello Resource Manager'ın sistem durumu uyarıları kısıtlamalarından ihlalleri örnektir. Örneğin, bir yerleştirme kısıtlaması tanımladıysanız (gibi `“NodeColor == Blue”`) ve hello Resource Manager kısıtlamayı ihlal algılarsa, sistem durumu uyarısı yayar. Bu, özel kısıtlamalar ve hello varsayılan kısıtlamalar (gibi hello hata etki alanı ve yükseltme etki alanı kısıtlamaları) için geçerlidir.

Böyle bir durum raporu bir örneği burada verilmiştir. Bu durumda, hello sistem durumu raporu hello sistem hizmetin bölümleri için biridir. Bu bölüm kopyalarını geçici olarak çok az yükseltme etki alanlarına paketlenmiş hello Hello sistem durumu ileti gösterir.

```posh
PS C:\Users\User > Get-WindowsFabricPartitionHealth -PartitionId '00000000-0000-0000-0000-000000000001'


PartitionId           : 00000000-0000-0000-0000-000000000001
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB', Property='ReplicaConstraintViolation_UpgradeDomain', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 130766528804733380
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577821
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528854889931
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577822
                        AggregatedHealthState : Ok

                        ReplicaId             : 130837073190680024
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.PLB
                        Property              : ReplicaConstraintViolation_UpgradeDomain
                        HealthState           : Warning
                        SequenceNumber        : 130837100116930204
                        SentAt                : 8/10/2015 7:53:31 PM
                        ReceivedAt            : 8/10/2015 7:53:33 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer has detected a Constraint Violation for this Replica: fabric:/System/FailoverManagerService Secondary Partition 00000000-0000-0000-0000-000000000001 is
                        violating hello Constraint: UpgradeDomain Details: UpgradeDomain ID -- 4, Replica on NodeName -- Node.8 Currently Upgrading -- false Distribution Policy -- Packing
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Ok->Warning = 8/10/2015 7:13:02 PM, LastError = 1/1/0001 12:00:00 AM
```

İşte ne bu sistem durumu ileti bize olduğunu bildiriyor:

1. Tüm hello çoğaltmaları kendilerini sağlıklı: her AggregatedHealthState vardır: Tamam
2. Merhaba yükseltme etki alanı dağıtım kısıtlaması şu anda ihlal. Bu, belirli bir yükseltme etki alanı bu bölümü gerekenden daha fazla çoğaltmalardan olduğu anlamına gelir.
3. Hangi düğümün hello çoğaltma neden hello ihlali içerir. Bu durumda hello adı "Node.8" Merhaba düğümle olur
4. Bu bölüm için ("şu anda yükseltme--false") olup olmadığını yükseltme şu anda gerçekleştiriliyor
5. Bu hizmet için dağıtım ilkesi Hello: "Dağıtım ilkesi--paketleme". Bu hello tarafından yönetilir `RequireDomainDistribution` [yerleştirme İlkesi](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). "Sevk" gösterir, bu durumda DomainDistribution olduğunu _değil_ yerleştirme İlkesi bu hizmet için belirtilmedi biliyoruz şekilde, gerekli. 
6. Ne zaman hello rapor oldu - 8/10/2015 19:13:02: 00

Bilgiler bir şeyler yanlış geçti ve ayrıca bildiğiniz üretim toolet yangın toodetect kullanılan bu powers uyarıları ister ve hatalı yükseltmeler durdur. Bu durumda, biz hello Resource Manager toopack hello çoğaltmaları hello yükseltme etki alanı içine neden olan çıkışı şekil, biz toosee istersiniz. Merhaba Hello düğümler diğer yükseltme etki alanları aşağı, örneğin olduğundan genellikle sevk geçicidir.

Diyelim ki hello küme Resource Manager tooplace bazı hizmetler çalışıyor, ancak iş çözümleri yok. Hizmetleri yerleştirilemez genellikle hello aşağıdaki nedenlerden birinden dolayı olur:

1. Bazı geçici koşul imkansız tooplace yaptı bu hizmet örneği veya çoğaltma doğru
2. Merhaba hizmetin yerleştirme unsatisfiable gereksinimleridir.

Bu durumlarda, hello küme Resource Manager sistem durumu raporlarını hello hizmeti neden yerleştirilemez belirlemenize yardımcı. Bu işlem hello kısıtlaması eleme sırası diyoruz. Bunu sırasında hello sistem ne ortadan hello hizmeti ve kayıtları etkileyen yapılandırılmış hello kısıtlamaları anlatılmaktadır. Hizmetleri konumdaki mümkün toobe değil, bu şekilde, hangi düğümlerin ortadan görebilirsiniz ve neden.

## <a name="constraint-types"></a>Kısıtlama türleri
Her bir hello farklı kısıtlamalar bu sistem durumu raporları hakkında şimdi konuşun. Çoğaltmaları yerleştirildiğinde, sistem durumu iletileri ilgili toothese kısıtlamaları görürsünüz.

* **ReplicaExclusionStatic** ve **ReplicaExclusionDynamic**: Bu kısıtlamaların gösteren bir çözüm toobe yerleştirilen hello üzerinde aynı aynı bölüm iki hizmet nesnelerden hello nedeniyle reddedildi düğümü. Daha sonra bu düğümü aşırı o bölümün etkileyebilecek bu için izin verilmiyor. ReplicaExclusionStatic ve ReplicaExclusionDynamic neredeyse aynı kural ve hello farklar gerçekten önemi yoktur hello markalarıdır. Yeterli düğüm değil ya da hello ReplicaExclusionStatic veya ReplicaExclusionDynamic kısıtlaması, hello Küme Kaynak Yöneticisi'ni içeren bir kısıtlama eleme sırası düşündüğü görüyorsanız. Bu çözümleri toouse izin verilmiyor bu geçersiz yerleşimi kalan gerektirir. Hello hello dizisindeki diğer kısıtlamaları genellikle neden düğümleri hello ilk yerinde ortadan bize.
* **PlacementConstraint**: Bu iletiyi görürseniz, bu hello hizmetin kısıtlamalarından eşleşmedi çünkü biz bazı düğümler ortadan anlamına gelir. Biz bu iletiyi bir parçası olarak yapılandırılmış hello kısıtlamalarından izleme. Tanımlanan bir yerleştirme kısıtlaması varsa, bu normaldir. Ancak, yerleştirme kısıtlaması ortadan çok fazla düğüm toobe yanlış neden olup olmadığını nasıl fark etmesi budur.
* **NodeCapacity**: Bu kısıtlamayı küme Resource Manager uygulanamadı yerleştireceğinize hello çoğaltmaları bu hello anlamına gelir, bunları kapasite aşımı taşmasına neden olabileceğinden hello belirtilen düğümleri.
* **Benzeşim**: hello benzeşim kısıtlaması ihlali neden olacağından bu yana biz hello çoğaltma etkilenen hello düğümlerinde yerleştirmenizi uygulanamadı bu kısıtlamayı belirtir. Benzeşimi hakkında daha fazla bilgi yer [bu makalede](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
* **FaultDomain** ve **UpgradeDomain**: hello yerleştirme hello kopyada düğümleri neden bir belirli hatası veya yükseltme etki alanında sevk belirtilmişse bu kısıtlamayı düğümleri ortadan kaldırır. Merhaba konudaki sunulur bu kısıtlamayı ele çeşitli örnekler [hata ve yükseltme etki alanı kısıtlamaları ve bunun sonucunda oluşan davranışı](service-fabric-cluster-resource-manager-cluster-description.md)
* **PreferredLocation**: varsayılan olarak bir iyileştirme çalışır olduğundan düğüm hello çözümden kaldırmak bu kısıtlamayı normalde görmemesi. Merhaba tercih edilen konum kısıtlaması yükseltmeler sırasında mevcuttur. Yükseltme sırasında kullanılan toomove Hizmetleri arka toowhere hello yükseltme başlatıldığında oldukları değil.

## <a name="blocklisting-nodes"></a>Blocklisting düğümler
Başka bir sistem durumu ileti hello küme Resource Manager raporlar düğümleri blocklisted olduğunda değildir. Blocklisting sizin için otomatik olarak uygulanan geçici bir kısıtlama olarak düşünebilirsiniz. Yinelenen hatalarının bu hizmet türünün örneklerini başlatılırken karşılaşırsanız, düğümleri blocklisted alın. Düğüm başına-service-type olarak blocklisted ' dir. Bir düğüm için bir hizmet türünün blocklisted olabilir, ancak başka bir değil. 

Genellikle geliştirme sırasında ilkenin etkisini gösterip blocklisting görürsünüz: bazı hata başlangıçta hizmeti konak toocrash neden olur. Service Fabric toocreate hello hizmet konağı birkaç kez çalışır ve hello hatası gerçekleşen tutar. Birkaç denemeden sonra blocklisted hello düğümünü alır ve hello küme Resource Manager toocreate hello başka bir yerde hizmet çalışacaktır. Birden çok düğümde bu hata gerçekleştiği tutar, tüm geçerli düğüm hello küme sonlandırmayı hello engellenen mümkündür. Blocklisting ayrıca çok fazla sayıda düğüm yeterli başarıyla hello hizmet toomeet istenen hello ölçek başlatabilirsiniz kaldırabilirsiniz. Ek hatalar genellikle göreceğiniz ya da hello hizmet hello istenen çoğaltma veya örnek sayısı yanı sıra hangi hello hatası gösteren durum iletilerinin olduğunu küme Resource Manager hello belirten uyarıların toohello baştaki Merhaba ilk yerinde blocklisting.

Blocklisting kalıcı bir durum değil. Birkaç dakika sonra hello düğümü hello engelleme kaldırılır ve Service Fabric hello Hizmetleri bu düğümde yeniden etkinleştirebilirsiniz. Hizmetleri toofail devam ederseniz, hello blocklisted hizmet türü için yeniden düğümdür. 

### <a name="constraint-priorities"></a>Kısıtlama öncelikler

> [!WARNING]
> Kısıtlama önceliklerini değiştirmek önerilmez ve kümenizi önemli olumsuz etkileri olabilir. Aşağıdaki bilgileri Hello hello varsayılan kısıtlama önceliklerini ve davranışlarını başvurusunu sağlanır. 
>

Tüm bu kısıtlamaların, "Merhaba – ı hata etki alanı kısıtlamaları my sisteminde hello en önemli şey olduğunu düşünün. düşünüyorum Sipariş tooensure hello hata etki alanı kısıtlaması ihlal edildi değil, ben tooviolate diğer kısıtlamaları istekli. "

Kısıtlamaları farklı öncelik düzeyleri ile yapılandırılabilir. Bunlar:

   - "sabit" (0)
   - "yumuşak" (1)
   - "en iyi duruma getirme" (2)
   - (-1 "kapalı"). 
   
Merhaba kısıtlamaların büyük bir bölümü sabit kısıtlamaları varsayılan olarak yapılandırılır.

Kısıtlamaları Hello önceliğini değiştirmek seyrek olur. Burada kısıtlaması öncelikleri gerekli toochange, genellikle başka bir hata veya hello ortamı etkileyen davranış geçici toowork kez olmuştur. Genellikle hello esneklik hello kısıtlaması öncelik altyapısının çok iyi çalışmıştır ancak genellikle gerekli değildir. Başlangıç zamanının çoğunu her şeyi varsayılan öncelikleri bulunur. 

Merhaba öncelik düzeyleri yok anlamına gelir, belirli bir kısıtlama _olacak_ ihlal, ya da her zaman karşılanması. Kısıtlama öncelikleri kısıtlamaları zorunlu tutulmaz sipariş tanımlayın. İmkansız toosatisfy olduğunda öncelikleri hello bileşim tüm kısıtlamalarını tanımlayın. Genellikle olmadıkça hello ortamında geçmeden başka bir şey tüm hello kısıtlamalarını karşılanabilir. Çakışan kısıtlamaları tooconstraint ihlalleri götürür senaryoları bazı örnekleri şunlardır ya da çok sayıda eş zamanlı hataları.

Gelişmiş durumlarda hello kısıtlaması önceliklerini değiştirebilirsiniz. Örneğin, tooensure istediğinizi varsayalım gerekli toosolve düğüm kapasitesi gönderdiğinde, benzeşimi'nin her zaman ihlal. tooachieve bunu hello benzeşim kısıtlaması çok "yumuşak" (1) hello önceliğini ayarlamak ve "sabit" çok ayarlanan hello kapasite kısıtlamasına (0) bırakın.

Merhaba farklı kısıtlamaları Hello varsayılan öncelik değerleri yapılandırma aşağıdaki hello belirtilir:

ClusterManifest.xml

```xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PlacementConstraintPriority" Value="0" />
            <Parameter Name="CapacityConstraintPriority" Value="0" />
            <Parameter Name="AffinityConstraintPriority" Value="0" />
            <Parameter Name="FaultDomainConstraintPriority" Value="0" />
            <Parameter Name="UpgradeDomainConstraintPriority" Value="1" />
            <Parameter Name="PreferredLocationConstraintPriority" Value="2" />
        </Section>
```

tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PlacementConstraintPriority",
          "value": "0"
      },
      {
          "name": "CapacityConstraintPriority",
          "value": "0"
      },
      {
          "name": "AffinityConstraintPriority",
          "value": "0"
      },
      {
          "name": "FaultDomainConstraintPriority",
          "value": "0"
      },
      {
          "name": "UpgradeDomainConstraintPriority",
          "value": "1"
      },
      {
          "name": "PreferredLocationConstraintPriority",
          "value": "2"
      }
    ]
  }
]
```

## <a name="fault-domain-and-upgrade-domain-constraints"></a>Hata etki alanı ve yükseltme etki alanı kısıtlamaları
Merhaba Küme Kaynak Yöneticisi hata ve yükseltme etki alanları arasında dağılmış tookeep Hizmetleri istemektedir. Bu hello küme kaynak yöneticisinin altyapısı içinde bir kısıtlama olarak modeller. Bunların nasıl kullanıldığı hakkında daha fazla bilgi ve belirli davranışlarını için hello makalesine kontrol [küme yapılandırması](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior).

Merhaba küme Resource Manager toopack, yükseltmeler, hataları veya başka bir kısıtlama ihlali sipariş toodeal içindeki bir yükseltme etki alanına birkaç çoğaltmaları yüklemeniz gerekebilir. Yalnızca birkaç hataları veya diğer karmaşası doğru yerleştirme önleme hello sistemde hatası veya yükseltme etki alanlarına normalde sevk olur. Bu durumlarda bile sırasında sevk tooprevent istiyorsanız hello kullanabilir `RequireDomainDistribution` [yerleştirme İlkesi](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). Bu hizmet kullanılabilirliği ve güvenilirliği bir yan etkisi olarak etkiler, bu nedenle dikkatlice düşünün dikkat edin.

Merhaba ortamı doğru şekilde yapılandırıldıysa, tüm kısıtlamalarını tam olarak, bile yükseltmeler sırasında kullanılır. Merhaba anahtar kısıtlamaları için küme Resource Manager izliyor bu hello şeydir. Bir ihlali algıladığında hemen rapor ve toocorrect hello sorunu çalışır.

## <a name="hello-preferred-location-constraint"></a>tercih edilen hello konum kısıtlaması
iki farklı kullanımlar olduğu gibi hello PreferredLocation kısıtlaması biraz farklıdır. Bir kısıtlamanın uygulama yükseltmeler sırasında kullanılır. Merhaba Küme Kaynak Yöneticisi, bu kısıtlamayı yükseltmeler sırasında otomatik olarak yönetir. Kullanılan tooensure olan olduğunda yükseltmeleri çoğaltmaları ilk konumları tootheir dönüş tamamlandı. Merhaba diğer hello PreferredLocation kısıtlaması Merhaba kullanımıdır [ `PreferredPrimaryDomain` yerleştirme İlkesi](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md). Bunların her ikisi de en iyi duruma getirme ve bu nedenle çok ayarlanan hello yalnızca kısıtlamasına hello PreferredLocation kısıtlaması olduğundan varsayılan olarak "iyileştirme".

## <a name="upgrades"></a>Yükseltme
Merhaba Küme Kaynak Yöneticisi ayrıca uygulama ve hangi sırasında iki iş bulunmuyor Küme yükseltme sırasında yardımcı olur:

* Merhaba kuralları hello kümesinin tehlikeye emin olun
* toohelp hello yükseltme Git sorunsuz deneyin

### <a name="keep-enforcing-hello-rules"></a>Merhaba kuralları zorunlu tutun
Merhaba ana şeyi toobe farkında hello kuralları – kısıtlamalarından ve kapasiteleri gibi hello katı kısıtlamaları - yükseltmeler sırasında zorunlu tutulmaz ' dir. Kısıtlamalarından iş yüklerinizi yalnızca burada bunlar, hatta yükseltmeler sırasında izin verilen çalıştırdığınızdan emin olun. Hizmetler yüksek oranda kısıtlı kullanılırken yükseltmeler uzun sürebilir. Merhaba hizmet ya da hello düğüm üzerinde çalıştırıldığı olduğunda bu gidebilecekleri için birkaç seçenek olabilir bir güncelleştirme için duruma.

### <a name="smart-replacements"></a>Akıllı değişiklik
Yükseltme başladığında hello Resource Manager hello geçerli hello küme düzenlenmesi, bir anlık görüntüsünü alır. Her yükseltme etki alanı tamamlandığında, yükseltme etki alanı tootheir özgün düzeninde tooreturn hello hizmetler çalışır. Bu şekilde var. en çok bir hizmet için iki geçişleri hello yükseltme sırasında Etkilenen hello düğümünün çıkışı bir taşıma yoktur ve bir geri içeri taşı. Merhaba yükseltme, aynı zamanda hello yükseltme sağlar önceki hello küme veya hizmet toohow döndürme hello küme hello düzenini etkilemez. 

### <a name="reduced-churn"></a>Azaltılmış karmaşası
Yükseltme sırasında gerçekleşen başka bir küme kaynağı Yöneticisi Dengeleme devre dışı bırakır, hello şeydir. Dengeleme önleme Hizmetleri hello yükseltme için Boşaltılan düğümleri taşınmasını gibi gereksiz tepki toohello yükseltme kendisini engeller. Küme yükseltme Hello yükseltme söz konusu ise, hello tüm küme hello yükseltme sırasında dengelenir değil. Kısıtlama denetimleri etkin kalır, yalnızca taşıma hello öngörülü ölçümlerini Dengeleme üzerinde temel devre dışı bırakıldı.

### <a name="buffered-capacity--upgrade"></a>Arabelleğe alınan kapasite & yükseltme
Genellikle Hello küme kısıtlanmış veya kapatma toofull olsa bile hello yükseltme toocomplete istersiniz. Merhaba küme Hello kapasitesini yönetme yükseltmeler sırasında normalden daha da önemlidir. Merhaba yükseltme yapar aracılığıyla hello kümesi gibi hello bağlı olarak kapasite yüzde 20'si ile 5 arasındaki yükseltme etki alanlarının sayısı geçirilmesi gerekir. Bu iş toogo yere sahiptir. Bu olduğu yere hello kavramı [kapasiteleri arabelleğe](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity) yararlıdır. Arabelleğe alınan kapasite normal işlem sırasında dikkate. Merhaba Küme Kaynak Yöneticisi'ni (Merhaba arabellek tüketen) tootheir toplam kapasite düğümlerini gerekiyorsa, yükseltme sırasında yerine getirebilir.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba baştan başlatın ve [giriş toohello Service Fabric kümesi Kaynak Yöneticisi Al](service-fabric-cluster-resource-manager-introduction.md)
