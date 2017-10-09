---
title: "Azure Service Fabric güvenilir hizmetlerini hello yaşam döngüsünün aaaOverview | Microsoft Docs"
description: "Service Fabric güvenilir hizmetler hello farklı yaşam döngüsü olayları hakkında bilgi edinin"
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek;
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 0d75ed5ee7cda85ac9af6a02e160727277804a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Güvenilir hizmetler yaşam döngüsüne genel bakış
> [!div class="op_single_selector"]
> * [Windows üzerinde C#](service-fabric-reliable-services-lifecycle.md)
> * [Linux üzerinde Java](service-fabric-reliable-services-lifecycle-java.md)
>
>

Güvenilir hizmetler Hello yaşam döngüleri hakkında düşünürken, hello yaşam döngüsü hello temelleri hello en önemli olan. Genel olarak:

- Başlatma sırasında
  - Hizmetleri oluşturulur
  - Bir fırsat tooconstruct olması ve sıfır veya daha fazla dinleyicileri Döndür
  - Merhaba hizmeti ile iletişimi sağlayan tüm döndürülen dinleyiciler açıldı
  - yöntemi çağrıldığında, hello hizmetin RunAsync toodo uzun süredir çalışıp hizmet hello izin verme veya iş arka plan
- Kapatma sırasında
  - Merhaba iptal belirteci geçirilen tooRunAsync iptal edilir ve hello dinleyicileri kapalı
  - Bu işlem tamamlandıktan sonra destructed hello hizmeti nesnesinin kendisi

Bu olaylar sıralama tam hello ayrıntılarla vardır. Özellikle, olayların hello sırası biraz hello güvenilir hizmet Stateless veya durum bilgisi olan olmasına bağlı olarak değişebilir. Ayrıca, durum bilgisi olan hizmetler için toodeal hello birincil takas senaryo ile sahibiz. Bu dizisi sırasında birincil hello rolü aktarılan tooanother çoğaltma (veya geri gelir) olmadan hello hizmet kapatılıyor. Son olarak, hata veya hata durumları hakkında toothink sahip.

## <a name="stateless-service-startup"></a>Durum bilgisiz hizmetini başlatma
bir durum bilgisi olmayan hizmetin Hello yaşam döngüsü oldukça basittir. Olayların hello sırası şöyledir:

1. Merhaba hizmet oluşturulur
2. Ardından paralel iki şey olur:
    - `StatelessService.CreateServiceInstanceListeners()`çağrılır ve tüm döndürülen dinleyiciler açılır. `ICommunicationListener.OpenAsync()`Her Dinleyicide çağrılır
    - Merhaba hizmetin `StatelessService.RunAsync()` yöntemi çağrılır
3. Varsa, hizmetin hello `StatelessService.OnOpenAsync()` yöntemi çağrılır. Seyrek bir geçersiz kılma budur ancak kullanılabilir değildir.

Merhaba çağrıları toocreate ve açık hello dinleyicileri ve RunAsync arasında sıralamaya olduğu önemli toonote olur. RunAsync başlatılmadan önce hello dinleyicileri açılabilir. Benzer şekilde, RunAsync hello iletişim dinleyicileri açık veya hatta oluşturulan önce çağrılan bitirebilirsiniz. Herhangi bir eşitleme gerekiyorsa, bir alıştırma toohello uygulayan kalır. Yaygın çözümleri:

  - Bazen diğer bazı bilgiler oluşturulur veya çalışma kadar dinleyicileri çalışamaz. İş genellikle başka bir konumda gibi yapılabilir durum bilgisi olmayan hizmetler için: 
    - Merhaba hizmetin Oluşturucusu
    - Merhaba sırasında `CreateServiceInstanceListeners()` çağırın
    - Merhaba dinleyicisi kendisini hello yapımı bir parçası olarak
  - Merhaba dinleyicileri açık kadar bazen hello RunAsync kodda toostart istemiyor. Bu durumda ek koordinasyon gereklidir. Bir ortak bunlar tamamlandığında belirten hello dinleyicileri içinde bazı bayrağı çözümüdür. Bu bayrak, ardından tooactual iş devam etmeden önce RunAsync içinde denetlenir.

## <a name="stateless-service-shutdown"></a>Durum bilgisiz hizmet kapanması
Durum bilgisi olmayan bir hizmeti kapatılıyor, hello aynı düzeni, yalnızca geriye doğru izlenir:

1. Paralel olarak
    - Tüm açık dinleyiciler kapatılır. `ICommunicationListener.CloseAsync()`Her dinleyici adı verilir.
    - Merhaba iptal belirteci geçirilen çok`RunAsync()` iptal edilir. Denetimi hello iptal belirteci `IsCancellationRequested` özelliği true döndürür ve hello belirtecin çağrıldıklarında `ThrowIfCancellationRequested` yöntemi atar bir `OperationCanceledException`.
2. Bir kez `CloseAsync()` her Dinleyicide tamamlandıktan ve `RunAsync()` tamamlandıktan ayrıca hello hizmetin `StatelessService.OnCloseAsync()` yöntemi çağrıldığında, varsa. Seyrek toooverride olan `StatelessService.OnCloseAsync()`.
3. Sonra `StatelessService.OnCloseAsync()` tamamlandıktan hello hizmet nesnesi destructed

## <a name="stateful-service-startup"></a>Durum bilgisi olan hizmet başlatma
Durum bilgisi olan hizmetler birkaç değişikliklerle benzer bir desen toostateless Hizmetleri sahiptir. Bir durum bilgisi olan hizmet başlatılırken olayların hello sırası aşağıdaki gibidir:

1. Merhaba hizmet oluşturulur
2. `StatefulServiceBase.OnOpenAsync()`adı verilir. Bu uncommonly hello hizmetinde geçersiz kılındı.
3. Merhaba aşağıdaki paralel olarak olacaklar
    - `StatefulServiceBase.CreateServiceReplicaListeners()`çağrılır 
      - Merhaba service birincil ise tüm döndürülen dinleyicileri açılır. `ICommunicationListener.OpenAsync()`Her dinleyici adı verilir.
      - Merhaba service ikincil ise, yalnızca bu dinleyicileri olarak işaretlenmiş `ListenOnSecondary = true` açılır. İkincil üzerinde açık dinleyicileri sahip daha az yaygın bir durumdur.
    - Merhaba Hizmet şu anda bir birincil hello hizmetin ise hello `StatefulServiceBase.RunAsync()` yöntemi çağrılır
4. Tüm çoğaltma dinleyicisi'nın hello sonra `OpenAsync()` çağrılarını tamamlamak ve `RunAsync()` olarak adlandırılır, `StatefulServiceBase.OnChangeRoleAsync()` olarak adlandırılır. Bu uncommonly hello hizmetinde geçersiz kılındı.

Benzer şekilde toostateless Hizmetleri hangi hello dinleyicileri oluşturulur ve açılan hello sipariş arasında hiçbir düzenlemesi yoktur ve RunAsync zaman çağrılır. Düzenleme gerekiyorsa, hello çözümleri olan çok hello aynı. Bir ek söz konusu değildir: hello iletişim dinleyicileri ulaşan hello çağrılar bazı içinde tutulur Bilgi gerektirir söyleyin [güvenilir koleksiyonları](service-fabric-reliable-services-reliable-collections.md). Hello iletişim dinleyicileri açamadı. önce Hello güvenilir koleksiyonları okunabilir veya yazılabilir olduğundan ve RunAsync başlamadan önce bazı ek koordinasyon gereklidir. Merhaba basit ve en yaygın çözümü hello iletişim dinleyicileri tooreturn için istemci kullanır tooknow tooretry hello istek hello bazı hata kodudur.

## <a name="stateful-service-shutdown"></a>Durum bilgisi olan hizmet kapatma
Benzer şekilde tooStateless Hizmetleri hello yaşam döngüsü olayları kapatma sırasında aynı şekilde başlatılırken hello olsa da tersine. Durum bilgisi olan hizmet kapatılıyor hello aşağıdaki olaylar oluşur:

1. Paralel olarak
    - Tüm açık dinleyiciler kapatılır. `ICommunicationListener.CloseAsync()`Her dinleyici adı verilir.
    - Merhaba iptal belirteci geçirilen çok`RunAsync()` iptal edilir. Denetimi hello iptal belirteci `IsCancellationRequested` özelliği true döndürür ve hello belirtecin çağrıldıklarında `ThrowIfCancellationRequested` yöntemi atar bir `OperationCanceledException`.
2. Bir kez `CloseAsync()` her Dinleyicide tamamlandıktan ve `RunAsync()` tamamlandıktan ayrıca hello hizmetin `StatefulServiceBase.OnChangeRoleAsync()` olarak adlandırılır. (Bu uncommonly hello hizmetinde geçersiz kılınır.)
    - RunAsync için bekleyen toocomplete yalnızca bu hizmeti çoğaltma birincil ise gereklidir.
3. Bir kez hello `StatefulServiceBase.OnChangeRoleAsync()` yöntemi tamamlayan, hello `StatefulServiceBase.OnCloseAsync()` yöntemi çağrılır. Seyrek bir geçersiz kılma budur ancak kullanılabilir değildir.
3. Sonra `StatefulServiceBase.OnCloseAsync()` tamamlandıktan hello hizmet nesnesi destructed.

## <a name="stateful-service-primary-swaps"></a>Durum bilgisi olan hizmet birincil değiştirir
Durum bilgisi olan hizmet çalışırken, yalnızca hello durum bilgisi olan hizmet birincil çoğaltmalarının açılan kendi iletişim dinleyicileri ve adlı kendi RunAsync yöntemi vardır. İkincil oluşturulur ancak hiçbir sonraki çağrılar bakın. Durum bilgisi olan hizmet ancak çalışırken, hangi şu anda hello birincil çoğaltmadır değiştirebilirsiniz. Bu ne bir çoğaltma görebilirsiniz hello yaşam döngüsü olayları şartlarında anlama geliyor? Merhaba davranışı hello durum bilgisi olan çoğaltma görür hello çoğaltma veya indirgenir hello takas sırasında yükseltilmiş olmasından bağlıdır.

### <a name="for-hello-primary-being-demoted"></a>Merhaba indirgenen birincil
Service Fabric iletileri işleme Bu çoğaltma toostop gerekiyor ve yapmakta olduğu herhangi bir arka plan iş çıkın. Sonuç olarak, bu adım görünüyor benzer toowhen hello hizmet kapatılıyor. Hizmet değil veya destructed ikincil olarak kalır beri kapalı bu hello bir farktır. API'ler aşağıdaki hello çağrılır:

1. Paralel olarak
    - Tüm açık dinleyiciler kapatılır. `ICommunicationListener.CloseAsync()`Her dinleyici adı verilir.
    - Merhaba iptal belirteci geçirilen çok`RunAsync()` iptal edilir. Denetimi hello iptal belirteci `IsCancellationRequested` özelliği true döndürür ve hello belirtecin çağrıldıklarında `ThrowIfCancellationRequested` yöntemi atar bir `OperationCanceledException`.
2. Bir kez `CloseAsync()` her Dinleyicide tamamlandıktan ve `RunAsync()` tamamlandıktan ayrıca hello hizmetin `StatefulServiceBase.OnChangeRoleAsync()` olarak adlandırılır. Bu uncommonly hello hizmetinde geçersiz kılındı.

### <a name="for-hello-secondary-being-promoted"></a>Merhaba yükseltilmekte ikincil
Benzer şekilde, Service Fabric hello hat üzerinde iletiler için dinleme Bu çoğaltma toostart gerekiyor ve ilgili cares herhangi bir arka plan görevi başlatın. Sonuç olarak, benzer toowhen hello hizmeti oluşturulur, bu işlem görünüyor dışında hello yineleme kendisini zaten mevcut. API'ler aşağıdaki hello çağrılır:

1. Paralel olarak
    - `StatefulServiceBase.CreateServiceReplicaListeners()`çağrılır ve tüm döndürülen dinleyiciler açılır. `ICommunicationListener.OpenAsync()`Her dinleyici adı verilir.
    - Merhaba hizmetin `StatefulServiceBase.RunAsync()` yöntemi çağrılır
2. Tüm çoğaltma dinleyicisi'nın hello sonra `OpenAsync()` çağrılarını tamamlamak ve `RunAsync()` çağrıldı, `StatefulServiceBase.OnChangeRoleAsync()` olarak adlandırılır. Bu uncommonly hello hizmetinde geçersiz kılındı.

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>Durum bilgisi olan hizmet kapanması ve birincil indirgeme sırasında ortak sorunlar
Service Fabric değişiklikleri birincil bir durum bilgisi olan hizmet çeşitli nedenlerle hello. Merhaba en yaygın olan [küme dengelenmesi](service-fabric-cluster-resource-manager-balancing.md) ve [uygulama yükseltme](service-fabric-application-upgrade.md). Bu işlemleri sırasında (yanı sıra hello hizmeti silinmiş olup olmadığını göreceğiniz gibi normal hizmet kapatma sırasında), önemlidir, hello hizmet saygı hello `CancellationToken`. İptal düzgün bir şekilde işleyemez Hizmetleri birkaç sorunlarıyla karşılaşırsınız. Service Fabric hello Hizmetleri toostop için düzgün biçimde bekler özellikle, bu işlemlerin yavaş olur. Sonuç olarak bu zaman aşımı toofailed yükseltmeler sağlama ve geri alma olabilir. Hata toohonor hello iptal belirteci de neden olabilir imbalanced küme düğümleri etkin alır ancak hello Hizmetleri olamaz yeniden dengelenir uzun toomove sürdüğünü beri olduğundan bunları başka bir yerde. 

Merhaba hizmetler durum bilgisi olduğundan, ayrıca hello kullanıyorsanız büyük olasılıkla [güvenilir koleksiyonları](service-fabric-reliable-services-reliable-collections.md). Birincil indirgenir, Service Fabric içinde gerçekleşen hello ilk şey yazma erişimi toohello alttaki durumu iptal edilmediğini biridir. Bu tooa ikinci hello hizmet yaşam döngüsü etkileyebilir sorun kümesini sağlar. dönüş özel durumlar hello zamanlama ve hello çoğaltma olup taşındığı göre hello koleksiyonları veya kapat. Bu özel durumlar doğru yapılmalıdır. Service Fabric tarafından oluşturulan özel durumları kalan kalıcı [(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet) ve geçici [(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet) kategoriler. Kalıcı özel durumları günlüğe ve bazı yeniden deneme mantığına göre hello geçici özel durumlar denenen ancak oluşturulur.

Merhaba kullanımdan gelen hello özel durumları işleme `ReliableCollections` hizmet yaşam döngüsü olayları ile birlikte test etme ve güvenilir bir hizmeti doğrulanıyor önemli bir parçasıdır. Merhaba öneri her zaman yükseltme gerçekleştirilirken toorun hizmetinizi yük altında olduğu ve [chaos sınama](service-fabric-controlled-chaos.md) hiç tooproduction dağıtmadan önce. Bu temel adımları hizmetinizin doğru uygulanır ve yaşam döngüsü olayları doğru olarak işler sağlamaya yardımcı olur.


## <a name="notes-on-service-lifecycle"></a>Hizmet yaşam döngüsü ile ilgili notlar
  - Her iki hello `RunAsync()` yöntemi ve hello `CreateServiceReplicaListeners/CreateServiceInstanceListeners` çağrıları isteğe bağlıdır. Bir hizmeti bunları, her ikisini birden veya hiçbiri olabilir. Örneğin, hello hizmet yanıt toouser çağrıları tüm işlerini varsa, gerek yoktur, için tooimplement `RunAsync()`. Yalnızca hello iletişim dinleyicileri ve bunların ilişkili kodu gereklidir. Benzer şekilde, oluşturma ve iletişim dinleyicileri döndürme hello hizmeti yalnızca toodo iş arka plan seçilmiş olabilir isteğe bağlıdır ve yalnızca tooimplement bekliyor`RunAsync()`
  - Hizmet toocomplete için geçerli `RunAsync()` başarıyla ve dönüş almaktır. Tamamlanıyor bir hata durumu değil. Tamamlanıyor `RunAsync()` hello hizmetinin hello arka plan çalışması tamamlandı gösterir. Durum bilgisi olan güvenilir hizmetler için `RunAsync()` hello çoğaltma birincil tooSecondary indirgendi ve geri tooPrimary yükseltilmiş yeniden adlandırılır.
  - Gelen bir hizmet bulunup bulunmadığını `RunAsync()` bazı beklenmeyen bir özel durum atma tarafından bu bir hata oluşturduğunu. Merhaba hizmet nesnesi kapatılır ve bir sistem durumu hatası bildirdi.
  - Varken hiçbir zaman sınırı bu yöntemlerden döndürme, hemen hello özelliği toowrite tooReliable koleksiyonları kaybeder ve bu nedenle herhangi bir gerçek iş tamamlayamıyor. Merhaba iptal isteği aldıktan sonra hızlı bir şekilde olabildiğince dönüş önerilir. Hizmetiniz bir makul sürede Service Fabric zorla olabilir toothese API çağrıları yanıt vermezse, hizmetiniz sonlanır. Genellikle yalnızca uygulama yükseltmelerini ya da hizmet zaman siliniyor sırasında meydana gelir. Bu zaman aşımı, varsayılan değer 15 dakikadır.
  - Merhaba hatalarına `OnCloseAsync()` yolu sonucunda `OnAbort()` hello için bir son olasılığı en yüksek çaba fırsat olduğu çağrılan hizmet tooclean yukarı ve talep tüm kaynakları serbest bırakmak.

## <a name="next-steps"></a>Sonraki adımlar
- [Giriş tooReliable Hizmetleri](service-fabric-reliable-services-introduction.md)
- [Güvenilir hizmetler hızlı başlangıç](service-fabric-reliable-services-quick-start.md)
- [Kullanım Gelişmiş güvenilir hizmetler](service-fabric-reliable-services-advanced-usage.md)
