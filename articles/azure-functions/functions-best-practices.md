---
title: "Azure işlevleri için aaaBest uygulamaları | Microsoft Docs"
description: "Azure işlevleri için en iyi yöntemler ve yaklaşımlar öğrenin."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, desenleri, en iyi uygulama, işlemler ve olay işleme, Web kancalarını, dinamik işlem, sunucusuz mimarisi"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a>Merhaba performansı ve güvenilirliği Azure işlevleri için en iyi duruma getirme

Bu makalede Kılavuzu tooimprove hello performansı ve güvenilirliği işlevi uygulamalarınızın sağlar. 


## <a name="avoid-long-running-functions"></a>İşlevler uzun süre çalışan kaçının

Büyük, uzun süre çalışan işlevler beklenmeyen zaman aşımı sorunlara neden olabilir. Bir işlev toomany Node.js bağımlılıkları büyüyebilir. Bağımlılıklar alma beklenmeyen zaman aşımlarına neden artan yükleme süreleri de neden olabilir. Bağımlılıklar her ikisi de açıkça ve örtülü olarak yüklenir. Kodunuz tarafından yüklenen tek bir modül ek modülleri yükleyebilir.  

Mümkün olduğunda, daha küçük işlevine düzenleme büyük işlevlerin o iş birlikte ayarlar ve yanıtları hızlı döndürür. Örneğin, bir Web kancası veya HTTP tetikleyicisi işlevi belirli bir süre içinde bir bildirim yanıt gerektirebilir; Web kancası toorequire hemen yanıt verilmesi için yaygın bir durumdur. Bir kuyruk tetikleyici işlev tarafından işlenen bir sıra toobe içine hello HTTP tetikleyicisi yükü geçirebilirsiniz. Bu yaklaşım toodefer hello gerçek iş sağlar ve hemen bir yanıt döndürür.


## <a name="cross-function-communication"></a>İşlev iletişimi arası

Birden çok işlevleri tümleştirdiğinizde, genellikle bir en iyi yöntem toouse depolama kuyruklarında işlevi iletişim çapraz içindir.  Merhaba ana nedeni olan depolama kuyrukları ucuz ve çok daha kolay tooprovision. 

Bir depolama kuyruğu tek bir ileti boyutu too64 sınırlı KB. İşlevler arasında daha büyük ileti toopass gerekiyorsa, bir Azure hizmet veri yolu kuyruğu kullanılan toosupport ileti boyutları too256 KB olabilir.

Service Bus konu başlıklarını ileti işleme önce filtreleme gerektiriyorsa yararlı olur.

Olay hub'ları yararlı toosupport yüksek hacimli iletişimleri ' dir.


## <a name="write-functions-toobe-stateless"></a>Durum bilgisiz işlevleri toobe yazma 

İşlevler durum bilgisiz ve mümkünse ıdempotent. Tüm gerekli durum bilgilerini verilerinizle ilişkilendirin. Örneğin, işlenmekte olan büyük olasılıkla sahip olabilir ilişkili bir sipariş `state` üyesi. Bir işlev hello işlevi kendisini durum bilgisiz devam ederken bu durumuna bağlı bir sipariş işlem gerçekleştirilemedi. 

Idempotent işlevleri ile Zamanlayıcı Tetikleyicileri özellikle önerilir. Kesinlikle günde bir kez çalıştırmanız gereken bir şey varsa, onu hello gün sırasında her zaman aynı sonuçları hello ile çalıştırabilmeniz için örneğin, okuma ve yazma. belirli bir gün için hiçbir iş olduğunda hello işlevi çıkabilirsiniz. Ayrıca bir önceki çalıştırma toocomplete başarısız olursa, sonraki çalıştırma hello kaldığı yerden yukarı seçmeniz gerekir.


## <a name="write-defensive-functions"></a>Savunma işlevler yazma

İşlevinizi dilediğiniz zaman bir özel durum karşılaşabileceği varsayalım. İşlevlerinizi hello özelliği toocontinue bir önceki başarısız noktasından ile Merhaba sonraki yürütme sırasında tasarlayın. Aşağıdaki eylemler hello gerektiren bir senaryo düşünün:

1. Bir db 10.000 satır için sorgu.
2. Bu satırlar tooprocess daha fazla hello satır aşağı her bir kuyruk iletisi oluşturun.
 
Nasıl karmaşık sisteminize bağlı olarak, size sahip olabilir: hatalı davranmakta söz konusu aşağı akış hizmetleriyle ağ kesintileri veya kota sınırları ulaşıldığında, vb.. Tüm bunların herhangi bir zamanda işlevinizi etkileyebilir. Bunun için hazırlanmış, işlevleri toobe toodesign gerekir.

İşleme kuyruğuna bu öğelerinin 5.000 ekledikten sonra bir hata oluşursa, kodunuzu nasıl tepki vermez? Öğeleri, tamamladığınız kümesindeki izler. Aksi takdirde, bunları yeniden başlattığınızda ekleyebilirsiniz. Bu, iş akışınızı üzerinde ciddi bir etkisi olabilir. 

Bir kuyruk öğesi zaten işlenmiş ise işlevi toobe Hayır op izin verir.

Hello Azure işlevleri platformunda kullandığınız bileşenleri için zaten sağlanan savunma önlemleri yararlanın. Örneğin, **zarar iletileri işleme** hello belgelerinde [Azure depolama kuyruğu tetikler](functions-bindings-storage-queue.md#trigger).
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a>Karışımı test ve üretim hello aynı kod olmayan işlev uygulaması

Bir işlev uygulaması işlevlerinde kaynakları paylaşır. Örneğin, bellek paylaşılır. Bir işlev uygulaması üretimde kullanıyorsanız, test ilgili işlevleri ve kaynakları tooit eklemeyin. Üretim kodu yürütme sırasında beklenmeyen yükünü neden olabilir.

Üretim işlevi uygulamalarınızda yük dikkatli olun. Bellek hello uygulamasında her işlev üzerinden ortalaması alınır.

Birden çok .net işlevlerde başvurulan paylaşılan bir derleme varsa, ortak bir paylaşılan klasöre yerleştirin. Örneğin aşağıdaki deyim benzer toohello hello derleme başvurusu: 

    #r "..\Shared\MyAssembly.dll". 

Aksi takdirde, kolay tooaccidentally birden çok test sürümleri arasında farklı şekilde davranan aynı ikili işlevleri hello dağıtın.

Ayrıntılı günlük üretim kodunda kullanmayın. Olumsuz bir etkisi vardır.



## <a name="use-async-code-but-avoid-blocking-calls"></a>Zaman uyumsuz kod kullanır ancak çağrıları engelleme kaçının

Zaman uyumsuz programlama önerilen en iyi uygulamadır. Bununla birlikte, her zaman hello başvuran kaçının `Result` özelliği veya arama `Wait` yöntemi bir `Task` örneği. Bu yaklaşım toothread Tükenme yol açabilir.


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için kaynakları aşağıdaki hello bakın:

Azure işlevleri Azure App Service kullandığından, ayrıca uygulama hizmeti yönergelerini farkında olmalıdır.
* [Patterns and Practices HTTP performans iyileştirmeleri](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

