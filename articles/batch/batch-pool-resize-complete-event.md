---
title: "aaa \"Azure Batch havuzu yeniden boyutlandırma complete olayını | Microsoft Docs\""
description: "Batch havuzundaki başvurusunu complete olayını yeniden boyutlandırın."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a>Havuzu yeniden boyutlandırma complete olayı

 Havuzu yeniden boyutlandırma tamamlandı veya başarısız olduğunda bu olay yayınlanır.

 Merhaba aşağıdaki örnek boyutu artar ve başarıyla tamamlandı bir havuz için havuzu yeniden boyutlandırma complete olayını hello gövdesi gösterir.

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "hello operation succeeded"
}
```

|Öğesi|Tür|Notlar|
|-------------|----------|-----------|
|id|Dize|Merhaba havuzun Hello kimliği.|
|nodeDeallocationOption|Dize|Merhaba havuz boyutunun küçülmesi durumunda ne zaman düğümleri hello havuzdan kaldırılabilir belirtir.<br /><br /> Olası değerler şunlardır:<br /><br /> **requeue** – yürütülen görevleri sonlandırır ve onları yeniden kuyruğa alır. Merhaba iş etkinleştirildiğinde hello görevler yeniden yürütülür. Görevler sonlandırıldı hemen düğümleri kaldırın.<br /><br /> **sonlandırma** – çalışan görevlerin sonlandır. Merhaba görevleri yeniden çalışmaz. Görevler sonlandırıldı hemen düğümleri kaldırın.<br /><br /> **net_offline_option** – çalışmakta olan görevleri toocomplete izin ver. Beklenirken hiç yeni görev zamanlamaz. Tüm görevler tamamlandığında düğümleri kaldırın.<br /><br /> **Retaineddata** - çalışmakta olan görevleri toocomplete izin verin ve sonra tüm veri bekletme dönemleri tooexpire görev için bekleyin. Beklenirken hiç yeni görev zamanlamaz. Tüm görev bekletme süreleri dolduğunda düğümleri kaldırın.<br /><br /> requeue Hello varsayılan değerdir.<br /><br /> Hello havuz boyutunun artırılması sonra hello değeri çok ayarlanır**geçersiz**.|
|currentDedicated|Int32|işlem düğümü sayısını Hello toohello havuzuna atanmış.|
|targetDedicated|Int32|Merhaba hello havuzu için istenen işlem düğümleri sayısı.|
|enableAutoScale|bool|Merhaba havuz boyutu otomatik olarak zaman içinde ayarlar olup olmadığını belirtir.|
|isAutoPool|bool|Bir işin AutoPool mekanizması Hello havuzu oluşturulup oluşturulmadığını belirtir.|
|startTime|Tarih saat|Merhaba havuzu yeniden boyutlandırma hello zaman başlatıldı.|
|endTime|Tarih saat|Merhaba hello havuzu yeniden boyutlandırma süresi tamamlandı.|
|ResultCode|Dize|Merhaba Hello sonucunu yeniden boyutlandırın.|
|resultMessage|Dize|Merhaba yeniden boyutlandırma hatası hello sonuç hello ayrıntılarını içerir.<br /><br /> Başarıyla Hello yeniden boyutlandırmak, işlemi başarılı oldu hello durumları tamamlandı.|
