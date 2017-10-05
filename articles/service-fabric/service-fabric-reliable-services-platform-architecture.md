---
title: "Güvenilir hizmet mimarisi | Microsoft Docs"
description: "Durum bilgisi olan ve durum bilgisi olmayan hizmetler için güvenilir hizmet mimarisine genel bakış"
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
ms.openlocfilehash: a00a16945356b9731485554e06df46528b5c7bb2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Durum bilgisiz ve durum bilgisi olan güvenilir hizmetler için mimarisi
Azure Service Fabric güvenilir hizmeti durum bilgisi olan veya durum bilgisiz olabilir. Her hizmet türü belirli bir mimari içinde çalışır. Bu makalede bu mimarileri açıklanmaktadır.
Bkz: [güvenilir hizmetine genel bakış](service-fabric-reliable-services-introduction.md) durum bilgisi olan ve durum bilgisi olmayan hizmetler arasındaki farklar hakkında daha fazla bilgi için.

## <a name="stateful-reliable-services"></a>Durum bilgisi olan güvenilir hizmetler
### <a name="architecture-of-a-stateful-service"></a>Durum bilgisi olan hizmet mimarisi
![Durum bilgisi olan hizmet mimarisi diyagramı](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Durum bilgisi olan güvenilir hizmet
Durum bilgisi olan güvenilir hizmet StatefulService veya StatefulServiceBase sınıfından türetilen. Temel sınıflar her ikisi de Service Fabric tarafından sağlanır. Bunlar, çeşitli düzeyde destek ve durum bilgisi olan hizmet ile Service Fabric--arabirim ve Service Fabric kümesi içinde bir hizmet olarak katılmak için Özet sunar.

StatefulService StatefulServiceBase türer. StatefulServiceBase Hizmetleri daha fazla esneklik sunar, ancak daha fazla Service Fabric içyüzü anlaşılmasını gerektirir.
Bkz: [güvenilir hizmetine genel bakış](service-fabric-reliable-services-introduction.md) ve [güvenilir kullanım Gelişmiş Hizmet](service-fabric-reliable-services-advanced-usage.md) StatefulService ve StatefulServiceBase sınıflarını kullanarak Hizmetleri yazma özellikleri hakkında daha fazla bilgi için.

Her iki temel sınıfları yaşam süresi ve hizmet uygulaması rolü yönetin. Hizmet uygulaması, hizmet uygulaması noktalarda hizmet uygulama yaşam döngüsü--yapmak için iş varsa veya bir iletişim dinleyici nesnesi oluşturmak isterse, her iki temel sınıfın sanal yöntemleri geçersiz kılabilir. İletişim dinleyicisi bir hizmet uygulaması ICommunicationListener, yukarıdaki diyagramda gösterme kendi iletişim dinleyici nesnesi uygulayabilir rağmen hizmet uygulaması kullandıkça Service Fabric tarafından--uygulanır Not bir Service Fabric tarafından uygulanan iletişimi dinleyicisi.

Bir durum bilgisi olan güvenilir hizmet güvenilir koleksiyonları yararlanmak için güvenilir durum Yöneticisi'ni kullanır. Güvenilir koleksiyonları olan hizmete--yüksek oranda kullanılabilir yerel veri yapılarını, her zaman hizmeti yerine bağımsız olarak kullanılabilir. Her tür güvenilir koleksiyonunun bir güvenilir durumu sağlayıcısı tarafından uygulanır.
Güvenilir Koleksiyonlar hakkında daha fazla bilgi için bkz: [güvenilir koleksiyonları genel bakış](service-fabric-reliable-services-reliable-collections.md).

### <a name="reliable-state-manager-and-state-providers"></a>Güvenilir durum Yöneticisi ve durumu sağlayıcıları
Güvenilir durum Yöneticisi güvenilir durum sağlayıcılarının yöneten nesnesidir. Oluşturma, silme, listeleme ve güvenilir durum sağlayıcılarının kalıcı ve yüksek oranda kullanılabilir olduğundan emin olmak için bir işleve sahiptir. Bir güvenilir durumu sağlayıcı örneği bir sözlük ya da sırası gibi bir kalıcı ve yüksek oranda kullanılabilir veri yapısı örneği temsil eder.

Her güvenilir durumu Sağlayıcısı güvenilir durumu sağlayıcısı ile etkileşim kurmak için bir durum bilgisi olan hizmeti tarafından kullanılan bir arabirim sunar. Örneğin, IReliableDictionary kullanılabilir IReliableQueue kullanılırken güvenilir sözlük ile arabirim oluşturmak için güvenilir sıra ile arabirim oluşturmak için. Tüm güvenilir durum sağlayıcılarının IReliableState arabirimini uygular.

Güvenilir durumu Yöneticisi erişim olanak sağlayan bir durum bilgisi olan hizmetinden IReliableStateManager adlı bir arabirim sahiptir. Güvenilir durum sağlayıcılarının arabirimleri IReliableStateManager döndürülür.

Güvenilir durum yöneticisi eklenti mimarisi kullanır, böylece yeni tür güvenilir koleksiyonların dinamik olarak takılı.

Güvenilir sözlük ve güvenilir sıra yüksek performanslı, sürümlü bir fark mağaza uygulaması üzerinde oluşturulmuştur.

### <a name="transactional-replicator"></a>İşlem çoğaltması
İşlem çoğaltması bileşen hizmetinin (diğer bir deyişle, güvenilir durum Yöneticisi'ni ve güvenilir koleksiyonları içinde durumunu) durumunu hizmetini çalıştıran tüm çoğaltmalar arasında tutarlı olmasını sağlamak için sorumludur. Ayrıca, durumu günlüğüne kalıcı olmasını sağlar. Özel bir mekanizma aracılığıyla işlem çoğaltması güvenilir durumu Yöneticisi arabirimleriyle.

İşlem çoğaltması, böylece tüm çoğaltmaları güncel durum bilgilerini hizmet örneği diğer yinelemelerle durumunu iletmek için bir ağ protokolü kullanır.

İşlem çoğaltması, böylece durum bilgisi işlemi devam eder veya düğüm çöküyor durum bilgilerini kalıcı hale getirmek için bir günlük kullanır. Günlük arabirimi özel bir mekanizmadır.

### <a name="log"></a>Günlük
Yazma işlemi için iyileştirilmiş bir yüksek performanslı kalıcı depoya günlük bileşeni sağlar dönen veya katı hal diskleri.  Günlük (yani, sabit diskler) kalıcı depolama için durum bilgisi olan hizmet çalışan düğümlerine yerel olarak tasarımdır. Bu, düşük gecikme ve düğüme yerel olmayan uzak kalıcı depolama ile karşılaştırıldığında yüksek verimlilik sağlar.

Günlük bileşeni, birden çok günlük dosyalarını kullanır. Tüm çoğaltmaları durumu verilerini depolamak için en düşük gecikme süreli ve yüksek verimlilik sağlayabilir olarak kullanan bir düğüm genelinde paylaşılan günlük dosyası yok. Varsayılan olarak Service Fabric düğümü çalışma dizininde paylaşılan günlük yerleştirilir ancak yalnızca paylaşılan günlüğü için ayrılmış bir disk üzerinde ideal olarak, başka bir konumda yerleştirilmesi için de yapılandırılabilir. Her çoğaltma hizmeti için de bir ayrılmış günlük dosyası vardır ve ayrılmış bir günlük hizmetin çalışma dizini içinde yerleştirilir. Farklı bir konumda yerleştirilmesi için ayrılmış bir günlük yapılandırmak için bir mekanizma yoktur.

Ayrılmış günlük dosyası olduğu kalıcı son hedefi olsa da paylaşılan günlük yinelemenin durumu bilgileri için geçici bir alandır. Bu tasarımda, durum bilgisi ilk paylaşılan günlük dosyasına yazılır ve arka planda ayrılmış bir günlük dosyasına gevşek taşındı. Bu şekilde, paylaşılan günlüğüne yazma ilerleme hızlandırmak hizmet veren yüksek verimlilik ve düşük gecikme süresi gerekir.

Okur ve paylaşılan günlüğe yazmaya ön tahsis paylaşılan günlük dosyası için disk alanı için doğrudan g/ç aracılığıyla yapılır. Ayrılmış günlükleriyle sürücüsünde disk alanı optimum kullanımına izin vermek için ayrılmış bir günlük dosyası NTFS seyrek dosya olarak oluşturulur. Bu disk alanının işleminin izin verir ve işletim sistemi gerçekte kullanılan daha çok fazla disk alanı kullanarak ayrılmış günlük dosyaları gösterecektir unutmayın.

Günlük için en az kullanıcı modu arabirimi yanı sıra, bir çekirdek modu sürücüsü olarak günlüğüne yazılır. Bir çekirdek modu sürücüsü olarak çalıştırarak günlük kullanan tüm hizmetler için en yüksek performans sağlar.

Günlük yapılandırma hakkında daha fazla bilgi için bkz: [durum bilgisi olan güvenilir hizmetler yapılandırma](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Durum bilgisiz güvenilir hizmeti
### <a name="architecture-of-a-stateless-service"></a>Durum bilgisi olmayan hizmetin mimarisi
![Durum bilgisiz hizmet mimarisi diyagramı](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Durum bilgisiz güvenilir hizmeti
Durum bilgisiz hizmet uygulamaları StatelessService veya StatelessServiceBase sınıfından türetilir. StatelessServiceBase sınıfı StatelessService sınıfı daha fazla esneklik sağlar.
Her iki temel sınıfları yaşam süresi ve bir hizmetin rolünü yönetin.

Hizmet uygulaması hizmet noktalarda hizmet yaşam döngüsü--yapmak için iş varsa veya bir iletişim dinleyici nesnesi oluşturmak isterse, her iki temel sınıfın sanal yöntemleri geçersiz kılabilir. Bu hizmet uygulaması bir iletişimi kullandıkça hizmet ICommunicationListener, yukarıdaki diyagramda gösterme kendi iletişim dinleyici nesnesi uygulayabilir rağmen iletişimi dinleyicisi Service Fabric tarafından uygulandığını unutmayın Service Fabric tarafından uygulanan dinleyicisi.

Bkz: [güvenilir hizmetine genel bakış](service-fabric-reliable-services-introduction.md) ve [güvenilir kullanım Gelişmiş Hizmet](service-fabric-reliable-services-advanced-usage.md) StatelessService ve StatelessServiceBase sınıflarını kullanarak Hizmetleri yazma özellikleri hakkında daha fazla bilgi için.

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
Service Fabric hakkında daha fazla bilgi için bkz:

[Güvenilir hizmetine genel bakış](service-fabric-reliable-services-introduction.md)

[Hızlı başlangıç](service-fabric-reliable-services-quick-start.md)

[Güvenilir koleksiyonları genel bakış](service-fabric-reliable-services-reliable-collections.md)

[Kullanım Gelişmiş güvenilir hizmeti](service-fabric-reliable-services-advanced-usage.md)

[Güvenilir hizmet yapılandırması](service-fabric-reliable-services-configuration.md)  

