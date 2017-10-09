---
title: aaaUnderstand Azure IOT Hub kotalar ve azaltma | Microsoft Docs
description: "Geliştirici Kılavuzu - tooIoT Hub ve hello uygulamak hello kotaları açıklaması azaltma davranışı bekleniyordu."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 425e1b08-8789-4377-85f7-c13131fae4ce
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 023fa29bfbfb1de35708d6d121a1c56b50adfed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-quotas-and-throttling"></a>Başvuru - IOT hub'ı kotalar ve azaltma

## <a name="quotas-and-throttling"></a>Kotalar ve azaltma
Her Azure aboneliğinin en fazla 10 IOT hub'ları ve en fazla 1 ücretsiz hub sahip olabilir.

Her IOT hub'ı belirli bir sayıda belirli bir SKU birimlerinde ile sağlanan (daha fazla bilgi için bkz: [Azure IOT Hub fiyatlandırma][lnk-pricing]). Merhaba SKU ve birim sayısını hello maksimum günlük kotası gönderebileceğiniz iletilerin belirler.

Merhaba SKU azaltma, tüm işlemler IOT hub'ı zorlayan sınırları hello de belirler.

## <a name="operation-throttles"></a>İşlem kısıtlamaları
İşlemi kısıtlamaları olan hello dakika aralıklardaki uygulanır ve olan oranı sınırlamaları tooavoid kötüye amaçlar. Mümkün olduğunda hataları döndürüyor tooavoid IOT hub'ı çalışır ancak hello kısıtlama çok uzun süre ihlal edilirse özel durumları döndüren başlatır.

Aşağıdaki tablo gösterir hello hello kısıtlamaları zorunlu. Değerleri tooan tek tek hub bakın.

| Kısıtlama | Ücretsiz ve S1 hub'ları | S2 hub'ları | S3 hub'ları | 
| -------- | ------- | ------- | ------- |
| Kimlik kayıt defteri işlemleri (oluşturma, alma, liste, Güncelleştir, Sil) | 1.67/sec/Unit (min/100/birim) | 1.67/sec/Unit (min/100/birim) | 83.33/sec/Unit (min/5000/birim) |
| Cihaz bağlantıları | En fazla 100/sn veya sn/12/birim <br/> Örneğin, iki S1 2 birimleridir\*12 = 24/sn, ancak en az 100/sn, birim üzerinde. Saniye başına 108 sahip dokuz S1 birimleriyle (9\*12), birim üzerinde. | 120/sn/birim | 6000/sn/birim |
| Cihazdan buluta gönderim | En fazla 100/sn veya sn/12/birim <br/> Örneğin, iki S1 2 birimleridir\*12 = 24/sn, ancak en az 100/sn, birim üzerinde. Saniye başına 108 sahip dokuz S1 birimleriyle (9\*12), birim üzerinde. | 120/sn/birim | 6000/sn/birim |
| Buluttan cihaza gönderim | 1.67/sec/Unit (min/100/birim) | 1.67/sec/Unit (min/100/birim) | 83.33/sec/Unit (min/5000/birim) |
| Buluttan cihaza alım <br/> (yalnızca cihaz HTTP kullandığında)| 16.67/sec/Unit (min/1000/birim) | 16.67/sec/Unit (min/1000/birim) | 833.33/sec/Unit (min/50000/birim) |
| Karşıya dosya yükleme | 1.67 dosya karşıya yükleme bildirimleri/sn/birim (min/100/birim) | 1.67 dosya karşıya yükleme bildirimleri/sn/birim (min/100/birim) | 83.33 dosya karşıya yükleme bildirimleri/sn/birim (min/5000/birim) |
| Doğrudan yöntemler | 20/sn/birim | 60/sn/birim | 3000/sn/birim | 
| Cihaz ikizi okumaları | 10/sn | Maksimum saniye başına 10 veya sn/1/birim | 50/sn/birim |
| Cihaz ikizi güncelleştirmeleri | 10/sn | Maksimum saniye başına 10 veya sn/1/birim | 50/sn/birim |
| İş işlemleri <br/> (oluşturma, güncelleştirme, listeleme, silme) | 1.67/sec/Unit (min/100/birim) | 1.67/sec/Unit (min/100/birim) | 83.33/sec/Unit (min/5000/birim) |
| İşler işlemleri için cihaz başına aktarım hızı | 10/sn | Maksimum saniye başına 10 veya sn/1/birim | 50/sn/birim |

Merhaba önemli tooclarify olan *cihaz bağlantılarını* kısıtlama yeni cihaz bağlantılarını kurulabileceği bir IOT hub ile Merhaba oranı yönetir. Merhaba *cihaz bağlantılarını* kısıtlama hello en fazla eş zamanlı cihaz sayısını belirleyen değil. Merhaba kısıtlama hello hello IOT hub için sağlanan birim sayısını bağlıdır.

Örneğin, tek bir S1 birim satın alırsanız, bir kısıtlama saniyede 100 bağlantısı alın. Bu nedenle, 100.000 cihaz tooconnect, en az 1000 saniye (yaklaşık 16 dakika) alır. Ancak, kimlik kayıt defterinizde kayıtlı cihazlara sahip sayıda eş zamanlı cihazı olabilir.

IOT hub'ı kapsamlı bir açıklama için davranış, azaltma blog yayınına bakın hello [IOT Hub'ın azaltma ve][lnk-throttle-blog].

> [!NOTE]
> İsteğe bağlı olarak belirli bir zamanda, olası tooincrease kotaları olduğu veya bir IOT hub'ındaki sağlanan birim hello sayısını artırarak sınırları azaltma.
> 
> [!IMPORTANT]
> Kimlik kayıt defteri işlemlerini aygıt yönetimi ve senaryoları sağlama çalışma zamanı kullanmak için tasarlanmıştır. Okunurken ya da çok sayıda cihaz kimliklerini güncelleştirilirken desteklenen aracılığıyla [içeri ve dışarı aktarma işleri][lnk-importexport].
> 
> 

## <a name="other-limits"></a>Diğer sınırları

IOT hub'ı diğer işlemsel sınırları uygular:

| İşlem | Sınır |
| --------- | ----- |
| Karşıya dosya yükleme URI'ler | 10000 SAS URI'ler çıkışı için bir depolama hesabı aynı anda olabilir. <br/> Tek seferde 10 SAS URI’si/cihaz çıkarılabilir. |
| İşler | İş Geçmişi too30 günleri korunur <br/> En fazla eşzamanlı iş olan 1 (ücretsiz ve S1, S2) (için 5, 10 (için S3). |
| Ek uç noktaları | SKU Ücretli hub 10 ek uç noktaları olabilir. Ücretsiz SKU hub'ları bir ek uç noktası olabilir. |
| İleti yönlendirme kuralları | SKU Ücretli hub 100 yönlendirme kuralları olabilir. Ücretsiz SKU hub beş yönlendirme kuralları olabilir. |
| Cihaz bulut Mesajlaşma | Maksimum ileti boyutu 256 KB |
| Bulut cihaz Mesajlaşma | Maksimum ileti boyutu 64 KB |
| Bulut cihaz Mesajlaşma | İletiler teslim için bekleyen maksimum 50'dir |

> [!NOTE]
> Şu anda, en fazla hello bağlanabilirsiniz aygıtların tooa tek IOT hub 500.000 olduğu. Bu sınır tooincrease istiyorsanız, ilgili kişi [Microsoft Support](https://azure.microsoft.com/support/options/).

## <a name="latency"></a>Gecikme süresi
IOT hub'ı tüm işlemleri için düşük gecikmeli tooprovide içindedir. Ancak, toonetwork koşullar ve diğer öngörülemeyen Etkenler, bir maksimum gecikme garanti edemez. Çözümünüzü tasarlarken, aşağıdakileri yapmalısınız:

* Tüm özelliklerinin hello maksimum gecikme hakkında herhangi bir IOT hub'ı işlem yapmaktan kaçının.
* IOT hub'hello Azure bölgesi en yakın tooyour cihazları sağlayın.
* Azure IOT kenar tooperform gecikme süresine duyarlı işlemleri hello aygıt ya da bir ağ geçidi Kapat toohello cihazı kullanmayı düşünün.

Birden çok IOT hub'ı birimleri, daha önce açıklandığı gibi azaltma etkiler, ancak herhangi bir ek gecikme avantajları veya garanti sağlamaz.
Beklenmeyen artar işlemi gecikme görürseniz, başvurun [Microsoft Support](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Sonraki adımlar
Bu IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:

* [IOT Hub uç noktaları][lnk-devguide-endpoints]
* [Cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgulama dili][lnk-devguide-query]
* [IOT Hub MQTT desteği][lnk-devguide-mqtt]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-throttle-blog]: https://azure.microsoft.com/blog/iot-hub-throttling-and-you/
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
