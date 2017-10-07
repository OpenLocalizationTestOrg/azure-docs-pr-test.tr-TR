---
title: "Fiyatlandırma ve faturalama aaaService Bus | Microsoft Docs"
description: "Hizmet veri yolu fiyatlandırma yapısına genel bakış."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7c45b112-e911-45ab-9203-a2e5abccd6e0
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/02/2017
ms.author: sethm
ms.openlocfilehash: 4d06fe015baba45fef04e198363447c5541d1724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-pricing-and-billing"></a>Service Bus fiyatlandırma ve faturalama
Hizmet veri yolu Basic'te sunulan standart, ve [Premium](service-bus-premium-messaging.md) katmanları. Oluşturduğunuz her Service Bus hizmeti ad alanı için bir hizmet katmanına seçebilir ve bu ad alanı içinde oluşturulan tüm varlıklar arasında bu katmanı seçimi uygular.

> [!NOTE]
> Merhaba geçerli hizmet veri yolu fiyatlandırma hakkında ayrıntılı bilgi için bkz: [Azure Service Bus fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/service-bus/)ve hello [Service Bus SSS](service-bus-faq.md#pricing).
>
>

Service Bus, kuyruklar ve konular/abonelikler için iki ölçümler aşağıdaki hello kullanır:

1. **Operations Mesajlaşma**: API çağrıları kuyruk veya konu başlığının/aboneliğinin hizmet uç noktalarına karşı olarak tanımlanır. Bu ölçüm, gönderilen veya kuyruklar ve konular/abonelikler için Faturalanabilir kullanımının hello birincil birim olarak alınan iletiler yerini alır.
2. **Aracılı bağlantı**: sıraları, konuları ve abonelikleri karşı belirli bir saatlik örnekleme süresi boyunca açık kalıcı bağlantılar hello en yüksek sayısı olarak tanımlanmış. Bu ölçüm, yalnızca içinde açabilirsiniz ek bağlantılar hello standart katmanında, geçerli olacaktır (daha önce bağlantıları konu/kuyruk/abonelik başına sınırlı too100 olan) bir nominal bağlantı başına ücret karşılığında.

Merhaba **standart** kuyruklar ve konular/abonelikler, birim tabanlı too80% hello en yüksek kullanım düzeyleri indirim sonuçta ile gerçekleştirilen işlemleri için derecelendirilmiş fiyatlandırma katmanı tanıtır. 10 aylık tooperform too12.5 milyon işlemleri hiçbir ek ücret ödemeden aylık yukarı sağlayan, bir standart katmanı temel ücret yoktur.

Merhaba **Premium** katmanı, böylece her müşterinin iş yükü yalıtımlı şekilde çalışır hello CPU ve bellek katmanında kaynak yalıtımına sağlar. Bu kaynak kapsayıcısı *mesajlaşma birimi* olarak adlandırılır. Her premium ad alanı, en az bir mesajlaşma birimi için ayrılmıştır. Her Service Bus Premium ad alanı için 1, 2 veya 4 mesajlaşma birimi satın alabilirsiniz. Tek iş yükü veya varlık birden çok Mesajlaşma birimine yayılabilir ve faturalandırma 24 saatlik veya günlük oran fiyatlarında içinde olsa da hello Mesajlaşma birimlerinin sayısı gerçekleştirilse değiştirilebilir. Merhaba, Service Bus tabanlı çözümünüz için tahmin edilebilir ve tekrarlanabilir bir performans sonucudur. Daha tahmin edilebilir ve kullanılabilir olmasının yanı sıra bu performans, daha hızlıdır.

Merhaba standart katmanı temel ücret aylık Azure abonelik başına yalnızca bir kez doludur unutmayın. Bu, tek bir standart katmanı Service Bus ad alanı oluşturduktan sonra mümkün toocreate olacağı anlamına gelir ek yansıtılmasını olmadan, aynı Azure abonelik altında istediğiniz sayıda ek standart ad alanları temel giderler.

Merhaba [Service Bus fiyatlandırma](https://azure.microsoft.com/pricing/details/service-bus/) tablo hello temel, standart ve Premium katmanlar arasında işlevsel farklılıklar hello özetler.

## <a name="messaging-operations"></a>Mesajlaşma işlemleri
Yeni fiyatlandırma modeli hello bir parçası olarak, kuyruklar ve konular/abonelikler için faturalama değiştiriyor. Bu varlıklar, ileti toobilling işlemi başına başına faturalama'den geçiş. Bir "işlem" tooany API çağrısı bir kuyruk veya konu başlığının/aboneliğinin hizmet uç noktası karşı yapılan başvuruyor. Bu, yönetim, gönderme ve alma ve oturum durumu işlemleri içerir.

| İşlem Türü | Açıklama |
| --- | --- |
| Yönetim |Oluşturma, okuma, güncelleştirme, Sil (CRUD) sıralar veya konuları/abonelikleri karşı. |
| Mesajlaşma |Sıralar veya konuları/abonelikleri ile ileti alma ve gönderme. |
| Oturum durumu |Alma veya bir kuyruk veya konu başlığının/aboneliğinin oturum durumunu ayarlama. |

Merhaba üzerinde listelenen hello fiyatlar maliyet Ayrıntılar için bkz [Service Bus fiyatlandırma](https://azure.microsoft.com/pricing/details/service-bus/) sayfası.

## <a name="brokered-connections"></a>Aracılı bağlantılar
*Aracılı bağlantı* çok sayıda "kalıcı olarak bağlı" Gönderenler/alıcılar sıralar, konuları ve abonelikleri karşı içeren müşteri kullanım desenlerini uyum sağlamak. Kalıcı olarak bağlı Gönderenler/alıcılar bir sıfır ile AMQP veya HTTP kullanarak bağlan o zaman aşımı (örneğin, HTTP uzun yoklama) alacak olan. HTTP göndericiler ile alıcılar hemen bir zaman aşımı ile aracılı bağlantılar oluşturmaz.

Bağlantı kotaları ve diğer hizmet sınırları için hello bkz [Service Bus kotaları](service-bus-quotas.md) makalesi.

Hello standart katmanı hello başına ad alanı aracılı bağlantı sınırını kaldırır ve birleşik aracılı bağlantı kullanım hello Azure aboneliği arasında sayar. Daha fazla bilgi için bkz: Merhaba [aracılı bağlantılar](https://azure.microsoft.com/pricing/details/service-bus/) tablo.

> [!NOTE]
> 1.000 aracılı bağlantılar hello standart Mesajlaşma katman (aracılığıyla hello temel ücret) dahil edilmiştir ve tüm kuyruklar, konular ve abonelikler hello ilişkili Azure abonelik içindeki arasında paylaşılabilir.
>
>

<br />

> [!NOTE]
> Faturalama hello yoğun eşzamanlı bağlantı sayısı temel alır ve her ay 744 saatleri saatlik dayalı eşit olarak bölünür.
>
>

| Premium Katman |
| --- |
| Aracılı bağlantılar hello Premium katmanındaki sizden ücret istenmese. |

Merhaba aracılı bağlantılar hakkında daha fazla bilgi için bkz: [SSS](#faq) bu konunun ilerleyen bölümlerinde.

## <a name="faq"></a>SSS

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a>Aracılı bağlantılar nelerdir ve nasıl ı kendileri için sizden ücret?
Aracılı bağlantı hello aşağıdakilerden biri olarak tanımlanır:

1. Bir istemci tooa hizmet veri yolu kuyruğu ya da konu başlığının/aboneliğinin bir AMQP bağlantısı.
2. Bir HTTP Service Bus konu ya da sıfırdan büyük bir alma zaman aşımı değerine sahip sıraya bir ileti tooreceive çağırın.

Hizmet veri yolu ücretleri hello yoğun hello aşan eşzamanlı aracılı bağlantı sayısı için dahil edilen sayısı (1.000 hello standart katmanındaki). Yükselmeleri 744 saat ay içinde bölünerek eşit olarak, bir saatlik olarak ölçülür ve aylık faturalama dönemi hello eklenen. Merhaba dahil edilen miktar (ayda 1000 aracılı bağlantılar) hello fatura dönemi için eşit oranda bölünmüş hello saatlik yükselmeleri hello toplamını karşı hello sonunda uygulanır.

Örneğin:

1. Her 10.000 cihaz tek bir AMQP bağlantısı üzerinden bağlanır ve hizmet veri yolu konusundan komutlarını alır. Merhaba aygıtları telemetri olayları tooan olay hub'ı gönderin. Tüm aygıtlar için 12 saat her gün bağlanıyorsanız, bağlantı ücretleri aşağıdaki hello Uygula (toplama tooany içindeki diğer Service Bus konu ücretleri): 10.000 bağlantıları * 12 saat * 31 gün / 744 = 5.000 aracılı bağlantılar. Merhaba aylık indirimi 1.000 aracılı bağlantı sonra 120 toplam aracılı bağlantı başına 0.03 hello hızında 4.000 aracılı bağlantılar için ücret.
2. 10.000 cihaz sıfır olmayan bir zaman aşımı belirten HTTP üzerinden Service Bus kuyruğuna iletileri alacak. Tüm aygıtlar için 12 saat her gün bağlanıyorsanız, bağlantı ücretleri aşağıdaki hello görürsünüz (toplama tooany içindeki diğer Service Bus ücretleri): 10.000 HTTP alan bağlantıları * gün başına 12 saat * 744 saatleri/31 gün = 5.000 aracılı bağlantılar.

### <a name="do-brokered-connection-charges-apply-tooqueues-and-topicssubscriptions"></a>Aracılı bağlantı tooqueues ve konuları/abonelikleri uygulanabilir?
Evet. Merhaba sayısı sistemleri veya aygıtları gönderme bağımsız olarak HTTP kullanarak olayları göndermek için bağlantı harcamanız yok. Olaylar bazen "uzun yoklama," olarak da adlandırılır sıfırdan büyük bir zaman aşımı kullanarak HTTP ile alma aracılı bağlantı ücretleri oluşturur. AMQP bağlantıları hello bağlantıları kullanılan toosend yükleniyor veya alma bağımsız olarak aracılı bağlantı ücretleri oluşturur. 100 aracılı bağlantılar ücretsiz olarak temel ad alanındaki izin verildiğini unutmayın. Bu ayrıca hello maksimum hello Azure aboneliğiniz için izin verilen aracılı bağlantı sayısıdır. Merhaba ilk 1.000 aracılı bağlantılar üzerinden Azure aboneliği standart tüm ad alanlarını (ötesinde hello temel ücret) Ekstra ücret ödemeden dahil edilir. Bu kesintileri yeterli toocover olduğundan çok sayıda hizmet Mesajlaşma senaryoları, aracılı bağlantı ücretlerinden genellikle yalnızca, çok sayıda istemci toouse AMQP veya HTTP uzun-yoklama düşünüyorsanız ilgili hale; Örneğin, tooachieve daha verimli olay akış veya etkinleştir çift yönlü iletişim sayıda cihaz veya uygulama örnekleri ile.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba Service Bus fiyatlandırma hakkında tam Ayrıntılar için bkz [Service Bus fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/service-bus/).
* Merhaba bkz [Service Bus SSS](service-bus-faq.md#pricing) fiyatlandırma ve faturalama Service bus hakkında bazı sık sık sorulan sorular için.

[Azure portal]: https://portal.azure.com
