---
title: "aaa \"Azure Batch havuzu yeniden boyutlandır olayını Başlat | Microsoft Docs\""
description: "Batch havuzu yeniden boyutlandırma için başvuru olay başlatın."
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a>Havuzu yeniden boyutlandırma başlangıç olayı

 Bir havuzu yeniden boyutlandırma başlatıldığında bu olay yayınlanır. Zaman uyumsuz bir olay Hello havuzu yeniden boyutlandırma olduğuna göre hello yeniden boyutlandırma sonra işlem yayılan bir havuzu yeniden boyutlandırma complete olayını toobe tamamlandıktan bekleyebilirsiniz.

 Aşağıdaki gösterildiği bir havuz 0 too2 düğümlerinden el ile yeniden boyutlandırma için havuzu yeniden boyutlandırma başlangıç olayı gövdesi hello örneğine hello yeniden boyutlandırın.

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|Öğesi|Tür|Notlar|
|-------------|----------|-----------|
|poolId|Dize|Merhaba havuzun Hello kimliği.|
|nodeDeallocationOption|Dize|Merhaba havuz boyutunun küçülmesi durumunda ne zaman düğümleri hello havuzdan kaldırılabilir belirtir.<br /><br /> Olası değerler şunlardır:<br /><br /> **requeue** – yürütülen görevleri sonlandırır ve onları yeniden kuyruğa alır. Merhaba iş etkinleştirildiğinde hello görevler yeniden yürütülür. Görevler sonlandırıldı hemen düğümleri kaldırın.<br /><br /> **sonlandırma** – çalışan görevlerin sonlandır. Merhaba görevleri yeniden çalışmaz. Görevler sonlandırıldı hemen düğümleri kaldırın.<br /><br /> **net_offline_option** – çalışmakta olan görevleri toocomplete izin ver. Beklenirken hiç yeni görev zamanlamaz. Tüm görevler tamamlandığında düğümleri kaldırın.<br /><br /> **Retaineddata** - çalışmakta olan görevleri toocomplete izin verin ve sonra tüm veri bekletme dönemleri tooexpire görev için bekleyin. Beklenirken hiç yeni görev zamanlamaz. Tüm görev bekletme süreleri dolduğunda düğümleri kaldırın.<br /><br /> requeue Hello varsayılan değerdir.<br /><br /> Hello havuz boyutunun artırılması sonra hello değeri çok ayarlanır**geçersiz**.|
|currentDedicated|Int32|işlem düğümü sayısını Hello toohello havuzuna atanmış.|
|targetDedicated|Int32|Merhaba hello havuzu için istenen işlem düğümleri sayısı.|
|enableAutoScale|bool|Merhaba havuz boyutu otomatik olarak zaman içinde ayarlar olup olmadığını belirtir.|
|isAutoPool|bool|Speficies hello havuzu bir işin AutoPool mekanizması olup oluşturuldu.|
