---
title: "aaaAzure Service Fabric Platform düzeyi izleme | Microsoft Docs"
description: "Platform düzeyi olaylar hakkında bilgi edinin ve günlükleri Azure Service Fabric kümeleri tanılamak ve toomonitor kullanılır."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: f8fb1c8b546e05c517ae12c91906acc04cd6eaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="platform-level-event-and-log-generation"></a>Platform düzeyi olay ve günlük oluşturma

## <a name="monitoring-hello-cluster"></a>Merhaba küme izleme

Merhaba platform düzeyi toodetermine olsun veya olmasın, donanım ve küme beklendiği gibi davranmakta olduğunu en önemli toomonitor olur. Service Fabric bir donanım hatası sırasında çalışan uygulamalar yine de kullanmaya devam edebilir, ancak bir uygulama veya hello altyapının bir hata oluşup oluşmadığını toodiagnose hala gerekir. Kümeleri toobetter planınız için kapasite ekleme veya kaldırma donanım hakkında kararlar yardımcı ayrıca izlemeniz gerekir.

Service Fabric beş farklı günlük kanalları out-of--olayları aşağıdaki hello üreten box sağlar:

* İşletimsel kanal: Service Fabric ve gelen dağıtılmakta olan yeni bir uygulama, bir düğüm için olaylar dahil olmak üzere hello küme tarafından gerçekleştirilen üst düzey işlemler veya geri alma, vb. yükseltme BT.
* İşletimsel kanal - ayrıntılı: sistem durumu raporları ve Yük Dengeleme kararları
* Veri & Mesajlaşma kanalı: kritik günlükleri ve bizim (şu anda yalnızca hello ReverseProxy) Mesajlaşma ve veri yolu (güvenilir hizmetler modeller) oluşturulan olayları
* Ayrıntılı veri & Mesajlaşma kanalı -: tüm hello kritik olmayan günlüklerinden veri ve (Bu kanal sahip çok yüksek hacimli olayları) hello kümede Mesajlaşma içeren kapsamlı kanal   
* [Güvenilir hizmetler olayları](service-fabric-reliable-services-diagnostics.md): programlama modeli belirli olayları
* [Güvenilir aktörler olayları](service-fabric-reliable-actors-diagnostics.md): programlama modeli belirli olayları ve performans sayaçları
* Günlükleri destekler: Service Fabric yalnızca toobe tarafımızca destek sağlarken kullanılan tarafından oluşturulan sistem günlükleri

Bu çeşitli kanalları önerilen hello platform düzeyinde günlüğe kaydetme çoğunu kapsar. Günlük, tooimprove platform düzeyi göz önünde bulundurun daha iyi anlamak hello sistem durumu modeli ve özel durum raporları ekleme ve ekleme yatırım özel **performans sayaçları** hello gerçek zamanlı bir anlayış etkisi, toobuild Hizmet ve uygulamalarınızı hello kümede.

### <a name="azure-service-fabric-health-and-load-reporting"></a>Azure Service Fabric sistem durumu ve yük raporlama

Service Fabric ayrıntılı bu makalelerde açıklanan kendi sistem durumu modeli vardır:
- [Giriş tooService doku sistem durumu izleme](service-fabric-health-introduction.md)
- [Hizmet durumunu raporlama ve denetleme](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
- [Özel Service Fabric sistem durumu rapor ekleme](service-fabric-report-health.md)
- [Service Fabric sistem durumu raporlarını görüntüle](service-fabric-view-entities-aggregated-health.md)

Sistem durumu izleme, kritik toomultiple yönlerini hizmet işletim olur. Service Fabric adlandırılmış uygulama yükseltme yaparken, sistem durumu izleme özellikle önemlidir. Her bir yükseltme etki alanı hello hizmetinin yükseltilir ve kullanılabilir tooyour müşteriler sonra hello dağıtım toohello sonraki yükseltme etki alanına gitmeden önce hello yükseltme etki alanı sistem durumu denetimleri geçmesi gerekir. İyi sistem durumu elde, Merhaba uygulaması bilinen, iyi bir durumda olmasını sağlamak hello dağıtım geri alınır. Merhaba hizmetler geri önce bazı müşteriler etkilenebilir rağmen müşterilerin çoğu bir sorunla karşılaşırsınız olmaz. Ayrıca, bir çözüm oldukça hızlı bir şekilde ve İnsan olan bir operatörü eylemden toowait kalmadan oluşur. kodunuza hello hizmetinizi toodeployment sorunları olduğundan daha esnektir dahil daha fazla sistem durumu denetimlerinin hello.

Hizmet durumu bir diğer unsuru hello hizmetinden ölçümleri bildiriyor. Çünkü bunlar kullanılan toobalance kaynak kullanımı ölçümlerini Service Fabric önemlidir. Ölçümleri de sistem durumu bir göstergesi olabilir. Örneğin, birçok Hizmetleri olan bir uygulama olabilir ve ikinci (RPS) ölçüm başına bir isteği her örnek raporlar. Bir hizmet başka bir hizmete daha fazla kaynak kullanıyorsa, Service Fabric hello küme geçici hizmet örneklerini taşır. tootry toomaintain bile kaynak kullanımı. Kaynak kullanımını nasıl çalıştığını daha ayrıntılı açıklaması için bkz: [kaynak tüketimini yönetmek ve ölçümler ile Service Fabric yük](service-fabric-cluster-resource-manager-metrics.md).

Ölçümleri hizmetinizin nasıl gerçekleştirmekte içine kavrayışı de yardımcı olabilir. Zaman içinde hello hizmet işletim içinde beklenen parametreleri ölçümleri toocheck kullanabilirsiniz. Örneğin, eğilimleri, 9'da Pazartesi sabahı hello üzerinde ortalama gösterirse RPS 1.000 olduğu sonra hello RPS 500 aşağıda veya üzerinde 1.500 ise, sizi uyarır bir sistem durumu raporu ayarlayabilir. Her şey mükemmel ince olabilir, ancak bir görünüm toobe müşterilerinizin harika bir deneyim yaşıyor emin olabilir. Hizmet sistem durumu denetimi amacıyla bildirilebilir ancak hello hello kümesinin kaynak Dengeleme etkilemeyen ölçümleri kümesi tanımlayabilirsiniz. toodo Bu, kümesi hello ölçüm ağırlığı toozero. Tüm ölçümleri sıfır ağırlığını ile başlatın ve kaynak kümeniz için Dengeleme hello ölçüm ağırlığı nasıl etkilediğini anladığınızdan emin olana kadar hello ağırlık artırmak değil öneririz.

> [!TIP]
> Çok fazla ağırlıklı ölçümleri kullanmayın. Zor toounderstand neden hizmet örnekleri Dengeleme için taşınan olabilir. Birkaç ölçümleri depoladıysanız gidebilirsiniz!

Merhaba sağlık ve uygulamanızın performansını belirtebilir herhangi bir bilgi ölçümleri ve sistem durumu raporları için bir adaydır. CPU performans sayacı düğümünüz nasıl kullandığı anlayabilirsiniz, ancak bu, tek bir düğümünde birden fazla hizmet çalışmıyor olabilir çünkü belirli bir hizmet sistem durumunun iyi olup söyler. Ancak, RPS, işlenen, öğeler ölçümleri ister ve tüm istek gecikme süresi belirli bir hizmet hello durumunu gösterebilir.

tooreport sistem durumu, kullanım kodunu benzer toothis:

  ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
  ```

tooreport bir ölçüm kodu benzer toothis kullanın:

  ```csharp
    this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("MemoryInMb", 1234), new LoadMetric("metric1", 42) });
  ```

### <a name="service-fabric-support-logs"></a>Service Fabric destek günlükleri

Destek günlükleri, toocontact Microsoft Destek ile Azure Service Fabric kümenizi için yardıma gereksinim duyarsanız, neredeyse her zaman gereklidir. Kümenizi Azure üzerinde barındırılıyorsa, destek günlükleri otomatik olarak yapılandırılır ve küme oluşturma bir parçası olarak toplanır. Merhaba günlükleri, küme kaynak grubu ayrılmış bir depolama hesabında depolanır. Merhaba depolama hesabı, sabit bir adı yoksa, ancak hello hesabında blob kapsayıcıları ve tabloları ile başlayan adlarla gördüğünüz *doku*. Tek başına küme için günlük koleksiyonları ayarlama hakkında daha fazla bilgi için bkz: [Oluştur bir tek başına Azure Service Fabric kümesi ve yönetebileceğiniz](service-fabric-cluster-creation-for-windows-server.md) ve [tek başına Windows için yapılandırma ayarları küme](service-fabric-cluster-manifest.md). Tek başına Service Fabric örnekleri için hello günlükleri tooa yerel dosya paylaşımı gönderilmelidir. Olduğunuz **gerekli** toohave bu oturum için destek, ancak bunlar olmayan hedeflenen toobe kullanılabilir hello Microsoft müşteri destek ekibi dışında herhangi bir kişi tarafından.

## <a name="enabling-diagnostics-for-a-cluster"></a>Bir küme için tanılama etkinleştirme

Sipariş tootake avantajlarından Bu günlükleri, küme oluşturma sırasında "tanılama" etkinleştirildiğini kullanmamanız önerilir. Tanılama üzerinde kapatarak hello küme dağıtıldığında, Windows Azure Tanılama, mümkün tooacknowledge hello işlemsel, Reliable Services ve Reliable actors kanalları ve deposu hello veri anlatıldığı gibi daha fazla [toplama olayları Azure tanılama](service-fabric-diagnostics-event-aggregation-wad.md).

Yukarıda görülen da ayrıca isteğe bağlı alan tooadd bir uygulama Öngörüler (AI) izleme anahtarı yok. Tüm olay çözümleme için toouse AI seçerseniz (Bu konuda daha fazla [olay çözümleme Application Insights ile](service-fabric-diagnostics-event-analysis-appinsights.md)), hello Appınsights'dan kaynak instrumentationKey (GUID) buraya dahil.


Toodeploy kapsayıcıları tooyour küme kullanacaksanız, bu tooyour "WadCfg > DiagnosticMonitorConfiguration" ekleyerek WAD toopick docker istatistikleri yukarı etkinleştirin:

```json
"DockerSources": {
    "Stats": {
        "enabled": true,
        "sampleRate": "PT1M"
    }
},

```

## <a name="measuring-performance"></a>Performansı ölçme

Kümenizi ölçü performansını nasıl kümenizi ölçeklendirme geçici mümkün toohandle yükleme ve sürücü kararları olduğunu anlamanıza yardımcı olur (küme ölçeklendirme hakkında daha fazla [azure'da](service-fabric-cluster-scale-up-down.md), veya [şirket içi](service-fabric-cluster-windows-server-add-remove-nodes.md)). Performans verileri aynı zamanda, veya uygulamalarınızın yararlıdır tooactions karşılaştırıldığında ve Hizmetleri, hello günlüklerini analiz ederken gelecekteki almış olabilir. 

Service Fabric kullanırken performans sayaçları toocollect listesi için bkz: [Service Fabric performans sayaçları](service-fabric-diagnostics-event-generation-perf.md)

Kümeniz için performans verilerini toplama yukarı ayarlayabilirsiniz iki genel yolu şunlardır:

* Bir aracı kullanarak: Bu bir makineden performans toplama hello tercih edilen yöntemdir, aracıları genellikle toplanabilir olası performans ölçüm listesine sahip ve görece olarak daha kolay işlem toochoose hello ölçümleri olduğundan toocollect istediğiniz veya bunları değiştirme . Hakkında bilgi edinin [nasıl tooconfigure hello OMS için Service Fabric](service-fabric-diagnostics-event-analysis-oms.md) ve [OMS Windows Aracısı hello ayarı](../log-analytics/log-analytics-windows-agents.md) makaleleri toolearn yukarı mümkün toopick olan bir tür İzleme Aracısı hello OMS Aracısı hakkında daha fazla bilgi küme sanal makineleri ve dağıtılan kapsayıcıları için performans verilerini.

* Tanılama toowrite performans sayaçları tooa tablosu: Azure ile ilgili daha fazla kümeler için bu hello VM'ler kümenizdeki gelen hello Azure tanılama yapılandırması toopick hello uygun performans sayaçları yukarı değiştirme ve yukarı toopick etkinleştirme anlamına gelir herhangi bir kapsayıcıdaki dağıtacaksanız docker istatistikleri. Yapılandırma hakkında okuyun [WAD performans sayaçları](service-fabric-diagnostics-event-aggregation-wad.md) Service Fabric tooset performans sayacı toplama yukarı içinde.

## <a name="next-steps"></a>Sonraki adımlar

Günlüklerini ve olayları tooany analiz platformu gönderilmeden önce bir araya getirilir toobe gerekir. Hakkında bilgi edinin [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) ve [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter bazı seçenekleri önerilen hello anlama.
