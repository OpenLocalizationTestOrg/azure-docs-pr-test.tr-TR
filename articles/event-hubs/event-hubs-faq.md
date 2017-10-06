---
title: "aaaAzure olay hub'ları ile ilgili SSS | Microsoft Docs"
description: "Azure Event Hubs sık sorulan sorular (SSS)"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: bfa10984-eb22-4671-861a-f377a90d9372
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm;shvija
ms.openlocfilehash: cc0844edcc38ad167cde9497d58d44155fc90b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-frequently-asked-questions"></a>Olay hub'ları sık sorulan sorular

## <a name="general"></a>Genel

### <a name="what-is-hello-difference-between-event-hubs-basic-and-standard-tiers"></a>Merhaba olay hub'ları temel ve standart katmanları arasındaki fark nedir?

Azure Event hubs Hello standart katmanı hello temel katmanında nelerin kullanılabildiğini ötesinde özellikler sunar. özellikler aşağıdaki hello standart eklenmiştir:
* Uzun olay saklama
* Aşma bir ücret dahil hello sayıdan daha fazla bilgi için ile ek aracılı bağlantılar
* Birden çok tek bir tüketici grubu
* [Yakalama](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)

Fiyatlandırma katmanlarına, olay hub'ları ayrılmış, dahil olmak üzere hakkında daha fazla bilgi için bkz: Merhaba [olay hub'ın fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="what-are-event-hubs-throughput-units"></a>Event Hubs işleme birimleri nelerdir?

Açıkça Event Hubs işleme birimleri, hello Azure portal aracılığıyla ya da olay hub'ları Resource Manager şablonları seçin. Üretilen iş birimleri tooall olay hub'ları olay hub'ları ad alanındaki uygulayın ve her işleme birimi özellikleri aşağıdaki hello ad alanı toohello hakkı verir:

* Giriş olayları (olayları bir event hub'ına gönderilen), ancak hiçbir 1000'den fazla giriş olayları, yönetim işlemlerini veya denetim saniyede too1 MB yukarı saniyede API'sini çağırır.
* Too2 MB (olayları bir event hub'ından tüketilen) çıkış olayların saniye başına.
* Too84 GB olay depolama (Merhaba varsayılan 24 saatlik saklama dönemi için yeterli).

Olay hub'ları işleme birimleri saat başı hello maksimum saat verilen hello sırasında seçilen birim sayısı göre faturalandırılır.

### <a name="how-are-event-hubs-throughput-unit-limits-enforced"></a>Event Hubs işleme birimi sınırları nasıl uygulanır?
Merhaba toplam giriş işleme veya bir ad alanındaki tüm event hubs arasında hello toplam giriş olay hızı hello toplam verimlilik birim kesintileri aşarsa Gönderenler kısıtlanan ve o hello giriş kotası aşıldı gösteren hatalar alabilirsiniz.

Hello toplam çıkış işleme veya bir ad alanındaki tüm event hubs arasında hello toplam olay çıkış hızı hello toplam verimlilik birim kesintileri aşarsa, alıcılar kısıtlanan ve o hello çıkış kotası aşıldı gösteren hatalar alabilirsiniz. Giriş ve çıkış kotaları ayrı olarak, böylece hiçbir göndereni aşağı olay tüketimi tooslow neden olabilir ya da bir alıcı olayları bir event hub'ına gönderilen engelleyebilirsiniz uygulanır.

### <a name="is-there-a-limit-on-hello-number-of-throughput-units-that-can-be-selected"></a>Seçilebilir üretilen iş birimleri hello sayısına bir sınır var mıdır?
Varsayılan kota ad alanı başına 20 işleme birimidir yoktur. Bir destek bileti dosyalama tarafından üretilen iş birimleri büyük kotası isteyebilir. Merhaba 20 işleme birimi sınırı aşan, paketleri 20 ve 100 üretilen iş birimleri içinde kullanılabilir. 20'den fazla üretilen iş birimleri kullanılarak hello özelliği toochange hello işleme birimlerinin sayısı bir destek bileti dosyalama olmadan kaldırdığını unutmayın.

### <a name="can-i-use-a-single-amqp-connection-toosend-and-receive-from-multiple-event-hubs"></a>I tek bir AMQP bağlantı toosend kullanabilir ve birden çok olay hub'larından alıyorsunuz?
Evet tüm hello olay hub'ları hello olduğu sürece, aynı ad.

### <a name="what-is-hello-maximum-retention-period-for-events"></a>Olaylar için başlangıç maksimum bekletme süresi nedir?
Olay hub'ları standart katmanı, şu anda maksimum Bekletme dönemi 7 gün destekler. Olay hub'ları kalıcı veri deposu olarak amaçlanmamıştır unutmayın. Bekletme süreleri 24 saatte bir olay akışı içine uygun tooreplay olduğu senaryolar için tasarlanmıştır büyük aynı sistemleri hello; Örneğin, tootrain veya yeni bir makine öğrenimi modeline var olan verileri doğrulayın. 7 gün dışında tutma iletisi varsa, etkinleştirme [olay hub'ları yakalama](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview) üzerinde olay hub'ı hello verileri olay hub'ı toohello depolama hesabı veya seçtiğiniz Azure Data Lake Service hesabı çeker. Yakalama etkinleştirme, satın alınan işleme birimine dayalı bir ücret doğurur.

### <a name="where-is-azure-event-hubs-available"></a>Burada Azure Event Hubs var mı?
Azure Event Hubs tüm desteklenen Azure bölgelerde kullanılabilir. Merhaba listesi için ziyaret [Azure bölgeleri](https://azure.microsoft.com/regions/) sayfası.  

## <a name="best-practices"></a>En iyi uygulamalar

### <a name="how-many-partitions-do-i-need"></a>Kaç tane bölümleri ihtiyacım var mı?
Lütfen bir olay hub'ındaki bölüm sayısı hello unutmayın Kurulumdan sonra değiştirilemez. İle unutmayın, bu başlamadan önce gereken kaç bölümleri ile ilgili önemli toothink olmasıdır. 

Olay hub'ları tasarlanmış tooallow tüketici grubu başına tek bir bölüm okuyucusu olur. Çoğu kullanım durumlarında hello varsayılan ayarı olan dört bölüm yeterli olur. Olay işleme tooscale arıyorsanız, ek bölümler ekleme tooconsider isteyebilirsiniz. Belirli üretilen iş sınırı yoktur bir bölüme ancak hello toplam verimlilik, ad alanında hello üretilen iş birimleri sayısıyla sınırlıdır. Ad alanınız içinde üretilen iş birimleri hello sayısı arttıkça, ek bölümler tooallow eşzamanlı okuyucu tooachieve kendi en yüksek verimlilik isteyebilirsiniz.

Uygulamanızı bir benzeşim tooa belirli bölümü olan bir model varsa, ancak bölümleri hello sayısını artırmayı herhangi bir avantajı tooyou olabilir. Bu konu hakkında daha fazla bilgi için bkz: [kullanılabilirlik ve tutarlılık](event-hubs-availability-and-consistency.md).

## <a name="pricing"></a>Fiyatlandırma

### <a name="where-can-i-find-more-pricing-information"></a>Daha fazla fiyatlandırma bilgileri nereden bulabilirim?
Event Hubs fiyatlandırması hakkında tam bilgi için bkz: Merhaba [olay hub'ın fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="is-there-a-charge-for-retaining-event-hubs-events-for-more-than-24-hours"></a>Olay hub'ları olayları 24 saatten fazla koruma için bir ücret var mı?
Merhaba olay hub'ları standart katmanı ileti bekletme dönemleri en fazla 7 gün 24 saatten uzun izin vermiyor. Saklı olayların toplam sayısı hello Hello boyutunu hello depolama indirimi seçili üretilen iş birimleri (işleme birimi başına 84 GB), hello sayısını aşarsa, hello indirimi aşıyor hello boyutu en doludur hello yayımlanan Azure Blob Depolama oranı. Merhaba işleme birimi toohello maksimum giriş indirimi Kurulumu kullanılsa bile hello depolama indirimi her işleme birimi olarak tüm depolama maliyetleri için bekletme süreleri 24 saatlik (Merhaba varsayılan) kapsar.

### <a name="how-is-hello-event-hubs-storage-size-calculated-and-charged"></a>Nasıl hello olay hub'ları depolama boyutu hesaplanan ücret ve nedir?
Tüm event hubs olay üstbilgileri veya disk depolama yapılarına iç herhangi ek yük dahil olmak üzere tüm saklı olayların toplam boyutu Hello hello gün boyunca ölçülür. Merhaba gün Hello sonunda hello en yüksek depolama boyutu hesaplanır. Merhaba günlük depolama indirimi (her işleme birimi 84 GB bir indirimi sağlayan) hello günde seçilmedi işleme birimleri en az sayıda hello temel alınarak hesaplanır. Merhaba toplam boyutu aşarsa hello hesaplanan günlük depolama indirimi, hello aşırı depolama faturalandırılır Azure Blob Depolama fiyatlarına kullanarak (Merhaba adresindeki **yerel olarak yedekli depolama** hızı).

### <a name="how-are-event-hubs-ingress-events-calculated"></a>Olay hub'ları giriş olayları nasıl hesaplanır?
Her olay tooan olay hub'ı Faturalanabilir bir ileti sayar gönderdi. Bir *giriş olay* küçük veya buna eşit olan verileri bir birim olarak tanımlanan too64 KB. Küçük veya ona eşit herhangi bir olay boyutu too64 KB toobe bir Faturalanabilir olay olarak kabul edilir. Merhaba olay 64 KB'den büyükse hello Faturalanabilir olayların sayısının toohello olay boyutu 64 KB'ün katları göre hesaplanır. Örneğin, olay hub'ı toohello gönderilen bir 8 KB olay bir olay olarak faturalandırılır ancak toohello olay hub'ı gönderilen bir 96 KB ileti iki olayları olarak faturalandırılır.

Yönetim işlemlerini ve denetim çağrıları kontrol noktaları gibi iyi Faturalanabilir giriş olayları sayılmaz, ancak toohello işleme birimi indirimi Kurulumu tahakkuk gibi bir olay hub'dan tüketilen olaylar.

### <a name="do-brokered-connection-charges-apply-tooevent-hubs"></a>Aracılı bağlantı ücretleri tooEvent hub uygulanır?
Yalnızca hello AMQP Protokolü kullanıldığında bağlantı ücretleri uygulanır. Merhaba sayısı sistemleri veya aygıtları gönderme bağımsız olarak HTTP kullanarak olayları göndermek için bağlantı harcamanız yok. Toouse AMQP planlıyorsanız (örneğin, tooachieve daha verimli olay akış veya tooenable çift yönlü iletişim IOT komut ve denetim senaryolarda), hello bkz [olay hub'ın fiyatlandırma bilgileri](https://azure.microsoft.com/pricing/details/event-hubs/) sayfa hakkında ayrıntılar için çok sayıda bağlantısı her hizmet katmanında dahil edilir.

### <a name="how-is-event-hubs-capture-billed"></a>Event Hubs Yakalama nasıl faturalandırılır?
Yakalama hello ad alanındaki tüm event hub'hello yakalama seçeneği etkin olduğunda etkindir. Olay hub'ları yakalama satın alınan işleme birimi saatlik faturalandırılır. Merhaba işleme birimi sayısı artırılabilir veya azaltılabilir gibi olay hub'ları yakalama faturalama tüm saat halinde bu değişiklikleri yansıtır. Olay hub'ları yakalama faturalama hakkında daha fazla bilgi için bkz: [olay hub'ın fiyatlandırma bilgileri](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="will-i-be-billed-for-hello-storage-account-i-select-for-event-hubs-capture"></a>Olay hub'ları yakalama için seçtiğim hello depolama hesabı için faturalandırılmaya?
Yakalama bir olay hub'ına etkinleştirildiğinde sağlayan bir depolama hesabı kullanır. Depolama hesabınız olarak, bu yapılandırma için herhangi bir değişikliğe Faturalanan tooyour Azure aboneliği olup.

## <a name="quotas"></a>Kotalar

### <a name="are-there-any-quotas-associated-with-event-hubs"></a>Event Hubs ile ilişkili olan kotaları bulunur?
Tüm Event Hubs kotaları listesi için bkz: [kotaları](event-hubs-quotas.md).

## <a name="troubleshooting"></a>Sorun giderme

### <a name="what-are-some-of-hello-exceptions-generated-by-event-hubs-and-their-suggested-actions"></a>Olay hub'ları ve bunların önerilen eylemleri tarafından oluşturulan hello özel durumlar bazıları nelerdir?
Olası olay hub'ları özel durumlar listesi için bkz: [özel durumlar genel bakış](event-hubs-messaging-exceptions.md).

### <a name="diagnostic-logs"></a>Tanılama günlükleri
İki tür olay hub'ları destekler [tanılama günlükleri](event-hubs-diagnostic-logs.md) -yakalama hata ve her ikisi de json'da temsil edilir ve aracılığıyla açılabilir işlem günlükleri - hello Azure portalı.

### <a name="support-and-sla"></a>Destek ve SLA
Olay hub'ları için teknik destek hello kullanılabilir [topluluk forumları](https://social.msdn.microsoft.com/forums/azure/home). Faturalandırma ve abonelik yönetimi desteği ücretsiz olarak sunulmaktadır.

toolearn bizim SLA hakkında daha fazla bilgi görmek hello [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/) sayfası.

## <a name="next-steps"></a>Sonraki adımlar
Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)
* [Olay Hub’ı oluşturma](event-hubs-create.md)
