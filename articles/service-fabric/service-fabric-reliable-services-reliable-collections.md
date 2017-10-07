---
title: "Azure Service Fabric durum bilgisi olan Hizmetleri'ndeki aaaIntroduction tooReliable koleksiyonları | Microsoft Docs"
description: "Service Fabric durum bilgisi olan hizmetler sağlayan güvenilir koleksiyonları toowrite yüksek oranda kullanılabilir, ölçeklenebilir ve düşük gecikme süreli bulut uygulamalarını sağlar."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>Azure Service Fabric durum bilgisi olan Hizmetleri'ndeki giriş tooReliable koleksiyonları
Tek bilgisayar uygulamaları yazıyordunuz gibi sorgulamanıza güvenilir koleksiyonları toowrite yüksek oranda kullanılabilir, ölçeklenebilir ve düşük gecikme süreli bulut uygulamaları etkinleştirir. Merhaba hello sınıflarda **Microsoft.ServiceFabric.Data.Collections** ad alanı, durumu otomatik olarak yüksek oranda kullanılabilir hale koleksiyonları kümesini sağlar. Geliştiriciler tooprogram yalnızca toohello güvenilir koleksiyonu API gerekir ve güvenilir hello kopyalanan ve yerel durumu yönetmek koleksiyonlar sağlayabilirsiniz.

Merhaba anahtar arasındaki güvenilir koleksiyonları ve diğer yüksek kullanılabilirlik teknolojiler (örneğin, Redis, Azure tablo hizmeti ve Azure kuyruk hizmeti) hello durumu yerel olarak hello hizmet örneği içinde de yüksek oranda kullanılabilir yapılan sırasında saklanacağını farktır. Bunun anlamı:

* Tüm okuma yerel, bunlar düşük gecikme sağlar ve yüksek verimlilik okur.
* İçinde düşük gecikme süresi sonuçları hello minimum sayısı ağ IOs, tüm yazma işlemlerini uygulanır ve yüksek verimlilik yazar.

![Koleksiyonları evrimi görüntüsü.](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

Güvenilir koleksiyonlar zorlayıcı hello doğal evrimi hello **System.Collections** sınıfları: yeni bir karmaşıklığını artırmadan hello Bulut ve birden çok bilgisayar uygulamaları için tasarlanmış koleksiyonları kümesi Merhaba Geliştirici. Bu nedenle, güvenilir koleksiyonları şunlardır:

* Çoğaltılmış: Durum değişiklikleri yüksek kullanılabilirlik için çoğaltılır.
* Kalıcı: Büyük ölçekli kesintileri (örneğin, bir veri merkezi güç kesintisi) karşı dayanıklılık için kalıcı toodisk verilerdir.
* Zaman uyumsuz: Zaman uyumsuz tooensure apı'leridir iş parçacığı GÇ yansıtılmasını zaman engellenmez.
* İşlem: bir hizmet içinde birden çok güvenilir koleksiyonları kolayca yönetilebilir API'leri hello soyutlama hareketlerinin kullanın.

Güvenilir koleksiyonları daha kolay uygulama durumu hakkında akıl hello kutusunu toomake dışında güçlü tutarlılık garanti sağlar.
Güçlü tutarlılık hello tüm işlem hello birincil dahil olmak üzere çoğaltmaları bir çoğunluğu çekirdek yalnızca oturum açılmış sonra işlemeleri son işlem sağlanarak elde edilir.
Hello zaman uyumsuz tamamlama döndürmeden önce tooachieve zayıf tutarlılık, geri toohello istemci/istek sahibi uygulamaları kabul.

Merhaba güvenilir koleksiyonları API'leri olan bir eş zamanlı koleksiyonları API'leri evrimi (hello bulunan **System.Collections.Concurrent** ad alanı):

* Zaman uyumsuz: eşzamanlı koleksiyonlarından farklı olarak hello işlemleri kalıcı ve çoğaltılmasını olduğundan, bir görev döndürür.
* Hayır out Parametreleri: kullanan `ConditionalValue<T>` tooreturn bool ve bir değer yerine out parametreleri. `ConditionalValue<T>`benzer `Nullable<T>` T toobe yapı gerektirmez, ancak.
* İşlemler: bir işlemde birden çok güvenilir koleksiyonlar üzerinde bir işlem nesnesi tooenable hello kullanıcı toogroup eylemlerini kullanır.

Bugün, **Microsoft.ServiceFabric.Data.Collections** üç koleksiyonları içerir:

* [Güvenilir sözlük](https://msdn.microsoft.com/library/azure/dn971511.aspx): anahtar/değer çiftlerinin çoğaltılmış, işlem ve zaman uyumsuz bir koleksiyonunu temsil eder. Benzer çok**ConcurrentDictionary**, hem de anahtar hello ve hello değeri, herhangi bir türde olabilir.
* [Güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx): bir çoğaltılmış, işlem ve zaman uyumsuz katı ilk çıkar (FIFO) sırayı temsil eder. Benzer çok**ConcurrentQueue**, hello değeri, herhangi bir türde olabilir.
* [Güvenilir eşzamanlı sıra](service-fabric-reliable-services-reliable-concurrent-queue.md): sıra yüksek verimlilik için sıralama çoğaltılmış, işlem ve zaman uyumsuz bir en iyi çaba temsil eder. Benzer toohello **ConcurrentQueue**, hello değeri, herhangi bir türde olabilir.

## <a name="next-steps"></a>Sonraki adımlar
* [Güvenilir koleksiyonu kılavuzları ve önerileri](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [Güvenilir Koleksiyonlar ile çalışma](service-fabric-work-with-reliable-collections.md)
* [İşlemler ve kilitleri](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Güvenilir durum Yöneticisi'ni ve koleksiyon dahili bileşenleri](service-fabric-reliable-services-reliable-collections-internals.md)
* Veri Yönetimi
  * [Yedekleme ve Geri Yükleme](service-fabric-reliable-services-backup-restore.md)
  * [Bildirimler](service-fabric-reliable-services-notifications.md)
  * [Güvenilir Koleksiyonu serileştirme](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [Seri hale getirme ve yükseltme](service-fabric-application-upgrade-data-serialization.md)
  * [Güvenilir durum Yöneticisi yapılandırması](service-fabric-reliable-services-configuration.md)
* Diğer
  * [Güvenilir hizmetler hızlı başlangıç](service-fabric-reliable-services-quick-start.md)
  * [Güvenilir koleksiyonlar için Geliştirici Başvurusu](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
