---
title: "aaaEnable toplu olayların - Azure günlüğe tanılama | Microsoft Docs"
description: "Kayıt ve havuzları ve görevler gibi Azure Batch hesabı kaynaklarına için tanılama günlük olayları analiz edin."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>Tanılama değerlendirme ve toplu çözümlerini izleme olayları günlüğe kaydedin

Çok sayıda Azure hizmetleriyle gibi belirli kaynaklara sırasında hello kaynak ömrü hello günlüğü olaylarını hello Batch hizmeti yayar. Azure Batch tanılama günlüklerini toorecord olayları havuzları ve görevler gibi kaynaklar için etkinleştirin ve ardından hello günlükleri tanılama değerlendirme ve izleme için kullanın. Havuzu gibi olaylar oluşturmak, havuzu silme, görev Başlat, görev tamamlandı ve diğerleri toplu tanılama günlüklerine eklenir.

> [!NOTE]
> Batch hesabı kaynaklarını kendileri için olayları günlüğe kaydetmeyi bu makalede ele, değil iş ve görev çıktı verileri. Merhaba çıktı verilerini işler ve görevler depolama hakkında daha fazla bilgi için bkz [kalıcı Azure Batch iş ve Görev çıkış](batch-task-output.md).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
* [Azure toplu işlem hesabı](batch-account-create-portal.md)
* [Azure Depolama hesabınız](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  toopersist toplu tanılama günlükleri, Azure hello günlükleri depolayacağınız bir Azure Storage hesabı oluşturmanız gerekir. Bu depolama hesabı belirtin olduğunda, [tanılama günlük kaydını etkinleştir](#enable-diagnostic-logging) Batch hesabınıza. Merhaba, belirttiğiniz günlük toplama etkinleştirdiğinizde depolama hesabı olan değil hello aynı bağlantılı depolama hesabı başvurulan tooin hello [uygulama paketleri](batch-application-packages.md) ve [görev çıktısını kalıcılığı](batch-task-output.md) makaleleri.
  
  > [!WARNING]
  > Olduğunuz **ücret** Azure depolama hesabınızda depolanan hello veriler. Bu makalede açıklanan hello tanılama günlükleri içerir. Bu tasarlarken göz önünde bulundurmanız, [günlük Bekletme İlkesi](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).
  > 
  > 

## <a name="enable-diagnostic-logging"></a>Tanılama günlüğünü etkinleştirme
Tanılama günlük varsayılan olarak, toplu işlem hesabı için etkin değil. Açıkça toomonitor istediğiniz her toplu işlem hesabı için tanılama günlük kaydını etkinleştirmeniz gerekir:

[Nasıl Tanılama günlüklerini tooenable koleksiyonu](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

Merhaba tam okumanızı öneririz [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makale toogain yalnızca nasıl tooenable günlüğe kaydetme, ancak hello kategorileri oturum bir anlamak çeşitli Azure hizmetlerine hello tarafından desteklenir. Örneğin, Azure Batch tek bir günlük kategori şu anda destekler: **hizmeti günlükleri**.

## <a name="service-logs"></a>Hizmet Günlükleri
Azure Batch hizmeti günlükleri toplu kaynak havuzu ya da görev gibi hello ömrü sırasında hello Azure Batch hizmeti tarafından oluşturulan olayları içerir. Batch tarafından gösterilen her olay belirtilen hello depolanan JSON biçiminde depolama hesabı. Örneğin, bu bir örnek hello gövdesi **havuzu oluşturma olayı**:

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

Her olay gövdesi bir .json bulunduğu hello dosyasında belirtilen Azure depolama hesabı. Tooaccess hello günlükleri doğrudan istiyorsanız, tooreview hello isteyebilir [tanılama günlüklerini şema hello depolama hesabındaki](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).

## <a name="service-log-events"></a>Hizmeti oturum açma olayları
Merhaba Batch hizmeti şu anda hizmeti oturum açma olayları aşağıdaki hello yayar. Bu makalede son güncelleştirmesinden bu yana ek olaylar eklenmemiş olabilir beri bu liste geniş kapsamlı, olmayabilir.

| **Hizmeti oturum açma olayları** |
| --- |
| [Havuz oluşturma][pool_create] |
| [Havuzu silme Başlat][pool_delete_start] |
| [Havuzu silme tamamlandı][pool_delete_complete] |
| [Havuzu yeniden boyutlandırma Başlat][pool_resize_start] |
| [Tam havuzu yeniden boyutlandırma][pool_resize_complete] |
| [Görev Başlat][task_start] |
| [Görev tamamlandı][task_complete] |
| [Görev başarısız][task_fail] |

## <a name="next-steps"></a>Sonraki adımlar
Toplama toostoring tanılama günlük olaylarında içinde bir Azure Storage hesabı, toplu işlem hizmeti oturum açma olayları tooan da sağlanabilir [Azure olay hub'ı](../event-hubs/event-hubs-what-is-event-hubs.md)ve çok gönderme[Azure günlük analizi](../log-analytics/log-analytics-overview.md).

* [Akış Azure tanılama günlükleri tooEvent hub'lar](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  Toplu iş Tanılama Olayları toohello yüksek düzeyde ölçeklenebilir bir veri alım, olay hub'ları akış. Olay hub'ları sonra dönüştürmek ve tüm gerçek zamanlı analiz sağlayıcısı kullanarak depolamak saniye başına milyonlarca olayı işleyebilen.
* [Günlük analizi kullanarak Azure tanılama günlüklerini çözümleme](../log-analytics/log-analytics-azure-storage.md)
  
  Tanılama günlüklerini tooLog buradan hello Operations Management Suite (OMS) Portalı'nda çözümlemek, veya Power BI veya Excel'den analiz için bunları dışarı aktarmak Analytics gönderin.

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
