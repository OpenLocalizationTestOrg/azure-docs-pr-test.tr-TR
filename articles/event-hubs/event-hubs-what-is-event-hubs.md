---
title: "aaaWhat Azure Event hubs ve neden kullanın | Microsoft Docs"
description: "Genel bakış ve giriş tooAzure Event Hubs - bulut ölçekli telemetri alım Web siteleri, uygulamalar ve cihazlar"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a>Event Hubs nedir?

Azure Event Hubs saniyede milyonlarca olay alıp işleyebilen, ölçeklenebilirlik yüzeyi yüksek bir veri akışı platformu ve olay alma hizmetidir. Event Hubs dağıtılan yazılımlar ve cihazlar tarafından oluşturulan olayları, verileri ve telemetrileri işleyebilir ve depolayabilir. Veri tooan olay hub'ı dönüştürülebilir ve herhangi bir gerçek zamanlı analiz sağlayıcısı veya toplu işlem/depolama bağdaştırıcısı kullanılarak saklanan gönderdi. Merhaba özelliği tooprovide ile [yayımlama-abonelik özellikleri](https://msdn.microsoft.com/library/aa560414.aspx) düşük gecikme ile ve büyük ölçekte olay hub'ları "on Rampa" Merhaba büyük veriler için görevi görür.

## <a name="why-use-event-hubs"></a>Event Hubs’ı neden kullanmalıyım?

Event Hubs olay ve telemetri işleme özellikler onu özellikle aşağıdaki durumlar için yararlı hale getirir:

* Uygulama izleme
* Kullanıcı deneyimi veya iş akışı işleme
* Nesnelerin İnterneti (IoT) senaryoları

Örneğin, Event Hubs mobil uygulamalarda davranış izleme, web gruplarından trafik bilgileri alma, konsol oyunlarında oyun içi olay yakalama veya sanayi makinelerinden ya da bağlı taşıtlardan telemetri verileri toplama olanağı sağlar.

## <a name="azure-event-hubs-overview"></a>Azure Event Hubs’a genel bakış

Merhaba olay hub'ın çözüm mimarilerinde oynadığı genel rol olan hello "ön adlandırılırlar kapı" bir olay ardışık düzeni için bir *olay yutucu*. Bir olay yutucu, bir bileşeni ya da olay yayımcıları ile olay tüketicileri toodecouple hello hello üretimini ilgili olayların olay akışının üretimini arasındaki bulunur service ' dir. Merhaba aşağıdaki şekilde bu mimari gösterilmektedir:

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

Event Hubs, ileti akışı işleme olanağı sağlar ancak geleneksel kurumsal mesajlaşmadan farklı özelliklere sahiptir. Event Hubs özellikleri, yüksek işleme ve olay işleme senaryoları üzerine inşa edilmiştir. Bu nedenle, Event Hubs farklıdır [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) Mesajlaşma ve bazı kullanılabilir hello özelliklerini uygulamıyor [Service Bus Mesajlaşma](/azure/service-bus-messaging/) konuları gibi varlıklar.

## <a name="event-hubs-features"></a>Event Hubs özellikleri

Olay hub'ları temel öğeleri aşağıdaki hello içerir:

- [**Olay üreticileri/yayımcıları**](event-hubs-features.md#event-publishers): tooan event hub'ı veri gönderen bir varlık. Olay AMQP 1.0 veya HTTPS üzerinden yayımlanır.
- [**Yakalama**](event-hubs-features.md#capture): bir Azure Blob storage hesabında depolamak ve toocapture olay hub'ın veri akış sağlar.
- [**Bölümler**](event-hubs-features.md#partitions): etkinleştirir, her tüketici tooonly okuma belirli alt ya da bölümü hello olay akışı.
- [**SAS belirteci**](event-hubs-features.md#sas-tokens): tanımlar ve hello olay yayımcısı kimliğini doğrular.
- [**Olay tüketicileri**](event-hubs-features.md#event-consumers): Bir olay hub'ından olay verilerini okuyan bir varlıktır. Olay tüketicileri AMQP 1.0 üzerinden bağlanır. 
- [**Tüketici grupları**](event-hubs-features.md#consumer-groups): hello olay akışının ayrı bir görünümle uygulama, bu tüketicileri tooact bağımsız olarak etkinleştirme her birden çok sağlar.
- [**İşleme birimleri**](event-hubs-features.md#capacity): Önceden satın alınan kapasite birimleridir. Tek bir bölüm en fazla 1 işleme biriminden oluşan ölçeğe sahiptir.

Bunlar ve diğer Event Hubs özellikleri hakkında teknik ayrıntılar için bkz: Merhaba [olay hub'ları özelliklere genel bakış](event-hubs-features.md). 

## <a name="next-steps"></a>Sonraki adımlar

Event Hubs ayrıntılı fiyatlandırma bilgileri için bkz. [Event Hubs Fiyatlandırması](https://azure.microsoft.com/pricing/details/event-hubs/).

Event Hubs hakkında daha fazla bilgi için bağlantılar aşağıdaki hello ziyaret edin:

* [Event Hubs öğreticisi](event-hubs-dotnet-standard-getstarted-send.md) ile çalışmaya başlayın
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)
* [Event Hubs kullanan örnek uygulamalar](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

