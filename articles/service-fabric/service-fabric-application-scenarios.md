---
title: "aaaApplication senaryolar ve tasarım | Microsoft Docs"
description: "Service Fabric bulut uygulamalarında kategorilerini genel bakış. Durum bilgisi olan ve durum bilgisiz hizmetleri kullanan uygulama tasarımı açıklanır."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3a8ca6ea-b8e9-4bc3-9e20-262437d2528e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 7/02/2017
ms.author: mfussell
ms.openlocfilehash: e36d5b2d21a6a1e3e85c9b21190072616e4921e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-scenarios"></a>Service Fabric uygulama senaryoları
Azure Service Fabric toowrite sağlayan güvenilir ve esnek bir platform sunar ve iş uygulamaları ve Hizmetleri türlerde çalıştırın. Bu uygulama ve mikro durum bilgisiz veya durum bilgisi olan olabilir ve bunlar arasında sanal makineleri toomaximize verimliliği kaynak dengeli. Service Fabric Hello benzersiz mimarisi tooperform yakın gerçek zamanlı veri analizi, bellek içi hesaplama, paralel işlemleri ve olay uygulamalarınızda işleme sağlar. Kolayca uygulamalarınızı yukarı veya aşağı (gerçekten içeri veya dışarı), değişen kaynak gereksinimlerinize bağlı olarak ölçekleme yapabilirsiniz.

azure'da Hello Service Fabric platformundan uygulama kategorileri aşağıdaki hello için idealdir:

* **Yüksek oranda kullanılabilir hizmetler**: Service Fabric Hizmetleri birden fazla ikincil service çoğaltma oluşturarak hızlı yük devretme sağlar. Bir düğüm, işlem veya bireysel hizmet toohardware veya diğer hatası kullanılamaz hale gelirse hello ikincil çoğaltmaları yükseltilen tooa birincil çoğaltma en az olarak hizmet kaybı ile biridir.
* **Ölçeklenebilir Hizmetler**: tek tek Hizmetleri bölümlenmiş olması, çıkışı hello küme üzerinde Genişletilmiş durum toobe sağlar. Ayrıca, tek tek Hizmetleri oluşturulabilir ve hello anında kaldırıldı. Hizmetleri hızlı ve kolay bir şekilde kullanıma birkaç düğüm toothousands birçok düğümlerde örnekleri üzerinde birkaç örneklerinden ölçeklendirilmiş ve ardından, yeniden kaynak gereksinimlerinize bağlı olarak ölçeklendirilebilir. Service Fabric toobuild bu hizmetleri kullanın ve bunların tam yaşam döngüleri yönetin.
* **Statik olmayan veriler üzerinde hesaplama**: Service Fabric sağlar toobuild verileri, giriş/çıkış ve işlem yoğunluklu durum bilgisi olan uygulamalar. Service Fabric uygulamalarda (hesaplama) işleme hello birlikte bulundurma özelliğini ve verileri sağlar. Normalde, uygulamanız erişim toodata gerektirdiğinde, bir dış veri önbelleği ya da depolama katmanı ile ilişkili ağ gecikme süresi yok. Durum bilgisi olan Service Fabric Hizmetleri ile bu gecikme, daha fazla kullanıcı etkinleştirme okuyan ve yazan ortadan kalkar. Örneğin, 100 milisaniyeden gidiş dönüş süresi gereksinimi sahip müşteriler için gerçek zamanlı öneri seçimleri yakın gerçekleştiren bir uygulamaya sahip söyleyin. Merhaba gecikme süresi ve performans özelliklerini (burada hello hesaplama öneri seçimin hello veri ve kuralları ile birlikte bulunan) Service Fabric Hizmetleri hello standart uygulama ile karşılaştırıldığında esnek deneyimi toohello kullanıcı sağlar modelin, uzaktaki depolama biriminden toofetch hello gerekli verilere sahip olmak için.  
* **Oturum tabanlı etkileşimli uygulamalar**: Service Fabric, çevrimiçi oyun veya anlık ileti, gibi uygulamalarınız düşük gecikme süresi okuma ve yazma işlemleri gerektiriyorsa yararlıdır. Service Fabric, ayrı depolama veya önbellek, durum bilgisiz uygulamaları için gerekli olarak toocreate gerek kalmadan, bu etkileşimli, durum bilgisi olan uygulamalar, toobuild sağlar. (Bu gecikme artar ve büyük olasılıkla tutarlılık sorunları tanıtır.).
* **Veri analizi ve iş akışları**: Hızlı Okuma hello ve Service Fabric yazma olayları veya veri akışları güvenilir bir şekilde işlemelidir uygulamaları etkinleştirin. Service Fabric ayrıca sağlar işleme ardışık düzenleri, burada sonuçlar olmalıdır güvenilir ve geçirilen açıklamak uygulamalar üzerinde toohello sonraki aşaması kaybı olmadan işleme. Bu, veri tutarlılığı ve hesaplama garantileri gerekli olduğu, işlem ve finansal sistemleri içerir.
* **Veri toplama, işleme ve IOT**: Service Fabric büyük ölçekli işleme ve düşük gecikme süresi, durum bilgisi olan hizmetlere sahip olduğundan, hello cihaz ve hello hesaplama hello verileri nerede milyonlarca cihaza üzerindeki veri işleme için idealdir birlikte bulunan.
Service Fabric dahil olmak üzere kullanarak IOT sistemleri yerleşik birkaç müşteriler anlatıldığı [BMW](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/24/service-fabric-customer-profile-bmw-technology-corporation/), [Schneider elektrik](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/05/service-fabric-customer-profile-schneider-electric/) ve [kafes sistemleri](https://blogs.msdn.microsoft.com/azureservicefabric/2016/06/20/service-fabric-customer-profile-mesh-systems/).

## <a name="application-design-case-studies"></a>Uygulama tasarım örnek olay incelemeleri
Service Fabric kullanılan toodesign uygulamaları nasıl gösteren çalışmalar sayısı üzerinde hello yayımlanan [Service Fabric ekip blogu](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/) ve hello [mikro çözümleri site](https://azure.microsoft.com/solutions/microservice-applications/).

## <a name="design-applications-composed-of-stateless-and-stateful-microservices"></a>Uygulamaları tasarlama durum bilgisiz ve durum bilgisi olan mikro oluşur
Azure bulut hizmeti çalışan rolleri ile uygulamaları oluşturmak, bir durum bilgisi olmayan hizmetin örneğidir. Buna karşılık, durum bilgisi olan mikro yetkili durumlarına hello istek ve yanıt dışında tutun. Bu, yüksek kullanılabilirlik ve çoğaltma tarafından yedeklenen işlem garanti sağlayan basit API'ler aracılığıyla hello durumu tutarlılığı sağlar. Service Fabric'ın durum bilgisi olan hizmetler yüksek kullanılabilirlik, uygulamalar, yalnızca veritabanları ve diğer veri depolarına tooall türleri getiren democratize. Doğal progression budur. Uygulamalar için yüksek kullanılabilirlik tooNoSQL veritabanları tamamen ilişkisel veritabanları kullanarak zaten taşınmış. Artık hello uygulamaların kendileri "etkin" durumu ve bunların içinde güvenilirlik, tutarlılık veya kullanılabilirlikten ödün vermeden ek performans artışları için yönetilen veri olabilir.

Mikro oluşan uygulamaları oluştururken, durum bilgisiz web uygulamaları (ASP.NET, Node.js, vb.) bileşimini genellikle sahip durum bilgisiz ve durum bilgisi olan iş orta katman Hizmetleri'ni çağrılırken, tüm hello aynı dağıtılan Service Fabric kümesi Merhaba Service Fabric dağıtım komutlarını kullanarak. Bu hizmetlerin her birini, büyük ölçüde geliştirme ve yaşam döngüsü Yönetimi'nde çeviklik geliştirme şekilde tooscale, güvenilirlik ve kaynak kullanımı bağımsızdır.

Durum bilgisi olan mikro hello ek sıraları hello gereksinimini kaldırın ve gerekli tooaddress geleneksel silinmiş önbellekleri tamamen durum bilgisiz uygulamaların kullanılabilirlik ve gecikme süresi gereksinimlerine hello çünkü uygulama tasarımları basitleştirin. Durum bilgisi olan hizmetler doğal olarak yüksek oranda kullanılabilir ve düşük gecikme süresi olduğundan, olduğunu daha az taşıma bölümleri toomanage uygulamanızda bir bütün olarak gelir. Aşağıdaki Hello diyagramlar tasarlama ve durum bilgisi olan bir durum bilgisi olmayan bir uygulama arasındaki hello farklar gösterilmektedir. Merhaba yararlanarak [Reliable Services](service-fabric-reliable-services-introduction.md) ve [Reliable Actors](service-fabric-reliable-actors-introduction.md) modellerini programlama, durum bilgisi olan hizmetler uygulama karmaşıklığını yüksek verimlilik ve düşük gecikme süresi elde etmeye devam ederken azaltın.

## <a name="an-application-built-using-stateless-services"></a>Durum bilgisi olmayan hizmetler kullanılarak oluşturulmuş bir uygulama
![Durum bilgisiz hizmetini kullanarak uygulama][Image1]

## <a name="an-application-built-using-stateful-services"></a>Durum bilgisi olan hizmetleri kullanılarak oluşturulan uygulama
![Durum bilgisiz hizmetini kullanarak uygulama][Image2]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar

* Çok dinleme[müşteri örnek olay incelemeleri](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=qDJnf86yC_5206218965
)
* Hakkında bilgi edinin [müşteri örnek olay incelemeleri](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)
* Daha fazla bilgi edinmek [modelleri ve senaryoları](service-fabric-patterns-and-scenarios.md)

* Durum bilgisiz ve durum bilgisi olan hizmetler hello Service Fabric ile oluşturmaya başlamak [güvenilir hizmetler](service-fabric-reliable-services-quick-start.md) ve [güvenilir aktörler](service-fabric-reliable-actors-get-started.md) modellerini programlama.
* Ayrıca aşağıdaki konularda hello bakın:
  * [Mikro hizmetler hakkında bilgi ver](service-fabric-overview-microservices.md)
  * [Hizmetinin durumunu yönetin](service-fabric-concepts-state.md)
  * [Service Fabric hizmetlerin kullanılabilirliğini](service-fabric-availability-services.md)
  * [Ölçek Service Fabric Hizmetleri](service-fabric-concepts-scalability.md)
  * [Bölüm Service Fabric Hizmetleri](service-fabric-concepts-partitioning.md)

[Image1]: media/service-fabric-application-scenarios/AppwithStatelessServices.jpg
[Image2]: media/service-fabric-application-scenarios/AppwithStatefulServices.jpg
