---
title: "aaa \"Azure Batch havuzu Sil Tamam olayını | Microsoft Docs\""
description: "Batch havuzundaki başvurusunu complete olayını silin."
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a>Havuz Sil Tamam olayını

 Bir havuzu silme işlemi tamamlandığında bu olay yayınlanır.

 Merhaba aşağıdaki örnek bir havuzu Sil Tamam olayını hello gövdesi gösterir.

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|Öğesi|Tür|Notlar|
|-------------|----------|-----------|
|id|Dize|Merhaba havuzun Hello kimliği.|
|startTime|Tarih saat|Merhaba havuzunu silme hello zaman başlatıldı.|
|endTime|Tarih saat|Merhaba hello havuzunu silme süresi tamamlandı.|

## <a name="remarks"></a>Açıklamalar
Durumları ve havuzu yeniden boyutlandırma işlemi için hata kodları hakkında daha fazla bilgi için bkz: [bir hesaptan bir havuzunu silme](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).