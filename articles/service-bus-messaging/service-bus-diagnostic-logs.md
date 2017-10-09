---
title: "aaaAzure Service Bus tanılama günlüklerini | Microsoft Docs"
description: "Bilgi nasıl tooset azure'da hizmet veri yolu için tanılama günlüklerini ayarlama."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a>Hizmet veri yolu tanılama günlükleri

Azure hizmet veri yolu için iki tür günlükleri görüntüleyebilirsiniz:
* **[Etkinlik günlükleri](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Bu günlükler bir iş üzerinde gerçekleştirilen işlemler hakkında bilgi içerir. Merhaba günlükleri her zaman etkindir.
* **[Tanılama günlüklerini](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. İçinde bir işi olur daha zengin hakkında bilgi için tanılama günlüklerini yapılandırabilirsiniz. Tanılama güncelleştirmeleri ve hello iş çalışırken oluşan etkinlikler dahil olmak üzere hello iş silinene kadar hello iş oluşturulur hello zamandan kapak etkinlikleri günlüğe kaydeder.

## <a name="turn-on-diagnostic-logs"></a>Tanılama günlüklerini Aç

Tanılama günlükleri, varsayılan olarak devre dışıdır. tooenable tanılama günlükleri, hello aşağıdaki adımları gerçekleştirin:

1.  Merhaba, [Azure portal](https://portal.azure.com)altında **izleme + Yönetim**, tıklatın **tanılama günlükleri**.

    ![Dikey gezinti toodiagnostic günlükleri](./media/service-bus-diagnostic-logs/image1.png)

2. Toomonitor istediğiniz hello kaynak'ı tıklatın.  

3.  Tıklatın **tanılamayı açın**.

    ![Tanılama günlüklerini Aç](./media/service-bus-diagnostic-logs/image2.png)

4.  İçin **durum**, tıklatın **üzerinde**.

    ![Tanılama günlüklerini durumunu değiştirme](./media/service-bus-diagnostic-logs/image3.png)

5.  İstediğiniz kümesi hello arşiv hedef; Örneğin, bir depolama hesabı, bir olay hub'ı veya Azure günlük analizi.

6.  Merhaba yeni tanılama ayarları kaydedin.

Yeni ayarları yaklaşık 10 dakika içinde etkinleşir. Bundan sonra günlükler hello üzerinde yapılandırılmış hello arşivleme hedef görünür **tanılama günlükleri** dikey.

Merhaba tanılama yapılandırma hakkında daha fazla bilgi için bkz: [Azure tanılama günlükleri'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-schema"></a>Tanılama günlüklerini şeması

Tüm günlükler JavaScript nesne gösterimi (JSON) biçiminde depolanır. Her giriş bölümden hello açıklanan hello biçimini kullanan alanlarına sahiptir.

## <a name="operational-logs-schema"></a>İşlem günlükleri şeması

Hello günlüklerini **OperationalLogs** kategori yakalama ne Service Bus işlemleri sırasında olur. Özellikle, bu günlükler hello işlem türü, kuyruk oluşturma, kullanılan, kaynakları dahil yakalamak ve hello işlemin durumunu hello.

İşlem günlüğü JSON dizeler, aşağıdaki tablonun hello listelenen öğeleri şunları içerir:

Ad | Açıklama
------- | -------
Etkinlik Kimliği | İzleme için kullanılan iç kimliği
EventName | İşlem adı           
resourceId | Azure Resource Manager kaynak kimliği
SubscriptionId | Abonelik Kimliği
EventTimeString | İşlem süresi
EventProperties | İşlem özellikleri
Durum | İşlem durumu
Çağıran | Arayan işlemi (Azure portalı veya yönetim istemcisi)
category | OperationalLogs

Bir işlem günlüğü JSON dize örneği şöyledir:

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Sonraki adımlar

Service Bus hakkında daha fazla bağlantılar toolearn aşağıdaki hello ziyaret edin:

* [Giriş tooService veri yolu](service-bus-messaging-overview.md)
* [Service Bus ile çalışmaya başlama](service-bus-dotnet-get-started-with-queues.md)
