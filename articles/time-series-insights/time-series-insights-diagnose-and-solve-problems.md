---
title: "aaaDiagnose ve sorunları çözme | Microsoft Docs"
description: "Bu öğretici kapsayan nasıl toodiagnose ve zaman serisi Öngörüler ortamınızdaki sorunları"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a>Zaman serisi Öngörüler ortamınızdaki sorunları tanılamada ve

## <a name="i-dont-see-my-data"></a>Verilerimi görmüyorum
Neden değil görebilirsiniz verilerinizi ortamınızdaki hello bazı nedenler şunlardır [Azure zaman serisi Insights portalında](https://insights.timeseries.azure.com).

### <a name="your-event-source-doesnt-have-data-in-json-format"></a>Olay kaynağı JSON biçiminde veri yok
Azure zaman serisi Öngörüler yalnızca JSON verilerini bugün destekler. JSON örnekler için bkz: [desteklenen JSON şekiller](time-series-insights-send-events.md#supported-json-shapes).

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a>Olay kaynağı kaydolurken hello gerekli izne sahip hello anahtar sağlamadı
* Bir IOT hub için ihtiyacınız olan tooprovide hello anahtar **service bağlanma** izni.

   ![IOT hub hizmeti connect izni](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   Görüntü, önceki hello gösterildiği gibi hello ilkeleri birini **iothubowner** ve **hizmet** çalışır, her ikisi de olduğundan **hizmetine bağlanın** izni.
* Bir event hub için ihtiyacınız olan tooprovide hello anahtar **dinleme** izni.

   ![Olay hub'ı dinleme izni](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   Görüntü, önceki hello gösterildiği gibi hello ilkeleri birini **okuma** ve **yönetmek** çalışır, her ikisi de olduğundan **dinleme** izni.

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a>Merhaba tüketici grubu değil özel tooTime serisi Öngörüler sağlanır
IOT hub'ı veya bir olay hub'ı için kayıt sırasında verilerinizi okumak için kullanılması gereken toospecify hello tüketici grubu isteriz. Bu bir tüketici grubundaki paylaşılmayan gerekir. Paylaşılıyorsa, hello temel olay hub'ı otomatik olarak hello okuyucular birini rastgele bağlantısını keser.

## <a name="i-see-my-data-but-theres-a-lag"></a>Verilerimi bakın, ancak bir gecikme yok
Neden görebilirsiniz kısmi veri ortamınızdaki hello nedenleri [zaman serisi Insights portalında](https://insights.timeseries.azure.com).

### <a name="your-environment-is-getting-throttled"></a>Ortamınızı azaltıldı
Azaltma sınırından hello hello ortamı SKU türüne ve kapasite göre uygulanır. Tüm olay kaynakları hello ortamında bu kapasite paylaşır. IOT hub'ını veya olay hub'ı için Hello olay kaynağı veri zorlanan hello sınırları ötesinde itmesi olursa, azaltma ve bir gecikme bakın.

Diyagram aşağıdaki Merhaba, SKU S1 ve 3 kapasiteye sahip bir zaman serisi Öngörüler ortamı gösterilmektedir. Gün başına giriş 3 milyon olayları dağıtabilirsiniz.

![Ortam SKU geçerli kapasitesi](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

Bu ortam diyagramı aşağıdaki hello gösterilen hello giriş oranı ile event hub'ındaki iletileri alma varsayın:

![Bir olay hub'ına yönelik örnek giriş oranı](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

Merhaba diyagramda gösterildiği gibi hello günlük giriş ~ 67,000 iletileri hızıdır. Bu oran too46 iletileri dakikada kabaca çevirir. Her olay hub'ı ileti düzleştirilmiş tooa tek zaman serisi Öngörüler olay ise, bu ortam hiçbir azaltma görür. Ardından her olay hub'ı ileti düzleştirilmiş too100 zaman serisi Öngörüler olayları ise, 4,600 olayları dakikada alınan. Dakikada 3 kapasiteye sahip bir S1 SKU ortam için giriş yalnızca 2,100 olayları (1 milyon olay günde 3 birimlerde dakikada 700 olayları = dakikada 2,100 olayları =). Bu nedenle, bir gecikme gördüğünüz son toothrottling. 

Mantığı düzleştirme nasıl çalıştığını üst düzey anlamak için bkz [desteklenen JSON şekiller](time-series-insights-send-events.md#supported-json-shapes).

#### <a name="recommended-steps"></a>Önerilen adımlar
toofix hello gecikme, artış hello ortamınızın SKU kapasitesi. Daha fazla bilgi için bkz: [nasıl tooscale zaman serisi Öngörüler ortamınızı](time-series-insights-how-to-scale-your-environment.md).

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a>Geçmiş verileri dağıtmaya ve yavaş giriş neden
Varolan bir olay kaynağına bağlanıyorsanız, IOT hub'ını veya olay hub'ı zaten verilerin içinde olduğunu olasıdır. Bu nedenle hello ortamı hello olay kaynağının ileti saklama döneminin hello başından veri çekme başlatır. 

Bu davranış hello varsayılan davranıştır ve değiştirilemiyor. Azaltma gerçekleştirmesine ve biraz zaman alabilir geçmiş veri alma üzerinde toocatch ayarlama.

#### <a name="recommended-steps"></a>Önerilen adımlar
toofix hello gecikme, aşağıdaki adımları gerçekleştirin hello:
1. Merhaba SKU kapasitesi toohello maksimum izin verilen değer (Bu durumda 10) artırın. Merhaba kapasitesi artırılır sonra çok daha hızlı yakalama hello giriş işlemini başlatır. Ne kadar hızlı, hello kullanılabilirlik hello grafikte aracılığıyla yakalama görselleştirebilirsiniz [zaman serisi Insights portalında](https://insights.timeseries.azure.com). Merhaba artan kapasite için sizden ücret kesilir.
2. Merhaba öteleme yakalanan sonra hello SKU kapasitesi geri tooyour normal giriş oranı azaltın.

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a>My olay kaynağının *zaman damgası özelliği adı* ayarı çalışmıyor
Merhaba ad ve değer toohello kurallara uygun emin olun:
* Merhaba zaman damgası özelliği adı _büyük küçük harfe duyarlı_.
* Olay kaynağınız bir JSON dizesi olarak geldiği hello zaman damgası özelliği değeri hello biçimi olmalıdır _yyyy-MM-ddTHH. FFFFFFFK_. Bu tür bir dize örneğidir "2008-04-12T12:53Z".
