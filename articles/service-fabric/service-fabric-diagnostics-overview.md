---
title: "aaaAzure Yapı Hizmeti izleme ve tanılama genel bakış | Microsoft Docs"
description: "İzleme ve tanılama Azure Service Fabric kümeleri, uygulamalar ve hizmetler hakkında bilgi edinin."
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
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 1ef6419863b056b76d81e915ab78df4facae88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>İzleme ve tanılama Azure Service Fabric için

İzleme ve Tanılama Sınama ve uygulamaları ve Hizmetleri herhangi bir ortamın içinde dağıtma kritik toodeveloping var. Service Fabric çözümleri, planlama ve izleme uygulama Yardım tanılama uygulamaları emin olmak ve Hizmetleri yerel geliştirme ortamında veya üretim beklendiği gibi çalıştığını en iyi çalışır.

İzleme ana hedefleri hello ve tanılama üzeresiniz:
* Donanım ve altyapı sorunlarını tanılamak ve Algıla
* Hizmeti kapalı kalma süresini kısaltabilir, yazılım ve uygulama sorunlarını Algıla
* Kaynak tüketimi ve Yardım sürücü işlemleri kararları anlama
* Uygulama, hizmet ve altyapı performansı en iyi duruma getirme
* İşletme öngörüleri oluşturmak ve geliştirme alanlarını tanımlayacak


İzleme genel iş akışı hello ve tanılama üç adımdan oluşur:

1. **Olay oluşturma**: Bu hello altyapısı (küme), platform ve uygulama / hizmet düzeyinde (günlüklerini, izlemeleri, özel olaylar) olaylarını içerir
2. **Olay toplama**: oluşturulan olay toplanır ve bunlar görüntülenebilmesi toplanan toobe gerekir
3. **Analiz**: olayları gereksinim toobe görselleştirilmiş ve bazı biçimi, tooallow erişilebilir çözümleme ve gerektiği gibi görünen için

Birden çok ürün kullanılabilir, bu üç alanlarını kapsar ve her biri için farklı teknolojilerin ücretsiz toochoose demektir. Önemli toomake çeşitli parçaları iş birlikte toodeliver kümeniz için uçtan uca bir izleme çözümü hello emin olur.

## <a name="event-generation"></a>Olay oluşturma

Merhaba ilk hello izleme ve tanılama iş akışı hello oluşturma ve olayları ve günlükleri nesil adımdır. Bu olaylar, günlüklerine ve izlemelere iki düzeyde oluşturulur: Merhaba platform katman (Merhaba küme, hello makineler veya Service Fabric Eylemler dahil) veya uygulama katmanı hello (tüm araçları tooapps ve Hizmetleri dağıtıldı toohello küme eklenir). Service Fabric bazı araçları varsayılan olarak sağlar ancak bu düzeylerin her birinde özelleştirilebilir olaylardır.

Daha fazla bilgi edinin [platform düzeyi olayları](service-fabric-diagnostics-event-generation-infra.md) ve [uygulama düzeyinde olayları](service-fabric-diagnostics-event-generation-app.md) toounderstand ne sağlanır ve nasıl tooadd daha ayrıntılı olarak izleme.

Karar toouse istediğinizi sağlayıcı günlüğü hello üzerinde yaptıktan sonra toomake emin günlüklerinizi olması gerekir toplanır ve doğru bir şekilde depolanır.

## <a name="event-aggregation"></a>Olay toplama

Merhaba günlüklerini ve uygulamalarınızı ve kümeniz tarafından oluşturulan olayları toplamak için genellikle kullanmanızı öneririz [Azure tanılama](service-fabric-diagnostics-event-aggregation-wad.md) (daha benzer tooagent tabanlı günlük toplama) veya [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)(işlemdeki günlük toplama).

Azure tanılama uzantısını kullanarak uygulama günlükleri toplamayı hello günlük kaynakları ayarlarsanız Service Fabric Hizmetleri için iyi bir seçenektir ve hedeflere genellikle değiştirmez ve hello kaynakları ve hedeflerine arasında basit bir eşleme yoktur. Azure tanılama bu yapılandırma için yapmayı önemli değişiklikler toohello yapılandırma hello küme güncelleştirme/yükleyecek şekilde hello neden hello Resource Manager katmanında olur. Ayrıca, en iyi günlüklerinizi emin yaparken kullanıldığı depolanıyor burada bunlar çeşitli analiz platformlar tarafından erişilebilen öğesinden biraz daha kalıcı bir yere. Bu, EventFlow gibi bir seçenekle erişmekten daha ardışık düzen daha az verimli olması sona ereceğini anlamına gelir.

Kullanarak [EventFlow](https://github.com/Azure/diagnostics-eventflow) toohave Hizmetleri gönderdiğiniz günlükleri doğrudan tooan analiz sağlar ve görselleştirme platform ve/veya toostorage. Diğer kitaplıkları (ILogger, Serilog, vb.) için kullanılabilir Merhaba aynı amacı ancak EventFlow özellikle işlem içi oturum koleksiyonu ve toosupport Service Fabric Hizmetleri için tasarlanmış hello avantajına sahiptir. Bu, birkaç olası faydalarını toohave eğilimi gösterir:

* Kolay yapılandırma ve dağıtma
    * tanılama veri toplama Hello yapılandırmasının değil yalnızca hello hizmet yapılandırmasını parçası. "Hello ile eşitleme", rest hello uygulamasının kolay tooalways Canlı olduğu
    * Her uygulama veya hizmet başına yapılandırma kolayca elde edilebilir
    * EventFlow aracılığıyla veri hedeflerini yapılandırma hakkında olduğu hello uygun NuGet paketi ekleme ve değiştirme hello yalnızca sağlasa da *eventFlowConfig.json* dosyası
* Esneklik
    * toogo, gereken her yerde hedeflenen hello veri depolama sistemi destekleyen bir istemci kitaplığı var olduğu sürece Merhaba uygulaması hello veriler gönderebilir. Yeni hedefler eklenebilir istenen şekilde
    * Karmaşık yakalama, filtreleme ve veri toplama kuralları uygulanabilir
* Erişim toointernal uygulama verilerini ve içeriği
    * Merhaba uygulama/hizmet işlemi içinde çalışan hello tanılama alt sistemi kolayca hello izlemeleri bağlamsal bilgilerle genişletebilirsiniz

Bir şey toonote olduğu iki Bu seçenekler birbirini dışlamaz ve olası tooget kullanarak ile yapılan bir benzer iş ya da diğer hello olsa da, ayrıca sizin için her ikisini de yedeklemek tooset anlamlı. Çoğu durumda, işlem içi koleksiyonuyla bir aracı birleştirme tooa iş akışı izleme daha güvenilir yol açabilir. EventFlow (işlemdeki toplama) kullanabilirken hello Azure tanılama uzantısını (aracı), uygulama düzeyinde günlükleri için seçilen yolunuzu platform düzeyi günlükleri için olabilir. Nelerin sizin için en iyi dahil edilir sonra nasıl görüntülenir ve analiz, veri toobe istediğinizle ilgili zaman toothink var.

## <a name="event-analysis"></a>Olay çözümleme

Toohello çözümleme ve görselleştirme izleme ve tanılama veri geldiğinde hello pazarında mevcut birkaç harika platformları vardır. Merhaba önerdiğimiz ikisidir [OMS](service-fabric-diagnostics-event-analysis-oms.md) ve [Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tootheir daha iyi tümleştirme Service Fabric, ancak son de hello görünmelidir [esnek yığın](https://www.elastic.co/products) (özellikle, bir küme çevrimdışı bir ortamda çalışan düşünüyorsanız), [Splunk](https://www.splunk.com/), ya da herhangi bir platform, tercih.

Merhaba önemli noktaları seçtiğiniz herhangi bir platform rahatlığı hello kullanıcı arabirimi ve seçenekleri, sorgulama olduğunuz içermelidir hello özelliği toovisualize veri ve kolay okunabilir panolar oluşturun ve hello ek araçlar tooenhance sunar, , otomatik uyarı gibi izleme.

Ayrıca bir Service Fabric kümesi bir Azure kaynağı olarak ayarladığınızda, seçtiğiniz toohello platform, belirli bir performans için yararlı olabilecek makineler için Giden Kutusu Erişim tooAzure'nın izleme ve ölçüm izleme de alırsınız.

### <a name="azure-monitor"></a>Azure İzleyici

Kullanabileceğiniz [Azure İzleyici](../monitoring-and-diagnostics/monitoring-overview.md) toomonitor birçok hello Azure kaynaklarını Service Fabric kümesi oluşturulur. Ölçümleri hello için bir dizi [sanal makine ölçek kümesi](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets) ve tek tek [sanal makineler](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesetsvirtualmachines) otomatik olarak toplanır ve hello Azure portalında görüntülenir. tooview hello hello Azure portal hello Service Fabric kümesi içeren select hello kaynak grubu içinde bilgi toplanmaz. Ardından, tooview istediğinizi seçin hello sanal makine ölçek kümesi. Merhaba, **izleme** bölümünde, select **ölçümleri** tooview hello değerlerin bir grafik.

![Toplanan ölçüm bilgileri Azure portal görünümü](media/service-fabric-diagnostics-overview/azure-monitoring-metrics.png)

toocustomize hello grafikler, hello yönergeleri izleyin [Microsoft Azure ölçümlerini](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md). Bu ölçümleri temel uyarılar açıklandığı gibi oluşturabilirsiniz [oluşturma uyarıları Azure İzleyicisi'nde için Azure services](../monitoring-and-diagnostics/insights-alerts-portal.md). Bölümünde açıklandığı gibi web kancaları kullanarak uyarıları tooa bildirim hizmeti gönderebilirsiniz [bir web kancası Azure ölçüm uyarıyı yapılandırmak](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Azure İzleyici yalnızca bir abonelik destekler. Birden çok abonelik toomonitor ihtiyacınız varsa veya ek özellikler, gerekirse [günlük analizi](https://azure.microsoft.com/documentation/services/log-analytics/), kısmen Microsoft Operations Management Suite hem şirket içi ve bulut tabanlı bir bütünsel BT yönetim çözümü sunar Altyapı. Azure İzleyici verilerden yönlendirebilir doğrudan tooLog Analytics ölçümleri ve günlükleri görebilmeleri tek bir yerde, tüm ortamınız için.

## <a name="next-steps"></a>Sonraki adımlar

### <a name="watchdogs"></a>Watchdogs

Bir izleme, sistem durumu izleyebilir ve hizmetler ve rapor sistem yükü hello sistem durumu modeli hiyerarşi içinde herhangi bir şey için ayrı bir hizmettir. Bu, tek bir hizmeti hello görünümü temel alarak algılanmayacağı hataları önlemeye yardımcı olabilir. Watchdogs de (örneğin, belirli zaman aralıklarında depolama günlük dosyalarında temizleniyor) kullanıcı etkileşimi olmadan düzeltici eylemler gerçekleştiren bir iyi toohost kodu olur. Bir örnek izleme hizmeti uygulaması bulabilirsiniz [burada](https://github.com/Azure-Samples/service-fabric-watchdog-service).

Nasıl olayları ve günlükleri hello sırasında oluşturulan anlama ile çalışmaya başlama [platform düzeyi](service-fabric-diagnostics-event-generation-infra.md) ve hello [uygulama düzeyinde](service-fabric-diagnostics-event-generation-app.md).
