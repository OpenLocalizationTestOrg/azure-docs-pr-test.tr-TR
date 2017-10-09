---
title: "aaaIntroducing hello Service Fabric kümesi Resource Manager | Microsoft Docs"
description: "Giriş toohello Service Fabric kümesi Resource Manager."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: cfab735b-923d-4246-a2a8-220d4f4e0c64
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e815925880e2f3a755294de1dcfb9b88fbdde08a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-hello-service-fabric-cluster-resource-manager"></a>Merhaba Service Fabric kümesi Kaynak Yöneticisi Tanıtımı
Geleneksel BT sistemleri veya çevrimiçi hizmetleri yönetmek için kullanılan belirli fiziksel veya sanal makinelere toothose belirli hizmetleri veya sistemleri ayrılması anlamına gelir. Hizmetleri katmanları tasarlanmış. "Web" bir katman ve "verileri" veya "depolama" katman olacaktır. Uygulamaları burada istekleri makineler ayrılmış toocaching bir dizi yanı sıra içeri ve dışarı aktarılan bir Mesajlaşma katmanına sahip olması gerekir. Her katman veya iş yükü türünü belirli makineler ayrılmış tooit vardı: hello veritabanı birkaç birkaç makineler ayrılmış tooit, hello web sunucuları aldı. Belirli bir iş yükü türünü toorun çok sıcak edildi hello makineler neden olursa, o aynı yapılandırma toothat katmanı ile daha fazla makine eklendi. Ancak, tüm iş yüklerinin çıkışı kolay ölçeklendirilmesi - özellikle hello veri katmanı ile genellikle daha büyük makineler makinelerle değiştirirsiniz. Kolay. Bir makine başarısız olursa hello genel uygulama kısmı hello makine geri kadar düşük kapasitede verdi. Hala oldukça kolay (değil mutlaka eğlenceli değilse).

Şimdi ancak hello world hizmetinin ve yazılım mimarisi değişti. Uygulamaları ölçeklendirme tasarım benimseyen daha yaygın bir durumdur. Kapsayıcılar veya mikro uygulamalarla (veya her ikisi de) oluşturma yaygındır. Yalnızca birkaç makineler hala olabilir, ancak artık, bir iş yükü yalnızca tek bir örneğini çalıştırdıkları değil. Bunlar bile birden çok farklı iş yükleri hello çalışmıyor olabilir aynı anda. Artık farklı türlerdeki Hizmetleri (none kaynaklar arasında tam makinenin eşitleyeceğini tüketen) düzinelerce belki farklı örnekleri hizmetlerin yüzlerce sahipsiniz. Her adlandırılmış örnek yüksek kullanılabilirlik (HA için) bir veya daha fazla örneği veya çoğaltmaları sahiptir. Merhaba boyutunu bu iş yüklerini ve ne kadar meşgul olduklarına bağlı olarak, kendiniz yüzlerce veya binlerce makinelerin ile karşılaşabilirsiniz. 

Aniden ortamınızı yönetme birkaç makineler ayrılmış toosingle tür iş yüklerinin yönetilmesi kadar basit değil. Sunucularınızın sanal ve artık adlara sahip (mindsets gelen geçtiyseniz [Evcil Hayvanlar toocattle](http://www.slideshare.net/randybias/architectures-for-open-and-scalable-clouds/20) tüm). Yapılandırma hello makinesinin hakkında hello Hizmetleri kendilerini hakkında daha fazla küçük. Ayrılmış tooa tek bir iş yükü örneğidir donanım büyük ölçüde bir hello geçmiş olan şeydir. Hizmetleri kendilerini, ticari donanım birden çok daha küçük parçalarını span küçük dağıtılmış sistemlerin hale getirildi.

Uygulamanız artık monoliths birkaç katmanları yayılan bir dizi olduğundan, artık çok daha fazla birleşimleri toodeal ile sahipsiniz. Kimin karar ne tür iş yüklerinin hangi donanımda çalıştırabilirsiniz veya kaç tane? Hangi iş yüklerini de hello üzerinde aynı iş donanım ve çakışan? Bir makinede aşağı nasıl yapılacağı gittiğinde ne var. Bu makinede çalışan biliyor? İş yükü sağlamaktan sorumlu kim yeniden çalışmaya başladıktan? Merhaba (sanal?) makine toocome geri bekleyin veya iş yüklerinizi tooother makineler ve çalışan Canlı üzerinden otomatik olarak başarısız? İnsan eli gerekli mi? Bu ortamdaki yükseltmeler nasıldır?

Geliştiriciler ve bu ortamda ilgilenme işleçleri bu karmaşıklık yönetme toowant Yardımı yapacağız. A binge işe alma ve toohide hello karmaşıklık kişilerle çalışırken büyük olasılıkla hello sağ yanıt, bu nedenle ne yapmak istersiniz?

## <a name="introducing-orchestrators"></a>Orchestrators Tanıtımı
Bir "Orchestrator" Merhaba genel bu tür ortamlarda yönetmesine yardımcı olan yazılım parçasının bir terimdir. Orchestrators "Benim ortamında çalışan bu hizmeti beş kopyası istiyorum."gibi isteklerinde ele hello bileşenlerdir Bunlar ne olacağını olsun toomake hello ortam eşleşme istenen hello durumu, deneyin.

Orchestrators (değil insanlar) ne bir makine hata verdiğinde veya beklenmeyen bir nedenden dolayı bir iş yükü sonlandırır eylemde ' dir. Çoğu orchestrators daha fazlasını hata ile ilgilidir. Sahip oldukları diğer özellikleri yükseltmeler işleme ve kaynak tüketimini ve idare ilgilenme yeni dağıtımlar, yönettiğiniz. Tüm orchestrators temelde hello ortamında yapılandırmasında istenen bazı durumunu korumak hakkında var. Toobe mümkün tootell bir orchestrator istediğiniz ne isterseniz ve onu sahip ağır lifting hello. Aurora Mesos, veri merkezi/Docker Docker Swarm, Kubernetes ve Service Fabric üstünde orchestrators, tüm örnekler verilmiştir. Bu orchestrators gerçek iş yüklerinin üretim ortamlarında etkin olarak geliştirilen toomeet hello gereksinimlerini yükleniyor. 

## <a name="orchestration-as-a-service"></a>Bir hizmet olarak düzenleme
Hello küme Resource Manager, Service Fabric düzenleme işleme hello sistem bileşenidir. Merhaba küme Resource Manager'ın iş üç bölüme ayrılmıştır:

1. Kural zorlama
2. Ortamınıza en iyi duruma getirme
3. Diğer işlemlerle yardımcı olma

toosee hello küme kaynak yöneticisi nasıl çalışır Microsoft Virtual Academy video aşağıdaki hello izleyin:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=d4tka66yC_5706218965">
<img src="./media/service-fabric-cluster-resource-manager-introduction/ConceptsAndDemoVid.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="what-it-isnt"></a>Ne değil
Geleneksel N katmanlı uygulamalar olduğundan her zaman bir [yük dengeleyici](https://en.wikipedia.org/wiki/Load_balancing_(computing)). Bu genellikle bir ağ yük dengeleyici (NLB) veya bir uygulama yük dengeleyici (burada hello ağ yığını sat bağlı olarak ALB) oluştu. Donanım tabanlı F5'ın Bigıp sunumu gibi bazı yük Dengeleyiciler, diğerleri ise, yazılım tabanlı gibi Microsoft NLB. Diğer ortamlarda, bir şey HAProxy, nginx, Istio veya haberci gibi bu rolde görebilirsiniz. Bu mimari, Yük Dengelemesi hello tooensure durum bilgisiz iş yükleri alır (yaklaşık) hello iş aynı iş miktarı. Dengeleme stratejileri, çeşitli yükleyin. Bazı dengeleyicileri her farklı çağrısı tooa farklı sunucu gönderebilir. Başkalarının sabitleme oturum/sürekliliği sağlanır. Daha gelişmiş dengeleyicileri gerçek yük tahmin veya bir çağrı, beklenen maliyeti ve geçerli makine yükü temel alarak raporlama tooroute kullanın.

Web/çalışan katmanı hello ağ dengeleyicileri veya ileti çalıştı yönlendiriciler tooensure kabaca dengeli kalan. Merhaba veri katmanı Dengeleme stratejileri farklı ve hello veri depolama mekanizmasını bağımlı. Merhaba veri katmanı Dengeleme önbelleğe alma, yönetilen görünümleri, saklı yordamları ve diğer depolama özgü mekanizmaları veri parçalama üzerinde dayanıyordu.

Bu stratejileri ilginç durumdayken hello Service Fabric kümesi Kaynak Yöneticisi herhangi bir şey Ağ Yük Dengeleyici veya önbellek gibi değil. Bir ağ yük dengeleyicisi, ön uçlar arasında trafiği yayarak ön uçlar dengeler. Merhaba Service Fabric kümesi Kaynak Yöneticisi, farklı bir strateji vardır. Temelde, Service Fabric taşır *Hizmetleri* trafiği bekleniyor çoğu algılama hello veya toofollow yük yaptıkları toowhere. Örneğin, çok iş vardır hello Hizmetleri yapmamanın olduğundan şu anda soğuk Hizmetleri toonodes taşıyın. Mevcut hello Hizmetleri silinmiş veya başka bir yere taşınmış olduğundan hello düğümleri soğuk olabilir. Başka bir örnek olarak, hello Küme Kaynak Yöneticisi ayrıca bir hizmet bir makine çıktığınızda taşıyabilirsiniz. Belki de hello makine yükseltilmiş toobe hakkında ya da tooa ani artış tüketimi nedeniyle üzerinde çalıştırılan hello Hizmetleri tarafından aşırı yüklendi. Alernatively, hello hizmetin kaynak gereksinimlerini artış gösterdi. Sonuç olarak çalışan bu makine toocontinue üzerinde yeterli kaynak yok. 

Merhaba küme Resource Manager hizmetlerin taşımak için sorumlu olduğu için bir ağ yük dengeleyicisi bulur farklı özellik kümesi karşılaştırıldığında toowhat içerir. Bu konum hello hizmetin kendisini çalıştırmak için ideal olsa bile Ağ Yük Dengeleyici zaten hizmetlerdir, ağ trafiğini toowhere teslim olmasıdır. Merhaba Service Fabric kümesi Kaynak Yöneticisi hello kümedeki hello kaynaklar verimli bir şekilde kullanıldığını sağlamaya yönelik temelde farklı stratejileri kullanır.

## <a name="next-steps"></a>Sonraki adımlar
- Merhaba mimarisi ve bilgi akışını hello küme Resource Manager içinde hakkında daha fazla bilgi için kullanıma [bu makalede](service-fabric-cluster-resource-manager-architecture.md)
- Merhaba küme Resource Manager hello küme açıklamak için birçok seçeneğiniz vardır. toofind ölçümler hakkında daha fazla bilgi, bu makalede denetleyin [açıklayan bir Service Fabric kümesi](service-fabric-cluster-resource-manager-cluster-description.md)
- Hizmetleri yapılandırma hakkında daha fazla bilgi için [hizmetleri yapılandırma hakkında bilgi edinin](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Kullanım ve kapasite hello kümedeki hello Service Fabric kümesi kaynak yöneticisi nasıl yönettiğini ölçümleridir. toolearn ölçümleri ve nasıl tooconfigure bunları kullanıma hakkında daha fazla [bu makalede](service-fabric-cluster-resource-manager-metrics.md)
- Merhaba küme Resource Manager ile Service Fabric'ın yönetim özelliklerini çalışır. Bu tümleştirme hakkında daha fazla toofind okuma [bu makalede](service-fabric-cluster-resource-manager-management-integration.md)
- toofind hello Küme Kaynak Yöneticisi yönetir ve dengeleyen hello kümedeki yük hakkında hello makalesine üzerinde kullanıma [Yük Dengeleme](service-fabric-cluster-resource-manager-balancing.md)
