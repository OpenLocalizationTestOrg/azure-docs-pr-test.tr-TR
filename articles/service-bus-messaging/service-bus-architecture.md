---
title: "aaaAzure Service Bus ileti mimarisine genel bakış işleme | Microsoft Docs"
description: "Azure Service Bus Hello ileti işleme mimarisini açıklar."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: f7606e40cdf6db3797a0db2de9365453ff2a158e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-architecture"></a>Service Bus mimarisi
Bu makalede Azure hizmet veri yolu hello ileti işleme mimarisini açıklar.

## <a name="service-bus-scale-units"></a>Service Bus ölçek birimleri
Service Bus, *ölçek birimleri* tarafından düzenlenir. Bir ölçek birimi dağıtım birimidir ve tüm bileşenler gerekli çalışma hello hizmeti içerir. Her bölge, bir veya daha fazla Service Bus ölçek birimi dağıtır.

Bir hizmet veri yolu ad alanı eşlenen tooa ölçek birimidir. Hizmet veri yolu varlıkları (kuyruklar, konular, abonelikler) tüm türleri Hello ölçek birimi işler. Service Bus ölçek birimi bileşenleri aşağıdaki Merhaba oluşur:

* **Ağ geçidi düğümleri kümesi.** Ağ geçidi düğümleri, gelen isteklerin kimliklerini doğrular. Her ağ geçidi düğümünün genel bir IP adresi vardır.
* **Mesajlaşma aracısı düğümleri kümesi.** Mesajlaşma aracısı düğümleri, mesajlaşma varlıkları ile ilgili istekleri işler.
* **Bir ağ geçidi deposu.** Merhaba ağ geçidi deposu, bu ölçek biriminde tanımlanan her varlık için hello verileri tutar. Hello ağ geçidi deposu, SQL Azure veritabanının üst kısmında uygulanır.
* **Birden çok mesajlaşma deposu.** Mesajlaşma depoları Merhaba iletileri tüm sıraları, konuları ve Abonelikleri, bu ölçek biriminde tanımlanan tutun. Ayrıca, tüm abonelik verilerini de içerir. Sürece [Mesajlaşma varlıkları bölümleme](service-bus-partitioning.md) olduğundan, kuyruk veya konu eşlenen tooone Mesajlaşma deposu etkindir. Abonelikleri hello depolanan olarak, üst konu başlıklarıyla aynı Mesajlaşma deposu. Hizmet veri yolu dışında [Premium Mesajlaşma](service-bus-premium-messaging.md), hello Mesajlaşma depoları, SQL Azure veritabanının üst kısmında uygulanır.

## <a name="containers"></a>Kapsayıcılar
Her mesajlaşma varlığı, belirli bir kapsayıcıya atanır. Bir kapsayıcı tüm ilgili verileri bu kapsayıcı için tam olarak bir Mesajlaşma deposu toostore kullanan mantıksal bir yapıdır. Her kapsayıcı tooa Mesajlaşma Aracısı düğümüne atanır. Genellikle, mesajlaşma aracısı düğümlerinden daha fazla sayıda kapsayıcı vardır. Bu nedenle, her mesajlaşma aracısı düğümü birden çok kapsayıcı yükler. Merhaba kapsayıcılara tooa Mesajlaşma Aracısı düğümü dağıtımını tüm Mesajlaşma Aracısı düğümlerine eşit olarak yüklenecek şekilde düzenlenmiştir. Merhaba yük düzeni değişiklikler (örneğin, biri çok meşgul Merhaba kapsayıcılara alır) veya bir Mesajlaşma Aracısı düğümü geçici olarak kullanılamaz hale gelmesi durumunda hello gelirse kapsayıcılar Mesajlaşma Aracısı düğümleri hello arasında dağıtılır.

## <a name="processing-of-incoming-messaging-requests"></a>Gelen mesajlaşma isteklerinin işlenmesi
Bir istemci isteği tooService Bus gönderdiğinde, hello Azure yük dengeleyici hello ağ geçidi düğümleri tooany yönlendirir. Merhaba ağ geçidi düğümü hello isteği yetkilendirir. Hello isteği bir Mesajlaşma varlığıyla (kuyruk, konu, abonelik) ilgiliyse hello ağ geçidi düğümü hello ağ geçidi deposunda hello varlığı arar ve varlığın hangi Mesajlaşma deposu hello bulunduğunu belirler. Ardından hangi Mesajlaşma Aracısı düğümü şu anda bu kapsayıcıya hizmet veren ve mesajlaşma Aracısı düğümü hello isteği toothat gönderir yukarı görünüyor. Mesajlaşma Aracısı düğümü hello hello isteği işler ve hello hello kapsayıcı deposundaki varlık durumunu güncelleştirir. Aracısı düğümü ardından Mesajlaşma hello uygun yanıtı geri toohello istemci o verilen hello özgün isteği gönderen hello yanıt geri toohello ağ geçidi düğümü, gönderir.

![Gelen Mesajlaşma İsteklerinin İşlenmesi](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>Sonraki adımlar
Service Bus mimarisine genel bakış okuduğunuza göre daha fazla bilgi için bağlantılar aşağıdaki hello ziyaret edin:

* [Service Bus mesajlaşma hizmetine genel bakış](service-bus-messaging-overview.md)
* [Service Bus ile ilgili temel bilgiler](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus kuyruklarını kullanan kuyruğa alınan mesajlaşma çözümü](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)


