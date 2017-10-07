---
title: "Service Fabric olay çözümleme OMS ile aaaAzure | Microsoft Docs"
description: "Görselleştirme ve izleme ve tanılama Azure Service Fabric kümeleri için OMS kullanarak olayları analiz etme hakkında bilgi edinin."
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
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 526519293e70982c95e31241465b87f190096f74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-oms"></a>Olay çözümleme ve OMS Görselleştirme

Operations Management Suite (OMS), izleme ve tanılama uygulamaları için yardımcı Yönetim Hizmetleri ve hello bulutta barındırılan hizmetleri koleksiyonudur. tooget OMS ve ne sunar, daha ayrıntılı bir genel bakış okuma [OMS nedir?](../operations-management-suite/operations-management-suite-overview.md)

## <a name="log-analytics-and-hello-oms-workspace"></a>Günlük analizi ve hello OMS çalışma

Günlük analizi bir Azure depolama tablo veya bir aracı da dahil olmak üzere yönetilen kaynaklardan veri toplayan ve merkezi bir depoya tutar. Merhaba veriler, ardından analiz, uyarı ve görselleştirme için kullanılan ya da daha fazla verme olabilir. Günlük analizi olayları, performans verileri ya da herhangi bir özel veri destekler.

OMS yapılandırıldığında, erişim tooa özel olacaktır *OMS çalışma*, burada veri yüklenebilir sorgulanan veya panolarında görselleştirilen kaynağı.

Günlük analizi tarafından alınan veri sonra OMS birkaç sahip *yönetim çözümleri* paketlenmiş çözümleri toomonitor gelen verileri, özelleştirilmiş tooseveral senaryoları şunlardır. Bunlar bir *Service Fabric Analytics* çözüm ve *kapsayıcıları* hello iki en ilgili olanları toodiagnostics ve Service Fabric kümeleri kullanırken izleme çözümü. Birkaç diğerleri de incelenmesi yararlı olan vardır ve OMS de sağlar hello oluşturulması hakkında daha fazla bilgiyi özel çözümler için [burada](../operations-management-suite/operations-management-suite-solutions.md). Bir küme hello yapılandırılacak için toouse seçin her bir çözüm için günlük analizi yanında aynı OMS çalışma. Çalışma alanları özel panolar ve veri görselleştirme için izin ve toocollect, istediğiniz değişiklikleri toohello verileri işlemek ve analiz edin.

## <a name="setting-up-an-oms-workspace-with-hello-service-fabric-solution"></a>Bir OMS çalışma hello hizmeti yapı çözümü ile ayarlama

Önerilen OMS çalışma alanınızda hello hizmeti yapı çözümü içerir, çünkü yararlı bir Pano sağlar hello hello platform ve uygulama düzeyi ve hello mümkün tooquery Service Fabric çeşitli gelen günlük kanalları belirli gösterir günlüğe kaydeder. Görece basit bir Service Fabric çözüm nasıl, hello kümesi üzerinde dağıtılmış tek bir uygulama ile göründüğünü aşağıda verilmiştir:

![OMS BT çözümü](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-solution.png)

İki yolu tooprovision vardır ve Resource Manager şablonu üzerinden veya doğrudan Azure Marketi'nden bir OMS çalışma yapılandırın. Merhaba eski bir küme dağıtımı ve Tanılama ile dağıtılan bir küme zaten varsa ikinci hello etkin olduğunda kullanın.

### <a name="deploying-oms-using-a-resource-management-template"></a>Kaynak Yönetimi şablonunu kullanarak OMS dağıtma

Bu hello küme oluşturma aşamada gerçekleşir - Resource Manager şablonu, hello şablonu kullanarak bir küme dağıtımı yeni bir OMS çalışma alanı da oluşturabilirsiniz, hello hizmeti yapı çözümü tooit ekleyin ve tooread verileri hello uygun depolama biriminden yapılandırın tabloları silin.

>[!NOTE]
>Bu toowork için tanılama hello Azure depolama tabloları tooexist sırada için OMS etkin toobe sahip / gelen günlük analizi tooread bilgileri.

[Burada](https://azure.microsoft.com/resources/templates/service-fabric-oms/) eylemleri gerçekleştirir gereksinime uygun şekilde değiştirin ve kullanan bir örnek şablonudur. Daha fazla isteğe bağlı olma istediğinizden, burada hello işleminde bir OMS çalışma ayarını olabilir bağlı olarak farklı seçenekler size birkaç daha fazla şablon vardır - konumunda bulunabilir hello durumda [Service Fabric ve OMS şablonları](https://azure.microsoft.com/resources/templates/?term=service+fabric+OMS).

### <a name="deploying-oms-using-through-azure-marketplace"></a>Azure Marketi'nde OMS kullanarak dağıtma

Bir küme dağıttıktan sonra tooadd bir OMS çalışma tercih ederseniz, head tooAzure Market ve Ara *"Service Fabric Analytics"*. Merhaba "+ Yönetimi izleme" kategorisi, aşağıda görüldüğü içinde gösteren bir kaynak yalnızca olmalıdır:

![OMS BT analizi pazarında](media/service-fabric-diagnostics-event-analysis-oms/service-fabric-analytics.png)

Tıklatarak **oluşturma** için OMS çalışma sorar. Tıklatın **bir çalışma alanı seçin** ve ardından **yeni bir çalışma alanı oluşturma**. Gerekli hello girişleri doldurun - hello yalnızca burada hello abonelik hello Service Fabric kümesi ve hello OMS çalışma olmalıdır için aynı hello gereksinimdir. Girişlerinizi doğruladıktan sonra OMS çalışma birkaç dakika içinde dağıtır. Dağıtma tamamlarken hello Service Fabric çözüm dikey penceresinde hello oluşturulmasını açık kalır. Altında aynı çalışma programları hello emin olun *OMS çalışma* ve isabet **oluşturma** hello altındaki tooadd hello Service Fabric çözüm toohello çalışma.

## <a name="using-hello-oms-agent"></a>Merhaba OMS Aracısı kullanma

Toouse EventFlow önerilen WAD toplama çözümler için daha modüler bir yaklaşım toodiagnostics izin verdiğinden ve izleme. Örneğin, EventFlow, çıkışlarından toochange istiyorsanız, hiçbir değişiklik tooyour gerçek araçları, yalnızca bir basit bir değişiklikle tooyour yapılandırma dosyası gerektirir. Ancak, OMS kullanarak tooinvest karar verin ve istekli, olay çözümleme için kullanarak toocontinue (yok toobe hello yalnızca platform kullanın, ancak bu BT hello platformları en az biri yerine olacaktır), hello ayarlamakeşfedinöneririz[</C0>OMSAracısı<spanclass="notranslate">](../log-analytics/log-analytics-windows-agents.md).</span> Ayrıca hello OMS Aracısı kapsayıcıları tooyour küme dağıtırken aşağıda açıklandığı gibi kullanmanız gerekir.

Uzantı tooyour Resource Manager şablonu, bir sanal makine ölçek kümesi gibi yalnızca tooadd hello aracı, her düğümleriniz yüklenmesini sağlayarak sahip olduğundan bunu hello işlem oldukça kolaydır. Hello OMS çalışma hello Service Fabric çözüm (yukarıdaki gibi) ile dağıtır ve hello Aracısı tooyour düğümleri ekleyen bir örnek Resource Manager şablonu çalıştıran kümeler için bulunabilir [Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows) veya [Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux).

Bu Hello avantajları hello şunlardır:

* Merhaba performans sayaçları ve ölçümleri tarafında daha zengin veri
* Hello toplanmakta olan kolay tooconfigure veri küme ve uygulamalarınızı yeniden dağıtmadan değişiklikleri tooit yapın veya hello Aracısı'nın toohello ayarlarını değiştirir hello OMS çalışma alanından yapılabilir ve yalnızca olacak hello küme hello Aracısı Sıfırla otomatik olarak. belirli performans sayaçları, Git toohello çalışma yukarı tooconfigure hello OMS Aracısı toopick **Giriş > ayarları > veri > Windows performans sayaçlarını** ve toplanan toosee gibi hello veri çekme
* Verileri görüntülenir, OMS tarafından çekilen önce depolanan toobe sahip daha hızlı / günlük analizi
* Docker günlükleri (stdout, stderror) ve istatistikleri (kapsayıcı ve düğüm düzeyde performans ölçümleri) seçebilirsiniz kapsayıcıları izleme çok daha kolay olduğu

Merhaba ana Burada, bir aracı olduğundan olur; böylece bazı uygulamalarınızın hello kümede en az etki toohello performansını, kümenizdeki tüm uygulamalarınızın, yanında dağıtılacak olduğunu noktadır.

## <a name="monitoring-containers"></a>Kapsayıcı izleme

Kapsayıcıları tooa Service Fabric kümesi dağıtırken hello küme hello OMS Aracısı ile ayarlanmış ve bu Merhaba kapsayıcılara çözüm tooyour OMS çalışma tooenable izleme ve tanılama eklendiğinden önerilir. Bir çalışma alanında çözüm benzer hangi hello kapsayıcıları aşağıda verilmiştir:

![Temel OMS Panosu](./media/service-fabric-diagnostics-event-analysis-oms/oms-containers-dashboard.png)

Merhaba Aracısı OMS sorgulanabilir veya toovisualized performans göstergelerini kullanılan birkaç kapsayıcı özgü günlükleri hello koleksiyonunu sağlar. toplanan hello günlük türleri şunlardır:

* ContainerInventory: kapsayıcı konumunu, adı ve görüntüleri hakkında bilgi gösterir
* ContainerImageInventory: bilgi kimlikleri veya boyutları dahil olmak üzere, dağıtılan görüntüler hakkında
* ContainerLog: belirli hata günlüklerini, docker günlükleri (stdout, vb.) ve diğer girişleri
* ContainerServiceLog: çalıştırılmış docker arka plan programı komutları
* Perf: kapsayıcı dahil olmak üzere performans sayaçlarını cpu, bellek, ağ trafiğini, disk g/ç ve hello özel ölçümleri makineler ana bilgisayar

Bu makalede hello adımları gerekli tooset kapsayıcı kümeniz için izleme yukarı kapsar. OMS'ın kapsayıcıları çözüm hakkında daha fazla toolearn kullanıma kendi [belgelerine](../log-analytics/log-analytics-containers.md).

Merhaba kapsayıcı çözüm çalışma alanınızdaki yukarı tooset yukarıda belirtilen hello adımları izleyerek, küme düğümlerinde dağıtılan hello OMS aracısı yüklü olduğundan emin olun. Merhaba küme hazır olduktan sonra bir kapsayıcı tooit dağıtın. İlk kez bir kapsayıcı görüntüsü hello aklınızda ayı dağıtılan tooa küme, boyutuna bağlı olarak birkaç dakika toodownload hello görüntü alır.

Azure Marketi'nde arama *kapsayıcıları* ve kapsayıcıları kaynağı oluşturun (altında hello izleme + yönetim kategorisi).

![Kapsayıcıları çözüm ekleme](./media/service-fabric-diagnostics-event-analysis-oms/containers-solution.png)

Merhaba oluşturma adımda bir OMS çalışma ister. Yukarıdaki hello dağıtımı ile oluşturulmuş bir Hello seçin. Bu adım, OMS çalışma kapsayıcıları çözümünüzde ekler ve hello şablon tarafından dağıtılan hello OMS aracısı tarafından otomatik olarak algılanır. Merhaba Aracısı Merhaba kapsayıcılara işlemler hello küme ve 15 dakikadan kısa üzerinde veri toplamayı başlatmak veya bu nedenle, hello çözüm hello Pano yukarıdaki hello görüntüsü olduğu gibi verilerle yukarı hafif görmeniz gerekir.


## <a name="next-steps"></a>Sonraki adımlar

OMS araçları aşağıdaki hello keşfedin ve seçenekleri toocustomize çalışma tooyour gerekiyor:

* Şirket içi kümeleri için OMS kullanılan toosend veri tooOMS olabilir bir ağ geçidi (HTTP İleri Proxy) sunar. Uygulamasında hakkında daha fazla bilgi [kullanarak Internet erişimini tooOMS hello olmadan OMS ağ geçidi bilgisayarları bağlama](../log-analytics/log-analytics-oms-gateway.md)
* Yukarı OMS tooset yapılandırma [uyarı otomatik](../log-analytics/log-analytics-alerts.md) tooaid algılama ve tanılama
* Merhaba ile familiarized [günlük arama ve sorgulama](../log-analytics/log-analytics-log-searches.md) günlük analizi bir parçası olarak sunulan özellikler
