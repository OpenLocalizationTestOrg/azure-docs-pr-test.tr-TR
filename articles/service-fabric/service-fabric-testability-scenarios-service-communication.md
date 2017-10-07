---
title: "Test Edilebilirlik: Hizmet iletişimi | Microsoft Docs"
description: "Hizmet hizmet iletişimi, Service Fabric uygulaması kritik tümleştirme noktasıdır. Bu makalede, tasarım konuları ve test teknikleri anlatılmaktadır."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a>Service Fabric Test Edilebilirlik senaryoları: hizmet iletişimi
Mikro hizmetler ve hizmet odaklı mimari stilleri yüzey doğal olarak Azure Service Fabric. Bu dağıtılmış mimariler türlerinde bileşenlerden oluşan mikro hizmet uygulamaları genellikle tootalk tooeach diğer gereken birden çok hizmetlerini oluşur. Hatta hello en basit durumda, genellikle en az bir durum bilgisi olmayan web hizmeti ve toocommunicate gereken bir durum bilgisi olan veri depolama hizmeti vardır.

Hizmet hizmet iletişimi kritik tümleştirme noktası bir uygulamanın çünkü her hizmetin bir Uzak API tooother hizmetleri sunar. Genellikle g/ç içeren bir dizi API sınırları çalışmak bazı dikkatli iyi miktarda sınama ve doğrulama gerektirir.

Bu hizmet sınırları birlikte dağıtılmış bir sistemde kablolu, çok sayıda konuları toomake vardır:

* *Aktarım Protokolü*. HTTP artan birlikte çalışabilirliğini ya da özel bir ikili protokol için en yüksek verimlilik kullanacaksınız?
* *Hata işleme*. Kalıcı ve geçici hataları nasıl işleneceğini? Bir hizmet tooa farklı bir düğüme taşındığında ne?
* *Zaman aşımları ve gecikme süresi*. Çok uygulamalarda her hizmet katmanı gecikme hello yığını ve toohello kullanıcı üzerinden nasıl işler mi?

Service Fabric tarafından sağlanan hello yerleşik hizmet iletişimi bileşenlerden biri kullanabilir veya kendi oluşturabilirsiniz, hizmetlerinizi arasındaki hello etkileşimler sınama kritik tooensuring dayanıklılık uygulamanızda olup.

## <a name="prepare-for-services-toomove"></a>Hizmetleri toomove için hazırlama
Hizmet örnekleri zaman içinde hareket etme. Bu, özellikle özel uyarlanmış en iyi kaynak Dengeleme için yük ölçümlerle yapılandırıldığında geçerlidir. Service Fabric hizmeti örnekleri toomaximize yükseltmeler, yük devretme, genişleme ve dağıtılmış bir sistemde hello ömrü boyunca gerçekleşen diğer durumlarda sırasında bile kullanılabilirliklerini taşır.

Merhaba kümede Hizmetleri dolaşmak gibi istemcilerinizi ve diğer hizmetleri tooa hizmet konuşurken hazırlıklı toohandle iki senaryo olmalıdır:

* Merhaba hizmet örneği veya bölüm çoğaltma tooit açıklandı son zamanı hello itibaren taşınmıştır. Bu hizmet yaşam döngüsü normal bir parçası olan ve uygulamanızı hello ömrü boyunca beklenen toohappen olmalıdır.
* Merhaba hizmet örneği veya bölüm çoğaltma taşıma hello işlemi devam ediyor. Bir düğüm tooanother hizmetinden Yük Devretmesini Service Fabric çok hızlı bir şekilde oluşur ancak bir gecikme olabilir kullanılabilirlik hello iletişim bileşeni hizmetinizin yavaş toostart ise.

Bu senaryolar düzgün biçimde işleme düzgün çalışmasını sistemi için önemlidir. toodo, bu nedenle, göz önünde bulundurun:

* Bağlı toohas olabilir her hizmetin bir *adresi* , (örneğin, HTTP veya WebSockets) dinler. Bir hizmet örneği veya bölüm taşındığında, adresi uç noktasında değiştirir. (Bu, farklı bir düğüme tooa farklı bir IP adresi ile taşınır.) Merhaba yerleşik iletişim bileşenleri kullanıyorsanız, bunlar yeniden çözümleme hizmeti adresleri sizin için işler.
* Olabilir hizmet gecikme hello hizmet örneği başlatır, dinleyicisi yukarı olarak geçici bir artış yeniden. Bu hello hizmet örneği taşındıktan sonra ne kadar hızlı hello hizmet hello dinleyicisi üzerinde bağlıdır.
* Var olan tüm bağlantıları yeni bir düğümde hello hizmet açıldıktan sonra kapatıp toobe gerekir. Normal düğümün kapanması veya yeniden başlatma düzgün biçimde kapatılamadı varolan bağlantılar toobe için zaman sağlar.

### <a name="test-it-move-service-instances"></a>Test: taşıma hizmet örnekleri
Service Fabric'ın Test Edilebilirlik araçlarını kullanarak, farklı şekillerde bu gibi durumlarda bir test senaryosu tootest yazabilirsiniz:

1. Bir durum bilgisi olan hizmetin birincil çoğaltma taşıyın.
   
    Merhaba bir durum bilgisi olan hizmet bölüm birincil çoğaltmasını birkaç nedenden dolayı için taşınabilir. Bu tootarget hello birincil çoğaltmasını nasıl tepki, hizmetleri toohello hareket çok denetimli bir şekilde belirli bir bölüm toosee kullanın.
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. Bir düğüm durdurun.
   
    Bir düğüm durdurulduğunda, tüm hello hizmet örneği veya bu düğüm tooone üzerinde olan bölümleri Service Fabric taşır hello kümedeki kullanılabilir diğer düğümlere hello. Bu tootest Burada, kümeden bir düğümü kaybolur ve tüm hello hizmet örneği ve çoğaltmaları bu düğümde toomove sahip bir durum kullanın.
   
    Merhaba PowerShell kullanarak bir düğümü durdurabilirsiniz **Stop-ServiceFabricNode** cmdlet:
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a>Hizmet kullanılabilirliği sürdürmek
Bir platform tasarlanmış tooprovide yüksek hizmetlerinizin kullanılabilirliğini Service Fabric eklentisidir. Ancak olağanüstü durumlarda, temel alınan altyapı hala kullanılamazlık sorunlara yol açabilir. Bu senaryolarda önemli tootest çok uzun.

Durum bilgisi olan hizmetler yüksek kullanılabilirlik için bir çekirdek tabanlı sistem tooreplicate durumu kullanın. Bu, bir çekirdek çoğaltmalarının toobe kullanılabilir tooperform yazma işlemleri gerektiği anlamına gelir. Nadir durumlarda, yaygın donanım arızası gibi bir çekirdek çoğaltmalarının kullanılamayabilir. Bu gibi durumlarda mümkün tooperform yazma işlemleri olmaz ancak mümkün tooperform okuma işlemleri olmaya devam edecektir.

### <a name="test-it-write-operation-unavailability"></a>Test: yazma işlemi kullanılamazlık
Service Fabric Hello Test Edilebilirlik araçlarını kullanarak, bir test olarak çekirdek kayıp gerektiriyorsa bir arıza ekleyemezsiniz. Böyle bir senaryo ender olsa da, istemciler ve durum bilgisi olan bir hizmete bağlı hizmetler toohandle durumlarda bunlar istekleri tooit yazma burada yapamazsınız hazırlanır önemlidir. Durum bilgisi olan hizmet hello kendisini bu olasılığını bilmektedir ve toocallers düzgün bir şekilde iletişim kurmak önemlidir.

Çekirdek kayıp hello PowerShell kullanarak anlamına **Invoke-ServiceFabricPartitionQuorumLoss** cmdlet:

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

Bu örnekte, ayarlarız `QuorumLossMode` çok`QuorumReplicas` tüm çoğaltmaları bırakmadan tooinduce çekirdek kayıp istiyoruz tooindicate. Bu şekilde, okuma işlemleri hala mümkündür. tootest bir senaryo burada bölümünün tamamını kullanılamıyor, bu anahtarı çok ayarlayabilirsiniz`AllReplicas`.

## <a name="next-steps"></a>Sonraki adımlar
[Test Edilebilirlik eylemler hakkında daha fazla bilgi edinin](service-fabric-testability-actions.md)

[Test Edilebilirlik senaryoları hakkında daha fazla bilgi edinin](service-fabric-testability-scenarios.md)

