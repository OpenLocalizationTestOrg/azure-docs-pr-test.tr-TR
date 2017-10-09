---
title: "aaaGuidelines & Azure Service Fabric güvenilir koleksiyonlar için öneriler | Microsoft Docs"
description: "Kılavuzları ve önerileri Service Fabric güvenilir koleksiyonları kullanma"
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
ms.date: 5/3/2017
ms.author: mcoskun
ms.openlocfilehash: bcdbc9d013bc044e06c43761e7f515c7e4bf340c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-and-recommendations-for-reliable-collections-in-azure-service-fabric"></a>Kılavuzları ve önerileri Azure Service Fabric güvenilir koleksiyonlar için
Bu bölümde, durum Yöneticisi'ni güvenilir ve güvenilir koleksiyonları kullanma yönergeleri sağlar. Merhaba toohelp kullanıcılar ortak tehlikesinden hedeftir.

Merhaba yönergeleri hello şartlarını önekli basit öneriler olarak düzenlenir *yapmak*, *düşünün*, *kaçının* ve *sağlamadığı*.

* Okuma işlemleri tarafından döndürülen özel türde bir nesne değiştirmeyin (örneğin, `TryPeekAsync` veya `TryGetValueAsync`). Eşzamanlı koleksiyonları gibi güvenilir koleksiyonları başvuru toohello nesneleri ve bir kopyasını döndürür.
* Derin kopyalama hello değiştirmeden önce bir özel tür nesnesinin döndürülen yapın. Yapılar ve yerleşik türler geçişi değerli olduğundan, bunları derin bir kopyasında toodo gerekmez.
* Kullanmayın `TimeSpan.MaxValue` zaman aşımları için. Zaman aşımları kullanılan toodetect kilitlenmeleri olmalıdır.
* Bunu kabul edilen, iptal, atıldı veya oluşturulduktan sonra bir işlem kullanmayın.
* Numaralandırma oluşturulduğu hello işlem kapsamı dışında kullanmayın.
* Bir işlem içinde başka bir işlemdeki oluşturmayın `using` deyimi kilitlenmeleri neden.
* Emin olun, `IComparable<TKey>` uygulamasıdır doğru. Merhaba sistemi bağımlılık yararlanır `IComparable<TKey>` kontrol noktalarına ve satır birleştirmek için.
* Güncelleştirme kilidi bir amaç tooupdate bir öğesiyle okunurken kullanın, tooprevent kilitlenmelerin belirli bir sınıf.
* 80 Kbayt öğelerinizi (örneğin, TKey + güvenilir sözlüğü için TValue) halde tutmayı düşünün: küçük hello daha iyi. Bu, büyük nesne yığın kullanımı yanı sıra disk ve ağ g/ç gereksinimleri hello miktarını azaltır. Genellikle, yalnızca bir küçük değerinin bir parçası hello güncelleştirildiğinde yinelenen veri çoğaltmak azaltır. Yaygın şekilde tooachieve güvenilir sözlükte budur toobreak, satır toomultiple satır.
* Yedekleme kullanmayı düşünün ve işlevselliği toohave olağanüstü durum kurtarma geri yükleyin.
* Tek bir varlık işlemleri ve birden çok varlık işlemleri karıştırma önlemek (örneğin `GetCountAsync`, `CreateEnumerableAsync`) hello içinde aynı işlem toohello farklı yalıtım düzeylerinde son.
* InvalidOperationException işleyin. Kullanıcı işlemleri çeşitli nedenlerle hello sistem tarafından iptal. Örneğin, hello güvenilir durum Yöneticisi rolüne birincil dışında değiştirirken veya uzun süre çalışan işlem zaman hello işlem günlük kesilmesi engelliyor. Böyle durumlarda, kullanıcı kendi işlem zaten sonlandırıldı belirten InvalidOperationException alabilirsiniz. Varsayıldığında, hello işlem hello sonlandırılması hello kullanıcı tarafından istenen değil, en iyi şekilde toohandle bu özel durumun toodispose hello işlem hello iptal belirteci işaret (veya hello çoğaltma hello rolü değiştirildi varsa), onay ve aksi durumda Yeni işlem ve yeniden oluşturun.  

Göz önünde bazı şeyleri tookeep şunlardır:

* Merhaba varsayılan zaman aşımı değeri, tüm hello güvenilir koleksiyonu API'leri için dört saniyedir. Kullanıcıların çoğunun hello varsayılan zaman aşımı kullanmanız gerekir.
* Merhaba varsayılan iptal belirteci olan `CancellationToken.None` tüm güvenilir koleksiyonları API'lerde.
* anahtar türü parametre hello (*TKey*) güvenilir bir sözlük doğru uygulamalıdır için `GetHashCode()` ve `Equals()`. Anahtarları sabit olmalıdır.
* tooachieve hello güvenilir koleksiyonlar için yüksek kullanılabilirlik, her hizmetin en az bir hedef ve en küçük çoğaltma kümesi boyutu 3 olmalıdır.
* Merhaba ikincil okuma işlemleri kaydedilen çekirdek değildir sürümleri okuyabilirsiniz.
  Başka bir deyişle, tek bir ikincil okuma verilerinin sürümü yanlış progressed.
  Birincil okuma kararlı her zaman: hiçbir zaman false progressed.

### <a name="next-steps"></a>Sonraki adımlar
* [Güvenilir Koleksiyonlar ile çalışma](service-fabric-work-with-reliable-collections.md)
* [İşlemler ve kilitleri](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Güvenilir durum Yöneticisi'ni ve koleksiyon dahili bileşenleri](service-fabric-reliable-services-reliable-collections-internals.md)
* Veri Yönetimi
  * [Yedekleme ve Geri Yükleme](service-fabric-reliable-services-backup-restore.md)
  * [Bildirimler](service-fabric-reliable-services-notifications.md)
  * [Seri hale getirme ve yükseltme](service-fabric-application-upgrade-data-serialization.md)
  * [Güvenilir durum Yöneticisi yapılandırması](service-fabric-reliable-services-configuration.md)
* Diğer
  * [Güvenilir hizmetler hızlı başlangıç](service-fabric-reliable-services-quick-start.md)
  * [Güvenilir koleksiyonlar için Geliştirici Başvurusu](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
