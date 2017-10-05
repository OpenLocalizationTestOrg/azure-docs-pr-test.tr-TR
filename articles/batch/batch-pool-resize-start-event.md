---
title: "Azure Batch havuzu yeniden boyutlandır olayını Başlat | Microsoft Docs"
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
ms.openlocfilehash: 826cd984d26b923ba38562e05a2e75c399be9121
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-start-event"></a>Havuzu yeniden boyutlandırma başlangıç olayı

 Bir havuzu yeniden boyutlandırma başlatıldığında bu olay yayınlanır. Zaman uyumsuz bir olay havuzu yeniden boyutlandırma olduğuna göre yeniden boyutlandırma işlemi tamamlandıktan sonra yayınlaması için havuzu yeniden boyutlandırma complete olayını bekleyebilirsiniz.

 Aşağıdaki örnek, bir havuz 0'dan 2 düğümlerine el ile bir yeniden boyutlandırma ile yeniden boyutlandırma için havuzu yeniden boyutlandırma başlangıç olayı gövdesi gösterir.

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
|poolId|Dize|Havuzun kimliği.|
|nodeDeallocationOption|Dize|Havuz boyutunun küçülmesi durumunda ne zaman düğüm havuzdan kaldırılabilir belirtir.<br /><br /> Olası değerler şunlardır:<br /><br /> **requeue** – yürütülen görevleri sonlandırır ve onları yeniden kuyruğa alır. İş etkinleştirildiğinde görevler yeniden yürütülür. Görevler sonlandırıldı hemen düğümleri kaldırın.<br /><br /> **sonlandırma** – çalışan görevlerin sonlandır. Görevler yeniden çalışmaz. Görevler sonlandırıldı hemen düğümleri kaldırın.<br /><br /> **net_offline_option** – tamamlamak için izin şu anda çalışan görevler. Beklenirken hiç yeni görev zamanlamaz. Tüm görevler tamamlandığında düğümleri kaldırın.<br /><br /> **Retaineddata** -izin şu anda çalışan görevlerin tamamlayın ve ardından tüm veri saklama sürelerini süresi dolmak üzere görev için bekleyin. Beklenirken hiç yeni görev zamanlamaz. Tüm görev bekletme süreleri dolduğunda düğümleri kaldırın.<br /><br /> Requeue varsayılan değerdir.<br /><br /> Havuz boyutunun artırılması sonra değer kümesine **geçersiz**.|
|currentDedicated|Int32|Şu anda havuzuna atanmış işlem düğümleri sayısı.|
|targetDedicated|Int32|Havuzu için istenen işlem düğümleri sayısı.|
|enableAutoScale|bool|Havuz boyutu otomatik olarak zaman içinde ayarlar olup olmadığını belirtir.|
|isAutoPool|bool|Speficies havuzu bir işin AutoPool mekanizması olup oluşturuldu.|
