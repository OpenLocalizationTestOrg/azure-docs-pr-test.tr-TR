---
title: "aaaAzure Service Bus Premium ve standart Mesajlaşma hizmeti fiyatlandırma katmanlarına genel bakış | Microsoft Docs"
description: "Service Bus Premium ve Standart Mesajlaşma katmanları"
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a>Service Bus Premium ve Standart Mesajlaşma katmanları

Kuyruklar ve konu başlıkları gibi varlıkları içeren Service Bus Mesajlaşma, kuruluşun mesajlaşma işlevlerini bulut ölçeğinde zengin yayımla-abone ol semantiği ile birleştirir. Service Bus Mesajlaşma hizmeti hello iletişimin temel öğesi olarak birçok gelişmiş bulut çözümü için kullanılır.

Merhaba *Premium* Service Bus Mesajlaşma katmanı adresleri yaygın müşteri isteklerini ölçek, performans ve görev açısından kritik uygulamalar için kullanılabilirlik karşılar. Merhaba özellik kümeleri neredeyse aynı olsa da, Service Bus Mesajlaşma hizmetinin bu iki katmanı tasarlanmış tooserve farklı kullanım örnekleridir.

Aşağıdaki tablonun hello bazı üst düzey farklılıklar vurgulanmıştır.

| Premium | Standart |
| --- | --- |
| Yüksek verimlilik |Değişken işleme |
| Tahmin edilebilir performans |Değişken gecikme süresi |
| Sabit fiyatlandırma |Kullandıkça Öde değişken fiyatlandırması |
| Yukarı ve aşağı özelliği tooscale iş yükü |Yok |
| İleti boyutu too1 MB ayarlama |İleti boyutu too256 KB ayarlama |

**Service Bus Premium Mesajlaşma** kaynak yalıtımına hello CPU ve bellek düzeyinde sunar, böylece her müşterinin iş yükü yalıtımlı şekilde çalışır. Bu kaynak kapsayıcısı *mesajlaşma birimi* olarak adlandırılır. Her premium ad alanı, en az bir mesajlaşma birimi için ayrılmıştır. Her Service Bus Premium ad alanı için 1, 2 veya 4 mesajlaşma birimi satın alabilirsiniz. Tek iş yükü veya varlık birden çok Mesajlaşma birimine yayılabilir ve faturalandırma 24 saatlik veya günlük oran fiyatlarında içinde olsa da hello Mesajlaşma birimlerinin sayısı gerçekleştirilse değiştirilebilir. Merhaba, Service Bus tabanlı çözümünüz için tahmin edilebilir ve tekrarlanabilir bir performans sonucudur.

Daha tahmin edilebilir ve kullanılabilir olmasının yanı sıra bu performans, daha hızlıdır. Service Bus Premium Mesajlaşma derlemeler sunulan hello depolama motorunda [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/). Premium Mesajlaşma sayesinde, en yüksek performans hello standart katmanı ile daha hızlıdır.

## <a name="premium-messaging-technical-differences"></a>Premium Mesajlaşmanın teknik farklılıkları

Merhaba aşağıdaki bölümlerde Premium ve standart Mesajlaşma katmanları arasındaki bazı farklar açıklanmaktadır.

### <a name="partitioned-queues-and-topics"></a>Bölümlenmiş kuyruklar ve konular

Bölümlenmiş kuyruklar ve konular, Premium Mesajlaşma hizmetinde desteklenir; aslında bu varlıklar her zaman bölümlenmiş durumdadır (ve devre dışı bırakılamaz). Ancak, Premium bölümlenmiş sıraları ve konuları hello çalışmıyor olarak aynı şekilde hello Service Bus Mesajlaşma hizmetinin standart ve temel katmanlarında. Premium Mesajlaşma kullanmıyorsa SQL'in veri deposu olarak ve artık paylaşılan platforma ilişkili olası kaynak rekabet hello. Sonuç olarak, bölümleme gerekli tooimprove performans değil. Ayrıca, hello bölüm sayısı 16 bölümlerinde too2 bölümlerinde standart Mesajlaşma Premium değiştirildi. İki bölümlemeye sahip olmak kullanılabilirliği sağlar ve hello Premium çalışma zamanı ortamı için daha uygun bir sayıdır. 

Merhaba boyutuna sahip bir varlık belirttiğinizde, Premium, Mesajlaşma ile [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), boyutu eşit hello 2 bölümleri arasında aksine bölünen olduğunu [standart bölümlenmiş varlıkları](service-bus-partitioning.md#standard) hangi hello içinde Merhaba belirtilen boyutu 16 kez toplam boyutudur. 

Bölümleme hakkında daha fazla bilgi için bkz. [Bölümlenmiş kuyruklar ve konular](service-bus-partitioning.md).

### <a name="express-entities"></a>İfade varlıkları

Premium mesajlaşma tamamen yalıtılmış bir çalışma zamanı ortamında çalıştığından Premium ad alanlarında ifade varlıkları desteklenmez. Merhaba hello express özelliği hakkında daha fazla bilgi için bkz: [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) özelliği.

İsteğe bağlı olarak standart Mesajlaşma ve istediğiniz tooport altında toohello Premium katmanı çalışan kodu varsa, emin hello olun [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) özelliği çok ayarlanmış**false** (Merhaba varsayılan değer).

## <a name="get-started-with-premium-messaging"></a>Premium Mesajlaşmayı kullanmaya başlama

Premium Mesajlaşma ile çalışmaya başlama basittir ve standart Mesajlaşma benzer toothat hello işlemidir. [Ad alanı oluşturarak](service-bus-create-namespace-portal.md) başlayın. **Fiyatlandırma katmanı** için **Premium**'u seçtiğinizden emin olun.

![create-premium-namespace][create-premium-namespace]

Ayrıca [Azure Resource Manager şablonlarını kullanarak premium ad alanları](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/) oluşturabilirsiniz.


## <a name="next-steps"></a>Sonraki adımlar

Service Bus Mesajlaşma hizmeti, hakkında daha fazla toolearn aşağıdaki konularda hello bakın.

* [Azure Service Bus Mesajlaşma hizmetine giriş (blog gönderisi)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Azure Service Bus Premium Mesajlaşma hizmetine giriş (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Service Bus Mesajlaşma hizmetine genel bakış](service-bus-messaging-overview.md)
* [Nasıl toouse Service Bus kuyrukları](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
