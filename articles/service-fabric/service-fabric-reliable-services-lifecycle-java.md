---
title: "Azure Service Fabric güvenilir hizmetlerini hello yaşam döngüsünün aaaOverview | Microsoft Docs"
description: "Service Fabric güvenilir hizmetler hello farklı yaşam döngüsü olayları hakkında bilgi edinin"
services: Service-Fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: pakunapa;
ms.openlocfilehash: 6d48c217d12bc5248c2da57b544aac747cecd872
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

* Başlatma sırasında
  * Hizmetleri oluşturulur
  * Bir fırsat tooconstruct olması ve sıfır veya daha fazla dinleyicileri Döndür
  * Merhaba hizmeti ile iletişimi sağlayan tüm döndürülen dinleyiciler açıldı
  * Merhaba hizmetin runAsync yöntemi çağrılır, hizmet toodo uzun süredir çalışıp hello erişime izin verme veya iş arka plan
* Kapatma sırasında
  * Merhaba iptal belirteci geçirilen toorunAsync iptal edilir ve hello dinleyicileri kapalı
  * Bu işlem tamamlandıktan sonra destructed hello hizmeti nesnesinin kendisi

Bu olaylar sıralama tam hello ayrıntılarla vardır. Özellikle, olayların hello sırası biraz hello güvenilir hizmet Stateless veya durum bilgisi olan olmasına bağlı olarak değişebilir. Ayrıca, durum bilgisi olan hizmetler için toodeal hello birincil takas senaryo ile sahibiz. Bu dizisi sırasında birincil hello rolü aktarılan tooanother çoğaltma (veya geri gelir) olmadan hello hizmet kapatılıyor. Son olarak, hata veya hata durumları hakkında toothink sahip.

## <a name="stateless-service-startup"></a>Durum bilgisiz hizmetini başlatma
bir durum bilgisi olmayan hizmetin Hello yaşam döngüsü oldukça basittir. Olayların hello sırası şöyledir:

1. Merhaba hizmet oluşturulur
2. Ardından paralel iki şey olur:
    - `StatelessService.createServiceInstanceListeners()`çağrılan tüm döndürülen dinleyiciler açıldığı (`CommunicationListener.openAsync()` her dinleyici adı verilir)
    - hizmetin runAsync yöntemi hello (`StatelessService.runAsync()`) olarak adlandırılır
3. Varsa, hello hizmetin kendi onOpenAsync yöntemi çağrılır (özellikle, `StatelessService.onOpenAsync()` olarak adlandırılır. Seyrek bir geçersiz kılma budur ancak kullanılabilir).

Merhaba çağrıları toocreate ve açık hello dinleyicileri ve runAsync arasında sıralamaya olduğu önemli toonote olur. runAsync başlatılmadan önce hello dinleyicileri açılabilir. Benzer şekilde, runAsync hello iletişim dinleyicileri açık veya hatta oluşturulan önce çağrılan bitirebilirsiniz. Herhangi bir eşitleme gerekiyorsa, bir alıştırma toohello uygulayan kalır. Yaygın çözümleri:

* Bazen diğer bazı bilgiler oluşturulur veya çalışma kadar dinleyicileri çalışamaz. İş genellikle hello hizmetin oluşturucuda hello sırasında yapılabilir durum bilgisi olmayan hizmetler için `createServiceInstanceListeners()` çağrısı, veya hello dinleyicisi kendisini hello yapımı bir parçası olarak.
* Merhaba dinleyicileri açık kadar bazen hello runAsync kodda toostart istemiyor. Bu durumda ek koordinasyon gereklidir. Bir ortak Yöneticiler, tooactual iş devam etmeden önce runAsync denetleneceği tamamladığınızda belirten hello dinleyicileri içinde bazı bayrağı çözümüdür.

## <a name="stateless-service-shutdown"></a>Durum bilgisiz hizmet kapanması
Durum bilgisi olmayan bir hizmeti kapatılıyor, hello aynı düzeni, yalnızca geriye doğru izlenir:

1. Paralel olarak
    - Tüm açık dinleyiciler kapalı (`CommunicationListener.closeAsync()` her dinleyici adı verilir)
    - Merhaba iptal belirteci geçirilen çok`runAsync()` iptal edildi (Merhaba iptal belirtecin denetimi `isCancelled` özelliği true döndürür ve hello belirtecin çağrıldıklarında `throwIfCancellationRequested` yöntemi atar bir `CancellationException`)
2. Bir kez `closeAsync()` her Dinleyicide tamamlandıktan ve `runAsync()` tamamlandıktan ayrıca hello hizmetin `StatelessService.onCloseAsync()` yöntemi çağrıldığında, varsa (yeniden seyrek bir geçersiz kılma budur).
3. Sonra `StatelessService.onCloseAsync()` tamamlandıktan hello hizmet nesnesi destructed

## <a name="notes-on-service-lifecycle"></a>Hizmet yaşam döngüsü ile ilgili notlar
* Her iki hello `runAsync()` yöntemi ve hello `createServiceInstanceListeners` çağrıları isteğe bağlıdır. Bir hizmeti bunları, her ikisini birden veya hiçbiri olabilir. Örneğin, hello hizmet yanıt toouser çağrıları tüm işlerini varsa, gerek yoktur, için tooimplement `runAsync()`. Yalnızca hello iletişim dinleyicileri ve bunların ilişkili kodu gereklidir. Benzer şekilde, oluşturma ve iletişim dinleyicileri döndürme hello hizmeti yalnızca toodo iş arka plan seçilmiş olabilir isteğe bağlıdır ve yalnızca tooimplement bekliyor`runAsync()`
* Hizmet toocomplete için geçerli `runAsync()` başarıyla ve dönüş almaktır. Bu bir hata durumu olarak kabul edilmez ve hizmet hello tamamlama hello arka plan iş temsil eder. Durum bilgisi olan güvenilir hizmetler için `runAsync()` hello hizmet birincil sunucudan indirgendi ve geri tooprimary yükseltilmiş yeniden çağrılması.
* Gelen bir hizmet bulunup bulunmadığını `runAsync()` bazı beklenmeyen bir özel durum atma tarafından bu bir hatadır ve hello hizmet nesnesi kapatmak ve bir sistem durumu hatası bildirdi.
* Varken hiçbir zaman sınırı bu yöntemlerden döndürme, hemen hello özelliği toowrite kaybeder ve bu nedenle herhangi bir gerçek iş tamamlayamıyor. Merhaba iptal isteği aldıktan sonra hızlı bir şekilde olabildiğince dönüş önerilir. Hizmetiniz bir makul sürede Service Fabric zorla olabilir toothese API çağrıları yanıt vermezse, hizmetiniz sonlanır. Genellikle yalnızca uygulama yükseltmelerini ya da hizmet zaman siliniyor sırasında meydana gelir. Bu zaman aşımı, varsayılan değer 15 dakikadır.
* Merhaba hatalarına `onCloseAsync()` yolu sonucunda `onAbort()` hello için bir son olasılığı en yüksek çaba fırsat olduğu çağrılan hizmet tooclean yukarı ve talep tüm kaynakları serbest bırakmak.

> [!NOTE]
> Durum bilgisi olan güvenilir hizmetler Java'da henüz desteklenmiyor.
>
>

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooReliable Hizmetleri](service-fabric-reliable-services-introduction.md)
* [Güvenilir hizmetler hızlı başlangıç](service-fabric-reliable-services-quick-start.md)
* [Kullanım Gelişmiş güvenilir hizmetler](service-fabric-reliable-services-advanced-usage.md)
