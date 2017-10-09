---
title: "aaaAzure olay hub'ları tanılama günlüklerini | Microsoft Docs"
description: "Bilgi nasıl tooset Azure event hubs için tanılama günlükleri ayarlama."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a>Olay hub'ları tanılama günlükleri

Azure Event Hubs için iki tür günlükleri görüntüleyebilirsiniz:
* **[Etkinlik günlükleri](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Bu günlükleri bir iş üzerinde gerçekleştirilen işlemler hakkında bilgi vardır. Merhaba günlükleri her zaman etkindir.
* **[Tanılama günlüklerini](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. Bir işin gerçekleşen daha zengin bir görünüm her şeyin için tanılama günlükleri yapılandırabilirsiniz. Tanılama güncelleştirmeleri ve hello iş çalışırken oluşan etkinlikler dahil olmak üzere hello iş silinene kadar hello iş oluşturulur hello zamandan kapak etkinlikleri günlüğe kaydeder.

## <a name="turn-on-diagnostic-logs"></a>Tanılama günlüklerini Aç
Tanılama günlükleri, varsayılan olarak devre dışıdır. tooenable tanılama günlükleri:

1.  Merhaba, [Azure portal](https://portal.azure.com)altında **izleme + Yönetim**, tıklatın **tanılama günlükleri**.

    ![Dikey gezinti toodiagnostic günlükleri](./media/event-hubs-diagnostic-logs/image1.png)

2.  Toomonitor istediğiniz hello kaynak'ı tıklatın.

3.  Tıklatın **tanılamayı açın**.

    ![Tanılama günlüklerini Aç](./media/event-hubs-diagnostic-logs/image2.png)

4.  İçin **durum**, tıklatın **üzerinde**.

    ![Tanılama günlüklerini hello durumunu değiştir](./media/event-hubs-diagnostic-logs/image3.png)

5.  İstediğiniz kümesi hello arşiv hedef; Örneğin, bir depolama hesabı, bir olay hub'ı veya Azure günlük analizi.

6.  Merhaba yeni tanılama ayarları kaydedin.

Yeni ayarları yaklaşık 10 dakika içinde etkinleşir. Bundan sonra günlükler hello üzerinde yapılandırılmış hello arşivleme hedef görünür **tanılama günlükleri** dikey.

Merhaba tanılama yapılandırma hakkında daha fazla bilgi için bkz: [Azure tanılama günlükleri'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-categories"></a>Tanılama günlüklerini kategorileri
Olay hub'ları iki kategorileri için tanılama günlükleri yakalar:

* **ArchiveLogs**: günlükleri ilgili tooEvent hub arşivler özellikle, ilgili tooarchive hataları günlüğe kaydeder.
* **OperationalLogs**: olay hub'ları işlemleri sırasında özellikle neler hakkında bilgi hello işlem türü, olay hub'ı oluşturma, kullanılan, kaynakları dahil ve hello hello işlem durumu.

## <a name="diagnostic-logs-schema"></a>Tanılama günlüklerini şeması
Tüm günlükler JavaScript nesne gösterimi (JSON) biçiminde depolanır. Her giriş hello aşağıdaki bölümlerde açıklanan hello biçimini kullanan alanlarına sahiptir.

### <a name="archive-logs-schema"></a>Arşiv günlükleri şeması

Arşiv günlük JSON dizeler, aşağıdaki tablonun hello listelenen öğeleri şunları içerir:

Ad | Açıklama
------- | -------
Görevadı | Başarısız hello görev açıklaması.
Etkinlik Kimliği | İzleme için kullanılan iç kimliği.
İzleme kodu | İzleme için kullanılan iç kimliği.
resourceId | Azure Resource Manager kaynak kimliği
EventHub | (Ad alanı adı dahildir) olay hub'ı tam adı.
PartitionID | Olay hub'ı üzerine yazılan bir bölüm.
archiveStep | ArchiveFlushWriter
startTime | Hata başlangıç saati.
hataları | Kaç kez başarısız oldu.
durationInSeconds | Hatanın süresi.
İleti | Hata iletisi.
category | ArchiveLogs

Merhaba aşağıdaki kod, bir arşiv günlüğü JSON dizesi örneğidir:

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a>İşlem günlükleri şeması

İşlem günlüğü JSON dizeler, aşağıdaki tablonun hello listelenen öğeleri şunları içerir:

Ad | Açıklama
------- | -------
Etkinlik Kimliği | İç kimlik tootrack amacı kullanılır.
EventName | İşlem adı.  
resourceId | Azure Resource Manager kaynak kimliği
SubscriptionId | Abonelik kimliği
EventTimeString | İşlem süresi.
EventProperties | İşlem özellikleri.
Durum | İşlem durumu.
Çağıran | İşlemi (Azure portalı veya yönetim istemcisi) çağırıcı.
category | OperationalLogs

Merhaba aşağıdaki kod, bir işlem günlüğü JSON dizesi örneğidir:

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooEvent hub'lar](event-hubs-what-is-event-hubs.md)
* [Event Hubs API’sine genel bakış](event-hubs-api-overview.md)
* [Event Hubs kullanmaya başlayın](event-hubs-csharp-ephcs-getstarted.md)
