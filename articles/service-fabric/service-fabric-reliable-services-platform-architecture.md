---
title: aaaReliable hizmet mimarisi | Microsoft Docs
description: "Durum bilgisi olan ve durum bilgisi olmayan hizmetler için hello güvenilir hizmet mimarisine genel bakış"
services: service-fabric
documentationcenter: .net
author: AlanWarwick
manager: timlt
editor: vturecek
ms.assetid: af002ae6-7f6d-4769-b049-82aa1ba0891b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2016
ms.author: alanwar
redirect_url: /azure/service-fabric/service-fabric-reliable-services-introduction
ms.openlocfilehash: d2d0ec9600275ae248ab7717be269cc7204a1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Durum bilgisiz ve durum bilgisi olan güvenilir hizmetler için mimarisi
Azure Service Fabric güvenilir hizmeti durum bilgisi olan veya durum bilgisiz olabilir. Her hizmet türü belirli bir mimari içinde çalışır. Bu makalede bu mimarileri açıklanmaktadır.
Merhaba bkz [güvenilir hizmetine genel bakış](service-fabric-reliable-services-introduction.md) hello durum bilgisi olan ve durum bilgisi olmayan hizmetler arasındaki farklar hakkında daha fazla bilgi.

## <a name="stateful-reliable-services"></a>Durum bilgisi olan güvenilir hizmetler
### <a name="architecture-of-a-stateful-service"></a>Durum bilgisi olan hizmet mimarisi
![Durum bilgisi olan hizmet mimarisi diyagramı](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Durum bilgisi olan güvenilir hizmet
Durum bilgisi olan güvenilir hizmet hello StatefulService veya StatefulServiceBase sınıfı türetilemeyeceğini. Temel sınıflar her ikisi de Service Fabric tarafından sağlanır. Bunlar, çeşitli düzeyde destek ve hello durum bilgisi olan hizmet toointerface Service Fabric--ve tooparticipate için Özet hello Service Fabric kümesi içinde bir hizmet olarak sunar.

StatefulService StatefulServiceBase türer. StatefulServiceBase Hizmetleri daha fazla esneklik sunar, ancak daha fazla Service Fabric hello içyüzü anlaşılmasını gerektirir.
Merhaba bkz [güvenilir hizmetine genel bakış](service-fabric-reliable-services-introduction.md) ve [güvenilir kullanım Gelişmiş Hizmet](service-fabric-reliable-services-advanced-usage.md) hello StatefulService ve StatefulServiceBase sınıflarını kullanarak Hizmetleri yazma hello özellikleri hakkında daha fazla bilgi için .

Her iki temel sınıflar hello yaşam süresi ve rol hello hizmet uygulamasının yönetin. Hello hizmet uygulaması hello hizmet uygulaması noktalarda hello hizmet uygulama yaşam döngüsü--iş toodo varsa veya toocreate iletişim dinleyici nesnesi istiyorsa, her iki temel sınıfın sanal yöntemleri geçersiz kılabilir. Bir hizmet uygulaması ICommunicationListener, yukarıdaki hello diyagramda gösterme kendi iletişim dinleyici nesnesi uygulayabilir rağmen hello iletişimi dinleyicisi tarafından Service Fabric--hizmet uygulaması hello olarak uygulandığını Not kullanan bir Service Fabric tarafından uygulanan iletişimi dinleyicisi.

Bir durum bilgisi olan güvenilir hizmet hello güvenilir durumu Yöneticisi tootake avantajı güvenilir koleksiyonları kullanır. Güvenilir koleksiyonları olduğu yüksek oranda kullanılabilir toohello hizmet--yerel veri yapılarını, her zaman hizmeti yerine bağımsız olarak kullanılabilir. Her tür güvenilir koleksiyonunun bir güvenilir durumu sağlayıcısı tarafından uygulanır.
Merhaba güvenilir Koleksiyonlar hakkında daha fazla bilgi için bkz: [güvenilir koleksiyonları genel bakış](service-fabric-reliable-services-reliable-collections.md).

### <a name="reliable-state-manager-and-state-providers"></a>Güvenilir durum Yöneticisi ve durumu sağlayıcıları
Merhaba güvenilir durum Yöneticisi güvenilir durum sağlayıcılarının yöneten hello nesnesidir. Merhaba işlevselliği toocreate sahip, silme, listeleme ve hello güvenilir durum sağlayıcılarının kalıcı ve yüksek oranda kullanılabilir olduğundan emin olun. Bir güvenilir durumu sağlayıcı örneği bir sözlük ya da sırası gibi bir kalıcı ve yüksek oranda kullanılabilir veri yapısı örneği temsil eder.

Her güvenilir durumu sağlayıcısı hello güvenilir durumu sağlayıcısı ile bir durum bilgisi olan hizmet toointeract tarafından kullanılan bir arabirim sunar. Örneğin, IReliableQueue hello güvenilir sıra ile kullanılan toointerface olsa IReliableDictionary hello güvenilir sözlüğü ile kullanılan toointerface ' dir. Tüm güvenilir durum sağlayıcılarının hello IReliableState arabirimini uygular.

Merhaba güvenilir durum Yöneticisi durum bilgisi olan hizmet erişim tooit veren IReliableStateManager adlı bir arabirim sahiptir. Arabirimleri tooreliable durumu sağlayıcıları IReliableStateManager döndürülür.

Merhaba güvenilir durum yöneticisi eklenti mimarisi kullanır, böylece yeni tür güvenilir koleksiyonların dinamik olarak takılı.

Merhaba güvenilir sözlük ve güvenilir sıra yüksek performanslı, sürümlü bir fark deposu hello uygulama üzerinde oluşturulmuştur.

### <a name="transactional-replicator"></a>İşlem çoğaltması
Merhaba işlem çoğaltması bileşen hizmetinin (diğer bir deyişle, hello güvenilir durum Yöneticisi ve hello güvenilir koleksiyonları içinde hello durumunu) hello durumunu hello hizmetini çalıştıran tüm çoğaltmalar arasında tutarlı olmasını sağlamak için sorumludur. Ayrıca, hello durumu hello günlüğüne kalıcı olmasını sağlar. özel bir mekanizma aracılığıyla hello işlem çoğaltması ile Merhaba güvenilir durumu Yöneticisi arabirimleri.

Böylece tüm çoğaltmaları güncel durum bilgilerini hello işlem çoğaltması bir ağ protokolü toocommunicate durumu hello hizmet örneği diğer yinelemelerle kullanır.

Merhaba işlem çoğaltması günlük toopersist durum bilgilerini kullanır, böylece hello durum bilgilerini işlemi devam eder veya düğüm çöker. Merhaba arabirimi toohello günlük özel bir mekanizmadır.

### <a name="log"></a>Günlük
Merhaba günlük bileşeni toospinning veya katı hal diskleri yazmak için iyileştirilmiş bir yüksek performanslı kalıcı depoya sağlar.  Merhaba hello günlüğünün hello kalıcı depolama (yani, sabit diskler) hello durum bilgisi olan hizmet çalıştıran toobe yerel toohello düğümleri tasarımdır. Bu seçenek, düşük gecikme ve yüksek verimlilik için yerel toohello düğümü değil karşılaştırılan tooremote kalıcı depolama alanı sağlar.

Merhaba günlük bileşeni, birden çok günlük dosyalarını kullanır. Tüm çoğaltmaları durumu verilerini depolamak için bu hello en düşük gecikme süreli ve yüksek verimlilik sağlayabilir olarak kullanan bir düğüm genelinde paylaşılan günlük dosyası yok. Varsayılan olarak hello paylaşılan günlük hello Service Fabric düğümü çalışma dizinine yerleştirilir ancak yapılandırılmış toobe ideal olarak yalnızca hello paylaşılan günlüğü için ayrılmış bir disk üzerinde başka bir konumda yerleştirilmiş olabilir. Her çoğaltma hello hizmeti için de bir ayrılmış günlük dosyası vardır ve hello ayrılmış günlük hello hizmetin çalışma dizini içinde yerleştirilir. Farklı bir konumda yerleştirilen hiçbir mekanizması tooconfigure ayrılmış hello günlük toobe yoktur.

Hello paylaşılan günlük hello yinelemenin durumu bilgileri için geçici bir alan, başlangıç sırasında ayrılmış günlük dosyası hello son hedefi olduğu kalıcıdır. Bu tasarımda hello durum bilgilerini ilk yazılı toohello paylaşılan günlük dosyası ve toohello ayrılmış günlük dosyası hello arka planda gevşek taşındı. Bu şekilde, hello yazma toohello paylaşılan günlük hello en düşük gecikme süresi ve daha hızlı hello servis toomake ilerlemeyi sağlayan en yüksek verimlilik gerekir.

Okur ve toohello paylaşılan günlük hello disk hello paylaşılan günlük dosyası için doğrudan g/ç toopreallocated alanı aracılığıyla yapılır yazar. tooallow en iyi ayrılmış günlükleriyle hello sürücüsünde disk alanı kullanımı, bir NTFS seyrek dosya olarak hello ayrılmış günlük dosyası oluşturulur. Bu disk alanının işleminin izin verir ve hello OS gerçekte kullanılan daha çok fazla disk alanı kullanarak hello ayrılmış günlük dosyaları gösterecektir unutmayın.

En az kullanıcı modu arabirimi toohello günlük yanı sıra, bir çekirdek modu sürücüsü olarak hello günlüğüne yazılır. Bir çekirdek modu sürücüsü olarak çalıştırarak hello günlük kullanmak tooall Hizmetleri hello yüksek performans sağlayabilir.

Merhaba günlük yapılandırma hakkında daha fazla bilgi için bkz: [durum bilgisi olan güvenilir hizmetler yapılandırma](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Durum bilgisiz güvenilir hizmeti
### <a name="architecture-of-a-stateless-service"></a>Durum bilgisi olmayan hizmetin mimarisi
![Durum bilgisiz hizmet mimarisi diyagramı](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Durum bilgisiz güvenilir hizmeti
Durum bilgisiz hizmet uygulamaları hello StatelessService veya StatelessServiceBase sınıfından türetilir. Merhaba StatelessServiceBase sınıfı hello StatelessService sınıfı daha fazla esneklik sağlar.
Her iki temel sınıflar hello yaşam süresi ve bir hizmetin rol yönetin.

Merhaba hizmet uygulaması hello hizmet noktalarda hello hizmet yaşam döngüsü--iş toodo varsa veya toocreate iletişim dinleyici nesnesi istiyorsa, her iki temel sınıfın sanal yöntemleri geçersiz kılabilir. Bu hizmet uygulaması bir iletişimi kullandıkça hello hizmet ICommunicationListener, yukarıdaki hello diyagramda gösterme kendi iletişim dinleyici nesnesi uygulayabilir rağmen hello iletişimi dinleyicisi Service Fabric tarafından uygulanır unutmayın Service Fabric tarafından uygulanan dinleyicisi.

Merhaba bkz [güvenilir hizmetine genel bakış](service-fabric-reliable-services-introduction.md) ve [güvenilir kullanım Gelişmiş Hizmet](service-fabric-reliable-services-advanced-usage.md) hello StatelessService ve StatelessServiceBase sınıflarını kullanarak Hizmetleri yazma hello özellikleri hakkında daha fazla bilgi için .

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
Service Fabric hakkında daha fazla bilgi için bkz:

[Güvenilir hizmetine genel bakış](service-fabric-reliable-services-introduction.md)

[Hızlı başlangıç](service-fabric-reliable-services-quick-start.md)

[Güvenilir koleksiyonları genel bakış](service-fabric-reliable-services-reliable-collections.md)

[Kullanım Gelişmiş güvenilir hizmeti](service-fabric-reliable-services-advanced-usage.md)

[Güvenilir hizmet yapılandırması](service-fabric-reliable-services-configuration.md)  

